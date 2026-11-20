---
layout: post
title:  "Diagnostics for loss spikes"
---


* [2026] [Stanford's Deep Learning Alchemy](https://deep-learning-alchemy.github.io/): Most of the course is about training stability, and how to transfer hyperparams (LR, batch size) across scale.  
* [2025] [Marin 32B](https://marin.community/blog/2025/10/28/marin-32b-retro/): [Loss spike](https://github.com/marin-community/marin/issues/1368) mitigated by QK-norm. 8B was stable without it. [Tweet](https://x.com/dlwh/status/1938282075326710146).  
* [2024] [2 Olmo 2 Furious](https://arxiv.org/abs/2501.00656): QK-norm (section 3.3.2). Normalize the key and query projections with RMSNorm before calculating attention. This avoids attention logits being too large.  
* [2024] [DBRX](https://www.databricks.com/blog/introducing-dbrx-new-state-art-open-llm): QKV clipping ([tweet](https://x.com/zeuxcg/status/1780765558558097440)).  
* [2023] [Scaling Vision Transformers to 22B](https://arxiv.org/abs/2302.05442): 8B diverged due to huge attention logits. Fixed by QK-norm (LayerNorm), parallel layers and no biases. LR decreased with scale.  
* [2023] [Spike No More](https://arxiv.org/abs/2312.16903): 1.5B. Init weights to small values and scale embedding by sqrt(d) or add LayerNorm to embedding layer to reduce variance.  
* [2021] [Cogview](https://arxiv.org/abs/2105.13290): Gradients of embeddings higher than other layers, so scale it by 0.1 and detach (1-0.1). Sandwich-LN.  
