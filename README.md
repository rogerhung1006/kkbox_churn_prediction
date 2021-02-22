# Will they go or will they stay?
## User churn prediction and prevention of an online music streaming service
## Table of contents
  * [Introduction](#Introduction) 
  * [Part 2. What is RFM Analysis?](#part-2-what-is-rfm-analysis-)
  * [Part 3. Feature Engineering through RFM Analysis](#part-3-feature-engineering-through-rfm-analysis)
  * [Part 4. Segmentation by K-Means Clustering](#part-4-segmentation-by-k-means-clustering)
  * [Part 5. Interpretation of Clusters](#part-5-interpretation-of-clusters)
  * [Part 6. Customer Profiling and Suggestion](#part-6-customer-profiling-and-suggestion)
  * [Part 7. The Potential Problem for the Business](#part-7-the-potential-problem-for-the-business)

## Introduction 
Building up and keeping a loyal customer can be challenging for any company, especially when customers are free to choose from various providers within a product category. Furthermore, retaining existing customers is generally more cost-effective than acquiring new ones. For this reason, evaluating user retention is crucial for business. It is essential to measure the level of customer satisfaction and measure the number of clients that will potentially stop the contract or make purchases with a company or service.

Customer churn, also known as customer attrition, is the percentage of customers that stopped using a company's service during a particular period. Keeping churn rates as low as possible is what every business pursuits. Identifying potential churners and influential features in advance allows the company to develop strategies to prevent customers from leaving. There are numerous ways a company can do to keep their customers. For example, offer incentives, like discounts or loyalty programs, provide additional services or engage with your user on social media in an attempt to reduce the churn rate. 

After identifying the potential churners, I will introduce the Survival Analysis and Customer Life Time Value Analysis. Why bother? It would be great to know every customer who will churn, but how much insight would that information really bring? And how would you know when and what to focus on if you wanted to keep them and how much you could spend to keep them before having them as a customer turned into a loss? Our churn prediction model provides no clear answer as to what time scale it is predicting for. And this is when Survival Analysis and Customer Life Time Value Analysis come into play. The former allows us to model the time to an event(churn). The latter gives us crucial insights into how much money we should be spending on acquiring the customers by calculating how much value they'll bring to the business in the long run. Rather than just racing to keep my head above water, I would like to understand which customers I should be focusing on and, more importantly, why I should be focusing on them. Let's begin by looking into the dataset to predict churn of KKBOX's paid users!

## Dataset
The data I will be using for this project is from KKBOX. KKBOX is Asia’s leading music streaming service, holding the world’s most comprehensive Asia-Pop music library with over 30 million tracks. They offer a generous, unlimited version of their service to millions of people, supported by advertising and paid subscriptions. After initial data processing, I have two data sets, user_sample_data and user_log. The former contains 1,704,672 entires and 15 columns, and the latter contains

- msno: user id
- city
- bd: age
- gender
- registered_via: registration method
- registration_init_time: format %Y%m%d
- expiration_date: format %Y%m%d, taken as a snapshot at which the member.csv is extracted. Not representing the actual churn behavior.
- payment_method_id: payment method
- payment_plan_days: length of membership plan in days
- plan_list_price: in New Taiwan Dollar (NTD)
- actual_amount_paid: in New Taiwan Dollar (NTD)
- is_auto_renew
- transaction_date: format %Y%m%d
- membership_expire_date: format %Y%m%d
- is_cancel: whether or not the user canceled the membership in this transaction.


- msno: user id
- date: format %Y%m%d
- num_25: # of songs played less than 25% of the song length
- num_50: # of songs played between 25% to 50% of the song length
- num_75: # of songs played between 50% to 75% of of the song length
- num_985: # of songs played between 75% to 98.5% of the song length
- num_100: # of songs played over 98.5% of the song length
- num_unq: # of unique songs played
- total_secs: total seconds played


## User churn prediction
In this section, my goal is to predict whether or not a customer will churn based on various features that I created previously. I will be using supervised machine learning techniques to make predictions. Before the modeling process, I also conducted a simple exploratory data analysis and feature engineering to create insightful new features. Notice that I won't dig too deep in terms of data exploration. I am doing the complete and extensive exploratory data analysis of this data on another project, which will be posted soon.


