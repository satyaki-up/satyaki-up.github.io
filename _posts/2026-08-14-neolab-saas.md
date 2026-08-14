---
layout: post
title:  "AI neolabs vs traditional software companies"
---

These are the main differences between the recent "neolabs" and traditional software startups. A neolab is defined as a company whose raison d'etre is to train AI models. So companies which primarily sell some product and post-train models for it, are excluded.  

#### Mathematical maturity of technical staff

The specific term "mathematical maturity" I [took](https://vladfeinberg.com/2026/05/10/how-to-land-a-job-at-a-frontier-lab.html) from the Gemini Flash pre-training lead. Most software startups over the past 30 years have focused on software engineering. Being a valuable contributor often meant just "shipping things" and it was fairly easy to become productive soon, by just writing code fast. Research labs run experiments and there's thinking involved - the code is often a few lines but those changes were made after a lot of thinking. An example would be clipping the importance sampling [ratio](https://fengyao.notion.site/off-policy-rl) instead of the update. For changes like this, you need to have an intuitive understanding of the math. This takes time to build, often via a PhD. Coming up with a novel research idea/direction needs this intuition and then scaling it involves some engineering. For example, gradient updates for large batch sizes led to numerical instability errors in BF16 but worked in FB32, so you do the computations in FP32 and then downcast to FP16 at the end - this is an example of an engineering solution at scale. Research is not engineering at slower speed [[source](https://voiceinthemachine.com/2026/06/10/research-is-not-engineering-at-a-slower-speed/)].

It would help to have an intuitive grasp of the basics of the following fields:  
1) Calculus  
2) Optimization  
3) Information theory  
4) Probability theory  
5) Neural networks  
6) Classical machine learning  
7) Linear algebra  

There are many online resources for this [[book](https://mml-book.github.io/)]. It's definitely doable but takes time.  

#### Thinking-Doing ratio

This is related to the point above. I came up with this metric, defined as the amount of time you spend Thinking to the time you spend Doing. In this case, Doing refers to coding.  
1) TDR is low for software startups, especially product oriented ones. You get a list of features/bug reports and just keep knocking them off.  
2) When it comes to the engineering aspects of training models, eg. data pipelines, TDR is similar to traditional software. A great example would be Poolside's [Model Factory](https://www.latent.space/p/poolside).  
3) TDR is high for research, whether the actual code changes might not be much but there's a lot of thinking beforehand.  

 Modern LLMs in the "AI race" have often been reduced to engineering problems - you take a known playbook (maybe one of the recent technical reports) and then just execute. This will be enough to get a respectable model. But at the frontier, labs do genuine research. It's not just in the US - [mHC](https://arxiv.org/abs/2512.24880) from Deepseek, [Attention Residuals](https://arxiv.org/abs/2603.15031) from Kimi, [DAPO](https://arxiv.org/abs/2503.14476) from Bytedance.  

 I used to take part in "competitive programming" contests [[Codeforces](https://codeforces.com/profile/satyaki3794)][[Topcoder](https://profiles.topcoder.com/satyaki3794)][[IOI Camp](https://www.iarcs.org.in/inoi/2017/)] and those problems also had a high TDR ratio - you had to come up with the math/algorithm and quickly coded it. This might be a reason that people who trained for competitive olympiads do so well in AI labs.    


#### Marginal costs and economies of scale

Traditional software startups have low marginal costs. An additional user can be served on the same server and the hardware cost of this is tiny. In contrast, AI models are hardware-intensive and have a big dependency of the number of GPUs in the cluster. There's a GPU crunch which bottlenecks scaling to higher traffic loads.  


#### Geopolitics

Given the promise and potential of AI, it invites government scrutiny unlike previous technologies which means that neolabs are subject to geopolitical factors (eg cut off from TSMC which worsens the GPU crunch, government action because of unemployment risk). Tradtional software startups do not have this.



