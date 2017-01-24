---
title: Homework 0
permalink: /cs267/hw0
---

## CS 267

### Homework 0

#### Ziheng Lin

 

#### About me

I am a third year PhD student in the Civil and Environmental Engineering department with a focus on transpiration behavior studies. My research is to model human activity sequences using generative models, especially recurrent neural network, and large-scale cellular phone data. The model should be capable of capturing complex daily sequences of urban populations and be able to generate close-to-reality synthetic data for transportation demand forecasting. I would like to develop some knowledge about parallelizing the model so that it can be scaled to the massive amount of data that we have. I would also like to learn about fundamentals of machine architecture. 

#### Parallel computing for speech recognition

Speech recognition has a wide range of application that varies from voice control to video captioning. The main challenges for speech recognition systems are accuracy and latency and those can be solved by applying parallel computing techniques. There are two areas where parallel computing applies in speech recognition problem: model training and data processing pipeline.

A speech recognition system can be very accurate when it is trained with enough data. The current state of art speech recognition model is recurrent neural network, which relatively inefficient in training due to the large amount of parameters that their sequential dependencies. Many parallelization techniques have been proposed in order to optimize training the parameter of models [2, 3]. 

Some streaming speech recognition pipelines are designed that streaming data is passed into multiple models and different features are extracted in parallel. The features are then combined and proceed by a neural network.

 
[1] S.  Hochreiter  and  J.  Schmidhuber.   Long  short-term  memory. Neural computation, 9(8):1735–1780, 1997.

[2] Hidasi, Balázs, et al. "Parallel recurrent neural network architectures for feature-rich session-based recommendations." Proceedings of the 10th ACM Conference on Recommender Systems. ACM, 2016.

[3] Lyu, Qi, and Jun Zhu. "Revisit long short-term memory: An optimization perspective." Advances in neural information processing systems workshop on deep Learning and representation Learning. 2014.

[4] Chong, Jike, et al. "Opportunities and challenges of parallelizing speech recognition." Proceedings of the 2nd USENIX conference on Hot topics in parallelism. USENIX Association, 2010.



