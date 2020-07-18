# NLPWork

Collecting my thoughts surrounding NLP (specifically related to the coupon project).

## Important Repos/Packages/Containers:

- [Hugging Face](https://github.com/huggingface), obviously
- [Oscar](https://oscar-corpus.com/) - massive text dump
- [Sentence-level transformers](https://github.com/UKPLab/sentence-transformers)

## Helpful tutorials:

**Tutorials I've tried:**

**Tutorials I haven't tried:**

- [Hugging Face Tutorial](https://huggingface.co/blog/how-to-train)

## Important concepts:


#### Deciding which NLP problem I'm facing:  

The problem I'm primarily facing is one of [Named Entity Recognition](https://en.wikipedia.org/wiki/Named-entity_recognition), where I need to determine the part of speech of noisy coupon descriptions. Likely because of the fact that these are not complete sentences, basic [ner functionality](https://huggingface.co/transformers/usage.html#named-entity-recognition) has not been successful. For this reason, I'm likely going to have to fine-tune it myself using [run_ner.py](https://github.com/huggingface/transformers/blob/master/examples/token-classification/run_ner.py). Using [pipelines](https://huggingface.co/transformers/main_classes/pipelines.html) may also be successful.  

An alternative to this would be to use [sentence-level embeddings](https://arxiv.org/abs/1908.10084) instead that may be better at classifying/clustering different coupon concepts. E.g. batch-bin coupons using the top ~100 words and use those to fine-tune the model.

#### Deciding on the tokenizer:   

Starting with the [tokenizer](https://huggingface.co/transformers/main_classes/tokenizer.html) to see if we can successfully split up the comments into digestible chunks.   

#### Deciding on the down-stream model to use:

Interestingly [this paper](https://arxiv.org/abs/1907.11692) found that BERT was *under*trained, and that training it up a bit more (thus resulting in [RoBERTa](https://huggingface.co/transformers/model_doc/roberta.html)) got great results. Consider using that instead of BERT.
