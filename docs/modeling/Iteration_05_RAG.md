# Iteration 3. Retrieval Augmented Generation

_15-05-2024_

## Goal

Can we improve the LB score by using RAG to select the most similar problems?

## Motivation

So far we have been doing few-shot prompting with random problems. I believe that if we select
similar problems we could improve the scores. We could do that using text embeddings.

## Development

### Selecting the embedding model

The [Massive Text Embedding Benchmark](https://huggingface.co/spaces/mteb/leaderboard) allows to
see the ranking of the best embedding models and to use different filters.

[gte-large-en-v1.5](https://huggingface.co/Alibaba-NLP/gte-large-en-v1.5) is a model with `apache-2.0` license
that is available on [sentence-transformers](https://huggingface.co/sentence-transformers) library.
The model is small enough to be able to run in CPU in less than 1 second.

## Results

I did a first experiment that did not show any improvement.

## Conclusion

## Next steps

## TODO

- [ ]
