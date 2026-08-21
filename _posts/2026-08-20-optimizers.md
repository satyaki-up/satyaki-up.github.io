---
layout: post
title:  "Rundown: Optimizers"
---

AdamW has been the standard for more than a decade - even the beta parameters have standard initializations. But second-order methods like Muon are becoming popular (thanks to Kimi). AdamW uses an adaptive method, using the first two moments to decide the step side, and adds weight decay instead of L2 regularization. Many earlier methods used momentum (eg Polyak heavy-ball or Nesterov). Second-order methods like L-BFGS, Shampoo and SOAP are considered infeasible because of computational reasons (calculating the Hessian) - many of them incporate information about the curvature of the function by somehow approximating the Hessian (eg. multiplying the gradient with a preconditioner before taking an optimization step). AdamW needs to store the first and second moments for each parameter which triples memory - frameworks like ZeRO shard these across GPUs. Many of these formulae are not intuitive - Nesterov allegedly said "zero intuition, just calculation".  


#### References

* [2026] [Is optimization theory relevant for neural networks?](https://www.cs.ubc.ca/~schmidtm/Documents/2026_ICML_Tutorial.pdf)  
* [2025] [Muon is Scalable for LLM Training](https://arxiv.org/abs/2502.16982)  
* [2025] [Deriving Muon](https://jeremybernste.in/writing/deriving-muon)  
* [2024] [SOAP: Improving and Stabilizing Shampoo using Adam](https://arxiv.org/abs/2409.11321)  
* [2021] [Understanding Modern Techniques in Optimization: Frank-Wolfe, Nesterov's Momentum, and Polyak's Momentum](https://arxiv.org/abs/2106.12923)  
* [2018] [Three Mechanisms of Weight Decay Regularization](https://arxiv.org/abs/1810.12281)  
* [2018] [Shampoo: Preconditioned Stochastic Tensor Optimization](https://arxiv.org/abs/1802.09568)  
* [2017] [Decoupled Weight Decay Regularization](https://arxiv.org/abs/1711.05101)  
* [2017] [The Marginal Value of Adaptive Gradient Methods in Machine Learning](https://arxiv.org/abs/1705.08292)  
* [2017] [Visualizing the Loss Landscape of Neural Nets](https://arxiv.org/abs/1712.09913)  
* [2015] [Adam: A Method for Stochastic Optimization](https://arxiv.org/abs/1412.6980)  
* [2015] [Optimizing Neural Networks with Kronecker-factored Approximate Curvature](https://arxiv.org/abs/1503.05671)  
* [2013] [On the importance of initialization and momentum in deep learning](https://proceedings.mlr.press/v28/sutskever13.html)  
* [2012] [RMSProp](https://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf)  
* [2011] [Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](https://jmlr.org/papers/v12/duchi11a.html)  
* [2010] [Deep learning via Hessian-free optimization](https://icml.cc/Conferences/2010/papers/458.pdf)  
* [1998] [Efficient Backprop](https://bottou.org/papers/lecun-98x)  
* [1996] [Using weight decay to optimize the generalization ability of a perceptron](https://ieeexplore.ieee.org/document/548898)  
* [1991] [A Simple Weight Decay Can Improve Generalization](http://yaroslavvb.com/papers/krogh-simple.pdf)  


