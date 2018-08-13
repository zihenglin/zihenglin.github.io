---
layout: page
title: Detecting Breath in Podcasts
description: 
img: /assets/img/project_breath_detection/cover.png
thumbnail: /assets/img/project_breath_detection/cover.png
---

Audio editing for podcast production can be extremely labor intensive. Automation for the process is highly desired, however, the existing ones are rarely seen. The major part of the problem in automating the audio editing process is to detect the sound pieces that needs to be masked or cut. In this project, we introduce a method for detecting breath in podcasts.

### Breath in podcasts

Here is a short video clip showing what a breath event sounds like. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/NV7IN4HzvCI?start=566&end=569" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

<br/>

The breath event is very distinguishable by listening to it. However, when the sound is transferred into a spectrogram for deep learning, the visual patterns of breath events are not easily identifiable from our eyes. Below, you can see 3 examples of spectrogram, when breath events happened in speeches.

<img class="two" src="{{ site.baseurl }}/assets/img/project_breath_detection/examples.png">




### The LSTM Model

LSTM model shall be applied for breath event detection. A plot of the model structure is shown below. I applied the state of art model introduced in [this paper](https://www.cs.tut.fi/sgn/arg/dcase2017/documents/challenge_technical_reports/DCASE2017_Lim_204.pdf).  At each timestamp, a thin slice of spectrogram is input into the LSTM model via 1D convolutional filters. The 1D convolutional filters learn the correlations between different pitch and tone (the "spatial" relationship). The LSTM cells are responsible of learning the temporal information due to its capability of modeling sequences.

At each timestamp, the LSTM model consume a slice of the spectrogram and outputs a probability whether this slice is part of a breath event. Therefore, the LSTM model is able identify the location of a breath event when the audio is continuously passed into the model.

<img class="two" src="{{ site.baseurl }}/assets/img/project_breath_detection/model_structure.png">



### Detection Results

The LSTM models are trained on podcast episodes with breath event labeled. Below, there are some examples of breath event detection. The audio spectrogram is transformed into resolution of 46ms that each slice represents 46ms of audio. The ground truth shows the binary indicator of breath events. The prediction plots show the probability output from the LSTM model with respect to time. 

<img class="two" src="{{ site.baseurl }}/assets/img/project_breath_detection/detection_examples.png">

