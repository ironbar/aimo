# Iteration 9. Giving hints to the model

_17/06/2024_

## Goal

Can we improve the accuracy of the model by giving hints of how to solve the problem?

1. Does the model improve if being given hints?
2. Can I automate the process of giving hints?

## Motivation

![ways of improvement](res/2024-06-06-09-16-28.png)

I have explored almost all ideas:

- Using VLLM to speedup inference. Inference was much faster but results didn't improve.
- Could not fine-tune the model to be more accurate
- Could not make the model to validate or select the correct answer
- Using the instruct model in an ensemble with the RL model did not improve

So today I was re-reading the forum and read some comments about how brittle the model is. Changing
small parts of a problem results in very different inferences. So maybe we can use that in our favour.

## Development

On a first step I'm going to take problems where the model is struggling to solve them. Since the
MATH dataset has solutions I could use them for inspiration to give hints to the model. I will
measure how much the model improves and if it is promising I will have to find a way to automate
the process of giving hints.

## Results

## Conclusion

## Next steps

## TODO

- [ ]
