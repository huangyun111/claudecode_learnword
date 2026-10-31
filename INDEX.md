# 推送索引（INDEX）

按日期倒序记录每天推送，方便回看与检索。

| 日期 | 主菜标题 | 阶段 | 标签 |
|---|---|---|---|
| 2026-10-31 | 阶段 J 复盘：从“渲染得像”到“恢复得对”——可辨识物理场景的五道关 | J·复盘 | inverse graphics, differentiable rendering, identifiability, forward model, observation design, parameterization, optimization, independent evidence |
| 2026-10-30 | 当 RGB、深度、法向与偏振同时说话：多模态融合怎样真正减少物理多解 | J4 | multimodal fusion, inverse graphics, identifiability, RGB-D, surface normal, polarization, photometric stereo, illumination intervention, uncertainty, sensor calibration |
| 2026-10-29 | 把光从物体上“剥下来”：Intrinsic Decomposition 为什么不能只靠重建原图 | J3 | intrinsic decomposition, inverse rendering, albedo, normal, roughness, environment lighting, BRDF, light baking, relighting, identifiability |
| 2026-10-28 | Mesh、SDF、Occupancy 与 3D Gaussians：你选择的几何表示，正在替优化决定答案 | J2 | geometry representation, mesh, SDF, occupancy, 3D Gaussian Splatting, regularization, topology, differentiable rendering, geometry bias |
| 2026-10-27 | 把照片倒着渲染：Inverse Graphics 为什么不只是“让渲染器可导” | J1 | inverse graphics, inverse rendering, differentiable rendering, rendering equation, identifiability, geometry, material, lighting, visibility |
| 2026-10-26 | 阶段 I 复盘：从像素到可核验三维场景——别让一张好看的新视图替你证明几何 | I·复盘 | feed-forward 3D, pointmap, camera, gauge, 3D tracks, visibility, Gaussian rendering, geometry evaluation, evidence chain |
| 2026-10-23 | 从 Geometry Backbone 到 Gaussian Reconstruction：有了三维点，为什么还没有一幅可渲染的新视图 | I4 | geometry backbone, 3D Gaussian Splatting, pointmap, camera, covariance, opacity, appearance loss, geometry loss, novel-view synthesis |
| 2026-10-22 | 3D Tracks、遮挡与跨视图一致性：同一个表面点怎样在多张图里保持身份 | I3 | 3D tracks, correspondence, visibility, occlusion, reprojection, cycle consistency, dynamic scene, tracking evaluation |
| 2026-10-21 | 坐标、相机与 Gauge Contract：为什么“对齐后很好看”仍可能算错几何 | I2 | coordinate frame, camera extrinsics, W2C, C2W, SE(3), Sim(3), gauge freedom, registration, metric scale |
| 2026-10-20 | Pointmap 与前馈式 3D 重建：模型直接回归三维点，是否就绕开了相机几何 | I1 | pointmap, feed-forward 3D reconstruction, DUSt3R, VGGT, camera frame, projective geometry, Sim(3), confidence |
| 2026-10-19 | 阶段 H 复盘：一篇论文不是结果集合，而是一条“主张到决定”的可核验链 | H·复盘 | paper argument, claim–evidence mapping, method necessity, results organization, rebuttal, decision rule, traceability, scope |
| 2026-10-16 | Review / Rebuttal / 答辩：不要“赢过质疑”，要让争议变成可核验的判断 | H4 | peer review, rebuttal, defense, concern taxonomy, evidence gap, scope control, response matrix, decision relevance |
| 2026-10-14 | Results / Figures / Tables：让读者扫一眼，就能找到每条主张的证据 | H3 | results organization, main table, matched ablation, qualitative comparison, failure case, caption, paired effect, uncertainty |
| 2026-10-13 | Method 叙事与设计必要性：别从模块名字开始，要从不可回避的约束开始 | H2 | method narrative, design gap, constraint, identifiability, inductive bias, representation, reliability weighting, ablation |
| 2026-10-09 | Claim–Evidence Mapping：论文里的每一句主张，究竟需要什么证据 | H1 | claim–evidence mapping, claim taxonomy, scope, matched evidence, traceability, limitations, artifact |
| 2026-10-08 | 从“我有一个想法”到“我有一条证据链”：研究实验怎样首尾闭环 | G·复盘 | research evidence, estimand, matched control, paired evaluation, uncertainty, decision rule, provenance, reproducibility |
| 2026-09-29 | 指标、决策与可复现记录：0.1° 提升什么时候才值得采用 | G3 | effect size, practical significance, decision rule, error taxonomy, failure analysis, experiment tracking, artifact package, reproducibility |
| 2026-09-28 | 数据划分与统计汇总：别让“平均提升”偷走实验结论 | G2 | data split, leakage, selection bias, paired evaluation, bootstrap, multiple seeds, subgroup, worst-case reporting |
| 2026-09-27 | 实验设计与证据链：一张更高的指标表，究竟能证明什么 | G1 | experimental design, research question, hypothesis, estimand, baseline, matched control, ablation, negative control, held-out evaluation, causal claim |
| 2026-09-25 | VAE / GAN / Flow / Diffusion：四类生成模型到底把难题藏在了哪里 | A3 | generative modeling, maximum likelihood, VAE, GAN, Normalizing Flow, Diffusion, ELBO, implicit model, exact likelihood, denoising |
| 2026-09-24 | GAN 与 Normalizing Flow：一个不写密度也会生成，一个把密度算得清清楚楚 | A2 | GAN, discriminator, minimax game, Jensen–Shannon divergence, mode collapse, Normalizing Flow, change of variables, Jacobian, Real NVP, exact likelihood |
| 2026-09-23 | VAE 与 ELBO：为什么给数据加入“看不见的变量”，反而更容易学习生成 | A1 | latent variable model, variational inference, ELBO, VAE, encoder, decoder, reparameterization, KL divergence |
| 2026-09-21 | Sora / Genie 类世界生成：会生成视频，离“可交互世界模型”还有几道门 | F4 | Sora, Genie, world model, video diffusion, interactive generation, latent action, action controllability, counterfactual, planning |
| 2026-09-19 | Latent World Models（Dreamer）：不必画出每个未来像素，怎样在“想象”里学会行动 | F3 | latent world model, Dreamer, RSSM, posterior, prior, latent imagination, actor-critic, lambda return, model-based reinforcement learning |
| 2026-09-18 | Action-conditioned Prediction：模型怎样预测“我这样做以后会发生什么” | F2 | action-conditioned prediction, state transition, intervention, stochastic dynamics, visual foresight, model predictive control, world model |
| 2026-09-16 | Video Diffusion：把“每帧都好看”升级为“整段运动说得通” | F1 | video diffusion, spatiotemporal denoising, temporal attention, motion, consistency, video prediction, world model |
| 2026-09-15 | 偏振成像与 Shape from Polarization：四张灰度图怎样约束表面法向 | E4 | polarization imaging, Stokes, DoLP, AoLP, Fresnel, Shape from Polarization, surface normal, ambiguity |
| 2026-09-14 | NeRF / 3D Gaussian Splatting：同一组照片，为何一种沿射线积分，另一种把椭球投到屏幕 | E3 | NeRF, neural radiance field, volume rendering, transmittance, 3D Gaussian Splatting, alpha compositing, novel view synthesis |
| 2026-09-13 | SfM / COLMAP：怎样从一堆无序照片恢复相机与三维结构 | E2 | Structure from Motion, COLMAP, local features, matching, RANSAC, PnP, triangulation, bundle adjustment |
| 2026-09-10 | 多视图几何基础：第二台相机怎样把一条射线变成一个三维点 | E1 | multi-view geometry, pinhole camera, rigid transform, epipolar geometry, essential matrix, fundamental matrix, triangulation |
| 2026-09-09 | Reliability-guided Residual Refinement：不是“哪里可能错就改哪里”，而是先判断“改了是否更好” | D4 | reliability, residual refinement, expected benefit, no-harm gate, bounded residual, causal ablation |
| 2026-09-08 | Diffusion 做密集预测：从“生成一张图”到“估计每个像素的深度” | D3 | dense prediction, conditional diffusion, Marigold, monocular depth, ensemble, affine alignment, uncertainty, efficiency |
| 2026-09-07 | 深度与法向：一张“距离图”怎样变成一张“朝向图” | D2 | surface normal estimation, depth-normal consistency, perspective projection, camera intrinsics, multi-task learning |
| 2026-07-30 | 单目深度估计：一张图里的“远近”，为什么不天然等于真实米数 | D1 | monocular depth estimation, metric depth, relative depth, scale ambiguity, shift ambiguity, inverse depth, evaluation |
| 2026-07-27 | Dense Prediction Uncertainty：一张像素级不确定性图，怎样真正参与决策 | C4 | dense prediction, pixel-wise uncertainty, heteroscedastic NLL, selective prediction, active learning, safe refinement |
| 2026-07-26 | Reliability / Confidence Estimation：模型说“我有把握”，这句话可信吗 | C3 | reliability, confidence, calibration, temperature scaling, selective prediction, risk-coverage |
| 2026-07-25 | Bayesian Deep Learning：让神经网络不只给答案，也表达“我可能没学会” | C2 | Bayesian deep learning, posterior predictive, MC Dropout, Deep Ensembles, epistemic uncertainty |
| 2026-07-22 | Aleatoric vs Epistemic：模型说“不确定”时，到底在不确定什么 | C1 | uncertainty, aleatoric, epistemic, heteroscedastic regression, predictive variance |
| 2026-07-16 | Diffusion 训练实操：真正决定模型能不能稳定收敛的细节 | B8 | diffusion, training, noise schedule, v-prediction, EMA, mixed precision, DDP |
| 2026-07-09 | 采样加速：为什么扩散模型可以少走很多步 | B7 | diffusion, sampling acceleration, DPM-Solver, consistency models, distillation |
| 2026-07-07 | Latent Diffusion：为什么 Stable Diffusion 不在像素里直接扩散 | B6 | diffusion, latent diffusion, Stable Diffusion, VAE |
| 2026-07-06 | 条件注入机制：条件不是贴标签，而是进入 U-Net 的特征流 | B5 | diffusion, conditional generation, cross-attention, ControlNet, T2I-Adapter |
| 2026-07-02 | Guidance：条件生成不是“加提示词”，而是在改写 score 方向 | B4 | diffusion, guidance, CFG, conditional generation |
| 2026-07-01 | Score/SDE：把 DDPM 和 DDIM 收进同一张地图 | B3 | diffusion, score matching, SDE, ODE |
| 2026-06-29 | DDIM：同一个网络，把上千步压到几十步 | B2 | diffusion, DDIM, 确定性采样, 加速 |
| 2026-06-26 | DDPM 完整推导：从「加噪」到「猜噪声」 | B1 | diffusion, DDPM, ELBO, 推导 |
