# DSA210-project
Data science project repository for the DSA 210, covering the full pipeline from data collection to machine learning analysis

# Project Overview
This project investigates whether Google Search trends and Reddit sentiment can anticipate real-world product demand for smartphones and laptops. By analyzing digital footprints, we aim to build a model that predicts market shifts before they happen.

# Data Sources and Enrichment
To meet the project's enrichment requirements, I have integrated three distinct data streams:

Sales Data (Base): Electronic Products Pricing Data (Kaggle) - Provides the ground truth for product demand.
Google Trends (Enrichment 1): Collected via the pytrends library to track search interest for 10-15 keywords over 5 years.
Reddit Data (Enrichment 2): Scraped via PRAW from r/gadgets and r/technology to capture post volume and consumer sentiment.

# Methodology 
Based on the proposal feedback, the following techniques are utilized:

Data Processing: All datasets are aligned to a weekly frequency to ensure consistency across 250 observations.
EDA: Time-series decomposition to find seasonality and Pearson Correlation to test lead/lag relationships.
Planned ML Technique: I will implement a Random Forest Regressor to model the non-linear relationship between social hype and sales.

# How to reproduce the analysis
Access the Notebook: Open DSA210_Analysis.ipynb in this repository.
Environment Setup: Launch the environment by clicking the button below.
Install Dependencies: Execute the following command in the first cell of the notebook to install the required libraries.
