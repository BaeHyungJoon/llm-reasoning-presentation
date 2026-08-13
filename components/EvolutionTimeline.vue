<script setup lang="ts">
withDefaults(defineProps<{ variant?: 'cover' | 'question' }>(), { variant: 'question' })
</script>

<template>
  <div class="evolution" :class="`evolution--${variant}`" aria-label="Prediction에서 Instruction Following, Reasoning, Acting으로 이어지는 발전 흐름">
    <div class="rail" aria-hidden="true"><i></i><i></i><i></i></div>
    <div class="stage stage--prediction"><span>01</span><strong>Prediction</strong><small>다음 token</small></div>
    <div class="stage stage--instruction"><span>02</span><strong>Instruction Following</strong><small>사용자 의도</small></div>
    <div class="stage stage--reasoning"><span>03</span><strong>Reasoning</strong><small>검증·수정</small></div>
    <div class="stage stage--acting"><span>04</span><strong>Acting</strong><small>도구·환경</small></div>
  </div>
</template>

<style scoped>
.evolution { position:relative; display:grid; grid-template-columns:repeat(4,1fr); gap:18px; height:166px; align-items:center; }
.rail { position:absolute; left:10%; right:10%; top:50%; display:grid; grid-template-columns:repeat(3,1fr); transform:translateY(-50%); }.rail i { height:2px; background:var(--color-line); position:relative; }.rail i::after { content:""; position:absolute; right:-1px; top:-3px; width:8px; height:8px; border-top:2px solid currentColor; border-right:2px solid currentColor; transform:rotate(45deg); }.rail i:nth-child(1) { color:var(--color-rl); background:linear-gradient(90deg,var(--color-line),var(--color-rl)); }.rail i:nth-child(2) { color:var(--color-rl); background:var(--color-rl); }.rail i:nth-child(3) { color:var(--color-agency); background:linear-gradient(90deg,var(--color-rl),var(--color-agency)); }
.stage { position:relative; z-index:1; min-width:0; height:112px; padding:17px 16px; display:flex; flex-direction:column; justify-content:center; border:1px solid var(--color-line); border-top:3px solid var(--tone); border-radius:var(--radius-lg); background:var(--color-surface); box-shadow:0 0 0 5px var(--color-bg); }
.stage--prediction { --tone:#8492a6; }.stage--instruction,.stage--reasoning { --tone:var(--color-rl); }.stage--acting { --tone:var(--color-agency); }
.stage span { color:var(--tone); font:700 10px/1 ui-monospace,SFMono-Regular,Consolas,monospace; letter-spacing:.1em; }.stage strong { color:var(--color-text); font-size:18px; line-height:1.15; margin-top:10px; }.stage small { color:var(--color-muted); font-size:12px; margin-top:7px; }
.evolution--cover { height:104px; gap:12px; }.evolution--cover .stage { height:76px; padding:12px 14px; border-top-width:2px; }.evolution--cover .stage span { display:none; }.evolution--cover .stage strong { font-size:15px; margin:0; }.evolution--cover .stage small { font-size:10px; margin-top:5px; }
</style>
