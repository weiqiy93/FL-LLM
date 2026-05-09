# FDLoRA: Personalized Federated Learning of Large Language Model via Dual LoRA Tuning

**Paper:** [arXiv 2406.07925](https://arxiv.org/abs/2406.07925)  
**Venue:** Preprint  
**Year:** June 2024  
**Tags:** personalized FL, dual LoRA, global knowledge, local knowledge, adaptive fusion

---

## Problem

Federated fine-tuning of LLMs faces a fundamental tension: clients need to incorporate **global knowledge** (from other clients' data) without losing their own **local specialization**. Single-adapter approaches force a trade-off — high aggregation weight improves global knowledge but dilutes local adaptation, while low aggregation weight preserves local knowledge but wastes collaborative potential.

## Key Idea

FDLoRA sidesteps this trade-off by assigning **two dedicated LoRA modules per client**:
- A **global LoRA** that participates in federated aggregation to capture cross-client knowledge.
- A **personal LoRA** that stays local and captures client-specific patterns.

An **adaptive fusion** mechanism combines the outputs of both LoRAs during inference, with fusion weights learned to balance global vs. local contributions.

## Method

- **Dual LoRA setup:** Each client attaches two independent LoRA adapters to the base LLM at the same target layers.
- **Training:** Both LoRAs are updated locally during each round.
- **Communication:** Only the global LoRA is uploaded to the server; personal LoRA never leaves the client.
- **Server aggregation:** FedAvg on global LoRAs produces an updated global adapter, returned to clients.
- **Adaptive fusion:** A learnable scalar or vector blends global and personal LoRA outputs; learned via local training.
- Supports both single-device clients and clustered multi-device clients.

## Results

- Outperforms 6 baselines across performance, stability, robustness, computation cost, and communication cost.
- Adaptive fusion weights converge to meaningful values that reflect each client's data distribution shift.
- Robust to highly heterogeneous (non-IID) settings where single-adapter methods degrade significantly.

## Strengths

- Explicit separation of global and personal knowledge eliminates the tension between collaboration and personalization.
- Adaptive fusion is lightweight (few extra parameters) and learned end-to-end.
- Flexible client topology: works for both individual devices and device clusters.

## Limitations

- Maintaining two LoRAs doubles the local adapter memory relative to single-LoRA approaches.
- Fusion weights must be learned per client; may need a warm-up period to converge.

## Relevance to Personalized FL

FDLoRA is one of the most direct approaches to personalized federated fine-tuning: it **architecturally separates** the two goals (global generalization and local personalization) rather than trying to achieve both with a single adapter, making the personalization mechanism explicit and interpretable.

---

**Citation:**  
> Qi, J., et al. FDLoRA: Personalized Federated Learning of Large Language Model via Dual LoRA Tuning. arXiv:2406.07925, June 2024.
