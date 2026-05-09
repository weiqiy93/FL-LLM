# PF2LoRA: Personalized Federated Fine-tuning via Automatic Rank Learning with Two-Level LoRA

**Paper:** [arXiv 2503.03920](https://arxiv.org/abs/2503.03920)  
**Venue:** OpenReview (under review)  
**Year:** March 2025  
**Tags:** personalized FL, LoRA, rank learning, data heterogeneity

---

## Problem

Existing federated LoRA methods fix the LoRA rank as a hyperparameter shared across all clients. A single predefined rank is agnostic to the actual data heterogeneity: clients with complex distributions may need higher rank while simpler clients waste computation on unnecessary parameters. This one-size-fits-all design limits personalization quality.

## Key Idea

PF2LoRA decomposes LoRA adaptation into **two levels**:
1. **Level 1 (Global Adapter):** A shared LoRA adapter learned collaboratively across all clients — captures common cross-client knowledge.
2. **Level 2 (Personal Adapter):** A small client-specific adapter that personalizes based on local data.

Crucially, the rank of each client's personal adapter is **automatically learned** from data rather than manually specified, enabling adaptive personalization.

## Method

- Each client trains two stacked LoRA adapters: one shared (aggregated globally) and one private (kept local).
- A rank learning mechanism prunes or expands the personal adapter's rank based on local gradient signals.
- Only Level 1 adapter parameters are uploaded to the server for aggregation; Level 2 stays on-device.
- Minimal additional memory: Level 2 adapters have far fewer parameters than Level 1 by design.

## Results

- Outperforms existing federated fine-tuning methods on natural language understanding (GLUE) and generation tasks.
- Automatic rank selection consistently identifies appropriate ranks per client without manual tuning.
- Achieves better personalization with less communication than methods using full-rank local adapters.

## Strengths

- No need to manually tune LoRA rank for each client — rank adapts to data heterogeneity automatically.
- Two-level design elegantly separates global knowledge from personal knowledge.
- Minimal overhead: personal adapter is much smaller than the global one.

## Limitations

- Rank learning mechanism may require careful regularization to prevent collapse (rank → 0) or explosion.
- Two-level structure increases training complexity slightly compared to single-LoRA baselines.

## Relevance to Personalized FL

PF2LoRA directly addresses **parameter-level personalization**: the adaptation capacity itself (LoRA rank) is tailored per client, not just the weights. This is a more fine-grained form of personalization than fixed-architecture approaches.

---

**Citation:**  
> Personalized Federated Fine-tuning for Heterogeneous Data: An Automatic Rank Learning Approach via Two-Level LoRA. arXiv:2503.03920, March 2025.
