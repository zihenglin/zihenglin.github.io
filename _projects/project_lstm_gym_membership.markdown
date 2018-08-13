---
layout: page
title: Predicting Gym Members' Next Activity
description: 
img: /assets/img/project_lstm_gym_membership/cover.png
thumbnail: /assets/img/project_lstm_gym_membership/cover.png
---

For business, such as gym, the owners would like to know when are their members coming to the gym and which class are they going to purchase next. Building forecasting models for the members' behavior is valuable for helping the business owner make decisions. Usually, historical data is available for the modeling tasks. It includes history of members' behaviors, such as classes they enrolled and when they show up, and etc.

### The LSTM Model 

Here we formulate the problem as given all the historical behavior of a member, what class is the person member going to choose next and when is the member going to show up next. We define the LSTM structure below. At each timestamp, the LSTM observes a member's behavior that is encoded by its features. After the observation, the model predicts the member's next behavior.

<img class="two" src="{{ site.baseurl }}/assets/img/project_lstm_gym_membership/lstm_diagram.png">


### Formulation the prediction

#### Predicting time gaps

The first thing we would like to predict is the time gap between the last observed activity to the nearest future activity. This is a continuous variable, but there are patterns in such time gaps that we are able to simplify the problem.

We are able to observe peak in the time gaps histogram around 0, 24, 48,... hours. This shows members come to gym in relatively fixed time of day but different days of week. Therefore, we are able to discretize the time gaps into unite of days. Thus, we are able to formulate the output distribution from the LSTM model as a discrete distribution.

<img class="three" src="{{ site.baseurl }}/assets/img/project_lstm_gym_membership/time_gap_distribution.png">


#### Predicting class choices

There are total of 17 different classes in the gym for members to choose from. The histogram of the number of unique classes per member is shown below.  The LSTM model predicts the probability of each class choice given the history of a member's behavior. Majority of members stick with 1-4 unique classes and the very few members tried more than 4 different classes.

<img class="two" src="{{ site.baseurl }}/assets/img/project_lstm_gym_membership/unique_classes_distribution.png">


### Results

We first show the prediction accuracy for the time gaps below. Human activities, as we all know, are difficult to predict. If we restrict the prediction to the most probable output from the model the accuracy of time gaps remains at around 50% correct. However, if we relax the such a constrain and allow the second and third most probable prediction, the chances of the model being correct increase to close to 90%. The plot below shows the prediction accuracy vs such constrain relaxation.

<img class="two" src="{{ site.baseurl }}/assets/img/project_lstm_gym_membership/time_gap_accuracy.png">

We first show the class choice prediction accuracy. We show the prediction vs constrain relaxation as discussed above. The best choice from the model prediction over 60% accuracy, which is already significantly better than random guess amount 17 choices. If we inculde the second and third best choice, the accuracy increases to around 90%.

<img class="two" src="{{ site.baseurl }}/assets/img/project_lstm_gym_membership/class_accuracy.png">

Lastly, we would like to investigate if the accuracy of the model prediction is related to the observation length of each member. We plot the prediction accuracy vs the number of observed data points of each member and we couldn't observe significant correlation between the two. Thus, we suggest that the predictability of members' behavior varies from person to person.

<img class="three" src="{{ site.baseurl }}/assets/img/project_lstm_gym_membership/accuracy_vs_observation.png">