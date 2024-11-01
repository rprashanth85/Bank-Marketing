# Bank Digital Marketing Model


# Link
https://github.com/rprashanth85/Bank-Marketing.git

# Overview
In this practical application, the goal is to compare the performance of the classifiers we encountered in this section, namely K Nearest Neighbor, Logistic Regression, Decision Trees, and Support Vector Machines. 
We will utilize a dataset related to marketing bank products over the telephone.

Our business objective is to develop a model that can predict the success of client contact, specifically whether a client subscribes to the deposit. 
This model will boost campaign efficiency by pinpointing key factors influencing success, enabling better resource management (such as personnel, calls, and time) and helping to target a high-quality, cost-effective pool of potential customers.


# Data
Our dataset comes from the UCI Machine Learning repository [link](https://archive.ics.uci.edu/dataset/222/bank+marketing). 
The data is from a Portugese banking institution and is a collection of the results of multiple marketing campaigns. 
The dataset collected is related to 17 campaigns that occurred between May 2008 and November 2010.

# Data Investigation
Based on the initial analysis from the PDF attached. There are no null values. All the null values are coerced as UNKNOWN category.
Target variable / class is a binary object and it is imbalanced. YES is 11% and NO is 89%.
There are 20 features the target variable is dependent on. 
There are few columns like 'pdays', 'previous', 'nr.employed' can be removed as their mean value is almost same as the 25,50,75, and max percentages. 
Meaning no impact. But removing also will not impact the modeling.

Summary of Numerical Features

<img width="1077" alt="Screenshot 2024-10-30 at 11 50 47 PM" src="https://github.com/user-attachments/assets/b01caa7a-54ba-48b7-aa97-bfca1758757b">

Summary of Categorical Features

<img width="836" alt="Screenshot 2024-10-30 at 11 50 56 PM" src="https://github.com/user-attachments/assets/14119482-d718-4983-8b70-ac5b6b1b11fe">

More than investigating data key here is the Classifier model itself.

# Data Preparation for Modeling 

  1.  Considered all the columns for X and target variable mapped as 1 and 0 for the booleans and captured as y
  2.  Train and Test sets captured with the ratio of 80-20.
  3.  Applied Standard Scaler for numerical features and One Hot Encoder for the categorical features.
  4.  As we a dealing with classifier models did not apply polynomial degree.

# Basic Modeling 
Established a baseline to compare the other models. For this used DummyClassifier with strategy as 'most-fequent'. Considered AUC and ROC for the scores and gives a value of 0.5.
Indicates that the predictions are positive.

Dummy Classifier ROC Curve-AUC score

<img width="630" alt="ROC Curve Dummy Classifier with AUC" src="https://github.com/user-attachments/assets/51e323f2-8c73-4c5c-a22e-cf540108695a">


# Simple Logistic Model 
Simple Logictic Regression Model did improve the prediction rate overall with AUC 0.71 and predicting NO with 93% and Yes with 71%

Simple Logistic Classification Report 

<img width="413" alt="Screenshot 2024-10-31 at 12 04 49 AM" src="https://github.com/user-attachments/assets/91218cd4-59fc-49c7-81d4-146e95414d77">

Simple Logictic Regression ROC Curve-AUC score

<img width="651" alt="ROC Curve Simle Logistic Model with AUC" src="https://github.com/user-attachments/assets/134d656b-4335-48d4-ab41-930163b7c7ea">


# All Model Comparison - Default Parameterization
Task is to create a Data frame and capture the Training Time, Training Accuracy and Test Accuracy.
When comparing all models Decision Tree performed better with AUC score of 0.74. 
SVM and KNN with score of 0.70.
Still it is not a clear difference whcih model is better.

<img width="441" alt="Screenshot 2024-10-31 at 12 11 51 AM" src="https://github.com/user-attachments/assets/ebf023c8-179e-4cbd-95fe-3fc3fe81388d">

# Improving the models - With Hyperparameters
Below are the hyperparameters defined for each of the classifiers and model them. 

<img width="460" alt="All Model Hyperparameters" src="https://github.com/user-attachments/assets/35f645cc-690a-4dfc-b559-0b502c153ae6">

Results from Grid Search are below

<img width="540" alt="Grid Search All Model Results" src="https://github.com/user-attachments/assets/7482339c-6d2d-410c-b720-b9635a1bfb41">

**Key Insights**

Decision Tree has the highest overall accuracy at 91.9% and performs consistently between training and testing.

SVM has good accuracy at 91.1% but a very high computation time (1274 seconds).

KNN achieves a strong balance with 90.9% accuracy and the lowest fit time (1.2 seconds).

Logistic Regression has moderate performance with 90.7% accuracy but lower training/testing accuracy.

# Adjusting performance metrics

Based on the metrics above Decision Tree and SVC are best models.

Considering the Grid Search best parameters of decision tree I have captured 
1) Tuned Decision Tree Model
2) Precision Score
3) ROC Curve
4) AUC

ROC and AUC will remain the same as Grid Search whcih is 75%. Train and Test precision scores are 66% and 68% respectively.

# Further Analysis

Through out this exercise I have been using roc_curve, auc library from sklearn.metrics for the measuring the scores. 
Based on that Decision Tree performed better and second best is the SVC. 

There is a different library called RocCurveDisplay from sklearn.metrics

Using RocCurveDisplay I got a score of 94% for SVC and 93% for Decision Tree. 
For this SVC performed better slightly that the Decision Tree.

And this result is more in line with the scores presented in the CRIS-DM-BANK.pdf file.

Next step would be to measure the performance of all models with hyper parameters based on RocCurveDisplay from sklearn.metrics library.

Below is the metric for Decision Tree 

<img width="601" alt="RocCurveDisplay for Decision Tree" src="https://github.com/user-attachments/assets/0c30a5a4-151d-4d85-ac35-53f4fea0b612">




