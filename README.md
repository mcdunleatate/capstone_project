# Ethereum Anomaly Detection and Analysis

![Alt Text](./images/_07947a30-b034-45c6-b688-3102c2a63203.png)




## Problem Statement 
### Identifying Anomolous Ethereum Address through Transaction Analysis 

This project will develop a clustering model to identify Ethereum addresses that exhibits increased transaction volume prior to significant price changes. Smart-contract usage will be analyzed. The hope is to be able to create actionable insights and patterns to recognize when the market is particularly volatile.

## data_collection

### Data Sources

1. **Arkham Intelligence:**
   - Ethereum addresses of interest are identified using Arkham Intelligence.

2. **Etherscan.io API:**
   - Utilized to collect detailed information about transactions associated with each Ethereum address.
   - The data is collected in two stages to optimize efficiency.

3. **Yahoo Finance API:**
   - Employed to retrieve historical values of Ethereum.
### Data Dictionary

#### This corresponds to eth_trans_data_clean.csv

| Column Name         | Data Type          | Description |
|------------|-----------------|---------|
| blockNumber          | int64              | The number assigned to a block in the blockchain. |
| timeStamp            | int64           | The timestamp of the block in Unix timestamp format (seconds since the epoch). |
| hash               | object             | A unique identifier for the block, represented by a cryptographic hash. |
| nonce                | int64           | A number used in the process of mining a block. |
| blockHash       | object             | The cryptographic hash of all the transactions in the block. |
| transactionIndex     | int64           | The index of the transaction within the block. |
| from                 | object             | The address that initiated the transaction (sender). |
| to             | object             | The destination address of the transaction (recipient). |
| value                | float64            | The amount of cryptocurrency (in Wei) transferred in the transaction. |
| gasPrice        | int64              | The price paid per unit of gas in Wei. |
| isError              | int64            | A flag indicating whether the transaction encountered an error (0 for success, 1 for error). |
| input  | object           | The input data of the transaction, usually containing encoded function calls for smart contracts. |
| contractAddress   | float64  | The address of the smart contract if the transaction is interacting with a contract (NaN if not applicable). |
| cumulativeGasUsed   | int64          | The total amount of gas used by all transactions in the block up to this one. |
| gasUsed      | int64            | The amount of gas used by this specific transaction. |
| confirmations    | int64             | The number of confirmations received for the block. |
| methodId       | object            | The signature for a smart contract function. |
| functionName       | object         | The name of the function associated with the methodId (if applicable). |
| dateTime    | datetime64[ns]     | The datetime of the transaction. |
| timeOnly           | object          | The time component extracted from the datetime. |
| dateOnly         | object            | The date component extracted from the datetime. |
| hoursOftheday | int64         | The hour of the day when the transaction occurred. |
| ethValusd       | float64        | The Ethereum value in USD. |
| volatility          | float64       | A measure of volatility |
| dayChange        | float64 | The change in value over the day. |
| perc75_Neg          | float64       | Negative changes corresponding with volatility in the 75th percentile |
| valueUSD         | float64          | The value of the transaction in USD. |


## cleaning_and_feature_engineering

This notebook focuses on the cleaning and feature engineering steps in preparing the dataset for Ethereum price prediction. Key processes include lagging the closing prices, calculating daily price changes (dayChange), measuring volatility, and creating additional features such as 'perc75_Neg' to identify addresses with better predictive capabilities.

#### 1. Lagging Closing Prices

   - Lag the closing price of Ethereum for the past 4 days.

#### 2. Calculating DayChange

   - Measure the daily change in Ethereum closing prices.

#### 3. Calculating Volatility

   - Compute volatility, representing the variance over the past 4 days.

#### 4. Creating perc75_Neg Columns

   - Identify addresses with high volatility in the top 75 percentile and predict future changes.

#### 5. Mapping Information to Transactions

   - Map the engineered features onto each Ethereum transaction.

#### 6. Mapping Transaction Frequency

   -  Map transaction frequency onto the price per day dataframe.

#### 7. Abandom Ship Metric

   -  A sum of the days that include perc75_Neg flags.

## EDA - (Pre-Clustering EDA)
This notebook conducts an Exploratory Data Analysis (EDA) on Ethereum transactions to gain insights into various aspects of the data.

### Analysis Highlights

#### 1. Analysis of Transaction Value Over Years

   - The analysis of transaction value over the years revealed significant skewness due to a single address making substantial transactions, impacting the overall distribution.

#### 2. Analysis of Gas Price Over Time

   - Gas price analysis did not reveal any particularly notable trends; however, it showed a general increase in gas prices with a high volume of transactions.

#### 3. Analysis of Time of Day for Transactions

   - Distinguished time-of-day patterns were observed for contract and non-contract transactions. Contract transactions tend to occur more frequently during the beginning or end of the day (UTC), while non-contract transactions are more prominent around midday.

#### 4. Analysis of Ethereum Price Over Time

   - The analysis of Ethereum price over time, including volatility, indicated a generally high volatility. Notably, volatility surged around periods of high transaction volume.

#### 5. 'Abandon Ship' Metric Analysis

   - Attempted to identify addresses making the most transactions just before a significant price drop. This was mostly unsuccessful because it just showed addresses that made a lot of trades.


## modeling (Clustering)

1. **Objective:**
   - Create a DBSCAN clustering based on every transaction utilizing PCA for dimensionality reduction.

2. **Features:**
   - ['timeStamp', 'valueUSD', 'volatility', 'ethValusd', 'perc75_Neg_lag1', 'perc75_Neg_lag2', 'perc75_Neg_lag3', 'get_out_metric']

3. **Silhouette Score:**
   - Achieved a silhouette score of 0.42.

## Clustering Based on Transactions Per Day

1. **Objective:**
   - Create a DBSCAN clustering based on the number of transactions per day.

2. **Features:**
   - ['Close', 'volatility', 'perc75_Neg'] along with the number of transactions for each address assigned to a particular day.

3. **Silhouette Score:**
   - Achieved a silhouette score of 0.36.


## Conclusion 
This project aimed to identify unique Ethereum addresses through a robust clustering model, utilizing data from Arkham Intelligence, Etherscan.io API, and Yahoo Finance API. Cleaning and analysis revealed two addresses adept at selling before price drops, and clusters with a knack for buying before price hikes. While the 'Abandon Ship' metric faced challenges, this research provides actionable insights for traders navigating market volatility.Looking ahead, future endeavors could focus on fine-tuning clustering techniques and establishing a monitoring system for high-performance addresses. Furthermore, the development of an application designed to autonomously seek new high-performing addresses would fortify the model's proactive capabilities, enhancing its adeptness in identifying valuable opportunities within the Ethereum market.
