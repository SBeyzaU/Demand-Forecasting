# HIV Treatment Time Series Forecast
### Author: Beyza Ulasti


![share-deaths-aids](https://user-images.githubusercontent.com/122234730/233189009-f53a641e-b855-4c32-86eb-bfe3e63f0259.png)


# Project Description
This project aims to forecast the demand for HIV treatment (ARV) and HIV rapid diagnostic test (HRDT) using time series models. Initially, a one-shift ARIMA model was utilized as a baseline for comparing the performance of the final SARIMA model. However, since the original dataset was supply chain shipment pricing, the project faced some challenges in achieving optimal model performance. The limited amount of data might have hindered the models' ability to perform better. To address this issue, separate models were developed for each item. Overall, the project's goal is to improve the accuracy of demand forecasting for HIV treatment and HIV rapid diagnostic tests, which can help ensure the regular availability of these critical resources.




#### Summary of Repository Contents:
* Supply Chain Shipment Pricing Data sourced from [USAID](https://catalog.data.gov/dataset/supply-chain-shipment-pricing-data-07d29)
* The [final presentation](presentation.pdf) in PDF format
* The [final notebook](Final-Notebook.ipynb) containing detailed analysis and accompanying code


## Business Problem
Over a ten-year study, The University of New South Wales discovered that a modest 27% increase in HIV treatment access resulted in a significant 66% decrease in HIV infections. With a staggering 38.4 million people around the world HIV-positive in 2021, two-thirds of whom reside in Africa, regular HIV treatment is crucial as the disease remains incurable. By reducing the amount of HIV in the bloodstream, treatment helps prevent transmission to others and reduces the risk of drug resistance. Effective demand forecasting could be the key to alleviating the HIV crisis in many countries, especially by automating the process and eliminating the need for human resources. Predicting future needs would help prevent medication shortages, ensuring that essential drugs are accessible to those who require them.

This project aims to meet the needs of USAID, which is already contributing to relief efforts, although it is important to note that this is a hypothetical stakeholder for academic purposes, and this project is not affiliated with USAID.



#### Limitations of Data

* No inventory data
* Not enough instances of every country featured


## Bottom Line

On average, the final forecast for antiretroviral drugs was inaccurate by 19,000 units per month, whereas the HIV rapid diagnostic test forecast was only off by 2,000 units per month.


## Data Preparation

* Data cleaning 
    * Dropped columns regarding to shipment and pricing
    * Dropped countries with less than 100 instances
    * Dropped vendors with less than 50 instances
    * Checked for null values
    * Filled null values with 0
* Feature Engineering
    * Compared scheduled delivery date with actual delivery date to create "unscheduled_delivery" column
* Datetime
    * Converted "delivered to client date" to string type
    * Converted "delivered to client date" to datetime object 
    * Set delivery date as index
* Visualizations
    * Plotted the final deliveries

* TimeSeries Dataframe
    * Created a pivot table with delivery date as index, columns as product group and values as line item quantity
    * Removed the timezone information to fix plot errors
    * Resampled the timseries dataframe from daily to monthly
    * Filled the null values with 0
    
    ![deliveries-over-time](https://user-images.githubusercontent.com/122234730/233246784-b62136ed-3777-4ce5-933b-d7ea24ec0071.png)

    
## Preprocessing
 * Stationarity
    > Performed a stationarity test--adfuller on both product groups separately 
    > While the ARV was stationary, HRDT was non-stationary
 * Log Differencing
    > To avoid getting -inf, I added 1 to the timeseries dataframe
    > Performed log differencing
    > Checked for nulls
    

## Baseline Model
  * Train-Test Split: Train data ranges from the beginning to 09-2014 and test data covers frin 10-2014 to the end.
  * Predictions range from 11-2014 to 10-2015
  
  
  
 The baseline model or the First Simple Model is an Arima model with a shift of one. Both ARV and HRDT models have order=(1, 1, 1) and monthly frequency. 
 
 #### Baseline Model Results:
 
    ARV Mean Absolute Error: 28,586.06
    
    
    HRDT Mean Absolute Error: 1.84






## SARIMA MODEL

  * Preprocessing
  
    ACF (Auto-Correlation Function) and PACF (Partial Auto-Correlation Function) plots to understand the underlying patterns in the data and to ensure SARIMA is a good model to use with the dataset 
    
    Train-Test Split: Train data up to 09-2014 and Test data 10-2014 and on
    
Model Features:

   Order=(0,0,1)
   
   Seasonal order=(1,1,1,12)
   
   Enforce stationarity=False
   
   Enforce invertibility=False

 #### SARIMA Model Results:
 
    ARV Mean Absolute Error: 24,226. 53
    
    
    HRDT Mean Absolute Error: 1.89




  
  

## Finding Optimal SARIMA-GridSearch

Performed GridSearch with the parameter for  p, d, q in the range 0-3. The grid search works to find the parameters with minimal BIC value and returns the top 5 models with the best parameters.



## Final Model

The grid search returned the best ARV model as SARIMAX(2, 1, 0)x(2, 2, [1, 2], 12)  

ARV Plot Diagnostics:

![image](https://user-images.githubusercontent.com/122234730/233245294-3c3cfb0d-6428-417c-aede-2383c517b488.png)


The grid search returned the best HRDT model asHRDT model as SARIMAX(0, 0, 1)x(1, 2, 1, 12) 

HRDT Plot Diagnostics:
![image](https://user-images.githubusercontent.com/122234730/233245605-5ecaa23b-b804-4309-96fc-6f3e18acd981.png)



#### Final Model Results:

![arima-arv](https://user-images.githubusercontent.com/122234730/233246636-7e9b2b2f-e644-45c0-9104-9909fa133616.png)



![sarima-hrdt](https://user-images.githubusercontent.com/122234730/233246694-02ac2a26-4b00-4ee7-ad6c-4b37bfa16dd4.png)






--------------
Data citation: Doby. 2020. Supply Chain Shipment Pricing Data. Dataset. USAID Development Data Library. https://data.usaid.gov/d/a3rc-nmf6.
