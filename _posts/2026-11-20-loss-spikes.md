---
layout: post
title:  "Diagnosing loss spikes"
---


* [2026] [The Role of Quantization in Loss Spikes](https://arxiv.org/abs/2610.38277): Tested on 1.4B with 28x Chinchilla optimal tokens. A primary driver of these instabilities is the growth and divergence of output logits in the final LM head. Emerges after prolonged training. Replace AdamW with SGD-M on the head.  
* [2026] [Stanford's Deep Learning Alchemy](https://deep-learning-alchemy.github.io/): Most of the course is about training stability, and how to transfer hyperparams (LR, batch size) across scale.  
* [2025] [The smol training playbook](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook#fix-and-restart-vs-fix-on-the-fly): High LR, bad data, poor init.  
* [2025] [ZClip: Adaptive Spike Mitigation](https://arxiv.org/abs/2504.02507): Tested on 1B at high and low LRs. Tracks mean and stddev of gradnorm using EMAs.  
* [2025] [LLM360 K2](https://arxiv.org/abs/2501.07124): Benign and malignant loss spikes. Spikes usually occur alongside large gradient norms. Gradient clipping at 1. Most recover quickly.  
* [2025] [Marin 32B](https://marin.community/blog/2025/10/28/marin-32b-retro/): [Loss spike](https://github.com/marin-community/marin/issues/1368) mitigated by QK-norm. 8B was stable without it. [Tweet](https://x.com/dlwh/status/1938282075326710146). WSD runs could be spikier than cosine. Adam update norm spikes precede loss spikes, but not every update norm spike leads to a loss spike. Gradient norms typically spike after update norm spikes. Skipping steps with extremely large gradient norms, does not reduce time to recovery. Update norm spikes are of higher magnitude on lower layers. When update norm spikes occur, the second-order momentum remains mostly unchanged, but the first-order momentum increases by 2×. AdamC during decay.  
* [2025] [Llama-Nemotron](https://arxiv.org/abs/2505.00949): Section 4.2. Consistently high learning rates caused training instability. Required training resumption with reinitialized optimizer states.  
* [2024] [2 Olmo 2 Furious](https://arxiv.org/abs/2501.00656): QK-norm (section 3.3.2). Normalize the key and query projections with RMSNorm before calculating attention. This avoids attention logits being too large.  
* [2024] [DBRX](https://www.databricks.com/blog/introducing-dbrx-new-state-art-open-llm): QKV clipping ([tweet](https://x.com/zeuxcg/status/1780765558558097440)).  
* [2023] [Scaling Vision Transformers to 22B](https://arxiv.org/abs/2302.05442): 8B diverged due to huge attention logits. Fixed by QK-norm (LayerNorm), parallel layers and no biases. LR decreased with scale.  
* [2023] [Spike No More](https://arxiv.org/abs/2312.16903): 1.5B. Init weights to small values and scale embedding by sqrt(d) or add LayerNorm to embedding layer to reduce variance.  
* [2022] [Bloom](https://github.com/bigscience-workshop/bigscience/blob/master/train/tr11-176B-ml/chronicles.md#2022-04-12-first-lm-loss-spike): Many gradnorm spikes but one loss spike - recovered on its own. FP16 unstable - BF16 worked. Embedding LayerNorm.  
* [2022] [Megatron-Turning NLG](https://arxiv.org/abs/2201.11990): Higher learning rate increases the model instability. We also observed that using higher variance for weight initialization fails to converge. We also reduced β2 from its standard value of 0.99 to reduce spikes in the training loss.  
* [2022] [PaLM](https://arxiv.org/abs/2204.02311): Section 5.1. Re-started training from a checkpoint roughly 100 steps before the spike started, and skipped roughly 200–500 data batches, which cover the batches that were seen before and during the spike. Implies that spikes only occur due to the combination of specific data batches with a particular model parameter state. Also a z-loss to prevent logits growing too large.  
* [2021] [Gopher](https://arxiv.org/abs/2112.11446): Section C.1. Adafactor caused instability.  
* [2021] [Cogview](https://arxiv.org/abs/2105.13290): Gradients of embeddings higher than other layers, so scale it by 0.1 and detach (1-0.1). Sandwich-LN.  
* [2019] [Transformers without tears](https://arxiv.org/abs/1910.05895): Pre-norm instead of post-norm. ScaleNorm instead of LayerNorm. Reduce weight init.  
