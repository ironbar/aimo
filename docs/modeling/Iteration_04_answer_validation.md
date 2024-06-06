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

## Conclusion

## Next steps

## TODO

- [ ]
