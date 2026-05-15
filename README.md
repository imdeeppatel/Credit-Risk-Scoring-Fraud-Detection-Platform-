# Credit Risk Scoring & Fraud Detection Platform

**Deloitte – Fortune 500 Financial Client**

A production-grade machine learning platform for credit risk assessment and real-time fraud detection, built to process large-scale financial datasets — improving loan approval accuracy by 15% and reducing fraud false positives by 40%.

---

## Overview

This platform delivers two integrated ML-driven capabilities for a Fortune 500 financial institution:

1. **Credit Risk Scoring** — Predictive models that assess borrower risk profiles to inform loan approval decisions with greater accuracy and consistency than rule-based systems.
2. **Fraud Detection** — An anomaly detection module connected to real-time data feeds that flags suspicious transactions while dramatically reducing false positive rates and manual review burden.

Built with Python and PySpark to handle large-scale financial datasets, the platform is designed for reliability, interpretability, and operational integration.

---

## Key Features

- **ML-Based Credit Scoring** — Supervised models trained on historical loan and borrower data to produce risk scores for new applicants
- **Anomaly Detection Module** — Statistical modeling to identify fraudulent transaction patterns in real time
- **PySpark Pipeline** — Distributed data processing to handle large-scale financial datasets efficiently
- **False Positive Reduction** — Precision-tuned fraud models that cut false positive rate by 40%, reducing manual review overhead
- **Real-Time Data Integration** — Live data feeds connected to the fraud detection module for near-instantaneous flagging

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python |
| Distributed Processing | PySpark (Apache Spark) |
| ML Modeling | scikit-learn, MLlib |
| Statistical Modeling | scipy, statsmodels |
| Data Processing | pandas, NumPy |
| Real-Time Feeds | Kafka / Streaming pipeline |
| Environment | Databricks / Spark cluster |

---

## Architecture

```
Financial Data Sources
(loan applications, transaction feeds)
        │
        ▼
  PySpark Data Pipeline
  (ingestion, cleaning, feature engineering)
        │
        ├─────────────────────────────────────┐
        ▼                                     ▼
Credit Risk Scoring Module          Fraud Detection Module
(supervised ML models)              (anomaly detection)
        │                                     │
        ▼                                     ▼
  Risk Score Output               Real-Time Fraud Alerts
  (loan approval decision)        (flagged transactions)
        │                                     │
        └──────────────┬──────────────────────┘
                       ▼
            Downstream Systems
     (loan processing, fraud review queue)
```

---

## Modules

### 1. Credit Risk Scoring

Predicts the probability of default for loan applicants using supervised classification models.

**Approach:**
- Feature engineering on borrower attributes (credit history, income, DTI ratio, etc.)
- Model training with cross-validation and hyperparameter tuning
- Threshold calibration to balance approval rate vs. default risk
- Model interpretability via feature importance and SHAP values

**Models Evaluated:**
- Logistic Regression (baseline)
- Gradient Boosting (XGBoost / LightGBM)
- Random Forest

**Key Metric:** 15% improvement in loan approval accuracy over prior rule-based system

---

### 2. Fraud Detection & Anomaly Detection

Identifies fraudulent transactions in real time using statistical and ML-based anomaly detection.

**Approach:**
- Baseline behavioral profiling per account/user
- Statistical anomaly scoring (z-score, IQR, isolation forest)
- Real-time scoring against incoming transaction streams
- Alert thresholding tuned to minimize false positives

**Key Metric:** 40% reduction in false positives, significantly reducing manual review overhead

---

## KPIs & Model Performance

| Metric | Result |
|---|---|
| Loan Approval Accuracy Improvement | +15% |
| Fraud False Positive Reduction | -40% |
| Dataset Scale | Large-scale (distributed via PySpark) |
| Scoring Latency (Fraud) | Near real-time |

---

## Project Structure

```
credit-risk-fraud-platform/
├── data/
│   ├── raw/                        # Raw input datasets (not committed)
│   └── processed/                  # Feature-engineered datasets
├── credit_risk/
│   ├── feature_engineering.py      # Borrower feature extraction and transformation
│   ├── model_training.py           # Model training, cross-validation, tuning
│   ├── model_evaluation.py         # Accuracy, AUC-ROC, confusion matrix
│   └── scoring_pipeline.py         # Batch scoring for new applicants
├── fraud_detection/
│   ├── anomaly_detection.py        # Statistical anomaly scoring module
│   ├── realtime_feed.py            # Real-time data stream integration
│   ├── alert_thresholding.py       # False positive tuning logic
│   └── evaluation.py               # Precision, recall, F1 analysis
├── pyspark_jobs/
│   ├── ingest_pipeline.py          # PySpark ingestion and preprocessing jobs
│   └── feature_pipeline.py         # Distributed feature engineering at scale
├── notebooks/
│   ├── credit_risk_eda.ipynb       # Exploratory data analysis — credit data
│   └── fraud_eda.ipynb             # Exploratory data analysis — transaction data
├── docs/
│   ├── model_card.md               # Model documentation and intended use
│   └── data_dictionary.md          # Field-level documentation
├── requirements.txt
└── README.md
```

---

## Setup & Usage

### Prerequisites

- Python 3.9+
- Apache Spark / PySpark environment (Databricks or local Spark cluster)
- Access to financial data source (internal credentials required)

### Installation

```bash
git clone https://github.com/your-org/credit-risk-fraud-platform.git
cd credit-risk-fraud-platform
pip install -r requirements.txt
```

### Running the Credit Risk Pipeline

```bash
# Feature engineering
python credit_risk/feature_engineering.py --input data/raw/loan_applications.csv

# Model training
python credit_risk/model_training.py --config configs/credit_risk_config.yaml

# Batch scoring
python credit_risk/scoring_pipeline.py --input data/processed/new_applicants.csv
```

### Running the Fraud Detection Module

```bash
# Start real-time feed listener
python fraud_detection/realtime_feed.py --stream kafka://your-broker/transactions

# Run anomaly detection on historical data
python fraud_detection/anomaly_detection.py --input data/raw/transactions.csv
```

### PySpark Jobs (large-scale)

```bash
spark-submit pyspark_jobs/ingest_pipeline.py
spark-submit pyspark_jobs/feature_pipeline.py
```

---

## Impact

- **+15% loan approval accuracy** — Replaced rule-based credit decisions with ML-driven risk scoring, reducing both false approvals and unnecessary rejections
- **-40% fraud false positives** — Precision-tuned anomaly detection significantly cut manual review queue volume, saving analyst hours
- **Scalable architecture** — PySpark-based pipeline handles large-scale financial datasets with distributed processing

---

## Compliance & Security

- All financial data is handled in accordance with client data governance and compliance requirements
- No raw PII or financial records are committed to version control
- Models are documented via model cards covering intended use, limitations, and bias considerations

---

*Developed at Deloitte for a Fortune 500 Financial Client — Confidential*
