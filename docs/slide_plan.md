# slide_plan.md

# 24-Slide Implementation Specification

Each slide specification contains:
- **Goal**: what the audience should understand.
- **On-slide content**: visible text.
- **Visual**: primary visual structure.
- **Talk track**: speaker explanation.
- **Transition**: how to lead into the next slide.
- **Implementation notes**: Slidev/Codex guidance.

---

## Slide 1 — LLM은 어떻게 더 잘 생각하게 되었나

### Goal
Frame the talk as an evolution of LLM intelligence across architecture, training, and inference.

### On-slide content
**LLM은 어떻게 더 잘 생각하게 되었나**

Architecture Efficiency  
→ RLHF  
→ Reasoning RL  
→ Agentic RL

Small footer:
- SSAFY AI 자기주도학습
- presenter / date placeholders

### Visual
A minimal horizontal evolution line:
`GPT-style generation → aligned chat → reasoning → agentic system`

Do not overcrowd with model logos.

### Talk track
“This is not a presentation about one model. We are going to trace how a next-token predictor became a system that can reason, verify, revise, and use tools.”

### Transition
“먼저 오늘 발표 전체를 관통하는 질문 하나로 시작하겠습니다.”

### Implementation notes
Use a strong title slide.
No more than 15–20 visible words excluding subtitle/footer.

---

## Slide 2 — LLM은 어떻게 추론할 수 있게 되었을까?

### Goal
Introduce the central question without centering specific model names.

### On-slide content
**다음 토큰을 예측하던 언어모델은 어떻게  
문제를 분해하고, 검증하고, 수정하며 답을 찾게 되었을까?**

Bottom progression:
`Prediction → Instruction Following → Reasoning → Acting`

### Visual
One model/system icon evolving left-to-right:

1. Predict next token.
2. Follow user instruction.
3. Break down / verify / revise.
4. Use tools / act.

### Talk track
“초기 LLM의 기본 목표는 다음 token 예측이었습니다. 그런데 지금 모델은 문제를 여러 단계로 나누고, 자신의 접근을 검토하고, 필요하면 도구까지 씁니다. 그 변화는 어디에서 왔을까요?”

### Transition
“이 질문을 세 가지 축으로 나눠보면 전체 발전사가 훨씬 선명해집니다.”

### Implementation notes
Do not use “Why are o1/R1/K3 reasoning models?” as the title.
The question is about the evolution of reasoning capability itself.

---

## Slide 3 — 세 가지 발전 축

### Goal
Give the audience the conceptual map for the whole deck.

### On-slide content
Center:
**Better Reasoning**

Three axes:
- **Architecture** — 더 효율적으로 계산
- **Post-training** — 더 좋은 사고 전략 학습
- **Inference-time Compute** — 필요한 만큼 탐색·검증·행동

### Visual
Triangle or three-column convergence diagram.

Semantic colors:
- Architecture = cyan.
- Post-training = violet.
- Inference = amber.

### Talk track
“Reasoning을 RL 하나로 설명하면 부족합니다. 긴 context와 trajectory를 처리할 구조, 사고 전략을 학습시키는 post-training, 그리고 실제 문제에서 계산을 어떻게 쓸지 결정하는 inference가 함께 발전했습니다.”

### Transition
“먼저 모델이 더 긴 생각을 감당할 수 있게 만든 구조적 변화부터 보겠습니다.”

### Implementation notes
Create reusable `<ThreeAxes />` component.
These colors must remain consistent on all later slides.

---

# PART I — ARCHITECTURE

## Slide 4 — Transformer의 출발점: Attention

### Goal
Refresh attention only enough to motivate later efficiency work.

### On-slide content
**Attention = 어떤 token의 정보를 참고할지 계산**

Small labels:
- Query: 찾는 정보
- Key: 매칭 기준
- Value: 가져올 정보

Equation:
`Attention(Q,K,V) = softmax(QK^T / √d_k)V`

### Visual
Use one Korean sentence.
Show one token attending to several others with different line weights.

### Talk track
“Transformer의 핵심은 token 관계를 동적으로 계산하는 attention입니다. 오늘은 Q/K/V 전체를 다시 배우기보다, 모든 token 관계를 계산한다는 점에 집중하겠습니다.”

### Transition
“문제는 context가 길어질수록 이 관계 계산이 빠르게 비싸진다는 것입니다.”

### Implementation notes
Equation should be visually secondary to the intuition diagram.

---

## Slide 5 — Long Context 병목: Full Attention은 비싸다

### Goal
Explain why efficiency matters specifically in the reasoning era.

### On-slide content
**Full Attention**
- Context length: `N`
- Attention matrix: `N × N`
- Compute: `O(N²)`

Bottom:
`Long Context + Long CoT + Tool History → Efficiency matters`

### Visual
Left: growing attention matrices.
Right: curve showing quadratic growth.

### Talk track
“Reasoning model은 긴 CoT뿐 아니라 문서, 검색 결과, tool observation을 오래 유지해야 합니다. 그런데 full attention은 sequence가 길어질수록 모든 token pair를 비교합니다.”

### Transition
“그래서 먼저 생성 과정에서 계속 쌓이는 K/V를 어떻게 줄일지 연구가 진행됩니다.”

### Implementation notes
Do not imply every attention implementation has identical real-world scaling constants.
The slide teaches the full-attention conceptual bottleneck.

---

## Slide 6 — KV 효율화: MHA → MQA/GQA → MLA

### Goal
Show the intuition behind KV-cache efficiency.

### On-slide content
- **MHA** — head별 K/V
- **MQA** — K/V 공유
- **GQA** — 그룹별 K/V 공유
- **MLA** — K/V 정보를 latent representation으로 압축

Bottom statement:
**오래 생각하려면 KV cache도 효율적이어야 한다.**

### Visual
Four mini diagrams with progressively smaller cache blocks.

### Talk track
“Autoregressive generation은 과거 token의 K/V를 cache합니다. Context와 reasoning이 길어지면 cache가 커지므로 MQA/GQA는 공유를, MLA는 압축을 활용합니다.”

### Transition
“KV만 줄여도 충분하지 않습니다. 더 긴 context에서는 ‘무엇을 볼 것인가’ 자체도 바뀌기 시작합니다.”

### Implementation notes
Create `<AttentionEvolution />`.
Do not over-explain MLA matrices.

---

## Slide 7 — Long-context Architecture의 두 갈래

### Goal
Correctly present sparse and recurrent/linear approaches as parallel strategies.

### On-slide content
Left:
**Sparse Attention**
> 기억된 token 중 중요한 token만 선택

Right:
**Linear / Recurrent Attention**
> 과거 정보를 recurrent state로 압축

### Visual
Branch from `Long-context bottleneck` into:

A. Sparse:
context tokens → select relevant subset → attention.

B. Recurrent:
past stream → compressed memory state → current token.

### Talk track
“Sparse 계열은 과거 token을 유지하되 중요한 일부를 읽습니다. Recurrent/linear 계열은 과거 정보를 state에 압축해 읽고 쓰는 방향입니다. 하나가 다른 하나의 후속 단계라기보다 병렬적인 해법입니다.”

### Transition
“Kimi K3는 이런 효율화 문제를 sequence뿐 아니라 depth와 width까지 확장해서 봅니다.”

### Implementation notes
Create `<SparseVsRecurrent />`.
Do not render `Sparse → KDA` as a linear arrow.

---

## Slide 8 — Kimi K3: Sequence × Depth × Width

### Goal
Use K3 as a recent architecture case study showing multi-axis information-flow design.

### On-slide content
Center:
**Kimi K3**

Three axes:
- **Sequence** — KDA + Gated MLA
- **Depth** — Attention Residuals
- **Width** — Stable LatentMoE

Bottom:
**정보 흐름을 token · layer · expert 세 방향에서 재설계**

### Visual
Three-axis system diagram.

Sequence:
tokens / memory.

Depth:
layer representations with attention over previous layers.

Width:
router selecting experts.

### Talk track
“K3의 재미있는 점은 attention 하나의 개선으로 설명하지 않는다는 것입니다. Sequence 방향에서는 KDA와 MLA, depth에서는 AttnRes, width에서는 MoE를 통해 정보 흐름을 효율화합니다.”

Explain briefly:
- KDA: recurrent memory.
- AttnRes: layer representations can be selectively reused.
- LatentMoE: expert computation in a lower-dimensional/efficient form.

### Transition
“그렇다면 이런 구조가 모델에게 직접 ‘생각하는 법’을 가르친 걸까요?”

### Implementation notes
Priority custom component: `<KimiK3Architecture />`.
Keep technical details minimal and source-check all K3-specific claims.

---

## Slide 9 — Architecture가 만든 것은 ‘생각하는 기반’

### Goal
Prevent causal overclaim and transition to post-training.

### On-slide content
**Architecture ≠ reasoning policy**

Flow:
`Efficient Architecture`
→ `Long Context`
→ `Long CoT / Tool History`
→ `Long Agent Trajectory`

Key sentence:
**더 오래, 더 싸게 생각할 수 있는 기반**

### Visual
Foundation/platform metaphor:
architecture at bottom, long reasoning trajectory above it.

### Talk track
“MLA나 KDA가 reasoning을 직접 가르친 것은 아닙니다. 이들은 더 긴 context와 trajectory를 감당하는 계산 기반을 만듭니다. 이제 남는 질문은: 모델은 그 계산을 어떻게 사용해야 하는지 어떻게 배우는가?”

### Transition
“그 답을 찾으려면 GPT-3의 학습 목표부터 다시 봐야 합니다.”

---

# PART II — ALIGNMENT / POST-TRAINING

## Slide 10 — GPT-3의 한계: Next-token Prediction ≠ Instruction Following

### Goal
Explain why post-training became necessary.

### On-slide content
Left:
**Pretraining objective**
> 다음 token을 예측하라

Right:
**User objective**
> 내 질문에 정확하고 유용하게 답하라

Middle:
`≠`

### Visual
Two goal cards that do not align.

### Talk track
“GPT-3는 강력한 언어모델이지만 기본 objective는 사용자 만족이 아닙니다. 자연스럽게 text를 이어 쓰는 것과 instruction에 정확히 답하는 것은 다른 목표입니다.”

### Transition
“가장 직접적인 해결책은 좋은 답변의 예시를 보여주는 것이었습니다.”

---

## Slide 11 — SFT: 좋은 답변의 예시를 학습하다

### Goal
Introduce supervised instruction tuning.

### On-slide content
`Prompt → Human-written Answer → SFT → Instruction-following Model`

Key sentence:
**“이런 질문에는 이렇게 답하는 것이 좋다.”**

### Visual
Simple four-step pipeline.

### Talk track
“SFT는 사람이 작성한 demonstration을 사용해 instruction-response behavior를 학습합니다. 하지만 모든 질문의 완벽한 답을 사람이 작성하는 것은 매우 비쌉니다.”

### Transition
“답을 직접 쓰는 대신, 여러 답 중 더 좋은 답을 고르게 하면 어떨까요?”

---

## Slide 12 — RLHF: 답을 쓰지 말고 비교한다

### Goal
Explain human preference data intuitively.

### On-slide content
`Prompt`
→ `Response A / B / C / D`
→ `Human Ranking`
→ `B > A > D > C`

Bottom:
**Preference data**

### Visual
Four response cards and a human ranking interaction.

### Talk track
“여러 답변을 비교하는 것은 완벽한 답변을 직접 만드는 것보다 상대적으로 쉽습니다. 이 비교 데이터를 이용해 인간 선호를 학습하는 Reward Model을 만듭니다.”

### Transition
“이제 사람 대신 Reward Model이 반복적으로 점수를 줄 수 있습니다.”

### Implementation notes
Priority RLHF diagram.
May combine visually with Slide 13 via consistent component language.

---

## Slide 13 — Reward Model + PPO

### Goal
Explain the RLHF optimization loop at a high level.

### On-slide content
`LLM → Answer → Reward Model → Reward → PPO Update → LLM`

Small side note:
- Reward ↑
- policy drift는 제한

### Visual
Circular loop.
Reward Model visibly separate from Policy.

### Talk track
“Reward Model은 사람이 선호할 답변에 더 높은 score를 줍니다. PPO는 그 reward를 높이는 방향으로 policy를 업데이트하고, 기존 모델과 너무 멀어지는 것을 제한합니다.”

Optional verbal intuition:
“좋은 방향으로 움직이되 한 번에 너무 멀리 점프하지 않는다.”

### Transition
“GPT-4 시대에는 이 post-training 신호가 사람의 선호 하나보다 훨씬 다양해집니다.”

### Implementation notes
Do not put full PPO objective on this slide.

---

## Slide 14 — GPT-4: Post-training Feedback이 다양해진다

### Goal
Show post-training becoming a richer system.

### On-slide content
Inputs:
- Human Feedback
- Rule / Rubric
- Safety Data
- Synthetic Data
- Red-team Data

All flow into:
**Post-training**

### Visual
Multiple feedback/data sources converging.

### Talk track
“GPT-4 시대의 post-training은 단순 human ranking을 넘어 rule/rubric, safety, synthetic/adversarial data 등을 포함하는 복합 과정으로 확장됩니다.”

### Transition
“그런데 여기까지의 중심 질문은 여전히 ‘어떤 답변이 좋은가?’였습니다. Reasoning model에서 질문이 달라집니다.”

---

## Slide 15 — 전환점: 좋은 답변 → 좋은 사고 과정

### Goal
Create the conceptual midpoint of the talk.

### On-slide content
Left:
**Response Optimization**
> 사람이 좋아하는 답인가?

Arrow.

Right:
**Reasoning Optimization**
> 정답에 도달하는 전략인가?

Bottom:
`Answer quality → Problem-solving policy`

### Visual
Left: prompt → response.
Right: problem → try → check → revise → answer.

### Talk track
“RLHF는 response behavior를 정렬하는 데 큰 역할을 했습니다. Reasoning model에서는 reward를 이용해 문제 분해, 검증, 수정 같은 문제 해결 behavior 자체를 강화하려는 방향이 중요해집니다.”

### Transition
“이 전환을 대표적으로 보여준 모델이 o1입니다.”

### Implementation notes
One of the most important storytelling slides.
Use strong visual contrast between left and right.

---

# PART III — REASONING RL

## Slide 16 — o1: RL로 사고 전략을 강화하다

### Goal
Introduce reasoning-oriented RL without inventing undisclosed details.

### On-slide content
Loop:
`Break down → Try → Check → Correct → Try another strategy`

Key statement:
**Large-scale RL + productive use of reasoning**

### Visual
A self-correcting reasoning loop with one failed branch.

### Talk track
“OpenAI가 공개한 핵심은 large-scale RL을 통해 chain-of-thought를 더 생산적으로 사용하고, 실수를 인식·수정하고, 다른 전략을 시도하는 behavior를 강화했다는 것입니다.”

### Accuracy note
Do not name a specific undisclosed policy optimizer for o1.

### Transition
“여기서 또 하나의 변화가 생깁니다. 성능을 올리는 compute가 training에만 있는 게 아닙니다.”

---

## Slide 17 — Test-time Compute: 새로운 Scaling Axis

### Goal
Explain inference-time scaling.

### On-slide content
Top:
**Training-time scaling**
`model / data / training compute ↑`

Bottom:
**Test-time scaling**
`thinking / search / verification compute ↑`

Key statement:
**어려운 문제에 더 많은 추론 계산을 사용한다.**

### Visual
Two simple increasing-performance curves.

Optional visual labels:
- Easy task → small budget.
- Hard task → larger budget.

### Talk track
“Reasoning model에서는 답변 시 더 많은 compute를 사용하는 것도 성능 축이 됩니다. 이후 연구에서는 단순히 더 오래 생각하는 것뿐 아니라 얼마나 효율적으로 compute를 배분할지가 중요해집니다.”

### Transition
“o1은 원리를 보여줬지만 상세 recipe는 많이 공개하지 않았습니다. DeepSeek-R1이 그 다음 논의를 크게 열었습니다.”

---

## Slide 18 — DeepSeek-R1-Zero: RL만으로 Reasoning이 나타날까?

### Goal
Explain why R1-Zero was surprising.

### On-slide content
`DeepSeek-V3-Base`
→ `Reasoning RL`
→ `GRPO + Verifiable Reward`
→ `R1-Zero`

Emergent labels:
- longer reasoning,
- self-reflection,
- backtracking.

### Visual
Base model response transforms into longer iterative trajectory over RL training.

### Talk track
“R1-Zero는 reasoning SFT 없이 base model에 reasoning-oriented RL을 적용하는 실험입니다. 최종 correctness reward를 최적화하면서 long CoT, self-reflection, backtracking 같은 behavior가 나타난 점이 주목받았습니다.”

### Accuracy note
Explicitly label this as R1-Zero, not the final R1 multi-stage pipeline.

### Transition
“그런데 사람이 reasoning step마다 점수를 주지 않았다면 reward는 어디서 왔을까요?”

### Implementation notes
Priority component: `<R1ZeroPipeline />`.

---

## Slide 19 — Human Preference → Verifiable Reward

### Goal
Explain RLVR intuitively.

### On-slide content
Left:
**Human Preference**
> “어떤 답이 더 좋은가?”

Right:
**Verifiable Reward**
- Math: 정답 checker
- Code: unit test
- Format: rule checker

Bottom:
**정답을 자동 검증할 수 있다면 reward를 대규모로 생성할 수 있다.**

### Visual
Human judge on left; automated verifier stack on right.

### Talk track
“Open-ended helpfulness는 human preference가 유용하지만, 수학·코드처럼 correctness를 자동 검증할 수 있는 영역에서는 reward를 훨씬 확장하기 쉽습니다. 이 흐름을 RLVR이라고 부릅니다.”

### Transition
“이 reward를 가지고 policy를 업데이트할 때 DeepSeek가 선택한 대표 방법이 GRPO였습니다.”

---

## Slide 20 — PPO vs GRPO

### Goal
Give the audience an intuitive but technically meaningful comparison.

### On-slide content
Left:
**PPO**
- Policy
- Reward
- Critic / Value estimate
- Advantage

Right:
**GRPO**
- Same prompt
- Multiple rollouts
- Group rewards
- Relative advantage
- No separate critic

Equation:
`A_i = (r_i - mean(r_1,...,r_G)) / std(r_1,...,r_G)`

Key statement:
**“이 답은 같은 문제의 다른 답들보다 얼마나 좋은가?”**

### Visual
50:50 comparison.

PPO:
one trajectory + critic/value pathway.

GRPO:
prompt fans out to 4–8 candidate responses with rewards, then recombines into group statistics.

### Talk track
“PPO에서는 critic/value estimate를 이용해 action이 기대보다 얼마나 좋았는지 판단합니다. GRPO는 같은 prompt에서 여러 response를 만들고, 그 그룹 내 상대 reward를 이용해 advantage를 계산합니다. 그래서 별도 critic을 제거할 수 있습니다.”

Also say:
“RLHF와 GRPO는 같은 레벨의 비교가 아닙니다. 여기서는 PPO와 GRPO라는 optimizer 측면을 비교하고 있습니다.”

### Transition
“하지만 GRPO 역시 긴 reasoning을 대규모로 학습시키면서 새로운 문제를 드러냈습니다.”

### Implementation notes
Highest-priority technical slide.
Create `<PPOvsGRPO />`.
Do not overcrowd with full policy objectives.

---

## Slide 21 — R1 이후: GRPO도 완벽하지 않았다

### Goal
Show research moving from proof-of-concept to optimization quality.

### On-slide content
Center:
**GRPO**

Branches:
- **DAPO** — stability / exploration
- **Dr.GRPO** — length bias / token efficiency
- **GSPO** — sequence-level optimization

Top problem labels:
- instability,
- uninformative groups,
- overly long reasoning,
- optimization mismatch.

### Visual
GRPO hub → three improvements.

### Talk track
“R1 이후 질문은 ‘RL이 되느냐’에서 ‘어떻게 더 안정적이고 효율적으로 학습하느냐’로 이동합니다. DAPO는 실전 학습 안정화, Dr.GRPO는 length bias, GSPO는 sequence-level optimization 문제를 다룹니다.”

### Transition
“그리고 최신 흐름에서는 reasoning 성능뿐 아니라 어떤 domain에서 얼마나 오래 생각할지까지 학습하려고 합니다.”

### Implementation notes
Keep each method to one phrase.
This is a map, not a deep-dive slide.

---

## Slide 22 — Kimi K3: Domain × Reasoning Effort를 학습한다

### Goal
Show a recent post-training/system-level direction after R1.

### On-slide content
Matrix:

| | Low | High | Max |
|---|---|---|---|
| General | ● | ● | ● |
| Agent | ● | ● | ● |
| Coding | ● | ● | ● |

Label:
**3 domains × 3 effort levels = 9 RL specialists**

Then:
`9 specialists → MOPD → Unified Kimi K3`

Key statement:
**“더 오래 생각하라” → “문제에 맞게 얼마나 생각할지 학습하라”**

### Visual
Large 3×3 specialist matrix feeding into one unified model.

### Talk track
“K3 post-training의 흥미로운 포인트는 domain뿐 아니라 reasoning effort도 분리해 specialist policy를 만든 뒤 이를 통합한다는 것입니다. Reasoning의 목표가 단순 최대 길이가 아니라 compute-quality trade-off로 이동하고 있음을 보여줍니다.”

Mention at high level:
- agent/coding/general specialization,
- low/high/max effort,
- multi-teacher on-policy distillation,
- long-horizon agentic training as a system consideration.

### Accuracy note
Do not describe K3 as “the optimizer after GSPO.”
It is a broader post-training/system design case study.

### Transition
“Reasoning effort를 조절하고 domain을 나누기 시작하면, 다음 단계는 모델의 출력이 단순 token이 아니라 실제 action으로 확장되는 것입니다.”

### Implementation notes
Priority component: `<KimiK3PostTraining />`.

---

# PART IV — AGENCY

## Slide 23 — Agentic RL: Reasoning에서 행동으로

### Goal
Show how reasoning becomes a multi-step interaction policy.

### On-slide content
Core loop:
`Reason → Act → Observe → Verify → Retry`

Tool examples around loop:
- Search
- Python
- Database
- API
- Files

Bottom:
**Token policy → Reasoning policy → Action policy**

### Visual
Circular agent loop connected to external tool/environment icons.

### Talk track
“초기 LLM의 action space는 사실상 다음 token이었습니다. Agentic system에서는 검색 query를 만들고, 코드를 실행하고, 파일을 수정하고, 결과를 관찰한 뒤 다음 action을 선택합니다. RL의 학습 단위도 장기 interaction trajectory로 확장될 수 있습니다.”

### Transition
“이제 전체 발전을 한 문장으로 다시 정리해보겠습니다.”

### Implementation notes
Priority component: `<AgenticLoop />`.
This slide should feel more dynamic/loop-like than previous linear pipelines.

---

## Slide 24 — Generation → Reasoning → Agency

### Goal
Deliver a memorable synthesis.

### On-slide content
Three stages:

### Generation
**무엇을 말할까?**

↓

### Reasoning
**어떻게 풀까?**

↓

### Agency
**무엇을 해야 할까?**

Bottom equation:
**Better Reasoning = Efficient Architecture + Reasoning-oriented Post-training + Adaptive Inference-time Compute**

### Visual
Three-stage ascending structure or convergence diagram.

Reconnect the three semantic colors:
- Architecture cyan.
- Post-training violet.
- Inference/Agency amber.

### Talk track
“LLM이 어느 순간 갑자기 생각하게 된 것이 아닙니다. 구조가 더 긴 계산을 가능하게 했고, post-training이 문제 해결 behavior를 강화했으며, inference-time system이 계산·검증·도구 사용을 실제 문제에 배분하게 되었습니다.”

Final line:
“Generation에서 Reasoning으로, 그리고 Agency로 — 이것이 오늘 살펴본 LLM reasoning 발전의 큰 흐름입니다.”

### Implementation notes
Keep this visually simple.
Do not introduce new technical terms on the final slide.
