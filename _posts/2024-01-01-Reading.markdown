---
layout: single
title:  "2023 Technical Reading"
date:   2023-01-01
comments: true
# image: /assets/images/poizon_plants/poizon_plants_app.jpg
categories: 2023 Papers 
description: "Technical articles, research papers, etc. read in 2023"
keywords: research, ml, data-science, papers, nlp, audio, ai
show_date: true
words_per_minute: 300
---

**2023 Reading List**

* Table of Contents
{:toc}

## Audio
* [Self-supervised learning for infant cry analysis](https://arxiv.org/abs/2305.01578")
    * Self-supervised learning can be used to learn useful representations of infant cries from unlabeled data.
    * The self-supervised approach was able to achieve comparable performance to a supervised learning approach that was trained on a small amount of labeled data.
    * Self-supervised learning could be a valuable tool for developing new and improved infant cry analysis systems.
* [CryCeleb: A Speaker Verification Dataset Based on Infant Cry Sounds](https://arxiv.org/abs/2305.00969")
    * The CryCeleb dataset is a large and diverse dataset of infant cry sounds. This challenge has narrowed in on the task of distinguishing baby cries from each other.

## NLP
* [BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension](https://arxiv.org/abs/1910.13461)
    * BART is a denoising autoencoder, which means that it is trained on a dataset of corrupted text. The corruptions can be simple, such as replacing words with random words, or more complex, such as removing words or sentences. BART is trained to reconstruct the original text from the corrupted text.
    * This training procedure helps BART to learn to represent the meaning of text, even when the text is corrupted. This makes BART well-suited for natural language generation, translation, and comprehension tasks.
* [Backpack Language Models](https://arxiv.org/abs/2305.16765)
    * Backpacks is a neural architecture that combines strong modeling performance with interpretability and control. It learns multiple sense vectors for each word, representing different aspects of the word, and allows for intervention and modification of these vectors to change the model's behavior. It outperforms larger models in lexical similarity evaluations and enables controllable text generation and debiasing through sense vector manipulation.
* Date specific (might not age well) 05/25/23
    * [State of GPT (a Youtube update by Microsoft)](https://www.youtube.com/watch?v=bZQun8Y4L2A&t=518s&ab_channel=MicrosoftDeveloper)
    * [Discovering Language Model Behaviors with Model-Written Evaluations](https://arxiv.org/abs/2212.09251)
* [LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/) An OpenAI researcher's musing on RHL.
* [Prompt Receipes](https://github.com/linexjlin/GPTs) Great starting points for some specific use-cases in prompting. Some are shockingly effective.


### Large-Language Models
* [Parameter-Efficient Transfer Learning for NLP](http://proceedings.mlr.press/v97/houlsby19a/houlsby19a.pdf): using adapter modules as an efficient alternative to fine-tuning large pre-trained models in the context of numerous downstream tasks. Adapter modules introduce minimal trainable parameters per task, enabling the incorporation of new tasks without retraining the entire model. Demonstrating their effectiveness, the authors apply adapter modules to 26 text classification tasks, including the GLUE benchmark, achieving near state-of-the-art performance with only a slight increase in parameters. This approach contrasts with traditional fine-tuning, which requires training all parameters for each task, showcasing the efficiency and flexibility of adapter modules in handling diverse tasks.

* [RLHF: Reinforcement Learning from Human Feedback (A blog by Chip Huyen)](https://huyenchip.com/2023/05/02/rlhf.html)
* [StackLLaMA: A hands-on guide to train LLaMA with RLHF](https://huggingface.co/blog/stackllama): About the development of the StackLLaMA model, a reinforcement learning from human feedback (RLHF) fine-tuned LLaMA model for Stack Exchange question and answering. The model is trained using a combination of supervised fine-tuning, reward modeling, and reinforcement learning techniques. Challenges faced during training, such as balancing rewards and managing KL divergence, are highlighted, and the post emphasizes the ongoing efforts to improve RLHF methods. The StackLLaMA model demonstrates the application of RL techniques in natural language processing tasks, showcasing its potential for enhancing question-answering systems.
* [ReAct: Synergizing Reasoning and Acting in Language Models (web write-up)](https://react-lm.github.io/): a novel approach that leverages Large Language Models (LLMs) to generate both reasoning traces and task-specific actions concurrently. By using reasoning and acting, ReAct demonstrates enhanced synergy between the two, enabling the model to induce, track, and update action plans based on reasoning traces and interact effectively with external sources. The results show ReAct's effectiveness over existing methods in various language and decision-making tasks, addressing issues like hallucination and error propagation while improving human interpretability and trustworthiness.
* [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)
* [Who Wrote it and Why? Prompting Large-Language Models for Authorship Verification](https://arxiv.org/pdf/2310.08123.pdf): The text discusses the significance of Authorship Verification (AV) in natural language processing, highlighting challenges in existing techniques such as data requirements and explainability. To address these issues, the paper introduces PromptAV, a novel approach leveraging Large-Language Models for AV. PromptAV utilizes step-by-step stylometric explanation prompts, outperforming state-of-the-art methods with limited data and providing intuitive explanations for predictions. The research aims to enhance AV effectiveness and interpretability, presenting PromptAV as a promising solution in forensic analysis, plagiarism detection, and identification of deceptive content.
* [Building RAG-based LLM Applications for Production](https://www.anyscale.com/blog/a-comprehensive-guide-for-building-rag-based-llm-applications-part-1): Summary of      Retrieval Augmented Generation (RAG):

    Retrieval Augmented Generation (RAG) addresses the limitation of Large Language Models (LLMs) not being trained on specific user data. It involves incorporating user data into the LLMs' existing knowledge. In the RAG process, user data is loaded and prepared for queries, creating an index. User queries filter the data down to the most relevant context, and this context, along with the query, is sent to the LLM, which generates a response.

    Key stages within RAG include:

    * Loading: Retrieving user data from various sources and bringing it into the processing pipeline, supported by connectors like those provided by LlamaHub.
    * Indexing: Creating a data structure, often involving vector embeddings and metadata strategies, to facilitate efficient querying and retrieval of contextually relevant data.
    * Storing: Saving the indexed data and associated metadata to avoid the need for re-indexing in the future.
    * Querying: Utilizing LLMs and LlamaIndex data structures for various query strategies, such as sub-queries, multi-step queries, and hybrid approaches.
    * Evaluation: Assessing the effectiveness of the pipeline through objective measures, comparing strategies and evaluating the accuracy, fidelity, and speed of query responses.

* [Memory and MIPS (Max Inner Product Search)](https://chat.openai.com/share/46ff149e-a4c7-4dd7-a800-fc4a642ea389) Generally speaking, this deals with the concepts of having large corpus of documents that are represented in a high-dimensional space. After being given a new document, you want to find the document in your existing collection that is most similar to it. This is the maximum inner product search. The chat with GPT involves a discussion of this idea in relation to memory.

## Vision
* [YOLOv7: Trainable bag-of-freebies sets new state-of-the-art for real-time object detectors](https://arxiv.org/abs/2207.02696)
* [ByteTrack: Multi-Object Tracking by Associating Every Detection Box](https://arxiv.org/abs/2110.06864) To reduce missing detections and keep the persistence of trajectories, authors keep detection boxes and associate across every of them.
* [BoT-SORT: Robust Associations Multi-Pedestrian Tracking](https://arxiv.org/abs/2206.14651)
* [Object Detection for Dummies Part 3: R-CNN Family](https://lilianweng.github.io/posts/2017-12-31-object-recognition-part-3/) Good discussion on loss of object recognition.
* [A good overview of object Detection and Image Segmentation](https://www.oreilly.com/library/view/practical-machine-learning/9781098102357/ch04.html)
* [Noise or Signal: The role of Backgrounds in Image Classification](https://gradientscience.org/background/) Trying to determine how many backgrounds of no fish in image is appropriate. Full paper [HERE](https://arxiv.org/abs/2006.09994)

## ML (General)
* [DeepHit: A Deep Learning Approach to Survival Analysis with Competing Risks
](http://medianetlab.ee.ucla.edu/papers/AAAI_2018_DeepHit) Time-to-event analysis is widely used in economics, finance, engineering, medicine and many other areas. Previous models rely on strong parametric assumptions that are often violated. DeepHit uses a deep neural network to learn the distribution of survival times directly. Comparisons with previous models on the basis of real and synthetic datasets demonstrate that DeepHit achieves statistically significant performance improvements.

### Recommendation and Search
* [Counterfactual Evaluation for Recommendation Systems](https://eugeneyan.com/writing/counterfactual-evaluation/): the challenge of evaluating recommendation systems and suggests that they should be treated as interventional problems rather than observational ones. It explains that traditional offline evaluation methods may not capture the true impact of recommendations on user behavior. The article introduces counterfactual evaluation as an alternative approach, particularly focusing on Inverse Propensity Scoring (IPS) and its variants like Clipped IPS (CIPS) and Self-Normalized IPS (SNIPS), highlighting their advantages and limitations.
* [Improving Deep Learning For Airbnb Search](https://arxiv.org/pdf/2002.05515.pdf): Airbnb's transition to deep learning for search ranking significantly impacted its roadmap, leading to a shift in strategy. While the initial optimism about incorporating machine learning ideas from literature surveys faded due to application-specific challenges, the focus shifted towards a process-driven approach, emphasizing the importance of iterative strategies over individual techniques for enhancing deep learning models in industrial settings.

## ML Ops
* [https://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf](Rules of Machine Learning: Best Practices for ML Engineering (M. Zinkevich))
* [Continuous Adaptation for Machine (Learning)](https://blog.tensorflow.org/2021/12/continuous-adaptation-for-machine.html)
* [Model training as a CI/CD system: Part I](https://cloud.google.com/blog/topics/developers-practitioners/model-training-cicd-system-part-i)
* [Model training as a CI/CD system: Part II](https://cloud.google.com/blog/topics/developers-practitioners/model-training-cicd-system-part-ii)
* [APIs for Model Serving](https://madewithml.com/courses/mlops/api/)
* [Github Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions) This is a great place to start especially since your project likely already has a Github repository. It covers all the basics of CI/CD. It discusses the components of a workflow and how to create one. Workflows can be triggered by events such as pushes to the repository. Each workflow run is executed on a runner, which can be a virtual machine or a self-hosted server. Jobs within a workflow can run in parallel or sequentially.

    * The process of building a CI/CD system specifically for model training.
    * Key components such as data management, environment setup, model training pipeline, and version control.
    * Emphasizes the benefits of automation, highlights cloud infrastructure support, and suggests specific tools for implementing a model training CI/CD system.
* [Application deployment and testing strategies (Google Cloud)](https://cloud.google.com/solutions/application-deployment-and-testing-strategies)
    * Best Practices: 1) Backward compatibility 2) Continuous integration/continuous deployment (CI/CD) 3) Automation 4) Operating environments and configuration management. 5) Rollback strategy in case things go wrong 6) Post-deployment monitoring
* [Leveraging TensorFlow-TensorRT integration for Low latency Inference](https://blog.tensorflow.org/2021/01/leveraging-tensorflow-tensorrt-integration.html):TensorRT integration in TensorFlow allows developers to optimize and accelerate their deep learning models for deployment on GPUs. By leveraging TensorRT's optimizations, TensorFlow users can achieve faster inference times and reduced memory footprint. This integration provides a seamless workflow, enabling efficient deployment of TensorFlow models with improved performance for real-time applications.
*[Bayesian hyperparameter tuning: Nuts & bolts](https://wandb.ai/site/articles/bayesian-hyperparameter-optimization-a-primer)

## Statistical
* [Bayesian stock assessment: a review and example application using the logistic model](https://watermark.silverchair.com/55-6-1031.pdf?token=AQECAHi208BE49Ooan9kkhW_Ercy7Dm3ZL_9Cf3qfKAc485ysgAAA1swggNXBgkqhkiG9w0BBwagggNIMIIDRAIBADCCAz0GCSqGSIb3DQEHATAeBglghkgBZQMEAS4wEQQMLx9G1vXE640UVIehAgEQgIIDDuVcAcoVq_sfbFu8CGHwHlYnMN-tbQb0neED632xB-3FiQ0-kQhsE5g0NRFg8gwNFssmYzIEeO6_4MGcdwX-mJrjT7_lnDBmJ7eETkYOW97K0674mc4BoQ4cIKgknvRaj3fMPPjGe_GDkr2vp8kOrSKxN8sAvBbxqOaDLVky_fyIhdVpX5pxHkbVxl30U4iY3wUNwGl2tuBv0atdLbNbocwpTpWCiiIlm1JjSDpDkdOyvoc9qYYg7pCh_gV45jMbNAHUktEJ_0OTcqnJYcvVWsqwjnkljnplWseVUhe6IgHGzN6juC5KuuB5Jciql8WZ7QQ5V7ju0Dn5YaUqk2G9y7EjxrEwcElx7ye48ZI2PmgEoLwMOiHMfV9iaNRsA9tErunzo2O0aH5ZT3MvCQZzcthfhTcx7j-vsRFxNj2Xnvkymp36xSKmF-7xjIzq2N2QuibF9bzFeOlzW3aIXtDhjZE99EG2EQmqcggTpUFyiXftzh0hBwFHLkygWx2oUMyI0sSYt-02MYrR8G2f_FSLEtUzKTKJ-Efuth9nm-4hLOvciBQkY_SnTvHqlAXy4wENtdXalYb5GDHN_07a92wpTm6pTL4BlgZwCj4MnLMwfnfUUSrJR4L20cKNSClQqE7hy_msylSEw_zYveyN-Pp9Sh7U1RQpqy_12Bp_UIqP5IsXTjAhX3Kg2UvuMNcmIZGUvYBludcopl1LWIafj_30RBY3BjCmVFGitP-hqa_veAmPx8rq7uTmlDN8IEeWz7TqsJEOlC6Y7sehB5zeKJORfNyjtXfzO-ImwLlk6kQm6aoUSHlHHRKNns-j76Ezhx6MCZ-Yr03gBRO1bz4dImQK7Euvf3dSVOT87QLsRTNyH5pEFe94TS90348PTXluxGy4FAqndt_rxc2epL2at7bHwGD_h3jcQzlXcVyekFzdFyFL5dh8qKRD4IPK7D203hD8U4UK-XoOUalY269vFMYuaNES3oosBQ4sugYMU7yH_IpMuoIZVG6kEhDyJ7sEBKm--AD9ggUqkLkT2_TC3ll6)