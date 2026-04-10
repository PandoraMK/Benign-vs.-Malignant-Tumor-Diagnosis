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

## Methodology

### 1. Exploratory data analysis
- Pairplots generated across all 10 mean features to visualise class separation, with a focused subset on `radius_mean`, `texture_mean`, and `perimeter_mean`
- Correlation heatmap computed for all mean features — `radius_mean`, `perimeter_mean`, and `area_mean` found to be highly correlated and excluded from modelling

### 2. Feature selection
Features with pairwise correlation above **0.80** were flagged for removal. VIF (Variance Inflation Factor) scores confirmed low multicollinearity among the retained features:
texture_mean, smoothness_mean, compactness_mean, symmetry_mean and fractal_dimension_mean.

### 3. Train / test split
- **70% training · 30% test** (`random_state=42`)
- Features standardised with `StandardScaler` before Logistic Regression; Random Forest was trained on unscaled data

---

## Models

### Logistic Regression
- Trained with `LogisticRegression(max_iter=1000)` on scaled features
- Model coefficients plotted as a horizontal bar chart to show feature importance

### Random Forest
- Trained with `RandomForestClassifier(n_estimators=100, random_state=42)` on unscaled features
- Gini impurity scores used to rank and visualise feature importance

---

##  Results

### Logistic Regression
| | Value |
|---|---|
| Correctly classified benign | 103 |
| Correctly classified malignant | 59 |
| False positives (benign → malignant) | 4 |
| False negatives (malignant → benign) | 5 |

### Random Forest
| | Value |
|---|---|
| Correctly classified benign | 105 |
| Correctly classified malignant | 57 |
| False positives (benign → malignant) | 6 |
| False negatives (malignant → benign) | 3 |

Both models achieve comparable overall accuracy. Random Forest produces fewer false negatives (missed malignancies), which is the more critical error in a clinical screening context.

---

## False detection analysis

For both models, false positives and false negatives are extracted from the test set and printed with their feature values, actual label, and predicted label. False positive patients — those who are benign but flagged as malignant — are surfaced at the end for prioritised follow-up medical testing.

---

## Requirements
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- statsmodels

