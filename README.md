# Marketing Strategies for Subscriptions to Term Deposits

## Introduction
A financial institution sought data-driven strategies for identifying successful and unsuccessful direct marketing efforts to increase the subscription of term deposits for their clients. Their current strategy involved making phone calls to customers, often multiple calls to the same customer to ensure their customers are subscribing to their products. For this project, the focus is on just one of their products: term deposits. Term deposits are usually short-term deposits with maturities ranging from one month to a few years. The goal of the direct marketing methods is to inform the customer of policies pertaining to the financial products; in this case, the customer must understand that term deposits can't be withdrawn at any time of preference but only when the agreed-upon term period ends. The institution provided information of 40,000 of its clients, omitting any information that breach privacy concerns. 

**Aim** <br />
Develop a machine learning model that can successfully predict whether a customer will subscribe to a term deposit or not with 81% accuracy or above, where accuracy is evaluated with 5-fold cross-validation. 

**The Data** <br />
The data provided included information pertaining to the customer can be classified into two categories: customer profile, the customer's financial profile, and marketing strategies. 

The customer profile includes information on the customers' ages, employment sector, marital status, and educational background. Their financial profile included information on the balance they maintained with the institution and previous borrowing history such as whether they have housing and personal loans and if the customer had defaulted on them or not. Finally, the marketing strategies information included how the customers were reached (telephone, cellular or unknown), the last day, month, duration of the last contact, and the number of contacts for each client for the current campaign (the term deposit). 

## Data Wrangling

Many of the data entries were made in inconvenient forms. For example, discrete numerical data such as the month of contact were entered as strings, so the first course of action was the amendment of the data types. The dataset is labelled with no missing entries for any of the clients. However, the distribution of the two classes was highly imbalanced: 92.76% of the dataset represented customers who did not sign up for term deposits whilst only 7.24% were customers who did subscribe. 
<p align = "center">
<img width="380" alt=image" src="https://user-images.githubusercontent.com/92346673/221760099-3ad02c92-c756-40e0-b918-6ef8c466e705.png">
</p>
<br />
Prior to deciding on how to handle the imbalance, first anomalous and spurious data had to be identified and addressed. In order to identify possible key features from each attribute, the data wrangling steps were broken down for each feature, and for each feature, the normalised distribution of the subscriptions was also explored. 

## EDA

To do so the different features in the dataset can be broken down into three main areas: 
### Customer Profile 
This included the age of the customers, the type of jobs they held, their marital status and their highest level of education. 

There are some clear age groups where there is a higher percentage of clients who sign up for term deposits. It's worth noting that customers aged 90 and 95 have exactly the same number of people, all of whom have subscribed for term deposits. This could possibly be spurious or a mere coincidence. For now, there's not sufficient information to suggest these groups out outliers and so these entries were left in the dataset. The distribution of the age groups of clients in the whole dataset is roughly comparable between those clients who did and didn't subscribe to term deposits. The median is slightly lower for those who with term deposit subscriptions when compared to those clients who didn't register for subscriptions: 37 compared to 39. It's also interesting to note that the dataset has a higher proportion of clients aged between 26 to 60, but the percentage of clients who sign up for term deposits is higher for clients who are older. The marital status between the two classes seemed to mirror each other whilst customers with tertiary education backgrounds formed a higher proportion of subscriptions. 

### Financial Profile

Some of the features can be used to group customers according to known financial information. For example, we can try to group customers based on their balance, and previous borrowing history such as whether they have defaulted on loans, or if they have housing and personal loans. 

As expected, those who have previously defaulted on loans mostly didn't sign up for term deposits. Those with secondary level education are the largest group of those who took out loans, again forming the largest segmentation of customers who did default on loans and signed up for term deposits. This doesn't necessarily mean that secondary education is what we should look for when trying to determine which customers to target and could be just a consequence of the unbalanced dataset. 

We see roughly 5% of customers who had defaulted on loans and had agreed to term deposits maintained an average annual balance of 0 or were overdrawn. This goes up to roughly 8% when we look at customers who haven't defaulted on loans. When we compare the customer profiling metrics between overdrawn and in-credit customers we see that both of these groups have roughly the same distribution in ages of customers. We see that the percentages of customers from various education backgrounds and to some extent in jobs are also mimicked between those who are overdrawn and those who aren't. This suggests that looking to differentiate between customers with overdrawn as a feature is not useful. When we look at the balance of customers who have signed up for term deposits grouped by employment and education backgrounds, we do see that for every segment customers who have higher balances sign up for term deposits. This suggests balance is a possible key feature, however, how to segment customers based on balance was identified as worthy of further exploration. 


#### Marketing Strategies 
The remaining features can be categorised as marketing strategies used by the Bank to inform their customers of the product. These included communication type, the last day and month of contact, duration of last contact, and the number of times contacted during the last campaign to see if there are strategies that have yielded a higher number of subscriptions for term deposits. 

The highest number of customers who subscribed and those who didn't subscribe for term deposits all occurred during the month of May. This is most likely due to there being a higher frequency of customers in May. This further supports the idea of looking deeper at the months of March and October as the months of higher subscription rates. 

## Feature Engineering

LabelEncoder was used to encode the categorical features: job, marital, education, default, housing, loan, contact, and classes. The numerical features were scaled using Standard Scalar and Robust Scalar. As each of the scaling methods uses slightly different techniques, both datasets were used to develop models. The idea here is to select a scaling method for future use that would optimise the model's weighted F1 score. 

## ML Models

Initially, the following series of models were developed and optimised by hyperparameter turning through GridSearchCV for unscaled data, then the scaled dataset was used or data with stratified sampling. Each of the models was tested for overfitting and underfitting by comparing the accuracy score with the training set score. Due to the imblanace in the data, the weighted F1 score was used to judge the quality of the model. The area under the ROC was calculated to help determine the best model, and when possible the feature importance was extracted.

1. K Nearest Neighbors Classifier: Weighted F1 score: 0.917, AUC: 0.755
2. Random Forest Classifier: Weighted F1 score: 0.928, AUC: 0.940, Feature Importance (greater than 10%): duration, balance, day, and age.
3. AdaBoosting: Weighted F1 Score of 0.919, AUC: 0.701, Feature Importance (greater than 10%): duration, balance, and day.
4. CatBoost: Weighted F1 Score of 0.933, AUC: 0.947, Feature Importance (greater than 10%): duration, month, and contact.
5. HistGradBoost: Weighted F1 Score of 0.932, AUC: 0.948
6. LightGBM: Weighted F1 Score of 0.934, AUC: 0.948, Feature Importance: duration, balance, day, month

These were then compared to models generated with a SMOTE dataset. 

1. K Nearest Neighbors Classifier: Weighted F1 score: 0.851, AUC: 0.762
2. Random Forest Classifier: Weighted F1 score: 0.928, AUC: 0.929, Feature Importance (greater than 10%): month, duration
3. AdaBoosting: Weighted F1 Score of 0.907, AUC: 0.733, Feature Importance (greater than 10%): duration and month.
4. CatBoost: Weighted F1 Score of 0.933, AUC: 0.930, Feature Importance (top three): month, duration, and contact.
5. LightGBM: Weighted F1 Score of 0.918, AUC: 0.932, Feature Importance: duration, month, balance, and day.

## Best Model

Random Forest Classifier

Parameters: 'criterion': 'gini', 'max_depth': 9, 'n_estimators': 27
Dataset: SMOTE analysis
Weighted F1 Score: 0.923
AUC of ROC: 0.919
Key Features: duration, contact, month

## Customer Segmentation

The aim was to perform KMeans Clustering with PCA to see if the segments identified (duration, contact and month) could be further confirmed. Silhouette Analysis and the Elbow Method were used to identify optimal values of KK for the K Means clustering. 

## Conclusion
The best-performing model here is a Random Forest Classifier which yield an accuracy score of 92% after SMOTE analysis was conducted to account for the imbalance in the dataset. It is important to note that whilst the success metrics outlined in the aim of the project are accuracy, the weighted f1 score was prioritised due to the imbalance in the dataset. For this model, the weighted f1 score is 92% as well. 

The Random Forest Classifier, alongside other classification algorithms, highlighted the month of the last contact, the duration of the last contact, the means of the last contact, and the balance as important features in the dataset for the classification. This was in line with the results of KMeans clustering with PCA. 3 to 4 clusters look visible. To gain a better idea of the problem, it's worth looking into how many clients signed up for subscriptions and then tried to withdraw their deposits before the maturity time. This alongside the duration of the contacts can help gain a better understanding of the relationship duration and subscription. Otherwise, it does look like the longer a customer is spoken with the higher the chance of them subscribing for term deposits. October and March have the highest subscription rates and therefore is worth driving more attention to these two months through telephone/cellphone contact. 

