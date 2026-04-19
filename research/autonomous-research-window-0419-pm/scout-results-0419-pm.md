# Scout Results — 0419 PM CNLSA/TrACE-Video 60天复查

**Scout 任务执行时间：** 2026-04-19 20:06 CST
**搜索范围：** cs.CV/cs.LG/cs.AI，Apr 13–19 2026 新提交 + Re2Pix相关 + test-time adaptation + VAE-free
**策略：** 重点找 0419-AM 扫描之后真正新增的高价值论文

---

## 核心结论

### **0419-AM 已全覆盖，无真正新增**

经逐篇核实 Apr 13–19 新提交，**无任何一篇属于对 CNLSA/TrACE-Video 有实质新增价值的工作**。具体说明如下。

---

## Apr 13–19 新提交逐篇核实

### Apr 16 — Seen-to-Scene (2604.14648)
- **论文：** [arXiv:2604.14648](https://arxiv.org/abs/2604.14648) | CVPR 2026 Findings
- **代码：** 无代码（project page: 无公开项目页）
- **方向：** Video Outpainting（空间扩展，而非语义漂移）
- **Relevance：** 提出了 temporal coherence + flow completion 联合方法，与 CNLSA 的时序一致性概念有方法论共鸣，但应用场景（outpainting）非 TrACE-Video 目标
- **判断：** 间接相关，非直接竞争/引用工作；视频outpainting不等同于视频生成语义漂移

### Apr 16–19 其他新提交（核实后均非CNLSA相关）
| arXiv ID | 方向 | Relevance | 判断 |
|----------|------|-----------|------|
| 2604.14816 | NTIRE 2026 Video Saliency Prediction workshop | 视频显著预测，非生成 | ❌ |
| 2604.14648 | Seen-to-Scene（video outpainting，上方已述） | 间接 | ⚠️ 非核心 |
| — | 16–19日期间未发现其他视频生成/DINOv3/test-time相关新提交 | — | — |

---

## Re2Pix (2604.11707, Apr 13) 相关工作核实

Re2Pix 是本轮最重要的新论文，0419-AM 已完整覆盖。PM 轮额外核实：

- **Related Work 搜索结果：** 未在 Apr 13–19 窗口内发现引用 Re2Pix 或基于其框架的 follow-up 工作
- **方法论关联：** Re2Pix 的 VFM semantic feature → pixels 两阶段范式，在方法上与 SVG（DINOv3 替代VAE）和 SFD（semantic VAE）形成呼应，三者共同指向 semantic latent space 是视频生成的关键方向
- **结论：** Re2Pix 目前是独立工作，Apr 19前无明确follow-up

---

## Test-Time Adaptation 方向复查

| 论文 | arXiv | 日期 | 代码 | Relevance |
|------|-------|------|------|-----------|
| TTA-Vid | 2604.00696 | Apr 1 | ❌ | 视频推理任务TTA，非视频生成；方法为test-time RL，与TTOM/CNLSA方向不同 |
| Video-T1 | 2503.18942 | Mar 2025 | [✅ Project](https://liuff19.github.io/Video-T1) | test-time scaling（搜索树/ToF），非test-time adaptation；相关但非新增 |
| Uni-ViGU | 2604.08121 | Apr 9 | [✅ Code](https://fr0zencrane.github.io/uni-vigu-page/) | 生成+理解统一，diffusion-based video generator为核心；非CNLSA直接相关 |
| TTOM | 2510.07940 | ICLR 2026 | ❌ | test-time latent optimization，**直接相关**；0419-AM已覆盖 |

**结论：** Test-time adaptation for video generation 方向的核心工作仍是 TTOM（无代码）和 Video-T1（Mar 2025），Apr 13–19 无新增。

---

## VAE-Free / DINOv3 方向复查

| 论文 | arXiv | 会议 | 代码 | 状态 |
|------|-------|------|------|------|
| SVG | 2510.15301 | ICLR 2026 | [✅ GitHub](https://github.com/shiml20/SVG) | v4，0419-AM已确认 |
| SFD | 2512.04926 | CVPR 2026 | [✅ GitHub](https://github.com/yuemingPAN/SFD) | 0419-AM已确认代码公开 |
| SemanticGen | 2512.20619 | — | [✅ Project](https://jianhongbai.github.io/SemanticGen/) | semantic space两阶段生成，Dec 2025；0419-AM已提及 |
| Feature Space Conditioning | 2604.01761 | Apr 2 | [✅ Project](https://dedoardo.github.io/projects/control-dino/) | DINO feature conditioning for i2v，Apr 2；非新窗口 |

**结论：** VAE-free / DINOv3 video generation 的最新实现仍是 SVG 和 SFD，Apr 13–19 无新竞争工作。

---

## Workshop Paper 新 Baseline 核实

经搜索 Apr 13–19 新提交中未发现任何面向 workshop paper 的新 baseline 论文（所谓"workshop paper relevant baselines"是指可能被 workshop paper 引用的新评测基准或对比方法）。

---

## 最终结论

| 类别 | 0419-AM 是否已覆盖 | 0419-PM 新增 |
|------|-------------------|-------------|
| Re2Pix (2604.11707) | ✅ 完整覆盖 | ❌ 无新增 |
| SVG / SFD / LVTINO / TTOM / Send-VAE | ✅ 60天rescan完成 | ❌ 无新版本 |
| Test-time adaptation for video gen | ✅ TTOM已覆盖 | ❌ 无真正新工作 |
| VAE-free / DINOv3 video gen | ✅ SVG/SFD已覆盖 | ❌ 无新竞争 |
| Apr 13–19 新增论文 | 全面检查 | ⚠️ 仅 Seen-to-Scene 属新窗口，但相关性低 |

**综合判断：0419-AM 已全覆盖，本轮 PM 复查无真正新增高价值论文。**

---

## 补充：Seen-to-Scene (2604.14648) 若 workshops 需要可引用

虽然非直接相关，但 Seen-to-Scene（CVPR 2026 Findings）提出了一种视频时序一致性保证方法（flow completion + reference-guided latent propagation），与其被接受为 CVPR 2026 Findings 有关注度。如果 TrACE-Video workshop paper 需要引用"视频时序一致性"的方法作为对比，Seen-to-Scene 可以作为一个评测对象。

**引用格式参考：**
> Jeon et al., "Seen-to-Scene: Keep the Seen, Generate the Unseen for Video Outpainting," CVPR 2026 Findings. [arXiv:2604.14648](https://arxiv.org/abs/2604.14648)

---

*Scout 0419-PM | 模型：MiniMax-M2.7 | 搜索：Tavily + arxiv.org 逐篇核实日期*
