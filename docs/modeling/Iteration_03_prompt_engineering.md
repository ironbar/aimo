# Iteration n. Iteration_title

_24-05-2024_

## Goal

Can I improve the LB score with prompt engineering?

## Motivation

I'm going to leave the evaluation fixed: I'm going to use MATH level 5 problems (580) and I will be using 5 repetitions for each problem (confidence level 100%).

I want to try different prompt strategies:

- No code prompt
- Bad prompt
- Few-shot prompt
- Few-shot prompt with RAG
- Carefully crafted prompts

If the model is steerable by prompts I will be able to improve the LB score. If not
I will have to find another strategy.

I need to improve from my current 21 on LB score to 27, that is a +12% in accuracy that I need to get.

## Development

## Results

## Conclusion

After a week and more than 20 experiments before I have not been able to improve LB score with prompt engineering. How could I improve?

- Using a better base model to generate answers. Fine-tuning DeepSeekMath may allow to do that.
  However people in the forum have said that they got worse results after fine-tuning. Remember that
  the model has already being trained with RL.
  It is uncertain if fine-tuning can improve the reasoning skills of a model.
- Change the generation process. Maybe giving as input already generated answers in a dialog between LLMs.
  Or we might give the possible answers to the model to choose between them, like in a test exam. [MMLU example](https://github.com/deepseek-ai/DeepSeek-Math/blob/main/evaluation/few_shot_prompts/cot_mmlu_stem_4_shot.py)
- Validate or verify the answers. I might discard wrong answers by validating them. Some problems might
  be easier to validate than others.
- Answer selection. Instead of relying on votes, I might use a model to select the best answer.
- Maybe rewriting the problem in a more clear way could help sometimes. I could create a dataset with rewritten problems and test the accuracy on it.

Score of 22 when increasing temperature to 0.9, probably luck.

## Next steps

- Reread the literature and better understand how DeepSeekMath model was trained

## TODO

- [x] How long does it take the evaluation with 5 repetitions? around 10 hours.
- [x] Prompts to evaluate
  - [x] CoT no code prompt
  - [x] Minimal prompt
  - [ ] ~~Bad prompt~~
  - [x] Few-shot prompt
  - [x] Few-shot prompt with RAG
  - [x] Temperature and top_p
  - [x] Prompt that uses code from the repo
  - [x] Ask the model to verify the answer. It ignores the request to verify the answer. If we want to do a verification we should do it manually.
- [ ] Document results
- [ ] Full evaluation with the best configuration
- [ ] Analysis merging the results of all the evaluations
