# 💳 German Credit Data Analysis & Risk Classification

<p align="center">
  Exploratory Data Analysis, Data Visualization, and Machine Learning for Credit Risk Assessment
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/Seaborn-4C72B0?logoColor=white" alt="Seaborn">
  <img src="https://img.shields.io/badge/Plotly-3F4F75?logo=plotly&logoColor=white" alt="Plotly">
  <img src="https://img.shields.io/badge/Scikit--learn-F7931E?logo=scikitlearn&logoColor=white" alt="Scikit-learn">
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white" alt="Jupyter Notebook">
</p>

## 📌 Project Overview

This project explores German credit data to understand customer characteristics, credit borrowing behavior, and the relationship between customer attributes and credit risk.

The analysis combines **Exploratory Data Analysis (EDA)**, statistical summaries, data visualization, feature engineering, and supervised machine learning classification.

Several classification algorithms are trained and evaluated to predict whether a customer's credit risk is classified as **Good** or **Bad**. The project also uses Grid Search Cross-Validation to tune Support Vector Machine (SVM) hyperparameters.

## 🎯 Objectives

- Explore customer demographics and credit-related characteristics.
- Analyze credit amounts and loan purposes across customer groups.
- Investigate relationships between age, gender, employment category, account balances, loan duration, and credit risk.
- Identify and handle missing values.
- Engineer features and encode categorical variables for machine learning.
- Train and compare multiple classification algorithms.
- Evaluate model predictions using accuracy and confusion matrices.
- Tune an SVM classifier using GridSearchCV.

## 📂 Dataset

The project uses the `german_credit_data.csv` dataset.

The dataset contains **1,000 customer records and 10 original columns** describing customer demographics, financial characteristics, loan details, and credit risk.

| Feature | Description |
|---|---|
| `Age` | Customer age |
| `Sex` | Customer gender |
| `Job` | Encoded job category |
| `Housing` | Housing status, such as own, rent, or free |
| `Saving accounts` | Savings account category |
| `Checking account` | Checking account category |
| `Credit amount` | Requested credit amount |
| `Duration` | Credit duration |
| `Purpose` | Purpose of the credit |
| `Risk` | Credit risk label: good or bad |

**Target variable:** `Risk`

- `good`: Good credit risk.
- `bad`: Bad credit risk.

The notebook also creates additional features, including `Age_Group` and `Risk_int`, during the analysis and modeling workflow.

## 🛠️ Technologies & Libraries

| Technology | Purpose |
|---|---|
| Python | Data analysis and machine learning |
| Pandas | Data manipulation and analysis |
| NumPy | Numerical operations and feature engineering |
| Matplotlib | Data visualization |
| Seaborn | Statistical charts and exploratory analysis |
| Plotly | Interactive visualizations |
| Scikit-learn | Classification, model evaluation, and hyperparameter tuning |
| Jupyter Notebook | Interactive analysis and experimentation |

## 🔍 Project Workflow

### 1. Data Loading and Inspection

- Imported the dataset using Pandas.
- Created a copy of the original data.
- Renamed selected columns for easier access in Python.
- Inspected data types, dataset dimensions, and descriptive statistics.
- Reviewed the first records to understand the data structure.

### 2. Data Quality Assessment

Missing values were identified in two columns:

| Feature | Missing Values |
|---|---:|
| `Saving accounts` | 183 |
| `Checking account` | 394 |
| All other original features | 0 |

The notebook visualizes missing values using a Seaborn heatmap and later fills missing savings and checking account categories with `little`.

### 3. Exploratory Data Analysis (EDA)

The notebook explores several dimensions of customer credit behavior.

**Credit Amount Analysis**
- Examines the distribution of credit amounts by gender.
- Compares credit amounts across loan purposes.
- Uses histograms, distribution plots, box plots, and scatter plots.

**Demographic Analysis**
- Examines the distribution of customer ages.
- Compares age distributions across genders.
- Investigates job categories by gender.
- Creates age groups for further analysis.

**Loan Purpose Analysis**
- Examines the distribution of loan purposes across genders.
- Compares credit amounts by loan purpose.
- Investigates the relationship between loan purpose and risk category.

**Credit Risk Analysis**
- Compares good-risk and bad-risk records across age groups.
- Examines checking account categories in relation to risk.
- Uses cross-tabulations to compare risk distributions across loan purposes.
- Explores relationships among credit amount, duration, age, job category, and risk.

### 4. Feature Engineering

The notebook creates an `Age_Group` feature with four categories:

| Age Group | Age Range |
|---|---|
| Young | 19–29 |
| Young Adults | 30–40 |
| Senior | 41–55 |
| Elder | Above 55 |

The target variable is converted into a numerical representation:

- `bad` → `0`
- `good` → `1`

Categorical features are also mapped to numerical values to prepare the dataset for classification.

### 5. Data Preparation

The modeling workflow includes:

- Filling missing values in savings and checking account categories.
- Encoding categorical variables.
- Creating the numerical target variable.
- Separating input features (`X`) from the target (`y`).
- Splitting the dataset into training and testing sets.

The notebook uses an **80% training / 20% testing split** with `random_state=42`.

### 6. Machine Learning Models

The following classification algorithms are implemented:

1. Logistic Regression
2. Support Vector Machine (SVM)
3. Tuned Support Vector Machine using GridSearchCV
4. K-Nearest Neighbors (KNN)
5. Gaussian Naive Bayes
6. Perceptron
7. Linear Support Vector Classification (Linear SVC)
8. Decision Tree
9. Stochastic Gradient Descent (SGD) Classifier
10. Random Forest

Each model is trained on the training set and evaluated on the test set. The notebook also generates confusion matrices to inspect classification errors.

### 7. Hyperparameter Tuning

GridSearchCV is applied to the SVM classifier using the following parameter grid:

- `C`: 0.75, 0.85, 0.95, 1
- `kernel`: linear, polynomial, RBF, sigmoid
- `degree`: 3, 4, 5

The search evaluates **48 parameter combinations using 5-fold cross-validation**.

The best parameters recorded in the notebook are:

```python
{
    "C": 0.95,
    "degree": 5,
    "kernel": "poly"
}
```

The tuned model is subsequently evaluated on the held-out test set.

## 📊 Model Performance

The following results are taken from the notebook's recorded test-set accuracy outputs.

| Rank | Model | Test Accuracy |
|---:|---|---:|
| 1 | Support Vector Machine (SVM) | 71.5% |
| 1 | Tuned SVM using GridSearchCV | 71.5% |
| 3 | Perceptron | 70.5% |
| 3 | Stochastic Gradient Descent (SGD) | 70.5% |
| 3 | Linear SVC | 70.5% |
| 6 | Random Forest | 69.5% |
| 7 | Logistic Regression | 67.5% |
| 8 | Gaussian Naive Bayes | 64.5% |
| 8 | Decision Tree | 64.5% |
| 10 | K-Nearest Neighbors (KNN) | 62.5% |

**Best recorded test accuracy: 71.5%**, achieved by both the default SVM and the tuned SVM.

The hyperparameter search did not improve the recorded test accuracy over the default SVM in this experiment.

> **Evaluation note:** Accuracy alone does not fully describe credit-risk classification performance. Precision, recall, F1-score, ROC-AUC, and class-specific confusion-matrix analysis would provide a more complete evaluation, particularly when misclassifying a bad-risk customer has a different cost from misclassifying a good-risk customer.

## 📈 Key Analysis Areas

The project investigates the following questions:

- How are credit amounts distributed across male and female customers?
- Which purposes account for the largest credit amounts?
- How do loan purposes differ across customer genders?
- How do credit amounts vary across age groups?
- How are good-risk and bad-risk records distributed across age groups?
- How do checking account categories relate to observed credit risk?
- What relationships can be observed between credit amount, loan duration, and risk?
- How do different classification algorithms compare on the same test split?

The notebook provides visualizations and grouped summaries to investigate these questions. Specific business conclusions should be drawn from the relevant charts and numerical results rather than assumed from the questions alone.

## 🚀 Getting Started

### Prerequisites

Install Python 3.9 or later and ensure that the following files are available:

- `german_credit_data.csv`
- The project Jupyter Notebook

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/german-credit-risk-analysis.git
cd german-credit-risk-analysis
```

Replace `YOUR_USERNAME` and the repository name with the actual GitHub details.

### 2. Create a Virtual Environment (Recommended)

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Activate it on macOS or Linux:

```bash
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install numpy pandas matplotlib seaborn plotly scikit-learn jupyter
```

The original notebook also imports `chart_studio`. Install it if you intend to run every original import cell:

```bash
pip install chart-studio
```

### 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open the project notebook and run the cells in sequence. Ensure that `german_credit_data.csv` is located in the expected working directory.

## 📁 Suggested Repository Structure

```text
german-credit-risk-analysis/
│
├── data/
│   └── german_credit_data.csv
│
├── notebooks/
│   └── german_credit_analysis.ipynb
│
├── images/
│   └── Add exported charts here
│
├── requirements.txt
└── README.md
```

This is a recommended repository layout. Adjust the file paths in the notebook if you place the dataset or notebook in different directories.

## 🔧 Potential Improvements

The following are recommendations for future development, not features already completed in the notebook:

- Use a `Pipeline` and `ColumnTransformer` for more consistent preprocessing.
- Apply stratified train-test splitting to preserve the target class distribution.
- Use appropriate categorical encoding rather than relying on arbitrary integer mappings.
- Scale numerical features for distance-based and margin-based algorithms such as KNN, SVM, and Logistic Regression.
- Evaluate models using precision, recall, F1-score, ROC-AUC, and class-specific confusion matrices.
- Compare models using a consistent cross-validation strategy.
- Review missing-value imputation choices and assess their impact on model performance.
- Use class weights or other imbalance-handling techniques if the evaluation indicates a need.
- Examine feature importance and model interpretability.
- Assess potential fairness concerns before using demographic attributes in credit-risk decisions.

## ⚠️ Limitations

- The dataset contains 1,000 records, so findings may not generalize to other populations or lending environments.
- The recorded best test accuracy is 71.5%; performance may vary with different splits, preprocessing choices, and model settings.
- The notebook uses numerical mappings for categorical variables that may introduce artificial ordering.
- Filling missing account categories with `little` assumes that missing values can be treated as the lowest category; this assumption requires validation.
- The current model comparison relies primarily on accuracy and confusion matrices.
- The analysis demonstrates an educational machine learning workflow and should not be treated as a production-ready credit approval system.

## 👩‍💻 Author

**Marwa Samy**

- GitHub: [Marwa Samy](https://github.com/Marwa23-rgb)
