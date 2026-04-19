# 5G-intrusion-detection-System
# Network Intrusion Detection using Machine Learning

This project focuses on detecting **malicious vs benign network traffic** using a Machine Learning model trained on a large encoded dataset.

---

## 📂 Dataset

Download the dataset from here:
👉 [Download Dataset](https://download.fairdata.fi:443/download?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE3NzY4NjQyODIsImRhdGFzZXQiOiI5ZDEzZWYyOC0yY2E3LTQ0YjAtOTk1MC0yMjUzNTlhZmFjNjUiLCJmaWxlIjoiL0VuY29kZWQuemlwIiwicHJvamVjdCI6IjIwMDY5MzgiLCJyYW5kb21fc2FsdCI6ImRlM2VkMGQ0In0.pTSPT7ZLkBeQUktdjPjLl1x9ttW5KUshfjzlaC88uWo)

* File used: `Encoded.csv`
* Total rows: ~1.2 million
* Features: 90+ numerical + encoded categorical features

---

## 🧠 Problem Statement

Classify network traffic into:

* **Benign**
* **Malicious**

---

## ⚙️ Tech Stack

* Python 🐍
* NumPy
* Pandas
* Matplotlib
* Scikit-learn

---

## 🔄 Workflow

### 1. Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

---

### 2. Load Dataset

```python
dataset = pd.read_csv("Encoded.csv")
```

---

### 3. Data Cleaning

* Dropped unnecessary columns
* Removed highly missing-value columns
* Removed null values

```python
drop_cols = [
    "Unnamed: 0", "Seq",
    "Attack Type", "Attack Tool",
    "dTos","dTtl","dHops",
    "SrcGap","DstGap",
    "SrcWin","DstWin",
    "sVid","dVid",
    "SrcTCPBase","DstTCPBase"
]

df = dataset.drop(columns=drop_cols, errors="ignore")
df = df.dropna()
```

---

### 4. Feature & Target Split

```python
y = df["Label"]
x = df.drop("Label", axis=1)
```

---

### 5. Train-Test Split

```python
from sklearn.model_selection import train_test_split

xtrain, xtest, ytrain, ytest = train_test_split(
    x, y, test_size=0.2, stratify=y, random_state=42
)
```

---

### 6. Model Training (Random Forest)

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    n_estimators=100,
    max_depth=20,
    n_jobs=-1,
    random_state=42
)

rf.fit(xtrain, ytrain)
```

---

### 7. Evaluation

```python
from sklearn.metrics import accuracy_score, classification_report

y_pred_rf = rf.predict(xtest)

print("Accuracy:", accuracy_score(ytest, y_pred_rf))
print(classification_report(ytest, y_pred_rf))
```

---

## 📊 Results

* **Accuracy:** ~98.5%
* High precision and recall for both classes

```
Accuracy: 0.9851

Benign:
Precision: 1.00
Recall: 0.96

Malicious:
Precision: 0.98
Recall: 1.00
```

---

## ❌ Error Analysis

```python
wrong = ytest != y_pred_rf
print("Total errors:", wrong.sum())
```

* Total Errors: **3612**
* Correct Predictions: **239566**

---

## 📁 Project Structure

```
├── Encoded.csv
├── model.ipynb
├── README.md
```

---

## 🚀 How to Run

```bash
pip install numpy pandas matplotlib scikit-learn
```

```bash
python your_script.py
```

---

## 📌 Key Insights

* Random Forest performs very well on large structured datasets
* Proper feature selection improves performance
* Stratified sampling ensures balanced evaluation

---

## 🤝 Contributing

Feel free to fork this repo and improve the model or preprocessing!

---

## 📜 License

This project is for educational purposes.
