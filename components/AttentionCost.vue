<template>
  <div class="attention-cost" aria-label="문맥 길이가 길어질수록 full attention 관계 수가 제곱으로 증가하는 시각화">
    <div class="growth">
      <div class="context context--small"><span>짧은 context</span><div class="grid grid--4"></div><small>N × N</small></div>
      <div class="grow-arrow"><span>context ↑</span><b>→</b></div>
      <div class="context context--large"><span>긴 context</span><div class="grid grid--9"></div><small>더 많은 token pair</small></div>
    </div>
    <div class="cost">
      <span>FULL ATTENTION</span><strong>O(N²)</strong><small>모든 token이 모든 token을 본다</small>
      <div class="burden"><i></i><b>Long Context</b><i></i><b>Long CoT</b><i></i><b>Tool History</b></div>
    </div>
  </div>
</template>

<style scoped>
.attention-cost { display:grid; grid-template-columns:1.25fr .75fr; gap:18px; height:270px; }
.growth,.cost { border:1px solid rgba(49,215,244,.34); border-radius:var(--radius-lg); background:rgba(49,215,244,.025); }
.growth { display:grid; grid-template-columns:1fr 62px 1fr; gap:12px; align-items:center; padding:19px 22px; }.context { display:grid; place-items:center; gap:9px; }.context > span { color:var(--color-text-soft); font-size:15px; font-weight:700; }.context small { color:var(--color-muted); font-size:12px; }.grid { border:1px solid rgba(49,215,244,.65); background-image:linear-gradient(rgba(49,215,244,.20) 1px,transparent 1px),linear-gradient(90deg,rgba(49,215,244,.20) 1px,transparent 1px); }.grid--4 { width:90px; height:90px; background-size:22.5px 22.5px; }.grid--9 { width:142px; height:142px; background-size:15.8px 15.8px; box-shadow:0 0 24px rgba(49,215,244,.08); }.grow-arrow { display:grid; place-items:center; color:var(--color-muted); }.grow-arrow span { font-size:10px; }.grow-arrow b { color:var(--color-architecture); font-size:27px; }
.cost { padding:24px 20px; display:flex; flex-direction:column; align-items:center; justify-content:center; text-align:center; }.cost > span { color:var(--color-muted); font:700 10px/1 ui-monospace,SFMono-Regular,Consolas,monospace; letter-spacing:.12em; }.cost > strong { color:var(--color-architecture); font:760 54px/1 ui-monospace,SFMono-Regular,Consolas,monospace; margin-top:15px; }.cost > small { color:var(--color-text-soft); font-size:14px; margin-top:11px; }.burden { width:100%; display:grid; grid-template-columns:1fr auto 1fr auto 1fr auto; gap:6px; align-items:center; margin-top:25px; color:var(--color-muted); font-size:10px; }.burden i { height:1px; background:var(--color-line); }.burden b { font-weight:600; }
</style>
