# Amazon_Vine_Analysis

## Overview
In this project, I am tasked to analyze Amazon reviews written by members of the paid Amazon Vine program, a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. Companies that will pay a fee to Amazon and may provide free products to Vine members who are then required to publish a review. In order to determine if there is any bias towards favorable reviews from Vine members vs. non-members, we need to identify the percentage of 5 star ratings to total rating. 

As part of this exercise, we were asked to choose from 50 datasets that contain reviews of a specific product to extract, transform and load into a dataframe in order to complete our analysis. Next, I’ll use PySpark, Pandas, or SQL to determine if there is any bias toward favorable reviews from Vine members in my dataset. Lastly, I’ll write a summary of the analysis to submit to the SellBy stakeholders.

Of the 50 datasets, I chose to analyze reviews that were made by users in the "Health Personal Care" category.
*https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Health_Personal_Care_v1_00.tsv.gz*

## Purpose
- PySpark to extract the dataset, transform the data, connect to AWS RDS instance and load the transformed data into pgAdmin.
- Google Colaboratory to import PySpark libraries and connect to Postgres in order to create SQL tables and export the results.

## Objectives:
1. Define big data and describe the challenges associated with it.
2. Define Hadoop and name the main elements of its ecosystem.
3. Explain how MapReduce processes data.
4. Define Spark and explain how it processes data.
5. Describe how NLP collects and analyzes text data.
6. Explain how to use AWS Simple Storage Service (S3) and relational databases for basic cloud storage.
7. Complete an analysis of an Amazon customer review.

## Results

### PySpark ETL (Extract, Transform and Load)
**Extract** We can connect to data storage, then extract that data into a DataFrame. 
![Extraction](https://user-images.githubusercontent.com/68654746/192007358-4c6013bf-5f2c-465a-9d07-82318b9a13b0.jpg)

### *Findings*
From the Health Personal Care category, I've extracted **5,331,449 reviews**. 

**Transform** Now that the raw data stored in S3 is available in a PySpark DataFrame, we can perform our transformations in order to focus on reviews that would be considered more likely to be helpful and to avoid having division by zero errors later on.

Filter and create a new DataFrame to retrieve all the rows where the total_votes count is equal to or greater than 20.
![20+](https://user-images.githubusercontent.com/68654746/192008868-c26406ab-953a-4b39-8695-0a7b6f105bd6.jpg)

Filter and create a new DataFrame to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.
![50%](https://user-images.githubusercontent.com/68654746/192008886-1c6d0f9c-b5b3-4777-8ee5-73269a4989ff.jpg)

### *Analysis*
1. How many Vine reviews and non-Vine reviews were there?

From the tables below, there were 497 paid Vine reviews () versus 120,863 unpaid or non-Vine reviews. 

![paid](https://user-images.githubusercontent.com/68654746/192009661-b4903970-f2cf-41e9-bca9-f8892bce0eed.jpg)
![unpaid](https://user-images.githubusercontent.com/68654746/192009705-4c6d0b90-4a1d-4e2e-9c3c-2dc653ba003a.jpg)

2. How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?

From the findings shown below, there were 220 paid Vine reviews versus 74,470 unpaid non-Vine reviews that were 5 stars. 

![percentage](https://user-images.githubusercontent.com/68654746/192013367-29a14ff9-8d16-4e74-a060-bf2fc268f542.jpg)

3. What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

Percent of 5-Star reviews for paid Vine program was: 44.265594%

Percent of 5-star reviews for unpaid Vine program was: 61.615217%

## Summary

1. Is there is any positivity bias for reviews in the Vine program. 

Based on the results, Vine members did not show a bias when rating their products using the Vine program. The number of 5-star ratings for Vine members was about 17% less than Non-Vine members (44.3% vs. 61.6%). With this finding, we can assume that Vine customers are more critical when submitting their review for products in the Health Personal Care category.

2. Provide one additional analysis that you could do with the dataset to support your statement.

Another analysis to support my conclusion above, I would include all of the data provided in the dataset rather than filtering it down to a percentage of helpful votes. If we came to the same or close conclusion when utilizing all of the data, it would further support our predictions.
