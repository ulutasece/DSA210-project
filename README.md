DSA210 — Can Google Search Trends Predict Consumer Electronics Demand?
Data science project for DSA 210: Introduction to Data Science.

Project Overview
This project investigates whether Google Search Trends for consumer electronics keywords (iphone, laptop, smartphone, gaming laptop) can predict consumer electronics demand. Demand is measured using Amazon Electronics product review volume — a publicly available proxy for purchasing activity — filtered to the Headphones and Computers & Accessories categories.
The core hypothesis is that search interest precedes purchasing behaviour by one to four weeks, meaning Trends data can serve as a leading indicator of demand.

Data Sources
Dataset
Description
Source
Amazon Electronics Reviews
1.29M product reviews, 2013–2018, filtered to Headphones + Computers & Accessories
UCSD Amazon Dataset
Google Trends
Weekly search interest for iphone, laptop, smartphone, gaming laptop (US, 2013–2018)
Collected via pytrends

Setting up the data
Download electronics.csv from the UCSD link above
Place it in the data/ folder as data/electronics.csv
Google Trends data is fetched automatically when you run the EDA notebook — no manual download needed


Repository Structure
DSA210-project/
├── data/
│   └── electronics.csv        ← place the Amazon dataset here
├── DSA210_EDA_Final.ipynb     ← data loading, preprocessing, EDA, hypothesis tests
├── DSA210_ML_Final.ipynb      ← ML models, feature importance, ablation, interpretation
├── requirements.txt
└── README.md

Methodology
EDA Notebook:
Filters Amazon data to target categories (Headphones, Computers & Accessories)
Aggregates to weekly review volume as the demand proxy
Fetches Google Trends data via pytrends for the matching keywords
Merges and cleans both datasets
Feature engineering: lag features, rolling statistics, seasonal flags
EDA: time-series decomposition, lag correlation analysis, correlation heatmap
Hypothesis testing: Shapiro-Wilk normality, Spearman/Pearson correlation, Mann-Whitney U for Q4 seasonality
Saves final_real_dataset.csv for the ML notebook
ML Notebook:
Loads final_real_dataset.csv
Engineers lag and rolling features for both demand and Trends signals
Selects train/test split using an elbow method (CV-RMSE curve)
Temporal train/test split with StandardScaler (no data leakage)
Trains and compares 5 models: Linear Regression, Ridge, Random Forest, Gradient Boosting, SVR
Feature importance analysis (Random Forest Gini importance)
Ablation study: quantifies how much removing Google Trends degrades performance
Residual analysis: ACF plot, Durbin-Watson statistic

Key Findings
Google Trends for electronics keywords shows a statistically significant correlation with Amazon review volume, peaking at a 2-week lag
Including Trends features reduces model CV-RMSE by 3–8% vs a model without them
Q4 (October–December) is the strongest structural driver of demand spikes (Mann-Whitney U p < 0.05)
Random Forest and Gradient Boosting outperform linear models due to non-linear seasonal interactions
Demand autoregression (past review lags) remains the single most important feature group

How to Reproduce
# 1. Clone the repo
git clone https://github.com/ulutasece/DSA210-project.git
cd DSA210-project

# 2. Install dependencies
pip install -r requirements.txt

# 3. Place electronics.csv in the data/ folder

# 4. Run the EDA notebook first — it generates final_real_dataset.csv
# 5. Then run the ML notebook
Run both notebooks top-to-bottom in order. The EDA notebook must be run first as it produces final_real_dataset.csv which the ML notebook loads.

