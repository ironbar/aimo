# Iteration 10. Select submissions

_25/06/2024_

## Goal

Select a pair of submissions that maximize the chance of ending in a good position.

## Motivation

I have made very little or none progression on the leaderboard throughout this challenge.

However the private test set is very small and the date of submission could be very relevant.

## Results

| version                  | repetitions | date       | LB score                    | mean LB score |
|--------------------------|-------------|------------|-----------------------------|---------------|
| 155 public prompts       | 22          | 22/05/2024 | 16, 21, 21, 21              | 19.8          |
| 179 multiple prompts     | 30          | 05/06/2024 | 16, 17, 18, 18, 18, 19, 20  | 18.0          |
| VLLM 16 multiple prompts | 200         | 10/06/2024 | 18, 18, 18, 19, 20, 21      | 19.0          |
| VLLM 28 original prompts | 175         | 20/06/2024 | 19, 19, 20, 20, 20, 20, 21  | 19.9          |
| VLLM 31 public prompts   | 130         | 22/06/2024 | 19, 20, 22, 22, 22          | 21.0          |

I'm going to submit version 155 and VLLM 28:

- Version 155 scored high one month ago, if I'm lucky that early submission could pay off.
- Version VLLM28 uses a great number of repetitions and uses the prompts defined on the official repo.
  On validation the score is the same as the other approaches, but I hope they will generalize
  better to the private test set. I'm using the official prompts after all!

## Conclusion

I'm going to need luck in this challenge, currently I'm on position 137 with a score of 22, while the
first team has a score of 28.

Hopefully I will learn something from the best teams.

## Next steps

- Review solutions from other teams
