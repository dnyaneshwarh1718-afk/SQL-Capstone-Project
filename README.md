
#  Loan Risk ETL Pipeline (MySQL) — Capstone Project

This project focuses on building an end-to-end SQL ETL pipeline for a loan risk dataset using **MySQL**.
The goal was to take raw banking data (accounts, loans, transactions, cards, etc.), clean it, validate it, engineer useful features, and generate a final **master table** that can be directly used for **ML modeling / Power BI reporting**.

---

##  What this project covers

### **1) Raw data preparation**

* Standardized raw table datatypes for performance and consistency
* Added **generated date columns** (`DATE` format) to avoid repeated parsing during queries
* Applied indexing strategy for faster joins and aggregations

### **2) Clean layer (views)**

Created `vw_clean_*` views for reusable cleaned data:

* trimming text fields
* consistent date fields
* safe null handling for numeric columns

### **3) Data validation checks**

Before building features, validation checks were added to ensure data quality:

* table row counts
* primary key uniqueness checks
* foreign key integrity (orphan record detection)
* null checks on critical columns
* loan status domain checks (`A/B/C/D`)

### **4) Feature engineering (SQL aggregations)**

Generated account-level behavioral features such as:

* transaction counts and activity ranges
* total / average transaction amounts
* balance statistics (min / max / avg)
* distinct transaction type and operation counts
* orders summary metrics
* card ownership summary

### **5) Master dataset creation**

Created a final `loan_master` table combining:

* loan info
* account & district metadata
* aggregated transaction behavior
* orders + cards summary features

This final table is structured for downstream tasks like:

* loan default prediction models
* risk segmentation
* dashboarding (Power BI/Tableau)

---

##  Repository Structure

```
data/
  account.csv
  card.csv
  client.csv
  disp.csv
  district.csv
  loan.csv
  orders.csv
  transaction_data.csv

sql/
  01_raw_schema_fix_and_index.sql
  02_data_cleaning_views.sql
  03_data_validation.sql
  04_feature_engineering_aggregations.sql
  05_master_table.sql
```

---

##  How to run this project (MySQL)

### Step 1: Import raw CSV files

Import all CSVs into MySQL using **MySQL Workbench Import Wizard** (or any method you prefer).

### Step 2: Run SQL scripts in order

Run these scripts sequentially:

1. `01_raw_schema_fix_and_index.sql`

   * datatype fixes
   * generated date columns
   * indexes

2. `02_data_cleaning_views.sql`

   * clean reusable views (`vw_clean_*`)

3. `03_data_validation.sql`

   * data quality checks (PK/FK/null/domain)

4. `04_feature_engineering_aggregations.sql`

   * aggregation tables for feature engineering

5. `05_master_table.sql`

   * final `loan_master` dataset

---

## 🧠 Key skills demonstrated

* **SQL ETL development**
* **Data cleaning using views**
* **Data quality validation (PK/FK/null/domain rules)**
* **Indexing strategy for performance optimization**
* **Feature engineering using SQL aggregations**
* **Building ML-ready datasets (master tables)**
* Strong understanding of **relational modeling & joins**

---

##  Output

The main output table is:

✅ `loan_master`

This table is ready for:

* model training pipelines (Python / scikit-learn)
* feature selection & EDA
* reporting & dashboards

---

## Next Improvements (Planned)

* Add time-based rolling features (last 30/90 days transaction behavior)
* Add customer segmentation features (activity buckets)
* Automate full pipeline execution using Python + SQLAlchemy
* Add model training notebook + evaluation metrics

---

