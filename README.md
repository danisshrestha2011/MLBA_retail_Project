# MLBA-CIA2
Retail Customer Repeat Purchase Prediction

A machine learning project that predicts whether an existing retail customer is likely to make a repeat purchase based on their historical purchasing behaviour.

Project Overview

This project uses the Online Retail transaction dataset and applies customer-level feature engineering and classification models to predict repeat purchasing behaviour.

The workflow covers:

Data loading and initial inspection

Data cleaning and preprocessing

Exploratory Data Analysis (EDA)

Customer-level feature engineering

Repeat-purchase target creation using a historical/future time split

Classification using Logistic Regression and Random Forest

Model evaluation using Accuracy, Precision, Recall and F1 Score

Random Forest feature-importance analysis

Model serialization using Joblib

A Streamlit application for interactive predictions

Business Problem

Retail businesses need to identify customers who are likely to purchase again so that they can improve customer retention, targeting and marketing decisions.

The objective of this project is:

To predict whether an existing customer will make a repeat purchase using their historical purchasing behaviour.

The prediction can help a business identify customers who may be more likely to return and support data-driven customer engagement strategies.

Dataset

The project uses the Online Retail.xlsx dataset.

The dataset initially contains:

541,909 transactions

8 columns

Main Variables

Column

Description

InvoiceNo

Invoice/transaction number

StockCode

Product code

Description

Product description

Quantity

Quantity purchased

InvoiceDate

Transaction date and time

UnitPrice

Price per unit

CustomerID

Customer identifier

Country

Customer country

The original data covers transactions from 1 December 2010 to 9 December 2011.

Data Cleaning

The notebook performs the following preprocessing steps:

Converts InvoiceDate to datetime format.

Removes records with missing CustomerID.

Removes duplicate records.

Removes cancellation transactions where InvoiceNo starts with C.

Removes transactions with non-positive Quantity.

Removes transactions with non-positive UnitPrice.

Creates TransactionValue:

TransactionValue = Quantity × UnitPrice

The notebook also checks missing values, duplicate records, negative quantities and non-positive prices before cleaning.

Machine Learning Approach

1. Historical and Future Split

Instead of randomly creating the target variable, the project uses a time-based approach.

A cutoff date is created 270 days after the earliest transaction date.

Transactions up to the cutoff date are treated as historical data.

Transactions after the cutoff date are treated as future data.

Customers appearing in the future period are labelled as repeat purchasers.

Target Variable

RepeatPurchase

Value

Meaning

0

No repeat purchase in the future period

1

Repeat purchase in the future period

This approach allows the model to learn from past customer behaviour while using future purchasing activity as the prediction target.

Feature Engineering

Customer-level behavioural features are generated from the historical transactions.

Feature

Description

Recency

Number of days since the customer's most recent purchase

Frequency

Number of unique invoices/orders

Monetary

Total historical transaction value

AvgOrderValue

Average transaction value per order

TotalQuantity

Total quantity purchased

UniqueProducts

Number of unique products purchased

These features represent key dimensions of customer purchasing behaviour.

Exploratory Data Analysis

The notebook explores:

Repeat purchase distribution

Recency vs. repeat purchase

Frequency vs. repeat purchase

Monetary value vs. repeat purchase

Correlation between numerical customer features

Visualizations are created using Matplotlib and Seaborn.

Models

Two classification algorithms are implemented.

Logistic Regression

Logistic Regression is used as a baseline classification model.

The numerical features are standardized using StandardScaler before training.

Random Forest

A Random Forest classifier is also trained with:

n_estimators = 200

random_state = 42

class_weight = "balanced"

The model is used for classification and feature-importance analysis.

Model Evaluation

The models are evaluated using:

Accuracy

Precision

Recall

F1 Score

Confusion Matrix

Classification Report

The notebook also creates a model comparison table containing the evaluation metrics for Logistic Regression and Random Forest.

The README intentionally does not hard-code model scores because the notebook should remain the source of truth for the latest executed results.

Feature Importance

Random Forest feature importance is calculated to understand which customer-level variables contribute most to the model's predictions.

The resulting feature-importance table is sorted in descending order.

Streamlit Application

The project includes an interactive Streamlit application, app.py.

The application contains three sections:

Business Problem

Explains the purpose of the customer repeat-purchase prediction project.

Data Insights

Displays the repeat-purchase distribution using an interactive bar chart.

Prediction

Users can enter:

Recency

Frequency

Monetary value

Average Order Value

Total Quantity

Unique Products

The application then returns:

Repeat Purchase or No Repeat Purchase

Probability of repeat purchase

Project Structure

.
├── MLBA_CIA2.ipynb
├── Online Retail.xlsx
├── app.py
├── logistic_regression_model.pkl
├── scaler.pkl
├── feature_names.pkl
├── retail_purchase_model.pkl
├── requirements.txt
└── README.md

File Description

File

Purpose

MLBA_CIA2.ipynb

Complete data analysis and machine learning workflow

Online Retail.xlsx

Retail transaction dataset

app.py

Streamlit prediction application

logistic_regression_model.pkl

Saved Logistic Regression model used by the Streamlit app

scaler.pkl

Saved feature scaler used by the Streamlit app

feature_names.pkl

Saved feature-name list used to construct prediction inputs

retail_purchase_model.pkl

Saved Random Forest model generated in the notebook

requirements.txt

Python dependencies

README.md

Project documentation

Installation

Clone the repository and move into the project directory:

git clone <your-repository-url>
cd <your-repository-folder>

Install the required Python packages:

pip install -r requirements.txt

If requirements.txt is not available, the main libraries used in the notebook/application include:

pip install pandas matplotlib seaborn scikit-learn openpyxl joblib streamlit

Run the Jupyter Notebook

Open the notebook with Jupyter:

jupyter notebook MLBA_CIA2.ipynb

Or open it in Google Colab after uploading the required dataset.

Make sure Online Retail.xlsx is available in the expected working directory.

Run the Streamlit App

After ensuring the dataset and saved model files are present, run:

streamlit run app.py

The application will open in your browser.

Technologies Used

Python

Pandas — data manipulation

NumPy — numerical operations

Matplotlib — visualization

Seaborn — statistical visualization

Scikit-learn — machine learning

Joblib — model serialization

Streamlit — interactive web application

Jupyter Notebook / Google Colab — development environment

Excel — source dataset format

Machine Learning Workflow

Online Retail Dataset
        ↓
Data Inspection
        ↓
Data Cleaning
        ↓
Transaction Value Creation
        ↓
Historical / Future Time Split
        ↓
Customer Feature Engineering
        ↓
Repeat Purchase Target
        ↓
Exploratory Data Analysis
        ↓
Train/Test Split
        ↓
 ┌───────────────────────┐
 │                       │
 ▼                       ▼
Logistic Regression   Random Forest
 │                       │
 └───────────┬───────────┘
             ↓
     Model Evaluation
             ↓
   Feature Importance
             ↓
      Model Serialization
             ↓
       Streamlit App

Key Learning Outcomes

This project demonstrates practical skills in:

Retail customer analytics

Data cleaning

Feature engineering

Customer behaviour analysis

Time-based target construction

Binary classification

Model comparison

Model evaluation

Feature importance

Model deployment basics

Streamlit application development

Limitations

The target variable is constructed from the available historical/future transaction period.

The model is based only on the behavioural variables engineered in the notebook.

The project does not include external customer demographic or marketing-channel information.

Model performance depends on the dataset and the time period used for training and evaluation.

The Streamlit application currently loads the Logistic Regression model and its corresponding scaler.

Future Improvements

Possible extensions include:

Hyperparameter tuning

Cross-validation

ROC-AUC and Precision-Recall analysis

Class imbalance analysis

More advanced customer segmentation

RFM-based segmentation

Additional temporal features

Gradient Boosting/XGBoost models

Model monitoring

Cloud deployment

Improved Streamlit dashboard with KPIs and customer segments

Author

Danis Shrestha

This project was developed as a machine learning and business analytics project using retail transaction data.
