# NLPWork
Collecting my thoughts surrounding NLP

## Important Repos/Packages/Containers:

- [Hugging Face](https://github.com/huggingface), obviously
- [Oscar](https://oscar-corpus.com/) - massive text dump

## Helpful tutorials:

**Tutorials I've tried:**

**Tutorials I haven't tried:**

- [Hugging Face Tutorial](https://huggingface.co/blog/how-to-train)

## Important concepts:

The problem I'm primarily facing is one of [Named Entity Recognition](https://en.wikipedia.org/wiki/Named-entity_recognition), where I need to determine the part of speech of noisy coupon descriptions. Likely because of the fact that these are not complete sentences, basic [ner functionality](https://huggingface.co/transformers/usage.html#named-entity-recognition) has not been successful. For this reason, I'm likely going to have to fine-tune it myself using [run_ner.py](https://github.com/huggingface/transformers/blob/master/examples/token-classification/run_ner.py). Using [pipelines](https://huggingface.co/transformers/main_classes/pipelines.html) may also be successful.
