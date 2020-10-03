---
layout: post
title: "Explainable Inference"
description: "A test"
comments: true
---

This post describes the proposed approach of our IJCAI paper "Explainable Inference on Sequential Tasks via Memory-Tracking" written by Biagio La Rosa, Roberto Capobianco and Daniele Nardi.


Sequential tasks are tipically solved by recurrent network like LSTM, MANN or more recently by transformers. These networks are black boxes.

The intuition is that during the parsing of the returned answer the controller should produce states similar to the states produced during the parsing of important premises.

Note that because the controller is an LSTM network each state contains information about ALL the previous steps. This means that if the current state is similar to a state of the second premise, then all the information after that point aren't so relevant to obtain the current state. This is especially true for the T-Maze problem where all the step after the indication can be easily ignored by the archtiecture.

Note that here the content of memory is **actively** used during the inference process. While in principle a similar mechanism could be used in LSTM, in that case the similarity should be computed manually and the information of past states not used actively.

- observation 1: the memory content is actively used during the inference process. The output depends on both the last controller state **and** the memory content
- observation 2: We expect that states produced during the parsing of premises are more similar to states produced during the chosen ending than ones of the other ending.
- observation 3: Each state in LSTM contains information from all the previous steps. But because it is not a bidirectional then it doesn't contain any information about the next steps.
  - This means that if my current state is similar to the state produced at step 4, then all the information AFTER that steps are not so relevant to obtain the current state
- intuition: during the parsing of the chosen ending the states produced should be similar to state produces during important premises