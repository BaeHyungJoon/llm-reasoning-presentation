# presentation_brief.md

## 1. Presentation Identity

### Title
# LLM은 어떻게 더 잘 생각하게 되었나

### Subtitle
**Architecture Efficiency → RLHF → Reasoning RL → Agentic RL**

### Central Question
# LLM은 어떻게 추론할 수 있게 되었을까?

### Duration
30–40 minutes.

### Audience
SSAFY AI self-directed learning session.

The audience:
- understands basic machine learning,
- has encountered Transformer / attention,
- does not necessarily understand reinforcement learning,
- should leave with a coherent conceptual map rather than implementation-level mastery.

---

## 2. Core Thesis

Modern LLM reasoning should not be explained by one technique.

Use this framing throughout the deck:

> **Better Reasoning = Efficient Architecture + Reasoning-oriented Post-training + Adaptive Inference-time Compute**

### Axis A — Architecture Efficiency
Architecture changes make long context, long chain-of-thought, and long agent trajectories computationally feasible.

Examples covered:
- MHA → MQA/GQA → MLA
- Sparse Attention
- Linear/recurrent attention
- Kimi K3 as a recent architecture case study:
  - Sequence: KDA + Gated MLA
  - Depth: Attention Residuals
  - Width: Stable LatentMoE

### Axis B — Post-training
Post-training evolved from aligning outputs with humans toward optimizing reasoning and action strategies.

Historical arc:
- SFT
- RLHF
- Reward Model
- PPO
- GPT-4-era richer feedback / safety post-training
- reasoning-oriented RL
- RLVR
- GRPO
- post-R1 optimizer improvements
- domain/effort-specialized RL and consolidation in Kimi K3

### Axis C — Inference-time Compute / Agency
The model increasingly decides how much computation and external action to use at inference time.

Arc:
- immediate answer,
- chain-of-thought,
- longer reasoning,
- verification / revision,
- adaptive reasoning effort,
- search / tools,
- agentic loop.

---

## 3. Narrative Arc

The talk must feel like one answer to one question:

> “How did a next-token predictor become a system that can reason, verify, revise, and act?”

### Act I — Compute the context efficiently
Start from Transformer attention and the long-context bottleneck.

Do not teach the whole Transformer architecture.
Only explain enough architecture to motivate efficient long-context reasoning.

### Act II — Align the model with user intent
Move from GPT-3 next-token prediction to SFT and RLHF.

Key point:
RLHF primarily shaped useful/aligned response behavior; it is not the full story of later reasoning-oriented RL.

### Act III — Optimize reasoning itself
Introduce the conceptual transition:
`Good response` → `Good problem-solving strategy`.

Use o1 as the public evidence that large-scale RL and test-time thinking became a new reasoning paradigm.

Use DeepSeek-R1/R1-Zero as the more openly documented recipe:
- verifiable reward,
- GRPO,
- reasoning emergence.

### Act IV — Improve reasoning RL
Explain that GRPO did not end the research problem.

Use:
- DAPO,
- Dr.GRPO,
- GSPO
as examples of stability, efficiency, and objective-design improvements.

Do not dive deeply into every loss function.

### Act V — Scale reasoning into agents
Use Kimi K3 and agentic RL to show the next stage:
- domain-specific and reasoning-effort-specific policies,
- consolidation,
- long-horizon trajectories,
- tool use,
- act/observe/verify/retry loops.

End with:
`Generation → Reasoning → Agency`.

---

## 4. What the Presentation Is NOT

This is not:
- a full Transformer lecture,
- a chronological list of frontier models,
- a benchmark leaderboard,
- a detailed PPO mathematics seminar,
- a Kimi K3 product introduction,
- a generic “AI agents are the future” talk.

Every included paper/model must serve the central reasoning-evolution story.

---

## 5. Required Conceptual Distinctions

### Pretraining vs Post-training
Use:
- Pretraining: creates broad capability / representations / knowledge.
- Post-training: shapes how capability is used for instruction-following, reasoning, safety, tools, and behavior.

Do not overstate this as a perfectly clean separation.

### Response Quality vs Reasoning Strategy
The critical midpoint of the talk is:

> RL moves from primarily shaping preferred responses toward optimizing problem-solving behavior under verifiable outcomes.

### Human Preference vs Verifiable Reward
Human preference:
- useful for open-ended quality/alignment.

Verifiable reward:
- useful when correctness can be automatically checked, such as math/code/structured tasks.

### Training-time vs Test-time Compute
Training scaling:
- more model/data/training compute.

Reasoning-era test-time scaling:
- spend more inference compute on difficult tasks,
- potentially search, verify, revise, or call tools.

### Architecture vs Post-training
Architecture efficiency enables longer/cheaper computation.
Post-training teaches behavior.
Inference system decides how computation is spent.

The talk should repeatedly reconnect these layers.

---

## 6. Scope of Architecture Section

Target duration: ~7–8 minutes.

Include:
1. Attention intuition.
2. `O(N^2)` long-context issue.
3. KV-cache efficiency:
   - MHA,
   - MQA/GQA,
   - MLA.
4. Two parallel long-context strategies:
   - Sparse Attention,
   - Linear/recurrent attention.
5. Kimi K3:
   - Sequence,
   - Depth,
   - Width.

Do not include:
- encoder/decoder block walkthrough,
- detailed positional encoding derivation,
- RoPE derivation,
- FlashAttention kernel implementation,
- KDA recurrence derivation,
- MoE load-balancing math,
- Mamba/SSM history.

FlashAttention may be mentioned in speaker notes as an implementation/IO optimization example, not as a main evolutionary step.

---

## 7. Scope of Post-training Section

Target duration: ~18–20 minutes.

Must include:
- GPT-3 limitation.
- SFT.
- Human preference.
- Reward Model.
- PPO intuition.
- GPT-4-era broader post-training feedback.
- transition to reasoning-oriented RL.
- o1.
- DeepSeek-R1-Zero.
- verifiable reward / RLVR.
- PPO vs GRPO.
- DAPO / Dr.GRPO / GSPO.
- Kimi K3 post-training.

Highest-priority learning moment:
**Slide 20, PPO vs GRPO.**

The audience should understand:
- why PPO uses a value/critic estimate,
- why GRPO can use within-group reward comparison instead,
- why this can simplify reasoning RL training.

---

## 8. Scope of Agentic Section

Target duration: ~4–6 minutes.

Use the following conceptual expansion:

`Token policy`
→ `Reasoning policy`
→ `Action/tool policy`

Core loop:

`Reason → Act → Observe → Verify → Retry`

Tool examples:
- web/search,
- Python/code execution,
- database,
- API,
- filesystem.

The point is not to catalogue agent frameworks.
The point is to show that reinforcement learning can optimize multi-step interaction trajectories, not only text responses.

---

## 9. Visual Story

The deck should visually evolve.

### Early slides
Structured, simple, foundational:
- token relationships,
- attention matrices,
- KV caches.

### Middle slides
Learning loops:
- SFT pipeline,
- human ranking,
- Reward Model,
- PPO,
- GRPO.

### Later slides
Branching and looping:
- reasoning loop,
- multiple rollouts,
- domain × effort matrix,
- agentic loop.

This progression should itself communicate:
`static generation → iterative reasoning → interactive agency`.

---

## 10. Presentation Pacing

Approximate pacing:

| Section | Slides | Time |
|---|---:|---:|
| Opening / framing | 1–3 | 3–4 min |
| Architecture | 4–9 | 7–8 min |
| GPT-3 → GPT-4 post-training | 10–15 | 8–9 min |
| o1 → R1 → GRPO | 16–20 | 9–11 min |
| Post-R1 + K3 + Agentic RL | 21–23 | 6–7 min |
| Conclusion | 24 | 1–2 min |

If time must be reduced to ~30 minutes:
- shorten Slides 4, 6, 14, 17, 21,
- do not remove Slides 3, 15, 18, 20, 22, 23.

---

## 11. Priority Slides

Spend the most design and explanation effort on:

### Slide 3
The three-axis framework.
This is the conceptual map for the entire presentation.

### Slide 8
Kimi K3 architecture.
Must clearly distinguish sequence/depth/width.

### Slide 15
The transition:
preferred response → reasoning strategy.

### Slide 18
R1-Zero.
Must be simple enough for the audience to grasp what made the experiment surprising.

### Slide 20
PPO vs GRPO.
The most technically important comparison.

### Slide 22
Kimi K3 post-training.
Must show `3 domains × 3 effort levels → 9 specialists → MOPD → unified model`.

### Slide 23
Agentic RL.
Must visually communicate a loop, not a linear text generator.

---

## 12. Final Takeaway

The audience should remember this sentence:

> **LLM reasoning did not appear because one model suddenly “learned to think.” Efficient architecture made longer computation feasible, post-training taught better problem-solving behavior, and inference-time systems learned to spend compute through reasoning, verification, and action.**

Final visual equation:

> **Better Reasoning = Efficient Architecture + Reasoning-oriented Post-training + Adaptive Inference-time Compute**

Final evolution:

> **Generation → Reasoning → Agency**
