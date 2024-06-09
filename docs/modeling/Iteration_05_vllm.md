# Iteration 5. VLLM

_07-06-2024_

<!---
The work is done using short iterations. Each iteration needs to have a very
clear goal. This allows to gain greater knowledge of the problem on each iteration.
--->

## Goal

Can I speedup inference using [VLLM](https://github.com/vllm-project/vllm)?

## Motivation

If I can make a more efficient inference maximizing hardware utilization I might increase the number
of repetitions. If I can double the number of repetitions from 30 to 60 I may increase the accuracy by 5%.

## Development

### What is [VLLM](https://github.com/vllm-project/vllm)?

> A high-throughput and memory-efficient inference and serving engine for LLMs

It is open-source and it has an Apache-2.0 license.

> GPU: compute capability 7.0 or higher (e.g., V100, T4, RTX20xx, A100, L4, H100, etc.)

My intuition is that the highest throughput will be achieved using 2xT4, which is on that list.

One option would be to create a server and make http requests to it. This will decouple the use of GPU and
the inference logic completely, allowing to parallelize the inference completely.

Another option might be to use this class:

- https://docs.vllm.ai/en/stable/dev/engine/async_llm_engine.html
- https://github.com/vllm-project/vllm/issues/1200

### Using VLLM on Kaggle on T4 GPUs

T4 GPUs have 15360MiB according to Nvidia-smi, 3090s have 24576MiB. So that is 0.625 of the memory of
my home PC. I could use that value to simulate and experiment faster at home.

Loading model weights took 12.8725 GB

#### Quantization

- `fp8`, althought is documented it does not find that option on Kaggle, maybe there is a missmatch between versions
- `awq` -> ValueError: Cannot find the config file for awq

'awq', 'gptq', 'squeezellm'

```
# when not using quantization and just a single worker I get this error
# maybe there is a problem with the installation of vllm
top_logprobs = prompt_logprobs + output.logprobs
TypeError: unsupported operand type(s) for +: 'NoneType' and 'NoneType'
```

## Results

## Conclusion

## Next steps

- Maybe some advanced inference like speculative decoding might improve the results? I'm not sure what it is but VLLM has some parameters for that.

## TODO

- [ ] Refactor current code to make room for VLLM
