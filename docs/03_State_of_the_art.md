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

## [DeepSeek Math](https://github.com/deepseek-ai/DeepSeek-Math)

## TODO:

- [ ] Latex model
- [ ] ORCA paper
- [ ] Search about the topic of LLMs and maths