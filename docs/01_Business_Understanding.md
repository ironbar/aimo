# Business Understanding

<!--- --->

## Challenge description

<!--- Look at the challenge description, understand the goal of the challenge
and write it here with your own words. Use images if they improve the explanation--->

> **The goal of this competition is to create algorithms and models that can solve tricky math problems written in LaTeX format.** Your participation will help to advance AI models’ mathematical reasoning skills and drive frontier knowledge.

Super interesting goal for a competition.

> The ability to reason mathematically is a critical milestone for AI. Mathematical reasoning is the foundation for solving many complex problems, from engineering marvels to intricate financial models. However, current AI capabilities are limited in this area. This competition includes 110 problems similar to an intermediate-level high school math challenge. The Gemma 7B benchmark for these problems is 3/50 on the public and private test sets.

So the task is to solve 110 problems similar to an intermediate-level high school math challenge.

> The assessment of AI models' mathematical reasoning skills faces a significant hurdle, the issue of train-test leakage. Models trained on Internet-scale datasets may inadvertently encounter test questions during training, skewing the evaluation process.
> To address this challenge, this competition uses a dataset of 110 novel math problems, created by an international team of problem solvers, recognizing the need for a transparent and fair evaluation framework. The dataset encompasses a range of difficulty levels, from simple arithmetic to algebraic thinking and geometric reasoning. This will help to strengthen the benchmarks for assessing AI models' mathematical reasoning skills, without the risk of contamination from training data

They have created new problems to address the problem of data contamination.

It is a code competition and the submission needs to run in less than 9 hours of time. So we have to
create a system that solves mathematical problems with limited hardware constraints.

> Because of the limited number of problems available, we are taking special precautions to secure the test set against probing. Among other things, during the submission period the test set will comprise only the 50 public set problems. Once the competition ends, when we rerun submissions, the test set will comprise only the 50 private set problems. You should attempt to make sure your submission will complete successfully on the 50 new private set problems. This may mean ensuring your submission is robust to unexpected inputs, or managing runtime and memory usage.

The system has to solve 50 problems in 9 hours, so that is around 10 minutes per problem.

[Alexander Gerko, competition host](https://www.kaggle.com/alexandergerko)

## Evaluation

<!--- Understand the metric used on the challenge, write it here and study
the characteristics of the metric --->

> Submissions are evaluated on the accuracy between their predicted labels and the ground-truth labels. In other words, submissions are ranked by the fraction of predicted labels that exactly match the ground-truth labels.
> In this competition, every ground-truth label is an integer between 0 and 999, inclusive.

So the model has to guess the exact answer to each problem.

> The answer to each problem is a non-negative integer, which you should report modulo 1000. If, for instance, you believe the answer to a problem is 2034, your prediction should be 34.

This is very interesting, instead of giving the answer we have to submit modulo 1000. It is likely to keep numbers within a manageable range, in this case, between 0 and 999, inclusive.

## Assess situation

<!---This task involves more detailed fact-finding about all of the resources,
constraints, assumptions, and other factors that should be considered in determining
the data analysis goal and project plan

* timeline. Is there any week where I could not work on the challenge?
* resources. Is there any other project competing for resources?
* other projects. May I have other more interesting projects in the horizon?
 --->

I already know that I can fine-tune Mixtral on my PC. But summer is coming and maybe I will need more
computing power so I will have to deal with that.

It is possible that I might have to do a project for Veridas and stop working on the challenge,
we will see.

### Restrictions

> Individual participants and Teams may use automated machine learning tool(s) (“AMLT”) (e.g., Google AutoML, H2O Driverless AI, etc.) to create a Submission, provided that the participant or Team ensures that they have an appropriate license to the AMLT such that they are able to comply with the Competition Rules. Teams may only use AI models and tools that are open source and were released prior to 23 February 2024. For example, programming languages, such as Python and Lean, and LLMs with publicly available weights, such as Llama or Gemma.

We cannot use models released after 23 February 2024 as a start point of research. We can generate
data for fine-tuning or training models.

#### Generating data with GPT4 is allowed

We can generate any dataset that we want, but it will have to be shared after the competition ends.

[Clarification about the use of ChatGPT to generate training data.](https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/493253#2760651)

#### LoRA and fine-tuning are allowed

- [LoRA is allowed?](https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/494337#2756872)
- [Is fine-tuning allowed in this competition?](https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/495158#2762854)

#### Llama 3 is not allowed

It was released after 23 February 2024, so it is not allowed.

[Is a fine-tuned model based on LLAMA3 eligible?](https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/495321#2763538)

### Speed race

> In the event of a tie, the Submission that was entered first to the Competition will be the winner. In the event a potential winner is disqualified for any reason, the Submission that received the next highest score rank will be chosen as the potential winner.

Although the test set is private, this competition is kind of similar to capture the flag competition
because the number of problems is small. Thus the first one to achieve a good score wins if there is a tie.

## Terminology

<!--- Sometimes the field of the challenge has specific terms, if that is the
case write them here, otherwise delete this section.--->

- [AIME](https://en.wikipedia.org/wiki/American_Invitational_Mathematics_Examination). The American Invitational Mathematics Examination (AIME) is a selective and prestigious 15-question 3-hour test given since 1983 to those who rank in the top 5% on the AMC 12 high school mathematics examination (formerly known as the AHSME), and starting in 2010, those who rank in the top 2.5% on the AMC 10.
- [AMC](https://en.wikipedia.org/wiki/American_Mathematics_Competitions). The American Mathematics Competitions (AMC) are the first of a series of competitions in secondary school mathematics that determine the United States of America's team for the International Mathematical Olympiad (IMO). AMC 12, for students under the age of 19.5 and in grades 12 and below.
- [Common Crawl](https://commoncrawl.org/) Common Crawl is a nonprofit 501 organization that crawls the web and freely provides its archives and datasets to the public. Common Crawl's web archive consists of petabytes of data collected since 2008. It completes crawls generally every month.
- [program-of-though (PoT)](https://arxiv.org/abs/2211.12588). In PoT the computation can be delegated to a program interpreter, thus decoupling complex computation from reasoning and language understanding.
- [chain-of-though (CoT)](https://www.promptingguide.ai/techniques/cot) prompting enables complex reasoning capabilities through intermediate reasoning steps. You can combine it with few-shot prompting to get better results on more complex tasks that require reasoning before responding.
- [tool-integrated reasoning](https://arxiv.org/abs/2309.17452) We propose ToRA a series of Tool-integrated Reasoning Agents designed to solve challenging mathematical problems by seamlessly integrating natural language reasoning with the utilization of external tools (e.g., computation libraries and symbolic solvers), thereby amalgamating the analytical prowess of language and the computational efficiency of tools. To train ToRA, we curate interactive tool-use trajectories on mathematical datasets, apply imitation learning on the annotations, and propose output space shaping to further refine models' reasoning behavior.
- [speculative decoding](https://medium.com/@TitanML/in-the-fast-lane-speculative-decoding-10x-larger-model-no-extra-cost-f33ea39d065a) It is a method to accelerate
  inference by combining a fast and a slow model.
- [MATH Dataset](https://arxiv.org/abs/2103.03874) a new dataset of 12,500 challenging competition mathematics problems. Each problem in MATH has a full step-by-step solution which can be used to teach models to generate answer derivations and explanations. The MATH dataset consists of problems from mathematics competitions including the
AMC 10, AMC 12, AIME, and more. Unlike most prior work, most problems in MATH cannot be solved with a straightforward application of standard K-12 mathematics tools. Instead, humans often solve such problem by applying problem solving techniques and “heuristics”
- [K-12 mathematics tool]
- [GSM8k dataset](https://huggingface.co/datasets/gsm8k) a dataset of middle-school level math word problems.
- [Self-Consistency](https://learnprompting.org/docs/intermediate/self_consistency) Self-consistency1 is an approach that simply asks a model the same prompt multiple times and takes the majority result as the final answer. It is a follow up to CoT prompting, and is more powerful when used in conjunction with it.
- [SymPy](https://docs.sympy.org/latest/index.html) is a Python library for symbolic mathematics. It can
  be used for example to [solve equations](https://docs.sympy.org/latest/guides/solving/index.html).
- **Few-shot prompting**. Create a prompt with a few examples of how to solve the task.
- [OpenAI Codex](https://openai.com/blog/openai-codex) AI system that translates natural language to code.
- [Generated Knowledge Prompting](https://www.promptingguide.ai/techniques/knowledge) Use the LLM to generate
  knowledge before making a prediction. This could be useful to recall some equations that might be
  relevant to solve the problem. I might have an specialized model for this task.
- [Isabelle](https://isabelle.in.tum.de/) Isabelle is a generic proof assistant. It allows mathematical formulas to be expressed in a formal language and provides tools for proving those formulas in a logical calculus.

## Questions

<!--- Write here any question that arises when reading about the challenge --->

## Project Plan

<!--- Write initial ideas for the project. This is just initial thoughts,
during the challenge I will have a better understanding of the project and
with better information I could decide other actions not considered here.--->

On a first step I need to read about the state of the art. I need more information to create
a plan for the challenge.

### Initial ideas

- Tool use. Calculator. LLMs ar not good at arithmetics.
- GPT4 with chain of thought to generate training data
- https://deepmind.google/discover/blog/alphageometry-an-olympiad-level-ai-system-for-geometry/
- https://alphacode.deepmind.com/
- In this competition the key is probably the data and how to use the data (loss function)
- ORCA paper
- Output python code could be a good way to avoid using calculators. Can ChatGPT solve more problems with that setup?
- I believe there was some model specialized on latex
- Chain of though, tree of thought, speculative decoding are some techniques that might help
- On AlphaCode there is a cheap way to filter bad solutions, and they can make 10 submits. Here I need
  to create the highest quality possible solution. Maybe I need a judge to score the candidate solutions.
  Judging might be easier than generating. Self-rewarding LLMs.
- A good validation set is needed
- The tokenizer might be relevant to have a good representation of the problem
- Inference speed will be relevant, a team capable of doing 20 predictions will beat another team doing 10 predictions.
- What if we search for similar problems in our dataset for few-shot prompting?
