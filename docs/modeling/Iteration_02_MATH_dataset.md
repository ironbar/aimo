# Iteration 2. MATH dataset

_06/05/2024_

## Goal

Can we improve LB score by focusing on MATH dataset?

## Motivation

There is a [conversation](https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/499464) on the forum that suggests that the correlation between train score and
leaderboard score is very weak. The host said:

> 10 public problems were intentionally chosen to be at or above average difficulty. 50 test problems have a range of difficulties from relatively simple problems to those approaching national Olympiad level

This implies that claiming the overall prize winner is going to be very hard, because progress on the leaderboard
is not expected to be linear because the difficulty of the problems is increasingly harder.

Futhermore the train set is very small, just 10 problems. Using a bigger dataset for validation will
allow to measure small improvements.

## Development

### About the MATH dataset

MATH is a new dataset of 12,500 challenging competition mathematics problems. Each problem in MATH has a full step-by-step solution which can be used to teach models to generate answer derivations and explanations.

The problems belong to these categories: algebra, counting and probability, geometry, intermediate algebra, number theory, prealgebra and precalculus. They also have levels of difficulty from 1 to 5. The problems are
written in latex and they have also a text response in latex.

The proposed division has 7500 train problems and 5000 test problems. If I were to evaluate all the
test problems once using Kaggle's hardware it would take 90 hours (current submission takes 9 hours to solve 50 problems with 10 repetitions each). So this is a problem. Evaluation is slow. But it is a problem that
all the teams are going to have. And I could use my resources from consultant job to pay for computation.
The prize is 130k$, it might be worth spending a few thousand dollars in evaluation to get the prize.
But I have to first find something that works and is scalable.

Links:

- [Original repo of the MATH dataset](https://github.com/hendrycks/math?tab=readme-ov-file)
- [Kaggle dataset with MATH and GSM8K datasets](https://www.kaggle.com/datasets/alejopaullier/aimo-external-dataset)

#### Token len distribution

![input_token_len_distribution](res/input_token_len_distribution.png)

![output_token_len_distribution](res/output_token_len_distribution.png)

As expected the more difficult problems have longer answers and descriptions. Very beautiful graph.

#### Removing problems with non positive integer answers

I'm left with 4345 train problems and 2828 test problems. The distribution of problems is more or less
balanced except for level 1 that has half the problems than the other categories.

### Evaluating the MATH dataset

If making a single prediction per problem evaluating 566 test problems in 85 minutes. That is around 6 problems per minute.
GPU usage is high, so I don't think there is much room for improvement. I can run two evaluations in parallel
with good GPU usage.

Uncertainty in the results is big, f.e. for an accuracy of 54% the uncertainty is around 4%. Using the whole
test set will reduce the uncertainty below 2%, but evaluation would take 7 hours on my PC.

## Results

## Conclusion

## Next steps

- What about the MATH code dataset?

## TODO

- [ ] How to evaluate the MATH dataset
- [ ] What if I use the MATH dataset to create few-shot prompts for the train dataset?
- [ ] Analyze evaluation results based on difficulty level, how do they correlate with LB score?
- [ ] Use kaggle notebooks for evaluation, I have 30 hours per week.
