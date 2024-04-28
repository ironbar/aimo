# Iteration 1. Overfit the train set

_25-04-2024_

## Goal

Can I get a perfect score on the train set?

## Motivation

I have spend two days refactoring the [Early Sharing Prize Notebook](https://www.kaggle.com/code/abdurrafae/improved-code-interpretation) and now I have a clean code notebook that will allow to do agile changes and iterations.

The notebook uses DeepSeekMath model with a code interpreter to solve math problems. There are many
parameters and parts of the code to tweak.

The train set is small, but that would enable faster evaluation than using other datasets. Once
I'm able to overfit to the train set I could expand to other datasets.

## Development

### Which parameters or changes I can make to improve the results?

- Prompt. I can modify the prompt or use few-shot prompting.
- Temperature. I could modify the `temperature` and `top_p` parameters that guide text generation.
- Dealing with the output. There are many output: boxed output, code output, text output... Can I
  find a better way to aggregate the information?
- Does quantization affect to the results?
- Dealing with code. I have seen problems when parsing the code from the model. Maybe have two
  conditions: one for starting code generation and another for ending.
- How many repetitions?

Finally being able to increase inference speed would enable for faster evaluation and also to run more repetitions on inference.

### What is the best way to use DeepSeekMath?

- [DeepSeekMath Paper](https://arxiv.org/abs/2402.03300). Are there clues in the paper of how to prompt the model, inference configuration...?
  No, the paper does not give too much details of the evaluation. It only mentions that `few-shot chain of thought prompting` was used. It does not
  show which prompts or parameters were used.
- [DeepSeekMath Github repo](https://github.com/deepseek-ai/DeepSeek-Math). Explore the repo to find examples of use.
- [OlympiadBench Github repo](https://github.com/OpenBMB/OlympiadBench). Here they use DeepSeekMath.

### Idea: Most authoritative result is from boxed

If I use examples that output boxed that should be the relevant result, because it is an intelligent LLM parsing the result for me.

Naive parsing the response from the text does not have sense. Especially if the limit of characters is reached.

## Results

### P100 vs 2xT4

| GPU \ Precision | 4bit | 16bit |
|-----------------|------|-------|
| P100            | 12.5 | 18.7  |
| 2xT4            | 11.7 | 15.2  |

My experiments show that P100 is slightly faster than 2xT4. The drawback is that `OOM` errors can arise
when using the 16 bit model.

It is likely that using the 2xT4 in parallel (loading the model in both gpus and making inferences like a server) will beat this speeds.


On my experiments 

P100 4bit 12.5  token/s

2024-04-25 14:38:02,421 - INFO - Generating code speed: 12.5 tokens/s (116)
2024-04-25 14:38:10,432 - INFO - Generating text speed: 12.2 tokens/s (87)
2024-04-25 14:38:18,692 - INFO - Generating code speed: 12.5 tokens/s (103)
2024-04-25 14:38:57,085 - INFO - Generating text speed: 12.8 tokens/s (485)


P100 16 bit 18.7 token/s (OOM problems)
2024-04-25 15:07:53,963 - INFO - Generating code speed: 19.6 tokens/s (119)
2024-04-25 15:08:03,003 - INFO - Generating text speed: 19.2 tokens/s (154)
2024-04-25 15:08:09,252 - INFO - Generating code speed: 18.7 tokens/s (117)
2024-04-25 15:08:22,227 - INFO - Generating text speed: 18.5 tokens/s (221)
2024-04-25 15:08:35,665 - INFO - Generating code speed: 17.9 tokens/s (241)

T4 4bit 11.7 token/s

2024-04-25 14:43:32,370 - INFO - Generating code speed: 11.7 tokens/s (142)
2024-04-25 14:43:39,061 - INFO - Generating text speed: 11.2 tokens/s (65)
2024-04-25 14:43:50,986 - INFO - Generating code speed: 11.7 tokens/s (140)
2024-04-25 14:43:58,058 - INFO - Generating text speed: 10.8 tokens/s (71)
2024-04-25 14:44:11,051 - INFO - Generating code speed: 11.7 tokens/s (152)
2024-04-25 14:52:29,408 - INFO - Generating text speed: 10.0 tokens/s (136)
2024-04-25 14:52:51,653 - INFO - Generating code speed: 10.9 tokens/s (242)

T4 16bit
2024-04-25 14:53:53,382 - INFO - Generating text speed: 8.3 tokens/s (41)
2024-04-25 14:54:01,175 - INFO - Generating code speed: 15.5 tokens/s (121)
2024-04-25 14:54:09,916 - INFO - Generating text speed: 15.4 tokens/s (120)
2024-04-25 14:54:18,102 - INFO - Generating code speed: 15.2 tokens/s (124)
2024-04-25 14:54:26,484 - INFO - Generating text speed: 14.2 tokens/s (96)
2024-04-25 14:54:41,359 - INFO - Generating code speed: 14.7 tokens/s (218)

https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/492578
https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/493345

### Single problem optimization

I have downloaded the notebook to my PC and it is running at around 30 token/s. I'm thinking of doing
a single problem optimization. Focus on a specific problem and run the solution search multiple times
maximizing the probability of getting the correct answers. Each run could take a few minutes so
the optimization speed would be nice.

## Conclusion

## Next steps

- I might try to replicate or even improve the results of DeepSeekMath on MATH dataset.

## TODO

- [ ] Problems when generating loops. https://huggingface.co/docs/transformers/en/main_classes/text_generation. That is `frequency_penalty` on OpenAI but on huggingface there are other options.
- [ ] Analyze deepseekmath library and define experiments
