# Modeling

## Select modeling technique

<!---Document the actual modeling technique that is to be used. If multiple
techniques are applied, perform this task separately for each technique.
Many modeling techniques make specific assumptions about the data—for example,
that all attributes have uniform distributions, no missing values allowed,
class attribute must be symbolic, etc. Record any such assumptions made. --->

https://www.kaggle.com/code/nayjest/gigabenchmark-llm-accuracy-math-problems

### Available models

- Mistral and Mixtral
- Gemma
- Llama 2
- [Code llama](https://huggingface.co/blog/codellama), built on top of Llama 2.
- [DeepSeek Math](https://github.com/deepseek-ai/DeepSeek-Math)
- WizardMath-70B

## Generate experimentation design

<!---Describe the intended plan for training, testing, and evaluating the models.
A primary component of the plan is determining how to divide the available dataset
into training, test, and validation datasets.

Doing a plot of score vs train size could be helpful to decide the validation strategy

Depending on the size of the data we have to decide how we are going to use submissions.
The less the submissions the most confidence we can have on the score. However sometimes
the data distribution is very different, or the size of the data is small and we have
to make a lot of submissions. Sometimes is not easy to have a good correlation between
validation score and LB score
--->
