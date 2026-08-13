<template>
  <div class="objective-gap" aria-label="다음 token 예측 목표와 사용자 의도 충족 목표의 차이">
    <section class="objective objective--prediction">
      <header><span>PRETRAINING OBJECTIVE</span><strong>다음 token을 예측</strong></header>
      <div class="continuation"><span>비가 오면 우산을</span><b>쓴다</b><i>챙긴다</i><i>사용한다</i></div>
      <footer>그럴듯한 다음 말</footer>
    </section>
    <div class="not-equal"><b>≠</b><span>목표가 다르다</span></div>
    <section class="objective objective--intent">
      <header><span>USER INTENT</span><strong>질문에 유용하게 답하기</strong></header>
      <div class="instruction"><span>“내 상황에 맞는 선택을 알려줘”</span><div><i>지시 이해</i><b>→</b><i>관련 답변</i></div></div>
      <footer>사용자가 원하는 행동</footer>
    </section>
  </div>
</template>

<style scoped>
.objective-gap { height:270px; display:grid; grid-template-columns:1fr 76px 1fr; gap:14px; }
.objective { display:grid; grid-template-rows:65px 1fr 42px; border:1px solid var(--color-line); border-top:3px solid var(--tone); border-radius:var(--radius-lg); background:var(--tone-bg); overflow:hidden; }.objective--prediction { --tone:#8492a6; --tone-bg:var(--color-surface); }.objective--intent { --tone:var(--color-rl); --tone-bg:rgba(173,124,255,.035); }
header { padding:14px 18px; border-bottom:1px solid var(--color-line-soft); }.objective header span { color:var(--color-muted); font:700 9px/1 ui-monospace; letter-spacing:.1em; }.objective header strong { display:block; color:var(--tone); font-size:19px; margin-top:8px; }.objective footer { display:grid; place-items:center; border-top:1px solid var(--color-line-soft); color:var(--color-muted); font-size:12px; }
.continuation { display:flex; flex-wrap:wrap; align-content:center; justify-content:center; gap:9px; padding:25px; }.continuation span { flex-basis:100%; color:var(--color-text-soft); font-size:18px; text-align:center; }.continuation b,.continuation i { padding:9px 12px; border:1px solid var(--color-line); border-radius:var(--radius-sm); color:var(--color-muted); font-size:12px; font-style:normal; }.continuation b { border-color:#8492a6; color:var(--color-text); }.instruction { display:grid; place-content:center; gap:22px; text-align:center; }.instruction > span { color:var(--color-text); font-size:17px; font-weight:650; }.instruction div { display:flex; align-items:center; justify-content:center; gap:10px; }.instruction i { padding:10px 13px; border:1px solid rgba(173,124,255,.4); border-radius:var(--radius-sm); color:var(--color-text-soft); font-size:12px; font-style:normal; }.instruction b { color:var(--color-rl); }.not-equal { display:grid; place-content:center; text-align:center; }.not-equal b { color:var(--color-text); font-size:43px; }.not-equal span { color:var(--color-muted); font-size:10px; margin-top:8px; }
</style>
