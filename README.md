# Horse-Race-Prediction
# Horse Race Prediction
 - [Background](#Background)
 - [Problem Statement](#Problem-Statement)
 - [Data Sources](#Data-Sources)
 - [Executive Summary](#Executive-Summary)
 - [Data Dictionary](#Data-Dictionary)
 - [Recommendations](#Recommendations)
 - [Conclusion](#Conclusion)
 

## Background
![HorseRacing](https://github.com/ethan-eplee/HorseRacePrediction/blob/main/images/horseracing.jpg)

Horse racing has a long and distinguished history, practised in civilisations across the world since ancient times. The modern horse racing became well-established in the 18th century in Britian. It continued to grow in popularity till this day, and was one of the few sports that continued during the Covid-19 crisis in Australia and Hong Kong.

Horse racing is the most important sport in Hong Kong. With only 24 trainers and a similar number of jockeys, participants are firmly in the spotlight. The regulation and governance of the horse racing industry comes under the supervision of the Hong Kong Jockey Club.

## Problem Statement
Punters have access to information available on the HKJC website, with veterinary and trackwork record available at the click of a button. There are many factors that could affect the race result and millions have tried to find a winning formula in order to make a profit from betting. We did a simple test to see what would happen if we had bet $1 on every horse with the lowest odds. Theoretically, this should work since the horse with the lowest odds tends to be the favourite. Our results showed otherwise.

![BetLowest](https://github.com/ethan-eplee/HorseRacePrediction/blob/main/images/bet_lowest_odds.jpg)

And so the problem we want to address here is: 

**Can we use machine learning to make predictions to profit from horse races?**

We will follow the data science process to answer this problem.
1. Define the problem
2. Gather & clean the data
3. Explore the data
4. Model the data
5. Evaluate the model
6. Answer the problem

--- 
## Data Sources
The dataset contains the race result of 1561 local races throughout Hong Kong racing seasons 2014-17. They can be downloaded from Kaggle at [this link](https://www.kaggle.com/datasets/lantanacamara/hong-kong-horse-racing).

The data dictionary will be provided at the bottom of this file.

---
## Executive Summary
**INTRODUCTION**

This project seeks to make predictions on the outcome of horse races through both classification and regression models. For classification models, we aim to predict the winner and top 3 positions of a race. For regression models, we aim to predict the finish time of the horses, hereby predicting the winner of the race.

With the prediction results, we will make bets using different strategies to profit from the horse race. Backtesting results of each model will also show the number of bets and profit made from each strategy.

**METHODOLOGY**

The work was done in 7 seperate notebooks.
1. Preprocessing - Cleaning and tidying of data, Feature Engineering
2. EDA - Data visualisation and analysis of key patterns
3. Classification Modelling - Training dataset fitted on 4 models to get classfication predictions
4. Regression Modelling - Testing dataset fitted on 4 models to get regression predictions
5. Evaluation - Evaluation of results, Feature Importance, SHAP values
6. Backtesting - Using betting strategy to answer the problem statement of whether we can profit from horse races
7. Deployment - To build an application using Streamlit, where punters can key in simplified inputs to get a prediction on whether to bet on a horse.

The application was deployed on Streamlit and can be accessed through this [link](https://ethan-horseraceprediction.streamlitapp.com/). A screenshot showing the app is shown below. Please note that this app was only intended as an educational and demo tool, and not meant to be used for real life betting.

![App](https://github.com/ethan-eplee/HorseRacePrediction/blob/main/images/app.jpg)


**SIGNIFICANT FINDINGS**

Classification models were evaluated on their F1, PR-AUC Score, Precision and Recall as the dataset is highly imbalanced when predicting the positive class of the top position. There is a tradeoff between precision and recall and in the case of making correct predictions, precision would be the more important consideration.

For regression models, the metric used was the root mean squared error (RMSE). Models were trained to generalized. With a regression prediction, finding the fastest horse from each race allowed us to obtain the accuracy (or precision) of predicting the top position and top 3 positions.

![Feature Importance](https://github.com/ethan-eplee/HorseRacePrediction/blob/main/images/shap_features.jpg)

The SHAP summary plot showed that lower values of a horse's recent ranks contributed to a higher probability of the horse finishing top. The quality of the jockey, as shown by his recent ranks, also play a big role in determinining if a horse will win.

In the backtesting phase, we ran our model predictions through different strategies, and found that 7 out of 8 models actually returned a positive value. In the notebook, we ran a few strategies, but the simplest ones were:
1. Bet $1 when model that predicted a horse will win the top position
2. Bet $1 on the horse that model predicted with the fastest time during a race

A summary of the backtesting results when ran on these two strategies are shown below.

|                **Model** 	| **Money** 	| **Bets Made** 	|
|-------------------------:	|----------:	|--------------:	|
|               SMOTE + RF 	|     375.2 	|           743 	|
| Random Forest Classifier 	|     268.1 	|            68 	|
|      Logistic Regression 	|      23.0 	|            32 	|
|     Gaussian Naive Bayes 	|      10.7 	|           177 	|
|         Ridge Regression 	|     360.4 	|           480 	|
|                     LGBM 	|     307.3 	|           617 	|
|           KNN Regression 	|     237.6 	|           480 	|
|  Random Forest Regressor 	|     -48.1 	|           542 	|

---
## Data Dictionary

There are two datasets obtained from Kaggle, courtesy of the Hong Kong Jocket Club. The first is the related to the horse and the the second is related to the race. Both of these tables can be joined on the race_id column.

| Columns               	| Description                                                                                                                                                                            	|
|-----------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| finishing_position    	| The rank of the horse. (E.g. the horse with finishing_position 1 is the first to finish)                                                                                               	|
| horse_number          	| The number for the horse in the specific race. (Note that the same horse may have different numbers in different races)                                                                	|
| horse_name            	| English name of the horse                                                                                                                                                              	|
| horse_id              	| ID of the horse. (The ID for a horse is unique in all the races)                                                                                                                       	|
| jockey                	| The one who rides the horse in the race. (A jockey can ride different horses in the races)                                                                                             	|
| trainer               	| The one who trains the horse. (Multiple horses from a trainer can appear in the same 
