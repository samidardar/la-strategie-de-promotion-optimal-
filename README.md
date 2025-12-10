# la-strategie-de-promotion-optimal- 
# 🛒 Causal Inference for Retail: Maximizing Promotion Profitability

![Python](https://img.shields.io/badge/Python-3.9-blue) ![CausalML](https://img.shields.io/badge/Library-CausalML-orange) ![XGBoost](https://img.shields.io/badge/Model-XGBoost-green) ![Status](https://img.shields.io/badge/Status-Enterprise%20Grade-gold)

## 📉 Executive Summary
This project answers a critical business question: **"Which stores should actually receive a promotion to maximize net profit?"**

Using **Causal Inference (Uplift Modeling)** on the [Rossmann Store Sales dataset](https://www.kaggle.com/c/rossmann-store-sales), I built a meta-learner system to estimate the **Individual Treatment Effect (ITE)** of promotions.

**Key Finding:** 46.5% of promotions were destroying value (generating less sales lift than their operational cost). By optimizing the targeting policy, the model is projected to increase net profit by **+€214M** compared to a blanket promotion strategy.

## 💼 The Business Problem
Retailers often apply "blanket promotions" (running sales across all stores). This is inefficient for two reasons:
1.  **The "Sure Things":** Stores that have high organic demand and would sell well without a discount (cannibalization).
2.  **The "Lost Causes":** Stores where the increase in sales is too small to cover the cost of running the promotion.

**Objective:** Shift from predicting *Sales* to predicting *Lift* (Incremental Sales) to optimize ROI.

## 🛠️ Technical Solution
I implemented a **Causal Meta-Learner** framework to solve the counterfactual problem (*"What would have happened if we didn't run the promo?"*).

### 1. Methodology
* **S-Learner (Baseline):** Trained a Single Learner (Random Forest) treating `Promo` as a feature.
    * *Result:* Failed to discriminate between store segments (Flat Uplift Curve). It learned the average effect but missed heterogeneity.
* **T-Learner (Champion):** Trained "Two Learners" (XGBoost) separately for Treatment and Control groups.
    * *Result:* Successfully captured variance in store sensitivity, creating a high-resolution ranking of opportunities.

### 2. Financial Optimization (Stress Testing)
I performed a sensitivity analysis simulating different promotional costs (€500 - €2000) to find the "Breaking Point" where the strategy shifts.

## 📊 Key Results
The T-Learner successfully segmented the store network into three tiers:

| Segment | Store Count | Avg Lift (€) | Recommendation |
| :--- | :--- | :--- | :--- |
| **Tier 1 (High Uplift)** | Top 25% | **+€2,375** | **✅ Aggressive Push:** High ROI targets. |
| **Tier 2 (Mid Uplift)** | Mid 28% | **+€1,175** | **⚠️ Test & Learn:** Promote during seasonal peaks. |
| **Tier 3 (Negative ROI)** | Bottom 47% | **+€400** | **❌ STOP:** Lift is < Cost (€1,100). |

### 📈 Impact Analysis
* **Baseline Strategy (Target Everyone):** €180M Net Profit
* **Causal AI Strategy (Target Top 53%):** €394M Net Profit
* **Net Business Value:** 🚀 **+€214M**

![Profit Curve](path_to_your_hill_chart_image.png)
*(The "Hill" demonstrates the optimal cutoff point where profit is maximized before diminishing returns set in)*

## 🚀 Technologies Used
* **CausalML / EconML**: Meta-learner implementation.
* **XGBoost**: Gradient boosting for treatment/control estimators.
* **Scikit-Learn**: Data preprocessing and pipelines.
* **Matplotlib/Seaborn**: Uplift curves and profit visualization.

## 📂 Dataset
[Rossmann Store Sales (Kaggle)](https://www.kaggle.com/c/rossmann-store-sales/data)
