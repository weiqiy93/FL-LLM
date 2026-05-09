# FedSA-LoRA: Selective Aggregation for Low-Rank Adaptation in Federated Learning

**Paper:** [arXiv 2410.01463](https://arxiv.org/abs/2410.01463)  
**Venue:** ICLR 2025  
**Year:** 2024 (preprint), 2025 (published)  
**Code:** [GitHub](https://github.com/Pengxin-Guo/FedSA-LoRA)  
**Tags:** federated LoRA, asymmetric aggregation, personalization, communication efficiency

---

## Problem

In standard federated LoRA, both the A and B matrices are aggregated at the server. This ignores a fundamental asymmetry in what these matrices learn: treating them identically during aggregation conflates globally shared structure with locally specific patterns, degrading both global generalization and local personalization.

## Key Idea

FedSA-LoRA is built on an **asymmetry analysis** of LoRA matrices in the federated setting:
- **A matrices** learn **general, cross-client knowledge** — they capture universal input representations shared across different data distributions.
- **B matrices** learn **client-specific knowledge** — they encode output transformations tailored to local data.

Therefore, only **A matrices should be shared** with the server for aggregation, while **B matrices remain local** as the personalization component.

## Method

- Each client trains both A and B matrices locally each round.
- Only A matrices are uploaded to the server.
- Server aggregates A matrices via FedAvg; B matrices stay on-device.
- Clients download the new global A and continue local training with their own B.
- Extended to LoRA variants: **FedSA-rsLoRA** and **FedSA-VeRA** apply the same selective aggregation principle to scaled and random-matrix LoRA variants.

## Results

- Outperforms full aggregation (both A+B) on NLU and NLG benchmarks.
- Reduces communication cost by ~50% (only A matrices uploaded).
- FedSA-rsLoRA and FedSA-VeRA confirm the asymmetry principle generalizes across LoRA variants.

## Strengths

- Theoretically motivated: asymmetry analysis provides principled justification for selective aggregation.
- Reduces communication by half with no architectural changes.
- Personalization is a natural byproduct of keeping B local — no extra mechanisms needed.
- Generalizes to multiple LoRA variants.

## Limitations

- Fixed assignment of A = global, B = local may not hold in all heterogeneity regimes.
- Personalization capacity is limited by B matrix rank; does not adaptively adjust capacity per client.

## Relevance to Personalized FL

FedSA-LoRA offers a **parameter-efficient personalization** by design: B matrices act as client-specific adapters without any additional modules, and the reduction in communication directly benefits federated systems with bandwidth constraints. It is a strong baseline for any personalized federated LoRA study.

---

**Citation:**  
> Guo, P., et al. Selective Aggregation for Low-Rank Adaptation in Federated Learning. arXiv:2410.01463, ICLR 2025.
