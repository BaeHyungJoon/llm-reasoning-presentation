# AGENTS.md

## 1. Project Mission

Create a polished 24-slide technical presentation for a 30–40 minute SSAFY AI self-directed learning session.

Presentation title:

> **LLM은 어떻게 더 잘 생각하게 되었나**  
> Architecture Efficiency → RLHF → Reasoning RL → Agentic RL

The central question is:

> **LLM은 어떻게 추론할 수 있게 되었을까?**

The presentation must explain LLM reasoning as the combined result of three evolving axes:

1. **Architecture Efficiency** — how models process longer context and trajectories more efficiently.
2. **Post-training / Reinforcement Learning** — how models learn instruction-following and reasoning strategies.
3. **Inference-time Compute / Agency** — how models spend compute at inference time, search, verify, use tools, and act.

Do not turn this deck into a generic Transformer history or a paper-by-paper literature review.

---

## 2. Source of Truth

When making content or design decisions, follow this priority order:

1. `docs/presentation_brief.md`
2. `docs/slide_plan.md`
3. files under `references/`
4. files under `assets/reference_figures/`
5. external research only when explicitly requested

If sources conflict, preserve the framing and scope in `presentation_brief.md` and flag the factual conflict instead of silently choosing one.

Never invent:
- model architecture details,
- training algorithms,
- benchmark values,
- release dates,
- parameter counts,
- reward formulations,
- citations,
- paper claims.

If a claim is uncertain, add a `TODO(source-check)` comment in the source rather than presenting it as fact.

---

## 3. Audience and Depth

Audience:
- SSAFY learners with basic AI/ML knowledge.
- They have learned basic Transformer concepts but are not expected to know PPO, GRPO, MLA, KDA, or agentic RL in detail.

Target level:
- technically accurate,
- intuitive first,
- equations only where they materially improve understanding.

Do not assume the audience knows reinforcement-learning notation.

---

## 4. Storytelling Rule

Every technical concept should appear because it solves a problem introduced immediately before it.

Preferred narrative pattern:

> Problem → Why previous method is insufficient → New idea → What changed → Why it matters for reasoning

Examples:

- Full Attention is expensive at long context → KV and attention efficiency → GQA / MLA / Sparse or recurrent approaches.
- Next-token prediction does not optimize for user intent → SFT → RLHF.
- Human preference optimizes response quality but not necessarily difficult problem solving → reasoning-oriented RL.
- PPO uses a critic → GRPO replaces critic estimation with group-relative comparison.
- GRPO has practical limitations → DAPO / Dr.GRPO / GSPO.
- Long CoT alone is insufficient → adaptive reasoning and agentic action.

Do not organize the deck as:
“Paper A → Paper B → Paper C → Paper D”.

---

## 5. Visual System

### Overall
- Aspect ratio: 16:9.
- Style: dark, clean, technical, modern.
- Prefer diagrams and visual comparisons over paragraphs.
- One dominant idea per slide.
- One dominant visual per slide.

### Semantic colors
Use a consistent semantic color system across the deck.

- **Architecture**: cyan / blue family.
- **Post-training / RL**: violet / purple family.
- **Inference / Agentic action**: amber / orange family.
- **Neutral / baseline**: gray / white.

Do not introduce unrelated accent colors.

### Typography
Target hierarchy:
- Slide title: 36–44px equivalent.
- Key statement: 26–32px.
- Body labels: 18–24px.
- Captions / source labels: 12–16px.

Do not reduce text size merely to fit overflow. Rewrite or simplify instead.

### Text density
Default maximum:
- 1 title,
- 1 core statement,
- 3–5 supporting labels,
- 1 visual.

Avoid paragraphs on slides.

Speaker explanation belongs in notes, not on the canvas.

---

## 6. Diagram Rules

Prefer custom Vue / SVG / CSS diagrams over screenshots of papers.

Original paper figures may be used only as:
- source references,
- visual inspiration,
- temporary placeholders.

For final slides, redraw important concepts using the deck design system.

Recommended custom components:

- `EvolutionTimeline.vue`
- `ThreeAxes.vue`
- `AttentionEvolution.vue`
- `SparseVsRecurrent.vue`
- `KimiK3Architecture.vue`
- `RLHFPipeline.vue`
- `ResponseVsReasoning.vue`
- `ReasoningLoop.vue`
- `R1ZeroPipeline.vue`
- `PPOvsGRPO.vue`
- `PostR1Branches.vue`
- `KimiK3PostTraining.vue`
- `AgenticLoop.vue`

Use Mermaid only for quick prototypes. Final high-value diagrams should be Vue/SVG/CSS components.

---

## 7. Equation Policy

Use equations sparingly.

The main deck should contain at most these core equations unless explicitly requested:

1. Attention:
   `Attention(Q,K,V) = softmax(QK^T / sqrt(d_k))V`

2. Full-attention scaling:
   `O(N^2)`

3. GRPO group-relative advantage:
   `A_i = (r_i - mean(r_1,...,r_G)) / std(r_1,...,r_G)`

Do not place full PPO or GRPO policy objectives on the main slides by default.

If deeper equations are useful, put them in appendix slides only if the user asks for an appendix.

---

## 8. Accuracy Guardrails

Keep these distinctions explicit:

### Architecture vs reasoning training
Do not claim:
> “MLA/KDA/Sparse Attention created reasoning ability.”

Say:
> These architectures improve efficiency/capacity for long context, long CoT, or long agent trajectories, while post-training shapes reasoning behavior.

### RLHF vs GRPO
Do not present “RLHF vs GRPO” as two equivalent categories.

Explain:
- RLHF is a feedback/training paradigm.
- PPO and GRPO are policy optimization approaches.
- A more precise comparison is:
  `Human preference + learned reward + PPO`
  vs
  `Verifiable/rule-based reward + GRPO`
  for the specific historical examples discussed.

### o1
Only state details publicly documented by OpenAI.
Do not claim an undisclosed exact optimizer or reward formula.

### R1 vs R1-Zero
Always distinguish:
- R1-Zero: direct reasoning RL experiment from a base model without reasoning SFT.
- R1: multi-stage training pipeline including cold-start/SFT and later alignment stages.

### Sparse vs recurrent/linear attention
Do not show:
`Sparse Attention → KDA`
as a single direct evolutionary chain.

Show them as alternative/parallel solutions to long-context efficiency.

### Kimi K3
Present K3 as a recent case study that combines architectural and post-training/system-level innovations.
Do not imply every component originated in K3 if the original idea predates the K3 report.

---

## 9. Slide Implementation Workflow

Work in phases.

### Phase 1 — Skeleton
- Create all 24 slides with titles, one key statement, and placeholder visuals.
- Verify slide count and narrative continuity.
- Do not over-design yet.

### Phase 2 — Priority diagrams
Polish these slides first:
- Slide 3 — Three axes
- Slide 8 — Kimi K3 architecture
- Slide 12/13 — RLHF pipeline
- Slide 15 — Response → reasoning transition
- Slide 18 — R1-Zero
- Slide 20 — PPO vs GRPO
- Slide 22 — Kimi K3 post-training
- Slide 23 — Agentic RL

### Phase 3 — Remaining visuals
Standardize the remaining slides.

### Phase 4 — Visual QA
For every slide:
- render or screenshot,
- inspect overflow,
- inspect alignment,
- inspect contrast,
- inspect text density,
- inspect whether the visual communicates without reading speaker notes.

### Phase 5 — Export QA
Verify:
- web presentation works,
- PDF export works,
- all 24 pages export,
- Korean text renders correctly,
- mathematical notation renders,
- no elements are clipped.

---

## 10. Editing Rules for Codex

When the user asks to change one slide:
- edit only that slide and shared components genuinely required by the change,
- do not rewrite unrelated slides,
- preserve the semantic color system,
- preserve slide numbering and narrative order unless explicitly asked.

When changing a shared component:
- check every slide that uses it.

When a content change affects a later conclusion:
- flag the affected slide(s) before changing them.

---

## 11. Speaker Notes

Each slide should eventually have speaker notes containing:

- `Goal`: what the audience should understand.
- `Talk track`: roughly 45–120 seconds depending on slide importance.
- `Transition`: one sentence linking to the next slide.
- `Source note`: primary source(s) supporting factual claims.

Do not place detailed citations in the visual center of the slide.
Keep small source labels in the footer when needed.

---

## 12. Build / QA Expectations

After material changes:

1. Run the Slidev dev/build command.
2. Fix compile errors.
3. Render all slides.
4. Check slide count = 24.
5. Check for visual overflow.
6. Verify export readiness.

Never claim the deck is finished without visually checking rendered output.

---

## 13. Definition of Done

The deck is done when a listener can answer these questions after the talk:

1. Why is next-token pretraining alone not the whole explanation for modern reasoning behavior?
2. Why did architecture efficiency become important for long-context reasoning?
3. What did SFT and RLHF change?
4. What changed when RL became reasoning-oriented?
5. Why are verifiable rewards important?
6. What is the intuitive difference between PPO and GRPO?
7. Why did post-R1 research explore DAPO, Dr.GRPO, and GSPO?
8. What does Kimi K3 illustrate about architecture/post-training co-design?
9. How does reasoning extend into agentic action?
10. Why should modern LLM progress be viewed through Architecture + Post-training + Inference-time Compute together?
