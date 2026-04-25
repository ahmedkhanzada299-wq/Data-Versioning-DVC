# 🚀 DVC (Data Version Control) — Complete Guide

## 📌 Overview

This project demonstrates how to use **DVC (Data Version Control)** for managing datasets in machine learning workflows.

DVC extends Git by enabling version control for:

* Large datasets
* Machine learning models
* Data pipelines

> **Key Idea:**
> **Git tracks code, DVC tracks data.**

---

## 🎯 Why Use DVC?

Traditional Git has limitations:

* ❌ Inefficient for large files
* ❌ No proper dataset versioning
* ❌ Difficult collaboration in ML projects

### ✅ DVC solves this by:

* Storing large data in remote storage
* Tracking lightweight metadata in Git
* Enabling reproducibility of experiments

---

## 🧠 Core Concepts

### 1. Data vs Metadata

* **Git:** Tracks `.dvc` files (metadata)
* **DVC:** Tracks actual data (stored in remote)

---

### 2. Remote Storage

DVC stores data in:

* AWS S3
* Google Drive
* Azure Blob
* Local directory (used in this project)

---

### 3. `.dvc` File

A `.dvc` file acts as a pointer to your data.

```yaml
outs:
- md5: <hash>
  path: data
```

👉 This file contains:

* Data path
* Version (hash)

---

### 4. Cache System

DVC internally stores data in:

```
.dvc/cache/
```

Benefits:

* Fast operations
* Deduplication (no duplicate storage)
* Efficient version switching

---

## 🛠️ Project Workflow

### Step 1: Initialize Git

```bash
git init
```

---

### Step 2: Create Data Script

```python
import pandas as pd

df = pd.DataFrame({"name": ["Ahmed"], "age": [22]})
df.to_csv("data/data.csv", index=False)
```

---

### Step 3: Commit Code

```bash
git add .
git commit -m "initial commit"
```

---

### Step 4: Initialize DVC

```bash
pip install dvc
dvc init
```

---

### Step 5: Setup Remote Storage

```bash
mkdir S3
dvc remote add -d myremote S3
```

---

### Step 6: Track Data

```bash
dvc add data/
```

Then remove data from Git:

```bash
git rm -r --cached data
```

---

### Step 7: Commit Metadata

```bash
git add .gitignore data.dvc
git commit -m "track data with DVC"
```

---

### Step 8: Push Data to Remote

```bash
dvc push
```

---

## 🔄 Data Versioning Workflow

Whenever your data changes:

```bash
# Check changes
dvc status

# Save version
dvc commit

# Push data
dvc push

# Save metadata in Git
git add .
git commit -m "data updated"
```

---

## 📂 Project Structure

```
project/
│
├── data/            # actual data (not tracked by Git)
├── data.dvc         # tracked by Git
├── .dvc/
│   └── cache/
├── .gitignore
├── mycode.py
```

---

## 👥 Collaboration Workflow

For team members:

```bash
git pull
dvc pull
```

This ensures:

* Latest code from Git
* Latest data from DVC

---

## ❗ Common Mistakes

* Tracking data with both Git and DVC
* Forgetting `dvc push`
* Not committing `.dvc` files
* Incorrect remote configuration

---

## 🎤 Interview Questions

### Q1: Difference between Git and DVC?

* Git → Code versioning
* DVC → Data & model versioning

---

### Q2: What is a `.dvc` file?

* A metadata file pointing to actual data

---

### Q3: What does `dvc push` do?

* Uploads data to remote storage

---

### Q4: Why use hashing?

* To detect changes in data efficiently

---

## 🔥 Key Takeaway

> **"Git tells what changed in code, DVC tells what changed in data."**

---

## 📌 Future Enhancements

* Add DVC pipelines (`dvc.yaml`)
* Experiment tracking
* Model versioning

---

## 📜 License

This project is for educational purposes.
