<template>
  <div class="comparison" aria-label="답변 최적화와 추론 전략 최적화의 비교">
    <section class="panel panel--response">
      <div class="panel__head"><span>BEFORE</span><strong>Response Optimization</strong></div>
      <div class="response-flow">
        <div class="node">Prompt</div><div class="arrow">→</div><div class="node node--answer">Response</div>
      </div>
      <div class="question">“좋은 답변인가?”</div>
    </section>

    <div class="shift" aria-hidden="true"><span>SHIFT</span><b>→</b></div>

    <section class="panel panel--reasoning">
      <div class="panel__head"><span>REASONING RL</span><strong>Reasoning Optimization</strong></div>
      <div class="reasoning-flow">
        <div class="step"><i>01</i><b>Problem</b></div><span>→</span>
        <div class="step"><i>02</i><b>Try</b></div><span>→</span>
        <div class="step"><i>03</i><b>Check</b></div><span>→</span>
        <div class="step"><i>04</i><b>Revise</b></div><span>→</span>
        <div class="step step--answer"><i>05</i><b>Answer</b></div>
        <svg class="retry" viewBox="0 0 320 44" preserveAspectRatio="none" aria-hidden="true">
          <path d="M244 3 C238 40 110 40 104 6" />
          <path d="M99 11 L104 5 L111 11" />
        </svg>
      </div>
      <div class="question">“정답에 도달하는 전략인가?”</div>
    </section>
  </div>
</template>

<style scoped>
.comparison { display: grid; grid-template-columns: .88fr 64px 1.42fr; gap: 14px; align-items: stretch; height: 274px; }
.panel { border: 1px solid var(--color-line); border-radius: var(--radius-lg); background: var(--color-surface); padding: 20px; display: flex; flex-direction: column; }
.panel--response { border-top: 3px solid #78869a; }.panel--reasoning { border-top: 3px solid var(--color-rl); background: rgba(173,124,255,.045); }
.panel__head { display: flex; align-items: baseline; justify-content: space-between; gap: 10px; }
.panel__head span { color: var(--color-muted); font: 700 10px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing: .12em; }
.panel__head strong { color: var(--color-text); font-size: 18px; }
.response-flow { flex: 1; display: flex; align-items: center; justify-content: center; gap: 12px; }
.node { min-width: 92px; padding: 16px 12px; text-align: center; color: var(--color-text-soft); font-size: 16px; font-weight: 680; border: 1px solid var(--color-line); border-radius: var(--radius-md); background: var(--color-bg-raised); }
.node--answer { border-color: #647187; color: var(--color-text); }.arrow { color: var(--color-muted); font-size: 24px; }
.question { padding-top: 14px; border-top: 1px solid var(--color-line-soft); text-align: center; color: var(--color-text); font-size: 20px; font-weight: 740; }
.panel--reasoning .question { color: var(--color-rl); }
.shift { align-self: center; display: grid; place-items: center; color: var(--color-muted); }
.shift span { font: 700 10px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing: .12em; }.shift b { color: var(--color-rl); font-size: 30px; margin-top: 6px; }
.reasoning-flow { position: relative; flex: 1; display: grid; grid-template-columns: repeat(4, minmax(0,1fr) auto) minmax(0,1fr); align-items: center; gap: 5px; padding-bottom: 32px; }
.reasoning-flow > span { color: rgba(173,124,255,.62); font-size: 17px; }
.step { position: relative; z-index: 1; height: 66px; display: grid; place-content: center; gap: 5px; text-align: center; border: 1px solid rgba(173,124,255,.34); border-radius: var(--radius-md); background: var(--color-bg-raised); }
.step i { color: var(--color-muted); font: 700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; font-style: normal; }.step b { color: var(--color-text-soft); font-size: 14px; }.step--answer { border-color: var(--color-rl); }.step--answer b { color: var(--color-rl); }
.retry { position: absolute; left: 66px; right: 44px; bottom: 3px; width: calc(100% - 110px); height: 42px; overflow: visible; }
.retry path { fill: none; stroke: rgba(173,124,255,.62); stroke-width: 1.5; vector-effect: non-scaling-stroke; }
</style>
