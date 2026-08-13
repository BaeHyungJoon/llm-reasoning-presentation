<template>
  <div class="foundation-map" aria-label="효율적 architecture가 긴 context와 trajectory를 가능하게 하지만 reasoning policy를 직접 가르치지는 않는 구조">
    <div class="architecture-layer"><span>ARCHITECTURE ENABLES</span><strong>더 오래 · 더 싸게 계산</strong><div class="capacity"><i>Long Context</i><i>Long CoT</i><i>Tool History</i><i>Agent Trajectory</i></div></div>
    <div class="boundary"><span>≠</span><small>행동 전략은 자동으로 생기지 않는다</small></div>
    <div class="policy-layer"><span>POST-TRAINING SHAPES</span><strong>그 계산을 어떻게 쓸 것인가</strong><div class="policy-path"><i>분해</i><b>→</b><i>검증</i><b>→</b><i>수정</i></div></div>
  </div>
</template>

<style scoped>
.foundation-map { height:270px; display:grid; grid-template-columns:1.16fr 82px .84fr; gap:16px; align-items:stretch; }
.architecture-layer,.policy-layer { padding:23px 24px; display:flex; flex-direction:column; justify-content:center; border:1px solid var(--tone-line); border-top:3px solid var(--tone); border-radius:var(--radius-lg); background:var(--tone-bg); }.architecture-layer { --tone:var(--color-architecture); --tone-line:rgba(49,215,244,.42); --tone-bg:rgba(49,215,244,.035); }.policy-layer { --tone:var(--color-rl); --tone-line:rgba(173,124,255,.42); --tone-bg:rgba(173,124,255,.035); }
.architecture-layer > span,.policy-layer > span { color:var(--color-muted); font:700 10px/1 ui-monospace; letter-spacing:.1em; }.architecture-layer > strong,.policy-layer > strong { color:var(--tone); font-size:23px; margin-top:12px; }.capacity { display:grid; grid-template-columns:repeat(2,1fr); gap:9px; margin-top:25px; }.capacity i,.policy-path i { padding:12px; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); color:var(--color-text-soft); font-size:13px; font-style:normal; text-align:center; }.boundary { display:grid; place-content:center; text-align:center; }.boundary span { color:var(--color-text); font-size:46px; }.boundary small { color:var(--color-muted); font-size:10px; line-height:1.35; margin-top:8px; }.policy-path { display:flex; align-items:center; justify-content:center; gap:7px; margin-top:32px; }.policy-path i { padding:11px 10px; }.policy-path b { color:var(--color-rl); }
</style>
