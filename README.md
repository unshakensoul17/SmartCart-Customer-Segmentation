# SmartCart Customer Segmentation (Clustering)

This project implements an **end-to-end customer segmentation pipeline** for SmartCart using unsupervised learning. It performs data cleaning, feature engineering, dimensionality reduction with PCA, and clustering using **K-Means** and **Agglomerative Clustering** to uncover meaningful customer segments and business insights.

The analysis is conducted in the Jupyter notebook `smartcart.ipynb` using the dataset `smartcart_customers.csv`.

---

## 📁 Project Files

* `smartcart.ipynb` — complete EDA, preprocessing, clustering, and insights
* `smartcart_customers.csv` — customer demographic and purchase behavior dataset

---

## 📊 Dataset Overview

The dataset contains **22 columns**, where each row represents a customer.

**Key attributes include:**

* Demographics: `Year_Birth`, `Education`, `Marital_Status`, `Income`
* Household info: `Kidhome`, `Teenhome`
* Purchase behavior: spending across product categories, purchase channels
* Engagement: `Recency`, `Response`, `Complain`

This is an **unsupervised learning problem** (no target variable).

---

## 🔍 Notebook Workflow

### 1) Data Preparation

* Loads the dataset and handles missing values (`Income` filled with median)
* Feature engineering:

  * `Age` = `2026 - Year_Birth`
  * `Customer_Tenure_Days` from `Dt_Customer`
  * `Total_Spending` from all `Mnt*` columns
  * `Total_Children` = `Kidhome + Teenhome`
* Normalizes:

  * `Education` into fewer categories
  * `Marital_Status` → `Living_With` (Partner / Alone)
* Drops replaced raw columns to form a clean feature set

---

### 2) Outlier Handling

* Visual inspection using pair plots
* Removes extreme values using simple thresholds on `Age` and `Income`

---

### 3) Exploratory Analysis

* Correlation heatmap for numeric features
* Initial behavioral pattern discovery

---

### 4) Encoding

* One-hot encoding of categorical features:

  * `Education`
  * `Living_With`

---

### 5) Feature Scaling

* Standardizes all features using `StandardScaler`
* Prepares data for distance-based clustering

---

### 6) PCA & Visualization

* Reduces dimensionality to **3 principal components**
* Enables 3D visualization and noise reduction

---

### 7) Choosing Number of Clusters

* Uses:

  * Elbow method (WCSS)
  * Silhouette score
* Final choice: **4 clusters**

---

### 8) Clustering Models

* Trains:

  * `KMeans (n_clusters=4)`
  * `AgglomerativeClustering (ward linkage)`
* Visualizes clusters in PCA space

---

### 9) Cluster Profiling & Insights

* Appends cluster labels to the feature table
* Generates:

  * Cluster sizes and customer percentages
  * Per-cluster averages (income, spending, recency, tenure)
  * Channel-wise purchase behavior
  * Complaint and response patterns
  * Top differentiating features per cluster
  * Dominant categories for education and living arrangement

---

## 📈 Outputs for Reports / Presentations

The notebook produces **ready-to-use outputs**, including:

* Cluster size and composition
* Business-focused summary tables
* Key differentiating features per segment
* Interpretable customer profiles

---

## ⚙️ Setup & Execution

### Option A: Jupyter Notebook

```bash
python -m pip install -U pip
python -m pip install pandas numpy matplotlib seaborn scikit-learn kneed jupyter
jupyter notebook
```

Open `smartcart.ipynb` and run all cells sequentially.

---

### Option B: VS Code

* Install Python & Jupyter extensions
* Open `smartcart.ipynb`
* Select the correct Python interpreter
* Run all cells

---

## 📝 Notes & Assumptions

* `Age` is computed using a fixed year (`2026`). Replace with `datetime.now().year` for dynamic calculation.
* Means of one-hot encoded columns represent **fractions**, not absolute counts.
* Clustering results may vary with changes in preprocessing, PCA components, or K.

---

## 🧯 Troubleshooting

* **Missing package**: install using `pip`
* **`kneed` error**: `python -m pip install kneed`
* **CSV not found**: ensure the dataset is in the same directory as the notebook

