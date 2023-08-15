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


## Data Cleaning and Exploration 
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

Note that I copied my dataset into another variable df_main to get rid of some warning errors jupyter notebook was throwing at me 
```python 
df_main[['debit', 'credit']] = df_main[['debit', 'credit']].fillna(0)
```

#### Step 4: Format Date 
I had to ensure that the date and value date columns were formatted properly. 
```
df_main.info
```
Showed information about the datatypes associated with every column. 
I converted that date and date value column from object data type to date datatype 
```python 
df_main['date'] = pd.to_datetime(df_main['date'], format='%d/%m/%Y')
df_main['value date'] = pd.to_datetime(df_main['value date'], format='%d/%m/%Y')
```
#### Step 5: Categorize Transactions 
I created a new column for transaction categories based on keywords for the description column as this categorization will later help us in understanding spending patterns. 

Using the np.where() function from the NumPy library, I was able to apply a condition which categorizes transactions based on certain keywords found in the transaction's description. I created the following transaction categories:
- Bank Charges
- Airtime
- Eat outs
- Digital Wallets
- Rent
- My baby
- Dt
- Selfcare
- Cash deposit
- Enike
- Mom 
- Dad
- Aunty Helen 
- Side business
- Fines
- Caleb


```python
# Bank Charge

df_main['category'] = np.where(df_main['description'].str.contains(
    'vat|electronic money transfer levy|sms notification charge|sms notification charge|visa card maintenance fee'), 
    'Bank charge', df_main['category'] )
    
# Airtime

df_main['category'] = np.where(df_main['description'].str.contains(
    'mtn|airtel|9mobile|08039646573'), 
    'Airtime', df_main['category'] )
                               
#Eat Outs

df_main['category'] = np.where(df_main['description'].str.contains(
    'yum delivery|yum\ndelivery|hasina confectionery|stone\ncastlerestaurant|/henry\nadebayo/fcmb/sheddy'), 
    'Eat outs', df_main['category'] )

#SelfCare

df_main['category'] = np.where(df_main['description'].str.contains(
    'chukwubueze paschal\nugwumba/opay|paystack|chukwubueze paschal|abdulsamad ayobami|chikwendu|ibrahim yakubu'), 
    'Selfcare', df_main['category'] )

#Digital Wallets

df_main['category'] = np.where(df_main['description'].str.contains(
    'shedrach\nnwali/gomon|ikenna\nshedrach/kuda|gomon'), 
    'Digital Wallets', df_main['category'] )

#My baby

df_main['category'] = np.where(df_main['description'].str.contains(
    'yunusa sarah\njenebu/gtb|yunusa sarah jenebu|khadija/gtb|jenebu'), 
    'My baby', df_main['category'] )

# DT

df_main['category'] = np.where(df_main['description'].str.contains(
    'daniel tolani|olorunyomi'), 
    'DT', df_main['category'] )

# Enike

df_main['category'] = np.where(df_main['description'].str.contains(
    'enike braimoh|enike\nbraimoh'), 
    'enike braimoh', df_main['category'] )

# Mom

df_main['category'] = np.where(df_main['description'].str.contains(
    'blessing\nnwali|blessing nwali'), 
    'Mom', df_main['category'] )

# Aunty Helen

df_main['category'] = np.where(df_main['description'].str.contains(
    'helen chicka'), 
    'Aunty Helen', df_main['category'] )


# Dad

df_main['category'] = np.where(df_main['description'].str.contains(
    'nwali\nedwin'), 
    'Dad', df_main['category'] )


# Rent

df_main['category'] = np.where(df_main['description'].str.contains(
    'ibrahim sule'), 
    'Rent', df_main['category'] )

# Cash deposit

df_main['category'] = np.where(df_main['description'].str.contains(
    'shago-//tunde'), 
    'Cash deposit', df_main['category'] )

# Side business

df_main['category'] = np.where(df_main['description'].str.contains(
    'rolez/baxi---/bax_trsf_|nip/capri/cdl|/capri/cdl/copper|usaini nasiru|onyedika elias|cash/trf/045rnbe02251681035150766'), 
    'Day Job', df_main['category'] )

# Fines

df_main['category'] = np.where(df_main['description'].str.contains(
    'george imeiba'), 
    'Fines & Dues', df_main['category'] )

# Caleb

df_main['category'] = np.where(df_main['description'].str.contains(
    'caleb amowomani'), 
    'caleb', df_main['category'] )


```

## Data Analysis
The goal of performing this Bank Statement Data Analysis is to find some useful insights and tips for managing my money better. We can do this by exploring these key questions which where outlined earlier in the project goals 

* Are there specific spending categories that dominate my transactions?
* What are my most recurring transaction types?
* Is there a correlation between the size of transactions and the day of the week?
* How does my account balance fluctuate throughout the month??
* Are there any notable anomalies or outliers in my financial activities?

The solutions to these questions are found [here](https://github.com/shedrachIkenna/Data-Analysis-Projects/blob/master/Bank_Statement_Analysis/Bank%20Statement%20Analysis.ipynb)


## Key Findings
After analysing the Bank Statements, severeal key findings emerged that revealed that: 
* 32% of my total debits was money sent to my Digital Wallets which is where I save
* Friday is the day I've spent the most money
* March recorded the highest aggregate debits, signifying the peak of total debit transactions within the analyzed period
* Bank charges stood out as the most frequent debits occuring 95 times.
* There were some notable outliers. I identified that five data points exceeded the upper bounds(std dev) which implies that they were potential outliers. But, upon thorough examinations, I noticed that these outliers are accurate and valid representation of the underlying data. Given their significance and authenticity, I made an informed decision to retain these outliers within the scope of my analysis. This approach ensures that the analysis encompasses the full range of data, including these exceptional instances that provides valuable insights into the dataset


## Recommendations 
#### Digital Wallet Management:
* Given that a significant portion of total debits (32%) is directed towards Digital Wallets, it is advisable to continue utilizing these platforms for efficient savings and financial transactions. Also, regular monitoring the Digital Wallet activity to ensure that funds are being used effectively and also aligns with financial goals.

#### Spending on Fridays:
* With Friday identified as the day of highest spending, consider allocating a specific budget for Fridays to better manage spendings. Implementing a budgeting strategy can help curb excessive spending on this day which also contributes to better financial discipline.

#### Monthly Debit Patterns:
* The observation of March recording the highest aggregate debits signifies a potential seasonality in spending. Monitor spending patterns across different months to identify any recurring trends. Adjust budgeting and financial plans accordingly to accommodate months with higher spending.

#### Understanding Bank Charges:
* The prominence of bank charges, occurring 95 times, suggests the significance of these debits. Carefully review the nature of these charges and consider investigating ways to minimize them. Engage with the bank to gain clarity on the types of charges incurred and explore potential options for reducing their frequency.

#### Handling Outliers:
* The identification of potential outliers is crucial to maintaining data integrity. The decision to retain verified outliers within the analysis is commendable, as it ensures a comprehensive understanding of the dataset. 

#### Data Quality Assurance:
* To ensure accurate and reliable analyses in the future, prioritize data quality. Regularly perform data validation checks and preprocessing steps to identify and rectify any anomalies or inaccuracies in the dataset. This will enhance the credibility of your analyses and the insights derived from them.


## Visualizing Bank Statement Insights
In the endeavor to communicate the outcomes derived from the Bank Statement Analysis project, I harnessed the power of Tableau to construct interactive and visually compelling visualizations. These visualizations stand as effective tools for presenting key findings, facilitating data comprehension and interpretation.

You can explore the interactive dashboard by following this [link](https://public.tableau.com/app/profile/shedrach.nwali/viz/FinancialAccountAnalysis/Dashboard1).

Below, you can find a snapshot of one of the visualizations created to provide a glimpse into the insights gained:
![Dashboard](visualization/Dashboard_snapshot.png)

Bank Statement Analysis Visualization

Notably, it's important to mention that due to the intricacies of the data and the depth of insights, a subset of the visualizations was chosen for inclusion in the Tableau dashboard. This decision was made to ensure a coherent and streamlined experience for viewers, avoiding overwhelming complexity.

Additionally, please note that while Tableau provides a powerful platform for visualization, the complete range of visualizations, including those that might have caused the dashboard to be congested, were crafted using Python within a Jupyter Notebook environment. This comprehensive approach allowed for a detailed exploration of insights that might not have been feasible solely within Tableau.
