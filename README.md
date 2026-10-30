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

## Author

Suad Binuyo - 23441964
