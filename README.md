# Will they go or will they stay?
## User churn prediction and prevention of an online music streaming service

## Introduction 
Building up and keeping a loyal customer can be challenging for any company, especially when customers are free to choose from various providers within a product category. Furthermore, retaining existing customers is generally more cost-effective than acquiring new ones. For this reason, evaluating user retention is crucial for business. It is essential to measure the level of customer satisfaction and measure the number of clients that will potentially stop the contract or make purchases with a company or service.

Customer churn, also known as customer attrition, is the percentage of customers that stopped using a company's service during a particular period. Keeping churn rates as low as possible is what every business pursuits. Identifying potential churners and influential features in advance allows the company to develop strategies to prevent customers from leaving. There are numerous ways a company can do to keep their customers. For example, offer incentives, like discounts or loyalty programs, provide additional services or engage with your user on social media in an attempt to reduce the churn rate. 

After identifying the potential churners, I will introduce the Survival Analysis and Customer Life Time Value Analysis. Why bother? It would be great to know every customer who will churn, but how much insight would that information really bring? And how would you know when and what to focus on if you wanted to keep them and how much you could spend to keep them before having them as a customer turned into a loss? Our churn prediction model provides no clear answer as to what time scale it is predicting for. And this is when Survival Analysis and Customer Life Time Value Analysis come into play. The former allows us to model the time to an event(churn). The latter gives us crucial insights into how much money we should be spending on acquiring the customers by calculating how much value they'll bring to the business in the long run. Rather than just racing to keep my head above water, I would like to understand which customers I should be focusing on and, more importantly, why I should be focusing on them. Let's begin by looking into the dataset to predict churn of KKBOX's paid users!

## Dataset
The data I will be using for this project is from KKBOX. KKBOX is Asia’s leading music streaming service, holding the world’s most comprehensive Asia-Pop music library with over 30 million tracks. They offer a generous, unlimited version of their service to millions of people, supported by advertising and paid subscriptions. After initial data processing, the contains 1,704,672 entires and 15 columns.

- msno: user id
- payment_method_id: payment method
- payment_plan_days: length of membership plan in days
- plan_list_price: in New Taiwan Dollar (NTD)
- actual_amount_paid: in New Taiwan Dollar (NTD)
- is_auto_renew
- transaction_date: format %Y%m%d
- membership_expire_date: format %Y%m%d
- is_cancel: whether or not the user canceled the membership in this transaction.


## Churn Prediction
