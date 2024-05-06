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

## Results

## Conclusion

## Next steps

## TODO

- [ ] How to evaluate the MATH dataset
- [ ] What if I use the MATH dataset to create few-shot prompts for the train dataset?
