---
layout: post
title:  "Rundown: Position encodings"
---

Modern LLMs are based on the attention operation which is a set operation, i.e. it has no concept of order. Position encodings add the concept of order, so the same word in different places in a sentence are not treated equivalently. The original Transformers paper used sinusoidal embeddings which are now deprecated - RoPE is the most popular. In modern LLMs, the attention block is also not standard full dot product but alternating between quadratic and linear - often both these have different position encodings or none (NoPE). Position encodings become particularly relevant for long-context training - if the model is trained on a smaller context length, it generally underperforms on longer contexts during inference.   


#### References

* [2024] [CoPE](https://arxiv.org/abs/2405.18719)  
* [2023] [YaRN](https://arxiv.org/abs/2309.00071)  
* [2023] [The Impact of Positional Encoding on Length Generalization](https://arxiv.org/abs/2305.19466)  
* [2022] [Position Information in Transformers](https://aclanthology.org/2022.cl-3.7.pdf)  
* [2021] [ALiBi](https://arxiv.org/abs/2108.12409)  
* [2021] [RoFormer](https://arxiv.org/abs/2104.09864)  
* [2021] [Rotary Embeddings: A Relative Revolution](https://blog.eleuther.ai/rotary-embeddings/)  
* [2020] [Rethinking Positional Encoding in Language Pre-training](https://arxiv.org/abs/2006.15595)  
* [2018] [Self-Attention with Relative Position Representations](https://arxiv.org/abs/1803.02155)  
* [2017] [Attention Is All You Need](https://arxiv.org/abs/1706.03762)  
* [2015] [End-To-End Memory Networks](https://arxiv.org/abs/1503.08895)  




