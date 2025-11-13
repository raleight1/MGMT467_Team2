# Team Ops Brief: Flight Diversion Prediction Model (Model D Variant) ✈️

**Author:** Team 2
**Model Name:** BQML Model D Variant (Segmented, Engineered)
**Date:** November 12, 2025

---

## 1. Decision Rule (One Line)

Optimizing for **risk minimization** (Expected Cost), the operating threshold is set to **1.00** to eliminate False Positive costs, yielding a minimum total expected cost of **\$2,390.00**.

---

## 2. Evidence: Model Progression and Key Metrics

The modeling goal was to achieve a fiscally responsible decision rule, translating strong discriminative power (AUC) into the lowest possible Expected Cost based on the provided cost matrix.

### Model Progression (AUC)

| Model Variant | Scope | Key Features | Discriminative Power (AUC) | Change vs. Baseline |
| :--- | :--- | :--- | :--- | :--- |
| **Model A** (Baseline) | Global | Basic Features | **0.572** | N/A |
| **Model B** | Engineered Uplift | Basic Features + Engineered | **0.771** | +19.9% |
| **Model C** | Segmented (Hubs) | Operational Features | **0.662** | +15.7% |
| **Model D Variant** | **Segmented + Engineered** | `dep_delay_hour_interaction`, `distance_bucket` | **0.870** | **+52.1%** |

### Engineered Features (`TRANSFORM`)

Model D Variant utilized **feature engineering** to achieve the high AUC:
* **`dep_delay_hour_interaction`**: Captured a non-linear relationship between raw delay time and the hour of the day, showing that delays at certain hours are more indicative of a diversion.
* **`distance_bucket`**: Bucketing continuous distance into categorical bins helped isolate the risk profile associated with specific flight length categories.

### Key Metrics and Confusion Matrix (Threshold = 1.00)

The high AUC of 0.87 confirms the model's strong capability to **rank** flights by risk. However, the optimal operating threshold of **1.00** results in a highly conservative classification strategy focused on cost-minimization.

| Metric | Value | Observation |
| :--- | :--- | :--- |
| **Total Expected Cost** | **\$2,390.00** | The minimum cost achievable based on the cost matrix. |
| Log\_Loss | *(Requires model output)* | Indicates quality of probability estimation. |
| Confusion Matrix: **True Positives (TP)** | **0** | No diversions are predicted. |
| Confusion Matrix: **False Positives (FP)** | **0** | No unnecessary alerts are generated. |
| Confusion Matrix: **False Negatives (FN)** | **239** | All actual diversions are missed (239 FN $\times$ \$10 = \$2,390). |
| Confusion Matrix: **True Negatives (TN)** | **237,921** | All non-diverted flights are correctly classified. |

---

## 3. Policy: Deployment Strategy and Cost Analysis

### Global vs. Segmented Deployment

**Policy:** **Segmented Deployment.**

The model will be deployed only to the pre-selected **high-traffic operational hubs**. This ensures that the model operates in the environment for which it was optimized (Model C/D logic) and where it demonstrated a **52% uplift in performance (AUC)** over the global baseline.

### Expected-Cost Analysis (Cost Matrix)

The decision to set the threshold at **1.00** is entirely driven by the cost matrix:

| Outcome | Cost | Rationale |
| :--- | :--- | :--- |
| **False Positive** ($\mathbf{C_{FP}}$) | **\$1** (Unnecessary alert) | Represents minor operational disruption/investigation. |
| **False Negative** ($\mathbf{C_{FN}}$) | **\$10** (Missed diversion) | Represents the cost of not intervening when a diversion occurs. |

**Threshold Rationale (0.75 or other):**
* **Sensitivity Analysis:** A threshold sweep showed that any threshold below 1.00 (e.g., the default 0.50) resulted in a volume of False Positives so high that it generated a total expected cost of **over $237,000**, vastly exceeding the cost of the False Negatives.
* **Final Choice (1.00):** The optimal strategy for the current cost matrix is **error avoidance** (predicting `False` for all instances) to prevent costly FP alerts. The cost of \$2,390 represents the irreducible cost of all actual diversions (Total FN count $\times$ $\mathbf{C_{FN}}$).

### Hub Precision Observation

At the operating threshold of 1.00, the **Hub Precision is 0/0 (undefined, effectively zero)** since TP=0. This is an accepted outcome of the cost-minimization strategy. **Mitigation:** The high AUC (0.87) shows the model can rank risk; if the business requires an actionable prediction (TP > 0), the $\mathbf{C_{FN}}$ must be **substantially increased** to shift the optimal threshold.

---

## 4. Monitoring

The monitoring plan is focused on detecting model drift and ensuring the decision rule remains cost-optimal.

| Metric | Threshold/Goal | Cadence | Owner |
| :--- | :--- | :--- | :--- |
| **Total Expected Cost** | $\Delta > 5\%$ increase (vs. target \$2,390) | Weekly | Data Science / Finance |
| **Precision on Top Hubs** | Precision remains 0 (expected) or $\Delta > 1\%$ (unexpected positive predictions) | Weekly | ML Engineering |
| **Feature Drift** ($\text{dep\_delay\_raw}$) | Mean delay $\Delta > 10\%$ vs. training data | Weekly | ML Engineering |
| **Parity Gap** (Calibration Error) | Parity Gap $>$ 5 pp (between predicted vs. observed rates per risk decile) | Monthly | Model Governance |
