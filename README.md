# particle_accelerator_LHC

# Problem Statement

The Large Hadron Collider (LHC) is the world’s largest and most powerful particle accelerator. The LHC was designed to discover new, unknown particles that may be produced in the collisions. The data collected in the experiments performed at the LHC can be classified as background events (particles that physicists have already discovered) or signal events (new, unknown particles; usually called new physics particles). In this project, we look for a simulated new physics signal that is hidden in a large background.

# Data Description

Each individual datapoint in the dataset contains information about an independent event that has been observed in the detector. More specifically, each event (each row in the dataset) is described by a set of 14 features. The last column indicates if the event corresponds to a signal or a background event. More specifically, each event (each row in the dataset) is described by a set of 14 features. The last column indicates if the event corresponds to a signal or a background event. In the dataset, there are 492 datapoints with class label value 1 and other 284245 are 0, which is highly unbalanced and makes the model a bit overfitted and biased for class 0. Balancing the unbalanced data by randomly sampling the class with more datapoints. We took 600 random sampled datapoints from class 0 and keeping all the 423 datapoints for class 1.

# Objective 1 : Supervised ML Solution (00supervised.ipynb)

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


# Objective 2 : Unsupervised ML Solution (01unsupervised.ipynb)
Build an unsupervised Machine Learning model and use it to construct a set of events that can be considered as signal events according to the model. Keeping in mind that the class labels cannot be used when training the model. Then, evaluate the performance of the unsupervised model at finding signal events.
