<template>
  <div class="k3-post" aria-label="세 도메인과 세 reasoning effort level의 아홉 specialist를 MOPD로 통합하는 Kimi K3 post-training">
    <section class="specialists">
      <div class="matrix-head"><span>DOMAIN × EFFORT</span><strong>9 specialist policies</strong></div>
      <div class="specialist-grid">
        <div class="blank"></div><div class="col">Low</div><div class="col">High</div><div class="col">Max</div>
        <div class="row">General</div><div class="cell"><i></i><span>G<sub>L</sub></span></div><div class="cell"><i></i><span>G<sub>H</sub></span></div><div class="cell"><i></i><span>G<sub>M</sub></span></div>
        <div class="row">Agent</div><div class="cell"><i></i><span>A<sub>L</sub></span></div><div class="cell"><i></i><span>A<sub>H</sub></span></div><div class="cell"><i></i><span>A<sub>M</sub></span></div>
        <div class="row">Coding</div><div class="cell"><i></i><span>C<sub>L</sub></span></div><div class="cell"><i></i><span>C<sub>H</sub></span></div><div class="cell"><i></i><span>C<sub>M</sub></span></div>
      </div>
    </section>

    <div class="transfer"><span>9 teachers</span><b>→</b></div>

    <section class="consolidation">
      <div class="mopd"><span>CONSOLIDATE</span><strong>Multi-Teacher<br>On-Policy Distillation</strong><small>MOPD</small></div>
      <div class="down">↓</div>
      <div class="unified"><span>ONE POLICY</span><strong>Unified Kimi K3</strong><div class="effort"><i>Low</i><i>High</i><i>Max</i></div></div>
    </section>

    <div class="concept-shift"><span>더 오래 생각하라</span><b>→</b><strong>문제에 맞게 얼마나 생각할지 학습하라</strong></div>
  </div>
</template>

<style scoped>
.k3-post { display:grid; grid-template-columns:1.16fr 62px .84fr; grid-template-rows:236px 42px; gap:10px 12px; height:288px; }
.specialists, .consolidation { border:1px solid rgba(173,124,255,.38); border-radius:var(--radius-lg); background:rgba(173,124,255,.035); overflow:hidden; }
.matrix-head { height:48px; padding:10px 15px; display:flex; align-items:baseline; justify-content:space-between; border-bottom:1px solid var(--color-line-soft); }.matrix-head span { color:var(--color-muted); font:700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing:.1em; }.matrix-head strong { color:var(--color-rl); font-size:18px; }
.specialist-grid { height:188px; padding:10px 13px 13px; display:grid; grid-template-columns:90px repeat(3,1fr); grid-template-rows:24px repeat(3,1fr); gap:6px; }.col, .row { display:grid; place-items:center; color:var(--color-muted); font-size:11px; font-weight:650; }.row { justify-content:start; color:var(--color-text-soft); font-size:13px; }.cell { min-width:0; display:flex; align-items:center; justify-content:center; gap:8px; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); }.cell i { width:8px; height:8px; border-radius:50%; background:var(--color-rl); box-shadow:0 0 0 3px rgba(173,124,255,.12); }.cell span { color:var(--color-text-soft); font:600 11px/1 ui-monospace; }
.transfer { align-self:center; display:grid; place-items:center; color:var(--color-muted); }.transfer span { font:700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing:.08em; }.transfer b { color:var(--color-rl); font-size:27px; margin-top:6px; }
.consolidation { padding:14px; display:grid; grid-template-rows:91px 17px 1fr; align-items:stretch; }.mopd, .unified { display:flex; flex-direction:column; justify-content:center; text-align:center; border:1px solid rgba(173,124,255,.42); border-radius:var(--radius-md); background:var(--color-bg-raised); }.mopd span, .unified span { color:var(--color-muted); font:700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing:.1em; }.mopd strong { color:var(--color-text); font-size:15px; line-height:1.25; margin-top:6px; }.mopd small { color:var(--color-rl); font-size:10px; margin-top:4px; }.down { color:var(--color-rl); text-align:center; line-height:17px; }.unified { border-color:var(--color-rl); }.unified strong { color:var(--color-rl); font-size:19px; margin-top:7px; }.effort { display:flex; justify-content:center; gap:5px; margin-top:9px; }.effort i { padding:3px 8px; border-radius:999px; background:rgba(173,124,255,.11); color:var(--color-text-soft); font-size:9px; font-style:normal; }
.concept-shift { grid-column:1 / 4; display:flex; align-items:center; justify-content:center; gap:13px; border-top:1px solid var(--color-line); color:var(--color-muted); font-size:14px; }.concept-shift b { color:var(--color-rl); font-size:20px; }.concept-shift strong { color:var(--color-text); font-size:16px; }
</style>
