# FedAMoLE: Personalized Federated Fine-Tuning for LLMs via Data-Driven Heterogeneous Model Architectures

**Paper:** [arXiv 2411.19128](https://arxiv.org/abs/2411.19128)  
**Venue:** ACM Web Conference 2026  
**Year:** 2024 (preprint), 2026 (published)  
**Tags:** personalized FL, LoRA, MoE, model heterogeneity

---

## Problem

Standard personalized federated fine-tuning of LLMs assumes all clients share the same model architecture. This uniform structure fails to accommodate highly heterogeneous data distributions across clients, leading to suboptimal local adaptation.

## Key Idea

FedAMoLE introduces a **data-driven heterogeneous mixture of LoRA experts** (AMoLE module) where each client receives a different number of LoRA-based domain experts based on its data distribution. The framework includes a **Reverse Selection-based Expert Assignment (RSEA)** strategy: instead of clients choosing experts, domain experts select the clients that best align with their knowledge, enabling automatic architecture adjustment during training.

## Method

- Each client hosts a heterogeneous MoE layer of LoRA adapters instead of a single LoRA.
- RSEA strategy lets domain experts identify which clients they should serve, reducing mismatched knowledge aggregation.
- Only LoRA parameters (not full model weights) are communicated, keeping per-round communication cost to ~25.66 MB (~1% of FedMoE's GB-level overhead).
- Server aggregates LoRA experts from heterogeneous architectures by matching expert domains, not client identities.

## Results

- Evaluated across 7 federated fine-tuning scenarios.
- Average improvement of **5.97%** over existing personalized FL methods.
- Reduces memory usage by nearly **50%** compared to full MoE baselines.
- Communication overhead remains practical despite model heterogeneity.

## Strengths

- Eliminates the assumption of uniform model architecture across clients.
- Data-driven architecture adjustment is automatic, requiring no manual configuration.
- Scales communication efficiency via LoRA compression.

## Limitations

- RSEA strategy adds complexity to the server's expert management.
- Performance of heterogeneous aggregation depends on having sufficiently diverse domain experts pre-defined.

## Relevance to Personalized FL

This paper is a strong example of **architecture-level personalization**: each client gets a custom model structure tailored to its local data, going beyond simple weight personalization.

---

**Citation:**  
> Personalized Federated Fine-Tuning for LLMs via Data-Driven Heterogeneous Model Architectures. arXiv:2411.19128, 2024.
