Approached the signal detection from background as Anomaly detection problem

Assumptions: Assumed each feature is independent in the row


Problems:
1. Dataset is highly imbalanced
Class 0 :  284310  : Background Event
Class 1:      492  : Signal event

2. Trainingg a classifier on this labelled and imbalanced will bias towards major class.

There are several ways to approach this problem in unsupervised fashion
1. Autoencoders can be used in an unsupervised fashion
2. K means clustering is also possible but because of class imbalance, it will bias the majority
samples
3. One more approach is to treat this problem as (AD) Anamoly detection problem. Since the
goal is to detect a signal event from a large background events.
This problem is similar to fradulent transation detection or object detection from a large set
of background pixels or defect detection in images using machine vision, medical diagnosis
and law enforcement.
We have used Anamoly approach to solve this problem. After analyzing features we found
it rarely happens. the signal is being formed.
There are several AD models like
4. Isolation Forest
5. Local Outlier Factor
6. Robust Covariance
7. One-Class SVM
8. One-Class SVM (SGD)
We used 1. Isolation Forest


Steps:
#First I look for Null values and replace them with zero
NOrmalization 
Analyzed various principal components to see which feture has more variance
Investigated the coorelation between features between backgound and Signal event on p3 and p14 features
From the graph, We observe that the p3 and p14 features didn't show any diffrence between signal and background events
From this plot, we observe most of signal events have smaller value of feature p14. 
We have only 0.17\% signal events from the dataset. This implies random guess by any model should produce 0.17\% accuracy for signal detection
Tested two models 
LocalOutlierFactor and isolationForest. Isolation one gives better results 
Afetr anayzing the confusion matrix, we can see 201/492 signal can be detected which is apprximately 40\% accuracy

Conf Matrix 
[[272806  11509]
[291        201]]

Signal Accuracy  = 201/492 ~ 40\%

Advantages of Model Isolation Forest
Computationaly Efficient and has been proven effective in other anamoly detection problems

Limtations
model is dependent on contanimaton parameter. i.e it should be estimated before what percetage is Signal beforehand
Model suffers from a bias because of branching factor
