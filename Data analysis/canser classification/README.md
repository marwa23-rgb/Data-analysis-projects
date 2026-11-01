<h1 align="center">🎗️ Breast Cancer Classification with Keras</h1>

<p align="center">
  Binary classification of breast tumors from the Wisconsin Diagnostic dataset using a Keras neural network, early stopping and dropout
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C8CBF" alt="Seaborn">
  <img src="https://img.shields.io/badge/scikit--learn-Preprocessing-F7931E?logo=scikitlearn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/TensorFlow-Keras-FF6F00?logo=tensorflow&logoColor=white" alt="TensorFlow">
  <a href="https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic)"><img src="https://img.shields.io/badge/Dataset-UCI-0B6BCB" alt="UCI"></a>
</p>

## 📌 Overview

This project uses the **Breast Cancer Wisconsin (Diagnostic)** dataset, in which 30 numeric features describe the cell nuclei in a digitized image of a fine needle aspirate (FNA) of a breast mass. It explores the data, scales the features, trains a small neural network, shows how **overtraining** raises the validation loss, and fixes it with **early stopping** and **dropout** layers. The final model is evaluated with a classification report and a confusion matrix.

> Each of the 10 base measurements (radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry, fractal dimension) is stored as three columns: the **mean**, the **standard error** and the **worst** (mean of the three largest values).

---

## ⚡ At a Glance

| 🧬 Samples | 📊 Features | 🎯 Target Column | ❓ Missing Values | 🧪 Test Split |
|:---:|:---:|:---:|:---:|:---:|
| **569** | **30** | **`benign_0__mal_1`** | **None** | **25% (143 rows)** |

---

## 🔄 Workflow

1. **Load & Inspect** – Checked data types, non-null counts and summary statistics (`info()`, `describe()`).
2. **Explore** – Plotted the class balance, a correlation heatmap, and each feature's correlation with the target.
3. **Split** – Divided the data 75/25 into 426 training and 143 test rows (`random_state=101`).
4. **Scale** – Fitted a `MinMaxScaler` on the training set only, then transformed both sets.
5. **Model** – Built a `Dense(30) → Dense(15) → Dense(1, sigmoid)` network compiled with `binary_crossentropy`.
6. **Tune** – Compared three training setups: too many epochs, early stopping, and early stopping with dropout.
7. **Evaluate** – Predicted the test set and reported precision, recall, F1 and a confusion matrix.

---

## 🧹 Data Quality

| Check | Result |
|---|---|
| Rows × columns | 569 × 31 (30 features + target) |
| Missing values | None (all columns have 569 non-null values) |
| Data types | 30 `float64` features, 1 `int64` target |
| Class distribution | 357 rows in class `1` (62.7%) · 212 rows in class `0` (37.3%) |
| Scaling | `MinMaxScaler` fitted on training data only |

> ⚠️ The target column is named `benign_0__mal_1`, but the class counts match the original dataset's 357 benign / 212 malignant, which suggests class `1` is actually the **benign** group in this file. Check the labels before interpreting results clinically.

---

## 🔍 Key Findings

| Question | Result |
|---|---|
| Feature correlations | Size-related features have the strongest relationship with the target, all **negative**: worst concave points (**−0.79**), worst perimeter (**−0.78**), mean concave points (**−0.78**), worst radius (**−0.78**), mean perimeter (**−0.74**) |
| Weakest features | Smoothness error, mean fractal dimension, texture error and symmetry error are close to **0** |
| Overtraining (600 epochs) | Training loss kept falling to ≈ **0.004**, but validation loss bottomed out near **0.11** and then climbed to ≈ **0.33** |
| Early stopping | Stopped at epoch **72** (`patience=25`), with validation loss around **0.115** |
| Dropout + early stopping | Training stopped at epoch **117**, with validation loss reaching about **0.09**, and smoother loss curves |
| Test accuracy | **97%** (139 of 143 correct) |

**Final classification report (test set)**

| Class | Precision | Recall | F1-score | Support |
|:--:|:--:|:--:|:--:|:--:|
| 0 | 0.95 | 0.98 | 0.96 | 55 |
| 1 | 0.99 | 0.97 | 0.98 | 88 |
| **Accuracy** | | | **0.97** | **143** |

**Confusion matrix**

| | Predicted 0 | Predicted 1 |
|---|:--:|:--:|
| **Actual 0** | 54 | 1 |
| **Actual 1** | 3 | 85 |

---

## 🧠 Model Architecture

| Layer | Units | Activation | Dropout |
|---|:--:|:--:|:--:|
| Dense | 30 | ReLU | 0.5 |
| Dense | 15 | ReLU | 0.5 |
| Dense (output) | 1 | Sigmoid | – |

> **Loss:** `binary_crossentropy` · **Optimizer:** `adam` (first two experiments), `rmsprop` (dropout model) · **Early stopping:** monitor `val_loss`, `patience=25`

---

## 📊 Visualizations

| Plot | Shows |
|---|---|
| Count plot | Class balance of the target |
| Heatmap | Correlation between all columns |
| Bar plot | Correlation of every feature with the target |
| Line plot | Training vs. validation loss with 600 epochs (overfitting) |
| Line plot | Training vs. validation loss with early stopping |
| Line plot | Training vs. validation loss with early stopping and dropout |

---

## ⚠️ Limitations

- The same 143 rows are used for early stopping (`val_loss`) and for the final evaluation, so the reported 97% is slightly optimistic. A separate validation split or cross-validation would be fairer.
- The dropout run also changed the optimizer from `adam` to `rmsprop`, so its improvement cannot be credited to dropout alone.
- `EarlyStopping` was not set to `restore_best_weights=True`, so the saved model is the one from the last epoch, not the best one.
- The dataset is small (569 rows), and a single random split can shift the metrics.
- In a medical setting the 3 misses where an actual class-1 case was predicted as class 0 matter as much as the single opposite error, so per-class recall deserves attention beyond overall accuracy.
- The target column name conflicts with the class counts (see Data Quality).


## 👩‍💻 Author

**Marwa Samy** · [GitHub](https://github.com/marwa23-rgb)
