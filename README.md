# Marketing Strategies for Subscriptions to Term Deposits

## Introduction
A financial institution sought data driven strategies for identifying successful and unsuccessful direct marketing efforts to increase the subscription of term deposits for their clients. Their current strategy involved making phone calls to customers, often multiple calls to the same customer to ensure their custoers are subscribing to their products. For this project, the focus is on just one of their products: term deposits. Term deposits are usually short term deposits with maturities ranging from one month to a few years. The goal of the direct marketing methods is to inform the customer of policies pretaining to the financial products; in this case,the customer must understand that term deposits can't be withdrawn at any time of preferences but only when the agreed upon term period ends. The institution provided information of 40,000 of their clients, omitting any information that breach privacy concerns. 

**Aim** <br />
Develop a machine learning model that can successfully predcit whether a customer will subscribe to a term deposit or not with 81% accuracy or above, where accrucay is evaluated with 5-fold cross validation. 

**The Data** <br />
The data provided included information pertaining to the customer can be classified into two categories: customer profile, the cutomer's financial profile, and marketing strategies. 

Customer profile includes information on the customers' ages, employment sector, marital status, and educational background. Their financial profile included information on the balance they maintained with the institution, and previous borrowing history such as whether they have housing and personal loans and if the customer had defaulted on them or not. Finally, the margetting strategies information included how the customers were reached (telephone, cellular or unknown), the last day, month, duration of the last contact, and the number of contacts for each client for the current campaign (the term deposit). 

## Data Wrangling

Many of the data entry were made in inconvenient forms. For example, discrete numerical data such as the month of contact were entered as strings, so the first course of action was the ammendment of the data types. The dataset is labelled with no missing entries for any of the clients. However, the distribution of the two classes was highly imbalanced: 92.76% of the dataset represented customers who did not sign up for term deposits whilst only 7.24% were customers who did subscribe. 
<p align = "center">
<img width="380" alt=image" src="https://user-images.githubusercontent.com/92346673/221760099-3ad02c92-c756-40e0-b918-6ef8c466e705.png">
</p>
<br />
Prior to deciding on how to handle the imbalnace, first anomalous and spurious data had to be identified and addressed. In order to identify possible key features from each attribute, the data wrangling steps were broken down for each feature, and for each feature the normalised distribution of the subscriptions were also explored.
                                                                                                                                       
                                                                                                                                   

                                                                                                                                       
