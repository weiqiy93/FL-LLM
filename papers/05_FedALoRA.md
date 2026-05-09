# FedALoRA: Adaptive Local LoRA Aggregation for Personalized Federated Learning in LLM

**Paper:** [IEEE Xplore](https://ieeexplore.ieee.org/document/11048575) | [Springer](https://link.springer.com/chapter/10.1007/978-981-96-8731-2_9)  
**Venue:** WASA 2025 (Wireless Artificial Intelligent Computing Systems and Applications)  
**Year:** 2025  
**Tags:** personalized FL, LoRA, non-IID, adaptive aggregation

---

## Problem

Federated LLM fine-tuning (FedLLM) is challenged by the **non-IID problem**: clients have heterogeneous local data distributions (cross-domain or cross-task), making a single globally aggregated model a poor fit for any individual client. Standard FedAvg-based LoRA aggregation blends all client adapters uniformly, ignoring local distribution differences.

## Key Idea

FedALoRA combines **personalized model aggregation** with **LoRA-based fine-tuning**. Rather than uniformly averaging all clients' LoRA adapters, the server adaptively aggregates a personalized global model for each client by weighting contributions based on client similarity. The resulting personalized global model initializes local LoRA training, so each client learns general knowledge from similar peers while retaining its own domain expertise.

## Method

- **Similarity-based Weighting:** Before each round, the server estimates pairwise client similarity (e.g., via gradient cosine similarity or data distribution proxies).
- **Adaptive Aggregation:** Each client receives a customized global LoRA adapter weighted more toward similar clients and less toward dissimilar ones.
- **Local LoRA Training:** Clients fine-tune their LLM using the personalized global LoRA as initialization, then upload updated adapters.
- Keeps training costs low by operating entirely within LoRA parameter space.

## Results

- Extensive experiments on cross-domain non-IID settings demonstrate FedALoRA outperforms standard FedAvg + LoRA and other personalized FL baselines.
- Better accuracy on local client tasks while maintaining knowledge of general capabilities.
- Practical for edge deployment due to LoRA's low parameter footprint.

## Strengths

- Personalization is achieved at the aggregation level — no structural changes to the model.
- Simple to implement on top of existing federated LoRA pipelines.
- Adaptive aggregation naturally handles varying degrees of client heterogeneity.

## Limitations

- Estimating client similarity requires either sharing some gradient information or a proxy, which may have privacy implications.
- The benefit diminishes if clients are highly heterogeneous and no natural clusters exist.

## Relevance to Personalized FL

FedALoRA implements **aggregation-level personalization**: each client's starting point for local training is already customized based on its peer neighborhood, making it directly relevant to personalized federated fine-tuning with non-IID data.

---

**Citation:**  
> Yi, X., Hu, C., Cai, B. FedALoRA: Adaptive Local LoRA Aggregation for Personalized Federated Learning in LLM. WASA 2025.
