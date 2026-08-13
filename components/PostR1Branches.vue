<template>
  <div class="post-r1" aria-label="GRPO 이후 DAPO, Dr.GRPO, GSPO가 서로 다른 optimization 문제를 다루는 병렬 지도">
    <div class="hub"><span>BASELINE</span><strong>GRPO</strong><small>reasoning RL at scale</small></div>
    <div class="branches" aria-hidden="true"><i></i><i></i><i></i></div>
    <section><div class="problem">학습 안정성 · exploration</div><span>BRANCH A</span><strong>DAPO</strong><small>대규모 학습 안정화</small></section>
    <section><div class="problem">length bias · token efficiency</div><span>BRANCH B</span><strong>Dr.GRPO</strong><small>길이 편향 완화</small></section>
    <section><div class="problem">objective mismatch</div><span>BRANCH C</span><strong>GSPO</strong><small>sequence-level optimization</small></section>
    <div class="map-note">한 줄의 교체 역사가 아니라, <b>서로 다른 optimization 문제에 대한 병렬 개선</b></div>
  </div>
</template>

<style scoped>
.post-r1 { height:276px; display:grid; grid-template-columns:repeat(3,1fr); grid-template-rows:64px 28px 1fr 36px; gap:0 14px; }.hub { grid-column:1 / 4; width:270px; justify-self:center; padding:11px 18px; display:flex; align-items:baseline; justify-content:center; gap:11px; border:1px solid var(--color-rl); border-radius:var(--radius-md); background:rgba(173,124,255,.055); }.hub span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.08em; }.hub strong { color:var(--color-rl); font-size:21px; }.hub small { color:var(--color-muted); font-size:10px; }.branches { grid-column:1 / 4; width:68%; justify-self:center; display:grid; grid-template-columns:repeat(3,1fr); border-top:1px solid rgba(173,124,255,.48); transform:translateY(13px); }.branches i { justify-self:center; width:1px; height:26px; background:rgba(173,124,255,.48); }.post-r1 section { min-width:0; display:flex; flex-direction:column; justify-content:center; padding:17px 19px; border:1px solid rgba(173,124,255,.38); border-top:3px solid var(--color-rl); border-radius:var(--radius-lg); background:rgba(173,124,255,.03); }.problem { color:var(--color-muted); font-size:11px; padding-bottom:12px; margin-bottom:13px; border-bottom:1px solid var(--color-line-soft); }.post-r1 section > span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.08em; }.post-r1 section > strong { color:var(--color-rl); font-size:22px; margin-top:8px; }.post-r1 section > small { color:var(--color-text-soft); font-size:12px; margin-top:7px; }.map-note { grid-column:1 / 4; display:grid; place-items:center; color:var(--color-muted); font-size:11px; }.map-note b { color:var(--color-text-soft); }
</style>
