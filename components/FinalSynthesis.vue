<template>
  <div class="synthesis" aria-label="Generation에서 Reasoning과 Agency로 이어지고 세 발전 축이 Better Reasoning을 만드는 최종 요약">
    <div class="stages">
      <section class="stage stage--generation"><span>01</span><strong>Generation</strong><b>무엇을 말할까?</b></section><div class="arrow">→</div>
      <section class="stage stage--reasoning"><span>02</span><strong>Reasoning</strong><b>어떻게 풀까?</b></section><div class="arrow">→</div>
      <section class="stage stage--agency"><span>03</span><strong>Agency</strong><b>무엇을 해야 할까?</b></section>
    </div>
    <div class="equation-final"><span>Better Reasoning</span><b>=</b><div><i class="arch"></i><strong>Efficient Architecture</strong></div><b>+</b><div><i class="rl"></i><strong>Reasoning-oriented Post-training</strong></div><b>+</b><div><i class="agency"></i><strong>Adaptive Inference-time Compute</strong></div></div>
  </div>
</template>

<style scoped>
.synthesis { height:278px; display:grid; grid-template-rows:174px 86px; gap:14px; }.stages { display:grid; grid-template-columns:1fr 48px 1fr 48px 1fr; gap:8px; align-items:center; }.stage { height:146px; padding:21px 23px; display:flex; flex-direction:column; justify-content:center; border:1px solid var(--color-line); border-top:3px solid var(--tone); border-radius:var(--radius-lg); background:var(--tone-bg); }.stage--generation { --tone:#8492a6; --tone-bg:var(--color-surface); }.stage--reasoning { --tone:var(--color-rl); --tone-bg:rgba(173,124,255,.035); }.stage--agency { --tone:var(--color-agency); --tone-bg:rgba(255,180,84,.035); }.stage span { color:var(--tone); font:700 10px/1 ui-monospace; }.stage strong { color:var(--tone); font-size:22px; margin-top:13px; }.stage b { color:var(--color-text); font-size:17px; margin-top:12px; }.arrow { color:var(--color-muted); font-size:28px; text-align:center; }.equation-final { padding:16px 18px; display:grid; grid-template-columns:auto 18px 1fr 18px 1.28fr 18px 1.28fr; gap:9px; align-items:center; border:1px solid var(--color-line); border-radius:var(--radius-lg); background:var(--color-bg-raised); }.equation-final > span { color:var(--color-text); font-size:17px; font-weight:760; }.equation-final > b { color:var(--color-muted); text-align:center; }.equation-final div { min-width:0; }.equation-final div i { display:block; height:3px; margin-bottom:8px; }.equation-final div strong { color:var(--color-text-soft); font-size:11px; line-height:1.25; }.equation-final .arch { background:var(--color-architecture); }.equation-final .rl { background:var(--color-rl); }.equation-final .agency { background:var(--color-agency); }
</style>
