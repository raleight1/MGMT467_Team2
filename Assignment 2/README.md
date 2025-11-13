Overview

This project develops and evaluates several machine learning models to predict flight diversions and inform operational pre-staging decisions (e.g., crew, gates, hotel blocks).
The final deliverable — Flights_Team_Ops_Brief_Final.pdf — summarizes performance progression from baseline through feature-engineered, oversampled, segmented, and cost-optimized models, culminating in an actionable operational policy.

🚀 How to Run
1. Environment Setup

Requires Google Cloud Platform (GCP) with BigQuery ML (BQML) enabled.

Python notebooks use the BigQuery Python API within a Colab or Vertex AI Workbench environment.

pip install google-cloud-bigquery pandas numpy matplotlib
gcloud auth application-default login

2. Execution Steps

Open each notebook (Unit2_Tyler_BQML.ipynb, Unit2_Ryan_BQML.ipynb, Unit2_Rileigh_BQML_ModelC.ipynb).

Update the PROJECT_ID variable with your GCP project.

Ensure access to the dataset in BigQuery (see below).

Run cells in order:

Model A: Baseline (schedule-only features)

Model B: Feature engineering (operational features)

Model B2: Oversampling to handle class imbalance

Model C: Segmentation by hub

Model D: Cost-based threshold optimization

Collect metrics (AUC, log_loss, confusion matrix) from notebook outputs.

Review the final Flights_Team_Ops_Brief_Final.pdf for summarized findings and recommendations.

📊 Dataset Choice

Source: Kaggle — U.S. Carrier On-Time Performance Dataset

Scope: U.S. domestic flight records containing on-time, delay, and diversion information.
Features used:

Schedule features: origin, dest, sched_dep_time, sched_arr_time

Operational features: dep_delay_raw, dep_delay_bucket, hour_of_day

Derived features: categorical encodings, temporal bins, and imbalance-adjusted sampling.

Target: Binary classification — is_diverted (1 = diverted, 0 = not diverted).

⚙️ Assumptions

Cost Matrix:

False Positive (FP) = $1 (unnecessary pre-staging)

False Negative (FN) = $10 (missed diversion and disruption costs)
These were used to compute expected costs and select the optimal decision threshold.

Imbalance Handling:
The diversion class (<0.1% prevalence) required oversampling to improve recall.
Models B2 and D address this explicitly.

Segmentation:
Segmenting by hub airport captures localized operational behaviors, improving detection of rare events.

Threshold Selection:
Threshold = 1.00 minimizes total cost given the above cost matrix (Model D).
Threshold = 0.35 balances recall and precision in operational deployment (Model B2).

📈 Outputs

Flights_Team_Ops_Brief_Final.pdf — summarized decision brief for operations leadership.

Extracted notebooks with experiment logs (Unit2_Tyler_BQML, Unit2_Ryan_BQML, Unit2_Rileigh_BQML_ModelC).

🧭 Next Steps

Incorporate cost-sensitive learning directly into model training (e.g., weighted logistic regression).

Deploy monitoring pipelines in Vertex AI Model Monitoring or Cloud Functions for calibration drift and precision parity.

Periodically update cost parameters and thresholds as operational costs evolve.
