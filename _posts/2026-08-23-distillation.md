---
layout: post
title:  "Rundown: Distillation"
---

The term "distillation" was originally introduced by Hinton's paper in 2015, also coining "dark knowledge", i.e. every neural network has some hidden knowledge that can be extracted into a smaller one. There's been a long history of cutting down big networks to smaller ones (compression, sparsity, optimal brain damage) but distillation was one of the first to use the logits of the teacher as a soft target to run gradient descent on the student. Nowadays, the meaning of distillation has changed. Just generating outputs from a bigger teacher and then supervised learning on the student also counts - known as imitation learning or behaviour cloning. But the teacher is off-policy, so it has a different distribution than the student. To fix that, on-policy distillation uses traces from the student and gets the teacher to score them (i.e. retrieve teacher logits) and this plays nicely with RL trajectory generation.  


#### References

* [2026] [Self-Distilled Reasoner: On-Policy Self-Distillation for Large Language Models](https://arxiv.org/abs/2601.18734)  
* [2026] [On-Policy Context Distillation for Language Models](https://arxiv.org/abs/2602.12275)  
* [2025] [On-Policy Distillation](https://thinkingmachines.ai/blog/on-policy-distillation/)  
* [2023] [On-Policy Distillation of Language Models](https://arxiv.org/abs/2306.13649)  
* [2023] [MiniLLM: On-Policy Distillation of Large Language Models](https://arxiv.org/abs/2306.08543)  
* [2021] [Does Knowledge Distillation Really Work?](https://arxiv.org/abs/2106.05945)  
* [2020] [Towards Understanding Ensemble, Knowledge Distillation and Self-Distillation in Deep Learning](https://arxiv.org/abs/2012.09816)  
* [2019] [A Comprehensive Overhaul of Feature Distillation](https://openaccess.thecvf.com/content_ICCV_2019/papers/Heo_A_Comprehensive_Overhaul_of_Feature_Distillation_ICCV_2019_paper.pdf)  
* [2019] [Be Your Own Teacher](https://arxiv.org/abs/1905.08094)  
* [2018] [Knowledge Transfer with Jacobian Matching](https://arxiv.org/abs/1803.00443)  
* [2018] [Born-Again Neural Networks](https://arxiv.org/abs/1805.04770)  
* [2016] [Sequence-Level Knowledge Distillation](https://arxiv.org/abs/1606.07947)  
* [2016] [Unifying Distillation and Privileged Information](https://leon.bottou.org/publications/pdf/iclr-2016.pdf)  
* [2015] [FitNets: Hints for Thin Deep Nets](https://arxiv.org/abs/1412.6550)  
* [2015] [Distilling the Knowledge in a Neural Network](https://arxiv.org/abs/1503.02531)  
* [2015] [Learning Using Privileged Information](https://www.jmlr.org/papers/volume16/vapnik15b/vapnik15b.pdf)  
* [2013] [Do Deep Nets Really Need to be Deep?](https://arxiv.org/abs/1312.6184)  
* [2006] [Model Compression](https://dl.acm.org/doi/pdf/10.1145/1150402.1150464)  




