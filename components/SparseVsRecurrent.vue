<template>
  <div class="parallel" aria-label="Sparse Attention과 Linear 또는 Recurrent Attention의 병렬 long-context 전략">
    <div class="origin"><span>LONG CONTEXT</span><strong>모든 과거를 어떻게 다룰까?</strong></div>
    <div class="fork" aria-hidden="true"><i></i><i></i></div>
    <section class="strategy">
      <header><span>PARALLEL A</span><strong>Sparse Attention</strong></header>
      <div class="tokens"><i></i><i class="on"></i><i></i><i></i><i class="on"></i><i></i><i class="on"></i><i></i></div>
      <div class="read"><b>선택해서 읽기</b><small>저장된 token 중 중요한 일부</small></div>
    </section>
    <section class="strategy">
      <header><span>PARALLEL B</span><strong>Linear / Recurrent Attention</strong></header>
      <div class="compress"><div class="history"><i></i><i></i><i></i><i></i><i></i></div><b>→</b><div class="state">STATE</div></div>
      <div class="read"><b>state로 압축</b><small>과거 정보를 유한한 memory로 누적</small></div>
    </section>
  </div>
</template>

<style scoped>
.parallel { position:relative; height:276px; display:grid; grid-template-columns:1fr 1fr; grid-template-rows:64px 22px 1fr; gap:0 18px; }
.origin { grid-column:1 / 3; width:340px; justify-self:center; display:grid; place-content:center; text-align:center; border:1px solid var(--color-line); border-radius:var(--radius-md); background:var(--color-bg-raised); }.origin span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.1em; }.origin strong { color:var(--color-text); font-size:15px; margin-top:7px; }.fork { grid-column:1 / 3; display:grid; grid-template-columns:1fr 1fr; width:52%; justify-self:center; }.fork i { border-top:1px solid var(--color-architecture); }.fork i:first-child { border-left:1px solid var(--color-architecture); }.fork i:last-child { border-right:1px solid var(--color-architecture); }
.strategy { min-width:0; display:grid; grid-template-rows:52px 1fr 50px; border:1px solid rgba(49,215,244,.36); border-top:3px solid var(--color-architecture); border-radius:var(--radius-lg); background:rgba(49,215,244,.025); overflow:hidden; }.strategy header { padding:11px 16px; border-bottom:1px solid var(--color-line-soft); }.strategy header span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.1em; }.strategy header strong { color:var(--color-architecture); font-size:18px; margin-left:12px; }
.tokens { display:flex; align-items:center; justify-content:center; gap:13px; }.tokens i { width:17px; height:17px; border:1px solid var(--color-line); border-radius:50%; background:var(--color-bg-raised); }.tokens .on { border-color:var(--color-architecture); background:var(--color-architecture); box-shadow:0 0 0 5px rgba(49,215,244,.10); }.compress { display:flex; align-items:center; justify-content:center; gap:18px; }.history { display:flex; gap:6px; }.history i { width:13px; height:42px; border:1px solid rgba(49,215,244,.36); background:rgba(49,215,244,.08); }.compress > b { color:var(--color-architecture); font-size:22px; }.state { width:82px; height:58px; display:grid; place-items:center; border:1px solid var(--color-architecture); border-radius:50%; color:var(--color-architecture); font:700 11px/1 ui-monospace; }
.read { display:flex; align-items:center; justify-content:center; gap:12px; border-top:1px solid var(--color-line-soft); }.read b { color:var(--color-text); font-size:14px; }.read small { color:var(--color-muted); font-size:11px; }
</style>
