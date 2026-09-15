# Level 1 — Task 3: Cleaning Data (Systematic Data Cleansing & Quality Audit)

**Domain:** Data Analytics  
**Program:** Oasis Infobyte Summer Internship Program (OIBSIP)  
**Repository:** `OIBSIP_DataAnalytics_Task3`  
**Author:** Aryan  

---

## 1. Objective
The objective of this project is to demonstrate professional-grade data cleansing and data quality governance by taking an uncurated, deliberately messy dataset and systematically transforming it into a clean, analysis-ready format. Every data modification is documented with explicit technical justification and verified through an audited **Before vs. After Data Quality Matrix**.

---

## 2. Steps Performed
1. **Data Ingestion & Initial Quality Audit:**
   - Ingested raw dataset (`data/raw_dirty_dataset.csv`, 1,145 rows, 8 columns).
   - Produced a comprehensive pre-cleaning quality report cataloging missing values, duplicate rows, anomalous string formats, and numerical range violations.
2. **Deduplication & Primary Key Verification:**
   - Identified and permanently purged 45 duplicate records.
   - Enforced primary key integrity by stripping whitespace, standardizing uppercase formatting, and dropping records with missing `Customer_ID`.
3. **Categorical Standardization:**
   - Normalized 10+ informal gender casing variations (`"male"`, `"m"`, `"M"`, `"FEMALE"`, `"f"`) into uniform binary labels (`"Male"`, `"Female"`), imputing missing values with the statistical **mode**.
   - Standardized abbreviated customer tiers (`"std"`, `"prem"`, `"vip"`) into uniform title-cased labels (`"Standard"`, `"Premium"`, `"VIP"`), imputing missing entries with the **mode**.
4. **Currency Cleaning & Type Casting:**
   - Stripped currency symbols (`$`) and formatting commas (`,`) from `Annual_Income`.
   - Filtered negative income anomalies, cast to `float64`, and imputed missing entries with the robust **median** ($86,157.89).
5. **Multi-Format Date Standardization:**
   - Parsed multiple date format variants (`YYYY-MM-DD`, `DD/MM/YYYY`, `Month DD, YYYY`) into uniform ISO `datetime64[ns]` objects, filling missing timestamps using temporal forward-fill.
6. **Domain Bounding & Outlier Treatment:**
   - Bounded `Age` to valid human range [18, 80], replacing extreme anomalies (e.g., -8, 195) with the median (39).
   - Bounded `Credit_Score` to standard financial bureau limits [300, 850], replacing invalid scores (e.g., 45, 1,250) with the median (681).
   - Applied **Interquartile Range (IQR Winsorization)** on `Annual_Income`, capping extreme leverage outliers to the upper fence ($Q3 + 1.5 \times IQR = $205,807.23).
7. **Quality Verification & Dataset Export:**
   - Verified data completeness and exported the finalized, analysis-ready dataset to `data/cleaned_dataset.csv`.

---

## 3. Tools Used
- **Programming Language:** Python 3.12+
- **Data Cleansing & Transformation:** `pandas`, `numpy`
- **Data Visualization & Auditing:** `matplotlib`, `seaborn`
- **Interactive Computing:** Jupyter Notebook (`.ipynb`)
- **Version Control:** Git & GitHub

---

## 4. Outcome in Brief
- **100% Data Cleanliness Achieved:**
  - **Zero Duplicates:** 45 duplicate rows detected and purged (1,095 final distinct records).
  - **Zero Missing Values:** All 147 raw null values were systematically resolved using justified statistical methods (mode for categories, median for continuous financials, forward-fill for sequential metrics).
  - **100% Data Type Consistency:** All fields were converted to their correct analytical dtypes (`datetime64[ns]` for dates, `float64` for financials, `int64` for age and credit score).
- **Outlier Normalization:**
  - Eradicated biologically impossible ages (e.g., -8, 195) and bounded all customer ages within [18, 80].
  - Bounded credit scores to the official financial bureau range [300, 850].
  - Preserved sample size while mitigating extreme financial leverage by capping 2 extreme multi-million-dollar income outliers at the IQR threshold of $205,807.23.
- **Before vs. After Quality Matrix:**

| Quality Metric | Before Cleansing | After Cleansing | Audit Status |
| :--- | :---: | :---: | :---: |
| **Total Row Count** | 1,145 | 1,095 | Purged 45 duplicates & 5 unidentifiable keys |
| **Duplicate Rows** | 45 | 0 (0.0%) | 100% Unique |
| **Total Null Values** | 147 | 0 (0.0%) | 100% Imputed / Resolved |
| **Primary Key Nulls** | 7 | 0 | Cleaned & Unique |
| **Signup Date Dtype** | `object` (dirty strings) | `datetime64[ns]` | Standard ISO DateTime |
| **Gender Categories** | 10+ Variants | 2 (`Male`, `Female`) | Uniform Standard |
| **Annual Income Dtype** | Dirty String (`$`, commas) | `float64` | Valid Numeric Financials |
| **Age Anomalies** | 5 Detected (-8, 195) | 0 (Median 39) | Valid Human Range [18, 80] |
| **Credit Score Anomalies** | 3 Detected (45, 1,250) | 0 (Median 681) | Bureau Standard [300, 850] |

---

## 5. Repository Structure & How to Run
```
OIBSIP_DataAnalytics_Task3/
│
├── data/
│   ├── raw_dirty_dataset.csv          # Uncurated dirty input dataset
│   └── cleaned_dataset.csv            # Clean, validated, analysis-ready dataset
├── plots/
│   ├── 01_missing_data_before_after.png
│   ├── 02_outlier_boxplots_before_after.png
│   └── 03_cleaned_feature_distributions.png
├── Data_Cleaning_Pipeline.ipynb       # Fully executed interactive Jupyter Notebook
├── clean_data.py                      # Standalone Python cleaning pipeline
└── README.md                          # Project documentation
```

### Execution Instructions:
```bash
# Run standalone script:
python clean_data.py

# Launch interactive notebook:
jupyter notebook Data_Cleaning_Pipeline.ipynb
```