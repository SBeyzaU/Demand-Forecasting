# Demand-Forecasting
### Author: Beyza Ulasti


![share-deaths-aids](https://user-images.githubusercontent.com/122234730/233189009-f53a641e-b855-4c32-86eb-bfe3e63f0259.png)


# Project Description
This project is meant to use timeseries models to forecast demand for HIV treatment (ARV) and HIV rapid diagnostic test (HRDT). I used a one shift ARIMA model as a baseline to compare the performance of the final SARIMA model. As the original dataset was supply chain shipment pricing, I have faced some challenges with model performance. I believe the models would have performed better with more data. I have done two separate models for each item. 




#### Summary of Repository Contents:
* Supply Chain Shipment Data sourced from USAID
* The [final presentation](Presentation.pdf) in PDF format
* The [final notebook](FinalNotebook.ipynb) containing detailed analysis and accompanying code


## Business Problem
A ten-year study by The University of New South Wales found that just a 27% increase in people accessing HIV treatment saw HIV infections decrease by 66%. Additionally, according to the World Health Organization, 38.4 million people were HIV positive in 2021, 2/3 of which were in Africa. As HIV is not a curable disease it is important to receive treatment regularly Receiving HIV treatment reduces the amount of HIV in the blood, and it prevents transmission to others. Furthermore, taking HIV medicine as prescribed helps prevent drug resistance. Demand forecasting can help alleviate the HIV crisis some countries are still facing today. Automating the process would eliminate the need for human resources. Furthermore, demand forecasting can help us predict future need to prevent stocks from running dangerously low.  Again, the goal is to make sure much-needed medication is accessible on a regular basis. 


Stakeholder: This project is being developed with the needs of USAID in mind as USAID is already helping with relief efforts. This is a hypothetical stakeholder for acedemic purposes. This project is not associated with USAID. 


#### Limitations of Data


* No inventory data
* Not enough instances of every country featured


## Bottom Line
The final antiretroviral drug forecasting was off by 19000 units per month on average. Meanwhile, the HIV rapid diagnostic test forecasting was off by 2000 units monthly.


## Data Preparation
There was a lot of data cleaning that went into this dataset. 




## Baseline Model








## Finding Optimal Model


### GridSearch


## Final Model


#### Results









--------------
Data citation: Doby. 2020. Supply Chain Shipment Pricing Data. Dataset. USAID Development Data Library. https://data.usaid.gov/d/a3rc-nmf6.
