---
title: "Forecasting building energy demand"
categories: 
    - Data_Science
    - EDA
    - Time Series
tags: 
    - eda 
    - data science
    - AIcrowd
    - building energy demand
    - thesis 
    - neuefische
    - bootcamp 
last_modified_at: 2022-08-18T14:00:00-01:00
image: /assets/images/posts/green_city/ecantu_Take_a_realistic_4K_photograph_of_a_9-building_complex_f_3c8a11f4-5040-4f0d-b9ec-dec1a281d5f0.png
---

Final project done at the Neuefische bootcamp. The project focuses on forecasting hourly building energy demand of 9 buildings. The used data was from the [2021 CityLearn Challenge](https://sites.google.com/view/citylearnchallenge), based on 4 years energy consumption and weather data. 

## Introduction

Since energy prices are continuing to rise and the future of the energy situation is rather uncertain, cities may want to investigate the energy consumption of different building sectors to predict future energy demand and identify areas where energy can be saved.

Energy demand forecasting is fundamental for an energy utility’s decision making on:

- Grid stability

- Planning power supply activities

- Reducing energy wastage

Since the data available consists of a series of energy consumption values taken sequentially with a fixed time interval over four years, time series analysis and models are ideal for this problem.

## Methodology

Time series data was analyzed for trend and seasonality.

It seemed suitable to forecast the energy demand for 24 hours, as weather predictions get less accurate further in the future. Else, the power suppliers energy management is mainly focused on a 24 hour period.

Different models were applied and compared:

- Baseline (last years values)
- Linear Regression
- Polynomial Regression
- SARIMAX
- Prophet
- TBats
- XGBoost
- Random Forest

## Main  Results

A small trend in the net energy demand over 4 years was discovered with a slight increase over the first 3 years and a decrease in the 4th year (corresponding to the trend in the weather data). A clear yearly seasonality is found with the highest energy demand in summer (due to air conditioning) and the lowest energy demand in winter (due to mild winters). Furthermore a weekly as well as a daily seasonality was identified.

![image](https://raw.githubusercontent.com/erickCantu/TheGreenCitySolutionsGroup/main/images/decomposition_yearly_net_energy_usage_final_presentation.png)

## Conclusion

Tree-based machine learning models (Random forest and XGBoost) produced forecasts with the lowest mean absolute error compared to the observed data.

![image](https://raw.githubusercontent.com/erickCantu/TheGreenCitySolutionsGroup/main/images/benchmark.png)

---

## Links

The complete project is available at the [The Green City Solutions Group: Forecasting building energy demand through time series analysis and machine learning](https://github.com/erickCantu/TheGreenCitySolutionsGroup) GitHub repository. At the end of the analysis a presentation was done to the Neuefische team and other trainees. The presentation slides are available [here](https://github.com/erickCantu/TheGreenCitySolutionsGroup/blob/main/Capstone_Project_Presentation.pdf), while the presentation can be watch at: [The energy of tomorrow - YouTube](https://www.youtube.com/watch?v=jncUVXZKmCI). 
