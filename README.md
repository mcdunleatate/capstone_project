# capstone_project




# Goal 
## Identifying Anomolous Ethereum Address through Transaction Analysis 

The goal of this project is to develop a clustering model to identify Ethereum addresses that exhibit increased transaction volume prior to significant price changes. This will be separated by smartcontract transactions and non-smartcontract transactions. The hope is to be able to create actionable insights and patterns to recognize when the market is particularly volatile.

## Dataset
The dataset will consist of Ethereum transaction data, including Ethereum addresses, timestamps, transaction volumes, and corresponding prices over a specified time period. The transactions were scraped through etherscan.io and are full transaction reports of individual addresses.

### Data Dictionary

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
    * PCA
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
