# Hybrid LSTM + ARIMA for Aquifer Water Level Prediction

This project was developed as part of the **Statistical Learning course (AIT302)** at Xiamen University Malaysia.  
The objective was to forecast groundwater levels in the **Petrignano aquifer (Italy)** using the **ACEA Water Prediction dataset (Kaggle)**, by comparing traditional statistical models with deep learning methods and finally developing a **hybrid model** that combines their strengths.

---

## 🌍 Motivation
Water scarcity is one of the most pressing global challenges of our time. Aquifers act as natural reservoirs, supplying drinking water, supporting agriculture, and sustaining ecosystems. However, groundwater levels are influenced by a mix of complex factors including rainfall, temperature, river dynamics, and extraction volume.  

Accurate water-level prediction can:
- Support **sustainable water management**,  
- Help prevent over-extraction during droughts,  
- Assist agriculture and urban planning,  
- Protect natural ecosystems dependent on groundwater.  

The Petrignano aquifer was chosen for this study because it represents a **real-world, high-impact case** in central Italy where water management decisions directly affect human and environmental well-being.

---

## 📊 Dataset
- Source: [ACEA Water Prediction (Kaggle)](https://www.kaggle.com/competitions/acea-water-prediction)  
- Focus: **Petrignano Aquifer**  
- Variables analyzed: groundwater depth, rainfall, temperature, river hydrometry, and extraction rates.  
- Preprocessing steps:
  - Handled missing values (tested strategies, final choice: interpolation).  
  - Dropped features with weak correlation to groundwater levels.  
  - Resampled daily data to **weekly frequency** to smooth short-term noise and highlight seasonal patterns.  
  - Normalized selected features for stability in neural network training.

---

## ⚙️ Methodology
Three different modeling strategies were tested:

### 1. ARIMA (AutoRegressive Integrated Moving Average)
- Designed to capture **linear temporal dependencies**.  
- Parameters identified using **ACF/PACF plots** and the Augmented Dickey-Fuller (ADF) stationarity test.  
- Good at modeling general trend and short-term seasonality, but failed to capture more complex patterns.

### 2. LSTM (Long Short-Term Memory Network)
- Neural network capable of capturing **non-linear dependencies** and long-term patterns.  
- Architecture:
  - Two stacked LSTM layers (50 units each).  
  - Dropout layers for regularization.  
  - Dense output layer.  
- Trained with a look-back window of 4 (one month of weekly data).  
- Able to capture fluctuations better than ARIMA.

### 3. Hybrid LSTM + ARIMA
- Combined the two approaches:
  - Step 1: Train LSTM on the raw series to model non-linear dynamics.  
  - Step 2: Apply ARIMA on LSTM **residuals** to capture remaining linear patterns.  
  - Final forecast = LSTM prediction + ARIMA residual forecast.  
- Motivation: **LSTM handles complexity, ARIMA corrects bias**.

---

## 📈 Results
- **ARIMA**  
  - RMSE ≈ **1.11**  
  - Captured linear trends but poor at non-linear fluctuations.  

- **LSTM**  
  - RMSE ≈ **0.42**  
  - Strong improvement over ARIMA; captured both trend and seasonal shifts.  

- **Hybrid LSTM + ARIMA**  
  - RMSE ≈ **0.17**  
  - Best overall performance. Closely tracked observed water levels.  
  - Demonstrated the power of combining statistical and deep learning models.  

**Key insight:** The hybrid approach showed that linear + non-linear decomposition is more effective than relying on one model alone.

---

## 🌱 Reflection
Working on this project taught me several lessons:
- **Preprocessing is critical**: resampling to weekly data and carefully handling missing values made models more stable.  
- **Model choice matters less than data preparation**: ARIMA alone struggled, but after preparing features properly, even LSTM benefited.  
- **Hybrid models are practical**: the combination of LSTM and ARIMA gave robust results and improved interpretability.  
- **Statistical + ML approaches are complementary**: instead of replacing one with the other, the best results came from integration.  

This project strengthened my understanding of how to balance **traditional statistical methods with modern machine learning** for real-world forecasting tasks.

---

## 📌 Future Work
- Extend modeling to other aquifers in the ACEA dataset to test generalizability.  
- Incorporate **external climate variables** (temperature anomalies, rainfall indices) for richer input features.  
- Experiment with more advanced deep learning architectures (e.g., Temporal Convolutional Networks, Transformers for time series).  
- Package the hybrid approach into a **small forecasting application** for water management authorities.  

---

## 👩‍💻 Authors
- **Tan Yi Zhao** – Implemented LSTM and Hybrid model; led report writing and QA.  
- Sim Wen Ken – ARIMA modeling and literature review.  
- Leong Ting Yi – Evaluation metrics, experimental analysis, visualizations.  
- Wang Yuxuan – Data preprocessing, feature selection, introduction writing.  
