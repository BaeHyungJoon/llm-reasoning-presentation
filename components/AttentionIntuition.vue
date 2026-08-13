<template>
  <div class="attention-intuition" aria-label="한국어 문장에서 한 token이 다른 token 정보를 참고하는 attention 직관">
    <div class="sentence">
      <span>모델은</span><span>긴</span><span>문맥에서</span><span class="focus">중요한</span><span>정보를</span><span>찾는다</span>
      <svg viewBox="0 0 760 120" preserveAspectRatio="none" aria-hidden="true">
        <path class="weak" d="M475 95 C430 35 140 35 92 94" />
        <path d="M475 95 C465 42 360 42 335 94" />
        <path class="strong" d="M475 95 C490 45 585 45 614 94" />
      </svg>
    </div>
    <div class="legend"><span><i class="query"></i>지금 찾는 정보</span><span><i class="relation"></i>참고할 token 관계</span></div>
    <div class="attention-equation">Attention(Q,K,V) = softmax(QK<sup>T</sup> / √d<sub>k</sub>)V</div>
  </div>
</template>

<style scoped>
.attention-intuition { height:276px; display:grid; grid-template-rows:1fr 32px 45px; border:1px solid rgba(49,215,244,.34); border-radius:var(--radius-lg); background:rgba(49,215,244,.025); overflow:hidden; }
.sentence { position:relative; display:flex; align-items:flex-end; justify-content:center; gap:14px; padding:34px 20px 36px; }.sentence > span { position:relative; z-index:1; padding:12px 13px; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); color:var(--color-text-soft); font-size:18px; font-weight:650; }.sentence .focus { color:var(--color-architecture); border-color:var(--color-architecture); box-shadow:0 0 0 4px rgba(49,215,244,.08); }.sentence svg { position:absolute; left:10%; right:10%; top:18px; width:80%; height:118px; }.sentence path { fill:none; stroke:rgba(49,215,244,.55); stroke-width:2; vector-effect:non-scaling-stroke; }.sentence .weak { opacity:.42; }.sentence .strong { stroke-width:3; stroke:var(--color-architecture); }
.legend { display:flex; justify-content:center; gap:28px; color:var(--color-muted); font-size:12px; }.legend span { display:flex; align-items:center; gap:8px; }.legend i { display:inline-block; width:18px; height:4px; border-radius:2px; }.query { background:var(--color-architecture); }.relation { background:rgba(49,215,244,.45); }
.attention-equation { display:flex; align-items:center; justify-content:center; white-space:nowrap; border-top:1px solid var(--color-line-soft); color:var(--color-muted); font:600 15px/1 ui-monospace,SFMono-Regular,Consolas,monospace; }
</style>
