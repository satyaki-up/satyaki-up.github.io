---
layout: post
title:  "Diagnostics for loss spikes"
---


* [2026] [Stanford's Deep Learning Alchemy](https://deep-learning-alchemy.github.io/): Most of the course is about training stability, and how to transfer hyperparams (LR, batch size) across scale.  
* [2025] [Marin 32B](https://marin.community/blog/2025/10/28/marin-32b-retro/): [Loss spike](https://github.com/marin-community/marin/issues/1368) mitigated by QK-norm. 8B was stable without it. [Tweet](https://x.com/dlwh/status/1938282075326710146). WSD runs could be spikier than cosine. Adam update norm spikes precede loss spikes, but not every update norm spike leads to a loss spike. Gradient norms typically spike after update norm spikes. Skipping steps with extremely large gradient norms, does not reduce time to recovery. Update norm spikes are of higher magnitude on lower layers. When update norm spikes occur, the second-order momentum remains mostly unchanged, but the first-order momentum increases by 2×. AdamC during decay.  
* [2025] [Llama-Nemotron](https://arxiv.org/abs/2505.00949): Section 4.2. Consistently high learning rates caused training instability. Required training resumption with reinitialized optimizer states.  
* [2024] [2 Olmo 2 Furious](https://arxiv.org/abs/2501.00656): QK-norm (section 3.3.2). Normalize the key and query projections with RMSNorm before calculating attention. This avoids attention logits being too large.  
* [2024] [DBRX](https://www.databricks.com/blog/introducing-dbrx-new-state-art-open-llm): QKV clipping ([tweet](https://x.com/zeuxcg/status/1780765558558097440)).  
* [2023] [Scaling Vision Transformers to 22B](https://arxiv.org/abs/2302.05442): 8B diverged due to huge attention logits. Fixed by QK-norm (LayerNorm), parallel layers and no biases. LR decreased with scale.  
* [2023] [Spike No More](https://arxiv.org/abs/2312.16903): 1.5B. Init weights to small values and scale embedding by sqrt(d) or add LayerNorm to embedding layer to reduce variance.  
* [2022] [Megatron-Turning NLG](https://arxiv.org/abs/2201.11990): Higher learning rate increases the model instability. We also observed that using higher variance for weight initialization fails to converge. We also reduced β2 from its standard value of 0.99 to reduce spikes in the training loss.  
* [2022] [PaLM](https://arxiv.org/abs/2204.02311): Section 5.1. Re-started training from a checkpoint roughly 100 steps before the spike started, and skipped roughly 200–500 data batches, which cover the batches that were seen before and during the spike. Implies that spikes only occur due to the combination of specific data batches with a particular model parameter state.  
* [2021] [Cogview](https://arxiv.org/abs/2105.13290): Gradients of embeddings higher than other layers, so scale it by 0.1 and detach (1-0.1). Sandwich-LN.  
* [2019] [Transformers without tears](https://arxiv.org/abs/1910.05895): Pre-norm instead of post-norm. ScaleNorm instead of LayerNorm. Reduce weight init.  
