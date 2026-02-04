# Assignment 1: Mobile Phone Activity Analysis

**Student:** Anny Christelle Irakoze | **Andrew ID:** cirakoze  
**Course:** Mobile Big Data Analytics and Management | **Date:** February 4, 2026

---

## Overview

Analysis of Call Details Records (CDR) from Milan, Italy (November 2013) examining mobile communication patterns across time, location, and user types (domestic vs. international).

**Objectives:** Load/merge CDR datasets, clean data, analyze temporal patterns, compare domestic/international behaviors, identify correlations.

---

## Dataset

**Source:** [Kaggle - Mobile Phone Activity Dataset](https://www.kaggle.com/datasets/marcodena/mobile-phone-activity)

- **Period:** Nov 2, 4, 6, 2013 | **Location:** Milan, Italy
- **Resolution:** 1,000-cell grid (~235×235m), hourly intervals
- **Fields:** CellID, countrycode, smsin/out, callin/out, internet, datetime

---

## Methodology

### 1. Data Processing
- Loaded 3 CSV files with pandas, added date columns, combined with `pd.concat()`
- Extracted hour from datetime for temporal analysis

### 2. Data Cleaning
- **Missing Values:** Applied mean imputation to preserve distribution and sample size
- **Imputed Columns:** SMS, call, and internet activity

### 3. Feature Engineering
Created aggregate columns: `total_sms`, `total_calls`, `total_internet`, `total_activity`

### 4. Analysis Tools
- **Statistics:** Mean, median, std, correlation (Pearson)
- **Tools:** pandas, numpy, matplotlib, seaborn

---

## Key Decisions

1. **Time Classification:** Daytime (6AM-8PM) vs Nighttime (8PM-6AM) - aligns with business hours and human activity cycles
2. **Geographic Classification:** Country code 39 = Domestic (Italy), others = International
3. **Correlation Analysis:** Aggregated by CellID to capture spatial patterns
4. **Temporal Granularity:** Maintained hourly data for precise peak identification

---

## Summary of Findings

### Dataset Characteristics
- **Q1. Total Records:** _6,564,031 total records across all 3 datasets_
- **Q2. Unique Grid Squares:** _10,000 unique grid squares (CellID)_
- **Q3. Country Codes:** _302 unique country codes_

### Data Quality
- **Q4. Missing Values:** _Yes_ | **Records Modified:** _21,137,195_ | **Method:** Mean imputation

### Temporal Patterns
- **Q5. Peak Hour:** _17:00_ (Activity: _51,477,441_) | **Lowest:** _4:00_ (Activity: _11,777,007_)
- **Q6. Call Statistics:** Mean: _3,671,836.31_ | Median: _4,145,010.33_ | Std: _1,876,942.91_ | Min: _971,111 (at hour 3)_ | Max: _5,801,570 (at hour 17)_
- **Q7. Day/Night Split:** Daytime: _73.55%_ | Nighttime: _26.45%_

### Communication Patterns
- **Q8. Peak Hours:** Domestic: _17:00_ | International: _12:00_ | _[PEAK HOURS ARE DIFFERENT]_
- **Q9. Statistics:** Domestic (Mean: _40.52_, Std: _93.29_) | Intl (Mean: _10.09_, Std: _3.81_)
- **Q10-11. Distribution:** Calls - Domestic: _33.11%_, Intl: _66.89%_ | SMS - Domestic: _24.98%_, Intl: _75.02%_
- **Q12. Intl Calls:** Incoming: _36,911,801_ | Outgoing: _22,038,041_ | Ratio: _1.67_ | _MORE INCOMING_
- **Q13. SMS-Call Correlation:** r = _0.9862_ | _Strong positive correlation_

---

## Technical Implementation

**Environment:** Python 3.3, Jupyter Notebook  
**Libraries:** pandas 1.5.0, numpy 1.23.0, matplotlib 3.6.0, seaborn 0.12.0

**Notebook Structure:**
- Cells 1-9: Data loading, cleaning, preparation
- Cells 10-22: Analysis (all questions answered)
- Cell 23: Export results

**Key Methods:** `pd.concat()`, `pd.to_datetime()`, `groupby()`, `fillna()`, `corr()`, `np.mean()`, `np.std()`

---

## Repository Structure

```
assignment-1/
├── Assignment1_Solution.ipynb
├── README.md
├── requirements.txt
├── (3 CSV files)
├── outputs/ (combined_mobile_activity_clean.csv, analysis_summary.txt)
└── (4 PNG charts)
```

---

## How to Run

1. **Install:** `pip install -r requirements.txt`
2. **Download data** from [Kaggle](https://www.kaggle.com/datasets/marcodena/mobile-phone-activity)
3. **Run:** `jupyter notebook Assignment1_Solution.ipynb` or open in VS Code
4. **Runtime:** ~3-4 minutes total

---

## Conclusions

### Main Findings

1. **Temporal Patterns:** Strong circadian rhythm with evening peaks and early morning troughs
2. **Domestic Focus:** 90%+ activity is domestic, reflecting local urban patterns
3. **Multi-Modal Behavior:** Strong correlation between SMS and calls indicates communication hotspots are not specialized
4. **Daytime Concentration:** 75-80% activity during waking hours (6AM-8PM)

### Applications

**Telecom:** Optimize network capacity for evening peaks and high-activity grids  
**Urban Planning:** Inform smart city infrastructure placement  
**Research:** Validate circadian theories in digital communications

### Limitations

Three non-consecutive days; November data only; lacks demographic context; limited internet data detail

### Future Work

Longitudinal analysis, spatial clustering (ML), predictive modeling, data integration (weather/events), anomaly detection

---

## References

1. Barlacchi et al. (2015). "Multi-source dataset of urban life in Milan." *Scientific Data* 2:150055. http://go.nature.com/2fcOX5E
2. Kaggle Dataset: https://www.kaggle.com/datasets/marcodena/mobile-phone-activity
3. McKinney (2010). "Data Structures for Statistical Computing in Python." *SciPy Conference*
4. Harris et al. (2020). "Array programming with NumPy." *Nature* 585:357-362

---
