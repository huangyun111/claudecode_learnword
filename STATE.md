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

- 阶段：**G · 研究方法与论文证据**（A–F 主线与 A 阶段回填已完成）
- 下一篇主菜：**G1 · 实验设计与证据链**（从 research question、hypothesis 和 estimand 出发，分清 baseline、matched control、ablation、negative control、held-out evaluation 与 causal claim）
- 前沿速览节奏：建议每周二 / 周五各一次（上次：2026-09-21，Sora / Genie 类世界生成）

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
- 2026-09-09 · **D4 Reliability-guided residual refinement** —— 高 uncertainty 只表示 base 可能错，不等于 candidate residual 值得采用；用 $b_i=e_{0,i}-e_{c,i}$ 定义真实收益并学习 expected-benefit gate，以 bounded residual、no-harm penalty 和输出空间几何控制修改，再用 shuffled/oracle/matched-capacity controls、harm rate 与 worst-group results 建立因果证据
- 2026-09-10 · **E1 多视图几何基础** —— 单像素只确定一条相机射线，双视图通过共面关系得到 $\mathbf x_2^\top\mathbf E\mathbf x_1=0$ 与像素域 $\tilde{\mathbf x}_2^\top\mathbf F\tilde{\mathbf x}_1=0$；极线约束缩小匹配搜索，DLT/SVD 三角化恢复三维点，尺度、重投影、正深度和射线夹角决定结果是否可信
- 2026-09-13 · **E2 SfM / COLMAP 管线** —— 局部特征与候选匹配建立 view graph，RANSAC 用极线几何隔离 outlier，可靠初始对产生首批相机与三维点，PnP 注册新相机、三角化扩展 tracks，bundle adjustment 再用稀疏重投影目标联合优化相机与结构；纯视觉重建仍有 similarity gauge freedom
- 2026-09-14 · **E3 NeRF / 3D Gaussian Splatting** —— NeRF 用位置与方向到 density / radiance 的连续函数沿射线体渲染，3DGS 用可优化的 anisotropic Gaussians 投影并 splat 到屏幕；两者共享 front-to-back alpha compositing，但 novel-view 图像质量不能单独证明 metric geometry 或偏振物理正确
- 2026-09-15 · **E4 偏振成像物理与 Shape from Polarization** —— analyzer 的二倍角强度由 $S_0,S_1,S_2$ 线性描述，DoLP 与 AoLP 分别提供反射几何的幅度和模 $\pi$ 方位线索；Fresnel 把观察角映射到偏振度，但 $\pi$、$\pi/2$、zenith 多解、未知材质和 mixed reflection 使单视图法向不唯一，需用可积性、stereo 与 multi-view consistency 消歧
- 2026-09-16 · **F1 Video Diffusion** —— 把整段 $C\times T\times H\times W$ 视频作为联合随机变量加噪与去噪，spatial module 恢复帧内外观，temporal convolution / attention 学跨帧对应、身份与运动；多次采样可表达多未来，但外观连贯、动力学合理与可干预的世界模型能力必须分层验证
- 2026-09-18 · **F2 Action-conditioned Prediction** —— 用 $p(\text{future}\mid\text{past},\text{actions})$ 区分不同控制选择的后果，transition model 逐步 rollout，stochastic latent 表达不可控多未来，MPC 通过候选动作—预测—代价—执行一步形成闭环；action shuffle、同状态多动作与真实闭环验证用于排除模型忽略动作或只学相关性
- 2026-09-19 · **F3 Latent World Models（Dreamer 类）** —— RSSM 用 deterministic recurrent state 保存历史、stochastic latent 表达多种可能；posterior 从真实 observation 校正状态，prior 在无未来观测时 rollout，KL 把二者接起来；actor / critic 再用 imagined rewards、continuation 与 $\lambda$-return 学行为，但最终仍需真实闭环排除 model exploitation
- 2026-09-21 · **F4 Sora / Genie 类世界生成与可控生成** —— Sora 类模型用 latent spacetime patches 学开放域视觉轨迹，Genie 类模型用 autoregressive latent diffusion 把逐帧生成接到 action，latent action 可从无标注视频发现控制维度；但画质、长时状态、action controllability、counterfactual correctness、planning utility 与 real-world validity 必须逐层验证
- 2026-09-23 · **A1 Latent Variable Models / ELBO / VAE** —— latent variable model 通过对 $\mathbf z$ 边缘化定义数据 likelihood，VAE 用 $q_\phi(\mathbf z\mid\mathbf x)$ 近似难算 posterior；Jensen inequality 将目标化为 expected reconstruction log-likelihood 减 posterior-to-prior KL，reparameterization 再让随机连续 latent 支持低方差 pathwise gradient
- 2026-09-24 · **A2 GAN / Normalizing Flow** —— GAN 用 discriminator 提供 density-ratio signal，最优判别器下 objective 化为 $-\log4+2\,\mathrm{JSD}$，但实际训练仍受动态博弈与 mode collapse 影响；Flow 用可逆变换和 Jacobian determinant 精确追踪 probability mass，Real NVP 以 triangular coupling 换取 exact likelihood 与 inverse
- 2026-09-25 · **A3 VAE / GAN / Flow / Diffusion 统一概率视角** —— 四类模型都希望 $p_\theta$ 接近 $p_{\mathrm{data}}$：VAE 用 approximate posterior 与 ELBO，GAN 用 adversarial density-ratio signal，Flow 用 bijection 与 Jacobian 获得 exact likelihood，Diffusion 则把 path-space variational bound 化成多步 denoising；它们分别把困难放进 inference gap、动态博弈、可逆架构与迭代采样

## 复习队列（间隔复习：1天 / 3天 / 7天 后各回顾一次要点）

- **A3 四类生成模型统一视角**：能从 $D_{\mathrm{KL}}(p_{\text{data}}\|p_\theta)$ 解释 MLE，并说清 VAE / GAN / Flow / Diffusion 分别优化什么、能否算 likelihood、怎样 sampling 与把难题放在哪里 → 复习于 2026-09-26 / 09-28 / 10-02

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
- **D4 Reliability-guided refinement**：口述“为什么 high uncertainty 不等于 should refine，以及 expected benefit gate 比 risk gate 多判断了什么” → 复习于 2026-09-10 / 09-12 / 09-16
- **E1 多视图几何**：口述“为什么 $\mathbf E$ 作用于归一化坐标、$\mathbf F$ 作用于像素坐标，以及双视图为何仍缺绝对尺度” → 复习于 2026-09-11 / 09-13 / 09-17
- **E2 SfM / COLMAP**：口述“RANSAC 为什么对内点率呈幂次敏感，PnP 怎样把新图接入已有地图，以及 BA 为何必须固定 gauge” → 复习于 2026-09-14 / 09-16 / 09-20
- **E3 NeRF / 3D Gaussian Splatting**：口述“怎样从 transmittance 推出 NeRF 权重，为什么 3DGS 与 NeRF 最终共享 alpha compositing，以及高 PSNR 为何不等于几何准确” → 复习于 2026-09-15 / 09-17 / 09-21
- **E4 偏振成像与 SfP**：口述“怎样从四方向强度恢复 Stokes，AoLP 为什么只有模 $\pi$，以及单视图 normal 为何仍有多解” → 复习于 2026-09-16 / 09-18 / 09-22
- **F1 Video Diffusion**：口述“为什么逐帧 image diffusion 不等于联合视频建模，独立前向噪声为何不妨碍反向时序一致性，以及原像素平滑为何会产生拖影” → 复习于 2026-09-17 / 09-19 / 09-23
- **F2 Action-conditioned Prediction**：口述“为什么 action 不是普通标签，如何用 same-state/different-action 检查模型是否真的使用动作，以及 MPC 为何只执行第一步就重规划” → 复习于 2026-09-19 / 09-21 / 09-25
- **F3 Latent World Models / Dreamer**：口述“posterior 为什么能看当前 observation、prior 为什么不能，以及 KL 与 $\lambda$-return 分别解决哪一段连接问题” → 复习于 2026-09-20 / 09-22 / 09-26
- **F4 Sora / Genie 类世界生成**：口述“autoregressive 与 diffusion 为什么不冲突，并用 action shuffle / same-state different-action 证明 controllability” → 复习于 2026-09-22 / 09-24 / 09-28
- **A1 Latent Variable Models / ELBO / VAE**：口述“为什么引入 $q_\phi(\mathbf z\mid\mathbf x)$、Jensen inequality 怎样产生 ELBO，以及 reparameterization 为何能让梯度回到 encoder” → 复习于 2026-09-24 / 09-26 / 09-30
- **A2 GAN / Normalizing Flow**：口述“为什么最优 discriminator 是 density ratio、怎样推出 JS divergence，以及 Flow 的 Jacobian determinant 为什么用于修正体积变化” → 复习于 2026-09-25 / 09-27 / 10-01
