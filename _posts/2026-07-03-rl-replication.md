---
layout: post
title:  "Replicating RL for post-training"
---

Reinforcement learning is now widespread in the post-training of LLMs. It started with RLHF specifically for alignment ([paper](https://arxiv.org/abs/1706.03741), [inventor](https://x.com/dwarkesh_sp/status/1719371669847122278)) but is now used as RLVR, for other domains (mainly math and programming). We're a long way from the era of RL on games (most famously AlphaGo) and there's a plethora of algorithms now. In this post, I'll focus only on RLVR, not RLHF.

### Experiment Setup

I used my own fork of [SkyRL](https://github.com/novasky-ai/skyrl), one of the most RL frameworks right now (along with [slime](https://github.com/THUDM/slime), [verl](https://github.com/verl-project/verl) and [prime-rl](https://github.com/PrimeIntellect-ai/prime-rl)). I picked [Qwen2.5-1.5B-Instruct](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct) released in end-2024 just after the release of OpenAI o1 ([paper](https://arxiv.org/pdf/2412.15115)) and the [GSM8K](https://huggingface.co/datasets/openai/gsm8k) benchmark for math performance. As per the technical report, Qwen2.5-1.B scores around 68%.

All experiments were conducted on a single A100-SXM4 rented via Lambda Labs (currently going for $1.99 per hour). The RL climb ran for 100 steps with the default [config](https://github.com/NovaSky-AI/SkyRL/blob/main/examples/train/gsm8k/run_gsm8k.sh) after reducing the batch size to 128 and micro batch size to 16 to accommodate the lower VRAM. Every run took around 3 hours and I ran 6 algorithms, which brings the cost of the entire experiment (excluding a few trial runs) to around $36.

For each algorithm, I used the default settings, which SkyRL had set as per the recommendations from the respective papers.

GRPO: 5 samples per prompt  
Dr GRPO: 5 samples per prompt  
DAPO: eps 0.2 and 0.28, overlong length 512  
SAPO: tau 1.0 and 1.05  
Reinforce++  
RLOO  


### Results

All of them ended up in the [75%, 78%] range after 100 steps for pass@1. DAPO reaches the highest (79.4%) but the delta is low (~3%).

<img src="{{site.baseurl}}/assets/images/pass@1.png" title="Pass@1">

When we look at the rewards, we see that DAPO rewards are a lot lower than the others, even though it scores the highest on the eval.

<img src="{{site.baseurl}}/assets/images/reward.png" title="Mean positive reward">

DAPO takes the fewest tokens per turn on the eval and SAPO the highest, so DAPO seems to be more cost effective.

<img src="{{site.baseurl}}/assets/images/tokens_per_turn.png" title="Eval tokens per turn">

All the policies seem to have lost entropy, reducing exploration as training progresses.

<img src="{{site.baseurl}}/assets/images/policy_entropy.png" title="Policy entropy">

