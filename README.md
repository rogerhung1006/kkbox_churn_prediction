# Will they go or will they stay?
## User churn prediction and prevention of an online music streaming service
### *Table of contents*
  * [Introduction](#Introduction) 
  * [Dataset](#Dataset)
  * [User churn prediction](#User-churn-prediction)
  * [Survival Analysis](#Survival-analysis)
  * [Part 5. Interpretation of Clusters](#part-5-interpretation-of-clusters)
  * [Part 6. Customer Profiling and Suggestion](#part-6-customer-profiling-and-suggestion)
  * [Part 7. The Potential Problem for the Business](#part-7-the-potential-problem-for-the-business)

## Introduction 
Building up and keeping a loyal customer can be challenging for any company, especially when customers are free to choose from various providers within a product category. Furthermore, retaining existing customers is generally more cost-effective than acquiring new ones. For this reason, evaluating user retention is crucial for business. It is essential to measure the level of customer satisfaction and measure the number of clients that will potentially stop the contract or make purchases with a company or service.

Customer churn, also known as customer attrition, is the percentage of customers that stopped using a company's service during a particular period. Keeping churn rates as low as possible is what every business pursuits. Identifying potential churners and influential features in advance allows the company to develop strategies to prevent customers from leaving. There are numerous ways a company can do to keep their customers. For example, offer incentives, like discounts or loyalty programs, provide additional services or engage with your user on social media in an attempt to reduce the churn rate. 

After identifying the potential churners, I will introduce the Survival Analysis and Customer Life Time Value Analysis. Why bother? It would be great to know every customer who will churn, but how much insight would that information really bring? And how would you know when and what to focus on if you wanted to keep them and how much you could spend to keep them before having them as a customer turned into a loss? Our churn prediction model provides no clear answer as to what time scale it is predicting for. And this is when Survival Analysis and Customer Life Time Value Analysis come into play. The former allows us to model the time to an event(churn). The latter gives us crucial insights into how much money we should be spending on acquiring the customers by calculating how much value they'll bring to the business in the long run. Rather than just racing to keep my head above water, I would like to understand which customers I should be focusing on and, more importantly, why I should be focusing on them. Let's begin by looking into the dataset to predict churn of KKBOX's paid users!

## Dataset
The data I will be using for this project is from KKBOX. KKBOX is Asia’s leading music streaming service, holding the world’s most comprehensive Asia-Pop music library with over 30 million tracks. They offer a generous, unlimited version of their service to millions of people, supported by advertising and paid subscriptions. After initial data processing, I have two data sets, user_sample_data and user_log. The former contains 1,704,672 entires and 15 columns, and the latter contains 18,396,362 entires and 9 columns.

### user_sample_data
- msno: user id
- city: In total 21 cities and they are encoded by integers.
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

### user_log
- msno: user id
- date: format %Y%m%d
- num_25: # of songs played less than 25% of the song length
- num_50: # of songs played between 25% to 50% of the song length
- num_75: # of songs played between 50% to 75% of of the song length
- num_985: # of songs played between 75% to 98.5% of the song length
- num_100: # of songs played over 98.5% of the song length
- num_unq: # of unique songs played
- total_secs: total seconds played
</br>
Note that the integer features num_25, num_50, num_75, num_985, and num_100 tell us the number of songs for this day that the user played for <25%, 25-50%, 50-75%, 75-98.5%, or >98.5% of their total duration.

## User churn prediction
In this section, my goal is to predict whether or not a customer will churn based on various features that I created previously. I will be using supervised machine learning techniques to make predictions. Before the modeling process, I also conducted a simple exploratory data analysis and feature engineering to create insightful new features. Notice that I won't dig too deep in terms of data exploration. I am doing the complete and extensive exploratory data analysis of this data on another project, which will be posted soon.

### Feature engineering 
I create the following features:
- **Age_Range bucket(age_bin)**: I created buckets for the age-range 5-11(child), 12-18(teenagers), 19-25(college students), 26-35(newly grad and early career professionals), 36-45(mid-aged), 46-60, and 60-100.
- **days_to_first_trans**: The time between a user's registration and his or her first transaction with the company
- **days_between_trans**: The sum of time that a user was not in contract with the company during the observation period. Suppose there are five days after the termination/expiration of his first contract and before his second contract, and ten days after the termination/expiration of his third contract and before his fourth contract, the value of days_between_trans is then 15.  
- **tenure**: The number of days between the registration date and the membership expiration date, provided that this user had churned. If the user didn't churn, the tenure is then defined as the number of days between the registration date and the snapshot date.
- **no_records**: The number of records a user has in our data set, which, to some extent, represents how frequently a user is interacting with the company.
- **uniq_rate**: The ratio between the number of unique songs a user had listened to and the number of total songs he/she had listen to.
- **listening_type**: There are three types of listeners, loyalist_type, normal_type, and switcher_type. If the percentage of the number of songs a user played for >75% of their total duration over the number of all songs played is higher than 80%, the user is defined as a loyalist type of listener.
For more detailed information, please check out my jupyter notebook.

### Model results
For this project, I used four classification models. One simple linear classification model: Logistic Regression, and three non-linear tree-based models: Random Forest, Gradient Boosted tree, and Extreme Gradient Boosting tree. Here are the results 


We see that XGBoost is the game winner, with Logistic Regression being the runner-up (much to my surprise). XGBoost has been proving its effectiveness on Data Science projects for a while, and, in this project, it provided the best results among the models. For that reason, XGBoost algorithm would be our choice for the churn prediction model. According to Chen and Guestrin, the most important advantage of XGBoost is its scalability, which makes the technique adaptable to all sorts of different problems. XGBoost is an optimized version of the gradient boosting algorithm in terms of speed, handling missing values, and avoiding overfitting. For those who are interested in knowing more about the modeling as well as feature selection process, please check out the code. I also tried using the resampling methods to deal with the imbalance classification problem and for better prediction, but the results turned out to be not that satisfactory.

### Interpretation

## Survival Analysis 


