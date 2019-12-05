---
layout: post
title:  "Automated Health Responses Part 1"
date:   2018-08-26
comments: true
image: https://jekyllrb.com/img/octojekyll.png
categories: Natural Language Processing
---
*Code for this project can be viewed at: [Automated Health Responses Github](https://github.com/aus10powell/Automated-Health-Responses)*

## Intro

This is a proof-of-concept in generating appropriate responses to health-related questions. The general idea is that it could be part of a full-scale interaction between a healthcare professional and someone in need of healthcare. While the method of interaction (online, email, face-to-face) certainly would make a difference in how you went about any prototype, finding a reasonable source of data dictated simulating an interaction online.

## Dataset
The online forum Reddit has a sub-forum ("subreddit") called "AskDocs" where certified health professionals reply to questions by other forum members. The health professionals could be anyone from health students, nurses, to residents, to full-scale general practitioners, but had to provide evidence of their status to reddit moderators and can be identified as such.


### Key, guiding papers

* Diagnosing Disease: [A Self-Diagnosis Medical Chatbot Using Artificial Intelligence](http://matjournals.in/index.php/JoWDWD/article/view/2334/1613)
* Helped to decide on model for retrieval: [The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems](https://arxiv.org/abs/1506.08909)

## Main
