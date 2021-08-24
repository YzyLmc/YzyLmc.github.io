---
layout: post
title: A Study of Policy Gradient Methods for Seq2Seq Model in Neural Machine Translation
excerpt: Vanilla policy gradient methods could solve issues in classical MLE training, but how effective are they?
# theme: simple

tags: [presentation]
category: presentation
---
## Table of Contents

---
## Introduction
### Seq2Seq Model
Sequence-to-sequence model is a common framework for solving sequential problems which has been widely used in NLP tasks.In seq2seq models, the input is a sequence of certain data units and the output is also a sequence of data units. Traditionally, these models are trained using a ground-truth sequence via a mechanism known as teacher forcing, where the teacher is the ground-truth sequence. However, due to some of the drawbacks of this training approach, there has been significant line of research connecting inference of these models with reinforcement learning techniques.

![seq2seq](/images/seq2seq.png)  
<!--The encoder takes a sequence of length _T_e_ inputs ,and generates the output state _H_t_. In addition, each encoder receives the previous encoder’s hidden state *h_{t-1}* to generate its current hidden state _h_t_.  
The decoder takes the last state from the encoder and starts generating an output _Y_hat_, based on the current state of the decoder _s_t_ and the last output _y_hat_T_.-->

### BLEU
BLEU (bilingual evaluation understudy) is an algorithm for evaluating the quality of text which has been machine-translated from one natural language to another.  
The formulation of BLEU has two components: the modified n-gram precision and the brevity penalty component.

![bleu](/images/bleu_intro.png)

###  Problems of Standard NMT Model
<!--![lmle](/images/lmle.png) ![lrl](/images/lrl.png)-->

__Mismatch between training objectives:__ In the training phase of standard NMT model, we minimize the cross-entropy loss between the target sentence and output sentence, which aims at maximizing the likelihood of the model to produce the target sentence conditioned on the input. However, we use BLEU as metric for evaluation. This is because BLEU is non-differentiable, so we cannot build a loss function with it and do minimization. In RL, we could solve this problem by defining a reward function and maximizing expected return based on that reward function.In this case, we don't need the rewrad function to be differentiable.

__Exposure Bias:__ During the training phase of standard NMT model, we will also use teacher forcing to deal with the large state and action space, and it means that when we are using teacher forcing the input of the decoder will be the ground truth, instead of its own output from previous timestep.<!-- To be mathematically, when we are using teacher forcing, we are minimizing:
![lce](/images/lce.png)  
and when we are not using it, we are minimizing:
![linference](/images/linf.png)-->
However, in the evaluation phase, we won't have access to the ground truth and all we have is the input sequence. This will make the training and evaluation are done on different probability distribution, and it's definitely has a negative effect to our model.

---
## REINFORCE in Seq2Seq
![reinforce](/images/reinforce.png)  
![rl_train](/images/rl_train.png)  
After converged, reinforcement learning model has 10.48 BLEU-3 score on test set, while supervised learning model has 10.23.  
![rl_sample](/images/rl_sample.png)
![sl_sample](/images/sl_sample.png)  
Sample results of both models (left: RL; right: SL) show no obvious qualitative improvement is achieved.

__Analysis:__ We can see that SL model performs slightly better during the training phase, while that is because we are using teacher forcing.  We could also see that REINFORCE does have higher variance and need more time to converge during the training. By visualizing the sample results, though we cannot directly compare the performance, it shows that the model is making sense in some ways.

---
## Actor-Critic in seq2seq
