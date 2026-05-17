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
  <div class="team-name">AI 物理推导与仿真工作流</div>
  <div class="team-line">面向物理学院答辩：理论链条、公式复核、参数扫描与 EPOCH 执行</div>
</div>

---

## 结论先行

<div class="claim">我们的目标不是复述论文，而是用 AI Agent 把 FRA 的核心物理链条复现、审计，并推进到级联波长拓展方案。</div>

<div class="grid-3 mt-8">
  <div class="panel">
    <h3>理论复现</h3>
    <p>从三波耦合、色散关系与 Bessel 增益解出发，复核论文中 RFS/RBS 竞争、线性增益与非线性耗尽。</p>
  </div>
  <div class="panel">
    <h3>可审计推导</h3>
    <p>每一步保留公式来源、归一化假设、量纲检查与数值中间量，避免把 AI 输出当作不可追踪结论。</p>
  </div>
  <div class="panel">
    <h3>扩展设想</h3>
    <p>利用密度阶梯和级联 Stokes 过程，把近红外飞秒脉冲向更长波段、更高能量窗口推进。</p>
  </div>
</div>

<div class="takeaway mt-8">可信度来自闭环：原文定位 → 公式推导 → 参数扫描 → 图像验证 → 守恒检查 → 可执行仿真。</div>

---

## FRA 的最小物理图像

<div class="grid-2">
  <div>
    <div class="claim">泵浦光、种子光与电子等离子体波满足三波共振；能量从泵浦转移到 Stokes 种子。</div>
    <div class="panel mt-6">
      <p><span class="pump">Pump</span>：高频、较短波长，提供能量。</p>
      <p><span class="seed">Seed</span>：Stokes 下移频率，作为被放大的脉冲。</p>
      <p><span class="epw">EPW</span>：电子等离子体波，承担频率与动量失配。</p>
    </div>
  </div>
  <div class="figure-card">
    <img :src="'/ai-hackathon-fra/Fig1.png'" alt="Paper Fig. 1: pump seed EPW mechanism" />
  </div>
</div>

<div class="proof">图像来自原论文 Fig. 1，用于锚定 pump / seed / EPW 的相互作用关系。</div>

---

## 共振条件决定可放大窗口

FRA 的三波匹配条件为

$$
\omega_0=\omega_1+\omega_{\rm pe},
\qquad
k_0=k_1+k_{\rm epw}.
$$

电磁波在等离子体中的色散关系为

$$
\omega^2=\omega_{\rm pe}^2+c^2k^2,
\qquad
v_g=c\sqrt{1-\frac{\omega_{\rm pe}^2}{\omega^2}}.
$$

<div class="takeaway mt-8">这两个式子同时约束频率下移、群速度失配和可传播性；后续 RFS/RBS 竞争与密度窗口都从这里展开。</div>

---

## 由泵浦波长推得 Stokes 波长

在固定电子密度下，Stokes 波长可写成

$$
\lambda_{\rm seed}
=
\frac{\lambda_{\rm pump}}
{1-\sqrt{n_e/n_{c,p}}}.
$$

<div class="grid-3 mt-8">
  <div class="panel">
    <h3>密度越高</h3>
    <p>等离子体频率越高，Stokes 频移更大，种子波长更长。</p>
  </div>
  <div class="panel">
    <h3>但窗口有限</h3>
    <p>密度接近截止时，传播、群速度匹配和不稳定性都会迅速恶化。</p>
  </div>
  <div class="panel">
    <h3>级联的意义</h3>
    <p>一级 FRA 产生的 Stokes 可作为下一阶段种子，逐级拓展波长。</p>
  </div>
</div>

---

## RFS/RBS 竞争给出密度选择

令 $\mu=n_e/n_{c0}$，增长率可写为

$$
g_{\rm RFS,RBS}=
\frac{a_0\omega_0}{4}
\left[
\sqrt{1-\mu}\mp\sqrt{1-2\sqrt{\mu}}
\right]
\sqrt{\frac{\sqrt{\mu}}{1-\sqrt{\mu}}}.
$$

论文参数示例：

$$
\lambda_0=1.0\,\mu{\rm m},\quad
a_0=0.0854,\quad
\mu=0.2,\quad
\frac{g_{\rm RFS}}{g_{\rm RBS}}\approx0.47.
$$

<div class="takeaway mt-8">密度不是越高越好；我们需要在前向放大效率、反向散射抑制和传播窗口之间取平衡。</div>

---

## 参数扫描：密度、增长率与增益

<div class="evidence-grid mt-5">
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/density_growth_rates.png'" alt="Growth rates versus density" />
    <div class="evidence-caption">RFS 与 RBS 增长率随密度变化，标出论文使用的 $\mu=0.2$ 区域。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/density_gain_factor.png'" alt="Linear gain factor versus density" />
    <div class="evidence-caption">线性增益因子显示可用密度窗口，而不是单点参数。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/linear_gain_slices.svg'" alt="Linear gain slices" />
    <div class="evidence-caption">不同传播长度与相互作用时间下，增益对密度的敏感性。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/linear_gain_isolines.svg'" alt="Linear gain isolines" />
    <div class="evidence-caption">等增益线用于判断实验与仿真的参数容忍度。</div>
  </div>
</div>

---

## 线性理论不是简单的 $\exp(gt)$

弱种子线性解具有 Bessel 结构：

$$
a_1(\zeta,\tau)
=
a_{10}I_0\!\left(2g\sqrt{\zeta\tau}\right).
$$

对应强度增益为

$$
G_I(\zeta,\tau)
=
\left|\frac{a_1}{a_{10}}\right|^2
=
I_0^2\!\left(2g\sqrt{\zeta\tau}\right).
$$

<div class="takeaway mt-8">这是时空耦合问题，不能只用单一时间指数增长近似；这也是 AI 推导中最容易出错的环节之一。</div>

---

## Bessel 解与时空增益图像

<div class="evidence-grid three mt-5">
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/bessel_exact_vs_approx.svg'" alt="Bessel exact and asymptotic gain comparison" />
    <div class="evidence-caption">精确 Bessel 解与渐近近似的适用区间对比。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/spacetime_gain_zeta_tau.png'" alt="Spacetime gain in zeta tau coordinates" />
    <div class="evidence-caption">在 $\zeta,\tau$ 坐标中，增益沿相互作用区域累积。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/temporal_gain_profiles.png'" alt="Temporal gain profiles" />
    <div class="evidence-caption">不同位置的时间增益曲线，用来检查线性解的形状。</div>
  </div>
</div>

---

## 非线性阶段需要守恒检查

<div class="evidence-grid three mt-5">
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/nonlinear_pump_seed_xt_maps.png'" alt="Pump depletion and seed amplification maps" />
    <div class="evidence-caption">泵浦耗尽和种子增强必须发生在同一相互作用区。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/nonlinear_plasma_wave_xt_map.png'" alt="Plasma wave map" />
    <div class="evidence-caption">等离子体波振幅提供三波耦合是否同步的独立证据。</div>
  </div>
  <div class="evidence-tile">
    <img :src="'/ai-hackathon-fra/figures/nonlinear_manley_rowe_check.png'" alt="Manley Rowe conservation check" />
    <div class="evidence-caption">Manley-Rowe 型能量交换检查用于避免“图像像对了但物理不守恒”。</div>
  </div>
</div>

---

## 级联 FRA：从单级复现到设计问题

<div class="grid-2 mt-6">
  <div class="figure-card">
    <img :src="'/ai-hackathon-fra/cascade.svg'" alt="Cascaded FRA concept" />
  </div>
  <div>
    <div class="panel">
      <h3>核心设想</h3>
      <p>每一级的 Stokes 输出作为下一级种子，密度重新选择，使频移逐步累积。</p>
    </div>
    <div class="panel mt-4">
      <h3>主要约束</h3>
      <p>群速度失配、泵浦耗尽、RBS 抑制和级间时序必须同时满足。</p>
    </div>
  </div>
</div>

---

## 级联系统的时间窗口

<div class="grid-2 mt-6">
  <div>
    <div class="claim">级联不是把“更长波长”简单接起来，而是要保证每一级仍有足够重叠长度和可控不稳定性。</div>
    <div class="takeaway mt-6">时间窗口图把物理可行性转化为可扫描、可检验的设计空间。</div>
  </div>
  <div class="figure-card">
    <img :src="'/ai-hackathon-fra/timescale_window.svg'" alt="Timescale window for cascaded FRA" />
  </div>
</div>

---

## Agent 工作流：把物理复现变成可审计链条

<div class="flow mt-8">
  <div class="flow-step">
    <b>1. 锚定原文</b>
    <span>从题目描述定位论文、图像、公式编号和参数表。</span>
  </div>
  <div class="flow-step">
    <b>2. 原文解读</b>
    <span>抽取物理假设、归一化方式和关键推理链。</span>
  </div>
  <div class="flow-step">
    <b>3. 多 Agent 推导</b>
    <span>并行复核公式、量纲、符号和边界条件。</span>
  </div>
  <div class="flow-step">
    <b>4. 理论复现</b>
    <span>用解析式复现图像，并做 AI 内部交叉检查。</span>
  </div>
  <div class="flow-step">
    <b>5. 仿真执行</b>
    <span>扫描参数后自动编译、提交和执行 EPOCH 任务。</span>
  </div>
</div>

---

## AI 工作流全链路图

<div class="workflow-image-wrap mt-5">
  <img :src="'/ai-hackathon-fra/ai-workflow-fra.png'" alt="AI research workflow for FRA reproduction and EPOCH execution" />
</div>

<div class="evidence-note">从题目检索、论文解读、多 Agent 推导、理论复现、参数扫描，到 EPOCH 自动编译执行，形成可追溯闭环。</div>

---

## 面向 EPOCH 的落地路径

<div class="grid-3 mt-8">
  <div class="panel">
    <h3>输入文件生成</h3>
    <p>由解析参数自动写入密度、激光包络、边界条件和诊断输出。</p>
  </div>
  <div class="panel">
    <h3>编译与运行</h3>
    <p>AI 负责批量配置、提交任务和记录版本；人负责审核物理假设。</p>
  </div>
  <div class="panel">
    <h3>结果审计</h3>
    <p>把场图、能量交换、频谱和守恒检查回写到同一条证据链。</p>
  </div>
</div>

<div class="takeaway mt-8">最终交付的不是单张漂亮曲线，而是一套可以复跑、可定位错误、可扩展到新参数区的研究流程。</div>

---

## 答辩要点

<div class="grid-2 mt-7">
  <div class="panel">
    <h3>物理可信性</h3>
    <p>所有结论都回到共振条件、色散关系、增长率、Bessel 解和守恒检查。</p>
  </div>
  <div class="panel">
    <h3>AI 的角色</h3>
    <p>AI 不替代物理判断，而是加速论文定位、公式复核、参数扫描和仿真执行。</p>
  </div>
</div>

<div class="claim mt-8">如果每一步都能被复查，AI 才能真正进入物理研究工作流。</div>
