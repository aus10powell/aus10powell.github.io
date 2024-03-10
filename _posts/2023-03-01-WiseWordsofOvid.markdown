---
layout: single
title:  "Wise Words of Ovid"
date:   2024-02-01
comments: true
categories: NLP LLM
description: "A bot generating memorable quotes and replies based on works of Ovid"
keywords: text generation, sentiment analysis, Twitter,X , NLP, LLM, Transformers, HuggingFace, RESTful API
show_date: true
classes: wide
---

**A wise bot retrieving quotes from antiquity**

# WiseWordsofOvid

## TBD
* Prompt-based "wisdom" responses based on sentiment using [cardiffnlp/twitter-roberta-base-sentiment](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment?text=Whoa.+CNN+is+now+reporting+that+several+Republican+voters+have+said+that+they+voted+for+Tom+Suozzi+today+because+Republicans+sabotaged+the+border+security+deal.+This+is+huge+%26+amazing.+Voters+see+right+through+Republican+nonsense+%26+they+are+making+them+find+out+big+time.). 
E.g.:
<mark> Here is why I think we’re seeing this: Time & time again, the media focuses on polls & draws conclusions about the state of the race without focusing on 1.) all Democrats have done & 2.) the real threat of Trump/MAGA extremism. But VOTERS ARE NOT DUMB! Wake up, media. /END</mark> ==>
<!-- ## Table of Contents
* Table of Contents
{:toc}

## Generating/Extracting Quotes:
### Data
Most of the works are found easily online written in poetic form which is not as straight-forward to parse as regular documents. Found a vast improvement in text extraction from Ovid works using 300 dimension vs 200 dimension embeddings. This is consistent with many of the recommendation for creating RAGs.

### Prompts
### Problem Definition
Generally, to reply to a different X tweets with a quote that strikes a neutral tone. Depending on humerous/ironc/sarcastic tone if comment is overtly negative.

### Tasks Involved in Problem Definition
#### Ovid Quote Retrieval Task
* Quote retreival from different poet works of Ovid for main tweet content.
    * Quote generation using different LLMs
        * The expected challenge of hallucinations arises here particurly when the LLM was not allowed to choose which person it was quoting
        * RAG: E.g. "What did Ovid have to say about different political parties"
    * Sentence-similarity
* Responses:
    * RAG-based:
        * Metrics:
            * **Context Relevance:** Ensuring the retrieved context is pertinent to the user query, utilizing LLMs for context relevance scoring.
            * **Groundedness:** Separating the response into statements and verifying each against the retrieved context.
            * **Answer Relevance:** Checking if the response aptly addresses the original question.
    * Political: For political determined the type of response (LLM can generate the actual text), sentiment can be used but also clustering may be useful [Clustering Sentence Embeddings to Identify Intents in Short Text](https://towardsdatascience.com/clustering-sentence-embeddings-to-identify-intents-in-short-text-48d22d3bf02e)
    * **Take-away:** RAG-based methods were better at making factual statements, e.g. "Who is Arachne?" -> "Arachne is the protagonist of a tale in Greek mythology known primarily from the version told by the Roman poet Ovid, which is the earliest extant source for the story."

#### Tweets needed: Tweet Probability of Repeated Occurrence over Time
Baseline for tweets retrieved needs to seed initial content with replacement.

$$\begin{equation*}P(\text{repeated in 2 weeks}) = 1 - \left( \frac{N - 1}{N} \right)^{\frac{14}{m}}\end{equation*}$$

 Substituting in the values:

 $$\begin{equation*} P(\text{repeated in 2 weeks}) = 1 - \left( \frac{99}{100} \right)^{14}\end{equation*}$$

 Calculating this gives:

 $$\begin{equation*} P(\text{repeated in 2 weeks}) \approx 0.135\end{equation*}$$

Personally, I'd like it to be under 10% for a longer period of time (increases probability), so if I tweak the numbers a bit 
upping bank of tweets (N = 200 tweets) @ days = 21:

$$\begin{equation*}P(\text{repeated in 3 weeks}) \approx  0.0980\end{equation*}$$

##### Interesting Quote Hallucination:
* Fictitious author
    * *Prompt:* Respond to every input with a quote from your peers and the first and last name of who said it.
    * *Input:* "all of this has happened before, all of this will happen again" (Sam Altman)
    * *Output:* The only way to deal with the void is to continue to try to fill it. - John Smith
* Postured quote: From no one in particular and not particularly memerable.
    * *Prompt:*  *Generate a response to a self-promotional tweet expressing a strong stance against politics.*
    * *Input:*  *We all come from somewhere, but we’re all Americans.*
    * *Output:* We all come from different places and backgrounds, but at the end of the day, we're all Americans. -Unknown


## Dual-Encoder:
<div align="center">
 <img src="/assets/images/wisewordsofovid/dual_encoder_architectures.png"
     alt="askDocs example"
     style="width:350px;"/>
<figcaption>Different architectures of Dual-Encoders (https://aclanthology.org/2022.emnlp-main.640.pdf)</figcaption>
</div> -->



## Infrastructure:

- Digital Ocean Droplets utilized for hosting, ensuring efficient and scalable deployment.
- Github Actions employed for Continuous Integration/Continuous Deployment (CI/CD) and workflow automation, streamlining the development pipeline.
- X API for deployment

### Machine Learning Stack:

- Leveraging Huggingface's library for Twitter Sentiment.
- Incorporating OpenAI GPT-3.5 Turbo for queries
- Langchain integrated to handle specific language-related tasks involving GPT.

### Model Training:
- Training/experimentation with natural language models on diverse datasets to enhance performance.
- Fine-tuning GPT-3.5 Turbo on domain-specific tasks, optimizing for accuracy and relevance.
