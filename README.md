# Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery
# INTRODUCTION

#### The following data analysis was performed by Marc Rivera(https://www.linkedin.com/in/marcrivera9/) for my personal investment strategy on Bitcoin, and was finalized on 11/04/2023.

# OBJECTIVE

#### The primary goal of this project is to enhance my personal investment portfolio by conducting a comprehensive analysis of the relationship between Bitcoin prices and selected stocks (COIN, CRWD, PFE) during the COVID-19 pandemic. The focus will be on identifying potential correlations and trends that could inform strategic investment decisions. By gaining insights into how these assets interacted in the context of a global health crisis, I aim to optimize my portfolio allocation and mitigate risks. The findings will serve as a foundation for informed decision-making, contributing to the overall improvement of my investment strategy. Additionally, this analysis may provide valuable insights for other investors interested in navigating similar market conditions."

# TOOLS
* Python (Pandas,Matplotlib,Seaborn)
* Visual Studio Code (enviroment)
* Jupyter Notebook
* API's

# STEPS
## 1. Collecting data
##### For the purpose of this project, I utilized Coingecko's free APIs to access historical cryptocurrency data for the last 365 days, starting from 11/03/23. Coingecko's API provides comprehensive historical data on various cryptocurrencies, including Bitcoin, enabling a thorough analysis of price movements over the specified timeframe.

#### In parallel, I employed Alpha Vantage's API to gather real-time stock market data for the selected stocks (COIN, CRWD, PFE). Alpha Vantage's API offers a user-friendly interface and reliable access to live stock market information, ensuring that the analysis includes the most recent and up-to-date data.

#### This dual-source approach, combining cryptocurrency data from Coingecko and stock market data from Alpha Vantage, allows for a holistic examination of the relationship between Bitcoin prices and the selected stocks during the past year. The combination of historical cryptocurrency trends and real-time stock market dynamics enhances the robustness of the analysis and provides a comprehensive foundation for portfolio optimization and decision-making.

#### In addition to cryptocurrency and stock market data, I obtained relevant COVID-19 information to explore potential correlations between market trends and the impact of the pandemic on public health. Specifically, I accessed hospital visit data directly from the CDC website. This data spans the last 365 days, aligning with the timeframe of the cryptocurrency and stock market data.

#### The inclusion of COVID-19 hospital visit data aims to shed light on whether there is a discernible relationship between the frequency of hospital visits and the observed market movements. By triangulating these datasets, I seek to identify potential patterns or trends that could further inform investment strategies and decision-making.

#### All link to the data documentation will be linked below:

#### 5 datasets were used:
  * Bitcoin Data:(https://www.coingecko.com/api/documentation)
  * CRWD Data:(https://alphavantage.co/documentation/)
  * COIN Data:(https://alphavantage.co/documentation/)
  * PFE Data:(https://alphavantage.co/documentation/)
  * Hospital Visits Data :(https://covid.cdc.gov/covid-data-tracker/#trends_weeklyhospitaladmissions_select_00)

## 2. Import Data using Apis/ CDC data using CSV
 Coin geckos api documentation is pretty straight forward within their documentation the give a snippet of what code to script to import the real time data:

 ### Bitcoin data for the last 365 days: 
 
![APi coingeck](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/acfa486d-7ac6-4c0d-8ef2-6a77de13a8b5)

### API importation CRWD, COIN, PFE 

#### In this comprehensive analysis, I have strategically selected three distinct stocks—CrowdStrike Holdings Inc. (CRWD), Coinbase Global Inc. (COIN), and Pfizer Inc. (PFE)—to gain nuanced insights into their market behaviors and potential correlations. CRWD, as a technology company, represents the broader tech sector, providing an opportunity to explore how tech stocks, in general, respond to market trends. COIN, being intricately tied to the cryptocurrency space, offers a unique perspective on the relationship between Bitcoin and a company directly involved in the crypto industry. Lastly, PFE, a prominent pharmaceutical company, witnessed significant volume during the peak of the COVID-19 pandemic due to its involvement in vaccine development. By analyzing the correlation between these stocks and Bitcoin, I aim to uncover patterns and trends that go beyond individual sector dynamics. This diversified approach not only enriches the analysis but also enables a holistic understanding of how assets from different sectors interact, contributing valuable insights for optimizing my investment portfolio in response to varying market conditions.

![pfe api](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/4d1f41aa-3634-4161-95cc-8e0774b5e044)
![crwd api](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/701f5d51-f384-4395-8f26-7da285774c4c)
![coin api](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/d0d9463a-144f-4f65-9d22-c4e1238bc444)

### Import CDC data using Pandas .readcsv()

![cdc](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/07e8fb6d-412f-4510-8606-db89614b1d19)

 
## 3. Data Cleansing/Wrangling/Manipulation 

#### Import necessary libraries
  
![libraries](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/4b94c9db-73f0-4ad4-9669-325a444c4b23)

### Bitcoin 

#### Fix timestamp to YYYY - MM - DD, this will help for combining data, the data will be our common column to merge.

  ![times](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/bd61bc36-3fe6-4b40-9ecc-4fc7b3a97b98)

#### Use .info() to verify are dtypes are correct and there are no nulls.

![btc_info](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/701923b9-085d-4ee0-94d3-5d762d5a36c9)

#### There were two rows for the date of 11/04, and 365 rows, so I used .truncate() to cut that last row off, the index starts from zero so we need exactly 365 rows.

![ss](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/f3cac7d4-cd5e-4714-88e6-26e12c0077ae)

### CRWD

#### Create a dictionary and use pandas dataframe function 

![crwd data](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/75536f81-ed37-449a-8382-556e1e04f79e)

#### .info() & .shape() to understand my dataframe and find nulls if there is any.

![shape](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/58b82872-aa24-46cd-8a63-f5ce11846ba9)

![info crws](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/2598dbea-05b8-4d3c-b721-ebe3d47ecc87)

#### drop unecessary columns

![drop](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/f48c7d7a-4fdd-4e9a-8a3a-6172d261ed06)

#### I only need the dates from where the bitcoin data started so I will condition out the dates before it.

![dates needed](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/4891d569-d824-44b1-81ed-cfe9c2eafb15)

### COIN 

#### The process is the same so I will show the code together.

![COIN datra](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/a1fc68da-eaea-4ace-99ee-e687c145ca10)

### PFE 

![pfe data](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/fab52117-e6eb-45e2-a234-5b751192ec3e)

### Merge data to one table

![merged](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/387cb02f-baa5-4dc0-a2fd-64c2728565e8)

#### I decided to use the closing prices for my analysis because they give us a more reliable picture of how the market is doing for a particular day. Unlike the opening prices, which can be influenced by pre-market factors and don't really tell us where the day is headed, closing prices represent the final value of a stock at the end of the trading day. It's like capturing the overall sentiment and performance of the market when all is said and done. So, for my study on CrowdStrike (CRWD), Coinbase (COIN), and Pfizer (PFE), I'm focusing on these closing prices. This way, I can better understand how these stocks are performing over time without getting caught up in the day-to-day ups and downs that might not be as meaningful for my analysis.

### CDC Hospital Visits Data

#### Changed the date to match format (YYYY - MM - DD)

![datetime sss](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/7d17d672-05dc-49e8-a15e-de3e55006011)

#### Rename columns for better clarity

![renamess](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/ebd5bf80-d5e6-46b8-ab5f-ff221b86631e)

#### Drop columns not needed 

![dropss](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/7013a405-6442-4fc8-bffc-50e615c19621)

### Reformat BTC DATA to weekly 

#### I'm opting for weekly averages for Bitcoin prices because the hospital visit data is reported on a weekly basis. Aligning the frequencies like this just makes sense for a more accurate analysis. By calculating the average Bitcoin price for each week, it smoothens out the daily fluctuations and gives a more stable measure. This way, when examining the correlation with hospital visits, I'm avoiding getting caught up in daily market volatility. It's like ensuring a consistent comparison—apples to apples, you could say. This approach is aimed at uncovering trends and relationships over time, providing a clearer understanding of how Bitcoin prices might be connected to the weekly hospital visit data. It's all about enhancing the meaningfulness and accuracy of the analysis

![weekly](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/e58406bb-6be7-418f-9e51-02f72a77f15d)

### Merge Data

![merge data](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/8fc64218-3261-4367-897d-251cfb1c2c80)

#### Now that the data cleaning and manipulation steps are complete, it's time to dive into the heart of the analysis—exploring trends and uncovering key findings. I'll be leveraging visualization tools and statistical methods to bring out meaningful insights from the datasets. This stage involves not just looking at individual stock or cryptocurrency movements but also exploring the interplay between Bitcoin prices, tech stocks like CrowdStrike (CRWD) and Coinbase (COIN), and the healthcare stock Pfizer (PFE). I'm particularly interested in identifying any correlations or patterns that might emerge, shedding light on how these assets interacted over the past year. The goal is to draw actionable conclusions that can inform investment decisions and contribute valuable insights to the broader understanding of market dynamics during the COVID-19 pandemic. Let's see what the data reveals!

## 4. Findings/Visualizations

#### My initial focus is on uncovering the trends of Bitcoin (BTC), CrowdStrike (CRWD), Coinbase (COIN), and Pfizer (PFE) over the past year. By examining the historical performance of these assets, I aim to identify and visualize their trends. This involves using Matplotlib lineplot to illustrate how each asset has moved over time. Looking at trends can provide valuable insights into the overall market sentiment, potential periods of volatility, and any notable patterns that may have influenced their trajectories. This foundational analysis will set the stage for further exploration and help me grasp the broader market dynamics that shaped these assets during the specified timeframe.

### BTC lineplot

![lineplot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/23fceb18-8818-4d50-b0c6-af477b26cf53)

![btc_lineplot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/987dca9c-28f1-4d8c-a5e4-4d82468d8a39)

### COIN Lineplot

![coin line plot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/f35d5023-1077-4344-9914-7fa2fc6a413a)

![coin_lineplot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/d679076a-e321-46b8-a447-fd7d03a4f3ff)

### CRWD lineplot\

![crwd line plot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/9b576b93-8469-4242-aebc-a95482cdd8b5)

![crwd_lineplot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/442222c9-404a-4618-9f7e-70115a7bac9a)

### PFE lineplot

![pfe line plot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/3fbab4ce-4444-4777-aa69-4b29c456c3f8)

![pfe_lineplot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/afb5b4cf-599b-46bb-8e0b-798821ecaa07)

### Normalization Approach

#### To enhance the comprehensibility of the trends, I've taken a holistic approach by combining Bitcoin (BTC), CrowdStrike (CRWD), Coinbase (COIN), and Pfizer (PFE) using a normalized approach. Given the substantial difference in price ranges among these assets, normalization levels the playing field, offering a more accurate comparison of their trends. This approach ensures that each asset's movements contribute proportionally to the overall analysis, providing a closer and more detailed look at how these diverse assets interacted over the past year. By bringing them onto a similar scale, I'm better positioned to identify nuanced patterns, correlations, and anomalies that might have otherwise been overshadowed by the vast difference in individual price magnitudes. It's a method aimed at fostering a more meaningful and accurate interpretation of the combined trends

![normalized line plot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/7a756cbb-c893-4e12-9776-6eee78224abe)

![lineplot_normalized_prices_overtime](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/2221c7a3-96a8-466a-a703-d021b3275342)

### Insights from Lineplots: 

#### The insights derived from the merged line plots of BTC, COIN, CRWD, and PFE trends are quite revealing. The sustained uptrend observed in Bitcoin, Coinbase, and CrowdStrike since November of the previous year suggests a consistent and positive market sentiment toward these assets. This pattern indicates that investors have generally shown confidence and interest in these entities, potentially driven by factors such as growing adoption for Bitcoin, positive developments for Coinbase in the cryptocurrency space, and the overall success and potential of CrowdStrike as a tech company.

#### On the contrary, Pfizer's clear and continuous downtrend over the same period signifies a persistent decrease in its stock price. This downtrend may be attributed to various factors such as company-specific challenges, industry dynamics, or market sentiment towards healthcare and pharmaceutical stocks during the observed timeframe.

#### By visually assessing the trends, I've gained valuable insights into the relative performance of the assets in my portfolio and the broader market dynamics. It's evident that Bitcoin, Coinbase, and CrowdStrike have exhibited positive trends, suggesting potential areas of strength. Conversely, Pfizer has encountered challenges in sustaining its stock value, indicating a need for strategic consideration. These insights play a pivotal role in my decision-making process, offering guidance for potential adjustments to my portfolio and informing investment strategies. The observed trends prompt thoughtful reflection on how to strategically position my portfolio, considering the strengths and challenges associated with each asset. Additionally, the contrasting trends spark curiosity, encouraging further investigation into the underlying factors influencing market sentiment for each asset and helping shape a more informed and targeted approach to managing my investment portfolio.

### Correlation and Visualization Corr heatmap

![corrr code](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/e6b3b04e-daf5-4983-bf04-979f0cefb4b9)

![visualization ccc](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/b5695d8e-9a6e-4e64-84eb-6a07b71c467c)

![correlation_heatmap_btc_crwd_coin_pfe](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/388fdf29-0f03-4a16-a841-b04a4396fb54)

### Insights from Heatmap: 

#### Diversification Potential:
The negative correlations observed between Pfizer (PFE) and both Coinbase (COIN) and Bitcoin (BTC) suggest a potential diversification opportunity. When PFE prices decline, there tends to be an upward movement in COIN and BTC prices, providing a potential hedge against declines in traditional pharmaceutical stocks.

#### Hedging Strategy:
Given the robust negative correlations with PFE, incorporating COIN and BTC into your portfolio could act as a strategic hedge. This means that during periods when pharmaceutical stocks face challenges, the positive movement in cryptocurrency-related assets may offset potential losses.

#### Tech and Crypto Synchronization:
The positive correlations between COIN, CrowdStrike (CRWD), and BTC imply a certain synchronization in their movements. As COIN prices rise, there is a tendency for both CRWD and BTC prices to increase. This insight can guide your portfolio strategy, emphasizing the potential benefits of aligning investments in tech and crypto-related assets.

#### Risk Management:
Understanding the moderate positive correlation between CRWD and BTC provides insights into the synchronized movement of these assets. It's important to consider this correlation when managing risk in your portfolio. If there are shifts in the tech sector or cryptocurrency markets, a balanced approach to CRWD and BTC exposure could contribute to effective risk management.

#### Dynamic Asset Allocation:
Leveraging these correlation insights allows for a dynamic approach to asset allocation. During different market conditions, you can adjust your portfolio to capitalize on potential gains while managing risk effectively. The negative correlations with PFE and positive correlations among tech and crypto assets offer opportunities for strategic adjustments based on market trends



#### Hospital visits lineplot

![hospital visits line plot](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/5caaf565-1340-4214-a71e-06d6557e92e6)

![hospital_visits_full_line](https://github.com/marcrivera9/Analyzing-Bitcoin-Prices-and-Stocks-COIN-CRWD-PFE-Amid-COVID-19-Negative-Correlation-Discovery/assets/148594670/dad2a9af-fe55-41e3-8647-2cf672112b0e)



## 5. Recommendations/Investment Strategy
