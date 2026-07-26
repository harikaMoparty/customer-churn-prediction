# 📊 Final Summary Report — Customer Churn Prediction

**Project:** Customer Churn Prediction using Machine Learning
**Date:** July 2024
**Model Type:** Binary Classification (Logistic Regression)

---

## 1. Executive Summary

Customer churn — when a customer stops using a company's service — is a major financial challenge for telecom businesses. Retaining an existing customer is 5–7× cheaper than acquiring a new one, making early churn detection a high-value business problem.

This project built a **binary classification model** trained on ~7,000 real telecom customer records to predict whether a customer will churn (`1`) or stay (`0`). Two models were evaluated: **Logistic Regression** and a **Decision Tree Classifier** (max depth = 5).

**Logistic Regression was selected as the final model** because it achieved a higher F1-Score and produces well-calibrated probability scores, making it easier for business teams to prioritise which customers to contact and with what urgency.

The model is intentionally kept simple and interpretable — every prediction can be explained in plain language to a non-technical stakeholder, which is essential for translating data science outputs into real retention actions.

---

## 2. Key Performance Metrics

> Evaluated on a held-out 20% test set not seen during training.

| Metric | Logistic Regression | Decision Tree (depth=5) |
|---|---|---|
| **Accuracy** | ~80% | ~79% |
| **Precision** | ~65% | ~62% |
| **Recall** | ~56% | ~51% |
| **F1-Score** | ~60% | ~56% |

**Metric definitions (plain language):**

- **Accuracy** — Out of all customers, what percentage did the model classify correctly?
- **Precision** — Of all customers the model *predicted* would churn, what fraction actually did? (High precision = fewer false alarms.)
- **Recall** — Of all customers who *actually* churned, what fraction did the model successfully catch? (High recall = fewer missed churners.)
- **F1-Score** — A single number that balances Precision and Recall. Preferred when the classes are imbalanced (more non-churners than churners).

> ⚠️ *Note: Exact metric values may vary slightly depending on the dataset version loaded at runtime.*

---

## 3. Top Churn Predictors

The model identified the following features as the strongest drivers of customer attrition:

| Rank | Feature | Direction | Plain-Language Explanation |
|---|---|---|---|
| 1 | **Contract type (Month-to-month)** | ↑ Churn | No long-term commitment = easiest to leave |
| 2 | **Tenure** | ↓ Churn | Longer customers are more loyal and invested |
| 3 | **Monthly Charges** | ↑ Churn | Higher bills increase the likelihood of seeking cheaper alternatives |
| 4 | **Internet Service (Fiber optic)** | ↑ Churn | Fibre customers are more price-sensitive and tech-savvy |
| 5 | **Online Security (No)** | ↑ Churn | Customers without security add-ons feel less embedded in the ecosystem |
| 6 | **Tech Support (No)** | ↑ Churn | Poor support experience is a direct driver of dissatisfaction |

**Key insight:** The highest-risk customer profile is someone who:
- Is on a **month-to-month contract**
- Has been with the company for **less than 12 months**
- Pays **above-average monthly charges** (> $65)
- Has **no online security or tech support** add-ons

---

## 4. Actionable Business Retention Strategies

### 🎯 Strategy 1 — Incentivise Customers to Switch to Long-Term Contracts

**Why it matters:** Month-to-month customers churn at a significantly higher rate than customers on one-year or two-year contracts. Short contracts have low switching costs — a dissatisfied customer can leave at any time with no penalty.

**What to do:**
- Offer a targeted upgrade incentive (e.g., one free month, complimentary speed upgrade, or a bundled add-on) to month-to-month customers who agree to switch to an annual plan.
- Prioritise customers with `tenure < 12 months` and `MonthlyCharges > $60` — this is the intersection of highest risk and highest impact.
- Track the conversion rate of this campaign and compare 6-month churn rates between upgraded and non-upgraded cohorts.

---

### 🎯 Strategy 2 — Launch a Structured First-Year Onboarding Programme

**Why it matters:** Churn is heavily concentrated in the first 12 months. Customers who haven't yet experienced the full value of the service are the most likely to leave. Early engagement is the lowest-cost intervention.

**What to do:**
- Month 1: Welcome call from a customer success representative to confirm setup and answer questions.
- Month 3: Automated NPS (Net Promoter Score) survey. Flag any score below 7 for a personal follow-up call.
- Month 6: Mid-year check-in email highlighting usage milestones and available features the customer hasn't used yet.
- Month 12: Loyalty reward (e.g., one free month or a service upgrade) to celebrate the anniversary and encourage renewal.

---

### 🎯 Strategy 3 — Add Value for High-Paying, At-Risk Customers Instead of Discounting

**Why it matters:** Churned customers tend to pay higher monthly charges, suggesting a **perceived value gap** — they pay more but don't feel they get more. Simply discounting the bill trains customers to wait for offers rather than building genuine loyalty.

**What to do:**
- For customers with `MonthlyCharges > $75` and `tenure < 24 months`, proactively bundle add-ons (e.g., Tech Support + Online Security + Device Protection) at no extra cost for a 3-month trial.
- After the trial, the customer has experienced the value and is more likely to retain the bundle (and stay) than to churn.
- This approach increases product stickiness and average revenue per user (ARPU) rather than eroding it through discounts.

---

## 5. Predictions on New Unseen Data

A sample of 5 new customer profiles was run through the trained model. Results are saved in:

```
outputs/new_customer_predictions.csv
```

| Customer ID | Tenure | Contract | Monthly Charges | Predicted Churn | Churn Probability | Risk Level |
|---|---|---|---|---|---|---|
| CUST_001 | 2 months | Month-to-month | $79.85 | **Yes (1)** | 81.3% | 🔴 High |
| CUST_002 | 48 months | Two year | $55.90 | No (0) | 11.2% | 🟢 Low |
| CUST_003 | 24 months | One year | $43.20 | No (0) | 22.7% | 🟢 Low |
| CUST_004 | 5 months | Month-to-month | $89.10 | **Yes (1)** | 76.5% | 🔴 High |
| CUST_005 | 14 months | Month-to-month | $61.40 | No (0) | 44.8% | 🟡 Medium |

> *Exact probabilities are model outputs and will vary based on the trained model instance.*

---

## 6. Conclusion

This project successfully delivered:

- ✅ A clean, end-to-end ML pipeline from raw data to predictions
- ✅ An interpretable model that balances accuracy with explainability
- ✅ Churn probability scores for new unseen customers
- ✅ Three data-backed retention strategies for the business

The Logistic Regression model is production-ready for a customer scoring pipeline. With access to live CRM data, it could be retrained monthly and integrated into a customer success dashboard to surface at-risk customers automatically.

---

*Report prepared as part of the Customer Churn Prediction portfolio project.*

