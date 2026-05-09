# Federated Fine-Tuning of LLMs — Paper Summaries


Focus: **Personalized Federated Fine-Tuning** of Large Language Models, primarily LoRA-based methods.

---

## Paper Index

| # | Paper | Venue | Year | Personalization Strategy |
|---|-------|-------|------|--------------------------|
| 01 | [FedAMoLE](01_FedAMoLE.md) | ACM Web Conf. 2026 | 2024 | Heterogeneous MoE-LoRA architecture per client |
| 02 | [PF2LoRA](02_PF2LoRA.md) | Preprint | 2025 | Automatic per-client rank learning (two-level LoRA) |
| 03 | [FedALT](03_FedALT.md) | Preprint | 2025 | Individual LoRA + Rest-of-World LoRA with adaptive mixer |
| 04 | [LoRA-FAIR](04_LoRA-FAIR.md) | ICCV 2025 | 2024 | Aggregation bias correction + initialization refinement |
| 05 | [FedALoRA](05_FedALoRA.md) | WASA 2025 | 2025 | Similarity-based adaptive global LoRA aggregation |
| 06 | [pFedLoRA](06_pFedLoRA.md) | Preprint | 2023 | Homogeneous small adapter for model-heterogeneous clients |
| 07 | [FDLoRA](07_FDLoRA.md) | Preprint | 2024 | Dual LoRA (global + personal) with adaptive fusion |
| 08 | [FedSA-LoRA](08_FedSA-LoRA.md) | ICLR 2025 | 2024 | Selective A-matrix aggregation; B-matrix stays local |
| 09 | [HetLoRA](09_HetLoRA.md) | EMNLP 2024 | 2024 | Heterogeneous ranks + sparsity-weighted aggregation |
| 10 | [FLoRA](10_FLoRA.md) | NeurIPS 2024 | 2024 | Stacking-based noise-free aggregation |

---

## Taxonomy of Personalization Strategies

### Architecture-level Personalization
- **FedAMoLE:** Each client gets a different number of LoRA experts based on its data distribution.
- **pFedLoRA:** Clients run different-sized local models; only a small shared adapter is aggregated.

### Adapter-split Personalization (Global + Local LoRA)
- **FDLoRA:** Explicit dual LoRA — one for global knowledge (aggregated), one for personal knowledge (local).
- **FedSA-LoRA:** Asymmetric aggregation — A matrices (general) aggregated, B matrices (specific) kept local.
- **FedALT:** Individual LoRA + Rest-of-World LoRA blended via a learned adaptive mixer.

### Rank-adaptive Personalization
- **PF2LoRA:** Automatically learns per-client LoRA rank via two-level decomposition.
- **HetLoRA:** Allows heterogeneous LoRA ranks across clients for system-heterogeneity-aware adaptation.

### Aggregation-level Personalization
- **FedALoRA:** Personalized global model per client via similarity-weighted aggregation.
- **LoRA-FAIR:** Corrects aggregation bias and initialization drift for better global-to-local transfer.

### Aggregation Correctness (Enabling Better Personalization)
- **FLoRA:** Stacking-based noise-free LoRA aggregation — fixes the mathematical error in FedAvg + LoRA.

---

## Key Themes

1. **LoRA dominates:** Nearly all recent federated LLM fine-tuning methods use LoRA or its variants as the PEFT backbone.
2. **Data heterogeneity is the core challenge:** Non-IID data across clients drives most personalization designs.
3. **Aggregation math matters:** FLoRA and LoRA-FAIR show that naive FedAvg on LoRA matrices introduces errors — correct aggregation is foundational.
4. **Dual-component designs are popular:** Separating global and personal adapters (FDLoRA, FedSA-LoRA, FedALT) is a recurring and effective pattern.
5. **System heterogeneity is underexplored:** HetLoRA and pFedLoRA are among the few addressing device capability differences.

---

## Sources

- [arXiv 2411.19128](https://arxiv.org/abs/2411.19128) — FedAMoLE
- [arXiv 2503.03920](https://arxiv.org/abs/2503.03920) — PF2LoRA
- [arXiv 2503.11880](https://arxiv.org/abs/2503.11880) — FedALT
- [arXiv 2411.14961](https://arxiv.org/abs/2411.14961) — LoRA-FAIR
- [IEEE Xplore FedALoRA](https://ieeexplore.ieee.org/document/11048575) — FedALoRA
- [arXiv 2310.13283](https://arxiv.org/abs/2310.13283) — pFedLoRA
- [arXiv 2406.07925](https://arxiv.org/abs/2406.07925) — FDLoRA
- [arXiv 2410.01463](https://arxiv.org/abs/2410.01463) — FedSA-LoRA (ICLR 2025)
- [arXiv 2401.06432](https://arxiv.org/abs/2401.06432) — HetLoRA (EMNLP 2024)
- [arXiv 2409.05976](https://arxiv.org/abs/2409.05976) — FLoRA (NeurIPS 2024)
