<template>
  <div class="optimizer-comparison" aria-label="PPO와 GRPO의 advantage estimation 비교">
    <section class="optimizer optimizer--ppo">
      <header><div><span>LEARNED BASELINE</span><strong>PPO</strong></div><em>별도 Critic</em></header>
      <div class="ppo-flow">
        <div class="flow-node policy">Policy</div><div class="flow-arrow">→</div><div class="flow-node response">Response</div>
        <div class="merge merge--ppo">
          <div><span>Reward</span><b>r</b></div>
          <div class="critic"><span>Critic / Value</span><b>V(s)</b></div>
        </div>
        <div class="down">↓</div>
        <div class="flow-node advantage">Advantage<br><small>기대값 대비 얼마나 좋은가</small></div>
        <div class="down">↓</div>
        <div class="flow-node update">Policy update</div>
      </div>
    </section>

    <section class="optimizer optimizer--grpo">
      <header><div><span>GROUP-RELATIVE BASELINE</span><strong>GRPO</strong></div><em>Critic 불필요</em></header>
      <div class="grpo-flow">
        <div class="prompt">One prompt</div>
        <div class="fanout"><i></i><i></i><i></i><i></i></div>
        <div class="rollouts">
          <div><span>Rollout 1</span><b>r₁</b></div><div><span>Rollout 2</span><b>r₂</b></div><div><span>Rollout 3</span><b>r₃</b></div><div><span>Rollout G</span><b>r<sub>G</sub></b></div>
        </div>
        <div class="down">↓</div>
        <div class="group-stat"><span>Group statistics</span><b>mean · std</b></div>
        <div class="flow-arrow">→</div>
        <div class="relative"><span>Relative advantage</span><b>같은 문제의 답들과 비교</b></div>
        <div class="flow-arrow">→</div>
        <div class="flow-node update">Policy update</div>
      </div>
    </section>

    <div class="equation-band"><span>Group-relative advantage</span><strong>A<sub>i</sub> = (r<sub>i</sub> − mean(r<sub>1</sub>, …, r<sub>G</sub>)) / std(r<sub>1</sub>, …, r<sub>G</sub>)</strong></div>
  </div>
</template>

<style scoped>
.optimizer-comparison { display:grid; grid-template-columns:.9fr 1.1fr; grid-template-rows:238px 42px; gap:10px 14px; height:290px; }
.optimizer { min-width:0; border:1px solid var(--color-line); border-radius:var(--radius-lg); background:var(--color-surface); overflow:hidden; }.optimizer--grpo { border-color:rgba(173,124,255,.50); background:rgba(173,124,255,.04); }
header { height:48px; padding:10px 14px; display:flex; align-items:center; justify-content:space-between; border-bottom:1px solid var(--color-line-soft); }
header div { display:flex; align-items:baseline; gap:9px; } header span { color:var(--color-muted); font:700 9px/1 ui-monospace, SFMono-Regular, Consolas, monospace; letter-spacing:.08em; } header strong { color:var(--color-text); font-size:22px; } .optimizer--grpo header strong { color:var(--color-rl); }
header em { padding:5px 9px; border:1px solid var(--color-line); border-radius:999px; color:var(--color-muted); font-size:10px; font-style:normal; }.optimizer--grpo header em { border-color:rgba(173,124,255,.5); color:var(--color-rl); }
.ppo-flow { height:188px; display:grid; grid-template-columns:1fr 20px 1fr; grid-template-rows:31px 42px 7px 37px 7px 29px; gap:3px 7px; padding:8px 12px; align-items:center; }
.flow-node { display:grid; place-items:center; min-width:0; height:100%; padding:5px 8px; text-align:center; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); color:var(--color-text-soft); font-size:12px; font-weight:700; }.flow-node small { color:var(--color-muted); font-size:9px; font-weight:500; margin-top:3px; }
.policy { grid-column:1; }.ppo-flow > .flow-arrow { grid-column:2; grid-row:1; }.response { grid-column:3; }.merge { grid-column:1 / 4; display:grid; grid-template-columns:1fr 1fr; gap:8px; }.merge div { height:40px; padding:6px 10px; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); display:flex; align-items:center; justify-content:space-between; }.merge span { color:var(--color-muted); font-size:10px; }.merge b { color:var(--color-text); font:700 14px/1 ui-monospace; }.merge .critic { border-color:rgba(173,124,255,.45); }.merge .critic b { color:var(--color-rl); }
.down { color:rgba(173,124,255,.65); text-align:center; line-height:1; }.ppo-flow .down { grid-column:1 / 4; }.advantage { grid-column:1 / 4; border-color:rgba(173,124,255,.45); display:flex; align-items:center; justify-content:center; gap:8px; }.advantage br { display:none; }.advantage small { margin-top:0; }.update { border-color:var(--color-rl); color:var(--color-rl); }.ppo-flow .update { grid-column:1 / 4; }.flow-arrow { color:var(--color-rl); text-align:center; }
.grpo-flow { height:190px; padding:8px 10px; display:grid; grid-template-columns:1fr 18px 1.13fr 18px .9fr; grid-template-rows:29px 16px 43px 10px 39px 35px; gap:3px 5px; align-items:center; }
.prompt { grid-column:1 / 6; justify-self:center; min-width:120px; padding:7px 12px; text-align:center; border:1px solid rgba(173,124,255,.45); border-radius:var(--radius-sm); background:var(--color-bg-raised); color:var(--color-text); font-size:11px; font-weight:700; }
.fanout { grid-column:1 / 6; width:72%; height:16px; justify-self:center; display:grid; grid-template-columns:repeat(4,1fr); border-top:1px solid rgba(173,124,255,.4); }.fanout i { justify-self:center; width:1px; height:13px; background:rgba(173,124,255,.4); }
.rollouts { grid-column:1 / 6; display:grid; grid-template-columns:repeat(4,1fr); gap:6px; }.rollouts div { min-width:0; height:43px; padding:5px 7px; border:1px solid var(--color-line); border-radius:var(--radius-sm); background:var(--color-bg-raised); display:flex; align-items:center; justify-content:space-between; }.rollouts span { color:var(--color-muted); font-size:9px; }.rollouts b { color:var(--color-rl); font:700 12px/1 ui-monospace; }
.grpo-flow > .down { grid-column:1 / 6; }.group-stat, .relative { height:39px; padding:5px 8px; border:1px solid rgba(173,124,255,.4); border-radius:var(--radius-sm); background:var(--color-bg-raised); display:flex; flex-direction:column; justify-content:center; text-align:center; }.group-stat { grid-column:1; }.relative { grid-column:3; }.group-stat span, .relative span { color:var(--color-muted); font-size:8px; }.group-stat b, .relative b { color:var(--color-text-soft); font-size:10px; margin-top:3px; }.grpo-flow > .flow-arrow:nth-of-type(1) { grid-column:2; }.grpo-flow > .flow-arrow:nth-of-type(2) { grid-column:4; }.grpo-flow > .update { grid-column:5; height:39px; }
.equation-band { grid-column:1 / 3; display:flex; align-items:center; justify-content:center; gap:16px; padding:8px 14px; border:1px solid rgba(173,124,255,.32); border-radius:var(--radius-md); background:rgba(173,124,255,.045); }.equation-band span { color:var(--color-muted); font-size:10px; text-transform:uppercase; letter-spacing:.08em; }.equation-band strong { color:var(--color-text-soft); font:600 14px/1.2 ui-monospace, SFMono-Regular, Consolas, monospace; white-space:nowrap; }
</style>
