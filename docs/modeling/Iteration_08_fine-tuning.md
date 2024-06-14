# Iteration 8. Fine-tuning

_13/06/2024_

## Goal

Can I improve the LB score by fine-tuning DeepSeekMath on MATH problems?

## Motivation

The best team is getting a score of 27 on leaderboard, while my luckiest submission only gets 22.
I have done already many experiments with DeepSeekMath-RL model, so maybe their advantage is that they
have fine-tuned the model to high school problems.

## Development

### Direct Preference Optimization

My idea is to use DPO to teach the model to better solve the math problems. I have evaluated the MATH
dataset many times and thus for each problem I have a lot of good and bad answers. I can use that
data to fine-tune the model.

Then I will evaluate on the test set and I should get a huge improvement since I will be training
and evaluating on the same set. But that will validate that the training has worked.

The real test will be the leaderboard. If I see improvements in the leaderboard then the next step
would be to gather new data to evaluate and later fine-tune the model.

#### How to train with DPO?

- <https://huggingface.co/docs/trl/main/en/dpo_trainer>
- <https://github.com/huggingface/trl/blob/main/examples/scripts/dpo.py>
- I fine-tuned a model with LoRA for the LLM prompt recovery challenge. [Example notebook](https://github.com/ironbar/prompt_recovery/blob/main/notebooks/014_fine-tune_mistral_v2.ipynb)
- <https://www.philschmid.de/dpo-align-llms-in-2024-with-trl>
- <https://medium.com/@anchen.li/fine-tune-llama-2-with-sft-and-dpo-8b57cf3ec69>?

I have to create a dataset with the fields: prompt, chosen and rejected. The prompt does not need to
be in the answers. [Source code](https://github.com/huggingface/trl/blob/f5168fdbaf9cbf6a3f1bdc64dc44b9db3a9ae333/trl/trainer/dpo_trainer.py#L678)

#### Dataset for DPO

- 509 MATH test level 5 problems
- 10661 pairs of good and bad responses
- Max prompt length: 296
- Max length: 937

## Results

## Conclusion

## Next steps

## TODO

- [ ] Notebook to create train dataset, that will make the training notebook shorter.
- [ ] How to train the model using DPO and LoRA?
- [ ] How to make inference with VLLM and LoRA?
