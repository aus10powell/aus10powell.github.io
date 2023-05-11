---
layout: single
title:  "Twitter Account Sentiment and Text Generation"
date:   2023-11-16
comments: true
# image: /assets/images/poizon_plants/poizon_plants_app.jpg
categories: NLP API
description: "A text generation and sentiment analysis of 6 Twitter Accounts"
keywords: text generation, sentiment analysis, Twitter, NLP, Transformers, HuggingFace, RESTful API
show_date: true
words_per_minute: 300
---

**A text generation and sentiment analysis of 6 Twitter Accounts**


*Twitter App (warning: may be blank and take a minute to update while free servers spin up)*
<iframe
	src="https://aus10powell-twitteraccounts.hf.space"
	frameborder="0"
	width="850"
	height="650"
></iframe>


# Notes:
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