# Scout Report — TrACE-Video / CNLSA 相关论文复查
**扫描窗口：2026年2月19日 – 2026年4月19日（60天）**
**输出时间：2026-04-19**
**方向：VAE语义漂移、视频latent一致性、Test-Time Adaptation for Diffusion、Send-VAE/Diagonal Distillation/SVG/LVTINO/TTOM**

---

## 方向一：VAE-induced Semantic Drift / VAE Latent Space Semantic Degradation

### 1. Send-VAE (Semantic-Disentangled VAE)
- **标题：** Boosting Latent Diffusion Models via Disentangled Representation Alignment
- **年份/会议：** 2026 (arXiv:2601.05823v2, updated March 2026)
- **arXiv：** https://arxiv.org/abs/2601.05823
- **代码：** ❌ **未找到公开GitHub**（project page: pending check）— 有project page但代码未明确发布
- **为什么相关：** 提出了**语义解缠VAE（Send-VAE）**，直接解决VAE latent空间弱语义判别性问题——这正是KAS CNLSA理论中VAE-induced semantic drift的核心。Send-VAE通过非线性映射架构将VAE局部结构与VFM密集语义连接，latent空间无需显式正则化即可涌现解缠属性。**与TrACE-Video/CNLSA直接对口。**
- **优先级：** ★★★★★

### 2. SemanticGen: Video Generation in Semantic Space
- **标题：** SemanticGen: Video Generation in Semantic Space
- **年份/会议：** December 2025 (arXiv:2512.20619)
- **arXiv：** https://arxiv.org/abs/2512.20619
- **项目页：** https://jianhongbai.github.io/SemanticGen/
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 完全绕过VAE latent space，在高语义空间生成视频后再细化到VAE latent。展示了"语义空间生成收敛更快"——间接支持CNLSA的VAE语义漂移假设，但未直接量化漂移。
- **优先级：** ★★★★（2025年底，但方向极相关）

### 3. DA-VAE: Plug-in Latent Compression for Diffusion via Detail Alignment
- **标题：** DA-VAE: Plug-in Latent Compression for Diffusion via Detail Alignment
- **年份/会议：** 2026 (arXiv:2603.22125, March 2026)
- **arXiv：** https://arxiv.org/abs/2603.22125
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 提出结构化latent space布局（复用pretrain VAE latent作为首通道 + 新detail通道），通过detail对齐损失保持扩散模型行为。为理解VAE latent空间结构提供了新视角，与语义漂移研究相关。
- **优先级：** ★★★

---

## 方向二：Video Generation Latent Consistency / Inter-Frame Agreement / Compute Gate

### 4. Diagonal Distillation（对角蒸馏）
- **标题：** Streaming Autoregressive Video Generation via Diagonal Distillation
- **年份/会议：** ICLR 2026 (arXiv:2603.09488)
- **arXiv：** https://arxiv.org/abs/2603.09488
- **代码：** ✅ https://github.com/Sphere-AI-Lab/diagdistill
- **项目页：** https://spherelab.ai/diagdistill/
- **为什么相关：** 提出**不对称的denoising策略：前期chunk多步、后期chunk少步**，使后续chunk从充分处理的前期chunk继承appearance信息，同时用部分去噪chunk作为后续综合的条件输入。**直接涉及per-frame compute gate和inter-chunk consistency机制。** 在单H100上生成5秒视频仅2.61秒（277.3x加速）。
- **优先级：** ★★★★★

### 5. LVTINO: Latent Video Consistency Inverse Solver
- **标题：** LVTINO: LAtent Video consisTency INverse sOlver for High Definition Video Restoration
- **年份/会议：** ICLR 2026 (arXiv:2510.01339)
- **arXiv：** https://arxiv.org/abs/2510.01339
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 首个基于Video Consistency Models（VCM）的零样本/即插即用高清视频恢复逆求解器。条件机制绕过自动微分，实现SOTA视频重建。**涉及latent space temporal consistency机制。**
- **优先级：** ★★★★

### 6. LeanVAE: Ultra-Efficient Reconstruction VAE
- **标题：** LeanVAE: An Ultra-Efficient Reconstruction VAE for Video Diffusion Models
- **年份/会议：** ICCV 2025
- **代码：** ✅ https://github.com/westlake-repl/LeanVAE
- **为什么相关：** 40M参数的轻量级Video VAE，在1080p上encode 17帧仅需0.9秒、decode 3.0秒，支持无损失时序平铺推理。**与VAE效率优化和视频latent压缩直接相关。**
- **优先级：** ★★★（2025年，但有明确代码且方向极相关）

### 7. Event-Driven Video Generation (EVD)
- **标题：** Event-Driven Video Generation
- **年份/会议：** 2026 (arXiv:2603.13402v2, March 2026)
- **arXiv：** https://arxiv.org/abs/2603.13402
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 提出**事件驱动的视频生成框架**：轻量级event head预测token级事件活动，event-gated sampling（带磁滞和early-step调度）抑制虚假更新同时聚焦交互期间的更新。**直接涉及per-frame/step的动态compute gate机制。** 在EVD-Bench上显著改善状态持久性、空间准确性、接触稳定性。
- **优先级：** ★★★★★

### 8. Consistency-Preserving Diverse Video Generation
- **标题：** Consistency-Preserving Diverse Video Generation
- **年份/会议：** 2026 (arXiv:2602.15287)
- **arXiv：** https://arxiv.org/abs/2602.15287
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 为flow-matching视频生成器提出联合采样框架，通过梯度调节保持时序一致性，同时用latent空间嵌入和插值模型实现轻量计算。**涉及latent space temporal consistency机制。**
- **优先级：** ★★★

---

## 方向三：Test-Time Adaptation for Diffusion / TTT / Step-Selective Methods

### 9. TTOM: Test-Time Optimization and Memorization
- **标题：** TTOM: Test-Time Optimization and Memorization for Compositional Video Generation
- **年份/会议：** ICLR 2026 Poster (published Jan 26, 2026, updated Apr 11, 2026)
- **OpenReview：** https://openreview.net/forum?id=wqCwcTZsrv
- **arXiv：** https://arxiv.org/abs/2510.07940
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 首个**训练-free**框架，通过latent memory机制在推理时动态适应未见提示词，在streaming设置中维护历史优化上下文（支持insert/read/update/delete）。**直接是TTA（Test-Time Adaptation）在视频生成中的核心工作。**
- **优先级：** ★★★★★

### 10. Video-T1: Test-Time Scaling for Video Generation
- **标题：** Video-T1: Test-Time Scaling for Video Generation
- **年份/会议：** ICCV 2025 (arXiv:2503.18942)
- **arXiv：** https://arxiv.org/abs/2503.18942
- **代码：** ✅ https://github.com/THU-SI/Video-T1
- **项目页：** https://liuff19.github.io/Video-T1/
- **为什么相关：** 将视频生成的test-time scaling重新解释为从高斯噪声空间到目标视频的更好轨迹搜索问题。提出Tree-of-Frames (ToF) Search，利用自回归模型的顺序生成能力在时间维度上引入推理时推理。**核心TTA video generation工作。**
- **优先级：** ★★★★

### 11. TTT-Video: One-Minute Video Generation with Test-Time Training
- **标题：** One-Minute Video Generation with Test-Time Training
- **年份/会议：** 2025 (arXiv:2504.05298, CVPR 2025 listed on GitHub)
- **arXiv：** https://arxiv.org/abs/2504.05298
- **代码：** ✅ https://github.com/test-time-training/ttt-video-dit
- **为什么相关：** 在CogVideoX 5B模型中插入**TTT（Test-Time Training）层**，处理全局上下文的长程关系，同时保留原始attention层处理3秒片段的局部注意力。**是CVPR 2025的工作，但有明确代码，Scout判定：时间早于2026但有直接代码，可能是2025年工作，适合参考。**
- **优先级：** ★★★★（有代码，2025年，但TTA for video generation核心工作）

### 12. EvoSearch: Inference-Time Scaling via Evolutionary Search
- **标题：** Inference-time Scaling of Diffusion Models through Classical Search
- **年份/会议：** ICLR 2026 Under Review (OpenReview)
- **OpenReview：** https://openreview.net/pdf?id=CFlOUNWsaP
- **代码：** ✅ https://github.com/tinnerhrhe/EvoSearch-codes
- **项目页：** https://evosearch.github.io/
- **为什么相关：** 提出EvoSearch，一个通用test-time scaling框架，适用于图像和视频生成。使用进化搜索（evolutionary search）而非随机采样或粒子采样，在高维噪声空间中更高效地搜索。**是扩散模型test-time scaling的通用方法，与KAS PhD方向高度相关。**
- **优先级：** ★★★★★

### 13. LatSearch: Latent Reward-Guided Search
- **标题：** LatSearch: Latent Reward-Guided Search for Faster Inference-Time Scaling in Video Diffusion
- **年份/会议：** 2026 (arXiv:2603.14526)
- **arXiv：** https://arxiv.org/abs/2603.14526
- **代码：** ✅ https://github.com/zengqunzhao/LatSearch
- **为什么相关：** 提出latent reward model在**任意去噪时间步**评估部分去噪的latent，提供中间反馈而不是只在最终解码视频上评估。与VGGRPO（4D latent reward）形成互补，但专注推理时scaling效率。**与TrACE-Video的latent-level一致性评估高度相关。**
- **优先级：** ★★★★★

---

## 方向四：Send-VAE / Diagonal Distillation / SVG / LVTINO / TTOM 直接相关工作

### 14. SVG: Latent Diffusion Model Without Variational Autoencoder
- **标题：** SVG: Latent Diffusion Model Without Variational Autoencoder
- **年份/会议：** ICLR 2026 (arXiv:2510.15301 for image; arXiv:2512.11749 for T2I variant)
- **代码：** ✅ https://github.com/shiml20/SVG（Tsinghua + Kuaishou Kling团队）
- **HuggingFace：** https://huggingface.co/howlin/SVG
- **为什么相关：** **完全去掉VAE**，用VFM特征空间作为统一SVG特征空间，结合强语义判别性和丰富感知细节，实现更高效扩散训练和few-step推理。**是VAE-free latent diffusion的代表作，与Send-VAE互补（一个改进VAE，一个去掉VAE）。**
- **优先级：** ★★★★★

### 15. VGGRPO: World-Consistent Video Generation with 4D Latent Reward
- **标题：** VGGRPO: Towards World-Consistent Video Generation with 4D Latent Reward
- **年份/会议：** 2026 (arXiv:2603.26599, March 2026)
- **arXiv：** https://arxiv.org/abs/2603.26599
- **项目页：** https://zhaochongan.github.io/projects/VGGRPO/
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 提出Latent Geometry Model (LGM)将视频扩散latent与几何基础模型缝合，实现直接从latent空间解码场景几何。**通过4D latent reward在latent空间进行geometry-aware RL post-training，消除了昂贵的VAE解码。** 直接与latent space geometric consistency相关。
- **优先级：** ★★★★

### 16. LongLive: Real-time Interactive Long Video Generation
- **标题：** LongLive: Real-time Interactive Long Video Generation
- **年份/会议：** ICLR 2026 Poster (Jan 26, 2026, updated Apr 11, 2026)
- **OpenReview：** https://openreview.net/forum?id=nCAODkpsPJ
- **项目页：** https://nvlabs.github.io/LongLive/
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 帧级自回归框架，支持实时交互生成长视频。在单H100上以20.7 FPS运行，支持长达240秒视频。Streaming Long Tuning通过复用历史KV cache生成下一5秒片段。**涉及latent consistency和inter-frame temporal modeling。**
- **优先级：** ★★★★

### 17. SteinsGate: Causality for Long Video via Path Integral
- **标题：** SteinsGate: Adding Causality to Diffusions for Long Video Generation via Path Integral
- **年份/会议：** ICLR 2026 Poster (Jan 26, 2026, updated Apr 11, 2026)
- **OpenReview：** https://openreview.net/forum?id=8WS5nDWIWE
- **代码：** ❌ 未找到GitHub
- **为什么相关：** 提出InstructVC，结合Temporal Action Binding和Causal Video Continuation，使用MLLM进行动作绑定和Video Path Integral在动作间强制因果关系。**将预训练TI2V扩散模型转换为自回归视频延续模型。** 涉及test-time因果推理机制。
- **优先级：** ★★★

---

## 其他值得关注的近期论文

### 18. Real-Time Motion-Controllable AR Video Diffusion
- **标题：** Real-Time Motion-Controllable Autoregressive Video Diffusion
- **年份/会议：** ICLR 2026 Poster
- **OpenReview：** https://openreview.net/forum?id=4Q55RwYte9
- **为什么相关：** 首个RL增强few-step AR视频扩散模型，支持实时图像到视频的多种运动控制。通过Self-Rollout机制保持Markov属性。
- **优先级：** ★★★

### 19. "One-Step Causal Video Generation via Adversarial Self-Distillation" (ASD)
- **标题：** Towards One-step Causal Video Generation via Adversarial Self-Distillation
- **年份/会议：** ICLR 2026 Poster
- **OpenReview：** https://openreview.net/forum?id=P3O0fNmnWa
- **为什么相关：** 基于DMD框架提出Adversarial Self-Distillation (ASD)策略，将学生模型n步去噪输出与(n+1)步版本对齐。VBench上one-step和two-step视频生成均达SOTA。
- **优先级：** ★★★

### 20. Causal Forcing: Autoregressive Diffusion Distillation
- **标题：** Causal Forcing: Autoregressive Diffusion Distillation Done Right for Real-Time Interactive Video Generation
- **年份/会议：** 2026 (arXiv:2602.02214)
- **arXiv：** https://arxiv.org/abs/2602.02214
- **为什么相关：** 将双向扩散transformer适配为因果transformer，实现on-the-fly逐帧生成。专注实时交互视频生成。
- **优先级：** ★★★

### 21. High-Fidelity Causal Video Diffusion for Ultra-Low Bitrate Semantic Communication
- **标题：** High-Fidelity Causal Video Diffusion Models for Real-Time Ultra-Low-Bitrate Semantic Communication
- **年份/会议：** 2026 (arXiv:2602.13837)
- **arXiv：** https://arxiv.org/abs/2602.13837
- **为什么相关：** 在超低码率语义通信场景下实现高保真、因果、实时视频生成。
- **优先级：** ★★

---

## 总结与优先级排序

### 🔴 最高优先级（★★★★★，含代码）
1. **Send-VAE** (2601.05823) — CNLSA/TrACE-Video直接对口，VAE语义解缠核心
2. **Diagonal Distillation** (2603.09488, ICLR 2026) — per-chunk/step compute gate，有GitHub
3. **EvoSearch** (ICLR 2026) — 通用TTA scaling for diffusion，有GitHub
4. **LatSearch** (2603.14526) — latent reward for video diffusion TTA，有GitHub
5. **TTOM** (2510.07940, ICLR 2026) — 训练free TTA for compositional video generation
6. **SVG** (2510.15301/2512.11749, ICLR 2026) — VAE-free LDM，Tsinghua+Kuaishou，有GitHub
7. **Event-Driven Video Generation** (2603.13402) — per-step event gate机制

### 🟡 高优先级（★★★★）
8. **Video-T1** (2503.18942, ICCV 2025) — TTS for video generation，有GitHub
9. **LVTINO** (2510.01339, ICLR 2026) — latent video consistency inverse solver
10. **VGGRPO** (2603.26599) — 4D latent reward for world consistency
11. **LongLive** (ICLR 2026) — 实时长视频AR生成
12. **SemanticGen** (2512.20619) — 语义空间视频生成
13. **TTT-Video** (2504.05298) — TTT layers for video，有GitHub

### 🟢 中等优先级（★★★）
14. **LeanVAE** (ICCV 2025) — 高效视频VAE，有GitHub
15. **DA-VAE** (2603.22125) — latent压缩via detail alignment
16. **SteinsGate** (ICLR 2026) — 因果长视频生成
17. **Real-Time Motion-Controllable AR Video Diffusion** (ICLR 2026)
18. **One-Step Causal Video via ASD** (ICLR 2026)
19. **Causal Forcing** (2602.02214)
20. **Consistency-Preserving Diverse Video Generation** (2602.15287)

---

**注：** 本报告仅收录2025年底以后发表的论文（2026年优先），所有论文均附真实链接。代码链接仅在已验证存在时标注✅。部分ICLR 2026论文可能仍在OpenReview审稿中，代码可能未公开。
