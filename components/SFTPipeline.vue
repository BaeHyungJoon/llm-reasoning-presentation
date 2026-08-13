<template>
  <div class="sft" aria-label="Prompt, Human Answer, SFT, Instruction-following Model로 이어지는 supervised fine-tuning pipeline">
    <div class="stage"><span>01 · INPUT</span><strong>Prompt</strong><small>사용자 질문</small></div><div class="arrow">→</div>
    <div class="stage stage--human"><span>02 · DEMONSTRATION</span><strong>Human Answer</strong><small>원하는 응답 예시</small></div><div class="arrow">→</div>
    <div class="stage stage--train"><span>03 · SUPERVISED</span><strong>SFT</strong><small>예시를 따라 학습</small></div><div class="arrow">→</div>
    <div class="stage stage--model"><span>04 · BEHAVIOR</span><strong>Instruction-following</strong><small>질문에 맞춰 응답</small></div>
    <div class="lesson"><span>사람이 정답을 직접 작성</span><i></i><strong>좋은 답변의 형태를 보여준다</strong></div>
  </div>
</template>

<style scoped>
.sft { height:266px; display:grid; grid-template-columns:1fr 28px 1fr 28px 1fr 28px 1.12fr; grid-template-rows:204px 44px; gap:10px 6px; align-items:center; }.stage { height:164px; padding:19px 17px; display:flex; flex-direction:column; justify-content:center; border:1px solid var(--color-line); border-top:3px solid var(--tone,#8492a6); border-radius:var(--radius-lg); background:var(--color-surface); }.stage--human,.stage--train,.stage--model { --tone:var(--color-rl); }.stage--model { background:rgba(173,124,255,.055); border-color:var(--color-rl); }.stage span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.08em; }.stage strong { color:var(--tone,var(--color-text)); font-size:18px; line-height:1.2; margin-top:16px; }.stage small { color:var(--color-muted); font-size:12px; margin-top:10px; }.arrow { color:var(--color-rl); font-size:23px; text-align:center; }.lesson { grid-column:1 / 8; display:grid; grid-template-columns:auto 1fr auto; gap:14px; align-items:center; color:var(--color-muted); font-size:12px; padding:0 18px; }.lesson i { height:1px; background:linear-gradient(90deg,var(--color-line),var(--color-rl)); }.lesson strong { color:var(--color-rl); font-size:14px; }
</style>
