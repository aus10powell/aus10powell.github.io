---
layout: splash
title:  "Automated Health Responses"
date:   2018-08-26
comments: true
#image: /assets/images/automated_health_responses/
categories: Natural-Language-Processing AI Chatbotg Machine-Learning
---
 
*This is a proof-of-concept for generating appropriate responses to health-related questions.*


*Code for this project can be viewed at: [Automated Health Responses](https://github.com/aus10powell/Automated-Health-Responses)*

## Intro

The goal of this project is to demonstrate a proof-of-concept for generating appropriate responses to health-related questions. The idea is to understand what it would take to create a full-scale interaction between a healthcare professional and someone in need of healthcare. While the medium of interaction, whether online, email, or face-to-face, would certainly affect the approach for any full-scale prototype, having a minimal viable product to showcase the approach is crucial.

This is a bootstrapped initiative, focusing on what can be safely shared with the audience without exposing any patient data. The envisioned AI system would interact with the user in a way that is relative and complementary to a doctor's expertise, never having the final say. However, this is a highly complex and layered problem, and reducing it to a simpler problem is a crucial step. For instance, given a statement or query about someone's health, what would be an appropriate response from a clinician?

This problem is only one step in the direction of a comprehensive system that can be integrated with the likes of Google voice or Alexa, once they determine that the user is talking about their health. The aim of this project is to lay the groundwork for such a system, exploring the possibilities of generating appropriate responses to health-related queries.

#### General approaches to machine generated conversational responses
Although it seems like most developed solutions are a little mix-and-match, these categories are generally how most people would bucket at chatbot approach. Researching these was particularly helpful in characterizing my understanding.

* <u>Rule-base:</u> This is along the lines of: given a serious question about heart attack. Tell them to call 911. Not robust. Hard to maintain. Etc...

* <u>Generative:</u> Also called auto-encounters and basically the way an auto-translate service works. Given a sequence of characters or tokens. Predict the following sequence of tokens or characters. Not the best choice for this project largely because although some amazing advances have been made. It is very much to random especially in a medical context with often sparsely used words.
* <u>Selective:</u> There are many different approaches here. But generally speaking,  so far it the most most robust and time tested. Basically you want to select the best response (or best set of response) using a classified of sorts (more on that later) from a bank of potential responses.

While the choice of a rule-based and generative approach may have seemed appropriate initially, it is important to note that this type of model can be limited in its ability to capture the nuances of natural language and human conversation. In particular, a rule-based approach may struggle to handle the complex and varied language used in clinical settings, which can include medical jargon, colloquialisms, and other forms of domain-specific language.

Additionally, while giving clinicians control over the response selection process may seem beneficial, it can also introduce bias into the system and limit the diversity of responses generated. This is especially important in the context of healthcare, where a diverse range of perspectives and approaches may be necessary to provide effective care to patients.

This led to the well-known paper *The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems* [(here)](https://arxiv.org/pdf/1506.08909.pdf) which introduces Ubuntu data to model appropriate responses to technical questions on a public forum. Coincidentally, the dataset that I had chosen was also based on public forum data, Reddit's AskDocs Forum [(here)](https://www.reddit.com/r/AskDocs/).

In the context of clinical conversations, a seq-to-seq model can be trained to map a sequence of input utterances from the patient to a sequence of output utterances from the clinician. This type of model can capture the context and flow of the conversation, as well as the nuances of language and domain-specific terminology that are unique to clinical settings.

Furthermore, a seq-to-seq model can incorporate attention mechanisms that allow the model to focus on specific parts of the input sequence when generating the output sequence. This can be particularly useful in clinical conversations, where certain aspects of the patient's history or symptoms may be more important than others.

## Dataset Description
It took some exploring, but I found a suitable, health-centric, conversational dataset in Reddit. There is a sub-forum ("subreddit") called "AskDocs" where certified health professionals reply to questions by other forum members. The health professionals could be anyone from health students, nurses, to residents, to full-scale general practitioners, but had to provide evidence of their status to reddit moderators and can be identified as such. The data is updated and stored in [Google's BigQuery](https://cloud.google.com/bigquery/public-data/), however if you wish to download the data I used you can do directly at [this link](https://storage.googleapis.com/health-conversations.appspot.com/2014_2017_askDocs.gz).

#### Formatting data and cleaning
In order to model forum data the form of a query and response, the authors of the Ubuntu paper had to estimate (using a time window) whether a new post was in direct response to a previous post. With the Reddit data, the same approach certainly could have been applied. However, in Reddit, it is explicit as to whether a new post under a thread (an ongoing conversation concerning a topic started by the original post) is in direct response to the original post or in response to another comment. Also, per the paper's recommendation, only threads with at least 3 posts were retained in order to provide context. The lower-cased form of all text was used along with standard tokenization using Keras. In total this generated 955,610 samples of unique 282,433 words which was split into train/test/validate 80/10/10 respectively:

<figure>
<div align="center">
 <img src="/assets/images/automated_health_responses/askDocs.png"
     alt="askDocs example"
     style="width:650px;"/>
<figcaption>Example start of thread</figcaption>
</div>
</figure>

A key way of measuring how dynamic a conversation is for a thread is counting the number of turns in a conversation (or thread). Turns refer to the switching between speakers. This is follows the assumption for human-like chatbots that conversation partners take turns in a conversation (or thread). Given that most of the posts in AskDocs only generate around 4-5 posts it is a safe assumption to say that all posts following that initial post are generally on the same topic. (great Medium post [here](https://chatbotsjournal.com/designing-for-conversational-ui-humanizing-chatbots-f199e59b363e) on humanizing your chatbot)

<figure>
<div align="center">
 <img src="{{ site.url }}{{ site.baseurl }}/assets/images/automated_health_responses/turns_per_thread.png"
      alt="turns per thread"
      style="float: center boarder:5"
      style="width:700px;" />
<figcaption> Distribution of number of turns per AskDocs Forum thread</figcaption>
</div>
</figure>

## The Model

*To briefly summarize what we're modeling: For a given query (i.e. question), can we make a binary selection from a list of possible answers saying if the answer is appropriate.*


I started with code provided in [this excellent blog: Implementation of dual encoder using Keras](https://basmaboussaha.wordpress.com/2017/10/18/implementation-of-dual-encoder-using-keras/), updating some of the code for my needs. I recommend reading the blog and paper it is based on. Although the model can train embeddings as it goes along, both the 6B token and 840B token Glove embeddings were tested with substantial improvements made with the 840B tokens. Embeddings built on all 2015 reddit comments were also tested but with no decrease in loss.

<figure>
<div align="center">
 <img src="/assets/images/automated_health_responses/dual_encoder_model_architecture.png"
     alt="turns per thread"
     style="float:left;width:42px;"
     style="width:650px;" border="5"/>
<figcaption> Architecture</figcaption>
</div>
</figure>

The key structural advantage of this model is information is mapped in pairs. In Keras this is defined as a sequential model then embedding layer which is initialized with the GLoVe embeddings. I chose to allow these embeddings to be trained further during training process.

### Results
<figure>
<div align="center">
 <img src="/assets/images/automated_health_responses/model_scores1.png"
     alt="turns per thread"
     style="float:left;width:42px;"
     style="width:650px;" border="5"/>
<figcaption> turns per thread</figcaption>
</div>
</figure>


### Conclusion
This project was largely attempting to duplicate the original Ubuntu Dual Encoder paper for health data. Comparison of base metrics were quit similar to original paper with minimal effort in tuning model and adjusting parsing of data. One key difference in this implementation of that paper was the omission of comments previous to a given query to give context in selecting response. The results from these data however are promising and suggest a worthwhile effort in creating a more satisfying and health-centric responses. If successful, the application of this technology could potentially revolutionize the healthcare industry by providing accessible and accurate responses to health-related queries in real-time. However, the approach is highly dependent on the quality of the dataset used, and further research is needed to test the generalizability of the model on other datasets.

### Papers

* Diagnosing Disease: [A Self-Diagnosis Medical Chatbot Using Artificial Intelligence](http://matjournals.in/index.php/JoWDWD/article/view/2334/1613)
* Helped to decide on model for retrieval: [The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems](https://arxiv.org/abs/1506.08909)

##### Dataset creation
* There are a few changes to how the data was manipulated that might train a model for an appropriate response. For example the model currently is train on a response to every query so there can be multiple responses to the same query. Using something like the number of upvotes, one response could be selected (at least for the initial query).
* Conversation history in the thread could be include in the encoder portion of the model. This would potentially help the correct results so that we would be able to select the most relevant response given the history as opposed to a technically correct, but non-sensical result like the one below.


<figure>
<div align="center">
 <img src="/assets/images/automated_health_responses/answer_selection.png"
     alt="askDocs example"
     style="float:left;width:42px;"
     style="width:500px;" border="5"/>
<figcaption> Answer Selection</figcaption>
</div>
</figure>



#### Refinement of "Health" purposes
Most of this work was towards creating an initial viable solution in human-like responses to a health-related statement or question. One way of refining the types of responses would be to determine what type of statement/questions started the conversation and score possible answers only within that concept space.
