# Iteration n. Iteration_title

_13/06/2024_

## Goal

Can I improve the LB score by changing parameters such as temperature, top_p or output tokens?

## Motivation

There might be room for improvement by changing the inference parameters.

## Development

## Results

### Output tokens

On some previous experiments it seemed that using a maximum number of output tokens of 640 could
be enough to solve the problems. Now that using VLLM I can do more repetitions I want to revisit
that.

| Output tokens | runtime (min)  | Accuracy maj | Accuracy pass |
|---------------|----------------|--------------|---------------|
| 640           | 463            | 59%          | 87%           |
| 896           | 604            | 62%          | 90%           |
| 1024          | 650            | 61%          | 91%           |

### Temperature and top_p

How does temperature affect to validation accuracy?

## Conclusion

## Next steps

## TODO

- [ ]
