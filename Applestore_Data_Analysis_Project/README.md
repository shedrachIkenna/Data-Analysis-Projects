# Applestore Data Analysis

## Introduction
The primary objective of carrying out a Data Analysis on the applestore dataset is to gain insights into the mobile apps market by exploring features such as app genres, pricing trends, user ratings and more.
By identifying relationships between variables, I was able to uncover patterns, identify outliers and uncover meaningful conclusions. 

## Data Source
This [dataset](https://www.kaggle.com/datasets/ramamet4/app-store-apple-data-set-10k-apps) was obtained from [Kaggle](https://www.kaggle.com) which is a popular and reliable data source for data science and machine learning enthusiasts. The dataset is quite old and hasn't been update for while but it provided an opportunity to showcase my EDA skills. The dataset comes in a .csv file format. I downloaded it, imported it into a database in Microsoft Sql Server Management Studio for analysis.

## Tool Used 
* Microsoft Sql Server Management Studio (SSMS)

## Project Goals
The primary goal of this project is to gain valuable insights into the mobile app market and user preferences within the ios ecosystem.
My aim is to uncover meaningfull patterns, trends and relationships that can aid in both understanding and answering question like
* Do paid apps have higher user ratings than free apps?
* Do apps with multiple language support have higher user ratings?
* Is there a correlation between the lenght of app description and user ratings?
* Whats the average user ratings for each app genre?
* What are the top rated apps for each genre?

By effectively answering the above questions, I will be able to provide actionable insights and data-driven recommendations for app developers, marketers and stakeholders in the iOS app ecosystem. This analysis can lead to informed decision making, strategic planning and ultimately contribute to the success of apps in the competitive mobile app market

## Data Exploration and Data Cleaning
The dataset contained 7197 rows and 16 columns. The goal here was to identify and correct errors, incosistencies and inaccuracies in the dataset to ensure that the data is accurate, complete and reliable. 
* Check for missing values in 'key' fields of AppleStore table
  ```sql
  SELECT 
    COUNT(*) AS MissingValues 
  FROM PortfolioProject..AppleStore
  Where track_name is Null OR user_rating is Null OR prime_genre is null
  ```

    | MissingValues |
  |-------------------|
  | 0             |
  
* Check for missing values in key fields of appleStore_description table
  ```sql
  Select
    Count(*) as MissingValues 
  from PortfolioProject..appleStore_description 
  Where app_desc is Null

  ```

  | MissingValues |
  |-------------------|
  | 0             |


* Check for duplicates in both AppleStore and appleStore_description tables
  Since there are 7197 rows, the count of unique ids also must be 7197 otherwise, that row is considered a duplicate
  ```sql
  SELECT 
  	COUNT(DISTINCT id) AS UniqueIds
  FROM PortfolioProject..AppleStore
  ```

  | UniqueIds |
  |-------------|
  | 7197 |

    ```sql
  SELECT 
  	COUNT(DISTINCT id) AS UniqueIds
  FROM PortfolioProject..appleStore_description
  ```

  | UniqueIds |
  |-------------|
  | 7197 |

## Data Analysis
Just as stated in the project goals, data analysis of this dataset aims to provide actionable insights and data-driven recommendations for app developers, marketers and stakeholders in the iOS app ecosystem by anwering the following questions
* Do paid apps have higher user ratings than free apps?
* Do apps with multiple language support have higher user ratings?
* Is there a correlation between the lenght of app description and user ratings?
* Whats the average user ratings for each app genre?
* What are the top rated apps for each genre?

The solutions to these questions are found [here](https://github.com/shedrachIkenna/Data-Analysis-Projects/blob/master/Applestore_Data_Analysis_Project/applestore.md)

## Key Findings
After analysing this Applestore dataset, severeal key findings emerged that revealed that: 
* Paid apps generally have better ratings compared to free apps
* Apps supporting between 10 and 30 languages have better ratings
* Finance and Book apps have low ratings
* Apps with a longer description have better ratings
* Game and entertainment app genre have high competition

## Recommendations 
* If you are an app developer or stakeholder in the iOS development industry and your app is perceived as having high value and quality, the data analysis indicates that paid apps tend to receive higher user ratings than free ones. It may be worthwhile to charge a fee for your app to capitalize on its positive reception and potentially increase its ratings.
* The data analysis shows that apps that support between 10 and 30 languages have higher ratings. Therefore, it's not about the number of languages your app supports, but focusing on the right ones.
* It is likely that user needs are not fully met in genres such as Finance and Books. As a result, there is potential for a high user rating and penetration with very low competition if you can create quality apps in this genre that address users' needs better than the current market apps.
* The length of the app description has a positive correlation with the user ratings. This means that users appreciate detailed and clear descriptions that help them understand an app's features and capabilities before they decide to download it. So, taking the time to craft a comprehensive and well-explained app description can lead to happier users, which in turn, may boost your app's ratings and satisfaction level.
* On average, all the apps have a rating of 3.5 so aiming for a user rating above the average of 3.5 is a wise strategy to stand out from the crowd. Since the average rating is 3.5, achieving a higher rating indicates that users find your app to be above average and more satisfying than the majority of apps.
