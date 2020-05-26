---
layout: post
title:  "Automated Health Responses"
date:   2018-08-26
comments: true
image: ../assets/images/automated_health_responses/
categories: Natural-Language-Processing AI Chatbot Machine-Learning
---
*This is a proof-of-concept for generating appropriate responses to health-related questions.*


*Code for this project can be viewed at: [Automated Health Responses](https://github.com/aus10powell/Automated-Health-Responses)*

## Intro

This is a proof-of-concept for generating appropriate responses to health-related questions. The motivating idea is understanding what it would take to be part of a full-scale interaction between a healthcare professional and someone in need of healthcare. While the medium of interaction (online, email, face-to-face) certainly would make a difference in how you went about any full-scale prototype, it is very important to have some sort of minimal viable product to demonstrate approach.

This is very much a bootstrapped initiative: what can be safely (i.e. not patient data) shown to any audience about providing appropriate responses. Of course, the AI system people might often imagine is one that interacts with you at least in some way relative and complementary to how a doctor might. Relative, because it should have a doctor's expertise; complementary because it should never have the final word. Literally. But this a very layered and complex problem. Reducing this to simpler problem might be something like: *given statement or query about my health, what is an appropriate response from a clinician?*  This might be one step in a system some day from the likes of Google voice or Alexa after they determine you are talking about your health.

#### General approaches to machine generated conversational responses
Although it seems like most developed solutions are a little mix-and-match, these categories are generally how most people would bucket at chatbot approach. Researching these was particularly helpful in characterizing my understanding.

* <u>Rule-base:</u> This is along the lines of: given a serious question about heart attack. Tell them to call 911. Not robust. Hard to maintain. Etc...

* <u>Generative:</u> Also called auto-encounters and basically the way an auto-translate service works. Given a sequence of characters or tokens. Predict the following sequence of tokens or characters. Not the best choice for this project largely because although some amazing advances have been made. It is very much to random especially in a medical context with often sparsely used words.
* <u>Selective:</u> There are many different approaches here. But generally speaking,  so far it the most most robust and time tested. Basically you want to select the best response (or best set of response) using a classified of sorts (more on that later) from a bank of potential responses.

  This seemed like the appropriate choice. Best of the rule-based and generative approaches. Also gives clinicians the ability to exert control over response by deciding on which of the top response to select. Also, from which bank of response to choose from in the first place. This led to the well-known paper *The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems* [(here)](https://arxiv.org/pdf/1506.08909.pdf) which introduces Ubuntu data to model appropriate responses to technical questions on a public forum. Coincidentally, the dataset that I had chosen was also based on public forum data, Reddit's AskDocs Forum [(here)](https://www.reddit.com/r/AskDocs/).

## Dataset Description
It took some exploring, but I found a suitable, health-centric, conversational dataset in Reddit. There is a sub-forum ("subreddit") called "AskDocs" where certified health professionals reply to questions by other forum members. The health professionals could be anyone from health students, nurses, to residents, to full-scale general practitioners, but had to provide evidence of their status to reddit moderators and can be identified as such. The data is updated and stored in [Google's BigQuery](https://cloud.google.com/bigquery/public-data/), however if you wish to download the data I used you can do directly at [this link](https://storage.googleapis.com/health-conversations.appspot.com/2014_2017_askDocs.gz).

#### Formatting data and cleaning
In order to model forum data the form of a query and response, the authors of the Ubuntu paper had to estimate (using a time window) whether a new post was in direct response to a previous post. With the Reddit data, the same approach certainly could have been applied. However, in Reddit, it is explicit as to whether a new post under a thread (an ongoing conversation concerning a topic started by the original post) is in direct response to the original post or in response to another comment. Also, per the paper's recommendation, only threads with at least 3 posts were retained in order to provide context. The lower-cased form of all text was used along with standard tokenization using Keras. In total this generated 955,610 samples of unique 282,433 words which was split into train/test/validate 80/10/10 respectively:

<figure>
<div align="center">
<img src="{{ site.url }}{{ site.baseurl }}/assets/images/automated_health_responses/askDocs.png"
     alt="askDocs example"
     style="float:left;width:42px;"
     style="width:500px;" border="5"/>
<figcaption> Sample thread post start</figcaption>
</figure>


A key way of measuring how dynamic a conversation is for a thread is counting the number of turns in a conversation (or thread). Turns refer to the switching between speakers. This is follows the assumption for human-like chatbots that conversation partners take turns in a conversation (or thread). Given that most of the posts in AskDocs only generate around 4-5 posts it is a safe assumption to say that all posts following that initial post are generally on the same topic. (great Medium post [here](https://chatbotsjournal.com/designing-for-conversational-ui-humanizing-chatbots-f199e59b363e) on humanizing your chatbot)

<figure>
<div align="center">
 <img src="{{ site.url }}{{ site.baseurl }}/assets/images/automated_health_responses/turns_per_thread.png"
      alt="turns per thread"
      style="float: center boarder:5"
      style="width:700px;" />
<figcaption> Distribution of number of turns per AskDocs Forum thread</figcaption>
</figure>


## The Model

*To briefly summarize what we're modeling: For a given query (i.e. question), can we make a binary selection from a list of possible answers saying if the answer is appropriate.*

I started with code provided in [this excellent blog: Implementation of dual encoder using Keras](https://basmaboussaha.wordpress.com/2017/10/18/implementation-of-dual-encoder-using-keras/), updating some of the code for my needs. I recommend reading the blog and paper it is based on. Although the model can train embeddings as it goes along, both the 6B token and 840B token Glove embeddings were tested with substantial improvements made with the 840B tokens. Embeddings built on all 2015 reddit comments were also tested but with no decrease in loss.

<figure>
<div align="center">
 <img src="{{ site.url }}{{ site.baseurl }}/assets/images/automated_health_responses/dual_encoder_model_architecture.png"
      alt="turns per thread"
      style="float: center boarder:5"
      style="width:700px;" />
</figure>

The key structural advantage of this model is information is mapped in pairs.

which in Keras is defined as a sequential model then embedding layer which is initialized with the GLoVe embeddings. I chose to allow these embeddings to be trained further during training process.



### Results
<figure>
<div align="center">
 <img src="{{ site.url }}{{ site.baseurl }}/assets/images/automated_health_responses/model_scores1.png"
      alt="turns per thread"
      style="float: center "
      style="width:700px;" />
</figure>



### Conclusion
This project was largely attempting to duplicate the original Ubuntu Dual Encoder paper for health data. Comparison of base metrics were quit similar to original paper with minimal effort in tuning model and adjusting parsing of data. One key difference in this implementation of that paper was the omission of comments previous to a given query to give context in selecting response. The results from these data however are promising and suggest a worthwhile effort in creating a more satisfying and health-centric responses.

### Papers

* Diagnosing Disease: [A Self-Diagnosis Medical Chatbot Using Artificial Intelligence](http://matjournals.in/index.php/JoWDWD/article/view/2334/1613)
* Helped to decide on model for retrieval: [The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems](https://arxiv.org/abs/1506.08909)


## Future Work



##### Dataset creation
* There are a few changes to how the data was manipulated that might train a model for an appropriate response. For example the model currently is train on a response to every query so there can be multiple responses to the same query. Using something like the number of upvotes, one response could be selected (at least for the initial query).
* Conversation history in the thread could be include in the encoder portion of the model. This would potentially help the correct results so that we would be able to select the most relevant response given the history as opposed to a technically correct, but non-sensical result like the one below.
<figure>
<div align="center">
 <img src="{{ site.url }}{{ site.baseurl }}/assets/images/automated_health_responses/answer_selection.png"
      alt="turns per thread"
      style="float: center boarder:5"
      style="width:700px;" />
</figure>

##### Refinement of "Health" purpose
Most of this work was towards creating an initial viable solution in human-like responses to a health-related statement or question. One way of refining the types of responses would be to determine what type of statement/questions started the conversation and score possible answers only within that concept space.
