# Ethereum Anomaly Detection and Analysis

![Alt Text](./images/_07947a30-b034-45c6-b688-3102c2a63203.png)




## Problem Statement 
### Identifying Anomolous Ethereum Address through Transaction Analysis 

This project will develop a clustering model to identify Ethereum addresses that exhibits increased transaction volume prior to significant price changes. Smart-contract usage will be analyzed. The hope is to be able to create actionable insights and patterns to recognize when the market is particularly volatile.

## Dataset
The dataset will consist of Ethereum transaction data, including Ethereum addresses, timestamps, transaction volumes, and corresponding prices over a specified time period. The transactions were scraped through etherscan.io and are full transaction reports of individual addresses.

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

## Preprocessing 

* Cleaning
    * Imputation of nulls *
    * Changing of data types *
    * Converting hexadecimal to decimal *

* Feature Engineering
    * Creation of hour column *
    * Creation of change of eth price column *
    * Creation of leading change column
    * Creation of reduced transactions per day *
    * Strech goal: include into the clustering a success (or high-growth) of the address

* EDA
    * Strech Goal: Understanding PCA
        * PCA visualizer
    * Analyze time zone Activity
        * What time of day are most people trading? *
        * What time do smart contracts trade?
        * What time of day is the market most volatile *
    * Contract popularity
        * What is most popular and why?
        * 
    * Pulling key features from a more generalized clustering model
    * Gas price/usage analysis
    * Strech goal: incorporate a news sentiment metric into clusterings
        * https://rapidapi.com/bruceowenga-771Y05KlODq/api/crypto-news-api2/



standard deviation movement
flesh out criteria for volitility



## Clustering
Create DBscan model to identify clusters associated with large changes in price.

## Model Evaluation
Target metric will be silhouette score.
Silhouette plot() maybe a heatmap

## Stretch goal: Deploying a monitoring system looking for similar selected clustered scenarios
only realistically possible if the most successful(hopefully selling before price drops), are within the extremes of the n-dimensional space

## Conclusion
* analyze the pros and cons of the clusters created.
* summarize other behavioral insights
