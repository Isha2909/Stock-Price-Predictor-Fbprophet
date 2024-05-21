# Stock-Market-Close-Price-Prediction
![Screenshot 2024-05-21 190524](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/6ffab10e-c2ee-4e03-8157-7288a15aabec)
## Overview :
Understanding the stock market entails grappling with a myriad of factors—from company performance to global events—that influence stock prices. Predicting these prices requires a comprehensive analysis of historical data, encompassing price trends, trading volumes, financial metrics, and external influences.
## Why Forecast Stock Market CLosing Prices??
 Here are some important reasons !
* __Informed Investment Decisions__: Predictions help investors decide when to buy, sell, or hold stocks, maximizing profits and minimizing losses.
* __Risk Management__: Anticipating price movements enables investors to mitigate risks associated with their investments.
* __Financial Planning__: Forecasted prices aid in planning for long-term financial goals such as retirement or education expenses.
* __Market Analysis__: Insights from forecasts contribute to broader market analysis, guiding trading strategies and policy recommendations
* __Driving Financial Innovation__: Advancements in predictive analytics drive innovation, improving forecasting accuracy and adapting to market changes.

## Project Tasks:
Navigate through historical stock market data across different companies. 
__Our mission?__--> ""Uncover insights, identify trends, and build predictive models that paint an accurate picture of future closing prices"".
## Getting started 
__So We Will Perform The Following Steps__
* __Explore Data__: Dive into historical stock market data to understand how prices have behaved over time.
* __Find Insights__: Look for patterns and trends in the data to see the behaviour of our timeseries data
* __Build Models__: Create models that can analyze historical data and make predictions about future prices.
* __Check Performance__: Evaluate how well our model performs by comparing its predictions to actual prices using different metrics.
* __Make Predictions__: Use our model to make predictions about future stock prices with confidence and accuracy.
# TABlE-OF_CONTENTS
* __Data Description__
* __Methodolgy__
* __Results__
* __Usage__
* __Future Stock Predictions__
# Data Description
* Id: Unique identifier for each row
* Date: Date of the stock prices
* Open: Opening price of the stock
* High: Highest price of the stock during the day
* Low: Lowest price of the stock during the day
* Close: Closing price of the stock
* Adj Close: Adjusted closing price of the stock
* Volume: Number of shares traded
* Company: Name of the company
# Methodology 
* ## Loading the dataset
  Here is a sample of the original dataset:
![Screenshot 2024-05-21 194803](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/51da2b31-8d21-4604-ae25-510e655f9a75)
* ## Pivoting the dataset
  It is required to make it easier to analyze the closing prices of each company over time
  
  Here is a sample of the pivoted dataset:
![Screenshot 2024-05-21 212807](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/75d4ecd5-8b4c-457c-bd44-d498ab29bf63)
# Why we are using only close prices for close price forcasting ??
## Reasons :
* Stability: Closing prices are more stable than intraday prices.
* Widely Accepted: Common practice in the financial industry.
* Less Noise: Intraday price movements (open, high, low) can be influenced by various short-term factors, such as news releases, market sentiment shifts, or even speculative trading.
* Simplicity: Simplifies the model and makes it easier to understand.
* ## Check for null values and duplicates
  The data is clean, with no null values or duplicates.
* ## Outlier detection
-  We used  two methods :
-  Box plot method --> Box that represents the interquartile range (IQR) of the data, with a line inside the box representing the median.Extending whiskers represent range of data  and indvidual points are outliers
  ![Screenshot 2024-05-21 220353](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/5ca9c940-16ab-406d-8e9c-5e77692d8fec)
-  Interquartile Range (IQR) Method :
   IQR = Q3-Q1[ third quartile --> (Q3) ,first quartile --> (Q1) of the dataset], Outliers are the  data points that fall below Q1 - 1.5 * IQR or above Q3 + 1.5 * IQR.
   
 ![Screenshot 2024-05-21 221612](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/3e730a63-32bc-4544-be54-b848b5ea8d45)
![Screenshot 2024-05-21 221649](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/4c8a6f51-4992-4924-902e-caadcb5f0740)
* ## Seaonality determination using ACF plots
   - We do -> Visual Inspection of ACF Plots:
      * Look for significant spikes at regular intervals.
      * For daily data with yearly patterns, significant spikes at or around 365 lags indicate yearly seasonality.
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/79dbc1dc-59a1-4a36-a492-025610f44e85)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/8c78661f-953f-4f04-a237-2ba9ecbcf2a2)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/9d61218f-156e-430e-af0b-353b81eac84f)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/bb424e4f-f50c-4c24-aa9e-d17979f49d6b)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/23ee69e7-2632-49c5-8b1d-4087f99e9d9a)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/738600cc-f264-4e4f-86be-d94e38e22a38)


* ## Time Series Decomposition
  - Breaking down time series into its fundamental components :
    * Trend: The long-term progression or direction in the data.
    * Seasonality: The repeating short-term cycle in the data.
    * Residual (Noise): The random variation or noise in the data after removing trend and seasonality.
  - Additive Decomposition
    * In an additive model, the components are added together. This model is suitable when the seasonal variations are roughly constant over time. The formula for an additive model is:
       - Y(t) = T(t)+ S(t) + R(t)
  - Multiplicative Decomposition
    * In a multiplicative model, the components multiply together. This model is suitable when the seasonal variations change proportionally with the level of the time series. The formula for a multiplicative model is:
       - Y(t) = T(t)*S(t)*R(t)
       - Where: Y(t) is the observed valiue at time t
       - T(t) is trend component at time t
       - S(t) is the seasonal component at time t
       - R(t) is Residual(noise) component at time t
  * Here are the timeseries decomposition for each company
  * ## Visualization of Additive amd Multiplicative decomposition for each company
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/694f17ac-6b46-4ded-a3ee-f2321773a2f0)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/7ef9bb5a-a0c5-4cd7-b51e-5481c9e77e16)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/7399993c-b4e8-4ddf-b2e3-23acb8717a1b)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/0adfc2e6-f362-463a-b96b-33c2f1207a66)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/e470f2d3-42e1-4558-8042-60530b85a30e)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/e7b44a21-6b9f-4859-b922-72602813e3c6)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/66625d36-cfbd-4252-8487-8c3954f48ae0)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/b8a40e58-2c71-40dc-b082-0ab468ad8fd9)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/dff493ef-bdeb-4caa-8d9b-f8f9312d79f8)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/bc4a5a99-5f89-4fe9-bb82-d2aa92529b27)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/f2c1e36c-0228-4e07-9d9a-7ccf7a41732a)
  ![image](https://github.com/Isha2909/Stock-Price-Predictor-LSTM-FBProphet-Sarimax/assets/162286426/b01da8a9-e07f-4324-ad82-0fd4ed705a3c)
  

* ### Conclusion from above visualisation
  - **Trend Analysis for every comapny**
     * Comapny0 - From 2033 to 2035 -->SIDEWAYS TREND ,FRom 2035 end to 2037 --> UPTREND then again  till 2038 its a SIDEWAYS trend
     * Comapny1 - From  2033 to 2035(March or April ) --> DOWNTREND  then till 2036(july)--> UPTREND then till 2038 --> SIDEWAYS
     * Comapny2 - From  2033 to 2035(Jan) --> DOWNTREND then till 2038 its Sideways
     * Comapny3 - From  2033 to 2035(March or April ) --> DOWNTREND then till 2037(July)--> SIDEWAYS then till 2038--> UPTREND
     * Comapny4 - From  2033 to 2035(March or April ) --> DOWNTREND then till 2038--> UPTREND
     * Comapny5 - From  2033 to 2035(March or April ) --> DOWNTREND then till 2038--> UPTREND
* How to Determine Whether a TimeSeries is Additive or Multiplicative ?
     - Requirements for additivity and multiplicity
     * The additive model assumes constant seasonal fluctuations, with the seasonal component oscillating around a constant mean (zero).
     * The multiplicative model assumes that seasonal fluctuations vary proportionally with the level of the time series, with the seasonal component oscillating around a mean value (one).
       
       **Given the stability and consistency observed in the multiplicative decomposition, particularly in the seasonal and residual components, it suggests that the time series is better represented by a multiplicative decomposition.** 

  












 



