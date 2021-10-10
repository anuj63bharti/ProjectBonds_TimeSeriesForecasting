# Project_Bonds
Project Title : Price forecasting of SGB and IRFC Bonds and comparing there returns.
## Introduction of the Project
The 2008-09 global financial crises and 2020-21 pandemic have shown us the volatility of the market. Many people have are finding a way to invest money to secure their future. People are trying to find a secure investment with minimum financial risks with higher returns. This is also a fact that with investment their also comes with risks. There is a saying in the world of investment “Do not put all your egg in one basket”. We need to diverse portfolio in the area of investment, so that if one investment does not give you enough yields due to fluctuations in the market rates then other will give you higher yield. Bonds are one such investment people prefer the most. The Bonds we have selected are two government bonds – SGB (Sovereign Gold Bond) and IRFC (Indian Railway Finance Corporation). The objective was to forecast the prices of SGB and IRFC bond and calculate the returns. Compare the returns and recommend the client which one to pick based on the input that is number of years to forecast.

## Technologies Used
* Python – ML model (auto_arima (for grid search to find p,q,d values), ARIMA(for forecasting values))<br>
* SQLite – Database<br>
* Flask – Front End for deployment<br>
* Python Libraries – numpy, pandas, Statsmodels, re, nsepy, matplotlib<br>
* HTML/CSS<br>

## General info
This project is simple Forecasting model. Not taxes were put into use when calculating returns. IRFC Bond is a tax free bond but SGB we need to pay taxes if we try to sell it before the maturity period is over.
Inflation rate and global pandemic situation is a rare phenonmenon and it is beyond anyone's control. It has been taken into business restriction.<br>
Data has been collected from [National Stock exchange of India](https://www1.nseindia.com/index_nse.htm)
The two bonds selected from NSE was -
* [Indian Railway Finance Corporation Limited Bond (IRFC)](https://www1.nseindia.com/live_market/dynaContent/live_watch/get_quote/GetQuote.jsp?symbol=IRFC&series=N2)
* [Sovereign Gold Bonds(SGBAUG24)](https://www1.nseindia.com/live_market/dynaContent/live_watch/get_quote/GetQuote.jsp?symbol=SGBAUG24&illiquid=0&smeFlag=0&itpFlag=0)


## Requirement file (contains libraries and their versions)
[Libraries Used](https://github.com/tuhinbasu/Project_Bonds/blob/main/requirements.txt)

## Project Architecture
![alt text](https://github.com/tuhinbasu/Project_Bonds/blob/main/img/project_arch.PNG)

## Explaining Project Architecture
### Live data extraction
The data collected from NSE website (historical data) and the library which is used to collect live daily data from the website is [nsepy](https://nsepy.xyz/). The data is then goes to python, two things happens in python. First, out of all the attributes, we only take "Close Price" and then the daily is then converted into monthly data. We use mean to calculate the the monthly average.
### Data storage in sqlite 
We chose SQLite because it is very easy to use and one does not need the knowledge of sql to observe the data. the database is created locally and and is being updated when the user usses the application. the user can easliy take the database and see the data in SQL viewr online available.
### Data is then used by the model
When data is then called back by the python. the python then perform differencing method to remove the trend and seasonality from the data so that our data can be stable. For successful forecasting, it is necessary to keepp the time series data to be stationary.
#### p,d,q Hyperparameters
We use auto_arima function to calculate p,d,q value. We use re(regex) to store the summary of auto_arima in string format. then use "re.findall()" funtion to collect the value of p,d,q values. The downpoint of using this auto_arima function is that it runs two times when the programes gets executed. It calculate the hyperparameter values for both SGB and IRFC data.
### ARIMA
This part is where the data is taken and then fit & predict.<br>
This is for 12 months.
![Actual Data vs Predicted Data](https://github.com/tuhinbasu/Project_Bonds/blob/main/img/actualvspred.PNG)
### Model Evaluation
#### SGB
The RMSE: 93.27 Rs. & The MAPE: 0.0185
#### IRFC
The RMSE: 21.62 Rs. & The MAPE: 0.0139<br>
(Pretty Good)
### Forecasting (12 Months)
![Forecasted Data (12 Months)](https://github.com/tuhinbasu/Project_Bonds/blob/main/img/forecast.PNG)
### Returns
This is the part where both SGB and IRFC foecasted data is being collected and based on that returns are calculated. If the SGB returns is higher than IRFC bonds then it will tell the customer about the amount of return for a specific time period.
### User Input
The user will be given 3 options as Input. The user will select a specific time period from a drop down list. The options are -<br>
1. 4 Months (Quaterly)<br>
2. 6 Months (Half yearly)<br>
3. 12 Months (Anually)<br>
This options are time pperiod to forecast. If the user press 6 then the output page will show "6" forecasted values with a range Upper Price, Forecasted Price, Lower Price for both the bonds side by side. Below there will be a text where the returns will be diplayed if the user decides to sell the bonds then.<br>





## Setup
To run this project, install it locally using npm:

```
$ cd ../lorem
$ npm install
$ npm start
