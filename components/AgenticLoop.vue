<template>
  <div class="agentic" aria-label="Reason, Act, Observe, Verify, Retry 순환과 외부 도구를 연결하는 agentic loop">
    <div class="tools tools--left"><span>Search</span><span>Python</span><span>Database</span></div>
    <div class="loop">
      <svg viewBox="0 0 430 210" aria-hidden="true">
        <defs><marker id="agent-arrow" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" /></marker></defs>
        <path d="M215 20 C316 20 381 65 380 106" /><path d="M380 106 C380 164 309 190 259 189" /><path d="M259 189 C176 204 88 170 65 129" /><path d="M65 129 C39 76 108 24 171 20" />
      </svg>
      <div class="loop__center"><span>INTERACTION</span><strong>Trajectory</strong><small>환경의 결과가 다음 판단을 바꾼다</small></div>
      <div class="step step--reason"><i>01</i><b>Reason</b></div>
      <div class="step step--act"><i>02</i><b>Act</b></div>
      <div class="step step--observe"><i>03</i><b>Observe</b></div>
      <div class="step step--verify"><i>04</i><b>Verify</b></div>
      <div class="step step--retry"><i>05</i><b>Retry</b></div>
    </div>
    <div class="tools tools--right"><span>API</span><span>Files</span><span>External environment</span></div>
    <div class="policy-evolution">
      <div><small>01</small><strong>Token Policy</strong></div><b>→</b>
      <div><small>02</small><strong>Reasoning Policy</strong></div><b>→</b>
      <div class="active"><small>03</small><strong>Action Policy</strong></div>
    </div>
  </div>
</template>

<style scoped>
.agentic { height:294px; display:grid; grid-template-columns:126px 1fr 145px; grid-template-rows:236px 48px; gap:10px 14px; align-items:center; }
.tools { display:flex; flex-direction:column; gap:11px; }.tools span { padding:10px 11px; border:1px solid rgba(255,180,84,.36); border-radius:var(--radius-sm); background:rgba(255,180,84,.035); color:var(--color-text-soft); font-size:12px; font-weight:650; text-align:center; }.tools--left span::after { content:"  →"; color:var(--color-agency); }.tools--right span::before { content:"←  "; color:var(--color-agency); }
.loop { position:relative; height:236px; }.loop svg { position:absolute; inset:0; width:100%; height:100%; overflow:visible; }.loop svg path { fill:none; stroke:rgba(255,180,84,.62); stroke-width:1.8; marker-end:url(#agent-arrow); vector-effect:non-scaling-stroke; }.loop svg marker path { fill:var(--color-agency); stroke:none; }
.loop__center { position:absolute; left:50%; top:51%; transform:translate(-50%,-50%); width:184px; height:92px; display:flex; flex-direction:column; align-items:center; justify-content:center; text-align:center; border:1px solid var(--color-line); border-radius:50%; background:var(--color-bg-raised); }.loop__center span { color:var(--color-muted); font:700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing:.1em; }.loop__center strong { color:var(--color-agency); font-size:20px; margin-top:7px; }.loop__center small { color:var(--color-muted); font-size:9px; margin-top:5px; }
.step { position:absolute; z-index:1; width:91px; height:48px; display:flex; align-items:center; justify-content:center; gap:7px; border:1px solid rgba(255,180,84,.5); border-radius:var(--radius-md); background:var(--color-surface); box-shadow:0 0 0 4px var(--color-bg); }.step i { color:var(--color-muted); font:700 9px/1 ui-monospace; font-style:normal; }.step b { color:var(--color-text); font-size:14px; }.step--reason { left:50%; top:0; transform:translateX(-50%); }.step--act { right:2px; top:64px; }.step--observe { right:48px; bottom:0; }.step--verify { left:48px; bottom:0; }.step--retry { left:2px; top:64px; }
.policy-evolution { grid-column:1 / 4; height:48px; display:grid; grid-template-columns:1fr auto 1fr auto 1fr; gap:14px; align-items:center; padding:0 18px; border:1px solid var(--color-line); border-radius:var(--radius-md); background:var(--color-bg-raised); }.policy-evolution div { display:flex; align-items:center; justify-content:center; gap:10px; }.policy-evolution small { color:var(--color-muted); font:700 9px/1 ui-monospace; }.policy-evolution strong { color:var(--color-text-soft); font-size:14px; }.policy-evolution > b { color:var(--color-agency); }.policy-evolution .active strong { color:var(--color-agency); }
</style>
