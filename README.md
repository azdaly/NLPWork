# NLPWork

Collecting my thoughts surrounding NLP (specifically related to the coupon project).

## Table of contents:
 * [Important repos/packages/containers](#irpc)  
 * [Helpful tutorials/blog posts/videos/slide decks](#htbpvsd)  
 * [Important concepts](#ic)  
 * [Questions I would like to have answered](#qiwltha)   
 * [Publications worth reading](#pwr)   

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
- [Discussion of Hugging Face papers](https://github.com/huggingface/awesome-papers)
- [Distilbert blog post](https://medium.com/huggingface/distilbert-8cf3380435b5)
- [Understanding emojis](https://medium.com/huggingface/understanding-emotions-from-keras-to-pytorch-3ccb61d5a983)
- [Training models on GPUs](https://medium.com/huggingface/training-larger-batches-practical-tips-on-1-gpu-multi-gpu-distributed-setups-ec88c3e51255)
- [Tokenizer summary](https://huggingface.co/transformers/master/tokenizer_summary.html)
- [Jay Alammar blog](http://jalammar.github.io/) - incredibly helpful blog visualizing many key concepts of NLP and MLMs. 
- [Approachable introduction to BERT](https://yashuseth.blog/2019/06/12/bert-explained-faqs-understand-bert-working/)

<a name="ic"/>

## Important concepts:


#### Deciding which NLP problem I'm facing:  

The problem I'm primarily facing is one of [Named Entity Recognition](https://en.wikipedia.org/wiki/Named-entity_recognition), where I need to determine the part of speech of noisy coupon descriptions. Likely because of the fact that these are not complete sentences, basic [ner functionality](https://huggingface.co/transformers/usage.html#named-entity-recognition) has not been successful. For this reason, I'm likely going to have to fine-tune it myself using [run_ner.py](https://github.com/huggingface/transformers/blob/master/examples/token-classification/run_ner.py). Using [pipelines](https://huggingface.co/transformers/main_classes/pipelines.html) may also be successful.  

An alternative to this would be to use [sentence-level embeddings](https://arxiv.org/abs/1908.10084) instead that may be better at classifying/clustering different coupon concepts. E.g. batch-bin coupons using the top ~100 words and use those to fine-tune the model.

#### Deciding on the tokenizer:   

Starting with the [tokenizer](https://huggingface.co/transformers/main_classes/tokenizer.html) to see if we can successfully split up the comments into digestible chunks.   

#### Deciding on the down-stream model to use:

Interestingly [this paper](https://arxiv.org/abs/1907.11692) found that BERT was *under*trained, and that training it up a bit more (thus resulting in [RoBERTa](https://huggingface.co/transformers/model_doc/roberta.html)) got great results. Consider using that instead of BERT.
  
#### Sentence-level embedding:  

 * [Sentence-BERT](https://github.com/UKPLab/sentence-transformers) - A method of generating sentence embeddings in which sentences with similar meaning will be close together in high-dimensional space.  
 * [Simply using CLS tags is remarkably effective.](https://github.com/huggingface/transformers/issues/1950#issuecomment-558770861). Specifically [this](https://arxiv.org/pdf/1810.04805.pdf) paper says how the token representations can be used for token-level tasks such as question-answering and sentence tagging, whereas the CLS tag can be used for things like classification.
 * [bert-as-service](https://github.com/hanxiao/bert-as-service) - A far more popular (stars-wise) method of sentence-level embeddings than sentence Bert.

<a name="qiwltha"/>

## Questions I would like to have answered:  
  
* When following [this](https://huggingface.co/blog/how-to-train) tutorial, why does this work:  
      ```RobertaTokenizer.from_pretrained(./dir_with_tokenizer_model)```  
      but this doesn't:  
      ```DistilBertTokenizer.from_pretrained(./dir_with_tokenizer_model)```   
      Using DistilBertTokenizer errors out saying that the tokenizer is not a part of the models on HuggingFace, and it requires a vocab.txt file, though the work in the tutorial only generates the vocab.json and merges.txt file (helpfully explained [here](https://github.com/huggingface/transformers/issues/1083#issuecomment-524303077)).
* What's the difference between [this](https://github.com/huggingface/transformers/blob/master/notebooks/01-training-tokenizers.ipynb) tokenizer initialization and [this one?](https://huggingface.co/blog/how-to-train)?  
      - Looking at the ByteLevelBPETokenizer class, it becomes apparent that all of the items explicitly stated [here](https://github.com/huggingface/transformers/blob/master/notebooks/01-training-tokenizers.ipynb) are simply under the hood [here](https://huggingface.co/blog/how-to-train) when initializing ByteLevelBPETokenizer with a couple extra flags.

<a name="pwr"/>

## Publications worth reading:

 * [Black sheep paper](https://dl.acm.org/doi/abs/10.1145/2509558.2509563?casa_token=xByjqpBg-PQAAAAA%3AnQlfSI4-OdkAvaD9r8kDz4ZMunYV1lfxE2d4-Or22zJZrOEZ6rwXPv3tlBdfFZ5K84S8OjGhSrhxcA) - Paper discussing reporting bias, in which we don't talk about the obvious, thus preventing models from learning basic facts (e.g. sheep are generally white). Work (e.g. [ERNIE publication](https://arxiv.org/pdf/1905.07129.pdf)) has been done to solve this problem. Multi-models (including images, other media) can also correct this.
 * [Byte Pair Encoding Tokenizer](https://arxiv.org/pdf/1508.07909.pdf)
