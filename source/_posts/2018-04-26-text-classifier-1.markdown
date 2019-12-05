---
layout: post
title:  "Text Classifier Part 1: CNN Classifier Using Pytorch"
date:   2018-09-01
comments: true
image: ../../../images/2018-09-01-text-classifier-part-1/cnn-image-thumbnail.png
categories: Natural Language Processing, AI, Machine Learning
---

*Estimated read time: 5 min*

## Intro

Originally I was motivated to replicate the work of researches from the 2016 paper [Hierarchical Attention Networks for Document Classification](https://www.cs.cmu.edu/~diyiy/docs/naacl16.pdf). However, after reading through the [excellent posts by Richard Liao](https://richliao.github.io/supervised/classification/2016/11/26/textclassifier-convolutional/), I decide to roughly follow his journey in order to get more familiar with Pytorch. As I have learned, Tensorflow, and by extension Keras, for multiple reasons (not necessarily with user use in mind) have many more resources available. You can read a breakdown for choosing Keras over PyTorch [Here](https://www.reddit.com/r/MachineLearning/comments/6bicfo/d_keras_vs_pytorch/). Another option if speed of implementation were a large issue would be to use the [FastAI library headed by Jeremey Howard](https://www.fast.ai/)

<br><br>

This was also an exploration into [TorchText](https://torchtext.readthedocs.io/en/latest/) which I also prefer to Keras. Similar to Keras has some useful features:
  * Data loaders
  * Batch generators
  * Easy loading of GLove and FastText embeddings
  * Easy loading of datasets (such as the IMBD ratings dataset)

There are base NN frameworks that can be used. A recursive or recurrent neural network or convolutional neural network could all be used for the exact same task.


### CNN
  Due to the different convolutions not being dependent on each other is one of the primary reasons for speedup. This frame-work is well-suited for sentence classification (however may not be the best for larger corpora) [Comparative Study of CNN and RNN for Natural Language Processing](https://arxiv.org/pdf/1702.01923.pdf). Although due to faster training and therefore faster iteration, many researchers have found performance losses are negligible.



### Loss Function:
$$L(x,y) = \sum{x_i}$$



## Dataset
From the UCI Machine Learning Repository [Here](https://archive.ics.uci.edu/ml/datasets/Drug+Review+Dataset+%28Druglib.com%29). Although the dataset has several attributes, I'll be focusing on patient reviews on specific drugs along with related conditions and their ratings. Although the ratings are ordinal, they will be treated as independent.


# Code

**Initialize TorchText Data Parameters**
<td><pre>
import spacy
import torchtext
# I recommend to use at least the medium-sized spacy embeddings
nlp = spacy.load('en_core_web_md')

def spacy_tokenizer(text): # create a tokenizer function
    """Simple tokenizer. Returns tokenized text of corpus as list."""
    return [tok.text) for tok in nlp.tokenizer(str(text))]

# Define a Field class: this is a class that contains information on how you want the data preprocessed.
TEXT = torchtext.data.Field(sequential=True,
                            tokenize=spacy_tokenizer,
                            batch_first=True,
                            # kept fix_length relatively conservative because most text is fairly short
                            fix_length=100,
                            include_lengths=True,
                            lower=True
                           )
LABEL = torchtext.data.Field(sequential=False,
                             is_target=True,
                            # use_vocab=False
                            )
</pre></td>

## Data Prep

<td><pre>
# Xavier uniform initialization is for tokens that are not seen in the corpus. This particular
# initialization enables you to have the same variance input as you do output from the word vectors.

TEXT.build_vocab(train,val,test, vectors=GloVe(name='6B', dim=300), unk_init=torch.nn.init.xavier_uniform_) # fills in uniform for unknown words
LABEL.build_vocab(train,val,test,)

batch_size = 32
train_iter, valid_iter, test_iter = torchtext.data.BucketIterator.splits(
                                                                    (train, val, test), sort_key=lambda x: len(x.text),
                                                                    batch_size=batch_size,
                                                                    sort_within_batch=True, # necessary to use in pack_pad_sequence
                                                                    shuffle=True,
                                                                    repeat = False,
                                                                    device=device)

</pre></td>


### Model






### Additional Resources/Paper References:
* [Convolutional Neural Networks (for NLP) Stanford lecture](https://www.youtube.com/watch?v=vYJtZwoO9Rw&t=0s&index=13&list=PLlJy-eBtNFt4CSVWYqscHDdP58M3zFHIG)
* [Recurrent Continuous Translation Models](https://www.aclweb.org/anthology/D13-1176)
* [A Sensitivity Analysis of (and Practitioners’ Guide to) Convolutional Neural Networks for Sentence Classification](https://arxiv.org/abs/1510.03820)
* [Neural Networks for Sentence Classification](https://arxiv.org/pdf/1510.03820.pdf)
