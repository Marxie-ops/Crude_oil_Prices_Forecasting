# Documentation: Crude Oil Price Forecasting Forecasting with Prophet Using External Regressors
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

## ***Trend, Seasonal, and Residual Analysis of Crude Oil Prices (2015–2025)***
Trend Component 
The trend component shows the long-term direction of crude oil prices from 2015 to 2025. It reveals major structural movements over time:

2015 to 2020: Crude oil prices fluctuate between 20 and 80 USD, reflecting normal market conditions.
Mid-2020 Dip: A significant drop aligns with global COVID-19 lockdowns that reduced demand, caused supply chain disruptions, and led to oil production cutbacks.
Post-2020 Recovery: Prices spike from 2021 to 2022 due to the recovery in demand, persistent supply chain issues, and geopolitical instability.
Post-2022 Decline: Prices trend downward, influenced by changes in supply, inflation, and recession fears.
Seasonal Component (Green Oscillations)
The seasonal component captures the cyclical patterns inherent in the crude oil market. It highlights periodic fluctuations driven by regular supply and demand changes:

Repeating Cycles: Clear seasonal spikes occur, often associated with summer driving demand and winter heating needs.
Post-2022 Volatility: The seasonal volatility increases post-2022, likely due to supply chain disruptions and geopolitical risks, particularly the Russia-Ukraine war and OPEC+ policy changes.
Consistent Seasonality: Despite shocks, predictable seasonal patterns persist, but changes in demand elasticity are evident.
Residual Component (Red Noise)
The residual component accounts for the "unexpected shocks" or anomalies not explained by the trend or seasonal components:

Spikes (2015-2021): Significant volatility due to external factors like geopolitical conflicts (Middle East tensions, Libya), global events (COVID-19 pandemic), and market manipulations (OPEC+ decisions).
2024 Impact: The residual component also captures market volatility linked to political shifts, such as U.S. President Joe Biden's resignation and reelection bid, which contributed to market speculation and price uncertainty.

### ***Stationarity Check with Augmented Dickey-Fuller (ADF) Test***
The Augmented Dickey-Fuller (ADF) test is used to check whether the time series data is stationary, which is essential for effective time series modeling. Stationarity means that the statistical properties of the series (e.g., mean, variance) do not change over time. Here's the result of the ADF test on the Close prices of crude oil:
Since the test statistic does not fall below the critical value at the 5% significance level, the time series of crude oil prices is non-stationary.

## ***Key External Regressors Impacting Crude Oil Prices (2015–2025)***
The fluctuations in crude oil prices have been significantly influenced by several external factors. These regressors include:

* Geopolitical Factors:
Tensions and Conflicts: Conflicts in the Middle East, the Russia-Ukraine war, and instability in Libya have disrupted supply and added uncertainty to oil prices.
Sanctions: Sanctions on Iran, Venezuela, and Russia have led to a reduction in oil supply, causing volatility in prices.
* Economic Factors:
Global Economic Growth: Changes in global economic growth, particularly in emerging markets, directly impact oil demand.
Interest Rates and Inflation: Central bank monetary policies and inflation rates influence oil prices by affecting investment behavior and overall economic activity.
Exchange Rates: Currency fluctuations, especially in oil-producing countries, impact the global oil market.
* Supply and Demand Shocks:
OPEC+ Decisions: Changes in oil production targets by OPEC+ countries, such as production cuts, have caused significant price movements.
Natural Disasters and Political Instability: Events like hurricanes, pipeline disruptions, and political instability in oil-producing regions have led to supply disruptions and price spikes.
* Policy and Regulatory Factors:
Energy Policies: Government regulations, such as subsidies, taxes, and renewable energy investments, play a significant role in shaping oil market dynamics.
* Market Sentiment:
Investor Confidence: Financial market volatility and global economic uncertainty impact oil price fluctuations, especially in response to political events such as presidential elections and international trade negotiations.
 Performed correlation to see which regressors had alot of impact on the close prices and remained with just two:

***Strong Positive Correlations:***
* *Biden Policy Shift (0.77):* The positive correlation between Biden's policy changes and oil prices suggests that significant policy shifts, particularly those related to energy and environmental regulations, are likely to influence crude oil prices. For instance, the shift towards renewable energy or changes in oil extraction and production regulations under his administration may cause market reactions, driving prices up.
* 
***Strong Negative Correlations:***
*Shale Oil Impact (-0.49):** The negative correlation between shale oil production and oil prices indicates that as the U.S. expands its shale oil production (particularly in the 2015-2019 period), oil prices tend to decrease. The increase in domestic oil supply from shale production likely exerts downward pressure on global prices.

## ***Building The Prophet Model***
* **Key Steps** 
***Data Splitting***

* Training Data: The first 8 years of data (2015–2022) are used to train the model.
* Forecast Data: Data beyond the 8-year cutoff point is used for testing and forecasting.
A training_end_date is calculated dynamically using the pd.DateOffset() function.

***Defining Regressors***

* shale_oil_impact: A binary regressor (1/0) that captures the impact of U.S. shale oil production between 2015 and 2019.
* biden_policy_shift: A binary regressor (1/0) that accounts for the impact of policies during U.S. President Joe Biden’s administration from 2021 to 2024.
These regressors are included using the model.add_regressor() function in Prophet.

## ***Model Training***

The Prophet model is fitted to the training data, which includes both the time series values (ds, y) and the defined regressors.
Forecasting

A future dataframe is created using make_future_dataframe() for the specified forecast period.

The regressors (shale_oil_impact and biden_policy_shift) are defined in the future dataframe as binary values based on specific date ranges.

## ***Model Evaluation***

The model performance metrics provided suggest that the model is performing quite well based on several key evaluation metrics:

* MAE (Mean Absolute Error): 40.77
Interpretation: The average absolute difference between the predicted and actual values is approximately 40.77. Depending on the scale of your data (e.g., if the target variable is in the range of hundreds or thousands), this value could be considered acceptable or high. A lower MAE is generally better.

* RMSE (Root Mean Squared Error): 6.39
Interpretation: RMSE is a common metric to assess model accuracy, and it penalizes larger errors more due to the squaring of the residuals. A lower RMSE is preferable, and the fact that the RMSE is much smaller than the MAE suggests that there might not be many large prediction errors in your model, which is a positive sign. Given the context (whether the target values are large or small), this could indicate that your model is doing fairly well.

* MAPE (Mean Absolute Percentage Error): 8.91%
Interpretation: This is a very strong performance, as MAPE values under 10% are often seen as very good for many applications, particularly in time series forecasting. It suggests that, on average, your model's predictions are off by less than 9% from the actual values. This indicates the model is capturing the trend and seasonality in the data well.

* R-squared (R²): 0.86
Interpretation: R² indicates how well the model's predictions match the actual data. An R² value of 0.86 means that about 86% of the variance in the target variable is explained by your model. This is a strong result and suggests that the model is able to explain most of the variability in the data. An R² above 0.8 is generally considered good in many predictive modeling scenarios.

* Accuracy: 91.09%
Interpretation: An accuracy of 91.09% indicates that the model is correct approximately 91% of the time. This is a good result, especially for forecasting or regression tasks where exact matches are rare but the general trend is well-captured.

## ***Conclusion:***

***Overall Performance:***

The model is performing well, as indicated by the low MAE and RMSE, as well as the high R² and accuracy. Interpretation: The model has a good balance between minimizing error and capturing the data's variability. MAPE being under 10% is excellent, which suggests it is effective for forecasting purposes. Next Steps: You could try to further fine-tune the model or explore additional features or algorithms to improve the performance slightly. However, based on the metrics, the model is already performing at a high level.
