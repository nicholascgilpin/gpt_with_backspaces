# gpt_with_backspaces
What happens if we fine tune a small reasoning GPT model on reasoning traces with backspaces?

## Introduction
Autoregressive models are believed to be limited in their reasoning ability because their internal mechanisms function similar to [beam search](https://en.wikipedia.org/wiki/Beam_search). The problem with beam seach like methods is that they often start down a wrong or difficult path and can't go back. Tracking backspace characters would allow for backtracking and may allow an autoregressive model system to function more like [depth first search](https://en.wikipedia.org/wiki/Depth-first_search). A backtracking reasoning model would be useful because it would be able to return to an earlier state if it encountered an unresolvable problem much deeper along the path it was taking. However, it couldn't return to an exact earlier state, it would need to leave itself a note to not take the incorrect path. 

## Experiment Plan
1. Check to see if anyone's done this already. (Backspaces were implemented, but not with reasoning models or GRPO.)
2. If not, create a dataset by tracking myself solving some problems while including the backspace character. Likely around 1,000. <-- In progress
3. Fine tune a small reasoning model like Deepseek-R1:8B on the reasoning traces with [GPRO](https://arxiv.org/abs/2501.12948) using Qlora to get the code right
4. Do full fine tuning without Qlora on the cloud (https://app.hyperbolic.xyz/)

## How to Help
The main slow down is creating and recording high quality reasoning traces with the back space characters included. If you can do that, then add them to the dataset folder. Also, let me know if there's an easy way to do that. I'm currently looking for a key logger. 

Reasoning Trace Requirements:
1. Must write down all thoughts and remembered facts
2. Some examples must recover from errors or distractions
3. Must show all steps used to solve the problem
4. Must solve an easily verifiable problem
5. Must include answer
6. Use the JSON format

**The JSON Format**

q1.json
```
{
"Question": "A simple math question string.",
"Answer": <Integer>,
"Reasoning": "Your reasoning with any backspaces included. Try to reason in under 2048 characters for the training budget :)"
}
```
## Project Estimates
I'm estimating this would take about a week of full time work or a few months of part time work. 
- Man hours: 80-320
- H100 hours: Just 1 assuming perfection
- VRAM required: ~24GB
- Cost: $1-$10

## Related Work

DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning
DeepSeek-AI
https://arxiv.org/abs/2501.12948

Step Back to Leap Forward: Self-Backtracking for Boosting Reasoning of Language Models
Xiao-Wen Yang, Xuan-Yi Zhu, Wen-Da Wei, Ding-Chu Zhang, Jie-Jing Shao, Zhi Zhou, Lan-Zhe Guo, Yu-Feng Li
https://arxiv.org/abs/2502.04404

SequenceMatch: Imitation Learning for Autoregressive Sequence Modelling with Backtracking
Chris Cundy, Stefano Ermon
https://arxiv.org/abs/2306.05426
