
# Food Delivery Time Prediction Using Data Analytics and AI

**IBM Data Analytics with AI Project**  
**Author:** Bhavana  
**Dataset:** Food_Delivery_Times.csv (1,000 records)  
**Target Variable:** Delivery_Time_min

---

## Project Overview

This project builds a complete machine learning pipeline to predict food delivery time in minutes using regression analysis. The dataset contains 1,000 delivery records with weather, traffic, vehicle, and courier attributes.

### Key Results

| Model | MAE | RMSE | R² |
|---|---|---|---|
| Linear Regression | 7.2867 | 10.4505 | 0.7563 |
| Decision Tree | 8.5053 | 11.9056 | 0.6838 |
| **Random Forest** ⭐ | **6.9695** | **9.8684** | **0.7827** |

**Best Model: Random Forest Regressor** (R² = 0.7827 — explains 78.27% of variance)

---

## Dataset Description

| Column | Type | Description |
|---|---|---|
| Order_ID | Integer | Unique order identifier |
| Distance_km | Float | Delivery distance (0.59 – 19.99 km) |
| Weather | Categorical | Clear, Rainy, Foggy, Snowy, Windy |
| Traffic_Level | Categorical | Low, Medium, High |
| Time_of_Day | Categorical | Morning, Afternoon, Evening, Night |
| Vehicle_Type | Categorical | Bike, Car, Scooter |
| Preparation_Time_min | Integer | Kitchen prep time (5–29 min) |
| Courier_Experience_yrs | Float | Years of courier experience (0–9) |
| Delivery_Time_min | Integer | **TARGET** – Total delivery time (8–153 min) |

**Missing Values:** 30 records each in Weather, Traffic_Level, Time_of_Day, and Courier_Experience_yrs — handled via mode/median imputation.

---

## Project Structure

```
Bhavana_FoodDeliveryTimePrediction/
├── Food_Delivery_Times.csv                          # Dataset
├── Bhavana_FoodDeliveryTimePrediction.ipynb         # Main Jupyter Notebook
├── requirements.txt                                  # Python dependencies
├── README.md                                         # This file
├── Bhavana_FoodDeliveryTimePrediction_ProjectReport.docx  # Project Report
├── app.py                                            # Flask backend API
├── best_model.pkl                                    # Trained Random Forest model
├── scaler.pkl                                        # Feature scaler
├── label_encoders.pkl                                # Categorical encoders
├── model_results.json                                # Model metrics & stats
├── templates/
│   └── index.html                                    # Web application (single-page)
└── static/                                           # Static assets
```

---

## Setup and Installation

### 1. Install Dependencies
```bash
python -m pip install -r requirements.txt
```

### 2. Run the Jupyter Notebook
```bash
jupyter notebook Bhavana_FoodDeliveryTimePrediction.ipynb
```
Run all cells in order. The notebook will:
- Load and clean the dataset
- Perform EDA with 10+ visualizations
- Train Linear Regression, Decision Tree, and Random Forest
- Evaluate models and save artifacts (`.pkl`, `.json`)

### 3. Launch the Web Application
```bash
python app.py
```
Open [http://127.0.0.1:5001](http://127.0.0.1:5001) in your browser.

---

## Key Insights

1. **Distance is the #1 predictor** (importance: 73.3%) — longer routes always take more time
2. **Preparation time ranks 2nd** (importance: 15.5%) — reducing kitchen prep time has the biggest direct impact
3. **Snowy weather** causes the highest average delay: 67.1 min vs 53.1 min in clear conditions
4. **High traffic** adds ~12 minutes compared to low traffic (64.8 vs 52.9 min avg)
5. **Experienced couriers** (≥5 yrs) deliver significantly faster than new couriers
6. **Bike** is the most common vehicle (50.3%) but all vehicles have similar average delivery times

---

## Feature Importance (Random Forest)

| Rank | Feature | Importance |
|---|---|---|
| 1 | Distance_km | 73.27% |
| 2 | Preparation_Time_min | 15.53% |
| 3 | Courier_Experience_yrs | 3.67% |
| 4 | Traffic_Level | 2.65% |
| 5 | Weather | 2.42% |
| 6 | Time_of_Day | 1.27% |
| 7 | Vehicle_Type | 1.19% |

---

## Web Application Features

- **Home:** Project overview and KPI cards with real statistics
- **Analytics Dashboard:** Interactive charts (weather, traffic, vehicle, time-of-day)
- **Prediction Page:** Form using all 7 actual features → real model prediction
- **Dataset Explorer:** Browse and filter all 1,000 records
- **Model Performance:** Side-by-side comparison of all 3 models
- **Insights:** Data-driven findings and business recommendations
- **About:** Project details and methodology

---

## API Endpoints

| Endpoint | Method | Description |
|---|---|---|
| `/` | GET | Web application |
| `/api/predict` | POST | Predict delivery time |
| `/api/stats` | GET | Dataset statistics |
| `/api/models` | GET | Model performance metrics |
| `/api/dataset` | GET | Paginated dataset |
| `/api/feature-importance` | GET | Feature importance scores |

### Example Prediction Request
```json
POST /api/predict
{
  "Distance_km": 10.5,
  "Weather": "Rainy",
  "Traffic_Level": "High",
  "Time_of_Day": "Evening",
  "Vehicle_Type": "Bike",
  "Preparation_Time_min": 15,
  "Courier_Experience_yrs": 3
}
```

---

## IBM Data Analytics with AI — Methodology

1. **Data Collection:** 1,000 real delivery records
2. **Data Cleaning:** Mode/median imputation, duplicate check, outlier analysis
3. **EDA:** 10+ visualizations including distributions, correlations, category comparisons
4. **Preprocessing:** Label encoding, StandardScaler, 80/20 train-test split
5. **Model Training:** Linear Regression, Decision Tree, Random Forest
6. **Evaluation:** MAE, RMSE, R², 5-fold cross-validation
7. **Deployment:** Flask REST API + responsive web application
