# HetLoRA: Heterogeneous LoRA for Federated Fine-tuning of On-Device Foundation Models

**Paper:** [arXiv 2401.06432](https://arxiv.org/abs/2401.06432)  
**Venue:** EMNLP 2024  
**Year:** 2024  
**Tags:** federated LoRA, system heterogeneity, rank heterogeneity, on-device, data heterogeneity

---

## Problem

On-device federated fine-tuning must handle **dual heterogeneity**:
1. **System heterogeneity:** Clients have vastly different compute/memory budgets (e.g., mobile phones vs. edge servers), making a uniform LoRA rank impractical.
2. **Data heterogeneity:** Clients' local data distributions differ significantly, calling for personalized adaptation.

Existing federated LoRA methods either fix a common rank (wasting resources on capable clients or exceeding limits on constrained ones) or fail to leverage rank diversity during aggregation.

## Key Idea

HetLoRA allows each client to use a **different LoRA rank** suited to its local resource budget. Two mechanisms make heterogeneous ranks compatible across clients:
- **Rank Self-Pruning:** Low-resource clients prune their local LoRA to a smaller rank before uploading, minimizing communication while maintaining quality.
- **Sparsity-Weighted Aggregation:** The server aggregates LoRA matrices from different-rank clients using weights inversely proportional to sparsity (i.e., higher-rank contributions weighted more, reflecting more information content).

An additional **data-aware** dimension lets the aggregation account for client data distributions, bridging system and data heterogeneity simultaneously.

## Method

1. Each client selects a local LoRA rank based on its compute budget.
2. During upload, low-rank clients optionally apply rank pruning to match a target upload rank.
3. Server performs sparsity-weighted aggregation, combining adapters of different effective ranks.
4. Aggregated adapter is redistributed; clients re-expand or truncate to their local rank.

## Results

- Validated on large-scale NLP tasks across clients with heterogeneous resource profiles.
- Outperforms fixed-rank federated LoRA in both personalization quality and resource utilization.
- Sparsity-weighted aggregation better utilizes contributions from high-rank (resource-rich) clients.

## Strengths

- Directly addresses the practical constraint of mixed-capability edge devices.
- Rank self-pruning keeps communication costs proportional to client capability.
- Data-aware aggregation addresses both heterogeneity axes simultaneously.

## Limitations

- Sparsity-weighted aggregation requires clients to report their rank, which may be a privacy concern in some settings.
- Rank re-expansion after aggregation may introduce approximation errors for low-rank clients.

## Relevance to Personalized FL

HetLoRA is particularly relevant to **real-world deployment** scenarios where device capability differences are as challenging as data differences. Its heterogeneous rank design is a natural form of system-level personalization in federated fine-tuning.

---

**Citation:**  
> Heterogeneous LoRA for Federated Fine-tuning of On-Device Foundation Models. arXiv:2401.06432, EMNLP 2024.
