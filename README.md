#### Capstone Project Analysis <u/> 
### Customers Sales Data Analysis
## Table of Contents
- [Customers Sales Data Analysis](#customers-sales-data-analysis)
- [Introduction ](#introduction)
- [Data overview](#data-overview)
- [Basic Statistics of Dataset](basic-statistics-of-dataset)
- [Analytical approach](#analytical-approach)
- [Dashboard And Tables Overview](dashboard-and-tables-overview)
- [Exploratory Data Analysis](exploratory-data-analysis)
- [Key insights](#key-insights)
- [Recommendations](#recommendations)
- [Conclusion](#conclusion)
  
### Introduction 

### *1. Summary*

This project involves analyzing customer data for a subscription service to identify segments and trends. The goal is to understand customer behavior, track subscription types, and identify key trends in cancellations and renewals.The final deliverable is a Power BI dashboard that present Insight to inform strategic decisions in optimizing growth, reducing subscription cancelation, and improving revenue.

---

### Data Overview

The dataset includes the following fields:
- *Customer Name*: Identifies the customer.
- *Customer ID*: Unique identifier for each customer.
- *Subscription Start Date*: The start date of the subscription.
- *Subscription End Date*: The end date of the subscription.
- *Subscription Duration*: Length of the subscription in days.
- *Region*: Geographical location of the customer.
- *Canceled*: Indicates the state of subscription using True/False.
- *Revenue*: The total revenue generated by each customer.

---
### Basic Statistics of Dataset

* Total Revenue/sales:68,000,000
* Total number of customer:33787
* Number of regions: 4
* Number of Subscription type category:3

---

### Analytical Approach

#### *Data Collection*
The dataset for the analysis was provided by the incubator Hub,an orgainization built to train and support women in technology.The data was provided in excel workbook format for easy accessibility.

#### *Data manipulation*
- *Data Cleaning*:
   .Removed duplicates entry in excel and checkedfor speling errors and blank cells to ensure data quality.
- *Data Transformation*
   .Ensured all data fields were assigned correctly with the date field formatted to date formats.
   . Created new columns:
     - Cancelation Rate: Using conditional Formation in Power Bi a column cancelation rate was created to enable manipulation of the data contained in the canceled column.
     - Subscription Duration: Extracted the duration between subscription start date and subscription end data by using the add column button and finding the difference between the two 
       dates.
### *Tools Used*
- Microsoft Excel for data cleaning and analysis using pivot table.[Download Here](https://www.microsoft.com)
- SQL For querying of data.
- POWERBI for data visualization.

---

### Dashboard And Tables Overview

#### EXCEL TABLE

#### SQL TABLE

#### POWER BI

![Customerdatadash](https://github.com/user-attachments/assets/ded95d1b-e494-490e-8d5c-477ada58ba39)

![Customers Data Dash](https://github.com/user-attachments/assets/6377977f-ec9a-4a00-9923-79a63ac3d25c)

---

### Exploratory Data Analysis

SQL QUERY OVERVIEW

This is an overview of query language used to generate dataset from the customer subscription data. 
```SQL
create database customerdata

-1. Total number of customers from each region.

SELECT Region, COUNT(CustomerID) AS TotalCustomers
FROM dbo.[cust data]
GROUP BY Region;
-2. Most popular subscription type by the number of customers.

SELECT Top (1) SubscriptionType, COUNT(CustomerID) AS MostPopularSubscriptionType
FROM dbo.[cust data]
GROUP BY SubscriptionType
ORDER BY MostPopularSubscriptionType DESC
-3.Customers who canceled their subscription within 6 months.-

SELECT CustomerName, SubscriptionStart, SubscriptionEnd
FROM dbo.[cust data]
WHERE Subscription_Duration <= 180
-4. --Average subscription duration for all customers.

SELECT customername ,AVG(subscription_duration)as avgsubscription_duration
from dbo.[cust data]
group by customername
-5. find customers with subscriptions longer than 12 months.

SELECT CustomerID ,CustomerName, Subscription_Duration
FROM dbo.[cust data]
WHERE Subscription_Duration > 365;

-6. Total revenue by subscription type.--

SELECT SubscriptionType, SUM(Revenue) AS TotalRevenue
FROM dbo.[cust data]
GROUP BY SubscriptionType
ORDER BY TotalRevenue DESC

-7. Top 3 regions by subscription cancellations.

SELECT  Top (3) Region, COUNT(Cancelation_Rate) AS Cancellations
FROM dbo.[cust data] WHERE Canceled = 'TRUE'
GROUP BY Region
ORDER BY Cancellations DESC;

-8. find the total number of active and canceled subscriptions.

SELECT
    SUM(CASE WHEN Canceled = 'TRUE' THEN 1 ELSE 0 END) AS TotalCanceled,
    SUM(CASE WHEN Canceled = 'FALSE' THEN 1 ELSE 0 END) AS TotalActive
   FROM dbo.[cust data].
```
---

### Key Insights

#### *customers insight*



![count pivot](https://github.com/user-attachments/assets/cb10bac1-7fb1-46e3-8e54-33977e4ed199)

- Customers with a total count of 8488 in the east region subscribe to the basic package only.
- Customers with a total count of 8466 from the south region are subscribed to the premium package only.
- Customers from the north region with a total count of 8433 are subscribed to the basic package only
- Customers from the west with a total count of 8420 are subscribed to the standard package.
This shows that most populated subscription type is the basic package.It also suggests that the north and east region have a lower standard of living compared to the south and west region whose subscription type is the standard and premium package.

#### *Sales Optimization*

![region pivot](https://github.com/user-attachments/assets/5132eaf7-e879-4d6d-bde3-355f136f31c2)

- The total revenue generated from all region is a sum of 67,540,175.
- The East Region contributes a total of 16,958,783 to the sum total revenue.
- The North Region contributes a total of 16,817,972 to the sum total revenue.
- The South Region contributes a total of 16,899,064 to the sum total revenue.
- The west Region contributes a total of 16,864,376 to the sum total revenue.

#### *Revenue by Subscription Type*

![sub type](https://github.com/user-attachments/assets/39eba708-7865-44d7-9c73-32af6aa84768)

The basic subscribers contributes a total of 33,776,735 to the total revenue.
The premium subscribers contributes a total of 16,899,064 to the total revenue.
the standard subscribers contributes a total of 16,864,376 to the total revenue.

This indicates that the region contributing the largest amount to the total revenue is the east region.The east region consist of only basic subscribers,also the subscribers contributing the  largest part to the total revnue originates from the basic subscription package.This suggest that the basic subsription is well structed to suits the basic customer base.

#### *Subscription Duration & Retention*

-33.39% of basic subscribers cancelled their subscription.
-33.37% of premium subscribers cancelled their subscription.
-33.24% of standard subscribers cancelled their subscription.

 High cancellation rates could indicate dissatisfaction with the product, price sensitivity, or competitive pressure. It is important to Perform root cause analysis on why users are canceling subscriptions—this could include surveys, follow-up emails, or exit interviews with customers.

---

### Recommendations

#### *Improve Customer Retention*
- *Action*: Introduce targeted retention initiatives such as regular check-ins, proactive support, and loyalty incentives (e.g., discounts for long-term subscribers).
- *Action*: Offer customized solutions or tailored pricing models based on customer needs, especially for larger organizations or long-term users.

#### *Optimize Subscription Pricing*
- *Action*: Evaluate the pricing model to aligned with customer expectations in different regions. Introducing additional features for higher-paying customers could increase retention and revenue.
  
#### *Region-Specific Marketing*
- *Action*: Invest in region-specific marketing strategies.

#### *Address Cancellation Drivers*
- *Action*: Investigate the reasons behind cancellations (e.g., pricing, competition, product issues) and address them directly through product enhancements or customer engagement strategies.
  
---

### Conclusion

The dataset provides valuable insights into Customers data subscription trends, cancellations, and revenue generation. By focusing on improving customer retention, optimizing pricing, and addressing regional challenges, the service provider can also  better position itself for sustainable growth and profitability. Future analysis should continue to track subscription trends over time, with an emphasis on mitigating churn and improving long-term engagement.







   


  


