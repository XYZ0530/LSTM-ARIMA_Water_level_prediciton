# LSTM-ARIMA_Water_level_prediciton

# Hybrid LSTM + ARIMA for Aquifer Water Level Prediction

This project was developed for the **Statistical Learning course (AIT302)** at Xiamen University Malaysia.  
The goal was to predict groundwater levels in the **Petrignano aquifer (Italy)** using statistical and machine learning methods, applying them to the **ACEA Water Prediction dataset (Kaggle)**.

---

## 🌍 Motivation
Water scarcity is one of the most pressing global challenges. Aquifers are vital groundwater reservoirs, but their dynamics are complex, influenced by rainfall, temperature, river levels, and extraction rates.  
Accurate forecasting of water levels is critical for:
- Ensuring sustainable extraction,
- Preventing overuse during droughts,
- Supporting agriculture and urban water supply,
- Protecting ecosystems.

---

## 📊 Dataset
- Source: [ACEA Water Prediction (Kaggle)](https://www.kaggle.com/competitions/acea-water-prediction)  
- Focus: **Petrignano Aquifer**  
- Variables considered: groundwater depth, rainfall, temperature, river hydrometry, and extraction volume.  
- Preprocessing steps:
  - Dropped weakly correlated features,
  - Handled missing values (tested multiple strategies, chose interpolation),
  - Resampled daily data to **weekly level** to highlight long-term trends.

---

## ⚙️ Methodology
We compared three approaches:

1. **ARIMA (AutoRegressive Integrated Moving Average)**  
   - Captures **linear patterns** and short-term dependencies.  
   - Tuned using ACF/PACF plots and stationarity tests (ADF).  

2. **LSTM (Long Short-Term Memory networks)**  
   - Captures **non-linear dependencies** and long-term temporal patterns.  
   - Architecture: 2 LSTM layers (50 units each), dropout, dense output.  
   - Trained with look_back = 4 (one month of weekly data).  

3. **Hybrid LSTM + ARIMA**  
   - Step 1: LSTM predicts nonlinear dynamics.  
   - Step 2: ARIMA models residuals to capture leftover linear structure.  
   - Final forecast = LSTM prediction + ARIMA residual forecast.

---

## 📈 Results
- **ARIMA**: RMSE ≈ 1.11 → failed to capture non-linear fluctuations.  
- **LSTM**: RMSE ≈ 0.42 → significantly better at modeling patterns.  
- **Hybrid LSTM + ARIMA**: RMSE ≈ 0.17 → best performance, closely tracked actual groundwater levels.  

The hybrid approach combined the strengths of both models, delivering **accurate, stable, and interpretable forecasts**.

---

## 📂 Repository Structure
