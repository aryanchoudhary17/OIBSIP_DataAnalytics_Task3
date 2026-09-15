# Task 3: Cleaning Data (Systematic Data Cleansing & Quality Audit)

**Internship Track:** Data Analytics  
**Program:** Oasis Infobyte Summer Internship Program (OIBSIP)  
**Level:** Level 1 — Task 3  
**Folder Format:** `OIBSIP/DataAnalytics-L1-CleaningData`  
**Author:** Aryan  

---

## 📌 Project Objective
Real-world datasets regularly suffer from structural noise, duplicate records, missing entries, format discrepancies, and extreme outliers. The objective of this project is to build an end-to-end, reproducible data cleaning and governance pipeline that transforms a messy raw dataset into a clean, analysis-ready format with full documentation of all cleaning decisions.

---

## 🛠️ Tech Stack & Libraries
- **Language:** Python 3.12+
- **Data Manipulation & Cleaning:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Interactive Environment:** Jupyter Notebook (`.ipynb`)

---

## 📋 Feature Checklist Verification
- [x] **Data Quality Report (Before Cleaning):** Cataloged null counts per column, duplicate row counts, datatype issues, and range anomalies across all features.
- [x] **Missing Data Handling with Justification:**
  - *Primary Keys (`Customer_ID`):* Dropped records lacking IDs (an identity cannot be statistically estimated).
  - *Categorical Features (`Gender`, `Customer_Segment`):* Imputed using the statistical **mode**.
  - *Skewed Financial Features (`Annual_Income`):* Imputed using the robust **median**.
  - *Sequential Time Features (`Signup_Date`, `Activity_Score`):* Imputed using forward-fill (`ffill`) and back-fill (`bfill`).
- [x] **Duplicate Removal:** Identified and permanently purged 45 duplicate rows, with before/after audit tracking.
- [x] **Standardization & Formatting:**
  - Standardized gender casing variations (`"male"`, `"m"`, `"M"`, `"FEMALE"`, `"f"`) into uniform binary labels (`"Male"`, `"Female"`).
  - Standardized customer tiers (`"std"`, `"prem"`, `"vip"`) into standard title-case categories.
  - Parsed multi-format date strings (`YYYY-MM-DD`, `DD/MM/YYYY`, `Month DD, YYYY`) into ISO `datetime64[ns]`.
- [x] **Outlier Detection & Treatment:**
  - Bounded `Age` to biologically plausible range $[18, 80]$, replacing invalid values with median ($39$).
  - Bounded `Credit_Score` to standard financial bureau range $[300, 850]$, replacing invalid values with median ($681$).
  - Applied Interquartile Range (**IQR Winsorization**) on `Annual_Income`, capping extreme high-leverage outliers at the upper fence.
- [x] **Data Type Corrections:** Converted financial strings to `float64`, dates to `datetime64[ns]`, scores to `int64`, and IDs to uppercase `str`.
- [x] **Before vs. After Summary Table:** Audited null count, duplicate count, row count, and datatype accuracy side-by-side.
- [x] **Saved Cleaned Dataset:** Exported final clean dataset to `data/cleaned_dataset.csv`.

---

## 📊 Before vs. After Data Quality Audit Table

| Quality Metric | Before Cleansing | After Cleansing | Audit Status |
| :--- | :---: | :---: | :---: |
| **Total Row Count** | 1,145 | 1,095 | Purged 45 duplicates & 5 unidentifiable records |
| **Duplicate Rows** | 45 | 0 (0.0%) | 100% Unique |
| **Total Null Values** | 147 | 0 (0.0%) | 100% Imputed / Resolved |
| **Primary Key Nulls (`Customer_ID`)** | 7 | 0 | Cleaned & Unique |
| **`Signup_Date` Data Type** | `object` (inconsistent strings) | `datetime64[ns]` | ISO Formatted |
| **`Gender` Consistency** | 10+ Variants (`m`, `MALE`, etc.) | 2 Standardized (`Male`, `Female`) | Uniform Standard |
| **`Annual_Income` Data Type** | Messy strings (`$65,000.00`, `N/A`) | `float64` | Valid Numeric Financials |
| **`Age` Anomalies** | 5 Detected (`-8`, `195`, etc.) | 0 (Imputed to Median: 39) | Valid Human Range $[18, 80]$ |
| **`Credit_Score` Anomalies** | 3 Detected (`45`, `1250`) | 0 (Bounded to $[300, 850]$) | Financial Bureau Standard |

---

## 📂 Project Structure
```
OIBSIP/DataAnalytics-L1-CleaningData/
│
├── data/
│   ├── raw_dirty_dataset.csv          # Uncurated dirty input dataset
│   └── cleaned_dataset.csv            # Clean, validated, analysis-ready dataset
├── plots/
│   ├── 01_missing_data_before_after.png
│   ├── 02_outlier_boxplots_before_after.png
│   └── 03_cleaned_feature_distributions.png
├── Data_Cleaning_Pipeline.ipynb       # Executed interactive Jupyter Notebook
├── clean_data.py                      # Automated standalone Python cleaning pipeline
└── README.md                          # Comprehensive documentation
```

---

## 🚀 How to Run the Project

1. **Navigate to the Task Directory:**
   ```bash
   cd OIBSIP/DataAnalytics-L1-CleaningData
   ```

2. **Install Dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

3. **Run the Cleaning Script:**
   ```bash
   python clean_data.py
   ```

4. **Launch the Notebook:**
   ```bash
   jupyter notebook Data_Cleaning_Pipeline.ipynb
   ```

---

## 🎥 Video Walkthrough Guide (for Oasis Infobyte Submission)
- **Duration:** 3–5 minutes
- **Title Card (First 2 Seconds):**
  - **Full Name:** Aryan
  - **Assigned Track:** Data Analytics
  - **Task Title:** Level 1 — Task 3: Cleaning Data
- **Walkthrough Agenda:**
  1. Inspect the initial dirty dataset and explain the Data Quality Audit report.
  2. Explain duplicate identification and primary key validation.
  3. Walk through text standardization for categorical columns (`Gender`, `Customer_Segment`).
  4. Demonstrate currency string stripping and date parsing to standard datetime.
  5. Detail the IQR Winsorization for `Annual_Income` and boundary checking for `Age` and `Credit_Score`.
  6. Present the Before vs. After comparison summary table and final output CSV.

---

## 📱 LinkedIn Post Template
```
Pleased to announce the completion of Task 3 (Level 1) of my Data Analytics Internship at @Oasis Infobyte! 🧹✨

📊 Task 3: Systematic Data Cleaning and Quality Audit Pipeline
Data quality is paramount for trustworthy analytics and machine learning. In this project, I built a robust automated cleaning pipeline that tackles real-world data imperfections with audited governance decisions.

Key Highlights:
✅ Comprehensive Data Quality Audit Report (pre-cleaning diagnostics)
✅ Deduplication & primary key integrity preservation
✅ String normalization & categorical standardization
✅ Currency string parsing and multi-format ISO date parsing
✅ Outlier management via domain boundary capping & IQR Winsorization
✅ Rigorous Before vs. After audit verification matrix

GitHub Repository: [Insert Your GitHub Repo Link Here]
Demo Video: [Insert Video Link Here]

Gratitude to @Oasis Infobyte for providing practical real-world data challenges!

#oasisinfobyte #dataanalytics #datacleaning #dataengineering #python #pandas #eda #qualityassurance #internship
```