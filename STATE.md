# 进度状态（STATE）

> 每次生成前先读这里；生成后更新这里。这是保证「每天接得上昨天」的关键。

## 难度基线 / 偏好

- 受众：985 工科研究生。**工程上**用过 diffusion（调包、改并重训 PolarAnything），但**数学推导**要从台阶讲起——**不要假设他熟 ELBO / 高斯后验推导**。
- **讲法档位 = 直觉 + 完整推导（绝不跳步）**：先用大白话 / 比喻把"为什么这么做"讲透，再上数学；从前提到结论**每一步都展开、每个符号都解释**。
- **严禁直接砸浓缩结论**：像"L_simple 是 reweighted ELBO""ε≈score"这类结论，必须拆成可跟随的小台阶，不能一句带过（这正是 2026-06-26 第一版翻车的原因）。
- 每篇带最小可运行代码 + CVPR 连接 + 面试角度；语言：中文讲解，术语 / 代码保留英文。
- 临场反馈记录：
  - 2026-06-26：第一版太密、跳步看不懂 → 改档位 2（直觉 + 完整推导），当篇已重写为「8 台阶」版。

## 当前位置

- 阶段：**D · 可控密集预测**
- 下一篇主菜：**D4 · Reliability-guided residual refinement**（风险与可修性的区别、expected benefit、no-harm gate、残差幅度控制与因果消融）
- 前沿速览节奏：建议每周二 / 周五各一次（上次：无）

## 已讲清单

- 2026-06-26 · **B1 DDPM** —— 前向闭式加噪、`L_simple` 是 reweighted ELBO、预测噪声≈预测 score、最小训练/采样代码
- 2026-06-29 · **B2 DDIM** —— 非马尔可夫前向保持相同边缘、用 `ε_θ` 预测 x̂₀ 再合成、`η` 旋钮（0=确定性 / 1=DDPM）、子序列跳步加速、确定性→可逆与 ODE
- 2026-07-01 · **B3 Score-based / SDE 统一框架** —— score 是 `∇ log p_t(x)`，预测噪声等价于学习 denoising score；DDPM 是反向 SDE 的离散随机采样，DDIM/ODE 是确定性 probability-flow 采样
- 2026-07-02 · **B4 条件生成与 Guidance** —— 条件生成等价于把 `∇ log p_t(x)` 改成 `∇ log p_t(x|y)`；classifier guidance 用外部分类器梯度，CFG 用条件预测与无条件预测的差估计条件方向
- 2026-07-06 · **B5 条件注入机制** —— 条件不是贴标签，而是进入 U-Net 的特征流；类别条件可加到时间嵌入，文本常走 cross-attention，空间/物理条件更适合 ControlNet 或 T2I-Adapter 的多尺度注入
- 2026-07-07 · **B6 Latent Diffusion（LDM / Stable Diffusion）** —— 先用 VAE 把图像压到 latent，再在 `z_t` 上做扩散，显著降低高分辨率生成成本；但普通图像 latent 可能丢掉 dense physical modality 需要的像素级/物理级细节
- 2026-07-09 · **B7 采样加速** —— 采样慢的根源是 U-Net 前向次数太多；DPM-Solver 把反向过程当 ODE 用高阶求解器少走弯路，Consistency Models 学不同噪声水平到同一干净结果的一致映射，Distillation 让少步 student 模仿多步 teacher；少步数会放大误差，dense physical task 还要检查物理一致性
- 2026-07-16 · **B8 训练实操** —— noise schedule 安排不同 SNR 的学习难度，`v-prediction` 在数据与噪声方向间建立可逆参数化，EMA 平滑评估权重；mixed precision、gradient accumulation 与 DDP 必须保持 prediction type、有效 batch、更新步和断点状态契约一致
- 2026-07-22 · **C1 Aleatoric vs Epistemic** —— aleatoric 来自给定模型后的数据散布，epistemic 来自有限数据下参数 posterior 的分歧；heteroscedastic Gaussian NLL 可学习输入相关噪声，全方差公式把总预测方差拆为模型内方差与模型间均值分歧
- 2026-07-25 · **C2 Bayesian Deep Learning** —— posterior predictive 对参数可能性积分；MC Dropout 用随机子网络近似采样，Deep Ensembles 用独立训练形成模型分歧，多次预测的模型间方差近似 epistemic uncertainty，并可与模型内 aleatoric variance 合成总方差
- 2026-07-26 · **C3 Reliability / Confidence Estimation** —— uncertainty 只是风险信号，reliability 要用独立数据验证信号与真实错误的对应；分类可用 reliability diagram、ECE 与 Temperature Scaling 校准，密集回归可用 risk-coverage 同时检查排序能力，并把“哪里错”与“哪里值得安全修”分开
- 2026-07-27 · **C4 Dense Prediction Uncertainty** —— heteroscedastic NLL 用误差加权项与 log-variance penalty 联合学习像素级 aleatoric uncertainty，ensemble 分歧近似 epistemic uncertainty；落地时要把 loss weighting、selective prediction、active learning 与 expected-benefit refinement 分开验证，高风险不等于 refiner 一定能改对
- 2026-07-30 · **D1 单目深度估计基本范式** —— 针孔投影只观察 $X/Z$ 与 $Y/Z$，因此单幅图像天然存在整体 scale ambiguity；metric depth 要直接负责真实单位，relative depth 则允许 scale 或 inverse-depth 空间的 scale-and-shift 对齐；训练 loss、测试 alignment、相机内参与有效 mask 必须遵守同一输出契约
- 2026-09-07 · **D2 法向估计与深度—法向几何约束** —— surface normal 来自反投影曲面的两条切向量叉乘；透视 depth-to-normal 显式依赖相机内参、像素位置与 depth gradient，全局乘法尺度不改变法向，但 additive shift、边界差分和错误内参会破坏几何；多任务 consistency 必须与独立监督、有效 mask 和 no-harm 分层评估配套
- 2026-09-08 · **D3 Diffusion 用于密集预测** —— conditional diffusion 把直接点估计改写为对 $p(d\mid I)$ 的逐步去噪建模，可复用预训练生成器的对象与布局先验；latent diffusion 降低空间计算成本，多次采样前要先处理 affine alignment，sample disagreement 只有经过 held-out error 校准后才能成为 reliability signal；总成本约随 ensemble size 与 denoising steps 的乘积增长

## 复习队列（间隔复习：1天 / 3天 / 7天 后各回顾一次要点）

- **B1 DDPM**：口述"为什么训练是预测噪声的 MSE" → 7 天回顾于 07-03
- **B2 DDIM**：口述"为什么能跳步还用同一个网络" → 复习于 2026-06-30 / 07-02 / 07-06
- **B3 Score/SDE**：口述"`ε_θ` 为什么可以换成 score" → 复习于 2026-07-02 / 07-04 / 07-08
- **B4 Guidance**：口述"为什么 `ε_cond - ε_uncond` 可以理解为条件方向" → 复习于 2026-07-03 / 07-05 / 07-09
- **B5 条件注入机制**：口述“ControlNet 为什么不是简单 concat” → 复习于 2026-07-07 / 07-09 / 07-13
- **B6 Latent Diffusion**：口述“为什么扩散发生在 `z_t` 而不是 `x_t`” → 复习于 2026-07-08 / 07-10 / 07-14
- **B7 采样加速**：口述“为什么 DPM-Solver 是 ODE 求解器而不是魔法” → 复习于 2026-07-10 / 07-12 / 07-16
- **B8 训练实操**：口述“为什么 `v` 能同时恢复 `x_0` 与 `ε`，训练和 sampler 又为何必须匹配” → 复习于 2026-07-17 / 07-19 / 07-23
- **C1 两类不确定性**：口述“全方差公式如何把总预测方差拆成 aleatoric 与 epistemic” → 复习于 2026-07-23 / 07-25 / 07-29
- **C2 贝叶斯深度学习**：口述“为什么 MC Dropout / Deep Ensembles 的多次预测能近似参数不确定性” → 复习于 2026-07-26 / 07-28 / 08-01
- **C3 可靠度与校准**：口述“calibration 与 risk ranking 有什么区别，为什么 confidence 高不等于可靠” → 复习于 2026-07-27 / 07-29 / 08-02
- **C4 密集预测不确定性**：口述“为什么高 uncertainty 不等于值得大幅 refinement，expected-benefit gate 应学习什么” → 复习于 2026-07-28 / 07-30 / 08-03
- **D1 单目深度估计范式**：口述“为什么单目图像不能仅靠投影确定米制尺度，对齐后的 relative 指标又为何不能证明 metric 能力” → 复习于 2026-07-31 / 08-02 / 08-06
- **D2 深度—法向几何约束**：口述“为什么 $(-z_u,-z_v,1)$ 只适合正交近似，以及强 consistency 为什么可能在边界传播错误” → 复习于 2026-09-08 / 09-10 / 09-14
- **D3 Diffusion 密集预测**：口述“为什么预测噪声能恢复 depth、affine-invariant ensemble 为何要先对齐，以及 sample spread 为什么不等于已校准 uncertainty” → 复习于 2026-09-09 / 09-11 / 09-15
