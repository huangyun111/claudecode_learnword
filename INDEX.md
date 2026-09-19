# 推送索引（INDEX）

按日期倒序记录每天推送，方便回看与检索。

| 日期 | 主菜标题 | 阶段 | 标签 |
|---|---|---|---|
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
