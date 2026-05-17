---
theme: scholarly
title: "Forward Raman Amplification with AI Agents"
info: |
  5-minute AI hackathon defense deck on reproducing and extending a paper about forward Raman amplification.
class: text-left
transition: fade
mdc: true
fonts:
  sans: Inter
  serif: "Noto Serif SC"
  mono: "JetBrains Mono"
---

<div class="cover-title">AI 复现与扩展: 前向拉曼放大 FRA</div>

<div class="paper-title">
Towards the Generation of Petawatt Near-Infrared Few-Cycle Light Pulses via Forward Raman Amplification in Plasma
</div>

<div class="team-block">
  <div class="team-name">AI炒大葱队</div>
  <div class="team-line">主讲人: 张峻华</div>
  <div class="team-line">队员: 伍先树, 倪昊, 申皓轩, 赵治崴（排名不分先后）</div>
</div>

<div class="grid-3 mt-10">
  <div class="panel">
    <h3>科学正确性</h3>
    <p class="muted">三波共振, 色散关系, 增长率, 时间尺度约束。</p>
  </div>
  <div class="panel">
    <h3>Agent 深度</h3>
    <p class="muted">PDF 定位, 公式推导, 单位审计, 参数扫描, 图表生成。</p>
  </div>
  <div class="panel">
    <h3>创新扩展</h3>
    <p class="muted">从 1.0 μm 到 1.8 μm 再到 3.2 μm 的级联 FRA。</p>
  </div>
</div>

<!--
Speaker notes:
这页只给总论点。评委先听到我们不是“把答案贴出来”, 而是用 AI 工具做科学工作流: 复现论文核心机制, 找出可行窗口, 再提出级联扩展。
-->

---

## 1. 高功率少周期红外脉冲的瓶颈, 在于“能不能在不损伤介质的情况下继续放大”。

<div class="grid-2 mt-5">
  <div>
    <div class="claim">传统固态光学链路越接近拍瓦级和少周期极限, 越需要面对材料损伤, 宽带相位和能量承载的共同约束。</div>
    <div class="panel mt-7">
      <h3>为什么这是问题</h3>
      <ul class="compact-list">
        <li>高峰值功率需要继续放大, 但晶体, 光栅和镀膜都有损伤阈值。</li>
        <li>少周期红外脉冲还要求宽带和相位稳定, 不能只靠堆能量。</li>
        <li>等离子体放大把问题转化为可计算的三波耦合与不稳定性窗口。</li>
      </ul>
    </div>
    <div class="takeaway mt-6">本项目的背景意义: 用等离子体把高功率红外放大从材料极限问题转化为三波耦合动力学问题。</div>
  </div>
</div>

---

## 2. 为什么 FRA 有意义?

<div class="claim">FRA 的关键反转是: 前向拉曼散射不再只是损耗通道, 而是同向追赶构型中的可用增益机制。</div>

<div class="grid-2 mt-7">
  <div class="panel">
    <h3>传统担忧: forward scattering 是寄生过程</h3>
    <p>在很多激光等离子体放大方案中, 前向散射会抽走泵浦能量, 激发副波和电子等离子体波, 并和成丝等横向不稳定性耦合。</p>
    <p class="muted">如果它不可控, 它就是损耗和噪声。</p>
  </div>
  <div class="panel">
    <h3>FRA 设计: 把寄生过程变成主过程</h3>
    <p><span class="pump">短波长泵浦</span> 与 <span class="seed">长波长种子</span> 同向传播。由于等离子体色散, 泵浦群速度更快, 从后方追上种子。</p>
    <p class="muted">同向构型给出长相互作用窗口, 密度调谐给出输出波长可控性。</p>
  </div>
</div>

<div class="big-eq mt-7">
  <div class="formula">ω<sub>0</sub> = ω<sub>1</sub> + ω<sub>pe</sub>, &nbsp;&nbsp; k<sub>0</sub> = k<sub>1</sub> + k<sub>epw</sub></div>
</div>

<div class="takeaway">一句话: FRA 不是绕开 forward scattering, 而是把它放进共振条件和时间尺度窗口里。</div>

---

## 3. 论文机制图: pump-seed-EPW

<div class="grid-2">
  <div>
    <div class="claim">Fig. 1 展示的是 FRA 的最小物理图像: 泵浦追上种子, 电子等离子体波承接相位匹配, 最后种子被放大并压缩。</div>
    <div class="panel mt-7">
      <h3>图中三种对象</h3>
      <p><span class="pump">Pump</span>: 更短波长, 更高频, 在等离子体中群速度更快。</p>
      <p><span class="seed">Seed</span>: 更长波长, 被同向泵浦追赶并获得能量。</p>
      <p><span class="epw">EPW</span>: 电子等离子体波, 提供频率差和波矢差。</p>
    </div>
  </div>
  <div class="figure-card">
    <img :src="'./figures/spacetime_gain_lab_xt.png'" alt="FRA pump seed EPW mechanism" />
  </div>
</div>

<div class="proof">AI 使用点: 从论文资料中定位 Fig. 1, 抽取机制语义, 再把它转写成答辩中的 pump-seed-EPW 三对象叙事。</div>

---

## 4. 理论框架: 三波耦合 + 共振 + 调谐

<div class="claim">FRA 的理论框架可以压缩成三个层次: 色散关系决定可传播波, 共振条件决定耦合, 密度决定输出波长。</div>

<div class="grid-3 mt-7">
  <div class="panel">
    <h3>1. 冷等离子体色散</h3>
    <div class="formula">ω<sup>2</sup> = ω<sub>pe</sub><sup>2</sup> + c<sup>2</sup>k<sup>2</sup></div>
    <p class="muted">光波群速度为 v<sub>g</sub> = c√(1 - ω<sub>pe</sub><sup>2</sup>/ω<sup>2</sup>)。</p>
  </div>
  <div class="panel">
    <h3>2. 三波共振</h3>
    <div class="formula">ω<sub>0</sub> = ω<sub>1</sub> + ω<sub>pe</sub></div>
    <div class="formula">k<sub>0</sub> = k<sub>1</sub> + k<sub>epw</sub></div>
    <p class="muted">泵浦, 种子和 EPW 同时满足能量与动量匹配。</p>
  </div>
  <div class="panel">
    <h3>3. 密度调谐</h3>
    <div class="formula">λ<sub>seed</sub> = λ<sub>pump</sub> / [1 - √(n<sub>e</sub>/n<sub>c,p</sub>)]</div>
    <p class="muted">调节 n<sub>e</sub> 就调节频差, 因而调节输出波长。</p>
  </div>
</div>

<div class="takeaway mt-8">这也是后面级联设计的根: 每一级都不是换机制, 而是重新选密度平台。</div>

---

## 5. 从线性到非线性: 只抓阶段划分

<div class="claim">复现不需要把每一步推导塞进路演; 关键是说明我们知道系统什么时候由线性增益进入非线性放大和自压缩。</div>

<div class="grid-3 mt-7">
  <div class="panel">
    <h3>线性种子增长</h3>
    <div class="formula">a<sub>1</sub>(ζ,τ) = a<sub>10</sub>I<sub>0</sub>(2g√ζτ)</div>
    <p class="muted">不是简单 e<sup>gt</sup>, 而是依赖传播距离和局域时间的时空增长。</p>
  </div>
  <div class="panel">
    <h3>非线性超辐射阶段</h3>
    <p>种子增长后开始显著抽取泵浦, 脉冲后沿增益更强, 形状演化不能再用线性响应完整描述。</p>
    <p class="muted">Task 回答中保留了论文给出的 I<sub>s</sub> ∝ a<sub>p</sub><sup>4</sup> n<sub>e</sub>L<sup>2</sup> 标度。</p>
  </div>
  <div class="panel">
    <h3>自相位调制压缩</h3>
    <p>放大后的长波种子继续在等离子体中演化, 通过自相位调制向少周期脉冲压缩。</p>
    <p class="muted">可行性取决于压缩是否早于成丝充分发展。</p>
  </div>
</div>

<div class="takeaway mt-8">路演表达: 线性增长给“能起振”, 非线性放大给“能变强”, 自压缩给“能少周期”。</div>

---

## 6. Q1: 增长率复现, RFS/RBS 对比

<div class="grid-2">
  <div>
    <div class="claim">中等密度是 FRA 的竞争性来源: RFS 增长率虽然低于 RBS, 但差距已经缩小到可由长相互作用窗口补偿。</div>
    <div class="big-eq">
      <div class="formula">
        g<sub>RFS</sub> = (a<sub>0</sub>ω<sub>0</sub>/4)
        · √[x<sup>1/2</sup>/(1 - x<sup>1/2</sup>)]
        · [√(1 - x) - √(1 - 2x<sup>1/2</sup>)]
      </div>
      <div class="formula dim">where x = n<sub>e</sub>/n<sub>c,p</sub></div>
    </div>
    <div class="panel">
      <p><strong>典型复现结果:</strong> λ<sub>0</sub> = 1.0 μm, a<sub>0</sub> = 0.0854, n<sub>e</sub> = 0.2 n<sub>c</sub>。</p>
      <p class="metric seed">g<sub>RFS</sub>/2π ≈ 3.28 THz</p>
      <p class="muted">g<sub>RFS</sub>/g<sub>RBS</sub> ≈ 0.47, 已经不是低密度极限下“前向远小于后向”的图像。</p>
    </div>
  </div>
  <div>
    <img class="full-img" :src="'./figures/density_growth_rates.png'" alt="RFS RBS growth comparison" />
  </div>
</div>

---

## 7. Q3: 时间尺度窗口决定可行区

<div class="claim">FRA 的可行性不是单看增长率, 而是看四个时间尺度能否排成正确顺序。</div>

<div class="grid-2 mt-6">
  <div>
    <div class="big-eq">
      <div class="formula">
        τ<sub>RFS</sub> &lt; τ<sub>window</sub> &lt; τ<sub>fil</sub>,
        &nbsp;&nbsp;τ<sub>sfc</sub> &lt; τ<sub>fil</sub>
      </div>
    </div>
    <div class="panel">
      <h3>参考点</h3>
      <p>λ<sub>0</sub> = 1.0 μm, a<sub>0</sub> = 0.0854, n<sub>e</sub> = 0.2 n<sub>c</sub>, τ<sub>pump</sub> = 240 fs。</p>
      <p class="muted">这个点对应论文 1D/2D PIC 参数量级, 不是随意选点。</p>
    </div>
    <div class="panel mt-4">
      <h3>AI 审计发现</h3>
      <p>Task3 中自压缩公式直接代入存在量纲异常。我们没有硬算出一个“漂亮数字”, 而是标出该问题, 并用 PIC 图像量级估计 τ<sub>sfc</sub> ≈ 1.5 ps。</p>
    </div>
  </div>
  <div>
    <img class="full-img" :src="'./figures/nonlinear_interaction_length_design.png'" alt="FRA timescale feasibility window" />
  </div>
</div>

<div class="takeaway mt-4">评分点: 这里体现的是科学复现中的单位审计和风险识别, 而不是只让 AI 代写公式。</div>

---

## 8. Q4: 级联 FRA 设计

<div class="claim">密度调谐让 FRA 天然适合级联: 上一级输出的长波种子, 可以成为下一级的泵浦。</div>

<div class="mt-2">
  <img class="cascade-img" :src="'./figures/density_gain_factor.png'" alt="Cascaded FRA route" />
</div>

<div class="grid-2 mt-2">
  <div class="panel tight-panel">
    <h3>两级主方案</h3>
    <table class="table">
      <thead>
        <tr><th>级</th><th>波长</th><th>n<sub>e</sub>/n<sub>c,p</sub></th><th>密度</th></tr>
      </thead>
      <tbody>
        <tr><td>1</td><td>1.0 → 1.8 μm</td><td>0.198</td><td>2.2×10<sup>20</sup> cm<sup>-3</sup></td></tr>
        <tr><td>2</td><td>1.8 → 3.2 μm</td><td>0.191</td><td>6.5×10<sup>19</sup> cm<sup>-3</sup></td></tr>
      </tbody>
    </table>
  </div>
  <div class="panel tight-panel">
    <h3>工程约束</h3>
    <p>不建议直接把第一级 9 fs 级自压缩输出作为第二级泵浦; 更合理的是在放大完成但强自压缩前提取, 或重新展宽到 100-200 fs。</p>
    <p class="muted">原因: 第二级仍需要“长泵浦追赶短种子”的群速度窗口。</p>
  </div>
</div>

---

## 9. AI agent 作为科学工作流

<div class="claim">比赛的核心不是“AI 写了一份答案”, 而是 agent 被组织成可检查的科学工作流。</div>

<div class="flow mt-8">
  <div class="flow-step">
    <b>1. 读资料</b>
    <span>从 MainManu, Supp, Qs 和 Task 回答定位问题, 图和关键参数。</span>
  </div>
  <div class="flow-step">
    <b>2. 复推导</b>
    <span>从色散关系和三波共振得到 RFS/RBS 增长率。</span>
  </div>
  <div class="flow-step">
    <b>3. 做数值</b>
    <span>计算 g<sub>RFS</sub>, 时间尺度, 密度平台和级联参数。</span>
  </div>
  <div class="flow-step">
    <b>4. 审单位</b>
    <span>检查公式量纲, 标出自压缩估计中的异常来源。</span>
  </div>
  <div class="flow-step">
    <b>5. 产出设计</b>
    <span>把复现结果转成可讲的路演结构和图表。</span>
  </div>
</div>

<div class="grid-3 mt-8">
  <div class="panel">
    <h3>不是黑箱</h3>
    <p class="muted">每个结论都对应公式, 参数或图表。</p>
  </div>
  <div class="panel">
    <h3>不是只复述</h3>
    <p class="muted">加入级联 FRA 和级间脉冲处理建议。</p>
  </div>
  <div class="panel">
    <h3>不是过度承诺</h3>
    <p class="muted">对量纲疑点和 PIC 估计边界明确标注。</p>
  </div>
</div>

---

## 10. 复现与扩展结果总表

<div class="claim">我们最终得到的是一个闭环: 机制可解释, 公式可复现, 参数可核查, 扩展有物理约束。</div>

<table class="table mt-6">
  <thead>
    <tr>
      <th>模块</th>
      <th>复现/扩展结果</th>
      <th>答辩价值</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>机制</td>
      <td>同向 pump-seed-EPW 三波耦合, 泵浦因色散追赶种子。</td>
      <td>解释 FRA 为什么不是普通 RFS 损耗。</td>
    </tr>
    <tr>
      <td>Q1</td>
      <td>g<sub>RFS</sub>/2π ≈ 3.28 THz, g<sub>RFS</sub>/g<sub>RBS</sub> ≈ 0.47。</td>
      <td>证明中等密度区 FRA 有竞争性。</td>
    </tr>
    <tr>
      <td>Q3</td>
      <td>0.0486 &lt; 0.783 &lt; 2.912 ps, 且 τ<sub>sfc</sub> ≈ 1.5 ps &lt; τ<sub>fil</sub>。</td>
      <td>把“能增长”提升为“能在不稳定性前完成”。</td>
    </tr>
    <tr>
      <td>Q4</td>
      <td>1.0 → 1.8 → 3.2 μm, 密度阶梯 2.2×10<sup>20</sup> → 6.5×10<sup>19</sup> cm<sup>-3</sup>。</td>
      <td>展示波长可调谐和中红外扩展潜力。</td>
    </tr>
  </tbody>
</table>

---

## 11. 总结

<div class="grid-2">
  <div>
    <div class="claim">:</div>
    <div class="panel mt-6">
      <p><strong>第一,</strong> 等离子体放大绕开固态光学损伤阈值, 适合极强场少周期脉冲。</p>
      <p><strong>第二,</strong> FRA 用同向追赶和三波共振, 把前向拉曼散射从寄生过程变成受控增益。</p>
      <p><strong>第三,</strong> AI agent 不只是写答案, 而是帮助完成复现, 审计和级联方案设计。</p>
    </div>
  </div>
  <div class="panel">
    <h3>最终主张</h3>
    <p class="metric">FRA = 放大 + 调谐 + 压缩</p>
    <p class="muted mt-5">在合适密度和泵浦强度下, 它给出一条从近红外到中红外少周期高功率脉冲的可行物理路线。</p>
    <div class="big-eq mt-8">
      <div class="formula">1.0 μm → 1.8 μm → 3.2 μm</div>
    </div>
  </div>
</div>

<div class="takeaway mt-8">这份答辩的定位: 不把论文讲散, 只围绕“为什么 FRA 可行, 我们如何用 AI 证明并扩展它”。</div>
