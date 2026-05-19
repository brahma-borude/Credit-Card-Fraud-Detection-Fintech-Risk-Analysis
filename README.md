## 💳 Credit Card Fraud Detection — Fintech Risk Analysis

> **Business Question:** What transaction patterns signal potential fraud,  
> and how accurately can we detect them before financial loss occurs?

---

### 🎯 Business Context

Credit card fraud costs the global financial industry $33 billion annually.  
For a fintech like Razorpay processing millions of daily transactions,  
even a 0.01% undetected fraud rate translates to significant losses.

This project simulates the work of a **Risk Analytics team** — identifying  
fraud patterns, building a detection model, and delivering actionable  
recommendations to the fraud operations team.

---

### 📊 Dataset

- **Source:** [Kaggle Credit Card Fraud Detection](https://kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Size:** 284,807 transactions | 492 fraud cases (0.17%)
- **Features:** Time, Amount, V1–V28 (PCA-transformed for privacy), Class
- **Period:** Two days of European cardholder transactions

---

### 🔍 Key Findings

| Finding | Detail |
|---|---|
| Fraud rate | 0.17% of all transactions |
| Peak fraud window | 2AM – 4AM (3× average rate) |
| Fraud amount pattern | Median €9.25 — small test transactions |
| Top detection signals | V14, V4, V11 |
| Model recall | ~90% on held-out test set |
| False positive rate | <2% |

---

### ⚙️ Technical Approach

#### 1. EDA
- Amount distribution by class
- Time-of-day fraud rate analysis  
- Feature separation power (|mean_fraud - mean_legit|)
- Correlation heatmap within fraud subset

#### 2. Handling Class Imbalance
- Applied **SMOTE** on training set only (after train/test split)
- Compared with class_weight='balanced' as baseline
- Evaluated using **Recall + F1** on fraud class — NOT accuracy

#### 3. Models
| Model | Recall | Precision | F1 | AUC |
|---|---|---|---|---|
| Logistic Regression (baseline) | 0.90 | 0.06 | 0.12 | 0.96 |
| XGBoost | **0.86** | **0.50** | **0.63** | **0.97** |

#### 4. Threshold Tuning
Optimised decision threshold to **0.85** (default 0.5) to maximise F1  
while maintaining operationally acceptable false positive rate.

---

### 💡 Recommendations

1. Deploy model at threshold **0.85** for real-time transaction scoring
2. Implement enhanced review queue for transactions between **2AM–4AM**
3. Flag accounts with **2+ transactions < €20 within 30 minutes**
4. Schedule quarterly retraining on confirmed fraud labels

---

### 🗂️ Project Structure

```
fraud_detection/
├── notebooks/fraud_analysis.ipynb
├── outputs/
│   ├── charts/          # All EDA and model charts
└── README.md
```

---

### 🛠️ Stack

Python · Pandas · Scikit-learn · XGBoost · imbalanced-learn · Seaborn · Matplotlib

---

### 👤 About

Built as part of a fintech data analyst portfolio targeting risk analytics  
roles at companies like Razorpay, Paytm, PhonePe, and HDFC Bank.
