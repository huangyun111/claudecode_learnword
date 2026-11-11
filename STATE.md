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

- 阶段：**L · 主动感知、具身几何与闭环采集（已完成）**
- 下一篇主菜：**待扩展下一阶段路线图**
- 前沿速览节奏：建议每周二 / 周五各一次（最近：2026-11-04，Dynamic NeRF / 4D Gaussian Splatting）

## 已讲清单

- 2026-11-11 · **阶段 L 复盘：从被动输入到可核验闭环** —— 把主动感知统一为 $b_t(\theta)\rightarrow a_t\rightarrow y_t\rightarrow b_{t+1}(\theta)$ 的 sequential decision loop，从 linear-Gaussian observation 完整推出 measurement Jacobian、Fisher information、posterior precision update 与 log-det information gain，再用 task-conditioned VOI 区分“减少 uncertainty”与“改变正确决定”；把 reachability、visibility、calibration、budget、cost、risk 和 hard safety constraint 接入 action utility，并以 predicted-vs-realized gain、independent geometry / task / physical endpoint、failure / subgroup 与 planner recalibration 封闭最后一条反馈边

- 2026-11-10 · **L4 主动多模态与物理采集** —— 把 viewpoint、illumination、analyzer angle、sensor 与 exposure 统一写成 acquisition action，从 local linearization 推出 measurement Jacobian、Fisher information、posterior precision update 与 log-det information gain，说明主动视角、photometric stereo、Stokes projection、RGB-D / NIR / tactile 等模态怎样通过互补 measurement equation 切断 geometry–material–lighting 多解；再把 visibility、validity、calibration、synchronization、time / energy / safety budget 与 predicted-vs-realized gain 接入闭环，并要求 complete-surface geometry、material、lighting 与 acquisition cost 四类独立端点

- 2026-11-09 · **L3 Task-aware embodied geometry** —— 从 geometry belief 与 task loss 出发，推出 posterior expected task loss、Bayes risk 和 task-conditioned value of information，说明“知道更多”与“足以改变决策”并不等价；再用 configuration space、uncertainty margin、affordance、reachability、friction cone、contact geometry 和 task-weighted error 把 navigation / manipulation 的局部需求接入闭环采集，同时要求 complete-surface geometry、task-region geometry、decision calibration、真实执行与 safety / worst-group 四类独立证据，防止任务成功和几何正确互相冒充

- 2026-11-08 · **L2 SLAM、pose uncertainty 与 active mapping** —— 从 pose 与 map 共同解释 measurement residual 出发，写出 $p(\mathbf X,\mathbf M\mid\mathbf Z,\mathbf U)$ 的 factorization 与 MAP objective，经 linearization、normal equation、information matrix 和 Schur complement 说明 pose–map cross-covariance 怎样削弱表面信息；再把 gauge、loop closure、false closure、neural-map compensation 与 frontier / relocalization / closure utility 接入 active mapping，并用冻结路径 / 帧数 / capacity 下的 trajectory、loop、geometry、efficiency 与 predicted-vs-realized gain 约束闭环建图主张

- 2026-11-07 · **L1 Active Perception 与 Next-Best-View** —— 从“最不确定处不等于最值得拍”出发，用 linear-Gaussian measurement model 完整推出 posterior precision update 与 log-det information gain，说明互补视角怎样切断旧观测的 null direction；再把 visibility、coverage、motion cost、risk 与 model mismatch 接入 action utility，并用冻结帧数 / 路径 / 失败预算下的 random、uniform、frontier、uncertainty 和 oracle controls，以及 predicted-vs-realized gain、surface accuracy / completeness、worst-group 和 held-out scenes 约束 active reconstruction claim

- 2026-11-06 · **阶段 K 复盘：从视频变化到可核验四维场景** —— 从世界点轨迹、针孔投影导数与时变 rendering equation 出发，把 frame / gauge、time / synchronization、identity、visibility、motion / geometry、representation 与 evidence 七份合同串成完整 4D reconstruction 装配线；推导 2D flow 的 depth–motion 多解、同步误差、temporal aliasing 与 canonical reparameterization gauge，并用 held-out view-time、long-range tracks、EPE3D、per-time accuracy / completeness、frozen global alignment、worst-group 与 matched controls 约束 physical 4D recovery claim

- 2026-11-05 · **K4 动态重建的观测与证据合同** —— 从时变场景与成像方程拆开 image reconstruction、novel-view、temporal prediction 与 physical 4D recovery，推导同步误差随运动速度和 time offset 放大；把 scene flow、long-range tracks、visibility / reappearance、per-time geometry 与 frozen global alignment 接成独立 motion / geometry evidence，再用 held-out view-time 网格、micro / macro / worst-group、困难运动 subgroup、matched / shuffled controls 防止静态背景均值和漂亮渲染替代真实四维恢复

- 2026-11-04 · **K3 Dynamic NeRF / 4D Gaussian Splatting** —— 从 time-conditioned spacetime field 与 canonical backward warp 完整推出动态 volume rendering，再从 per-Gaussian deformation、三维 covariance、投影 Jacobian 和 front-to-back compositing 推出 4DGS；说明 densification / pruning 会改变 support、capacity 与 primitive identity，区分遮挡、离开视野、出现 / 消失和数据缺失，并用采样频率的 aliasing 推导证明训练帧完全一致也不能唯一确定帧间运动，最终把 image、temporal、motion、geometry 与 FPS 拆成独立证据合同

- 2026-11-03 · **K2 Canonical space、deformation field 与动态 gauge** —— 用 forward / backward warp 建立跨时间 identity 与共享 template，完整推出任意可逆 canonical 重参数化如何被 radiance field 和 warp 吸收、使 observation-space rendering 不变；说明 cycle consistency 不能消除 gauge，再从 deformation Jacobian 推出 local rigidity 条件 $\mathbf J^\top\mathbf J=\mathbf I$，区分稳定优化的 prior 与真实物理证据，并把 topology change、deformation compensation、visibility、frozen alignment 和独立 4D endpoint 接成动态重建合同

- 2026-11-02 · **K1 Optical flow、scene flow 与相机—物体运动分解** —— 从 pixel + depth + camera pose 完整推出 world-frame scene flow，区分 camera-induced optical flow 与真实物体运动；用“近处慢移 / 远处快移”说明单目深度—运动多解，再把 rigid / piecewise rigid / non-rigid motion、canonical / 4D / per-primitive representation、occlusion、brightness constancy 与独立 motion / geometry endpoint 接成动态重建合同

- 2026-10-31 · **阶段 J 复盘：从可导拟合到可辨识物理场景** —— 把 forward model、observation design、parameterization、optimization 与 independent evidence 组织成五份相互校验的合同；用 measurement Jacobian、null-space intersection、information conditioning 与 representation chain rule 区分 differentiable、identifiable 和 recoverable，并以 held-out view / illumination、固定 support geometry 与 matched mechanism controls 防止 image fit 冒充物理恢复

- 2026-10-30 · **J4 多模态物理线索融合** —— 把 RGB、depth、normal、polarization 与 illumination intervention 统一写成带采集条件、噪声和有效域的 measurement model，用 stacked Jacobian、null-space intersection 与 information matrix 解释何时新模态真正增加可辨识性；区分 depth–normal consistency 与独立证据，推导 DoFP Stokes / DoLP / AoLP 和 calibrated photometric stereo，并以 reliability-aware fusion、missing / conflict handling、matched controls 与独立 geometry endpoint 约束“融合有效”的主张

- 2026-10-29 · **J3 Intrinsic decomposition 与材质—光照解耦** —— 从 rendering equation 与 $I=R\odot S$ 完整推出 albedo–shading scale ambiguity，再沿 Lambertian gradient、microfacet roughness 与 environment lighting 的频率补偿解释 parameter compensation 和 light baking；把同光照 novel view、intrinsic GT、held-out illumination、cross-combination 与物理端点组织成分层 relighting evidence，并为 RGB-only / RGB+polarization 冻结 matched protocol

- 2026-10-28 · **J2 几何表示与正则化** —— 把 mesh、SDF、occupancy 与 3D Gaussians 放进同一 representation contract，逐步推导 mesh Laplacian、SDF Eikonal 与 ray–surface implicit gradient，区分 zero set、distance field、decision boundary 与 radiance primitives；说明 topology、initialization、visibility 和 regularization 如何共同决定优化偏差，并以 fixed-support independent geometry evidence 约束“正则化改善几何”的主张

- 2026-10-27 · **J1 Inverse Graphics 与 differentiable rendering** —— 从 rendering equation 和 Lambertian 小模型拆开 geometry / material / lighting / camera / visibility，完整推导 photometric objective 的链式梯度，区分“能反传”与“参数可辨识”；用 Jacobian null direction 理解多视图、多光照和 polarization 怎样增加约束，并建立 image fitting、geometry、decomposition、mechanism 四层 evidence ladder

- 2026-10-26 · **阶段 I 复盘：从像素到可核验三维场景** —— 把 pixel ray、pointmap、camera、tracks / visibility、gauge alignment、Gaussian rendering 与独立 surface evaluation 串成带验收点的装配线；完整区分 reprojection consistency、novel-view appearance 与 geometry accuracy / completeness，强调固定 frame、support、alignment、budget 和 matched control 后才能把漂亮渲染升级为三维主张

- 2026-10-23 · **I4 从几何 backbone 到 Gaussian reconstruction** —— 从 pointmap / camera 的 frame contract 初始化 Gaussian center，用局部 footprint 与 normal 理解 covariance，再完整推导 $\mathbf\Sigma^{2D}\approx\mathbf J\mathbf R\mathbf\Sigma^w\mathbf R^\top\mathbf J^\top$ 和 front-to-back alpha compositing；把 geometry、appearance、camera 与 regularization loss 分工，并明确 novel-view PSNR 不能替代独立 surface geometry evidence

- 2026-10-22 · **I3 3D tracks、遮挡与跨视图一致性** —— 把 track 定义为同一物理点的跨视图身份，用 reprojection 与 world-frame 3D 会合连接 correspondence、depth 和 camera；显式区分 visibility、confidence 与 coverage，说明 cycle consistency 的必要非充分性，并把 static / dynamic scene、重复纹理、视角相关外观和独立 track / geometry evaluation 分层

- 2026-10-21 · **I2 坐标、相机与 gauge contract** —— 从 W2C / C2W 与 camera center 完整推导相机外参，区分 $z$-depth 与 ray distance、SE(3) 与 Sim(3)，说明纯视觉的 frame / scale gauge freedom，并用冻结的 registration protocol 防止 alignment 掩盖 metric、pose 与几何误差

- 2026-10-20 · **I1 Pointmap 与 feed-forward 3D reconstruction** —— pointmap 是逐像素三维坐标场；从 depth 反投影推导其 camera-frame 约束，再用 pairwise common frame、scale ambiguity、confidence loss、Sim(3) 全局对齐和相机重投影说明它统一了多种几何任务，但没有自动保证 metric scale、可见性与真实几何

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
- 2026-09-27 · **G1 实验设计与证据链** —— 从 population、intervention、control、outcome 与 protocol 定义 research question 和 estimand；baseline 提供参照，matched control 隔离变量，ablation 分解系统，negative control 搜索伪解释，held-out evaluation 阻断选择泄漏，最终把 descriptive、comparative、mechanistic 与 causal claim 分层
- 2026-09-28 · **G2 数据划分与统计汇总** —— split unit 决定结论覆盖的新图像、新物体或新传感器总体；leakage 也包括跨组样本、全量 preprocessing 与 test-driven selection；在匹配的 evaluation unit 上用 paired difference、正确层级 bootstrap、multiple seeds、预定义 subgroup 与 harm/worst-case 报告，避免总均值遮蔽失败
- 2026-09-29 · **G3 指标、决策与可复现记录** —— metric 只定义测量，paired effect 表示相对变化，practical threshold、harm 与成本决定是否值得行动；error taxonomy 把失败图变成可检验假设，run identity 与 artifact package 再把主张绑定到代码、数据、配置、选择规则、evaluator 和输出
- 2026-10-08 · **阶段 G 复盘：完整研究证据链** —— 用 $Q=(P,T,C,O,\Pi)$ 定义 estimand，以 matched design 隔离 nuisance、selection 与 measurement bias，在 claim 对应的 split unit 上计算 paired effect、uncertainty 与 harm，再用 practical threshold 作决策，并以 provenance graph 把 paper claim 追溯到代码、数据、配置、evaluator 和 artifact
- 2026-10-09 · **H1 Claim–Evidence Mapping** —— 把经验性 claim 正规化为 $(P,T,K,O,\Pi,S)$，区分构成性、比较性、机制性与泛化性主张，再用 population、protocol、outcome 与 scope 匹配检查把每句论文表述绑定到恰好足够的 table、figure、limitation 和 artifact；证据不足时只能补实验、降措辞或缩边界
- 2026-10-13 · **H2 Method 叙事与设计必要性** —— 把 Method 写成 design gap、task constraint、mechanism、observable prediction 与 matched evidence 的推导链；用 double-angle representation 和 inverse-variance fusion 展开约束到公式的完整推导，并以 replace / break / stratify 等 counterfactual 检查设计理由而非只列模块
- 2026-10-14 · **H3 Results / Figures / Tables 的证据组织** —— 把 main table、matched ablation、mechanism / subgroup figure、qualitative comparison 与 failure case 分配给不同 claim；用 scene-level paired effect、uncertainty、harm rate、固定显示与六槽 caption 把协议、现象和边界封装成可扫描证据
- 2026-10-16 · **H4 Review、Rebuttal 与答辩** —— 把 concern 正规化为 claim、evidence gap、decision impact、resolution 与 policy boundary，区分事实、协议、机制、泛化和表达问题；按决策相关性选择澄清、纠错、最小 matched check、scope 收缩或承认限制，让 paper、evidence 与 claim 重新一致
- 2026-10-19 · **阶段 H 复盘：从主张到可核验决定** —— 把 claim 的 $P,T,K,O,\Pi,S$ 契约、constraint–mechanism–prediction 设计链、paired effect / uncertainty / harm decision rule、Results evidence routing、argument graph 与 rebuttal 修复串成一条可审计的论文论证闭环

## 复习队列（间隔复习：1天 / 3天 / 7天 后各回顾一次要点）

- **阶段 L 复盘：从被动输入到可核验闭环**：能从 belief / action / observation / update 写出主动感知循环，推出 precision update 与 information gain，区分 global information 与 task-conditioned VOI，把 cost / risk / safety / budget 接入 policy，并用 predicted-vs-realized gain、independent endpoint、failure / subgroup 与 feedback calibration 检查一条 closed-loop claim → 复习于 2026-11-12 / 11-14 / 11-18

- **L4 主动多模态与物理采集**：能从 $\mathbf y_a=f(\boldsymbol\theta;a)+\boldsymbol\varepsilon_a$ 推出 $\mathbf\Lambda_{t+1}=\mathbf\Lambda_t+\mathbf J_a^\top\mathbf R_a^{-1}\mathbf J_a$，解释 viewpoint / light / analyzer / sensor 怎样提供互补 measurement direction，并用 calibration、validity、budget 与 predicted-vs-realized independent endpoint 防止 planner score 冒充真实物理收益 → 复习于 2026-11-11 / 11-13 / 11-17

- **L3 Task-aware embodied geometry**：能从 geometry belief 写出 posterior expected task loss、Bayes risk 与 task-conditioned VOI，解释 configuration space、affordance、reachability 和 friction cone 怎样把几何接到 navigation / manipulation，并用 complete-surface / task-region geometry、decision calibration、execution 与 safety endpoints 防止 task success 冒充 geometry correctness → 复习于 2026-11-10 / 11-12 / 11-16

- **L2 SLAM、pose uncertainty 与 active mapping**：能写出 joint posterior 与 factor-graph MAP objective，从 $\mathbf H$ 的 pose–map block 和 Schur complement 解释为何 pose uncertainty 会吃掉一部分 map information，说明 gauge、true / false loop closure 和 neural-map compensation，并用 trajectory / loop / geometry / efficiency 与 realized gain 检查 active SLAM → 复习于 2026-11-09 / 11-11 / 11-15

- **L1 Active Perception 与 Next-Best-View**：能从 linear-Gaussian measurement model 推出 posterior precision update 与 log-det information gain，解释互补视角为何比重复高分辨率观测更能缩小 uncertainty volume，并用 visibility / coverage / motion / risk / model mismatch 与 predicted-vs-realized gain、独立 geometry endpoint 检查一个 NBV policy → 复习于 2026-11-08 / 11-10 / 11-14

- **阶段 K 复盘：从视频变化到可核验四维场景**：能从 $\mathbf u\sim\mathbf K[\mathbf R\mid\mathbf t]\mathbf X(t)$ 解释像素为何压缩 geometry / motion / camera / visibility，依次检查 frame、time、identity、visibility、representation、3D endpoint 与 held-out evidence 七份合同，并说明 high PSNR / FPS 为什么不能替代 physical 4D recovery → 复习于 2026-11-07 / 11-09 / 11-13

- **K4 动态重建的观测与证据合同**：能解释同步误差为何近似为 $\|\mathbf v\||\Delta t|$，区分 held-out view / time / view-time / future time，用 EPE3D、long-range tracks、per-time geometry、frozen global alignment 与 worst-group 阻止静态背景和逐帧对齐掩盖动态失败 → 复习于 2026-11-06 / 11-08 / 11-12

- **K3 Dynamic NeRF / 4D Gaussian Splatting**：能从 dynamic ray、backward warp、density / radiance 写出离散 volume rendering，解释 per-Gaussian deformation 如何经 covariance projection 和 alpha compositing 形成像素，说明 densification / pruning 为何改变 support / identity、稀疏时间采样为何产生 aliasing，并为 image / motion / geometry / FPS 分开设计 endpoint → 复习于 2026-11-05 / 11-07 / 11-11

- **K2 Canonical space、deformation field 与动态 gauge**：能写出 forward / backward warp 与任意可逆 canonical reparameterization，解释 cycle consistency 为什么不能消除 gauge，从 $\mathbf J^\top\mathbf J=\mathbf I$ 推出 local rigidity，并区分 deformation prior、topology change、module compensation 与独立 4D evidence → 复习于 2026-11-04 / 11-06 / 11-10

- **K1 Optical flow、scene flow 与相机—物体运动分解**：能从 pixel + depth + C2W pose 写出两个时刻的 world point 与 scene flow，解释静态背景为何 optical flow 非零但 world motion 为零、同一 2D flow 为何对应不同 metric motion，并为动态重建分开 motion / geometry / rendering endpoints → 复习于 2026-11-03 / 11-05 / 11-09

- **阶段 J 复盘：从可导拟合到可辨识物理场景**：能沿 forward / observation / representation / optimization / evidence 五份合同排查 inverse graphics 系统，手推 Jacobian null direction 与 parameterization chain rule，区分 differentiable、identifiable、recoverable，并为 polarization geometry claim 冻结 matched controls 与 independent endpoints → 复习于 2026-11-01 / 11-03 / 11-07

- **J4 多模态物理线索融合**：能用 stacked Jacobian / null-space intersection 判断新模态是否增加局部可辨识信息，区分 derived normal 与独立观测，解释 polarization 和 illumination intervention 的约束与 ambiguity，并为 RGB-only / RGB+physical-cue 设计 calibration、validity、conflict、matched-control 和 independent-endpoint 合同 → 复习于 2026-10-31 / 11-02 / 11-06

- **J3 Intrinsic decomposition 与材质—光照解耦**：能从 rendering equation 化简并手推 $R'=cR,S'=S/c$ 的 scale ambiguity，解释 roughness / environment lighting compensation 与 light baking，用同光照 novel view / intrinsic GT / held-out illumination / cross-combination 分层判断分解证据，并为 polarization 设计 fixed-renderer matched control → 复习于 2026-10-30 / 11-01 / 11-05

- **J2 几何表示与正则化**：能比较 mesh / SDF / occupancy / 3D Gaussians 的 surface 定义、gradient path、topology 和 initialization，手推 ray–SDF implicit gradient，解释 same zero set 不等于 same distance field、same rendered depth 不等于 same surface thickness，并为 polarization geometry cue 设计 fixed-representation matched control → 复习于 2026-10-29 / 10-31 / 11-04

- **J1 Inverse Graphics 与 differentiable rendering**：能从 rendering equation 化简到 Lambertian 单像素模型，手推 albedo–lighting ambiguity 与 photometric loss 梯度，解释 differentiability 为什么不等于 identifiability，并为一个 inverse method 分开列出图像、几何、分解和机制证据 → 复习于 2026-10-28 / 10-30 / 11-03

- **阶段 I 复盘：从像素到可核验三维场景**：能沿 pixel ray / pointmap / camera / tracks / gauge / Gaussian / evaluation 定位最早坏掉的 contract，区分 camera、correspondence、appearance、geometry 四张成绩单，并解释 accuracy / completeness 为什么必须在固定 support 下共同报告 → 复习于 2026-10-27 / 10-29 / 11-02

- **I4 从几何 backbone 到 Gaussian reconstruction**：能从 pointmap / camera 写出 Gaussian center 初始化，解释 covariance 如何经投影 Jacobian 变成 screen-space footprint，区分 geometry / appearance loss，并说明 novel-view PSNR 为什么不能证明 surface geometry 正确 → 复习于 2026-10-24 / 10-26 / 10-30

- **I3 3D tracks、遮挡与跨视图一致性**：能把 track 写成 $(i,\mathbf p_{ik},v_{ik})$ 观测集合，解释 visibility 为什么不能被 confidence 替代、cycle consistency 为什么不是充分条件，并区分 static point 与 dynamic 4D track → 复习于 2026-10-23 / 10-25 / 10-29

- **I2 坐标、相机与 gauge contract**：能从 W2C 外参推出 camera center，区分 SE(3) / Sim(3) alignment 与 $z$-depth / ray distance，并说明 registration protocol 为什么决定一条 metric claim 是否成立 → 复习于 2026-10-22 / 10-24 / 10-28

- **I1 Pointmap 与 feed-forward 3D reconstruction**：能从 $\mathbf X=z\mathbf K^{-1}\tilde{\mathbf p}$ 推出逐像素 xyz，解释 pairwise common frame 与 Sim(3) 对齐，并说明为何直接输出 xyz 仍不自动拥有 metric scale 或可靠 confidence → 复习于 2026-10-21 / 10-23 / 10-27

- **阶段 H 复盘：从主张到可核验决定**：能从一条 claim 反推 constraint、mechanism、observable prediction、protocol、evidence、decision rule 与 artifact，并说明 review concern 应落在哪条论证边上 → 复习于 2026-10-20 / 10-22 / 10-26

- **H4 Review、Rebuttal 与答辩**：能为一条 concern 填写 claim / gap / impact / resolution / boundary 五槽，区分澄清、补证据与缩 scope，并用 Concern / Answer / Evidence / Consequence 写成闭环回应 → 复习于 2026-10-17 / 10-19 / 10-23

- **H3 Results / Figures / Tables 的证据组织**：能说明 main table、matched ablation、mechanism figure、qualitative comparison 与 failure case 分别回答什么，并为 caption 填写 what / data / encoding / metric / uncertainty / boundary 六槽 → 复习于 2026-10-15 / 10-17 / 10-21

- **H2 Method 叙事与设计必要性**：能为一个模块填写 gap / constraint / mechanism / prediction / evidence 五槽位，区分“约束必须处理”与“当前结构是唯一解”，并给出 matched replacement 或 cue intervention → 复习于 2026-10-14 / 10-16 / 10-20

- **H1 Claim–Evidence Mapping**：能把一句论文主张写成 $(P,T,K,O,\Pi,S)$，区分比较、机制与泛化 claim 的最低证据，并在证据不足时选择补实验、降措辞或缩 scope → 复习于 2026-10-10 / 10-12 / 10-16

- **阶段 G 复盘：完整研究证据链**：能从一个自然语言 claim 写出 $Q=(P,T,C,O,\Pi)$，解释 matched control、split / bootstrap unit、decision rule 与 provenance graph 怎样首尾相接 → 复习于 2026-10-09 / 10-11 / 10-15

- **G3 指标、决策与可复现记录**：能区分 effect size、statistical uncertainty 与 practical significance，为一次运行写出 $R=(C,D,S,H,E)$，并说明 artifact 可下载、可运行和复得主要结论为何是不同强度 → 复习于 2026-09-30 / 10-02 / 10-06

- **G1 实验设计与证据链**：能为一个模块写出 $P,T,C,O,\Pi$，区分 baseline / matched control / ablation / negative control，并说明为什么 test set 只要参与决策就不再 truly held-out → 复习于 2026-09-28 / 09-30 / 10-04

- **G2 数据划分与统计汇总**：能说明 split unit 如何决定泛化声称，写出 paired difference 和 bootstrap 重采样单位，并区分 sample、seed 与 subgroup uncertainty → 复习于 2026-09-29 / 10-01 / 10-05

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
