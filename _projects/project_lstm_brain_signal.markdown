---
layout: page
title: Detecting Seizure using LSTM
description: 
img: /assets/img/project_brain_signal/cover.png
thumbnail: /assets/img/project_brain_signal/cover.png
---

A seizure alert device may help notify others if a seizure happens. There are a few measurements that help seizure detection. Electroencephalogram (EEG) detects electrical activity in human brain using small electrodes attached to the scalp. Near-infrared spectroscopy (NIRS) is a non-invasive optical imaging technique that uses low levels of light to measure blood flow changes in the brain associated with brain activity. I implemented the LSTM models that detect seizure from EEG and NIRS measurements from human brains.


### The LSTM model

This is a sequence classification problem. The LSTM model takes EEG and NIRS signals as a short time-series input and output the probability of seizure in the input signal. EEG and NIRS signals are divided into fractions with fixed length. At each timestamp, the LSTM model takes selected channels of the EEG and NIRS singles. At the end of the sequence, the LSTM model outputs probability that classifies the input signal. The model is trained with label data with 4 classes non-seizure, pre-seizure, seizure, and post-seizure. 

<img class="three" src="{{ site.baseurl }}/assets/img/project_brain_signal/model_structure_demo.png">


### How does the LSTM model classify sequences

LSTM models have memories inside the cells that cumulate information as the models "see" the input. The LSTM models decide whether to write the information into its memory or to refresh its memory. At the end, the pattern of LSTM memories are going to determine the probability of each class given the input sequence. 

The middle plot and the bottom plot shows the LSTM neural activations and the change of activation.  We can observe that the LSTM neural activations started with rapid changes. Then, the LSTM neural activations stabilize so that it is ready for predicting the classes of the input sequence.

<img class="three" src="{{ site.baseurl }}/assets/img/project_brain_signal/lstm_activations_eeg_nirs_Post-seizure.png">

### LSTM model with attentions

I also implemented the LSTM model with attention. That is, at each timestamp, the LSTM model outputs a "filter" that is going to be overlaid on the input signal channels. The "filter" is just a probability distribution that sums to 1. So, the LSTM model decides what to pay attention to in the next timestamp.

We can observe from the example below. Despite, many channels are input into the model, the model pays most of its attention to only 3 input channels.

<img class="three" src="{{ site.baseurl }}/assets/img/project_brain_signal/lstm_activations_eeg_only_attention_Pre-seizure.png">


### Results

Here we show the ROC curves and confusion matrix for prediction on the testing dataset. The LSTM model does very good job in all four classes. 

<img class="three" src="{{ site.baseurl }}/assets/img/project_brain_signal/orc_confusion.png">