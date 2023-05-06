---
layout: single
title:  "Twitter Account Sentiment and Text Generation"
date:   2020-08-16
comments: true
# image: /assets/images/poizon_plants/poizon_plants_app.jpg
categories: NLP, API
description: "A text generation and sentiment analysis of 6 Twitter Accounts"
---

**A text generation and sentiment analysis of 6 Twitter Accounts**

<iframe
	src="https://aus10powell-test-space.hf.space"
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
    * Test whether the app can be hit with a RESTful call from another hosted site...on hugginface I suppose
    * Investigate as to whether there is a app structure that can be flexible in deployment to either Azure or Huggingface spaces
