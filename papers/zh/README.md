# 联邦 LLM 微调论文摘要（中文版）

研究重点：大语言模型的**个性化联邦微调**，主要关注基于 LoRA 的方法。

---

## 论文索引

| 编号 | 论文 | 发表于 | 年份 | 个性化策略 |
|------|------|--------|------|------------|
| 01 | [FedAMoLE](01_FedAMoLE.md) | ACM Web Conf. 2026 | 2024 | 异构 MoE-LoRA 架构，按数据分布分配专家 |
| 02 | [PF2LoRA](02_PF2LoRA.md) | 预印本 | 2025 | 双层 LoRA + 自动秩学习 |
| 03 | [FedALT](03_FedALT.md) | 预印本 | 2025 | 独立 LoRA + 世界其余 LoRA + 自适应混合器 |
| 04 | [LoRA-FAIR](04_LoRA-FAIR.md) | ICCV 2025 | 2024 | 修正聚合偏差 + 初始化漂移 |
| 05 | [FedALoRA](05_FedALoRA.md) | WASA 2025 | 2025 | 基于客户端相似度的自适应加权聚合 |
| 06 | [pFedLoRA](06_pFedLoRA.md) | 预印本 | 2023 | 同构小适配器适配模型异构客户端 |
| 07 | [FDLoRA](07_FDLoRA.md) | 预印本 | 2024 | 双 LoRA（全局聚合 + 个人本地）+ 自适应融合 |
| 08 | [FedSA-LoRA](08_FedSA-LoRA.md) | ICLR 2025 | 2024 | 仅聚合 A 矩阵（通用），B 矩阵留本地（个性化） |
| 09 | [HetLoRA](09_HetLoRA.md) | EMNLP 2024 | 2024 | 各客户端异构 LoRA 秩 + 稀疏度加权聚合 |
| 10 | [FLoRA](10_FLoRA.md) | NeurIPS 2024 | 2024 | 堆叠式无噪声 LoRA 聚合 |

---

## 个性化策略分类

### 架构层面个性化
- **FedAMoLE：** 每个客户端根据其数据分布获得不同数量的 LoRA 专家，实现架构级差异化。
- **pFedLoRA：** 客户端运行不同规模的本地模型，仅共享一个小型适配器进行聚合。

### 适配器拆分个性化（全局 + 本地 LoRA）
- **FDLoRA：** 明确的双 LoRA——全局 LoRA 参与聚合，个人 LoRA 保留本地。
- **FedSA-LoRA：** 非对称聚合——A 矩阵（通用表示）上传聚合，B 矩阵（特定变换）留本地。
- **FedALT：** 独立 LoRA + RoW LoRA，通过可学习的自适应混合器按 token 级别动态融合。

### 秩自适应个性化
- **PF2LoRA：** 通过双层分解自动学习每个客户端的 LoRA 秩。
- **HetLoRA：** 允许各客户端使用不同 LoRA 秩，面向系统异构性。

### 聚合层面个性化
- **FedALoRA：** 按相似度加权聚合，为每个客户端生成个性化的全局模型。
- **LoRA-FAIR：** 修正聚合偏差与初始化漂移，提升全局模型向本地迁移的质量。

### 聚合正确性（使个性化的基础更扎实）
- **FLoRA：** 堆叠式无噪声 LoRA 聚合——修复 FedAvg + LoRA 中的数学错误。

---

## 核心研究主题

1. **LoRA 是主流方法：** 近期几乎所有联邦 LLM 微调工作都以 LoRA 或其变体作为 PEFT 骨干。
2. **数据异构性是核心挑战：** 客户端间的非独立同分布数据分布驱动了绝大多数个性化设计。
3. **聚合数学的正确性至关重要：** FLoRA 和 LoRA-FAIR 表明，朴素的 FedAvg 直接作用于 LoRA 矩阵会引入数学误差——正确的聚合是一切的基础。
4. **双组件设计是主流趋势：** 将全局适配器与个人适配器分离（FDLoRA、FedSA-LoRA、FedALT）是一种反复出现且有效的设计模式。
5. **系统异构性仍待深入探索：** HetLoRA 和 pFedLoRA 是为数不多专门解决设备能力差异问题的工作。

---

## 论文链接

- [arXiv 2411.19128](https://arxiv.org/abs/2411.19128) — FedAMoLE
- [arXiv 2503.03920](https://arxiv.org/abs/2503.03920) — PF2LoRA
- [arXiv 2503.11880](https://arxiv.org/abs/2503.11880) — FedALT
- [arXiv 2411.14961](https://arxiv.org/abs/2411.14961) — LoRA-FAIR
- [IEEE Xplore FedALoRA](https://ieeexplore.ieee.org/document/11048575) — FedALoRA
- [arXiv 2310.13283](https://arxiv.org/abs/2310.13283) — pFedLoRA
- [arXiv 2406.07925](https://arxiv.org/abs/2406.07925) — FDLoRA
- [arXiv 2410.01463](https://arxiv.org/abs/2410.01463) — FedSA-LoRA（ICLR 2025）
- [arXiv 2401.06432](https://arxiv.org/abs/2401.06432) — HetLoRA（EMNLP 2024）
- [arXiv 2409.05976](https://arxiv.org/abs/2409.05976) — FLoRA（NeurIPS 2024）
