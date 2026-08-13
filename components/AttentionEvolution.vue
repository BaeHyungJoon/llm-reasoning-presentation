<template>
  <div class="kv-evolution" aria-label="MHA에서 MQA, GQA, MLA로 이어지는 KV cache 공유와 압축의 직관">
    <div class="kv-card kv-card--mha"><header><span>01</span><strong>MHA</strong></header><div class="heads"><i>Q₁</i><i>Q₂</i><i>Q₃</i><i>Q₄</i></div><div class="cache"><b></b><b></b><b></b><b></b></div><footer>head마다 K/V</footer></div>
    <div class="kv-arrow">→</div>
    <div class="kv-card"><header><span>02</span><strong>MQA</strong></header><div class="heads"><i>Q₁</i><i>Q₂</i><i>Q₃</i><i>Q₄</i></div><div class="cache cache--shared"><b></b></div><footer>하나의 K/V 공유</footer></div>
    <div class="kv-arrow">→</div>
    <div class="kv-card"><header><span>03</span><strong>GQA</strong></header><div class="heads"><i>Q₁</i><i>Q₂</i><i>Q₃</i><i>Q₄</i></div><div class="cache cache--group"><b></b><b></b></div><footer>그룹별 K/V 공유</footer></div>
    <div class="kv-arrow">→</div>
    <div class="kv-card kv-card--mla"><header><span>04</span><strong>MLA</strong></header><div class="heads"><i>Q₁</i><i>Q₂</i><i>Q₃</i><i>Q₄</i></div><div class="latent">latent<br>representation</div><footer>K/V를 latent로 압축</footer></div>
    <div class="cache-axis"><span>KV cache 구조</span><i></i><strong>공유 · 압축</strong></div>
  </div>
</template>

<style scoped>
.kv-evolution { position:relative; height:274px; display:grid; grid-template-columns:1fr 24px 1fr 24px 1fr 24px 1fr; grid-template-rows:230px 34px; gap:10px 6px; align-items:stretch; }
.kv-card { min-width:0; display:grid; grid-template-rows:46px 58px 1fr 39px; border:1px solid rgba(49,215,244,.32); border-radius:var(--radius-lg); background:rgba(49,215,244,.025); overflow:hidden; }.kv-card--mla { border-color:var(--color-architecture); }
header { padding:12px 14px; display:flex; align-items:baseline; gap:8px; border-bottom:1px solid var(--color-line-soft); } header span { color:var(--color-muted); font:700 9px/1 ui-monospace; } header strong { color:var(--color-architecture); font-size:20px; }
.heads { display:grid; grid-template-columns:repeat(4,1fr); gap:5px; padding:12px 10px 8px; }.heads i { display:grid; place-items:center; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); color:var(--color-text-soft); font:600 10px/1 ui-monospace; font-style:normal; }
.cache { display:grid; grid-template-columns:repeat(4,1fr); gap:5px; padding:9px 10px 14px; }.cache b { border:1px solid rgba(49,215,244,.5); border-radius:3px; background:rgba(49,215,244,.12); }.cache--shared { grid-template-columns:1fr; padding-inline:36px; }.cache--group { grid-template-columns:repeat(2,1fr); padding-inline:23px; }.latent { align-self:center; justify-self:center; width:80px; padding:12px 8px; text-align:center; border:1px solid var(--color-architecture); border-radius:999px; background:rgba(49,215,244,.10); color:var(--color-architecture); font:650 11px/1.25 ui-monospace; }
footer { display:grid; place-items:center; border-top:1px solid var(--color-line-soft); color:var(--color-text-soft); font-size:12px; }.kv-arrow { align-self:center; color:var(--color-architecture); font-size:21px; text-align:center; }
.cache-axis { grid-column:1 / 8; display:grid; grid-template-columns:auto 1fr auto; gap:12px; align-items:center; padding:0 12px; color:var(--color-muted); font-size:11px; }.cache-axis i { height:2px; background:linear-gradient(90deg,var(--color-line),var(--color-architecture)); }.cache-axis strong { color:var(--color-architecture); }
</style>
