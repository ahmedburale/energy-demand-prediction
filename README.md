# ⚡ Energy Demand Prediction

A complete data science pipeline that predicts power consumption for a city's electrical distribution network using **Random Forest** regression, exploratory data analysis, and Python visualization.

Built as a local Jupyter Notebook project in PyCharm.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Setup & Installation](#setup--installation)
- [Pipeline Overview](#pipeline-overview)
- [Key Findings](#key-findings)
- [Model Performance](#model-performance)
- [Business Recommendations](#business-recommendations)
- [Secret Mission: Peak Demand Classifier](#secret-mission-peak-demand-classifier)
- [License](#license)

---

## 🔍 Overview

Every time you flip a light switch or crank up the air conditioning, your local utility company is balancing the power grid in real time. Predicting when thousands of people will demand more electricity is one of the biggest challenges in the energy industry.

This project builds a machine learning model that predicts power consumption for a city's electrical distribution network using weather and time-based features. It explores the data with pandas, trains a Random Forest model in Python, and translates findings into actionable business recommendations for demand response planning.

---

## 📊 Dataset

- **Name:** Power Consumption of Tetouan City
- **Source:** [UCI Machine Learning Repository (Dataset #849)](https://archive.ics.uci.edu/dataset/849/power+consumption+of+tetouan+city)
- **Records:** 52,416 rows (10-minute intervals)
- **Time Range:** January 1, 2017 — December 30, 2017
- **File Size:** ~4 MB (CSV)

### Columns

| Column | Description |
|--------|-------------|
| `DateTime` | Timestamp at 10-minute intervals |
| `Temperature` | Weather temperature (°C) |
| `Humidity` | Relative humidity (%) |
| `Wind Speed` | Wind speed measurement |
| `general diffuse flows` | General diffuse solar radiation |
| `diffuse flows` | Diffuse solar radiation |
| `Zone 1 Power Consumption` | Power consumption in Zone 1 (target variable) |
| `Zone 2 Power Consumption` | Power consumption in Zone 2 |
| `Zone 3 Power Consumption` | Power consumption in Zone 3 |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.x | Programming language |
| pandas | Data loading, manipulation, and EDA |
| NumPy | Numerical computations |
| scikit-learn | Machine learning (Random Forest, train/test split, metrics) |
| matplotlib | Data visualization |
| seaborn | Statistical visualization (feature importance, confusion matrix) |
| Jupyter Notebook | Interactive development environment |
| PyCharm | IDE |

---

## 📁 Project Structure

```
Energy Demand Prediction/
├── energy-demand-prediction.ipynb    # Main Jupyter notebook with full pipeline
├── Tetuan City power consumption.csv # Dataset (download from UCI)
├── README.md                         # Project documentation
└── requirements.txt                  # Python dependencies
```

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.8+
- PyCharm (Community or Professional)

### Steps

1. **Clone or download this project**
   ```bash
   git clone 
   cd "Energy Demand Prediction"
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn jupyter
   ```

4. **Download the dataset**
   - Visit [UCI Dataset #849](https://archive.ics.uci.edu/dataset/849/power+consumption+of+tetouan+city)
   - Click **Download**, extract the zip
   - Place `Tetuan City power consumption.csv` in the project root

5. **Open the notebook**
   - Open PyCharm → Open the project folder
   - Open `energy-demand-prediction.ipynb`
   - Run all cells sequentially

---

## 🔬 Pipeline Overview

| Cell | Phase | Description |
|------|-------|-------------|
| 1 | **Data Loading** | Import libraries, load CSV with pandas, verify shape |
| 2 | **EDA - Summary Stats** | Date range, temperature range, zone averages |
| 3 | **EDA - Patterns** | Hourly consumption, top 10 peaks, temperature-demand relationship |
| 4 | **Feature Engineering** | Extract temporal features (hour, day_of_week, month, is_weekend), train/test split |
| 5 | **Model Training** | Train Random Forest Regressor, evaluate with MAE, RMSE, R² |
| 6 | **Visualization** | Actual vs Predicted scatter plot |
| 7 | **Feature Importance** | Horizontal bar chart ranking feature contributions |
| 8 | **Hourly Pattern** | Line chart showing daily demand curve |
| 9 | **Business Recommendations** | Programmatic recommendations for demand response |
| 10 | **🕵️ Peak Labels** | Define peak/off-peak using 75th percentile threshold |
| 11 | **🕵️ Classifier** | Train Random Forest Classifier, precision/recall report |
| 12 | **🕵️ Confusion Matrix** | Heatmap visualization, false negative rate analysis |

---

## 📈 Key Findings

### Consumption Patterns
- **Peak hours:** 18:00–22:00 (evening), with hour 20 reaching ~43,800 avg consumption
- **Low demand:** 05:00–06:00, dropping to ~23,200 avg consumption
- **Temperature impact:** Hot days (>25°C) average 37,683 vs Cold days (<15°C) at 29,016 — a **~30% increase**
- **Top 10 peaks:** All occurred in **August 2017** between **7–8 PM**, with temps 25–28°C

### Feature Importance (Random Forest)

| Rank | Feature | Importance |
|------|---------|------------|
| 1 | hour | 0.7554 |
| 2 | Temperature | 0.0951 |
| 3 | month | 0.0716 |
| 4 | general diffuse flows | 0.0231 |
| 5 | day_of_week | 0.0175 |
| 6 | Humidity | 0.0123 |
| 7 | diffuse flows | 0.0121 |
| 8 | Wind Speed | 0.0119 |
| 9 | is_weekend | 0.0010 |

> **Key insight:** Time of day alone accounts for **75.5%** of prediction power, making it the dominant demand driver.

---

## 🎯 Model Performance

### Regression Model (Random Forest Regressor)

| Metric | Value |
|--------|-------|
| **R² Score** | 0.9717 |
| **Variance Explained** | 97.2% |
| **n_estimators** | 100 |
| **max_depth** | 15 |
| **Features** | 9 (5 weather + 4 temporal) |
| **Training samples** | ~41,932 |
| **Test samples** | ~10,484 |

The scatter plot of Actual vs Predicted values shows tight clustering around the perfect prediction line across the full consumption range (15,000–52,000+).

---

## 💼 Business Recommendations

1. **Peak Demand Hours: [18, 19, 20, 21, 22]**
   Schedule demand response events during evening hours when consumption is highest.

2. **Temperature Trigger: 26.4°C**
   When temperature exceeds 26.4°C, consumption increases by **21.3%** on average. Pre-trigger demand response when forecasted temperature exceeds this threshold.

3. **Weekday vs Weekend**
   - Weekday average: 32,676
   - Weekend average: 31,517
   - Focus demand response resources on **weekdays**.

4. **Model Confidence: R² = 0.9717**
   The model explains 97.2% of consumption variance.
   Primary drivers: **hour** and **Temperature**.

---

## 🕵️ Secret Mission: Peak Demand Classifier

Reframed the regression problem as a **binary classification** task:
- **Peak:** Zone 1 consumption > 75th percentile
- **Off-Peak:** Zone 1 consumption ≤ 75th percentile

### Classifier Details
- **Algorithm:** RandomForestClassifier (100 trees, max_depth=15)
- **Evaluation:** Precision, Recall, F1-Score, Confusion Matrix

### Business Interpretation
- **False negatives** (missed peaks) are critical — failing to trigger demand response risks grid strain or expensive emergency power purchases
- **False positives** (unnecessary triggers) cost money but don't risk reliability
- In utility operations, **reliability > cost**, making recall the priority metric for peak detection

---

## 📝 Requirements

```
pandas>=1.5.0
numpy>=1.23.0
scikit-learn>=1.2.0
matplotlib>=3.6.0
seaborn>=0.12.0
jupyter>=1.0.0
```

Save as `requirements.txt` and install with:
```bash
pip install -r requirements.txt
```

---

## 🙏 Acknowledgments

- **Dataset:** [UCI Machine Learning Repository — Power Consumption of Tetouan City](https://archive.ics.uci.edu/dataset/849/power+consumption+of+tetouan+city)
- **Project:** Built as part of the [NextWork](https://learn.nextwork.org) Data Science learning path

---

## 📄 License

This project is for educational purposes. The dataset is provided by the UCI Machine Learning Repository under their terms of use.
