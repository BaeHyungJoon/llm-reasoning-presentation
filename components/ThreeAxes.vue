<template>
  <div class="axes" aria-label="Architecture, Post-training, Inference-time Compute가 Better Reasoning으로 수렴하는 세 축">
    <div class="axis axis--arch">
      <div class="axis__index">01</div>
      <div class="axis__title">Architecture</div>
      <div class="axis__desc">더 효율적으로 계산</div>
      <div class="axis__signal"><span></span><span></span><span></span></div>
    </div>
    <div class="axis axis--rl">
      <div class="axis__index">02</div>
      <div class="axis__title">Post-training</div>
      <div class="axis__desc">더 좋은 사고 전략 학습</div>
      <div class="axis__signal"><span></span><span></span><span></span></div>
    </div>
    <div class="axis axis--agency">
      <div class="axis__index">03</div>
      <div class="axis__title">Inference-time Compute</div>
      <div class="axis__desc">필요한 만큼 탐색·검증·행동</div>
      <div class="axis__signal"><span></span><span></span><span></span></div>
    </div>

    <svg class="axes__links" viewBox="0 0 864 96" preserveAspectRatio="none" aria-hidden="true">
      <path class="link link--arch" d="M142 2 C142 52 300 50 432 92" />
      <path class="link link--rl" d="M432 2 L432 92" />
      <path class="link link--agency" d="M722 2 C722 52 564 50 432 92" />
    </svg>

    <div class="reasoning">
      <span class="reasoning__kicker">COMBINED SYSTEM</span>
      <strong>Better Reasoning</strong>
      <div class="reasoning__bars"><i></i><i></i><i></i></div>
    </div>
  </div>
</template>

<style scoped>
.axes { position: relative; display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; height: 286px; padding-bottom: 100px; }
.axis { position: relative; min-width: 0; padding: 18px 20px 16px; border: 1px solid var(--color-line); border-top: 3px solid var(--tone); border-radius: var(--radius-lg); background: var(--color-surface); }
.axis--arch { --tone: var(--color-architecture); --wash: rgba(49,215,244,.12); }
.axis--rl { --tone: var(--color-rl); --wash: rgba(173,124,255,.12); }
.axis--agency { --tone: var(--color-agency); --wash: rgba(255,180,84,.12); }
.axis__index { color: var(--tone); font: 700 12px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing: .1em; }
.axis__title { color: var(--tone); font-size: 21px; line-height: 1.15; font-weight: 760; margin-top: 12px; }
.axis__desc { color: var(--color-text-soft); font-size: 15px; line-height: 1.35; margin-top: 8px; }
.axis__signal { position: absolute; right: 18px; top: 18px; display: flex; align-items: end; gap: 4px; height: 25px; }
.axis__signal span { width: 4px; border-radius: 2px; background: var(--tone); opacity: .78; }
.axis__signal span:nth-child(1) { height: 8px; opacity: .35; }.axis__signal span:nth-child(2) { height: 16px; opacity: .55; }.axis__signal span:nth-child(3) { height: 24px; }
.axes__links { position: absolute; left: 0; right: 0; bottom: 72px; width: 100%; height: 96px; overflow: visible; }
.link { fill: none; stroke-width: 2; vector-effect: non-scaling-stroke; }
.link--arch { stroke: var(--color-architecture); }.link--rl { stroke: var(--color-rl); }.link--agency { stroke: var(--color-agency); }
.reasoning { position: absolute; bottom: 0; left: 50%; transform: translateX(-50%); width: 330px; height: 76px; display: grid; place-content: center; text-align: center; border: 1px solid var(--color-line); border-radius: var(--radius-lg); background: var(--color-bg-raised); box-shadow: 0 0 0 5px var(--color-bg); }
.reasoning__kicker { color: var(--color-muted); font: 700 10px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing: .16em; margin-bottom: 8px; }
.reasoning strong { color: var(--color-text); font-size: 25px; line-height: 1; }
.reasoning__bars { position: absolute; inset: auto 22px 0; display: grid; grid-template-columns: repeat(3, 1fr); gap: 5px; transform: translateY(1px); }
.reasoning__bars i { height: 3px; }.reasoning__bars i:nth-child(1) { background: var(--color-architecture); }.reasoning__bars i:nth-child(2) { background: var(--color-rl); }.reasoning__bars i:nth-child(3) { background: var(--color-agency); }
</style>
