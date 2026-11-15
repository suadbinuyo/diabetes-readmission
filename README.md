# Machine Learning Assignment - Predicting 30 Day Hospital Readmission for Diabetic Patients

## Dataset
- Source: UCI ML Repository — https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008
- Licence: CC BY 4.0
- 101,766 encounters, 47 features
- Citation: Clore, J., Cios, K., DeShazo, J., & Strack, B. (2014). https://doi.org/10.24432/C5230J


## Requirements
- Python version: 3.14.7
- Packages (see requirements.txt)

## Folder Structure
```
diabetes-readmission/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/         # Jupyter notebooks
├── src/            
├── data/              # Dataset (not committed)
└── reports/           # Report and figures
```

## Setup

### 1. Clone the repo
```
git clone <repo_url>
cd diabetes-readmission
```

### 2. Create a virtual environment
```
# Mac / Linux
python3 -m venv venv

# Windows
python -m venv venv
```
### 3. Activate the virtual environment

```
# Mac / Linux
source venv/bin/activate

# Windows (PowerShell)
venv\Scripts\Activate.ps1
```

### 4. Install dependencies
```
pip install -r requirements.txt
```

### 5. Donwload the dataset
1. Go to the UCI ML Repository: https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008
2. Click "Download" (3 MB ZIP)
3. Extract `diabetic_data.csv` and `IDS_mapping.csv`
4. Place both files in the `data/` folder

### 6. Run the notebook

```
jupyter notebook notebooks/01_data_audit_and_baseline.ipynb
```

## Assistance Declaration
See ASSISTANCE.md

## Results (Milestone 3 — Model Comparison)

All models were evaluated using 5-fold `StratifiedGroupKFold` grouped by `patient_nbr`. Metrics are reported as Mean ± Standard Deviation across the folds.

| Model | PR-AUC | ROC-AUC | F1 | Recall | Precision | Balanced Acc |
|---|---|---|---|---|---|---|
| Dummy (most_frequent) | 0.1139 ± 0.0000 | 0.5000 ± 0.0000 | 0.0000 ± 0.0000 | 0.0000 ± 0.0000 | 0.0000 ± 0.0000 | 0.5000 ± 0.0000 |
| Logistic Regression (L2) | 0.2027 ± 0.0062 | 0.6467 ± 0.0022 | 0.2618 ± 0.0024 | 0.5186 ± 0.0061 | 0.1751 ± 0.0016 | 0.6023 ± 0.0028 |
| Logistic Regression (L1, tuned) | 0.2029 ± 0.0061 | 0.6473 ± 0.0023 | 0.2609 ± 0.0015 | 0.5144 ± 0.0055 | 0.1748 ± 0.0008 | 0.6011 ± 0.0018 |
| Random Forest (tuned) | 0.1973 ± 0.0070 | 0.6540 ± 0.0021 | 0.2664 ± 0.0034 | 0.5814 ± 0.0088 | 0.1727 ± 0.0022 | 0.6118 ± 0.0042 |
| **Gradient Boosting (tuned)** | **0.2192 ± 0.0119** | **0.6655 ± 0.0052** | **0.2721 ± 0.0033** | **0.5957 ± 0.0166** | 0.1763 ± 0.0014 | **0.6191 ± 0.0049** |

**Best model:** **Gradient Boosting (tuned)** — PR-AUC: 0.2192. It was chosen because it achieved the highest PR-AUC, ROC-AUC, F1, Recall, and Balanced Accuracy under identical evaluation conditions.

### Tuning & Hyperparameters
Hyperparameters were tuned using `GridSearchCV` scoring on PR-AUC, using the same `StratifiedGroupKFold` splitter.
- **LogReg L1**
- **Random Forest**
- **Gradient Boosting**

### Error Analysis & Fairness (Gradient Boosting)
- **Confusion Matrix (threshold 0.5):** True Negatives = 56,552; False Positives = 31,477; False Negatives = 4574; True Positives = 6740.
- **Precision/Recall Trade-off:** Because `class_weight='balanced'` was applied, the model prioritises catching readmissions (Recall approx 59.6%) at the cost of many false alarms (Precision approx 17.6%).
- **Feature Importance:** The strongest predictors were `number_inpatient` (prior inpatient visits), `discharge_disposition_id`, and `number_emergency`.
- **Subgroup Errors:** The False Negative rate varied by age (highest for ages 31–70 at approx 44%, lowest for <30 at approx 32%). Across race, it ranged from approx 39.9% (Caucasian) to approx 43.1% (Asian), with the "Other" category at 50%.

## Author

Suad Binuyo - 23441964
