# PUN index (GME) — Daily Forecasting with Terna Generation & Load data

This notebook builds a simple **day-ahead forecasting pipeline** for the Italian electricity price (**PUN index GME**), using public **Terna** data:
- generation by source (wind, photovoltaic, hydro, geothermal, thermal)
- total load, plus Terna’s **forecasted total load**

The goal is to keep everything **clean and reproducible**, showing a standard **time-series workflow**:
data loading, exploratory plots, lag analysis, and a baseline forecasting model compared to a **linear regression model**.

i.e. baseline “tomorrow ≈ yesterday”. This helps to check if a model is actually adding value.

**Main design choice:** the model predicts the **PUN at day D** using only information available up to **day D-1**.  
The only exception is **forecasted total load**, which is a Terna day-ahead estimate published for **D** (so it can be treated as available before delivery).



## Dataset construction

This dataset is built from public sources and then aggregated at **daily granularity**.

- **PUN (GME)**: daily average of the PUN price published by GME (MGP market results).  
  Unit: **€/MWh**.  
  Source: https://www.mercatoelettrico.org/en-us/Home/Results/Electricity/MGP/Results/PUN

- **Terna generation and load**: generation by source (wind, photovoltaic, hydro, geothermal, thermal) and total load downloaded from Terna’s data portal.  
  Unit in the original data is **MW** for total_load and forecasted_total_load, while **GW** for the generations.  
  In this dataset the values are already aggregated as **daily averages** (mean over the day).  
  Source: https://dati.terna.it/en/download-center


## Final considerations

- The linear regression improves MAE/MSE and $R^2$ compared to the **naive baseline** P̂_D = P_{D-1}, so the model is actually adding information.

- Most of the predictive power still comes from the autoregressive component (yesterday price). The 7-day lag contributes as well, consistent with a weekly pattern in electricity markets.

- Load and generation variables are informative. There is collinearity between historical load and forecasted load, but excluding either of the two worsens the results.

- Overall the model tracks the level reasonably well, but it tends to smooth spikes. This is expected with a linear setup.

  

  <img width="1240" height="534" alt="linear_regression" src="https://github.com/user-attachments/assets/1bb0bef3-08bb-46aa-b268-e8d271fb19ec" />
