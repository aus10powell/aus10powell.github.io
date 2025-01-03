---
layout: single
title: "Twitter Account Sentiment and Text Generation"
date: 2023-02-16
comments: true
categories: NLP API
description: "A text generation and sentiment analysis of 6 Twitter Accounts"
keywords: text generation, sentiment analysis, Twitter, NLP, Transformers, HuggingFace, RESTful API
show_date: true
classes: wide
toc: true
toc_label: "Contents"
toc_icon: "book" # Optional
toc_sticky: true # Makes ToC scroll with page
---

**A text generation and sentiment analysis of 6 Twitter Accounts**

# TwitterAPI

The TwitterAPI project aims to perform text generation and sentiment analysis on six different Twitter accounts. The project utilizes NLP techniques, Transformers, and the HuggingFace library to generate tweets in the style of the selected accounts and analyze the sentiment of their tweets. Additionally, the project provides a metric for the health of the account audience and identifies anomalous tweets within the last few months. The project is deployed using FastAPI, Docker, and Gunicorn, with models hosted on HuggingFace Spaces. The code and models are stored in a GitHub repository and synced using GitHub Actions.

<div align="center">
 <img src="/assets/images/twitter_accounts/TwitterAPIScreenshot1.png"
     alt="askDocs example"
     style="width:450px;"/>
<figcaption>Screenshot of App</figcaption>
</div>

## Goal:

- Generate a Tweet in the style of one from the following Twitter Accounts ("alikarimi_ak8", "elonmusk","BarackObama","taylorlorenz","cathiedwood","ylecun"). NOTE: alikarimi_ak8 tweets often in Persian however generated tweets are in English.
- Provide Sentiment Analysis for the 6 accounts NOTE: Based on saved historical data not live data due to the uncertain nature of scraping tweets with Elon Musk acquisition.
- "Account Health" Metric:
<div align="center">
 <img src="/assets/images/twitter_accounts/obamahealthmetric.png"
     alt="askDocs example"
     style="width:350px;"/>
<figcaption>Distribution of Obama Twitter Account metric</figcaption>
</div>

- Provide a metric for the account audience health
- Anomalous tweets within the last few months:

## Twitter Accounts

_Twitter App (warning: may be blank and take a minute to update while free servers spin up) and if scraping library is being block there may be internal error_

<div style="text-center;">
    <iframe src="https://aus10powell-twitteraccounts.hf.space"
            frameborder="100"
            width="1000"
            height="1550">
    </iframe>
</div>

### Deployment

**Tech Stack**

- **Web Stack:**
  - FastAPI
  - Docker (To simply build base potentially on larger deployment)
  - Gunicorn is used to spawn the FastAPI on four child worker processes using the Asynchronous Uvicorn Worker Class. Each Uvicorn worker class runs the FastAPI app on a randomly chosen process id. The Gunicorn runs on a process id that can be configured to run on a specified port and handles the request delegation. All four instances of the FastAPI will use the same database created in the Azure Database for PostgreSQL Server. The connection to the database is established and disconnected in the startup and shutdown events of the FastAPI, respectively. The App Service deployment configuration automatically pulls and deploys any changes made to the GitHub repository it is configured with.
  - Huggingface Spaces (Free, larger-than-standard free compute and memory. Enough to save models on space without using API)
  - _Docker_ container deployment on _HuggingFace Spaces_
- **ML/DevOps:**
  - Github Actions (to sync with Huggingface Spaces)
- **Models:**
  - Persion to English: For tweets from [mt5-base-parsinlu-opus-translation_fa_en](https://huggingface.co/persiannlp/mt5-base-parsinlu-opus-translation_fa_en)
  - Sentiment Model Used: [twitter-roberta-base-sentiment](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment)
  - Generative Model Used: [OpenAI GPT2](https://huggingface.co/transformers/v4.4.2/model_doc/gpt2.html).

<!-- # Notes:
* 04/26/2023:
  * Trained 2 accounts models
  * Buit response in index.html to generate one response from those 2 accounts
  * Investigated (potentially) hosting the site on huggingface spaces
  * Investigated (potentiallu) hosting models on huggingface to pull into site
  * NOTE: Account alikarimi_ak8 was particularily tricky as most/all tweets are written in Persian for which there is few translation apis freely available. I wound up using a huggingface library and dealing with some interesting emoji issues.
* 04/27/23:
  * TODO:
    * Train the rest of account models
      * Train english models
      * Train Persian to text model
      * resolve model names based of handles
    * Create sentiment dataset for all accounts using huggingface scraper from historical data until now and display in Altair.
    * Summarization:
      * Reformate old code and eliminate unnecessary code
      * Decide on next steps as far as necessary
  * COMPLETED:
    * Created a model for each account
    * Enabled translation for the Persion account
* 05/02/23
  * COMPLETED:
    * Successfully uploaded hugginface model to hugginface model hub in order to enable api from webpage to the hosted site at huggingface avoiding storage of models on webpage.
* 05/06/23
  * COMPLETED:
    * Successfully tested a hosted app as a RESTful API endpoint for all the trained GPT2 models. Main positive take-away from this is that the file requirements
    * Learned that HuggingFace Spaces doesn't allow function call to pass through URLs with their free space...or at least it is difficult to. Using a POST request is better.
  * TODO:
    * Investigate as to whether there is a app structure that can be flexible in deployment to either Azure or Huggingface spaces

* 05/08/23
  * COMPLETED:
    * Test whether the app can be hit with a RESTful call from another hosted site...on hugginface I suppose. It seems the spaces on Huggingface on distributed and need to run on Docker if departing from the strict format they have for static.
* 05/09/23
  * COMPLETED:
    * NOTE: It became too much to try and manage Docker as well as dealing with app when working with Azure Web Services, however the switch to Huggingface for the relative great utilization of their space makes Docker make more sense. For the generall use-case of trying to update and showcase personal projects that are not going to be leaking money, Docker does seem to be the way to go. You don't need to build a ton of images locally either. Just perhaps when you're trouble-shooting a Docker specific issue.
* 05/10/23
  * TODO:
    * Technical:
      * Having Huggingface spaces pull from the github page...or at least be automated.
    * Code within page:
      * Resolve visual issues with displaying notebook html within the page
      * Decide what should actually be displayed in the notebook
        * Sentiment analysis on the four accounts
    * Extra features:
      * Sentiment: Display a sentiment score on the generated response
      * Display a summary of the generated response. NOTE: this would fit in well with the tweet analysis over time.
      *
* 05/12/23
  * COMPLETED:
    * Somewhat justified display on Markdown page
    * Adjusted color-schemes and display of sentiments
    * Started again on summarization of tweets:
      * Reduce a long list of tweets down enough to run a deep learning summarizer on it

* 05/14/23:
  * COMPLETED:
    * Potentially tracked down one issue with the hugging face regarding why the response was not being generated.

* 05/15/23:
  * Completed index.html for returning tweets
  * added tweepy integration for returning specific tweets along with javascript callbacks.
  * TODO:
    * Reformate generate a reply...it doesn't make sense to be at the top

* 05/20/23
  * Completed refactoring of some old summarization and examples.ipynb code
  * Verified that additional information and metrics can be pulled for the tweets

* 06/01/23
  * COMPLETED:
    * Implemented sentiment score on table returned
    * Implemented Persian translation column to return if account was Persian text

* 06/02/23
  * COMPLETED:
    * Initial distributions for evaluating a good "account health" metric.
    *
* 06/03/23
  * COMPLETED:
    * moved spacy embeddings load to app start
    * Fixed the issue of reply not being generated

* 06/05/23
  * COMPLETED:
    * Dive deeper into thinking/justification for metrics
      * Conveneniece (don't have to look at audience tweets)
      * Normalized for different accounts to enable direct comparison
  * METRICS:
    * Account Health Metric:
      * "positives" * "likes" / account_subs:
        * Normalized to compare different "health" for different accunts
        * Reasonable metric for how engaged audience is with tweets that are positive messaging. May speak more to th
        * The logged distribution is surprisingly normal for the different accounts
    * Audience Health Metric:
      -->
