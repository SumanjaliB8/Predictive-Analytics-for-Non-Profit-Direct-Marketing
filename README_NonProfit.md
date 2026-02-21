# 🤝 Non-Profit Direct Marketing Optimization — Group 15

> Building classification and regression models to help a non-profit organization improve the cost-effectiveness of its direct mail donation campaigns.

**Course:** ADTA 5230 — Final Project | **Date:** May 5, 2025

---

## 👥 Team — Group 15

| Name |
|------|
| Sathvik Chava |
| Sumanjali Banjara |
| Paulina Gomez Ibarra |

---

## 📌 Project Overview

A non-profit organization approached us with a cost-effectiveness problem in their direct mail campaigns. Their current mass marketing approach results in a **loss of -$0.55 per mailing** due to a low response rate (~10%) and modest average donation ($14.50), against a mailing cost of $2.00 per person.

We were tasked with building two models to solve this:

| Question | Model Type |
|----------|-----------|
| Who is most likely to donate? | **Classification** (target: `donr`) |
| How much will each donor likely give? | **Regression/Prediction** (target: `damt`) |

---

## 📊 Dataset

| Property | Value |
|----------|-------|
| **Records** | 6,002 individuals |
| **Missing Values** | None |
| **Tool Used** | SAS Enterprise Miner |
| **Train / Validation Split** | 70% / 30% |

**Key Target Variables:**

| Variable | Type | Description |
|----------|------|-------------|
| `donr` | Binary | 1 = Donor, 0 = Non-donor (balanced: ~50/50) |
| `damt` | Continuous | Dollar amount donated (avg $14.45, range $8–$27) |

**Key Predictors:** `inc`, `region`, `ownd`, `wlth`, `kids`, `incavg`, `incmed`, `hv`, `gifdol`, `gifl`, `gifr`, `gifa`

---

## 🔬 Project Pipeline

| Step | Stage | Details |
|------|-------|---------|
| 1 | **EDA** | DMDB, StatExplore, Graph Explore, Variable Clustering, Multiplot nodes in SAS |
| 2 | **Data Preparation** | No imputation needed; categorical encoding; standardization via Transform node |
| 3 | **Train/Validation Split** | 70/30 split to balance learning and generalization |
| 4 | **Classification Modeling** | Logistic Regression, Neural Networks, Gradient Boosting |
| 5 | **Prediction Modeling** | HP Forest, Neural Network, Auto Neural |
| 6 | **Model Evaluation** | Misclassification rate, ASE, profitability analysis |
| 7 | **Deployment** | Score data applied to best models; targeted vs. mass marketing comparison |

---

## 🧠 Models Implemented

### Classification Models (Predict: `donr`)

| Model | Configuration |
|-------|--------------|
| Logistic Regression | Default settings |
| Logistic Regression | Stepwise selection |
| Neural Network | Default settings |
| Neural Network | Back propagation, 3 hidden units |
| Neural Network | Back propagation, 6 hidden units |
| Gradient Boosting | Default settings |

### Prediction Models (Predict: `damt`)

| Model | Configuration |
|-------|--------------|
| HP Forest | Default settings |
| Neural Network | Default settings |
| Neural Network | 6 hidden units |
| Auto Neural | 2 hidden units |
| Auto Neural | 6 hidden units |

---

## 📈 Results

### Classification — Ranked by Misclassification Rate

| Model | Validation Misclassification Rate |
|-------|----------------------------------|
| **Neural Network (default)** | **0.0921** 🏆 |
| Stepwise Regression | 0.1049 |
| Regression | 0.1054 |
| Gradient Boosting | 0.1088 |
| Neural Net BP (3 hidden units) | 0.1304 |
| Neural Net BP (6 hidden units) | 0.1315 |

### Classification — Ranked by Profitability

> Formula: Net Profit = (True Positives × $14.50) − ((True Positives + False Positives) × $2.00)

| Model | True Positives | False Positives | Profit |
|-------|---------------|-----------------|--------|
| **Neural Network (default)** | 830 | 97 | **$10,181.00** 🏆 |
| Stepwise Regression | 815 | 105 | $9,977.50 |
| Regression | 815 | 106 | $9,975.50 |
| Gradient Boosting | 805 | 102 | $9,858.50 |
| Neural Net BP (hu=3) | 795 | 131 | $9,675.50 |
| Neural Net BP (hu=6) | 794 | 132 | $9,661.00 |

### Prediction — Ranked by Validation ASE

| Model | Validation ASE |
|-------|---------------|
| **AutoNeural (6 hidden units)** | **16.91** 🏆 |
| Neural Network (default) | 17.90 |
| AutoNeural (2 hidden units) | 20.47 |
| Neural Net BP (6 hidden units) | 20.51 |
| HP Forest | 20.65 |

---

## 💡 Key Insights

- **Neural Network (default)** was the best classification model — lowest misclassification rate (0.0921) and highest profit ($10,181)
- **AutoNeural with 6 hidden units** was the best prediction model — lowest ASE (16.91) with minimal train-validation gap
- **Negative correlation** between `kids` and `damt` (r = -0.55) — households with more children donate less
- `inc`, `region`, `ownd`, and `wlth` had the strongest relationships with donor likelihood (Chi-Square p < 0.0001)
- Increasing neural network complexity (more hidden units) did not improve performance — simpler models generalized better

---

## 💰 Deployment & Profit Impact

Score data was applied to the best models to generate:
- `p_donr1` — probability an individual will donate (Classification)
- `p_damt` — predicted donation amount (Prediction)

**Expected Profit Formula:** `(p_donr1 × p_damt) − $2.00`

| Strategy | Individuals Targeted | Total Expected Profit | Avg Profit/Person |
|----------|---------------------|-----------------------|-------------------|
| **Mass Marketing** | 2,007 | $401.39 | $0.20 |
| **Targeted Marketing** | 508 | **$3,129.60** | **$6.16** |

> Targeted marketing generates approximately **8x more profit** than mass marketing by focusing only on individuals with a positive expected profit.

---

## 🌍 Real-World Impact

| Domain | Application |
|--------|-------------|
| **Cost Reduction** | Eliminate wasteful mailings to non-likely donors |
| **Revenue Maximization** | Focus budget on high-probability, high-value donors |
| **Campaign Strategy** | Shift from mass marketing to data-driven targeted outreach |
| **Donor Insights** | Understand demographic and behavioral drivers of giving |

---

*Made with ❤️ by Group 15 · ADTA 5230 · May 2025*
