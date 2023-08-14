# Bank Statement Analysis

## Introduction
The central goal of conducting a Bank Account Data Analysis project is to gain a comprehensive understanding of my personal money management habits through a indepth exploration of account transactions. We'll explore things like where I spend my money, how much I keep in my account, and more. By finding links between different financial details, we'll uncover interesting patterns and unusual things that might have happened. This project is all about helping me to better understand my finances by studying my bank account data and drawing important conclusions from it.


## Data Source
The dataset for this project is my personal bank statement which I downloaded as a PDF file from my bank's mobile app. It includes details of all my transactions between January 2023 to July 2023. Just like how Kaggle is a platform that provides datasets for data science enthusiasts, my bank statement serves as my personal dataset which we will dive into and explore for this analysis. Using this dataset also presents a perfect opportunity for showcasing my skills. 


## Tool Used 
* Microsoft Excel 
* Python using pandas, numpy, plotly, matplotlib
* Tableau 


## Project Goals
The core objective of this project is to obtain meaningful insights from my personal bank statement and discover patterns that showcases my financial behaviours and habits 

The project aims to address questions such as: 
* Are there specific spending categories that dominate my transactions?
* What are my most recurring transaction types?
* Is there a correlation between the size of transactions and the day of the week?
* How does my account balance fluctuate throughout the month??
* Are there any notable anomalies or outliers in my financial activities?

By answering these questions, we'll be able to uncover hidden connections within my financial data which will also provide a clearer view of my financial health, spending trends, and potential areas for optimization.  This project is driven by the aspiration to transform raw transactional data into actionable insights that can enhance my financial decision-making and guide future money management strategies 


Data Cleaning and Exploration 
Data in its raw form often carries imperfections that can obscure insights. Therefore, this is a crucial step in the process of this data analysis project because it plays a pivotal role in shaping the reliability and credibility of subsequent analysis. The primary objective here is to address these imperfections, ensuring that the dataset is accurate, consistent and ready for analysis. The following steps were used: 

#### Step 1: Import the Data
As stated earlier, I downloaded that data as a PDF file, then I used Microsoft Excel to extract and merge into one sheet using the power query editor. I then saved and exported the file as a .csv format for further cleaning. I imported the .csv file into jupyter notebook using the pandas library 

```python
import pandas as pd
df = pd.read_csv(r"C:\Users\DELL\Desktop\DataSets\Zenith_Bank_Statement.csv")
```

#### Step 2: Remove Duplicates 
This step was fairly easy. I had so first see the duplicates by running the code below
```python
df[df.duplicated(keep=False)]
```
I proceeded in dropping the duplicates
```python
df = df.drop_duplicates()
```

#### Step 3: Handle Missing Values
Missing values only appeared in the debit and credit columns. but, Looking at the dataset, I wouldn't say the values were missing, rather I would say they were empty. I would say this because each row represented either a debit or credit transaction, therefore, in a debit transaction row, we have only the debit value with and empty credit value and same goes for the credit transaction row.
I placed the empty values with zero
```python 
df_main[['debit', 'credit']] = df_main[['debit', 'credit']].fillna(0)
```
