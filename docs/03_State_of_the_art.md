# State of the art

## [AlphaCode 2](https://storage.googleapis.com/deepmind-media/AlphaCode2/AlphaCode2_Tech_Report.pdf)

![alphacode2](https://miro.medium.com/v2/resize:fit:707/1*DA0775ksid_HwEuBqj-g_w.png)

1. Finetune many models to generate code given a problem description
2. For each problem it generates up to 1M possible solutions. We don't have that much compute for our task.
3. Filter all the solutions that do not pass the public test or compile. This removes 95% of the solutions. We cannot do this on AIMO because we don't have any input and output data. If we decide to use code as the output of the model we might discard code with problems, but nothing more.
4. Clustering of the solutions. They generate new input data and use the output on that data to clusterize the solutions. This again will be hard to do, or impossible for our problem because not all the problems have this property.
5. Score the candidates. They have another model to estimate correctness of the solutions. This is something we can replicate.

They used Gemini Pro as the base model. This resulted on a big improvement over previous version of AlphaCode that I believe it used Palm. It is likely that even better results would have been obtained with Gemini Ultra, but at a higher computational cost.

### Learnings

- Generating a lot of solutions and scoring them could be a good strategy
- Having a good base model is very important

## [AlphaGeometry](https://deepmind.google/discover/blog/alphageometry-an-olympiad-level-ai-system-for-geometry/)

> AlphaGeometry is a neuro-symbolic system made up of a neural language model and a symbolic deduction engine, which work together to find proofs for complex geometry theorems. Akin to the idea of “thinking, fast and slow”, one system provides fast, “intuitive” ideas, and the other, more deliberate, rational decision-making.

![alphageometry](https://lh3.googleusercontent.com/CXoZ8QVYA7wKFPt3RurU7Z0SDyp32YQS9gJaEwE-U1AtjAQ-eXEaGxnOSTUH01oyN7YOxz-BILe390w2wHVEFF7XPmCOzqr0QMBroKc4J5kPFyqYVqU=w616-rw)

> AlphaGeometry solving a simple problem: Given the problem diagram and its theorem premises (left), AlphaGeometry (middle) first uses its symbolic engine to deduce new statements about the diagram until the solution is found or new statements are exhausted. If no solution is found, AlphaGeometry’s language model adds one potentially useful construct (blue), opening new paths of deduction for the symbolic engine. This loop continues until a solution is found (right). In this example, just one construct is required.

![alphageometry ranking](https://lh3.googleusercontent.com/y7r-p8VmkqSLE0ZcwidAO0osQ1Sz1y4FBhwQNkv7t1M5bajHTvCu1vTYxDmVJZ2WuknpHeQB2E6RkPUEu-fAVoAxgh8thMPR6bcK4NFyGFuQ4mo5=w616-rw)

> AlphaGeometry’s system combines the predictive power of a neural language model with a rule-bound deduction engine, which work in tandem to find solutions. And by developing a method to generate a vast pool of synthetic training data - 100 million unique examples - we can train AlphaGeometry without any human demonstrations, sidestepping the data bottleneck.

### Learnings

- It generates a huge dataset for training of 100M of samples
- By using a deduction engine they can check if they have arrived at the required solution
- Is there any deduction engine to solve math problems?
- Reasoning is done with the deduction engine, AI does the intuition.

## [DeepSeek Math](https://github.com/deepseek-ai/DeepSeek-Math)

They take the model DeepSeek-Coder and continue training with 120B math-related tokens. Next fine-tuning
on instructions and RL is done.

![deepseek-results](https://raw.githubusercontent.com/deepseek-ai/DeepSeek-Math/main/images/instruct_results.png)

## [Orca: Progressive Learning from Complex Explanation Traces of GPT-4](https://arxiv.org/pdf/2306.02707.pdf)

They fine-tune a Llama model in 5M chain of thought responses from ChatGPT and GPT4. This results
on much powerful model than simply fine-tuning on query, response pairs because it has traces of
the reasoning.

Training required around 3.2k A100-hours.

[Orca: The Model Few Saw Coming, by AI Explained](https://www.youtube.com/watch?v=Dt_UNg7Mchg)

## [Llemma: An Open Language Model For Mathematics](https://arxiv.org/abs/2310.10631)

They take Code Llama and fine-tune on 55B tokens math datasets. Training requires 23k A100 hours.

![llemma](https://blog.eleuther.ai/images/blog/llemma/plot.png)

## [Minerva: Solving Quantitative Reasoning Problems with Language Models](https://arxiv.org/abs/2206.14858)

## [Solving Challenging Math Word Problems Using GPT-4 Code Interpreter with Code-based Self-Verification](https://arxiv.org/abs/2308.07921v1)

## Comparison of closed source models

https://www.anthropic.com/news/claude-3-family 60.1% 0-shot CoT
[Gemini 1.5](https://arxiv.org/abs/2403.05530) 58.5% 4-shot Minerva prompt
https://github.com/openai/simple-evals 72.2% 0-shot CoT

Seems that `gpt-4-turbo-2024-04-09` is currently the king.

## Conclusions

The state of the art is far from the super-prize threshold of solving 94% of the problems. On the MATH dataset the highest score is GPT-4 with code interpreter that reaches 70%, without code interpreter the score is 53%. So
using a code interpreter could be very important.

MATH dataset could be the most similar dataset to the one in the challenge.

It seems that code training improves reasoning abilities, that is why code models are used as a base.

## Vision

A model trained to generate code to solve math problems using GPT4 demonstrations. Orca like.

## TODO

- [ ] Latex model
- [ ] Search about the topic of LLMs and maths
- [ ] Search papers in Kaggle
- [ ] https://paperswithcode.com/sota/math-word-problem-solving-on-math to watch
- [ ] Minerva prompt
- [ ] Download MATH dataset, 
