# Patient Readmission Risk Prediction with Interpretable ML

Predicting 30-day hospital readmission risk for diabetic patients, with a focus on model interpretability (SHAP) rather than raw predictive accuracy alone.

# Motivation
Predicting readmission risk is only half the problem, if a doctor can't see why the model flagged a patient, they're not going to trust it enough to act on it. So alongside the prediction itself, this project uses SHAP to show which factors pushed a given patient's risk up or down, in a way that's actually checkable against clinical judgement.

# Dataset
Diabetes 130-US Hospitals dataset (UCI Machine Learning Repository) - 101,766 inpatient encounters across 130 US hospitals and integrated delivery networks (1999–2008). Each row represents an encounter meeting three inclusion criteria: a diabetes diagnosis, a length of stay between 1 and 14 days, and at least one lab test and one medication administered during the stay. 47 features cover demographics, admission/discharge details, diagnoses, medications, and prior healthcare utilization.

Target: whether the patient was readmitted within 30 days of discharge.

# Approach

- Baseline: logistic regression (interpretable by design, sets a floor).
- Main model: gradient boosting (XGBoost/LightGBM), tuned with cross-validation, class weighting to handle imbalance.
- Interpretability: SHAP summary + dependence plots at the population level, force plots for individual predictions.
- Evaluation: beyond AUC — precision/recall trade-offs, calibration curves and a discussion of what threshold makes sense clinically (a screening tool trades off differently than a diagnostic one).
- App: a Streamlit interface where you enter patient features and get a risk score plus a SHAP explanation for that specific prediction.

# Results

# Limitations

- Historical data (1999–2008) from US hospitals - coding practices and care pathways have changed; results may not generalize to current populations.
- Readmission is a noisy proxy for care quality - many readmissions aren't preventable.
- No external validation cohort; performance is optimistic relative to deployment on a genuinely unseen hospital system.
- Model is for portfolio/demonstration purposes only - not validated for clinical use.
