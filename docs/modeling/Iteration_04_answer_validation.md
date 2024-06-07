# Iteration 4. Answer validation

_06-06-2024_

## Goal

Can we improve the accuracy of the model by validating the answers?

## Motivation

The current solution is able to achieve a 75% pass25 accuracy and 57% maj25 accuracy when being evaluated
on 580 level 5 MATH problems. This implies that the majority has an accuracy of 76% for selecting the
correct answer.

Can I use an LLM to validate or discard answers? That might help to improve the accuracy of the solution.

Another option would be to give the numerical answers as options and request to solve the problem again.
However there is very little information provided in that scenario, I don't believe it has sense.

We might give complete solutions to the model and ask the model to select the correct one. That way
the model has a lot of context and this might work. The downside is that when using the P100 the
available context window is small. We might have to use another model such as phi-2.

## Development

### Play with answer validation

The idea is to take the responses from an evaluation and request the model to validate them. Using the
chat format could be a good way to try that.

## Results

### DeepSeekMath is not able to validate responses or select the correct response

I have made multiple experiments with different problems and responses and almost always DeepSeekMath
says that the answer is correct. Even more surprising is that GPT4-o makes obvious mistakes also.

I have also tested giving multiple response to the model and asking to select the correct and the
responses seemed to be random. This DeepSeekMath model is not very intelligent.

I might try with other models.

## Conclusion

DeepSeekMath is a model that can generate responses to mathematical problems, but it is not able of
validating the answers or select the correct response among a few responses. It is not an intelligent model.

## Next steps

- Try different models instead of Kaggle's DeepSeekMath-RL
- Try [VLLM](https://github.com/vllm-project/vllm) to speedup model inference
- Experiments with different temperatures or increasing temperatures
- I might improve the results by rewriting the problems to make them more clear, or divide the problem in steps.

## TODO

- [ ]
