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
The encoder takes a sequence of length _T_e_ inputs ,and generates the output state _H_t_. In addition, each encoder receives the previous encoder’s hidden state *h_{t-1}* to generate its current hidden state _h_t_.  
The decoder takes the last state from the encoder and starts generating an output _Y_hat_, based on the current state of the decoder _s_t_ and the last output _y_hat_T_.

### BLEU
BLEU (bilingual evaluation understudy) is an algorithm for evaluating the quality of text which has been machine-translated from one natural language to another.  
The formulation of BLEU has two components: the modified n-gram precision and the brevity penalty component.

![bleu](/images/bleu_intro.png)
