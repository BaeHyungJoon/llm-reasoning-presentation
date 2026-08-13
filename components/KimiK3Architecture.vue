<template>
  <div class="k3-architecture" aria-label="Kimi K3의 Sequence, Depth, Width 정보 흐름">
    <section class="axis-card">
      <header><span>01 · TOKEN</span><strong>Sequence</strong></header>
      <div class="sequence-visual">
        <div class="tokens"><i>t₁</i><i>t₂</i><i>t₃</i><i>t₄</i></div>
        <div class="memory"><span>Recurrent memory</span><b>↻</b></div>
        <div class="gate"><i></i><span>Gated global path</span></div>
      </div>
      <footer><b>KDA</b><span>+</span><b>Gated MLA</b></footer>
    </section>

    <section class="axis-card">
      <header><span>02 · LAYER</span><strong>Depth</strong></header>
      <div class="depth-visual">
        <div class="layers"><i>L1</i><i>L2</i><i>L3</i><i>L4</i></div>
        <svg viewBox="0 0 210 106" preserveAspectRatio="none" aria-hidden="true">
          <path d="M25 86 C82 86 84 53 180 53" /><path d="M25 20 C90 20 110 86 180 86" /><path class="direct" d="M25 53 L180 53" />
        </svg>
        <div class="reuse">이전 표현을 선택적으로 재사용</div>
      </div>
      <footer><b>Attention Residuals</b></footer>
    </section>

    <section class="axis-card">
      <header><span>03 · EXPERT</span><strong>Width</strong></header>
      <div class="width-visual">
        <div class="router">Router</div>
        <div class="route-lines"><i></i><i></i><i></i><i></i></div>
        <div class="experts"><span>E1</span><span class="on">E2</span><span>E3</span><span class="on">E4</span></div>
        <div class="selection">필요한 expert로 routing</div>
      </div>
      <footer><b>Stable LatentMoE</b></footer>
    </section>
  </div>
</template>

<style scoped>
.k3-architecture { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; height: 278px; }
.axis-card { min-width: 0; display: grid; grid-template-rows: auto 1fr auto; border: 1px solid rgba(49,215,244,.34); border-top: 3px solid var(--color-architecture); border-radius: var(--radius-lg); background: rgba(49,215,244,.035); overflow: hidden; }
header { padding: 15px 17px 12px; border-bottom: 1px solid var(--color-line-soft); }
header span { display: block; color: var(--color-muted); font: 700 10px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing: .11em; } header strong { display: block; color: var(--color-architecture); font-size: 21px; margin-top: 8px; }
footer { min-height: 43px; display: flex; justify-content: center; align-items: center; gap: 8px; padding: 9px 12px; border-top: 1px solid var(--color-line-soft); color: var(--color-muted); font-size: 13px; }
footer b { color: var(--color-text); font-size: 14px; }
.sequence-visual, .depth-visual, .width-visual { position: relative; min-height: 0; padding: 13px 16px; }
.tokens { display: flex; justify-content: space-between; position: relative; }.tokens::before { content:""; position:absolute; left:14px; right:14px; top:16px; height:1px; background:rgba(49,215,244,.48); }
.tokens i { position: relative; display: grid; place-items: center; width: 32px; height: 32px; border: 1px solid rgba(49,215,244,.55); border-radius: 50%; background: var(--color-bg-raised); color: var(--color-text-soft); font: 600 12px/1 ui-monospace; font-style: normal; }
.memory { margin: 13px auto 0; width: 78%; height: 48px; display: flex; justify-content: center; align-items: center; gap: 12px; border: 1px solid var(--color-line); border-radius: 999px; background: var(--color-bg-raised); }.memory span { color: var(--color-text-soft); font-size: 12px; }.memory b { color: var(--color-architecture); font-size: 23px; }
.gate { display: flex; align-items: center; justify-content: center; gap: 8px; margin-top: 10px; color: var(--color-muted); font-size: 11px; }.gate i { width: 22px; height: 5px; border-radius: 3px; background: var(--color-architecture); }
.layers { position: absolute; inset: 13px 16px 40px; display: flex; flex-direction: column-reverse; justify-content: space-between; }.layers i { position: relative; z-index: 1; width: 38px; padding: 5px 0; text-align: center; border: 1px solid var(--color-line); border-radius: var(--radius-sm); background: var(--color-bg-raised); color: var(--color-text-soft); font: 600 11px/1 ui-monospace; font-style: normal; }
.depth-visual svg { position: absolute; left: 45px; right: 18px; top: 16px; width: calc(100% - 63px); height: 105px; }.depth-visual path { fill:none; stroke:rgba(49,215,244,.4); stroke-width:1.4; vector-effect:non-scaling-stroke; }.depth-visual .direct { stroke:var(--color-architecture); }
.reuse, .selection { position: absolute; left: 60px; right: 12px; bottom: 12px; color: var(--color-muted); font-size: 11px; text-align: center; }
.router { width: 76px; margin: 0 auto; padding: 8px; text-align: center; border: 1px solid var(--color-architecture); border-radius: var(--radius-sm); color: var(--color-architecture); font-size: 13px; font-weight: 720; background: var(--color-bg-raised); }
.route-lines { height: 28px; width: 78%; margin: 0 auto; display: grid; grid-template-columns:repeat(4,1fr); border-top: 1px solid rgba(49,215,244,.45); transform: translateY(15px); }.route-lines i { width:1px; height:16px; background:rgba(49,215,244,.42); justify-self:center; }
.experts { display:grid; grid-template-columns:repeat(4,1fr); gap:7px; margin-top:2px; }.experts span { display:grid; place-items:center; height:39px; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); color:var(--color-muted); font:600 11px/1 ui-monospace; }.experts .on { color:var(--color-architecture); border-color:var(--color-architecture); background:rgba(49,215,244,.08); }
.selection { left:12px; }
</style>
