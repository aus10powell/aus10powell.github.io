---
layout: single
title:  "Word Embedding Comparisons for Disease Name Entity Recognition"
date:   2018-10-31
comments: true
# image: /assets/images/poizon_plants/poizon_plants_app.jpg
categories: General
description: "An overview of out-of-box benefits evaluated on open-source health dataset"
keywords: Tensorflow, NLP, Healthcare
---

Named Entity Recognition (NER) is a crucial task in natural language processing, particularly in the field of biomedical research. With the rise of ELMo embeddings, I was curious to see how they stacked up against other popular word embedding techniques for a DNER task. Accurate identification and extraction of disease entities from medical texts is necessary for several applications, such as clinical decision support systems, drug discovery, and epidemiological studies. It can help researchers and healthcare professionals quickly identify relevant information from a vast amount of medical literature and electronic health records, leading to better patient outcomes and more efficient medical research. In this quick comparison, I explore the performance of different word embedding techniques for the DNER task, with a focus on the much-touted ELMo embeddings.

The motivation for comparing word embeddings for Named Entity Recognition (NER) with diseases and adverse conditions stems from the recent popularity of ELMo embeddings in health-related natural language processing tasks. ELMo embeddings have shown promising results in capturing context-specific information and could potentially enhance the performance of NER models in the biomedical domain. Therefore, I aimed to investigate the suitability of ELMo embeddings alongside other popular techniques, such as word2vec, GloVe, and fastText, for DNER tasks.

ELMo embeddings, developed by researchers at Allen Institute for AI, are a breakthrough in the field of natural language processing. These embeddings are unique because they are contextualized: they capture different shades of meaning of a word based on its surrounding context. This is a significant improvement over traditional word embeddings, which treat each word as a static entity independent of its context. The ELMo model is based on a deep, bi-directional language model that learns to predict the next word in a sentence given both its preceding and following words. By doing so, it captures a rich representation of the word's meaning, informed by both its syntactic and semantic context. The resulting embeddings are highly effective in a wide range of natural language processing tasks, including named entity recognition, sentiment analysis, and question answering.

I compared different word embedding techniques for Disease Named Entity Recognition (DNER) task. I focused on three popular methods, i.e., word2vec, GloVe, and fastText, and evaluated their performance on a biomedical text corpus.

The experiments were conducted on two datasets with distinct characteristics: one consisting of clinical notes from hospital settings, and the other from biomedical literature. The datasets were chosen to reflect the diversity of text sources encountered in real-world DNER tasks. To ensure fair evaluation, I employed a rigorous cross-validation protocol and carefully selected a representative subset of the data for training, validation, and testing. The resulting benchmark allows for meaningful comparisons of the performance of different embedding techniques across different text domains.

To evaluate the performance of the different word embeddings, we used a variety of evaluation metrics, including precision, recall, and F1 score. These metrics provide a comprehensive view of the embeddings' strengths and limitations in identifying named entities in biomedical text. However, as pointed out by Rob Hyndman in his work on forecasting accuracy measures, it is important not to rely solely on these metrics and to consider other factors such as computational efficiency and interpretability when selecting a word embedding technique. Moreover, we should be cautious of overfitting to a particular dataset and ensure that the embeddings generalize well to new data. By taking a nuanced approach to evaluation, we can gain a better understanding of the capabilities and limitations of each word embedding technique and make informed decisions when selecting an appropriate method for a DNER task.

However, my study also revealed that combining different embedding techniques and incorporating domain-specific features could further improve the performance of the models. I suggested that further research is needed to explore the use of hybrid models for biomedical named entity recognition tasks.

The finding that the choice of embedding method had minimal impact on the models' performance is important, as it suggests that practitioners can use a range of embedding methods without sacrificing performance. This echoes the sentiment expressed by Rob Hyndman in his work on time series forecasting, where he argues that the choice of forecasting method is less important than other factors such as data quality and feature selection. However, it's worth noting that this finding is based on the specific datasets and evaluation metrics used in this effort. As such, practitioners should exercise caution in extrapolating these findings to other contexts and datasets.

It's clear that the choice of word embedding technique can have a significant impact on the performance of natural language processing models, especially for tasks such as DNER.

You can read in more detail here: [Word Embedding Comparison For Disease Named Entity Recognition](https://medium.com/analytics-vidhya/word-embedding-comparison-for-disease-named-entity-recognition-a99850653e1c)