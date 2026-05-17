---
theme: scholarly
title: "Forward Raman Amplification with AI Agents"
info: |
  AI hackathon defense deck on reproducing and extending forward Raman amplification theory.
class: text-left
transition: fade
mdc: true
fonts:
  sans: Inter
  serif: "Noto Serif SC"
  mono: "JetBrains Mono"
---

<div class="cover-title">AI 复现与扩展：前向拉曼放大</div>

<div class="paper-title">
Towards the Generation of Petawatt Near-Infrared Few-Cycle Light Pulses via Forward Raman Amplification in Plasma
</div>

<div class="team-block">
  <div class="team-name">AI 炒大葱队</div>
  <div class="team-line">主讲人：张峻华</div>
  <div class="team-line">队员：伍先树、倪昊、申皓轩、赵治崴</div>
</div>

---

## 结论先行

<div class="claim">我们不是复述论文，而是用 AI agent 把 FRA 的核心链条复现、审计，并推到级联波长拓展方案。</div>

<div class="grid-3 mt-8">
  <div class="panel">
    <h3>物理复现</h3>
    <p>三波共振、冷等离子体色散、RFS/RBS 增长率与 Bessel 线性解。</p>
  </div>
  <div class="panel">
    <h3>可行性审计</h3>
    <p>把增长时间、群速度滑移、成丝时间和自压缩时间放到同一窗口中判断。</p>
  </div>
  <div class="panel">
    <h3>扩展设计</h3>
    <p>从 1.0 μm 到 1.8 μm 再到 3.2 μm，给出密度调谐的级联 FRA 路线。</p>
  </div>
</div>

<div class="takeaway mt-8">面向物理评审，关键不是“AI 生成了答案”，而是每一步结论都能回到方程、量纲、图像和守恒检查。</div>

---

## 为什么选择等离子体前向拉曼放大

<div class="claim">少周期近红外拍瓦脉冲的瓶颈，是如何在不损伤传统光学介质的情况下继续放大。</div>

<div class="grid-2 mt-8">
  <div class="panel">
    <h3>固体光学链路的限制</h3>
    <ul class="compact-list">
      <li>晶体、光栅、镀膜都有损伤阈值。</li>
      <li>少周期脉冲还要求宽带和相位稳定。</li>
      <li>继续堆能量会快速碰到材料极限。</li>
    </ul>
  </div>
  <div class="panel">
    <h3>等离子体作为增益介质</h3>
    <ul class="compact-list">
      <li>等离子体已电离，不存在普通透明介质的击穿问题。</li>
      <li>电子等离子体波可作为泵浦与种子之间的能量中介。</li>
      <li>问题转化为三波耦合是否能先于不稳定性完成放大。</li>
    </ul>
  </div>
</div>

---

## FRA 的最小物理图像

<div class="grid-2">
  <div>
    <div class="claim">泵浦与种子同向传播；泵浦群速度更快，从后方追上种子并转移能量。</div>
    <div class="panel mt-6">
      <p><span class="pump">Pump</span>：短波长、高频率、较快群速度。</p>
      <p><span class="seed">Seed</span>：长波长 Stokes 分支，被外部注入并受激放大。</p>
      <p><span class="epw">EPW</span>：电子等离子体波，承担能量与动量匹配。</p>
    </div>
  </div>
  <div class="figure-card">
    <img :src="'/Fig1.png'" alt="Paper Fig. 1: pump seed EPW mechanism" />
  </div>
</div>

<div class="proof">论文 Fig. 1 对应的物理对象被拆成 pump / seed / EPW 三个可审计变量，后续所有图都围绕这三个变量展开。</div>

---

## 三波共振关系是整个复现的支点

FRA 用电子等离子体波完成频率与波矢匹配：

$$
\omega_0=\omega_1+\omega_{\rm pe},
\qquad
k_0=k_1+k_{\rm epw}.
$$

冷等离子体中的光波色散为：

$$
\omega^2=\omega_{\rm pe}^2+c^2k^2,
\qquad
v_g=c\sqrt{1-\frac{\omega_{\rm pe}^2}{\omega^2}}.
$$

<div class="takeaway mt-8">这两组式子决定了：为什么泵浦能追上种子、为什么密度可以调谐输出波长、为什么 RFS/RBS 的差别最终进入波矢 mismatch。</div>

---

## 输出波长由等离子体密度调谐

由 Stokes 条件和冷等离子体色散，可得到种子波长：

$$
\lambda_{\rm seed}
=
\frac{\lambda_{\rm pump}}
{1-\sqrt{n_e/n_{c,p}}}.
$$

<div class="grid-3 mt-8">
  <div class="panel">
    <h3>低密度</h3>
    <p>频差小，输出波长接近泵浦。</p>
  </div>
  <div class="panel">
    <h3>中等密度</h3>
    <p>频差增大，FRA 可进入有效增益区。</p>
  </div>
  <div class="panel">
    <h3>接近边界</h3>
    <p>增益提高，但 Stokes 分支和不稳定性约束变得更紧。</p>
  </div>
</div>

---

## Q1：RFS/RBS 线性增长率复现

从三波耦合增长率出发，前向与后向的主要差异进入 EPW 波数：

$$
g=
\frac{a_0 c k_2}{4}
\sqrt{\frac{\omega_{\rm pe}}{\omega_0-\omega_{\rm pe}}}.
$$

令 $\mu=n_e/n_{c0}$，可写成：

$$
g_{\rm RFS,RBS}=
\frac{a_0\omega_0}{4}
\left[
\sqrt{1-\mu}\mp\sqrt{1-2\sqrt{\mu}}
\right]
\sqrt{\frac{\sqrt{\mu}}{1-\sqrt{\mu}}}.
$$

典型复现点：

$$
\lambda_0=1.0\,\mu{\rm m},\quad
a_0=0.0854,\quad
\mu=0.2,\quad
\frac{g_{\rm RFS}}{g_{\rm RBS}}\approx0.47.
$$

---

## 密度扫描把“前向是否足够强”量化

<div class="evidence-grid mt-5">
  <div class="evidence-tile">
    <img :src="'/figures/density_growth_rates.png'" alt="Growth rates versus density" />
    <div class="evidence-caption">RFS 与 RBS 增长率随密度升高而接近；典型点 mu = 0.2 时，RFS 已不是可忽略通道。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/density_gain_factor.png'" alt="Linear gain factor versus density" />
    <div class="evidence-caption">把增长率代入 Bessel 增益后，小的密度差别会被放大成数量级差异。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/linear_gain_slices.svg'" alt="Linear gain slices" />
    <div class="evidence-caption">不同时间切片显示早期增益较平缓，随后进入快速增长区。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/linear_gain_isolines.svg'" alt="Linear gain isolines" />
    <div class="evidence-caption">等增益线给出可设计区域：靠近边界增强 RFS，但也压缩安全余量。</div>
  </div>
</div>

---

## 线性阶段不是简单的 exp(gt)

小信号阶段的种子振幅满足 Bessel 形式：

$$
a_1(\zeta,\tau)
=
a_{10}I_0\!\left(2g\sqrt{\zeta\tau}\right).
$$

因此强度增益为：

$$
G_I(\zeta,\tau)
=
\left|\frac{a_1}{a_{10}}\right|^2
=
I_0^2\!\left(2g\sqrt{\zeta\tau}\right).
$$

<div class="takeaway mt-8">这个形式对教授评审很关键：它说明增长是时空重叠驱动的，不是把局域增长率机械乘上实验时间。</div>

---

## Bessel 解的图像证据

<div class="evidence-grid three mt-5">
  <div class="evidence-tile">
    <img :src="'/figures/spacetime_gain_zeta_tau.png'" alt="Spatiotemporal gain in zeta tau coordinates" />
    <div class="evidence-caption">zeta-tau 坐标中的增益沿双曲线增长，对应 Bessel 解中的 sqrt(zeta tau)。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/temporal_gain_profiles.png'" alt="Temporal gain profiles" />
    <div class="evidence-caption">固定传播位置时，种子增益峰随群速度追赶时刻后移。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/bessel_exact_vs_approx.svg'" alt="Bessel exact versus approximations" />
    <div class="evidence-caption">小信号区用级数近似；强增益区转入渐近指数行为。</div>
  </div>
</div>

---

## Q3：可行窗口由时间尺度夹逼决定

FRA 必须在有效增长窗口内完成放大，同时避开成丝等不稳定性：

$$
\tau_{\rm RFS}<\tau_{\rm window}<\tau_{\rm fil},
\qquad
\tau_{\rm sfc}<\tau_{\rm fil}.
$$

典型参数下：

$$
\lambda_0=1.0\,\mu{\rm m},\quad
a_0=0.0854,\quad
\mu=0.2,\quad
\tau_{\rm pump}=240\,{\rm fs}.
$$

$$
0.049\,{\rm ps}<0.78\,{\rm ps}<2.9\,{\rm ps}.
$$

<div class="takeaway mt-7">我们保留了 Task 3 中自压缩公式的量纲疑点，并用图像量级估计作为保守替代，而不是给出不可审计的漂亮数字。</div>

---

## 时间尺度窗口的图像证据

<div class="evidence-grid mt-5">
  <div class="evidence-tile">
    <img :src="'/timescale_window.svg'" alt="FRA timescale feasibility window" />
    <div class="evidence-caption">增长、滑移、成丝与自压缩被放在同一窗口中比较。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/linear_gain_heatmap.svg'" alt="Linear gain feasibility heatmap" />
    <div class="evidence-caption">参数平面显示可行区是一条受限带，不是单个最佳点。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/spacetime_gain_lab_xt.png'" alt="Lab-frame spatiotemporal gain map" />
    <div class="evidence-caption">实验室坐标中的 x-t 图便于和 PIC 或实验诊断对齐。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/nonlinear_interaction_length_design.png'" alt="Interaction length design" />
    <div class="evidence-caption">作用长度由群速度滑移、增益和不稳定性共同限制。</div>
  </div>
</div>

---

## Q4：级联 FRA 的波长拓展路线

密度调谐给出一级级 Stokes 转换：

$$
\mu_j
=
\frac{n_{e,j}}{n_{c,j}}
=
\left(1-\frac{\lambda_j}{\lambda_{j+1}}\right)^2.
$$

推荐两级路线：

| 级数 | 波长转换 | $\mu_j$ | 电子密度 |
|---|---:|---:|---:|
| 1 | $1.0\rightarrow1.8\,\mu{\rm m}$ | 0.198 | $2.2\times10^{20}\,{\rm cm^{-3}}$ |
| 2 | $1.8\rightarrow3.2\,\mu{\rm m}$ | 0.191 | $6.5\times10^{19}\,{\rm cm^{-3}}$ |

---

## 级联设计不能只看波长表

<div class="evidence-grid three mt-5">
  <div class="evidence-tile">
    <img :src="'/cascade.svg'" alt="Cascaded FRA route" />
    <div class="evidence-caption">级联路线：每一级用新的等离子体密度匹配下一段 Stokes 输出。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/nonlinear_three_wave_exchange.png'" alt="Nonlinear three-wave exchange" />
    <div class="evidence-caption">三波交换图显示泵浦、种子与 EPW 的能量流向。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/nonlinear_superradiant_scaling.png'" alt="Superradiant nonlinear scaling" />
    <div class="evidence-caption">非线性阶段出现 seed intensity proportional to pump intensity squared 的超辐射标度。</div>
  </div>
</div>

<div class="evidence-note">这页的重点是设计约束：级联不是“波长继续往下接”这么简单，还要检查每一级是否有足够泵浦、足够重叠长度和可控不稳定性。</div>

---

## Agent 工作流：把物理复现变成可审计链条

<div class="flow mt-8">
  <div class="flow-step">
    <b>1. 定位来源</b>
    <span>从论文、补充材料和任务问题中定位公式与参数。</span>
  </div>
  <div class="flow-step">
    <b>2. 推导结构</b>
    <span>从色散关系推出 RFS/RBS 增长率和调谐关系。</span>
  </div>
  <div class="flow-step">
    <b>3. 数值复现</b>
    <span>计算增长率、时间窗口和密度阶梯。</span>
  </div>
  <div class="flow-step">
    <b>4. 图像验证</b>
    <span>用参数扫描、时空图和非线性图检查结论。</span>
  </div>
  <div class="flow-step">
    <b>5. 物理审计</b>
    <span>检查量纲、守恒律和可行区边界。</span>
  </div>
</div>

---

## 非线性复现需要守恒检查

<div class="evidence-grid three mt-5">
  <div class="evidence-tile">
    <img :src="'/figures/nonlinear_pump_seed_xt_maps.png'" alt="Pump depletion and seed amplification maps" />
    <div class="evidence-caption">泵浦耗尽和种子增强必须发生在同一相互作用区。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/nonlinear_plasma_wave_xt_map.png'" alt="Plasma wave mediator map" />
    <div class="evidence-caption">EPW 场图验证中介波确实被激发，而不是由公式外推。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/figures/nonlinear_manley_rowe_check.png'" alt="Manley Rowe check" />
    <div class="evidence-caption">Manley-Rowe 检查用于排除“曲线好看但物理不守恒”的复现。</div>
  </div>
</div>

---

## 复现与扩展的最终表述

| 问题 | 我们复现/扩展了什么 | 给物理评审的判断 |
|---|---|---|
| 机制 | pump-seed-EPW 三波共振、群速度追赶和 Stokes 调谐 | FRA 可以作为受控前向增益机制讨论 |
| Q1 | $g_{\rm RFS}/g_{\rm RBS}\approx0.47$ at $\mu=0.2$ | 前向通道在中等密度下不可忽略 |
| Q3 | $0.049<0.78<2.9\,{\rm ps}$ | 存在增长先于成丝的时间窗口 |
| Q4 | $1.0\rightarrow1.8\rightarrow3.2\,\mu{\rm m}$ | 级联路线可由密度调谐给出一阶设计 |

---

## 总结

<div class="claim">FRA 的价值在于把高功率红外放大从材料损伤问题，转化为可计算、可诊断、可设计的等离子体三波耦合问题。</div>

<div class="grid-2 mt-8">
  <div class="panel">
    <h3>物理结论</h3>
    <p>在典型参数下，RFS 增长、群速度窗口和成丝时间之间存在可行排序。</p>
    <p>级联 FRA 可以把近红外种子推进到更长波段。</p>
  </div>
  <div class="panel">
    <h3>AI 的角色</h3>
    <p>AI agent 不是替代物理判断，而是加速公式定位、推导复核、参数扫描和图像审计。</p>
    <p>最终可信度仍来自方程、量纲、图像和守恒律。</p>
  </div>
</div>

$$
1.0\,\mu{\rm m}\rightarrow1.8\,\mu{\rm m}\rightarrow3.2\,\mu{\rm m}
$$
