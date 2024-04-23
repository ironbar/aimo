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

## TODO:

- [ ] Latex model
- [ ] ORCA paper
- [ ] Search about the topic of LLMs and maths