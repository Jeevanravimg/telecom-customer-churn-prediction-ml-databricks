# Telecom Customer Churn Prediction – End-to-End ML Pipeline (Databricks)

## 📌 Project Overview
This project implements a **production-grade, end-to-end Machine Learning pipeline** to predict **customer churn** in the telecom domain.  
The solution is built using **Databricks, PySpark, Delta Lake, and MLflow**, following **modern data engineering and MLOps best practices**.

The pipeline covers the **entire ML lifecycle**:
- Data generation
- Ingestion into Delta Lake (Bronze → Silver → Gold)
- Cleaning & validation
- Exploratory Data Analysis (EDA)
- Feature engineering
- Handling class imbalance (SMOTE)
- Model training & evaluation
- Model registration and inference readiness

---

## 🏗️ Architecture & Design Principles

- **Medallion Architecture**
  - **Bronze**: Raw ingested data
  - **Silver**: Cleaned, validated, standardized data
  - **Gold**: Feature-engineered, model-ready & inference outputs
- **No data leakage** (train-test split before cleaning & SMOTE only on train)
- **Reproducibility** using MLflow
- **Scalable** using Spark & Delta Lake
- **Modular pipeline** using Databricks notebooks

---

## 🧰 Tech Stack

- **Databricks**
- **Apache Spark (PySpark)**
- **Delta Lake**
- **Python**
- **Scikit-learn**
- **MLflow**
- **Pandas, NumPy**
- **Matplotlib, Seaborn**
- **Faker (Synthetic data generation)**

---

## 📂 Project Structure

telecom-customer-churn-ml/
│
├── notebooks/
│ ├── 0_Pipeline.ipynb
│ ├── 1_Data_Gen_Col.ipynb
│ ├── 2_Data_Ingestion.ipynb
│ ├── 3_Data_Splitting.ipynb
│ ├── 4_Data_Cleaning.ipynb
│ ├── 5_EDA.ipynb
│ ├── 6_Transformations.ipynb
│ ├── 7_SMOTE.ipynb
│ ├── 8_Feature_Engineering.ipynb
│ └── 9_ML_Pipeline_Flow.ipynb
│
│
├── README.md


---

## 🔄 End-to-End Pipeline Description

### 1️⃣ Data Generation & Collection
- Loaded original Telco Customer Churn dataset.
- Generated **5,00,000 synthetic records** using **Faker** to simulate large-scale production data.
- Synthetic churn logic based on:
  - Contract type
  - Tenure
  - Monthly charges
- Combined original and generated data.

---

### 2️⃣ Data Ingestion (Bronze Layer)
- Ingested raw data into **Delta tables**.
- Ensures traceability and reproducibility.

---

### 3️⃣ Train-Test Split (Before Cleaning)
- Converted Spark → Pandas for stratified split.
- **80% Train / 20% Test**
- Stratified on target (`Churn`) to preserve class distribution.

✔️ Prevents data leakage and simulates real-world ingestion.

---

### 4️⃣ Data Cleaning & Validation (Silver Layer)

#### ✔ Schema Validation
- Verified column types
- Checked nulls, blanks, invalid values

#### ✔ Standardization
- Trimmed strings
- Replaced `NULL`, `None`, empty strings
- Corrected numeric datatypes

#### ✔ Missing Value Handling
- Numeric → Median
- Categorical → Mode (from training data)

#### ✔ Outlier Treatment
- IQR-based capping
- Applied **train fences to test data**


---

### 5️⃣ Exploratory Data Analysis (EDA)
- Target distribution analysis
- Numeric feature distributions
- Boxplots for outliers
- Categorical frequency analysis
- Feature vs Churn analysis
- Correlation heatmaps

📊 Ensured no target leakage during EDA.

---

### 6️⃣ Data Transformation
- Log transformation for skewed numeric features
- Standard scaling using `StandardScaler`
- Categorical encoding:
  - `StringIndexer`
  - `OneHotEncoder`
- Schema consistency checks between train & test


---

### 7️⃣ Handling Class Imbalance (SMOTE)
- Converted Spark → Pandas
- Applied **SMOTE only on training data**
- Ensured all features were numeric
- Re-converted balanced dataset to Spark

✔️ Prevented synthetic data leakage into test set.

---

### 8️⃣ Feature Engineering
- Created domain-specific features:
  - `AvgMonthlySpend`
  - `Monthly_to_Total_Ratio`
  - `HasInternet`
  - `ActiveServiceCount`
- Feature correlation analysis
- Feature importance using Random Forest
- Dropped low-importance features
- Reordered features by importance

---

### 9️⃣ Feature Assembly & Scaling
- Combined features using `VectorAssembler`
- Applied `StandardScaler` on vectorized features

---

### 🔟 Model Training (Pure Python – Sklearn)
- Converted Spark vectors → Pandas arrays
- Trained **optimized RandomForestClassifier**
- Hyperparameters tuned for speed & generalization
- Evaluated on **exact same Spark test set**

#### 📊 Metrics
- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

---

### 1️⃣1️⃣ Experiment Tracking & Model Registry
- Logged:
  - Parameters
  - Metrics
  - Model artifacts
- Registered model:


✔️ Versioned, auditable, production-ready.

---

### 1️⃣2️⃣ Model Loading & Inference
- Loaded registered model using MLflow
- Performed sample predictions
- Ready for:
  - REST API serving
  - Batch scoring
  - Databricks Model Serving

---

## 📈 Business Impact
- Identifies customers likely to churn
- Enables proactive retention strategies
- Scales to large telecom datasets
- Production-ready architecture

---

## 🚀 Future Enhancements
- Real-time inference via REST API
- Data drift monitoring
- Automated retraining pipeline
- CI/CD with Databricks Asset Bundles
- Integration with dashboards (Power BI / Tableau)

---

## 👤 Author
**Jeevan M G**  
Machine Learning & Data Engineering Enthusiast  
Built using Databricks, Spark, and MLflow





