# Weather Prediction Model with LSTM and Ridge Regression

### Author: Abdelazim Lokma  
### Course: CS-542 Principles of Machine Learning  
### Task: Predicting Maximum Temperature for Multiple Cities

## Introduction

This project aims to predict the maximum temperature for a collection of cities using machine learning techniques. The goal is to leverage historical weather data to make predictions that can be used on the Kalshi event-based trading platform, which allows trading on the occurrence of events rather than stock prices. The main focus is to explore and compare the performance of two models: a complex LSTM model and a Ridge Regression model.

## Data Sources

The data used for model training and testing is collected from multiple APIs:

1. **Open Meteo**: Provides historical weather data, including temperature, daylight duration, sunshine duration, and wind speed. The data spans from 2015 to the present day.
2. **MeteoStat**: Another source of historical weather data, covering more years than Open Meteo, enriching the dataset with additional features such as average temperature (TAVG) and pressure.
3. **WeatherBit**: This API provides weather forecasts for future dates and was primarily used to compare the LSTM model's predictions against actual forecasts.
4. **NOAA**: Manually downloaded CSV files from Miami, used initially for quick testing.
5. **Visual Crossing**: Limited to 1000 records per day, this API fills any gaps that exist in the previous datasets.

## Model 1: LSTM Model

The LSTM (Long Short-Term Memory) model is designed to handle time-series data, making it suitable for weather predictions. Several variations of the LSTM model were experimented with, including different architectures and hyperparameters. The final model uses a bidirectional LSTM layer, followed by three LSTM layers, dropout layers for regularization, and dense layers for output processing.

### LSTM Model Architecture:
- **Input**: Weather data for each city with features like temperature, wind speed, and daylight duration.
- **Layers**: 
    - Bidirectional LSTM
    - Three stacked LSTM layers
    - Dense layers with ReLU activation
    - Dropout layers (0.3 rate) to reduce overfitting
- **Output**: Predicted maximum temperature for the next day.

### Results

- **Miami**: Mean Absolute Error (MAE) = 5°F
- **Chicago**: MAE = 7.2°F
- **Austin**: MAE = 4.8°F
- **New York**: MAE = 7.3°F

While the LSTM model performed reasonably well, the MAE varied significantly between cities, with warmer cities like Austin seeing better results.

## Model 2: Ridge Regression Model

Due to the LSTM model's poor performance on some cities, I implemented a simpler Ridge Regression model. This model performs better with significantly lower MAE values, especially for Miami.

### Ridge Regression Architecture:
- **Input**: Same as LSTM, but with additional feature engineering to create a "target" column for temperature.
- **Model**: Ridge regression with alpha=0.1 to prevent overfitting.

### Results

- **Miami**: MAE = 2.19°F
- **Chicago**: MAE = 5.6°F
- **Austin**: MAE = 3.7°F
- **New York**: MAE = 4.5°F

The Ridge Regression model achieved better results than the LSTM, particularly for cities with warm climates like Miami and Austin.

## Kalshi Trading Strategy

Kalshi is a trading platform that allows users to buy and sell contracts based on event outcomes, such as weather forecasts. In this project, I traded based on the temperature predictions of the LSTM model and later the Ridge Regression model.

- **Week 1**: Random trades while learning the platform.
- **Week 2**: Trades based on LSTM predictions.
- **Week 3**: Hedged trades, using both YES and NO contracts to minimize losses.

### Trading Results

My trading strategy initially struggled due to the LSTM model's poor performance. However, using a combination of the Ridge Regression model and a hedging strategy improved profitability. A detailed trading log is included in the project files.

## Conclusion

While the LSTM model is powerful for time-series prediction, its performance in this case was inconsistent across different cities. On the other hand, the Ridge Regression model proved to be simpler and more effective for this task, achieving better overall accuracy. In the future, I would like to explore hybrid models that combine the strengths of both approaches.

## How to Run This Project

1. Run the Jupyter notebook `lstm_and_rr_models.ipynb` to see the data processing, model training, and evaluation.

2. You can also execute the Kalshi trading strategy by using the trading script found in `kalshi_trading.py`.

## Project Files

- `lstm_and_rr_models.ipynb`: (Jupyter notebook with LSTM and Ridge Regression models)
- `kalshi_trading.py`: Python script for implementing the Kalshi trading strategy.
- `Kalshi-Recent-Activity.csv`: CSV file showing the trades made on Kalshi.
- `README.md`: This file.
