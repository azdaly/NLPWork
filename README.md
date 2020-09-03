# NLPWork

Collecting my thoughts surrounding NLP (specifically related to the coupon project).

## Table of contents:
 * [Important repos/packages/containers](#irpc)  
 * [Helpful tutorials/blog posts/videos/slide decks](#htbpvsd)  
 * [Important concepts](#ic)  
 * [Questions I would like to have answered](#qiwltha)   

<a name="irpc"/>

## Important repos/packages/containers:

- [Hugging Face](https://github.com/huggingface), obviously
- [Oscar](https://oscar-corpus.com/) - massive text dump
- [Sentence-level transformers](https://github.com/UKPLab/sentence-transformers)

<a name="htbpvsd"/>

## Helpful tutorials/blog posts/videos/slide decks:

- [Hugging Face Tutorial](https://huggingface.co/blog/how-to-train) - a helpful tutorial to get started, though it's lacking key parts, such as how to build the config files, how to integrate the new classes into the all-important run_language_modeling.py file, etc. [This](https://github.com/huggingface/transformers/issues/3192) Github issue helpfully points out many of the problems and links to [this](https://zablo.net/blog/post/training-roberta-from-scratch-the-missing-guide-polish-language-model/) far more helpful tutorial.
- [Comprehensive Hugging Face slide deck](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_50_205) - this slide deck is linked to [this](https://www.youtube.com/watch?v=rEGB7-FlPRs) video that talks broadly about transfer learning, and Hugging Face's use of it.
- [Repo A](https://github.com/keon/awesome-nlp) and [Repo B](https://nlpprogress.com/) intended to keep on track with the current advances in NLP. While these are repos, they're not software, which is why I'm putting them here.
- [Distilbert blog post](https://medium.com/huggingface/distilbert-8cf3380435b5)
- [Understanding emojis](https://medium.com/huggingface/understanding-emotions-from-keras-to-pytorch-3ccb61d5a983)

<a name="ic"/>

## Important concepts:


#### Deciding which NLP problem I'm facing:  

The problem I'm primarily facing is one of [Named Entity Recognition](https://en.wikipedia.org/wiki/Named-entity_recognition), where I need to determine the part of speech of noisy coupon descriptions. Likely because of the fact that these are not complete sentences, basic [ner functionality](https://huggingface.co/transformers/usage.html#named-entity-recognition) has not been successful. For this reason, I'm likely going to have to fine-tune it myself using [run_ner.py](https://github.com/huggingface/transformers/blob/master/examples/token-classification/run_ner.py). Using [pipelines](https://huggingface.co/transformers/main_classes/pipelines.html) may also be successful.  

An alternative to this would be to use [sentence-level embeddings](https://arxiv.org/abs/1908.10084) instead that may be better at classifying/clustering different coupon concepts. E.g. batch-bin coupons using the top ~100 words and use those to fine-tune the model.

#### Deciding on the tokenizer:   

Starting with the [tokenizer](https://huggingface.co/transformers/main_classes/tokenizer.html) to see if we can successfully split up the comments into digestible chunks.   

#### Deciding on the down-stream model to use:

Interestingly [this paper](https://arxiv.org/abs/1907.11692) found that BERT was *under*trained, and that training it up a bit more (thus resulting in [RoBERTa](https://huggingface.co/transformers/model_doc/roberta.html)) got great results. Consider using that instead of BERT.

<a name="qiwltha"/>

## Questions I would like to have answered:

- [ ] When following [this](https://huggingface.co/blog/how-to-train) tutorial, why does this work:  
      ```RobertaTokenizer.from_pretrained(./dir_with_tokenizer_model)```  
      but this doesn't:  
      ```DistilBertTokenizer.from_pretrained(./dir_with_tokenizer_model)```   
      Using DistilBertTokenizer errors out saying that the tokenizer is not a part of the models on HuggingFace, and it requires a vocab.txt file, though the work in the tutorial only generates the vocab.json and merges.txt file (helpfully explained [here](https://github.com/huggingface/transformers/issues/1083#issuecomment-524303077)).
