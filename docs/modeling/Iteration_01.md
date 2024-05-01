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

The following table shows inference speed in tokens/second.

| GPU \ Precision | 4bit | 16bit |
|-----------------|------|-------|
| P100            | 12.5 | 18.7  |
| 2xT4            | 11.7 | 15.2  |

My experiments show that P100 is slightly faster than 2xT4. The drawback is that `OOM` errors can arise
when using the 16 bit model.

It is likely that using the 2xT4 in parallel (loading the model in both gpus and making inferences like a server) will beat this speeds.

Links to forum posts:

- <https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/492578>
- <https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/493345>

### Zero shot vs Few shot instruction following

I have found that the model tends to ignore the instructions. It is much better at imitating the style of the few-shot prompt.

The most clear evidence comes from the instruction that asks to use `boxed` format
for highlighting the answer.

| prompt                 | responses with boxed |
|------------------------|----------------------|
| zero-shot              | 31%                  |
| 3-shot temperature 1   | 74%                  |
| 3-shot temperature 0.5 | 79%                  |
| 3-shot temperature 0.1 | 80%                  |

Despite the model being clearly required to use the format in the response it ignored
it on 69% of the responses, which is wild for an assistant. When being given 3 examples
it doubles the responses with boxed, but it is still far from 100%.

Lowering the temperature also seems to force the model to follow the instructions closely.

Thus it seems pretty clear that the correct way to prompt this model is using
few-shot prompts. That might enable to get rid of naively parsing the last integer.

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
- [x] Lower temperature when using few-shot to see if it returns more boxed answers. Shuffle the input examples to induce variability.
