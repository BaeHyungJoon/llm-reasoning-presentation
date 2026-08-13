---
theme: default
title: LLM은 어떻게 더 잘 생각하게 되었나
info: |
  SSAFY AI 자기주도학습 발표
  Architecture Efficiency → RLHF → Reasoning RL → Agentic RL
class: technical-deck
transition: fade
drawings:
  persist: false
comark: true
duration: 35min
aspectRatio: 16/9
canvasWidth: 980
---

<div class="cover-slide">
  <div class="eyebrow">SSAFY AI 자기주도학습</div>
  <h1>LLM은 어떻게 더 잘<br><span class="gradient-text">생각하게 되었나</span></h1>
  <div class="cover-path">
    <span class="arch-text">Architecture Efficiency</span><b>→</b>
    <span class="rl-text">RLHF</span><b>→</b>
    <span class="rl-text">Reasoning RL</span><b>→</b>
    <span class="agency-text">Agentic RL</span>
  </div>
  <div class="cover-footer">발표자 · YYYY.MM.DD</div>
</div>

<!--
Goal: 구조·학습·추론의 세 축을 따라 LLM 지능의 발전을 조망한다.
Talk track: 이 발표는 한 모델의 이야기가 아닙니다. 다음 토큰 예측기가 추론하고, 검증하고, 수정하고, 도구를 쓰는 시스템으로 변한 과정을 따라갑니다.
Transition: 먼저 오늘 발표 전체를 관통하는 질문 하나로 시작하겠습니다.
Source: references/post_training/01_instructgpt_rlhf.pdf; references/post_training/03_openai_o1_system_card.pdf; references/agentic_rl/04_react_reasoning_and_acting.pdf
-->

---

# LLM은 어떻게 추론할 수 있게 되었을까?

<div class="takeaway">한 번의 예측에서 지시 수행·추론·행동으로 무엇이 달라졌을까?</div>

<EvolutionTimeline />

<SourceFooter source="InstructGPT; OpenAI o1 System Card; Search-R1; ReAct" slide="02" />

<!--
Goal: 특정 모델이 아니라 추론 능력 자체의 발전을 중심 질문으로 제시한다.
Talk track: 초기 LLM의 기본 목표는 다음 token 예측이었습니다. 지금 모델은 문제를 나누고 접근을 검토하며 필요하면 도구까지 씁니다. 그 변화는 어디에서 왔을까요?
Transition: 이 질문을 세 가지 축으로 나누면 전체 발전사가 선명해집니다.
Source: references/post_training/01_instructgpt_rlhf.pdf; references/post_training/03_openai_o1_system_card.pdf; references/agentic_rl/01_search_r1.pdf; references/agentic_rl/04_react_reasoning_and_acting.pdf
-->

---

# 세 가지 발전 축

<div class="takeaway">Reasoning은 하나의 기술이 아니라 세 축의 결합으로 발전했다.</div>

<ThreeAxes />

<SourceFooter source="Kimi K3 Technical Report; InstructGPT; OpenAI o1 System Card" slide="03" />

<!--
Goal: 발표 전체를 이해할 세 축의 개념 지도를 제공한다.
Talk track: Reasoning을 RL 하나로 설명하면 부족합니다. 긴 context를 처리할 구조, 사고 전략을 학습시키는 post-training, 실제 문제에서 계산을 쓰는 inference가 함께 발전했습니다.
Transition: 먼저 더 긴 생각을 감당하게 만든 구조적 변화부터 보겠습니다.
Source: references/architecture/08_kimi_k3_technical_report.pdf; references/post_training/01_instructgpt_rlhf.pdf; references/post_training/03_openai_o1_system_card.pdf
-->

---

# Transformer의 출발점: Attention

<div class="takeaway arch-text">Attention은 어떤 token의 정보를 참고할지 계산한다.</div>

<AttentionIntuition />

<SourceFooter source="Attention Is All You Need" slide="04" />

<!--
Goal: 이후 효율화 논의를 위해 attention의 직관만 환기한다.
Talk track: Transformer의 핵심은 token 관계를 동적으로 계산하는 attention입니다. 오늘은 Q/K/V 전체보다 모든 token 관계를 계산한다는 점에 집중합니다.
Transition: 문제는 context가 길어질수록 관계 계산이 빠르게 비싸진다는 것입니다.
Source: references/architecture/01_attention_is_all_you_need.pdf
-->

---

# Long Context 병목: Full Attention은 비싸다

<div class="takeaway">Sequence가 길어질수록 모든 token pair를 비교해야 한다.</div>

<AttentionCost />

<SourceFooter source="Attention Is All You Need; DeepSeek Sparse Attention" slide="05" />

<!--
Goal: 추론 시대에 architecture efficiency가 필요한 이유를 설명한다.
Talk track: Reasoning model은 긴 CoT뿐 아니라 문서, 검색 결과, tool observation을 오래 유지해야 합니다. Full attention은 sequence가 길어질수록 모든 token pair를 비교합니다.
Transition: 그래서 생성 중 계속 쌓이는 K/V를 줄이는 연구가 진행됩니다.
Source: references/architecture/01_attention_is_all_you_need.pdf; references/architecture/05_deepseek_v3_2_sparse_attention.pdf
-->

---

# KV 효율화: MHA → MQA/GQA → MLA

<div class="takeaway arch-text">오래 생각하려면 KV cache도 효율적이어야 한다.</div>

<AttentionEvolution />

<SourceFooter source="GQA; DeepSeek-V2; DeepSeek-V3 Technical Report" slide="06" />

<!--
Goal: KV-cache 효율화의 흐름을 직관적으로 보여준다.
Talk track: Autoregressive generation은 과거 token의 K/V를 cache합니다. Context와 reasoning이 길어지면 cache가 커지므로 MQA/GQA는 공유를, MLA는 압축을 활용합니다.
Transition: KV만 줄여도 충분하지 않습니다. 더 긴 context에서는 무엇을 볼 것인가 자체도 바뀝니다.
Source: references/architecture/02_gqa.pdf; references/architecture/03_deepseek_v2_mla_moe.pdf; references/architecture/04_deepseek_v3_technical_report.pdf
-->

---

# Long-context Architecture의 두 갈래

<div class="takeaway">긴 context 병목을 푸는 서로 다른 병렬 전략</div>

<SparseVsRecurrent />

<SourceFooter source="DeepSeek Sparse Attention; Kimi Linear" slide="07" />

<!--
Goal: sparse와 recurrent/linear 접근을 병렬 전략으로 구분한다.
Talk track: Sparse 계열은 과거 token을 유지하되 중요한 일부를 읽습니다. Recurrent/linear 계열은 과거 정보를 state에 압축합니다. 둘은 선후 관계가 아니라 병렬 해법입니다.
Transition: Kimi K3는 효율화 문제를 sequence뿐 아니라 depth와 width까지 확장합니다.
Source: references/architecture/05_deepseek_v3_2_sparse_attention.pdf; references/architecture/06_kimi_linear_kda.pdf
-->

---

# Kimi K3: Sequence × Depth × Width

<div class="takeaway arch-text">정보 흐름을 token · layer · expert 세 방향에서 재설계한다.</div>

<KimiK3Architecture />

<SourceFooter source="Kimi K3 Technical Report; Kimi Linear; Attention Residuals" slide="08" />
<!--
Goal: K3를 다축 정보 흐름 설계의 최신 architecture 사례로 소개한다.
Talk track: K3는 attention 하나의 개선으로 설명되지 않습니다. Sequence에서는 KDA와 MLA, depth에서는 AttnRes, width에서는 MoE로 정보 흐름을 효율화합니다.
Transition: 그렇다면 이런 구조가 모델에게 직접 생각하는 법을 가르친 걸까요?
Source: references/architecture/08_kimi_k3_technical_report.pdf; references/architecture/06_kimi_linear_kda.pdf; references/architecture/07_attention_residuals.pdf
-->

---

# Architecture가 만든 것은 ‘생각하는 기반’

<div class="takeaway"><span class="arch-text">Architecture</span> ≠ reasoning policy</div>

<ArchitectureFoundation />

<SourceFooter source="DeepSeek-V2; Kimi Linear; Kimi K3 Technical Report" slide="09" />

<!--
Goal: architecture와 reasoning training의 인과를 과장하지 않고 post-training으로 전환한다.
Talk track: MLA나 KDA가 reasoning을 직접 가르친 것은 아닙니다. 더 긴 context와 trajectory를 감당하는 계산 기반을 만듭니다. 이제 모델이 그 계산을 어떻게 사용할지 배워야 합니다.
Transition: 그 답을 찾으려면 GPT-3의 학습 목표부터 다시 봐야 합니다.
Source: references/architecture/03_deepseek_v2_mla_moe.pdf; references/architecture/06_kimi_linear_kda.pdf; references/architecture/08_kimi_k3_technical_report.pdf
-->

---

# 다음 token 예측 ≠ 사용자 의도

<div class="takeaway">자연스럽게 이어 쓰는 것과 사용자에게 유용하게 답하는 것은 다른 목표다.</div>

<PredictionVsIntent />

<SourceFooter source="InstructGPT" slide="10" />

<!--
Goal: post-training이 필요해진 이유를 설명한다.
Talk track: GPT-3의 기본 objective는 사용자 만족이 아닙니다. 자연스럽게 text를 이어 쓰는 것과 instruction에 정확히 답하는 것은 다른 목표입니다.
Transition: 가장 직접적인 해결책은 좋은 답변의 예시를 보여주는 것이었습니다.
Source: references/post_training/01_instructgpt_rlhf.pdf
-->

---

# SFT: 좋은 답변의 예시를 학습하다

<div class="takeaway rl-text">“이런 질문에는 이렇게 답하는 것이 좋다.”</div>

<SFTPipeline />

<SourceFooter source="InstructGPT — labeler-written demonstrations" slide="11" />

<!--
Goal: supervised instruction tuning을 소개한다.
Talk track: SFT는 사람이 작성한 demonstration으로 instruction-response behavior를 학습합니다. 하지만 모든 질문의 완벽한 답을 사람이 쓰는 것은 매우 비쌉니다.
Transition: 답을 직접 쓰는 대신 여러 답 중 더 좋은 답을 고르게 하면 어떨까요?
Source: references/post_training/01_instructgpt_rlhf.pdf
-->

---

# RLHF: 답을 쓰지 말고 비교한다

<div class="takeaway">완벽한 답을 만드는 대신 여러 답의 선호 순서를 학습한다.</div>

<PreferenceRanking />

<SourceFooter source="InstructGPT — ranked model outputs" slide="12" />

<!--
Goal: human preference data를 직관적으로 설명한다.
Talk track: 여러 답변을 비교하는 것은 완벽한 답을 직접 만드는 것보다 상대적으로 쉽습니다. 비교 데이터로 인간 선호를 학습하는 Reward Model을 만듭니다.
Transition: 이제 사람 대신 Reward Model이 반복적으로 점수를 줄 수 있습니다.
Source: references/post_training/01_instructgpt_rlhf.pdf
-->

---

# Reward Model + PPO

<div class="takeaway rl-text">좋은 방향으로 움직이되 한 번에 너무 멀리 점프하지 않는다.</div>

<RLHFPipeline />

<SourceFooter source="InstructGPT; DeepSeekMath PPO preliminaries" slide="13" />

<!--
Goal: RLHF optimization loop를 high level로 설명한다.
Talk track: Reward Model은 선호될 답에 더 높은 score를 줍니다. PPO는 reward를 높이는 방향으로 policy를 업데이트하고 기존 모델과 너무 멀어지는 것을 제한합니다.
Transition: GPT-4 시대에는 post-training 신호가 사람의 선호 하나보다 훨씬 다양해집니다.
Source: references/post_training/01_instructgpt_rlhf.pdf; references/reasoning_rl/01_deepseekmath_grpo.pdf
-->

---

# GPT-4: Post-training Feedback이 다양해진다

<div class="takeaway">모델의 행동을 다듬는 신호와 안전 검증이 하나의 ranking loop를 넘어선다.</div>

<FeedbackSystem />

<SourceFooter source="GPT-4 System Card — feedback, safety fine-tuning, red teaming, testing, mitigations" slide="14" />

<!--
Goal: post-training이 더 풍부한 feedback system으로 확장됨을 보여준다.
Talk track: GPT-4 System Card는 human feedback 외에도 safety fine-tuning, prior-use data, classifiers, expert red teaming, adversarial testing과 system-level mitigation을 함께 설명합니다. 여기서는 이를 더 넓어진 post-training·deployment preparation으로 봅니다.
Transition: 하지만 중심 질문은 여전히 어떤 답변이 좋은가였습니다. Reasoning model에서는 질문이 달라집니다.
Source: references/post_training/02_gpt4_system_card.pdf
-->

---

# 전환점: 좋은 답변 → 좋은 사고 과정

<div class="takeaway">Reward의 초점이 답변 품질에서 문제 해결 behavior로 이동한다.</div>

<ResponseVsReasoning />

<SourceFooter source="InstructGPT; OpenAI o1 System Card; DeepSeek-R1 Technical Report" slide="15" />

<!--
Goal: 발표의 중심 전환인 response optimization에서 reasoning optimization으로의 이동을 설명한다.
Talk track: RLHF는 response behavior를 정렬하는 데 큰 역할을 했습니다. Reasoning model에서는 문제 분해, 검증, 수정 같은 문제 해결 behavior 자체를 강화하려는 방향이 중요해집니다.
Transition: 이 전환을 대표적으로 보여준 모델이 o1입니다.
Source: references/post_training/01_instructgpt_rlhf.pdf; references/post_training/03_openai_o1_system_card.pdf; references/reasoning_rl/02_deepseek_r1.pdf
-->

---

# o1: RL로 사고 전략을 강화하다

<div class="takeaway rl-text">Large-scale RL + productive use of reasoning</div>

<ReasoningLoop />

<SourceFooter source="OpenAI o1 System Card (2024) — optimizer and reward formula are undisclosed" slide="16" />
<!--
Goal: 공개된 범위 안에서 reasoning-oriented RL을 소개한다.
Talk track: OpenAI가 공개한 핵심은 large-scale RL로 chain-of-thought를 생산적으로 사용하고, 실수를 인식·수정하며, 다른 전략을 시도하는 behavior를 강화했다는 것입니다.
Transition: 여기서 성능을 올리는 compute가 training뿐 아니라 inference에도 생깁니다.
Source: references/post_training/03_openai_o1_system_card.pdf; exact optimizer/reward formulation intentionally not claimed
-->

---

# Test-time Compute: 새로운 Scaling Axis

<div class="takeaway agency-text">어려운 문제에 더 많은 추론 계산을 사용한다.</div>

<ScalingAxes />

<SourceFooter source="OpenAI o1 System Card; Kimi K3 Technical Report" slide="17" />

<!--
Goal: inference-time scaling을 새로운 성능 축으로 설명한다.
Talk track: Reasoning model에서는 답변 시 더 많은 compute를 사용하는 것도 성능 축이 됩니다. 핵심은 단순히 오래 생각하는 것이 아니라 compute를 효율적으로 배분하는 것입니다.
Transition: o1은 원리를 보여줬고, DeepSeek-R1은 더 공개적인 recipe로 논의를 확장했습니다.
Source: references/post_training/03_openai_o1_system_card.pdf; references/architecture/08_kimi_k3_technical_report.pdf
-->

---

# DeepSeek-R1-Zero: Reasoning SFT 없이 RL

<div class="takeaway">Reasoning SFT 없이 base model에 reasoning-oriented RL을 적용한 실험</div>

<R1ZeroPipeline />

<SourceFooter source="DeepSeek-R1 Technical Report — R1-Zero, not the final multi-stage R1 pipeline" slide="18" />
<!--
Goal: R1-Zero 실험이 왜 놀라웠는지 설명하고 최종 R1과 구분한다.
Talk track: R1-Zero는 reasoning SFT 없이 base model에 reasoning-oriented RL을 적용합니다. 최종 correctness reward를 최적화하며 long CoT, self-reflection, backtracking 같은 behavior가 나타난 점이 주목받았습니다.
Transition: 사람이 reasoning step마다 점수를 주지 않았다면 reward는 어디서 왔을까요?
Source: references/reasoning_rl/02_deepseek_r1.pdf; R1-Zero explicitly distinguished from DeepSeek-R1
-->

---

# Human Preference → Verifiable Reward

<div class="takeaway">정답을 자동 검증할 수 있다면 reward를 대규모로 생성할 수 있다.</div>

<PreferenceVsVerifier />

<SourceFooter source="InstructGPT; DeepSeek-R1; SWE-RL" slide="19" />

<!--
Goal: human preference와 자동 검증 가능한 reward의 서로 다른 용도를 구분한다.
Talk track: Open-ended helpfulness에는 human preference가 유용하지만, 수학·코드처럼 correctness를 자동 검증할 수 있는 영역에서는 reward를 훨씬 확장하기 쉽습니다.
Transition: 이 reward로 policy를 업데이트할 때 DeepSeek가 선택한 대표 방법이 GRPO였습니다.
Source: references/post_training/01_instructgpt_rlhf.pdf; references/reasoning_rl/02_deepseek_r1.pdf; references/agentic_rl/02_swe_rl.pdf
-->

---

# PPO vs GRPO

<div class="takeaway rl-text">“이 답은 같은 문제의 다른 답들보다 얼마나 좋은가?”</div>

<PPOvsGRPO />

<SourceFooter source="DeepSeekMath §4.1; DeepSeek-R1 §2.1 — PPO and GRPO are optimizer-level comparison" slide="20" />
<!--
Goal: critic을 쓰는 PPO와 group-relative comparison을 쓰는 GRPO의 직관을 비교한다.
Talk track: PPO는 critic/value estimate로 기대보다 얼마나 좋았는지 판단합니다. GRPO는 같은 prompt의 여러 response를 비교해 상대 advantage를 계산하므로 별도 critic을 제거할 수 있습니다. RLHF와 GRPO는 같은 레벨의 비교가 아닙니다.
Transition: 하지만 GRPO도 긴 reasoning을 대규모로 학습시키며 새로운 문제를 드러냈습니다.
Source: references/reasoning_rl/01_deepseekmath_grpo.pdf; references/reasoning_rl/02_deepseek_r1.pdf; references/reasoning_rl/05_gspo.pdf
-->

---

# R1 이후: GRPO도 완벽하지 않았다

<div class="takeaway">Reasoning RL의 다음 질문은 안정성·효율·objective 설계였다.</div>

<PostR1Branches />

<SourceFooter source="DAPO; Understanding R1-Zero-Like Training (Dr. GRPO); GSPO" slide="21" />
<!--
Goal: R1 이후 연구가 reasoning RL의 optimization quality로 이동했음을 보여준다.
Talk track: DAPO는 실전 학습 안정화, Dr.GRPO는 length bias, GSPO는 sequence-level optimization 문제를 다룹니다. 이 슬라이드는 세 방법의 지도이지 수식 deep dive가 아닙니다.
Transition: 최신 흐름은 domain과 reasoning effort까지 학습 대상으로 확장합니다.
Source: references/reasoning_rl/03_dapo.pdf; references/reasoning_rl/04_dr_grpo.pdf; references/reasoning_rl/05_gspo.pdf
-->

---

# Kimi K3: Domain × Reasoning Effort를 학습한다

<div class="takeaway">“더 오래 생각하라”에서 “문제에 맞게 얼마나 생각할지 학습하라”로</div>

<KimiK3PostTraining />

<SourceFooter source="Kimi K3 Technical Report §4.1 — 3 domains × {low, high, max} → MOPD" slide="22" />
<!--
Goal: R1 이후의 post-training/system-level 방향을 K3 사례로 보여준다.
Talk track: K3는 domain뿐 아니라 reasoning effort도 분리해 specialist policy를 만든 뒤 통합합니다. Reasoning 목표가 최대 길이보다 compute-quality trade-off로 이동함을 보여줍니다.
Transition: 출력이 token을 넘어 실제 action으로 확장되는 다음 단계로 가겠습니다.
Source: references/architecture/08_kimi_k3_technical_report.pdf
-->

---

# Agentic RL: Reasoning에서 행동으로

<div class="takeaway agency-text">RL의 학습 단위가 text response에서 장기 interaction trajectory로 확장된다.</div>

<AgenticLoop />

<SourceFooter source="ReAct; Search-R1; SWE-RL; ZeroTIR; Kimi K3 Technical Report" slide="23" />

<!--
Goal: reasoning이 multi-step interaction policy로 확장되는 모습을 보여준다.
Talk track: Agentic system은 검색 query를 만들고 코드를 실행하고 파일을 수정하고 결과를 관찰한 뒤 다음 action을 선택합니다. RL도 장기 interaction trajectory를 최적화할 수 있습니다.
Transition: 이제 전체 발전을 한 문장으로 정리하겠습니다.
Source: references/agentic_rl/04_react_reasoning_and_acting.pdf; references/agentic_rl/01_search_r1.pdf; references/agentic_rl/02_swe_rl.pdf; references/agentic_rl/03_agent_rl_scaling_law_zerotir.pdf; references/architecture/08_kimi_k3_technical_report.pdf
-->

---

# Generation → Reasoning → Agency

<div class="takeaway">LLM은 어느 순간 갑자기 생각하게 된 것이 아니다.</div>

<FinalSynthesis />

<SourceFooter source="Kimi K3; InstructGPT; OpenAI o1; Search-R1; ReAct" slide="24" />

<!--
Goal: 세 발전 축과 Generation → Reasoning → Agency를 기억에 남는 결론으로 통합한다.
Talk track: 구조가 더 긴 계산을 가능하게 했고, post-training이 문제 해결 behavior를 강화했으며, inference-time system이 계산·검증·도구 사용을 실제 문제에 배분하게 했습니다.
Transition: Generation에서 Reasoning으로, 그리고 Agency로 — 이것이 오늘 살펴본 큰 흐름입니다.
Source: references/architecture/08_kimi_k3_technical_report.pdf; references/post_training/01_instructgpt_rlhf.pdf; references/post_training/03_openai_o1_system_card.pdf; references/agentic_rl/01_search_r1.pdf; references/agentic_rl/04_react_reasoning_and_acting.pdf
-->
