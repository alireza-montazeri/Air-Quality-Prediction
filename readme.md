# Air Quality Prediction Based on Environmental Factors

### Scenario

Predicting air quality is crucial for managing urban environments and protecting public health. Developing a model to forecast Air Quality values helps issue warnings when air pollution levels exceed acceptable limits or when harmful conditions arise. This not only supports the work of environmental and health authorities but also contributes to improving city life by identifying key factors that impact air quality. By exploring how various environmental factors, such as temperature, humidity, and wind, influence air quality, we gain deeper insights into the causes of pollution. Incorporating spatial data allows for a more detailed analysis of geographical variations in pollution, guiding city planners and decision-makers in promoting cleaner, more sustainable urban development.

### What this use case will teach you

At the end of this use case you will:

- Understand how to clean and preprocess environmental datasets.
- Perform exploratory data analysis (EDA) to extract key insights.
- Analyze the importance of different environmental factors in influencing air quality.
- Conduct spatial analysis to visualize geographical variations in air quality.
- Perform data wrangling to ensure the dataset is ready for modeling and analysis.
- Develop and evaluate a machine learning model to predict AQI.
- Create an implementation framework for real-world application of the air quality prediction model.

### Datasets Used

1. **Microclimate sensors data:** This dataset contains climate readings from climate sensors located within the City. The data is updated every fifteen minutes and can be used to determine variations in microclimate changes throughout the day.(https://data.melbourne.vic.gov.au/explore/dataset/microclimate-sensors-data/information/)
2. **Argyle Square Air Quality:** Air quality measures in Argyle Square.(https://data.melbourne.vic.gov.au/explore/dataset/argyle-square-air-quality/information/)

These datasets are sourced from the City of Melbourne's open data portal.

### Usage

In urban environments, PM2.5 and PM10 are considered the primary pollutants due to their direct impact on human health. PM2.5 refers to particulate matter with a diameter of less than 2.5 micrometers, which is small enough to penetrate deep into the lungs and bloodstream, causing serious respiratory and cardiovascular problems. PM10, while larger (up to 10 micrometers), still poses a significant risk, especially to those with existing health conditions. Monitoring these two pollutants is essential for assessing air quality because they are the most prevalent and harmful airborne particles in urban areas, often caused by traffic, construction, industrial activities, and other pollution sources. By focusing on PM2.5 and PM10 as the main features, the model is better equipped to predict dangerous pollution levels and offer early warnings for public health and environmental management.

I used the datasets from **microclimate_sensors** and **argyle_air_quality** to train two models—an LSTM (Long Short-Term Memory) and a GRU (Gated Recurrent Unit) model. These models are well-suited for time-series prediction tasks like air quality forecasting, as they are designed to learn from sequential data and capture patterns over time.

Because of the data availability regarding these two datasets, I took two approaches when predicting air quality:

1. **Using only PM2.5 and PM10 history:** In the first approach, I focused solely on past values of PM2.5 and PM10 to predict future air quality. This approach is straightforward and highlights how well the model can predict future values based solely on the historical data of these two pollutants.

2. **Using historical environmental features:** In the second approach, I incorporated additional environmental factors such as temperature, humidity, and wind speed, which were found to have the most significant impact on PM2.5 and PM10 based on the feature importance analysis. By including these factors, the model takes into account the broader environmental context, which can influence fluctuations in air quality. This enriched dataset allowed the model to better understand how weather conditions affect pollutant levels and improve the accuracy of the predictions.

### Implementation

**Step 1: Data Cleaning and Preprocessing**

- Load **microclimate_sensors** and **argyle_air_quality** datasets from City of Melbourne containing environmental measurements from various sensors across different locations.

- Clean and preprocess the data to handle missing values and ensure consistency.

**Step 2: Exploratory Data Analysis (EDA)**

- Generate summary statistics to understand key metrics like the distribution of PM2.5 and PM10 concentrations over time.

- Plot time series of PM2.5 and PM10 to observe trends, spikes, and potential outliers.

- Perform geospatial analysis to understand how air quality varies across different locations by mapping the sensor positions and their corresponding PM measurements.

**Step 3: Feature Importance Analysis**

- Investigate how environmental factors like temperature, humidity, and wind influence air quality by examining correlations and using decision tree-based models (e.g., Random Forest) to rank feature importance.

- Visualize the contribution of each environmental factor to the prediction of air quality indices (PM2.5 and PM10) using feature importance plots from the decision tree models.

**Step 4: Data Wrangling**

- Identify gaps in data collection using date ranges and visualize periods of low activity, ensuring a better understanding of missing or anomalous data points.

- Handle missing values using linear interpolation and aggregate data from different sensors by resampling to hourly intervals for consistency.

- Normalize the dataset using a **MinMaxScaler** to scale features such as PM2.5 and PM10 between 0 and 1, preparing the data for time-series modeling with LSTM.

- Create sequences of 24-hour windows of PM2.5 and PM10 data to be used as input for an LSTM/GRU model, with the goal of predicting the next hour's PM2.5 and PM10 values.

**Step 5: Model Development and Evaluation**

- Split the data into training, validation, and test sets (70% training, 15% validation, and 15% test) while maintaining the chronological order.

- Develop and train an LSTM model with normalized data, using sequences of 24-hour windows to predict future air quality values.

- Evaluate the model's performance using metrics such as Root Mean Square Error (RMSE) and Mean Absolute Error (MAE) on the test dataset to assess prediction accuracy.

### Conclusion

By following this use case, you will gain a comprehensive understanding of how to leverage data analysis, and machine learning to predict air quality. The actionable insights and recommendations derived from this analysis will aid in improving air quality management and policy-making, contributing to a healthier and more sustainable urban environment.

### References

1. _City of Melbourne_. (2020). Microclimate Sensors Data.  
   Available at: [https://data.melbourne.vic.gov.au/explore/dataset/microclimate-sensors-data/information/](https://data.melbourne.vic.gov.au/explore/dataset/microclimate-sensors-data/information/)

2. _City of Melbourne_. (2020). Argyle Square Air Quality Data.  
   Available at: [https://data.melbourne.vic.gov.au/explore/dataset/argyle-square-air-quality/information/](https://data.melbourne.vic.gov.au/explore/dataset/argyle-square-air-quality/information/)

3. Zhou, Q., & Zheng, Z. (2020). Air quality forecasting using environmental parameters: A case study.  
   _Journal of Environmental Management_, 269, 110774.

4. Hochreiter, S., & Schmidhuber, J. (1997). Long Short-Term Memory.  
   _Neural Computation_, 9(8), 1735-1780.

5. Chung, J., Gulcehre, C., Cho, K., & Bengio, Y. (2014). Empirical Evaluation of Gated Recurrent Neural Networks on Sequence Modeling.  
   _arXiv preprint arXiv:1412.3555_.

6. Zhang, Y., Li, M., & Wang, T. (2018). PM2.5 forecasting using machine learning models.  
   _Environmental Science and Pollution Research_, 25(19), 19072-19085.

7. Brownlee, J. (2018). A Gentle Introduction to Long Short-Term Memory Networks (LSTMs) for Time Series Forecasting.  
   _Machine Learning Mastery_. Available at: [https://machinelearningmastery.com](https://machinelearningmastery.com)

8. Guyon, I., & Elisseeff, A. (2003). An Introduction to Variable and Feature Selection.  
   _Journal of Machine Learning Research_, 3, 1157-1182.
