Air Quality Prediction for West Bengal using Machine Learning
📝 Project Goal
This project aims to analyze and predict air quality in West Bengal, India, using historical data from 2019 to 2024. The primary objectives are:

To quantitatively understand the relationship between various air pollutants and local meteorological conditions.

To build a robust machine learning model capable of forecasting the concentration of 13 different pollutants for the next 7 days.

To evaluate the model's performance using both numerical and visual metrics to ensure its real-world applicability.

📊 Dataset
The dataset used is across West Bengal cities 2019 to 2024 (1).csv, which contains daily air quality and meteorological readings from various cities, with a primary focus on Siliguri for this analysis.

Key features include:

Pollutants: PM2.5, PM10, NO2, SO2, CO, Ozone, etc.

Meteorological Parameters: Air Temperature (AT), Relative Humidity (RH), Wind Speed (WS), and Wind Direction (WD).

⚙️ Methodology
The project follows a structured approach from data cleaning to model deployment and evaluation.

1. Data Preprocessing
Data Cleaning: Loaded the dataset, standardized inconsistent column names, and removed columns with no data.

Timestamp Handling: Converted the Timestamp column to a proper datetime format and set it as the index for time-series analysis.

Missing Value Imputation: Handled missing data points using an expanding mean. This technique fills a null value with the average of all preceding data points, which is ideal for time-series data as it avoids using future information.

2. Exploratory Data Analysis (EDA)
EDA was performed to uncover patterns and relationships within the data.

Histograms: Plotted to visualize the distribution of key pollutants and weather variables.

Correlation Heatmap: A heatmap was generated to show the statistical correlation between all numerical variables. This visually confirmed expected relationships, such as the negative correlation between wind speed and pollutant concentrations.

3. Feature Engineering
Lag Features: To help the model learn from past trends, "lag features" were created. These are the pollutant values from the previous 7 days, which were used as inputs for predicting the current day's values.

🧠 Models Used
Two distinct modeling approaches were used to tackle the forecasting problem.

1. RandomForestRegressor (Multivariate Regression)
This was the primary model used for forecasting all pollutants simultaneously.

Why was it chosen?

Multi-Output Capability: It can predict all 13 pollutant types within a single, efficient model.

Handles Complexity: As an "ensemble" of hundreds of decision trees, it excels at capturing complex, non-linear relationships between weather, time, and pollution.

Robustness: It is less prone to overfitting and generally performs very well without extensive tuning.

How it works: The model was trained on the first 80% of the historical data. It learned the patterns connecting meteorological parameters and past pollution levels (the inputs) to the current pollution levels (the outputs).

2. ARIMA (Time-Series Analysis)
ARIMA (AutoRegressive Integrated Moving Average) is a classic statistical model used for time-series forecasting.

Why was it used? To provide a baseline and a different analytical perspective focused purely on the temporal patterns of a single pollutant.

How it works: An ARIMA model was built specifically for PM2.5. The auto_arima function was used to automatically find the optimal model parameters (p, d, q) by testing for stationarity and seasonality (assuming a 7-day, weekly pattern).

📈 Results & Evaluation
The models were tested on the most recent 20% of the data, which was kept hidden during training.

1. Numerical Accuracy (RMSE)
The Root Mean Squared Error (RMSE) was calculated for each pollutant predicted by the RandomForestRegressor. This metric represents the average error in the model's predictions. The low RMSE values across all pollutants indicated a high degree of numerical accuracy.

2. Visual Evaluation
Actual vs. Predicted Plot: A plot comparing the model's predicted PM2.5 values against the actual measured values showed that the model's predictions followed the real-world trends very closely, successfully capturing most peaks and troughs.

Confusion Matrix: To assess practical performance, the numerical PM2.5 predictions were converted into standard air quality categories (e.g., 'Good', 'Moderate', 'Poor'). A confusion matrix was then generated, showing a high number of correct classifications along the diagonal. This confirms that the model is not just numerically accurate but also effective at predicting the correct air quality level.
