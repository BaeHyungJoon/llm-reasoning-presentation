<template>
  <div class="rlhf-loop" aria-label="Policy가 response를 만들고 Reward Model과 critic을 거쳐 PPO로 업데이트되는 RLHF loop">
    <svg viewBox="0 0 860 225" preserveAspectRatio="none" aria-hidden="true">
      <defs><marker id="rlhf-arrow" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path class="arrow-head" d="M0,0 L0,6 L7,3 z" /></marker></defs>
      <path d="M145 112 C185 30 290 25 349 78" /><path d="M470 78 C535 25 650 36 697 107" /><path d="M697 137 C650 208 535 207 470 157" /><path d="M349 157 C286 208 181 197 145 142" />
    </svg>
    <div class="node node--policy"><span>01</span><strong>Policy</strong><small>LLM</small></div>
    <div class="node node--response"><span>02</span><strong>Response</strong><small>후보 답변</small></div>
    <div class="node node--reward"><span>03</span><strong>Reward Model</strong><small>선호 score</small></div>
    <div class="node node--critic"><span>04</span><strong>Critic / Value</strong><small>advantage 추정</small></div>
    <div class="node node--update"><span>05</span><strong>PPO Update</strong><small>policy를 제한적으로 이동</small></div>
    <div class="loop-center"><span>RLHF EXAMPLE</span><strong>Reward ↑</strong><small>기존 policy와의 과도한 drift는 제한</small></div>
  </div>
</template>

<style scoped>
.rlhf-loop { position:relative; height:278px; }.rlhf-loop svg { position:absolute; inset:0; width:100%; height:100%; }.rlhf-loop svg > path { fill:none; stroke:rgba(173,124,255,.52); stroke-width:2; marker-end:url(#rlhf-arrow); vector-effect:non-scaling-stroke; }.rlhf-loop .arrow-head { fill:var(--color-rl); stroke:none; }.node { position:absolute; z-index:1; width:164px; height:72px; padding:12px 14px; display:flex; flex-direction:column; justify-content:center; border:1px solid rgba(173,124,255,.42); border-radius:var(--radius-md); background:var(--color-surface); box-shadow:0 0 0 5px var(--color-bg); }.node span { position:absolute; right:10px; top:9px; color:var(--color-muted); font:700 9px/1 ui-monospace; }.node strong { color:var(--color-text); font-size:16px; }.node small { color:var(--color-muted); font-size:10px; margin-top:6px; }.node--policy { left:0; top:87px; }.node--response { left:252px; top:4px; }.node--reward { right:80px; top:4px; }.node--critic { right:0; bottom:4px; }.node--update { left:252px; bottom:4px; border-color:var(--color-rl); }.node--update strong,.node--reward strong { color:var(--color-rl); }.loop-center { position:absolute; left:50%; top:52%; transform:translate(-50%,-50%); width:246px; height:90px; display:flex; flex-direction:column; align-items:center; justify-content:center; border:1px solid var(--color-line); border-radius:50%; background:var(--color-bg-raised); text-align:center; }.loop-center span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.1em; }.loop-center strong { color:var(--color-rl); font-size:22px; margin-top:7px; }.loop-center small { color:var(--color-muted); font-size:9px; margin-top:5px; }
</style>
