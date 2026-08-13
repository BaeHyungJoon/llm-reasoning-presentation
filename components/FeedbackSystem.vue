<template>
  <div class="feedback-system" aria-label="GPT-4 System Card에 기록된 다양한 post-training과 deployment feedback 및 safety inputs">
    <div class="sources">
      <div><span>01</span><strong>Human feedback</strong></div>
      <div><span>02</span><strong>Safety fine-tuning</strong></div>
      <div><span>03</span><strong>Prior-use data</strong></div>
      <div><span>04</span><strong>Classifiers</strong></div>
      <div><span>05</span><strong>Expert red teaming</strong></div>
      <div><span>06</span><strong>Adversarial testing</strong></div>
    </div>
    <div class="convergence" aria-hidden="true"><i></i><i></i><i></i><i></i><i></i><i></i></div>
    <div class="target"><span>BROADER SYSTEM</span><strong>Post-training + Deployment Preparation</strong><small>선호 비교 하나만으로 끝나지 않는다</small></div>
  </div>
</template>

<style scoped>
.feedback-system { height:272px; display:grid; grid-template-rows:116px 54px 1fr; }.sources { display:grid; grid-template-columns:repeat(3,1fr); gap:10px 13px; }.sources div { padding:12px 14px; display:flex; align-items:center; gap:11px; border:1px solid rgba(173,124,255,.32); border-radius:var(--radius-sm); background:var(--color-surface); }.sources span { color:var(--color-rl); font:700 9px/1 ui-monospace; }.sources strong { color:var(--color-text-soft); font-size:13px; }.convergence { width:78%; justify-self:center; display:grid; grid-template-columns:repeat(6,1fr); border-bottom:1px solid rgba(173,124,255,.5); }.convergence i { justify-self:center; width:1px; height:41px; background:rgba(173,124,255,.42); }.target { width:54%; justify-self:center; padding:13px 20px; display:flex; align-items:center; justify-content:center; gap:14px; border:1px solid var(--color-rl); border-top:3px solid var(--color-rl); border-radius:var(--radius-lg); background:rgba(173,124,255,.055); }.target span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.08em; }.target strong { color:var(--color-rl); font-size:17px; }.target small { color:var(--color-muted); font-size:10px; }
</style>
