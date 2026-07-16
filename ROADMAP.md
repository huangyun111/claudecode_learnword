# 知识路线图（ROADMAP）

主线：**可控密集预测 → 可控生成 → 世界模型**。
已从 **阶段 B（可控生成 / 扩散系统化）** 起步并完成，现进入阶段 C；阶段 A 按需回填，之后 D → E → F 推进。
每天主菜推进一个 ☐ 条目，讲完打勾并在 `STATE.md` 记录。

---

## 阶段 A · 生成模型统一视角（前置地基，按需简讲）

- ☐ latent variable models 与 ELBO；VAE
- ☐ GAN / Normalizing Flow 的核心思想与对比
- ☐ 四类生成模型（VAE / GAN / Flow / Diffusion）的统一概率视角

## 阶段 B · 可控生成 / 扩散系统化

- ☑ **B1 DDPM**：前向加噪、反向去噪、训练目标、为什么 work　（2026-06-26 ✅）
- ☑ **B2 DDPM → DDIM**：确定性采样、加速、隐空间语义与可逆性　（2026-06-29 ✅）
- ☑ **B3 Score-based / SDE 统一框架**：score matching、forward/reverse SDE、probability-flow ODE　（2026-07-01 ✅）
- ☑ **B4 条件生成与 Guidance**：classifier guidance、classifier-free guidance（CFG）、权衡　（2026-07-02 ✅）
- ☑ **B5 条件注入机制**：cross-attention、ControlNet、T2I-Adapter（贴偏振表征生成）　（2026-07-06 ✅）
- ☑ **B6 Latent Diffusion（LDM / SD）**：为什么进 latent、VAE + diffusion 的协同　（2026-07-07 ✅）
- ☑ **B7 采样加速**：DPM-Solver、consistency models、distillation　（2026-07-09 ✅）
- ☑ **B8 训练实操**：noise schedule、v-prediction、EMA、混合精度与多卡工程　（2026-07-16 ✅）

## 阶段 C · 不确定性建模 ⭐当前

- ☐ aleatoric vs epistemic 不确定性
- ☐ 贝叶斯深度学习、MC dropout、deep ensembles
- ☐ reliability / confidence estimation（**贴我 CVPR 方法核心**）
- ☐ 不确定性在密集预测中的落地用法

## 阶段 D · 可控密集预测

- ☐ 单目深度估计范式（metric vs relative、scale-shift）
- ☐ 法向量估计、深度↔法向几何约束、多任务联合
- ☐ 用 diffusion 做密集预测（Marigold / DDP 类）
- ☐ reliability-guided / confidence-guided 残差修正思想

## 阶段 E · 3D 与多视图（含偏振）

- ☐ 多视图几何基础、对极几何
- ☐ SfM / COLMAP 管线
- ☐ NeRF / 3D Gaussian Splatting
- ☐ 偏振成像物理 → 偏振-法向-形状（Shape from Polarization）

## 阶段 F · 世界模型

- ☐ video diffusion 基础
- ☐ action-conditioned prediction
- ☐ latent world models（Dreamer 类）
- ☐ Sora / Genie 类与可控生成的关系

---

> 路线图不是死的：可随时插入临时主题、调整顺序，或按实验需求临场改方向。
> 调整时同步更新本文件与 `STATE.md`。
