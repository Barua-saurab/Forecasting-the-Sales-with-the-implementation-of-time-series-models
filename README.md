# Forecasting-the-Sales-with-the-implementation-of-time-series-models

## 📌 Project Overview
This project focuses on **weekly sales forecasting** using time-series models applied to an online retail dataset.  
The objective is to **compare multiple forecasting techniques** and identify the model that provides the most accurate predictions for retail sales.

The analysis evaluates model performance using:
- **MAE (Mean Absolute Error)**
- **RMSE (Root Mean Squared Error)**

---

## 📊 Dataset
- **Source:** [Online Retail.xlsx  ](https://archive.ics.uci.edu/dataset/352/online+retail)
- **Data Type:** Transaction-level retail sales data  
- **Time Period:** December 2010 – November 2011  
- **Key Columns:** InvoiceDate, Quantity, UnitPrice, Country

---

## 🧹 Data Preparation & Feature Engineering

### Data Cleaning
- Removed records where:
  - `Quantity ≤ 0`
  - `UnitPrice ≤ 0`
- Converted `InvoiceDate` to datetime format
- Excluded **December 2011** to avoid incomplete month bias

### Feature Engineering
- Created a new column:Sales = Quantity × UnitPrice
  
### Resampling
- Aggregated transactional data into **Weekly Sales** using: resample('W').sum()

  ---

## 🔍 Exploratory Data Analysis (EDA)

The following analyses were performed:
- 📈 Weekly Sales Trend
  <img width="591" height="471" alt="image" src="https://github.com/user-attachments/assets/969cf251-c51c-4a47-89d3-99138499e84e" />

- 📉 Monthly Sales Trend
  <img width="561" height="471" alt="image" src="https://github.com/user-attachments/assets/ac394e13-8a94-4c34-a56f-34650b9db17c" />

- 🌍 Top 10 Countries by Sales
  <img width="534" height="552" alt="image" src="https://github.com/user-attachments/assets/de51dc41-d59f-4ce0-a1ea-833d8d7e77a4" />

- 🛒 Top 10 Products by Quantity Sold
<img width="1116" height="470" alt="image" src="https://github.com/user-attachments/assets/8b8dcc5c-4491-4110-83e8-e0a41877eedd" />

These visualizations helped identify:
- Overall sales trend
- Country-level contribution
- High-demand products

---

## 🔀 Train-Test Split
- **Chronological split** to preserve time order
- Last **10 weeks** used as test data
---
## 🛠️ Models Implemented
<img width="1012" height="528" alt="image" src="https://github.com/user-attachments/assets/d4243c6a-032c-4c3c-b451-a4753d1280f0" />

### 1️⃣ Double Exponential Smoothing (Holt’s Method)
- Captures **trend** but ignores seasonality
- Suitable for data with a consistent upward or downward movement

### 2️⃣ Triple Exponential Smoothing (Holt-Winters)
- Captures **trend + seasonality**
- Seasonal period set to **4 weeks**
<img width="1012" height="528" alt="image" src="https://github.com/user-attachments/assets/e4c011fa-f39a-4483-b793-59546dcfee1e" />

### 3️⃣ ARIMA (Auto-Regressive Integrated Moving Average)

#### Auto-ARIMA
- Used `pmdarima.auto_arima`
- Automatically selected optimal parameters using **AIC**
- Best model found: ARIMA(2,0,0)


#### Manual ARIMA (2,1,0)
- Manually tuned model
- Differencing (`d = 1`) applied to remove trend
- Provided the **best forecasting performance**

---


## 📈 Model Evaluation & Results

### 📊 Model Performance Comparison

| Model                              | MAE        | RMSE       |
|-----------------------------------|------------|------------|
| Double Exponential Smoothing      | 57,499.31  | 70,094.03  |
| Triple Exponential Smoothing      | 65,575.88  | 82,394.31  |
| Manual ARIMA (2,1,0)              | **57,152.43** | **69,572.43** |

---

## 🏆 Best Performing Model
- **Manual ARIMA (2,1,0)** achieved the **lowest MAE and RMSE**
- Differencing helped stabilize the sales trend
- Provided the most reliable weekly forecasts

---



### 🎯 Total Monthly Sales Target
**1,222,422.98**

---

## 🚀 Tools & Technologies
- Python  
- Pandas, NumPy  
- Matplotlib  
- statsmodels  
- pmdarima  
- Google Colab  

---

## 📌 Key Takeaways
- Weekly aggregation reduces noise in transactional data
- ARIMA models outperform exponential smoothing for this dataset
- Manual parameter tuning can outperform automated approaches
- Time-series forecasting is highly sensitive to trend handling
