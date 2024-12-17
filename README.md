# Documentation: Crude Oil Price Forecasting Using Prophet
## ***Introduction***
This project aims to forecast the future price movements of crude oil using historical data. We leverage Yahoo Finance (yfinance) to obtain 10 years of crude oil price data, clean and analyze the data, and ultimately use the Prophet model by Facebook for forecasting.

***Libraries Used***
* yfinance: Fetch historical financial data.
* pandas: Data manipulation and cleaning.
* numpy: Numerical operations.
* matplotlib and seaborn: Visualization.
* prophet: Time series forecasting.
* sklearn.metrics: Model performance metrics.
* scipy.stats: Statistical analysis.
  
***Data Collection***
The dataset for crude oil prices is fetched using the yfinance library:
Fetchs historical data of crude oil prices for the last 10 years. The data contains columns such as Open, High, Low, Close, Volume, Dividends, and Stock Splits.
## EDA 
***Data Inspection***
Basic inspection of the data helps ensure its completeness and identify potential issues:
Dividends and Stock Splits are generally empty in our dataset, which is typical for commodities like crude oil.
Checking for duplicates ensures the dataset's integrity.
***Correlation Matrix***
A correlation matrix is calculated to understand relationships between various numerical columns (Open, High, Low, Close, Volume):
Key Observations from the Heatmap:

Open, High, Low, and Close Prices: These variables are highly correlated, which is expected since they represent the oil price at different times.
Volume: There's a moderate negative correlation between volume and price, suggesting that higher prices might correlate with lower trading volumes.
***Distribution of Crude Oil Prices***
The distribution of the Close prices is visualized using a histogram:


This gives an understanding of the frequency and spread of the closing prices. We observe that crude oil prices tend to fluctuate but maintain a general upward trend.

***Skewness and Kurtosis***
We calculate the skewness and kurtosis to understand the distribution shape of Close and Volume:

positive skew suggests a right-tail bias.
Kurtosis: Measures the "tailedness" of the distribution. High kurtosis indicates heavy tails.
Price Trends and Market Volatility
A time series plot helps visualize trends and volatility in the crude oil prices from 2015 to 2024. Key observations are:

2015-2018: Relatively stable prices with occasional fluctuations.
2018-2019: A significant decline, possibly due to market corrections or geopolitical events.
2019-2020: A sharp recovery, likely due to bullish sentiment.
2020-2021: Significant spike due to COVID-19's market impact.
2021-2024: Price stabilization with minor fluctuations.
The spike in 2020, tied to the COVID-19 pandemic, was influenced by a reduction in demand due to lockdowns and an oil price war between Saudi Arabia and Russia.

Volume Analysis
A similar analysis is done for the Volume variable. It reveals the following:

2015-2018: Stable volume with minor fluctuations.
2018-2020: Increase in volume likely due to rising market uncertainty and trading activity during the pandemic.
2020-2021: High trading volume persists due to continued volatility.
***Outlier Detection and Cleaning***
Outliers in the Close prices are identified using z-scores. Prices beyond a threshold of 2.7 are considered outliers and removed:


This results in a cleaner dataset with fewer extreme values that could skew the analysis.

***Visualizing the Cleaned Data***
Histograms and boxplots are used to compare the original and cleaned data distributions:


These plots show how the Close and Volume values change over time, helping to visualize trends and anomalies.
