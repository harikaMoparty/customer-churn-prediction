# 📉 Customer Churn Prediction
### *Predicting customer attrition before it costs you — using interpretable ML*

**Author:** ***HARIKA MOPARTY***

---

## 🧩 Problem Statement & Business Impact

Customer churn — when a customer stops doing business with a company — is one of the costliest problems in subscription-based and service industries. Acquiring a new customer costs **5–7× more** than retaining an existing one.

This project trains and compares two **binary classification models** — **Logistic Regression** and a **Decision Tree Classifier** — to identify customers at high risk of churning *before* they leave. Both models are evaluated on the same test set; the better-performing one (by F1-Score) is automatically selected as the final model. Both algorithms are intentionally simple and interpretable so that business stakeholders — not just data scientists — can understand and act on their outputs.

---

## 🛠️ Tech Stack & Tools

| Category | Tools |
|---|---|
| Language | ![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python) |
| Data Manipulation | `pandas` · `numpy` |
| Visualization | `matplotlib` · `seaborn` |
| Machine Learning | `scikit-learn` |
| Environment | Jupyter Notebook |

---

## 📊 Dataset Description

**Source:** [Telco Customer Churn Dataset](https://docs.google.com/spreadsheets/d/1J2aMbLrRnk8g0Y5TSbz-en_7UxlI7xh0cLIZnIy4aew/export?format=csv) (~7,000 customers)

| Feature Type | Columns |
|---|---|
| Demographics | `gender`, `SeniorCitizen`, `Partner`, `Dependents` |
| Account info | `tenure`, `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges`, `TotalCharges` |
| Services | `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies` |
| **Target** | **`Churn`** — `Yes` (1) or `No` (0) |

**Class distribution:** ~73% No Churn · ~27% Churn (mildly imbalanced)

---

## 🏗️ Workflow Architecture

```
┌─────────────────────────────────────────────────────────┐
│                  RAW DATA (Google Sheets URL)            │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│  STEP 1 — Data Loading & Inspection                     │
│  • Load CSV from URL                                     │
│  • Check shape, dtypes, nulls, target distribution      │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│  STEP 2 — Data Cleaning & Preprocessing                 │
│  • Fix TotalCharges (blank → NaN → median fill)         │
│  • Drop customerID (no predictive value)                │
│  • Encode Churn: Yes → 1, No → 0                        │
│  • One-hot encode all categorical features              │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│  STEP 3 — Train-Test Split & Feature Scaling            │
│  • Stratified 80/20 split (random_state=42)             │
│  • StandardScaler fitted on train only (no leakage)     │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│  STEP 4 — Model Training & Evaluation                   │
│  • Logistic Regression (max_iter=1000)                  │
│  • Decision Tree Classifier (max_depth=5)               │
│  • Metrics: Accuracy, Precision, Recall, F1, Conf. Mat. │
│  • Best model selected by F1-Score                      │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│  STEP 5 — Inference on New Unseen Customers             │
│  • Apply identical preprocessing pipeline               │
│  • Output: Churn label + probability score + risk tier  │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│  STEP 6 — Business Insights & Recommendations           │
│  • Contract type analysis                               │
│  • Tenure-based churn patterns                          │
│  • Monthly charges vs. churn relationship               │
└─────────────────────────────────────────────────────────┘
```

---

## 📈 Results & Key Metrics

> Results are representative — exact numbers depend on the live dataset version.

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---|---|---|---|
| Logistic Regression | ~80% | ~65% | ~56% | ~60% |
| Decision Tree (depth=5) | ~79% | ~62% | ~51% | ~56% |

**Selected model:** Logistic Regression (higher F1-Score, better generalization)

**Top predictive features:**
1. `Contract_Two year` / `Contract_One year` (negative — long contracts reduce churn)
2. `tenure` (negative — longer tenure → lower churn risk)
3. `MonthlyCharges` (positive — higher bills → higher churn risk)
4. `InternetService_Fiber optic` (positive — fibre customers churn more)
5. `OnlineSecurity_No` (positive — no security add-on → higher churn risk)

---

## ⚙️ Local Setup & Run Instructions

### Prerequisites
- Python 3.10 or higher
- `pip` package manager

### 1 — Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/customer-churn-prediction.git
cd customer-churn-prediction
```

### 2 — Create and activate a virtual environment
```bash
# Create
python -m venv venv

# Activate (macOS / Linux)
source venv/bin/activate

# Activate (Windows)
venv\Scripts\activate
```

### 3 — Install dependencies
```bash
pip install -r requirements.txt
```

### 4 — Run the Jupyter Notebook
```bash
jupyter notebook notebooks/customer_churn_prediction.ipynb
```

> The dataset is loaded automatically from a public URL — no manual download required.

---

## 📁 Directory Structure

```
customer-churn-prediction/
│
├── notebooks/
│   └── customer_churn_prediction.ipynb   # Interactive step-by-step notebook
│
├── requirements.txt                       # Python dependencies
├── .gitignore                             # Files excluded from version control
├── LICENSE                                # MIT License
└── README.md                              # This file
```

---

## 🚀 Future Improvements

| Area | Improvement |
|---|---|
| Modelling | Add **Random Forest** or **Gradient Boosting** for performance benchmarking |
| Class Imbalance | Implement **SMOTE** or class weighting to improve recall on minority class |
| Deployment | Build a **Streamlit web app** for interactive churn scoring by business teams |
| Explainability | Integrate **SHAP values** for per-prediction, customer-level explanations |
| Automation | Set up a **CI/CD pipeline** with GitHub Actions for automated testing |
| Reproducibility | Containerize the pipeline with **Docker** for consistent environments |

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---


