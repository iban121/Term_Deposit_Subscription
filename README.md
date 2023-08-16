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
Prior to deciding on how to handle the imbalance, first anomalous and spurious data had to be identified and addressed. In order to identify possible key features from each attribute, the data wrangling steps were broken down for each feature, and for each feature, the normalised distribution of the subscriptions was also explored. However, it quickly became evident the data was clean and didn't have any missing entries. As to whether there were incorrect entries, that's a harder question to answer. Given the lack of background information and limited dataset, it was concluded we didn't have enough information to question the correctness of entries. 

## EDA

Each of the features was visualised, separated by their class to see if the two different classes agreed on the ratings of some features or not. This was also an effective way to observe modal rankings for each feature. 

## ML Models

Initially, the following series of models were developed and optimised using GridSearchCV:
*Logistic Regression 
*K Nearest Neighbors Classifier 
*Random Forest Classifier 
*Support Vector Classifier
*Gradient Boosting Classifier 
*XGBoot






