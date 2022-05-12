# particle_accelerator_LHC

# Problem Statement

The Large Hadron Collider (LHC) is the world’s largest and most powerful particle accelerator. The LHC was designed to discover new, unknown particles that may be produced in the collisions. The data collected in the experiments performed at the LHC can be classified as background events (particles that physicists have already discovered) or signal events (new, unknown particles; usually called new physics particles). In this project, we look for a simulated new physics signal that is hidden in a large background.

# Data Description

Each individual datapoint in the dataset contains information about an independent event that has been observed in the detector. More specifically, each event (each row in the dataset) is described by a set of 14 features. The last column indicates if the event corresponds to a signal or a background event. More specifically, each event (each row in the dataset) is described by a set of 14 features. The last column indicates if the event corresponds to a signal or a background event. In the dataset, there are 492 datapoints with class label value 1 and other 284245 are 0, which is highly unbalanced and makes the model a bit overfitted and biased for class 0. Balancing the unbalanced data by randomly sampling the class with more datapoints. We took 600 random sampled datapoints from class 0 and keeping all the 423 datapoints for class 1.

# Supervised Machine Learning Approach

We build a supervised Machine Learning model and evaluate its performance at signal vs. background classification. We run 5 different ML classifiers viz:

Random Forest Classifier
Decision Tree Classifier
KNN
Logistic Regression
SVM
Balanced Baggin Classifier (Decision Tree as Base)
Balanced Baggin Claasifier (Random Forest as Base)

where Balanced Baggin Classifier (Decision Tree as Base) and Balanced Baggin Claasifier (Random Forest as Base) are ensemble model method which takes care of inbalanced data. For each model we check validation and test acc, precision and recall
and also we can see the confusion matrix for validation and test set. We can see from the MODEL_LOGS that BALANCED BAGGIN CLASSIFIER (RANDOM FOREST as BASE) is the best model and most generalized as it has the following metric:

Validation Accuracy : 88.8 %

Validation Precision : 86.8 %

Validation Recall : 87.5 %

Test Accuracy : 90.9 %

Test Precision : 95 %

Test Recall : 90.4 %

So, BALANCED BAGGIN CLASSIFIER (RANDOM FOREST as BASE) performs best among all as an ensemble technique on this dataset.


# Unsupervised Machine Learning Approach

Approached the signal detection from background as Anomaly detection problem
Assmuptions: Assumed each feature is independent in the row


Problems:
1. Dataset is highly imbalanced
Class 0 :  284310  : Background Event
Class 1:      492  : Signal event

2. Trainingg a classifier on this labelled and imbalanced will bias towards major class.

There are several ways to approach this problem in unsupervised fashion:

1. Autoencoders can be used in an unsupervised fashion.
2. K means clustering is also possible but because of class imbalance, it will bias the majority
samples.
3. One more approach is to treat this problem as (AD) Anamoly detection problem. Since the
goal is to detect a signal event from a large background events. This problem is similar to fradulent transation detection or object detection from a large set of background pixels or defect detection in images using machine vision, medical diagnosis and law enforcement. We have used Anamoly approach to solve this problem. After analyzing features we found it rarely happens. The signal is being formed.

There are several Anamoly Detection mMdels like

4. Isolation Forest
5. Local Outlier Factor
6. Robust Covariance
7. One-Class SVM
8. One-Class SVM (SGD)

We use Isolation Forest.

Steps:
1. First I look for null values and replace them with zero and then normalization.
2. We analyze various principal components to see which feture has more variance.
3. We investigate the coorelation between features between backgound and Signal event on p3 and p14 features.
4. We observe that the p3 and p14 features didn't show any diffrence between signal and background events.
5. Also, we observe most of signal events have smaller value of feature p14. 

We have only 0.17% signal events from the dataset. This implies random guess by any model should produce 0.17% accuracy for signal detection.

We tested wo models, LocalOutlierFactor and Isolation Forest. Isolation Forest gives better results. 
After anayzing the confusion matrix, we can see 201/492 signal can be detected which is apprximately 40% accuracy.

Conf Matrix 
[[272806  11509]
[291        201]]

Signal Accuracy  = 201/492 ~ 40%

Advantages of Isolation Forest:
Computationaly Efficient and has been proven effective in other anamoly detection problems.

Limtations:
Model is dependent on contanimaton parameter. i.e., it should be estimated what percentage is Signal beforehand. Also, model suffers from a bias because of branching factor.




# Graph Machine Learning Approach
Graph Machine Learning is popular nowadays. We translate this problem into a graph machine learning by translating the tabular dataset into a graph dataset. Graph Machine Learning can model a problem on the grounds of supervised ML problem (node classification) here, unsupervised or a semi supervised problem, where we can perform the clustering of those node embeddings. Another main motivation is, sometimes the data could also have some non-euclidean properties and through message passing, similar nodes must gather together so that we can see the clusters that can be seperable. So to see whether the data has some non-euclidean properties or not and whether it can be modelled that way, we are using Graph ML.
The results do not create a significant difference in this problem. What we see from the embedding is that the data belonging to class1 1 is somewhow mixed with the datapoints belonging to class 0. Regardless of using any type of approaches, we see the overlapping between the embeddings. Although, the results do not appear so good but applying Graph Machine Learning on such problems is an exciting and emerging new field.
