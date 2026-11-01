<h1 align="center">🚢 Titanic Survival Prediction</h1>

<p align="center">
  Exploratory data analysis and machine learning on the Kaggle Titanic dataset using Python
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C8CBF" alt="Seaborn">
  <img src="https://img.shields.io/badge/scikit--learn-Modeling-F7931E?logo=scikitlearn&logoColor=white" alt="scikit-learn">
  <a href="https://www.kaggle.com/c/titanic"><img src="https://img.shields.io/badge/Dataset-Kaggle-20BEFF?logo=kaggle&logoColor=white" alt="Kaggle"></a>
</p>

## 📌 Overview

This project explores the **Titanic: Machine Learning from Disaster** dataset from Kaggle. It inspects and cleans the passenger data, engineers new features, visualizes which passengers were more likely to survive, and compares ten classification models that predict the `Survived` column.

> The data is split into `train.csv` (891 passengers, with the `Survived` label) and `test.csv` (418 passengers, without it). Both are expected in a `data/` folder.

---

## ⚡ At a Glance

| 🧍 Train Rows | 🧍 Test Rows | 📊 Columns (raw) | 💀 Survival Rate | 🎂 Avg. Age |
|:---:|:---:|:---:|:---:|:---:|
| **891** | **418** | **12** | **≈ 38.4%** | **≈ 29.7 years** |

---

## 🔄 Workflow

1. **Load & Inspect** – Checked column names, data types, missing values and summary statistics (`info()`, `describe()`, `describe(include=['O'])`).
2. **Explore** – Grouped survival rate by `Pclass`, `Sex`, `SibSp` and `Parch`, and plotted age, fare and port of embarkation against survival with Seaborn.
3. **Clean the Data** – Dropped `Ticket`, `Cabin`, `Name` and `PassengerId`, filled missing `Age`, `Embarked` and `Fare` values, and encoded text columns as numbers.
4. **Feature Engineering** – Created `Title`, `IsAlone` and `Age*Class`, and grouped `Age` and `Fare` into bands.
5. **Model** – Trained ten classifiers on the final 8 features and compared their scores.

> **Final features:** `Pclass` · `Sex` · `Age` · `Fare` · `Embarked` · `Title` · `IsAlone` · `Age*Class`

---

## 🧹 Data Cleaning

| Step | Action |
|---|---|
| **Dropped columns** | `Ticket` and `Cabin` (too many unique or missing values), `Name` (after extracting the title) and `PassengerId` (train only) |
| **Missing `Age`** | 177 values filled with the median age of passengers who share the same `Sex` and `Pclass` |
| **Missing `Embarked`** | 2 values filled with the most common port (`S`) |
| **Missing `Fare`** | 1 test value filled with the median fare |
| **Encoding** | `Sex` → 0/1, `Embarked` → S=0, C=1, Q=2, `Title` → 1–5 |

---

## 🛠️ Feature Engineering

| Feature | How it was built |
|---|---|
| **Title** | Extracted from `Name` (Mr, Miss, Mrs, Master). Uncommon titles were grouped into `Rare`, and Mlle/Ms/Mme were merged into Miss/Mrs |
| **Age bands** | `Age` grouped into 5 equal-width bins; the first four are coded 0–3 |
| **Fare bands** | `Fare` split into 4 quartile bands coded 0–3 |
| **FamilySize → IsAlone** | `SibSp + Parch + 1`, then reduced to a 1/0 flag for travelling alone. `SibSp`, `Parch` and `FamilySize` were dropped afterwards |
| **Age\*Class** | `Age` band multiplied by `Pclass` |

---

## 🔍 Key Findings

| Question | Result |
|---|---|
| Sex | **Women survived at 74.2%** versus **18.9% for men** |
| Passenger class | Survival fell with class: **63.0%** (1st) · **47.3%** (2nd) · **24.2%** (3rd) |
| Title | Mrs **79.4%** · Miss **70.3%** · Master **57.5%** · Rare **34.8%** · Mr **15.7%** |
| Age | Passengers aged 16 or under survived at **55%**; the oldest band (over 64) at about **9%**. Of 30 children under 4, 20 survived |
| Fare | Survival rose with fare band: **19.7%** → **30.4%** → **45.5%** → **58.1%** |
| Port of embarkation | Cherbourg (C) **55.4%** · Queenstown (Q) **39.0%** · Southampton (S) **33.9%** |
| Travelling alone | Passengers alone survived at **30.4%** versus **50.6%** for those with family |
| Family size | Families of 4 had the best survival (**72.4%**); sizes 5 and above did poorly |

---

## 🤖 Model Comparison

| Rank | Model | Score |
|:--:|---|:--:|
| 1 | Random Forest | 86.76 |
| 1 | Decision Tree | 86.76 |
| 3 | KNN (k = 3) | 84.74 |
| 4 | SVC with Grid Search (`C=1`, `gamma=0.1`, `rbf`) | 83.73 |
| 5 | Logistic Regression | 80.36 |
| 6 | Linear SVC | 79.01 |
| 7 | Perceptron | 78.34 |
| 8 | Support Vector Machines (default) | 78.23 |
| 9 | Stochastic Gradient Descent | 77.33 |
| 10 | Naive Bayes | 72.28 |

> ⚠️ These are **training accuracies** (`model.score(X_train, Y_train)`), so the tree-based models are likely overfitted. Cross-validation or a hold-out split would give a fairer ranking.

---

## 📊 Visualizations

| Plot | Shows |
|---|---|
| Histograms (FacetGrid) | Age distribution of survivors vs. non-survivors |
| Histograms (FacetGrid) | Age by `Pclass` and `Survived` |
| Point plots | Survival rate by `Pclass` and `Sex` for each port of embarkation |
| Bar plots | Average fare by `Sex` for each port and survival outcome |
| Histograms (FacetGrid) | Age by `Pclass` and `Sex` (used to fill missing ages) |
| Heatmaps | Missing values before and after cleaning |
| Confusion matrix | Helper function for evaluating a model's predictions |

## 👩‍💻 Author

**Marwa Samy** · [GitHub](https://github.com/marwa23-rgb)
