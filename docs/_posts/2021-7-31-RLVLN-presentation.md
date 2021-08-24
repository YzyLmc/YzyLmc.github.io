---
layout: post
title: On-Going>>  Improving Vision-based Text Generation by Multi-modal Reinforcement Learning
excerpt: A new method to enhance the performance of language generation model for vision-language navigation by using REINFORCE with multi-modal rewards
# theme: simple

tags: [presentation]
category: presentation
---
## Table of Contents


---
## Introduction
### RL in language generation
![MLE_BLEU](/images/bleu.png)

Reinforcement Learning (__RL__) in language generation has been investigated for a long time, particularly because it's supposed to be a solution for exposure bias and different learning targets during training and testing (train with MLE, test with BLEU). Policy gradient methods have been implemented widely, while the efficiency of RL is always questioned. In general, RL method suffers from high-dimensional discrete action space, reward sparsity, and easy to be trapped in local minimum.  

![peak](/images/peak.png)

Due to above reasons, RL in language generation has been controversial. 'On the Weaknesses of Reinforcement Learning
for Neural Machine Translation' ([Choshen et al](https://arxiv.org/abs/1907.01752)) and 'Revisiting the Weaknesses of Reinforcement Learning
for Neural Machine Translation' ([Kiegeland et al](https://arxiv.org/abs/2106.08942)) are two interesting papers to read. Chosen et al argued that RL just modified the probability distribution to be more 'peaked'. The most astonishing point they found is that the improvement over the pretrained model appears even when they replaced the reward function (BLEU score, in their case) by a constant reward. Following Choshen et al, Kiegeland et al conducted further experiments and showed empirically that empirical improvements
over a strong pretrained model vanish when there is little to learn from the new feedback, which means the reason of no obvious improvement is observed from Choshen et al's experiment is that minimizing MLE and maximizing BLEU score are optimizations at same objective.

### GAN in language Generation

![GAN](/images/GAN.png)

Generative Adversarial Model (__GAN__) for language generation as well been studied broadly. The biggest challenge in implementing GAN in language generation model is that the output of the generator (language generation model) is manually 'picked' at each timestep of the decoding phase. In other words, we pick the token according to the probability distribution of the generation model's output instead of using the probability itself as the result, which prevent us from backpropagating the GAN loss through the generator (in this sense, GAN loss is similar to BLEU for they're both non-differential). seqGAN by Yu et al introduced REINFORCE with Monte-Carlo roll-out for backpropagating, and there are also non-RL GANs like CoT and FM-GAN. However, at the time of 2019, a famous paper, ['Language GANs Falling Short' by Caccia et al](https://arxiv.org/abs/1811.02549), came out. It pointed out that GAN model in language generation is flawed by proving MLE models can outperform all existing GAN models when both quality and diversity are taking into account ('Temperature Sweep'). After that, language GANs became less popular.

---
## HTML or Markdown
Reveal.js works with either. Use whatever you are more comfortable with.
---
## Works Anywhere
By creating presentations using Reveal.js and hosting them on your Jekyll Academic site you will have access to them anywhere. No need to worry about software compatibility, no need to sign in to email accounts on public machines. Simply load your website and select the presentation.
---
## More Information
Jekyll Academic includes everything that you need in order to make Reveal.js work. Copy this file and edit it to begin making your own slide deck.  
For more information about all of the options available in Reveal.js please the [Reveal.js Demo Website](https://lab.hakim.se/reveal-js/#/)
