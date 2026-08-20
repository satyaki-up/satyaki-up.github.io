---
layout: post
title:  "Rundown: Scaling laws"
---

Scaling laws are an empirical way to predict the performance of big models by running experiments on small models, useful because big models are expensive. They fit curve between the model loss and the cost of the model (in terms of total parameters or amount of training data or GPU compute cost). It's generally an inverse power law, with the loss proportional to the inverse of ``N``/``D``/``C`` raised to an exponent.  

The most common ones are the Kaplan and Chinchilla laws, with the latter more recent and accurate - it mentions scaling both the model size and data in an equal ratio, and ``D = 20N`` as the total data required for a model with ``N`` parameters in an infinite-data regime (1 epoch over the dataset). This is now out-of-date, with models being trained with even ``D = 500N`` ratios. Though these laws are new, fitting a curve between model performance and data size is not - classical statistical learning had the VC dimension and Rademacher complexity. One tricky bit is how to transfer hyperparameters from the small-scale experiments to the larger scale runs. There're frameworks like ``muP`` but no clean solution as of now. These laws were also only for pretraining. They didn't include inference - for example, a smaller model is cheaper for inference and we might want to trade off longer pretraining cost in exchange for cheaper inference. Architecture might also play a role - unlike the dense transformers with full attention, nowadays models are MoEs with sparse attention variants. Another potential confounder is test-time compute. Now that model performance is rarely one-shot and often becomes better as we pay a larger compute cost and just let it run, the clean loss metric against which scaling laws are fit, does not apply. Ever since reinforcement learning became common, that has its own set of (undiscovered) scaling laws - unlike pretraining, it deals with very little data and makes up for it via long compute trajectories.

#### References

* [2026] [Small-Scale Experiments: Are We There Yet?](https://arxiv.org/abs/2608.11859)  
* [2026] [Scaling Laws, Carefully](https://lilianweng.github.io/posts/2026-06-24-scaling-laws/)  
* [2026] [Prescriptive Scaling Laws for Data Constrained Training](https://arxiv.org/abs/2605.01640)  
* [2025] [The Art of Scaling Reinforcement Learning Compute for LLMs](https://arxiv.org/abs/2510.13786)  
* [2024] [Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters](https://arxiv.org/abs/2408.03314)  
* [2024] [Reconciling Kaplan and Chinchilla Scaling Laws](https://arxiv.org/abs/2406.12907)  
* [2024] [Chinchilla Scaling: A replication attempt](https://arxiv.org/abs/2404.10102)  
* [2024] [Neural Scaling Laws Rooted in the Data Distribution](https://arxiv.org/abs/2412.07942)  
* [2023] [Beyond Chinchilla-Optimal: Accounting for Inference in Language Model Scaling Laws](https://arxiv.org/abs/2401.00448)  
* [2023] [Scaling Data-Constrained Language Models](https://arxiv.org/abs/2305.16264)  
* [2022] [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556)  
* [2022] [Unified Scaling Laws for Routed Language Models](https://arxiv.org/abs/2202.01169)  
* [2022] [Scaling Laws and Interpretability of Learning from Repeated Data](https://arxiv.org/abs/2205.10487)  
* [2021] [Explaining Neural Scaling Laws](https://arxiv.org/abs/2102.06701)  
* [2021] [Scale Efficiently: Insights from Pre-training and Fine-tuning Transformers](https://arxiv.org/abs/2109.10686)  
* [2021] [Scaling Laws for Transfer](https://arxiv.org/abs/2102.01293)  
* [2020] [Scaling Laws for Autoregressive Generative Modeling](https://arxiv.org/abs/2010.14701)  
* [2020] [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361)  
* [2019] [A Constructive Prediction of the Generalization Error Across Scales](https://arxiv.org/abs/1909.12673)  
* [2017] [Deep Learning Scaling is Predictable, Empirically](https://arxiv.org/abs/1712.00409)

