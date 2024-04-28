# Data Understanding

## Collect initial data

<!---Acquire the data (or access to the data) listed in the project resources.
This initial collection includes data loading, if necessary for data understanding.
For example, if you use a specific tool for data understanding, it makes perfect
sense to load your data into this tool. This effort possibly leads to initial data
preparation steps.
List the dataset(s) acquired, together with their locations, the methods used to
acquire them, and any problems encountered. Record problems encountered and any
resolutions achieved. This will aid with future replication of this project or
with the execution of similar future projects.

>	Indeed it's a pain downloading huge files. Especially when there are connection issues. I used "wget" to download the dataset with an option "-c" for resuming capability in case the download fails.  You would need to save the cookies in the page using a chrome extension Chrome Extension  save the cookies as cookies.txt from the extension  Then you can download the files by using the following command

	wget -c -x --load-cookies cookies.txt https://www.kaggle.com/c/dstl-satellite-imagery-feature-detection/data?train_wkt.csv.zip

--->

### Test data

There are 100 problems in the test set, 50 in the public and 50 in the private set.

> The answer to each problem is a non-negative integer, which you should report modulo 1000.

To receive the super prize I should aim to achieve a score of at least 94/100, current leaderboard score
is 20/50 so it might be possible.

### Train data

This is the train data, 10 hard mathematical problems. We can see that the problem description is short, in the longest case around 100 tokens.

| id     | problem                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | answer |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|
| 229ee8 | Let $k, l > 0$ be parameters. The parabola $y = kx^2 - 2kx + l$ intersects the line $y = 4$ at two points $A$ and $B$. These points are distance 6 apart. What is the sum of the squares of the distances from $A$ and $B$ to the origin?                                                                                                                                                                                                                                                                                  | 52     |
| 246d26 | Each of the three-digits numbers $111$ to $999$ is coloured blue or yellow in such a way that the sum of any two (not necessarily different) yellow numbers is equal to a blue number. What is the maximum possible number of yellow numbers there can be?                                                                                                                                                                                                                                                                 | 250    |
| 2fc4ad | Let the `sparkle` operation on positive integer $n$ consist of calculating the sum of the digits of $n$ and taking its factorial, e.g. the sparkle of 13 is $4! = 24$. A robot starts with a positive integer on a blackboard, then after each second for the rest of eternity, replaces the number on the board with its sparkle. For some `special` numbers, if they're the first number, then eventually every number that appears will be less than 6. How many such special numbers are there with at most 36 digits? | 702    |
| 430b63 | What is the minimum value of $5x^2+5y^2-8xy$ when $x$ and $y$ range over all real numbers such that $\|x-2y\| + \|y-2x\| = 40$?                                                                                                                                                                                                                                                                                                                                                                                            | 800    |
| 5277ed | There exists a unique increasing geometric sequence of five 2-digit positive integers. What is their sum?                                                                                                                                                                                                                                                                                                                                                                                                                  | 211    |
| 739bc9 | For how many positive integers $m$ does the equation $\vert \vert x-1 \vert -2 \vert=\frac{m}{100}$ have $4$ distinct solutions?                                                                                                                                                                                                                                                                                                                                                                                         | 199    |
| 82e2a0 | Suppose that we roll four 6-sided fair dice with faces numbered 1 to~6. Let $a/b$ be the probability that the highest roll is a 5, where $a$ and $b$ are relatively prime positive integers. Find $a + b$.                                                                                                                                                                                                                                                                                                                 | 185    |
| 8ee6f3 | The points $\left(x, y\right)$ satisfying $((\vert x + y \vert - 10)^2 + ( \vert x - y \vert - 10)^2)((\vert x \vert - 8)^2 + ( \vert y \vert - 8)^2) = 0$ enclose a convex polygon. What is the area of this convex polygon?                                                                                                                                                                                                                                                                                              | 320    |
| bedda4 | Let $ABCD$ be a unit square. Let $P$ be the point on $AB$ such that $\|AP\| = 1/{20}$ and let $Q$ be the point on $AD$ such that $\|AQ\| = 1/{24}$. The lines $DP$ and $BQ$ divide the square into four regions. Find the ratio between the areas of the largest region and the smallest region.                                                                                                                                                                                                                           | 480    |
| d7e9c9 | A function $f: \mathbb N \to \mathbb N$ satisfies the following two conditions for all positive integers $n$:$f(f(f(n)))=8n-7$ and $f(2n)=2f(n)+1$. Calculate $f(100)$.                                                                                                                                                                                                                                                                                                                                                    | 199    |

## External data

<!--- It is allowed in this challenge? If so write it here ideas of how to find
it and if people have already posted it on the forum describe it. --->

External data is going to be crucial in this challenge since the training data is tiny.

### AMC 12 Problems and Solutions

https://artofproblemsolving.com/wiki/index.php/AMC_12_Problems_and_Solutions

### AIME Problems and Solutions

https://artofproblemsolving.com/wiki/index.php/AIME_Problems_and_Solutions

### Other

- https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/488473
- https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/492945
- https://www.kaggle.com/datasets/pedromoya/math-problems-solved-dataset-andersonbcdefg-hf/data
- [MATH dataset](https://arxiv.org/abs/2103.03874) https://github.com/hendrycks/math
- https://github.com/kipok/nemo-skills
- https://huggingface.kxxx.link/datasets/pharaouk/math-orca-arch
- [OpenMathInstruct-1: A 1.8 Million Math Instruction Tuning Dataset](https://arxiv.org/abs/2402.10176)
- https://github.com/OpenBMB/OlympiadBench
- https://www.kaggle.com/datasets/pedromoya/math-and-python-code-datasets-hf-collection

## Describe data

<!---Describe the data that has been acquired, including the format of the data,
the quantity of data (for example, the number of records and fields in each table),
the identities of the fields, and any other surface features which have been
discovered. Evaluate whether the data acquired satisfies the relevant requirements. --->

> All problems are text-only with mathematical notation in LaTeX. Please see the `AIMO Prize - Note on Language and Notation.pdf` handout for details on the notational conventions used. Although some problems may involve geometry, diagrams are not used in any problem.

## Verify data quality

<!--- Examine the quality of the data, addressing questions such as: Is the data
complete (does it cover all the cases required)? Is it correct, or does it contain
errors and, if there are errors, how common are they? Are there missing values in
the data? If so, how are they represented, where do they occur, and how common are they? --->

Since the data is just 110 problems I assume they are all correct. The train set has been solved
manually in the [forum](https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/discussion/495265) thus I assume all the problems are correct.
