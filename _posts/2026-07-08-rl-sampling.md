---
layout: post
title:  "RL: problem-solving ability or sampling efficiency?"
---

RL is generally used to improve problem-solving ability of LLMs ever since OpenAI o1 started the trend. Over the past two years, this has led to a plethora of breakthroughs and related software, for example a bunch of RL environment [startups](https://pavlovslist.com/). Many people are now talking about RL as the missing piece to Artificial General Intelligence. But it's still a nascent research area lacking rigorous evaluations. I found a recent [paper](https://arxiv.org/abs/2504.13837) which was the runner-up in the ICML Best Paper track which looked pretty interesting and I tried reproducing the experiment.

The paper posits that RL does not actually improve problem solving ability, but rather makes it efficient. If a pre-RL model took _T<sub>1</sub>_ attempts to solve the problem, the post-RL model would do it in _T<sub>2</sub>_ attempts where _T<sub>2</sub>_ < _T<sub>1</sub>_.

So, the claim is that the _ability_ to solve the problem is already present (i.e. latent) inside the model and RL just _elicits_ it.

### Experiment Setup

Two metrics that will be relevant to us are ``pass@K`` and ``pass@1``. ``pass@1`` denotes the number of tasks solved by the model given exactly 1 attempt at it, and ``pass@K`` denotes the number of tasks solved by the model given exactly K attempts at it (if any one of them works, then it's considered to be solved). Generally, ``pass@K`` values are higher than ``pass@1`` because the chances of success are higher if the model gets multiple attempts.

Now, we want to compare the post-RL model with the pre-RL model. Given a particular task, compare two metrics:  
1) ``pass@K`` for that task using the pretrained (pre-RL) model  
2) ``pass@1`` for that task using the post-RL model  

If _1_ > _2_, that means there's a significant set of tasks that are _solvable_ using the pre-RL model and RL __did not__ actually add any previously missing problem-solving ability for those tasks. For RL to add that ability, _2_ would need to be more than _1_.  

The following generation params were used via SkyRL.  

```
generator.eval_n_samples_per_prompt=128 \
generator.eval_sampling_params.temperature=0.6 \
generator.eval_sampling_params.top_p=0.95 \
```

I took the [Qwen2.5-1.5B-Instruct](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct) model. Deliberately picked a small model because conventional wisdom is that reasoning ability (eg coding) generally appears at mid sizes (32B+). I evaluated this model on the [gsm8k](https://huggingface.co/datasets/openai/gsm8k) math dataset for values: ``K=16``, ``K=64`` and ``K=128``.  

__Costs:__ Everything ran on a single A100-SXM which go for about $2 per GPU per hour. The K128 run took 6 hours (=$12), K64 run 3.5 hours (=$7), K16 run 2.5 hours (=$5) and miscellaneous small runs around 2 hours total (=$4) which brings the total cost to around $28.

### Results

Looking at the ``pass@K`` metrics, the ``K=16`` eval reached 93% at step 10, the ``K=64`` eval reached 97% and ``K=128`` reached 98%. Compared to these, the post-RL model described in this [previous post](https://satyaki-up.github.io/2026/07/03/rl-replication.html) only reached 78% on the ``pass@1`` metric.  

So it seems like the post-RL model has a lot of room to improve. It's also possible that GSM8K was leaked into the training data which renders this benchmark meaningless, but I still find it surprising that a small 1.5B model could get such a high score.

<img src="{{site.baseurl}}/assets/images/post_2/post_2_pass_16.png" title="Pass@16">
<img src="{{site.baseurl}}/assets/images/post_2/post_2_pass_64.png" title="Pass@64">
<img src="{{site.baseurl}}/assets/images/post_2/post_2_pass_128.png" title="Pass@128">

**Addendum**: I was also pointed to a [survey](https://safe-lip-9a8.notion.site/Incorrect-Baseline-Evaluations-Call-into-Question-Recent-LLM-RL-Claims-2012f1fbf0ee8094ab8ded1953c15a37) (Chandak, Goel, Prabhu (2025)) (thanks [Felix](Felix Breuer)) about recent RL papers which seem to overstate what RL actually achieved. One common failure mode is sandbagging the baseline or not tuning its hyperparams a lot, but this is an [old problem](https://www.youtube.com/watch?v=wVkViYY_fwA).
