# Iteration n. Iteration_title

_12-06-2024_

## Goal

Can I improve the score using different models?

## Motivation

I have noticed that the DeepSeekMath-RL model that is on Kaggle has different files than the one
on Huggingface. Maybe it is worse.

## Development

## Results

### Evaluation without VLLM

The evaluation is done without VLLM because it was done previously to the development. So it only
has 25 repetitions. Moreover it was done just on half of the data to speedup the evaluation.

| model                  | Accuracy |
|------------------------|----------|
| Kaggle DeepSeekMath-RL | 61.50%   |
| DeepSeekMath-Instruct  | 51.50%   |
| DeepSeekMath-RL        | 59.00%   |

There are no significative differences between Kaggle's and Huggingface's models.

The Instruct model is clearly worse.

### Ensembling the models

Now let's do an evaluation with VLLM. What if I use a different model on each GPU? That might be beneficial.

The following experiment uses 100 repetitions, and only changes the model.

| model         | Accuracy |
|---------------|----------|
| RL + instruct | 58%      |
| RL            | 59%      |

We don't see any improvement when using two different models. This is probably happening because as
seen on the previous section the instruct model is clearly worse.

## Conclusion

We did not observe improvements in validation score when trying other models from the DeepSeekMath family.

## Next steps

## TODO

- [ ]
