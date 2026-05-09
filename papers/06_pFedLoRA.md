# pFedLoRA: Model-Heterogeneous Personalized Federated Learning with LoRA Tuning

**Paper:** [arXiv 2310.13283](https://arxiv.org/abs/2310.13283)  
**Venue:** Preprint (2023)  
**Year:** 2023  
**Tags:** personalized FL, model heterogeneity, LoRA, adapter, communication efficiency

---

## Problem

Real-world federated learning must handle **model heterogeneity**: clients have different hardware capabilities and may need to run different-sized local models (e.g., a small device running a 1B model, a server running a 7B model). Existing personalized FL methods assume all clients use the same model architecture, making them inapplicable to this setting.

## Key Idea

pFedLoRA introduces a **homogeneous small adapter** that bridges heterogeneous client models. Each client trains a large local model (of its own chosen size) but attaches a small, shared LoRA adapter of identical shape across all clients. The global exchange happens only via these small adapters, allowing the server to aggregate across architecturally diverse clients. An **iterative training procedure** alternates between local model updates and adapter updates to facilitate global-local knowledge exchange.

## Method

- Each client has its own (potentially different-sized) local model.
- A small, architecture-agnostic LoRA adapter is appended to every client's model at designated layers.
- Local training alternates: (1) update the local model with frozen adapter, (2) update the adapter with frozen local model.
- Only the small adapter is sent to the server for aggregation via FedAvg.
- The aggregated global adapter is returned to clients and used to transfer global knowledge into local models via the iterative update.

## Results

- Outperforms 6 state-of-the-art baselines by up to 1.35% in test accuracy.
- Achieves **11.81× reduction** in computation overhead.
- Achieves **7.41× reduction** in communication cost.
- Convergence is theoretically proven.

## Strengths

- First to address model-heterogeneous personalized FL with LoRA adapters.
- Adapter-only communication dramatically reduces bandwidth requirements.
- Theoretical convergence guarantees strengthen practical credibility.

## Limitations

- The homogeneous small adapter may be a bottleneck for very large local models if its capacity is insufficient.
- Iterative training (frozen alternation) may slow convergence compared to joint optimization.

## Relevance to Personalized FL

pFedLoRA tackles a rarely addressed dimension of personalized FL: **system heterogeneity**. By allowing clients with different model sizes to participate equally, it broadens the scope of personalized federated fine-tuning to truly heterogeneous deployments.

---

**Citation:**  
> pFedLoRA: Model-Heterogeneous Personalized Federated Learning with LoRA Tuning. arXiv:2310.13283, 2023.
