<template>
  <div class="r1zero" aria-label="DeepSeek-V3-Base에서 reasoning RL을 거쳐 R1-Zero로 이어지는 실험과 reasoning behavior 변화">
    <div class="r1-pipeline">
      <div class="stage"><span>BASE MODEL</span><strong>DeepSeek-V3-Base</strong><small>reasoning SFT 없음</small></div>
      <div class="arrow">→</div>
      <div class="stage"><span>TRAIN</span><strong>Reasoning-oriented RL</strong><small>결과에 reward</small></div>
      <div class="arrow">→</div>
      <div class="stage stage--method"><span>SIGNAL + OPTIMIZER</span><strong>GRPO</strong><small>+ verifiable reward</small></div>
      <div class="arrow">→</div>
      <div class="stage stage--result"><span>EXPERIMENT</span><strong>R1-Zero</strong><small>최종 R1 pipeline 아님</small></div>
    </div>

    <div class="emergence">
      <div class="emergence__label"><span>TRAINING PROGRESSION</span><strong>Reasoning behavior</strong></div>
      <div class="trajectory">
        <div class="behavior behavior--1"><span class="trace"><i></i></span><b>Short reasoning</b></div>
        <div class="behavior behavior--2"><span class="trace"><i></i><i></i></span><b>Longer reasoning</b></div>
        <div class="behavior behavior--3"><span class="trace"><i></i><i></i><i class="check">✓</i></span><b>Checking</b></div>
        <div class="behavior behavior--4"><span class="trace"><i></i><i class="turn">↩</i><i></i><i class="check">✓</i></span><b>Self-reflection · Backtracking</b></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.r1zero { height: 282px; display: grid; grid-template-rows: 112px 1fr; gap: 15px; }
.r1-pipeline { display: grid; grid-template-columns: 1fr 24px 1fr 24px 1fr 24px 1fr; gap: 7px; align-items: stretch; }
.stage { min-width:0; display:flex; flex-direction:column; justify-content:center; padding:14px 15px; border:1px solid rgba(173,124,255,.30); border-radius:var(--radius-md); background:var(--color-surface); }
.stage span { color:var(--color-muted); font:700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing:.1em; }.stage strong { color:var(--color-text); font-size:16px; line-height:1.2; margin-top:8px; }.stage small { color:var(--color-muted); font-size:11px; margin-top:6px; }
.stage--method { border-color:rgba(173,124,255,.62); background:rgba(173,124,255,.06); }.stage--method strong { color:var(--color-rl); font-size:20px; }.stage--result { border-color:var(--color-rl); border-top-width:3px; }.stage--result strong { color:var(--color-rl); font-size:21px; }
.arrow { align-self:center; color:var(--color-rl); font-size:21px; text-align:center; }
.emergence { display:grid; grid-template-columns:155px 1fr; gap:16px; min-height:0; padding:14px 16px; border:1px solid var(--color-line); border-radius:var(--radius-lg); background:var(--color-bg-raised); }
.emergence__label { display:flex; flex-direction:column; justify-content:center; border-right:1px solid var(--color-line-soft); }.emergence__label span { color:var(--color-muted); font:700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing:.1em; }.emergence__label strong { color:var(--color-rl); font-size:18px; line-height:1.2; margin-top:10px; }
.trajectory { display:grid; grid-template-columns:repeat(4,1fr); gap:9px; align-items:stretch; }.behavior { min-width:0; display:flex; flex-direction:column; justify-content:center; padding:9px 10px; border-left:1px solid var(--color-line); }.behavior b { color:var(--color-text-soft); font-size:12px; line-height:1.25; margin-top:10px; }
.trace { height:28px; display:flex; align-items:center; gap:5px; }.trace::before { content:""; flex:1; height:2px; background:rgba(173,124,255,.34); }.trace i { display:grid; place-items:center; width:8px; height:8px; border-radius:50%; background:var(--color-rl); color:var(--color-bg); font:700 9px/1 sans-serif; font-style:normal; }.behavior--2 .trace i:nth-child(2) { margin-left:15px; }.behavior--4 .trace .turn { width:20px; height:20px; background:rgba(173,124,255,.16); border:1px solid var(--color-rl); color:var(--color-rl); }.trace .check { width:19px; height:19px; }
</style>
