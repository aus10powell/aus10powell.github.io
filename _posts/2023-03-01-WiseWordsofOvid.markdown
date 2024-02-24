---
layout: single
title:  "Wise Words of Ovid"
date:   2023-12-01
comments: true
categories: NLP LLM
description: "A bot generating memorable quotes and replies based on works of Ovid"
keywords: text generation, sentiment analysis, Twitter, NLP, Transformers, HuggingFace, RESTful API
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

## Data
* Found a vast improvement in text extraction from Ovid works using 300 dimension vs 200 dimension embeddings. This is consistent with many of the recommendation for creating RAGs.

## Quotes
\begin{equation*}
P(\text{repeated in 2 weeks}) = 1 - \left( \frac{N - 1}{N} \right)^{\frac{14}{m}}
\end{equation*}

 Substituting in the values:

 \begin{equation*}
P(\text{repeated in 2 weeks}) = 1 - \left( \frac{99}{100} \right)^{14}
\end{equation*}

 Calculating this gives:

 \begin{equation*}
P(\text{repeated in 2 weeks}) \approx 0.135
\end{equation*}

Personally, I'd like it to be under 10% for a longer period of time (increases probability)

Tweaking the numbers a bit 
N = 200
days = 21

\begin{equation*}
P(\text{repeated in 3 weeks}) \approx  0.0980
\end{equation*}


### Prompts
## Fine-Tuning Prompts
* It feels a bit like trying a new recipe while baking when you're missing measuring cups. You have instructions, general template for what to do and instinct that too much of one thing is not good but at the end of the day it's going to be trial and error. Maybe you made the recipe the best it could be, but you wouldn't know but you're following in inperfect recipe. Maybe you measured things exactly but it's still not what you want.
* Some example prompts that

### RAG Triad of Metrics
* **Context Relevance:** Ensuring the retrieved context is pertinent to the user query, utilizing LLMs for context relevance scoring.
* **Groundedness:** Separating the response into statements and verifying each against the retrieved context.
* **Answer Relevance:** Checking if the response aptly addresses the original question.

## Dual-Encoder:
<div align="center">
 <img src="/assets/images/wisewordsofovid/dual_encoder_architectures.png"
     alt="askDocs example"
     style="width:350px;"/>
<figcaption>Different architectures of Dual-Encoders (https://aclanthology.org/2022.emnlp-main.640.pdf)</figcaption>
</div> -->

