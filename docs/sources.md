# Slide Source Map

This map is limited to the files currently available under `references/`. `assets/reference_figures/` is empty. It records claim-level support; it is not a general bibliography. Project framing comes from `presentation_brief.md` and `slide_plan.md`, while factual claims below are grounded only in the supplied papers.

## Slide 1 — LLM은 어떻게 더 잘 생각하게 되었나

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — *Training Language Models to Follow Instructions with Human Feedback*
- `post_training/03_openai_o1_system_card.pdf` — *OpenAI o1 System Card*
- `agentic_rl/04_react_reasoning_and_acting.pdf` — *ReAct: Synergizing Reasoning and Acting in Language Models*

Claims supported:
- Instruction-following, reasoning-oriented RL, and reasoning-plus-action are distinct stages in the deck's conceptual progression.
- The opening progression is a synthesis of the supplied literature, not a claim that one paper defines the whole sequence.

Do not use this source for:
- A single causal or chronological claim that these papers form one canonical lineage.

Source status:
- verified

## Slide 2 — LLM은 어떻게 추론할 수 있게 되었을까?

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — instruction following with human feedback
- `post_training/03_openai_o1_system_card.pdf` — reasoning, strategy refinement, and mistake recognition
- `agentic_rl/01_search_r1.pdf` — interleaved reasoning and search
- `agentic_rl/04_react_reasoning_and_acting.pdf` — interleaved reasoning, acting, and observation

Claims supported:
- Modern systems can extend beyond next-token continuation into instruction following, iterative reasoning, and tool-mediated action.

Do not use this source for:
- The claim that all deployed LLMs perform every stage autonomously.

Source status:
- verified

## Slide 3 — 세 가지 발전 축

Primary sources:
- `architecture/08_kimi_k3_technical_report.pdf` — architecture, post-training, test-time scaling, and long-horizon execution in one system case study
- `post_training/01_instructgpt_rlhf.pdf` — post-training for user intent
- `post_training/03_openai_o1_system_card.pdf` — RL and test-time compute for reasoning

Claims supported:
- Architecture efficiency, post-training, and inference-time computation are complementary explanatory axes.
- Kimi K3 is evidence of co-design across these layers, not the origin of the three-axis framing.

Do not use this source for:
- A mathematical identity claiming the three axes are independent or exhaustive.

Source status:
- verified

## Slide 4 — Transformer의 출발점: Attention

Primary sources:
- `architecture/01_attention_is_all_you_need.pdf` — *Attention Is All You Need*

Claims supported:
- Scaled dot-product attention computes weights from queries and keys and applies them to values.
- Self-attention relates positions in a sequence; the displayed attention equation is supported.

Do not use this source for:
- Later KV-cache, sparse-attention, or recurrent-attention designs.

Source status:
- verified

## Slide 5 — Long Context 병목: Full Attention은 비싸다

Primary sources:
- `architecture/01_attention_is_all_you_need.pdf` — per-layer self-attention complexity `O(N²·d)`
- `architecture/05_deepseek_v3_2_sparse_attention.pdf` — sparse attention motivated by long-context efficiency

Claims supported:
- Full self-attention forms all-pairs token interactions and has quadratic sequence-length complexity conceptually.
- Long-context efficiency motivates alternatives that reduce the attended set.

Do not use this source for:
- Identical wall-clock scaling constants across all implementations and hardware.

Source status:
- verified

## Slide 6 — KV 효율화: MHA → MQA/GQA → MLA

Primary sources:
- `architecture/02_gqa.pdf` — *GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints*
- `architecture/03_deepseek_v2_mla_moe.pdf` — *DeepSeek-V2*
- `architecture/04_deepseek_v3_technical_report.pdf` — MLA reuse in DeepSeek-V3

Claims supported:
- MHA uses separate key/value heads; MQA shares one; GQA shares key/value heads within query groups.
- MLA jointly compresses keys and values into a latent representation to reduce inference KV cache.

Do not use this source for:
- A universal claim that each successive method is always more accurate or faster in every setting.

Source status:
- verified

## Slide 7 — Long-context Architecture의 두 갈래

Primary sources:
- `architecture/05_deepseek_v3_2_sparse_attention.pdf` — top-k token selection with DeepSeek Sparse Attention
- `architecture/06_kimi_linear_kda.pdf` — recurrent/linear KDA memory and hybrid KDA/MLA architecture

Claims supported:
- Sparse attention selects a subset of stored token information.
- Linear/recurrent attention compresses history into finite recurrent state.
- These are parallel strategy families; the supplied papers do not establish `Sparse Attention → KDA` as a direct lineage.

Do not use this source for:
- Claiming one family universally replaces the other.

Source status:
- verified

## Slide 8 — Kimi K3: Sequence × Depth × Width

Primary sources:
- `architecture/08_kimi_k3_technical_report.pdf` — K3 architecture and its sequence/depth/width organization
- `architecture/06_kimi_linear_kda.pdf` — prior KDA and hybrid linear/full-attention design
- `architecture/07_attention_residuals.pdf` — prior Attention Residuals design

Claims supported:
- Sequence: K3 interleaves KDA with Gated MLA.
- Depth: Attention Residuals selectively aggregate preceding representations.
- Width: Stable LatentMoE expands and routes the expert space.
- KDA and Attention Residuals predate the K3 report; K3 integrates them rather than originating every component.

Do not use this source for:
- Claiming all three component ideas originated in Kimi K3.
- Claiming these architecture components alone created reasoning behavior.

Source status:
- verified

## Slide 9 — Architecture가 만든 것은 ‘생각하는 기반’

Primary sources:
- `architecture/03_deepseek_v2_mla_moe.pdf` — efficient KV cache and inference
- `architecture/06_kimi_linear_kda.pdf` — efficient long-sequence generation for agentic/test-time-scaling workloads
- `architecture/08_kimi_k3_technical_report.pdf` — architecture plus separate post-training and long-horizon systems

Claims supported:
- Architecture changes improve the efficiency/capacity available for long context and trajectories.
- The K3 report treats architecture, post-training, and infrastructure as separate co-designed contributions.

Do not use this source for:
- “MLA/KDA/Sparse Attention taught the model to reason.”

Source status:
- verified

## Slide 10 — 다음 token 예측 ≠ 사용자 의도

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — language-modeling objective differs from following user instructions helpfully and safely

Claims supported:
- Increasing model size alone does not inherently make a model follow user intent.
- Next-token prediction and instruction following are different objectives.

Do not use this source for:
- Claiming pretraining contributes no instruction-following capability.

Source status:
- verified

## Slide 11 — SFT: 좋은 답변의 예시를 학습하다

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — labeler-written demonstrations used for supervised fine-tuning

Claims supported:
- SFT learns desired prompt-response behavior from human-written demonstrations.

Do not use this source for:
- Claiming SFT is always necessary before every form of reasoning RL; R1-Zero is an explicit counterexample experiment.

Source status:
- verified

## Slide 12 — RLHF: 답을 쓰지 말고 비교한다

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — ranked model outputs and reward-model training

Claims supported:
- Labelers compare and rank multiple outputs.
- The comparisons train a reward model that predicts preferred outputs.

Do not use this source for:
- Treating preference ranking as objective correctness verification.

Source status:
- verified

## Slide 13 — Reward Model + PPO

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — SFT, reward-model training, and PPO stages
- `reasoning_rl/01_deepseekmath_grpo.pdf` — PPO value-model pathway in the PPO/GRPO comparison

Claims supported:
- In the InstructGPT example, PPO optimizes the policy against a learned reward model.
- PPO uses a learned value function/critic for advantage estimation; policy movement is constrained through proximal/KL mechanisms.

Do not use this source for:
- A full PPO objective on the main slide.
- The claim that all RLHF implementations use the identical recipe.

Source status:
- verified

## Slide 14 — GPT-4: Post-training Feedback이 다양해진다

Primary sources:
- `post_training/02_gpt4_system_card.pdf` — RLHF, safety fine-tuning, prior-use data, classifiers, expert red teaming, adversarial testing, and system-level mitigations

Claims supported:
- GPT-4 deployment preparation used multiple evaluation, feedback, safety, red-team, and system-level intervention channels.
- Post-training/deployment preparation was broader than a single human-ranking loop.

Do not use this source for:
- Undocumented claims that rule/rubric or synthetic-data inputs were part of GPT-4 post-training.

Source status:
- verified

## Slide 15 — 전환점: 좋은 답변 → 좋은 사고 과정

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — preferred response behavior under human feedback
- `post_training/03_openai_o1_system_card.pdf` — RL-trained reasoning, strategy refinement, and mistake recognition
- `reasoning_rl/02_deepseek_r1.pdf` — outcome incentives associated with reflection, verification, and alternative approaches

Claims supported:
- The historical examples motivate a shift in emphasis from preferred response behavior toward problem-solving behavior under outcome feedback.

Do not use this source for:
- Claiming RLHF and reasoning RL are mutually exclusive categories or that all reasoning steps are directly rewarded.

Source status:
- verified

## Slide 16 — o1: RL로 사고 전략을 강화하다

Primary sources:
- `post_training/03_openai_o1_system_card.pdf` — *OpenAI o1 System Card*

Claims supported:
- The o1 family is trained with large-scale reinforcement learning to reason using chain of thought.
- The models learn to refine thinking, try different strategies, and recognize mistakes.

Do not use this source for:
- An exact optimizer, reward formula, hidden chain-of-thought implementation, or other undisclosed recipe details.

Source status:
- verified

## Slide 17 — Test-time Compute: 새로운 Scaling Axis

Primary sources:
- `post_training/03_openai_o1_system_card.pdf` — capability increases from reasoning and test-time compute
- `architecture/08_kimi_k3_technical_report.pdf` — test-time computation as a second scaling axis and multi-effort scaling

Claims supported:
- Reasoning-era systems can use inference/test-time computation as a scaling axis.
- Reasoning effort can vary rather than being a fixed budget for every task.

Do not use this source for:
- A specific universal performance curve or guaranteed monotonic gain from more inference compute.

Source status:
- verified

## Slide 18 — DeepSeek-R1-Zero: Reasoning SFT 없이 RL

Primary sources:
- `reasoning_rl/02_deepseek_r1.pdf` — *DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning*

Claims supported:
- R1-Zero applies GRPO-based RL to DeepSeek-V3-Base without a preceding reasoning SFT stage.
- It uses rule-based accuracy and format rewards for verifiable domains.
- Longer responses, reflection/verification, and exploration of alternatives appear during training.
- DeepSeek-R1 is distinct: it adds cold-start data, rejection sampling/SFT, and later alignment stages.

Do not use this source for:
- Calling the R1-Zero pipeline the final DeepSeek-R1 training pipeline.
- Claiming every observed behavior was absent from the base model; `reasoning_rl/04_dr_grpo.pdf` raises base-model/pretraining caveats.

Source status:
- verified

## Slide 19 — Human Preference → Verifiable Reward

Primary sources:
- `post_training/01_instructgpt_rlhf.pdf` — human preference comparisons and learned reward models
- `reasoning_rl/02_deepseek_r1.pdf` — rule-based math correctness, code test cases, and format rewards
- `agentic_rl/02_swe_rl.pdf` — rule-based rewards in software-engineering RL

Claims supported:
- Human preference is useful for open-ended desired behavior.
- Math answers, code behavior, and formats can supply automatically checkable reward signals in the cited examples.

Do not use this source for:
- Treating all tasks as automatically verifiable.
- A broad formal definition or historical origin of the umbrella term RLVR, which is not used on the visible slide.

Source status:
- verified

## Slide 20 — PPO vs GRPO

Primary sources:
- `reasoning_rl/01_deepseekmath_grpo.pdf` — original GRPO introduction and PPO/GRPO comparison
- `reasoning_rl/02_deepseek_r1.pdf` — GRPO use and group-relative advantage equation
- `reasoning_rl/05_gspo.pdf` — concise PPO and GRPO preliminaries

Claims supported:
- PPO uses a learned value model/critic for advantage estimation.
- GRPO samples multiple responses to the same query and computes relative advantages from group rewards without a separate critic.
- The displayed standardized group-relative advantage equation is supported.

Do not use this source for:
- “RLHF vs GRPO” as equivalent categories. RLHF is a feedback/training paradigm; PPO and GRPO are policy optimization approaches.
- Claiming GRPO has no reference-policy, clipping, or regularization machinery.

Source status:
- verified

## Slide 21 — R1 이후: GRPO도 완벽하지 않았다

Primary sources:
- `reasoning_rl/03_dapo.pdf` — *DAPO: An Open-Source LLM Reinforcement Learning System at Scale*
- `reasoning_rl/04_dr_grpo.pdf` — *Understanding R1-Zero-Like Training: A Critical Perspective* / Dr. GRPO
- `reasoning_rl/05_gspo.pdf` — *Group Sequence Policy Optimization*

Claims supported:
- DAPO targets large-scale RL stability/efficiency with clip, sampling, token-level loss, and overlong-reward techniques.
- Dr. GRPO identifies optimization biases associated with response length and improves token efficiency.
- GSPO moves importance ratios, clipping, rewarding, and optimization to the sequence level to address stability and objective mismatch.

Do not use this source for:
- Presenting DAPO, Dr. GRPO, and GSPO as one linear replacement chain.
- Claiming one method solves every limitation of GRPO.

Source status:
- verified

## Slide 22 — Kimi K3: Domain × Reasoning Effort를 학습한다

Primary sources:
- `architecture/08_kimi_k3_technical_report.pdf` — K3 post-training stages and multi-effort specialists

Claims supported:
- K3 develops experts across general, agentic, and coding domains.
- Crossing three domains with `{low, high, max}` effort levels yields nine expert models.
- Multi-Teacher On-Policy Distillation (MOPD) consolidates domain/effort specialists into a unified model.

Do not use this source for:
- Describing K3 as “the optimizer after GSPO.”
- Claiming domain/effort specialization or distillation originated with K3.

Source status:
- verified

## Slide 23 — Agentic RL: Reasoning에서 행동으로

Primary sources:
- `agentic_rl/04_react_reasoning_and_acting.pdf` — interleaved reasoning, actions, and observations
- `agentic_rl/01_search_r1.pdf` — RL optimization of multi-turn reasoning/search trajectories
- `agentic_rl/02_swe_rl.pdf` — RL for software-evolution/code-edit behavior
- `agentic_rl/03_agent_rl_scaling_law_zerotir.pdf` — outcome-reward RL and emergent Python tool use
- `architecture/08_kimi_k3_technical_report.pdf` — long-horizon agentic environments and reason-act-observe-verify-adapt loop

Claims supported:
- Tool-using systems interleave reasoning with actions and environment observations.
- RL can optimize multi-turn interaction trajectories involving search, code, or persistent environments.
- K3 explicitly describes reasoning, acting, observing, verifying, and adapting over long horizons.

Do not use this source for:
- Claiming all listed tools were trained in one shared agentic RL recipe.
- Claiming ReAct itself is an RL algorithm; it is used here to ground the reasoning/action interaction pattern.

Source status:
- verified

## Slide 24 — Generation → Reasoning → Agency

Primary sources:
- `architecture/08_kimi_k3_technical_report.pdf` — architecture/post-training/inference co-design and long-horizon action
- `post_training/01_instructgpt_rlhf.pdf` — instruction-following post-training
- `post_training/03_openai_o1_system_card.pdf` — reasoning RL and test-time compute
- `agentic_rl/01_search_r1.pdf` — learned search interaction
- `agentic_rl/04_react_reasoning_and_acting.pdf` — reasoning/action synthesis

Claims supported:
- The final equation and `Generation → Reasoning → Agency` are evidence-backed synthesis statements across the supplied sources.
- Architecture enables efficient computation, post-training shapes behavior, and inference systems allocate reasoning/tool action.

Do not use this source for:
- Claiming a single paper proves the complete synthesis or that the three layers are cleanly separable in practice.

Source status:
- verified
