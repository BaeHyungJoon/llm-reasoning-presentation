<template>
  <div class="reasoning-loop" aria-label="문제를 나누고 시도하고 확인하고 수정하며 다른 전략을 시도하는 reasoning loop">
    <svg viewBox="0 0 860 230" preserveAspectRatio="none" aria-hidden="true"><defs><marker id="reason-arrow" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path class="arrow-head" d="M0,0 L0,6 L7,3 z" /></marker></defs><path d="M115 112 C160 24 310 23 369 74" /><path d="M491 74 C555 22 708 38 744 110" /><path d="M744 137 C700 215 535 208 484 161" /><path d="M370 161 C307 210 154 199 115 139" /></svg>
    <div class="step step--break"><span>01</span><strong>Break down</strong><small>문제 나누기</small></div>
    <div class="step step--try"><span>02</span><strong>Try</strong><small>한 전략 시도</small></div>
    <div class="step step--check"><span>03</span><strong>Check</strong><small>오류 인식</small></div>
    <div class="step step--correct"><span>04</span><strong>Correct</strong><small>수정</small></div>
    <div class="step step--alternate"><span>05</span><strong>Alternate strategy</strong><small>다른 접근</small></div>
    <div class="center"><span>PUBLICLY DOCUMENTED</span><strong>Large-scale RL</strong><small>productive use of reasoning</small></div>
  </div>
</template>

<style scoped>
.reasoning-loop { position:relative; height:278px; }.reasoning-loop svg { position:absolute; inset:0; width:100%; height:100%; }.reasoning-loop svg > path { fill:none; stroke:rgba(173,124,255,.6); stroke-width:2; marker-end:url(#reason-arrow); vector-effect:non-scaling-stroke; }.reasoning-loop .arrow-head { fill:var(--color-rl); stroke:none; }.step { position:absolute; z-index:1; width:156px; height:68px; padding:11px 13px; display:flex; flex-direction:column; justify-content:center; border:1px solid rgba(173,124,255,.48); border-radius:var(--radius-md); background:var(--color-surface); box-shadow:0 0 0 5px var(--color-bg); }.step span { position:absolute; top:8px; right:9px; color:var(--color-muted); font:700 9px/1 ui-monospace; }.step strong { color:var(--color-text); font-size:16px; }.step small { color:var(--color-muted); font-size:10px; margin-top:5px; }.step--break { left:0; top:92px; }.step--try { left:250px; top:3px; }.step--check { right:82px; top:3px; }.step--correct { right:0; bottom:3px; }.step--alternate { left:250px; bottom:3px; border-color:var(--color-rl); }.step--alternate strong { color:var(--color-rl); }.center { position:absolute; left:50%; top:53%; transform:translate(-50%,-50%); width:246px; height:92px; display:flex; flex-direction:column; align-items:center; justify-content:center; border:1px solid var(--color-line); border-radius:50%; background:var(--color-bg-raised); text-align:center; }.center span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.08em; }.center strong { color:var(--color-rl); font-size:22px; margin-top:7px; }.center small { color:var(--color-text-soft); font-size:11px; margin-top:6px; }
</style>
