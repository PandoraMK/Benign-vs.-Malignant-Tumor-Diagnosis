# Breast Cancer Diagnosis Classifier
A machine learning project that classifies breast cancer tumours as **benign** or **malignant** using clinical cell nucleus measurements from the Wisconsin Breast Cancer Diagnostic dataset. 
Two classification models are built, validated, and compared — Logistic Regression and Random Forest — with full false detection analysis.

---

## Dataset

- **Source:** UCI Machine Learning Repository — Wisconsin Breast Cancer Diagnostic
- **569** total patient records.
- **Target:** `diagnosis` — `M` (malignant) which was encoded as `1` and `B` (benign) encoded as `0`.
- **212** malignant · **357** benign (~37% / ~63%) which is mildly imbalanced but not enough to bias the models.

---

## ⚙️ Methodology

### 1. Exploratory data analysis
- Pairplots generated across all 10 mean features to visualise class separation, with a focused subset on `radius_mean`, `texture_mean`, and `perimeter_mean`
- Correlation heatmap computed for all mean features — `radius_mean`, `perimeter_mean`, and `area_mean` found to be highly correlated and excluded from modelling

### 2. Feature selection
Features with pairwise correlation above **0.80** were flagged for removal. VIF (Variance Inflation Factor) scores confirmed low multicollinearity among the retained features:
texture_mean, smoothness_mean, compactness_mean, symmetry_mean, fractal_dimension_mean
