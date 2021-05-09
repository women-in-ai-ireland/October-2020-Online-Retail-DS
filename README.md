WAI-LEARN-Online-Retail-DS
==============================

Cohort Analysis and customer segmentation 



Online Retail Data Project
WAI Learn | April 2021

## Introduction
Nowadays e-commerce companies are becoming more and more popular, the pandemic of Covid-19 just proved how organizations need to move online to keep their business alive. 
The internet makes shopping easy, fast, and handy for customers that have the convenience to choose among a ton of stores without leaving the sofa, however, such amazing freedom brings a huge challenge to companies to be more innovative in order to attract new customers and keep the old customers engaged. Hence, it is safe to say that a company’s capability to enlarge its number of clients has a significant relationship to its growth of sales. Nevertheless, just expanding the customer base is not enough since it would not meet its ability to drive sales. Furthermore, it's crucial to understand customer's behavior in order to make actionable decisions and support your business to grow, keep, and acquire the right consumers.
In this project, we are going to use a UCI data set that contains sales transactions of an online retail store based in the UK occurring between December 2010 and December 2011, the customer base of the company is mainly wholesale retailers. 
First, we are going to have a look at the data and see if we will need to perform any transformation in the data set as well as to get some insights from our customer base.

SCREENSHOT OF DATA SUMMARY:




Insights
The data set contains 8 columns and 541,909 rows.
The variables CustomerId and Description are the ones with the highest number of missing values.
Around 75% of the products cost  4.13 pounds or less and the most expensive product cost 38,970 pounds.

Data Cleaning
As we can see above the variable CustomerID need to be converted into character and the missing values needs to be handled, for this project we are going to drop all the rows which contain missing values, but bear in mind that you might need to solve them in another way depending on the purpose and impact of your project.





Data Exploration




Top 10 Countries with the Highest Volume of Purchases


Insights
We can observe that sales have been increased at the end of the year, this can be explained by the holiday season, where the demand for gift products is higher due to Christmas.
 World War 2 gliders are the most sold product.
The majority of the purchases are made in the UK, which makes sense since the product supplies reach faster and products’ deliveries are reliable within the same region.


Cohort Analysis
A cohort can be defined as a group of people that have similar characteristics.
Cohort analysis is a behavioral analysis where you group your customers based on their similarities to better understand their activities. Cohort analysis enables businesses to reduce churn and improve revenue by asking more precise questions and making data-driven decisions.
For the purpose of this project we are looking to answer the following questions:
Who are the customers engaging with the store throughout the year and who isn’t?
When do they churn? Can we identify/predict it?
What are the actions we can take to minimize customers chun?

For cohort analysis, we are going to add 3 extra columns to the dataset:
Invoice Month: A representation of the month and year of the transaction
Cohort Month: A month and year of a customer’s first purchase. This will be the same across all invoices for a particular customer.
Cohort Index: A representation of a customer's stage in its “lifetime”. This number describes how many months have passed since their first purchase.


This will enable us to build a retention table that will answer our initial questions and help us to understand how customers are throughout the year.







As we can see above this store is having some issues keeping their customers, on the next steps we will look at some techniques to help companies to identify valuable customers and take actions to prevent churn.

Customer segmentation using RFM (Recency, Frequency, Monetary) analysis.

What is FRM?
RFM model combines three different customer attributes to rank customers: Recency, Frequency, Monetary. It can be used for behavioral segmentation, grouping the customers based on their previous purchase.

Behavioral segmentation helps managers to identify valuable customers who are more profitable for the business. For example, which customers are buying expensive products but only one time and which are buying more frequently. Based on these findings, managers can decide which marketing campaign will be more effective for each group of customers.

In this dataset, we noticed that most of the customers are located in the UK, therefore, we decide only segmen UK customers.

                                                                                                                                                                                                                                           
Columns required 
We only needed 5 columns for this analysis; CustomerID, InvoiceDate, InvoiceNo, Quantity, and UnitPrice described as:

CustomerId: is needed to uniquely define the customer, 
InvoiceDate: helped to calculate recency of purchase,
InvoiceNo: we could count the number of time transaction were performed(frequency), 
Quantity: purchased in each transaction 
UnitPrice: of each unit purchased by the customer helped us to calculate the total purchased amount.

RFM Analysis 
We have used the following definitions in order to calculate recency, Frequency, and  Monetary values for each customer.
Recency — Calculate the number of days between the current date and date of last purchase each customer
Frequency —Calculate the number of transactions made over a given period for each customer
Monetary — Calculate the sum of money spent over a given period of time for each customer



Apply RFM Scores
Once we have RFM values from the purchase history, we assign a score from one to four to recency, frequency, and monetary values individually for each customer, this rank can be used to segment the customers into different groups. For this analysis, we used Quintiles as a method of ranking the RFM values on a scale of 1 to 4. 




Customers with the lowest recency, highest frequency and monetary amounts considered as top customers.



These scores are then used as inputs for clustering algorithms in order to group customers.








Business recommendation:
Here are some suggestions for business managers based on the RFM score and some possible actions they might take into account:


Score
Customer Segment
Activity
Action
111
Most valuable
Bought recently, buy often and spend the most
Reward them. Can be early adopters for new products. Will promote your brand.
311
Potential Loyalist
Recent customers, but spent a good amount and bought more than once.
Offer membership/loyalty programs, recommend other products.
324


Promising
Recent shoppers, but haven’t spent much.
Create brand awareness, offer free trials
411
At Risk	
Spent big money and purchased often. But a long time ago. Need to bring them back.
Send personalized emails to reconnect, offer renewals, provide helpful resources.



Clustering
In order to group the customers of our dataset, we are going to use an unsupervised machine learning technique called K-means which group similar data points and identify underlying patterns. To achieve that, K-means looks for a fixed number k of clusters (groups) in a dataset.
There are different ways to find the number of K for Kmeans clustering. Here we used the elbow method. The Elbow method plots the explained variation as a function of the number of clusters and picks the elbow of the curve as the number of clusters to use


From the above elbow graph, we can select 3 as our k value, which will be the number of clusters in our Kmeans model.


Insights
Most of the customers were assigned to cluster 1, where the median of a unit price is 7.2 pounds.
The cluster with fewer customers is the one with the highest unit price.






Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
