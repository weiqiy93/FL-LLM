# FedALT: Federated Fine-Tuning through Adaptive Local Training with Rest-of-World LoRA

**Paper:** [arXiv 2503.11880](https://arxiv.org/abs/2503.11880)  
**Venue:** Preprint (March 2025)  
**Year:** 2025  
**Tags:** personalized FL, LoRA, MoE mixer, cross-client interference

---

## Problem

Standard federated LoRA methods (e.g., FedAvg + LoRA) aggregate all client adapters into a global model and use it to reinitialize local training each round. Under data heterogeneity, this causes **cross-client interference**: the aggregated model is pulled toward the population average, harming local adaptation. Clients end up fighting the global model rather than building on it.

## Key Idea

FedALT departs from the FedAvg initialization paradigm. Each client maintains its **own individual LoRA** across rounds and incorporates global knowledge through a separate **Rest-of-World (RoW) LoRA** — an aggregated adapter representing the rest of the federation. An **adaptive mixer** (inspired by Mixture-of-Experts) dynamically weights the two adapters per input token.

## Method

- **Individual LoRA:** Client-private adapter; never reset to global state.
- **RoW LoRA:** Aggregated from other clients each round; downloaded but not used to overwrite local adapter.
- **Adaptive Mixer:** A learned, input-specific gating function that blends individual and RoW LoRA outputs for each forward pass.
- Training: both adapters and mixer are updated locally; only individual LoRA and mixer weights are shared with the server.

## Results

- Significantly outperforms FedAvg-based personalized federated LoRA methods on NLP benchmarks.
- Adaptive mixing prevents global knowledge from overriding local specialization.
- Maintains computational efficiency comparable to single-adapter baselines.

## Strengths

- Eliminates the core issue of FedAvg: no forced reinitialization from global state.
- Mixer enables dynamic, token-level personalization — adapts to distribution shifts within a single input.
- Conceptually clean separation of global and local knowledge.

## Limitations

- Mixer adds a small but non-zero parameter overhead.
- RoW LoRA still requires round-trip communication each round.
- Assumes clients can train both adapters simultaneously, which may strain memory-constrained devices.

## Relevance to Personalized FL

FedALT reframes personalization as a **dynamic knowledge mixing** problem. Rather than choosing between a global or local model, it learns when to trust global knowledge vs. local specialization on a per-input basis — a fundamentally more flexible personalization strategy.

---

**Citation:**  
> FedALT: Federated Fine-Tuning through Adaptive Local Training with Rest-of-World LoRA. arXiv:2503.11880, March 2025.
