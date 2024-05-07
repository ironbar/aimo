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

| prompt    | temperature | responses with boxed |
|-----------|-------------|----------------------|
| zero-shot | 1           | 31%                  |
| 3-shot    | 1           | 74%                  |
| 3-shot    | 0.5         | 79%                  |
| 3-shot    | 0.1         | 80%                  |

Despite the model being clearly required to use the format in the response it ignored
it on 69% of the responses, which is wild for an assistant. When being given 3 examples
it doubles the responses with boxed, but it is still far from 100%.

Lowering the temperature also seems to force the model to follow the instructions closely.

Thus it seems pretty clear that the correct way to prompt this model is using
few-shot prompts. That might enable to get rid of naively parsing the last integer.

### Single problem optimization: Problem 1

I have downloaded the notebook to my PC and it is running at around 30 token/s. I'm thinking of doing
a single problem optimization. Focus on a specific problem and run the solution search multiple times
maximizing the probability of getting the correct answers. Each run could take a few minutes so
the optimization speed would be nice.

The goal is to write python code that solves the problem.

1. Initial attempts with few-shot prompt from DeepSeekMath repo cannot solve the problem
2. If I add the solution as a few-shot prompt it is able to solve the problems, but it forgets to
   simplify the result many times.
3. I can automate the simplification in the print, and that leads to perfect answers. It returns
   the correct answer 5 out of 5 runs.
4. If I try the baseline few-shot prompt with automatic simplification the problem is not solved anytime
   despite trying with different temperatures.
5. If I ask GPT4 to create a similar problem, it reaches perfect solution. This suggests that if I give
   similar problems in the few-shot prompt I could boost the score. That also works with humans, if we
   are shown sample problems or sample code solutions that is very helpful for solving the problem.

It is worth saying that among all the experiments the model was able to reach the correct answer twice
without using code. It wasn't able to do the same with code unless receiving a very similar problem in
the few-shot prompt.

### Cheating to overfit on train set

I have solved all the train set problems. Now I'm going to create a few shot prompt with random solutions
from the train set. That is cheating, because the solution is on the prompt, but it is worth trying.

The outcome is the expected, the system is able to reach the correct answer for all the problems.

I'm going to use this few-shot prompt to make submissions.

### Number of repetitions

Self-consistency is a technique that makes multiple predictions for the same problem and returns the
most frequent answer. Intuition says that the higher the number of predictions the most likely the returned
answer will be correct.

| repetitions | LB score |
|-------------|----------|
| 4           | 15       |
| 8           | 20       |
| 12          | 19       |

The results show an improvement when increasing the repetitions from 4 to 8, but not from 8 to 12.
It might be randomness or maybe we need more resolution.

### Max output tokens

| max output tokens | LB score |
|-------------------|----------|
| 512               | 20       |
| 1024              | 19       |
| 2048              | 19       |

It seems that for the problems that the system is currently solving the number of output tokens
does not need to be big.

### Temperature

TODO: table with results

## Conclusion

DeepSeekMath seems to be capable of solving the train problems if given a similar problem as context
in a few-shot prompt. I have been able to achieve perfect score by giving the exact same problems as input,
but I also have seen that givin similar problems works.

It does not follow the instructions too well, is better to give examples with few-shot prompt.

## Next steps

- I might try to replicate or even improve the results of DeepSeekMath on MATH dataset.
- Bigger context window will increase the chance of having a similar problem in the prompt
- A good embedding model will also increase the likelihood of solving the problem, because more relevant
  problems will be given as context.
- Could I verify the answers to the problems? Instead of relying on self-consistency.
- Optimizing the inference speed will be very helpful.

## TODO

- [ ] Problems when generating loops. https://huggingface.co/docs/transformers/en/main_classes/text_generation. That is `frequency_penalty` on OpenAI but on huggingface there are other options.
- [ ] Analyze deepseekmath library and define experiments
- [x] Lower temperature when using few-shot to see if it returns more boxed answers. Shuffle the input examples to induce variability.
- [x] Submission with 9 few-shot examples
- [x] Submission with 12 repetitions
- [ ] Document results
- [x] Modify the temperature in the submissions
