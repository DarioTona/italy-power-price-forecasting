
## Dataset construction

This dataset is built from public sources and then aggregated at **daily granularity**.

- **PUN (GME)**: daily average of the PUN price published by GME (MGP market results).  
  Unit: **€/MWh**.  
  Source: https://www.mercatoelettrico.org/en-us/Home/Results/Electricity/MGP/Results/PUN

- **Terna generation and load**: generation by source (wind, photovoltaic, hydro, geothermal, thermal) and total load downloaded from Terna’s data portal.  
  Unit in the original data is **MW** for total_load and forecasted_total_load, while **GW** for the generations.  
  In this dataset the values are already aggregated as **daily averages** (mean over the day).  
  Source: https://dati.terna.it/en/download-center

