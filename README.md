<p align="center">

  <!-- FULL BADGE COLLECTION -->
  <img src="https://img.shields.io/badge/Field-Clinical%20Data%20Science-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Domain-Survival%20Analysis-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/Method-Kaplan--Meier%20%7C%20Cox%20PH-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Data-Clinical%20Trial%20(VAP%20Study)-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/Source-Randomized%20Controlled%20Trial-red?style=for-the-badge">
  <img src="https://img.shields.io/badge/Python-3.10+-yellow?style=for-the-badge&logo=python">
  <img src="https://img.shields.io/badge/Notebook-Jupyter-orange?style=for-the-badge&logo=jupyter">
  <img src="https://img.shields.io/badge/Libraries-lifelines%2C%20pandas%2C%20matplotlib-brightgreen?style=for-the-badge">
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge">

</p>

<hr>


# **Survival Analysis of Chlorhexidine Trial Outcomes Using Python** 🧪📈

This project is based on a real clinical trial titled  
**“Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash with 0.12 percent and 0.2 percent Concentration on Incidence of VAP”**,  
published in *Annals of International Medical and Dental Research, Vol (7), Issue (3), 2021*.  
The full article is included as **Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf**  
(Local path: `/data/Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf`)

This repository reproduces and interprets **time-to-VAP (Ventilator-Associated Pneumonia)** outcomes using classical Survival Analysis methods in Python. All results, tables and plots are generated using **Chlorhexidine_Trials.ipynb**.

---

## **1️⃣ Project Title**  
**Survival Analysis of Chlorhexidine Trial Outcomes Using Python**

---

## **2️⃣ Project Summary** ✍️

This project analyzes patient-level data from a randomized controlled trial comparing **0.12% vs 0.20% chlorhexidine** mouthwash for preventing VAP in mechanically ventilated ICU patients.

- **Outcome:** Time (days) until VAP (event = 1), with censoring for discharge, death or LAMA.  
- **Why survival analysis:** Different follow-up durations and heavy censoring require time-to-event models.  
- **Learning outcomes:** Kaplan–Meier curves, Log-Rank test, Cox Proportional Hazards model, Schoenfeld residual checks and clinical interpretation.

---

## **3️⃣ Dataset Description** 📚

- **Source:** Randomized controlled trial with 140 ICU patients.  
- **Working dataset:** Cleaned version derived from `Raw Data form Chlorhexidine Trial.xlsx`.

### **Core Variables**
| Column | Description | Type |
| ------ | ----------- | ---- |
| Age | Age in years | Continuous |
| Gender | Male / Female | Categorical |
| TrialArm_num | 1 = 0.12%, 2 = 0.20% | Categorical |
| APACHEII | APACHE II severity score | Continuous |
| TLC_D1 | Day-1 leukocyte count | Continuous |
| time | Time to VAP or censoring | Continuous |
| event | 1 = VAP, 0 = NO VAP | Binary |

---

## **4️⃣ Problem Statement** ❓

This project answers the following clinical questions:

1. Does 0.20% chlorhexidine reduce VAP risk compared to 0.12%?  
2. Is VAP-free survival different between treatment arms?  
3. Do Age, APACHE II, TLC Day 1 or Gender influence time to VAP?  
4. Are survival curves significantly different on Log-Rank test?  
5. How do hazard ratios from the Cox PH model inform clinical interpretation?

---

## **5️⃣ Objectives** 🎯

1. Perform data cleaning  
2. Conduct exploratory data analysis  
3. Estimate survival curves (KM) by treatment groups  
4. Compare groups using the Log-Rank test  
5. Fit a Cox PH model  
6. Check PH assumptions using Schoenfeld residuals  
7. Produce visualizations and clinical interpretation

---

## **6️⃣ Methodology** 🛠️

### **6.1 Data Preparation**
- Cleaned column names (`APACHE II Score` → `APACHEII`, `TLC Day 1` → `TLC_D1`).  
- Encoded `TrialArm` and `Gender` into numeric variables.  
- Ensured `time` and `event` were numeric for survival modelling.  
- **Model variables:** `time`, `event`, `Age`, `APACHEII`, `TLC_D1`, `TrialArm_num`, `Gender_binary`.

**Handling missing values:**  
- Median imputation used for missing values in `APACHEII` and `TLC_D1`, chosen for robustness against skewed clinical data.

---

### **6.2 Exploratory Data Analysis (EDA)** 🔍

**Baseline Summary**
- N = 106, VAP events = 10  
- Mean Age ≈ 47.6  
- APACHE II mean ≈ 16.9  
- TLC Day1 ≈ 15,216  
- Arm1 = 61 patients, Arm2 = 45  
- Male = 93, Female = 13  
- Mean follow-up ≈ 5.7 days  

**Visual Exploration**
- **1. Age Histogram:** Wide and evenly spread adult age range.  
- **2. APACHE II Histogram:** Most patients fall between scores 10–20.  
- **3. TLC Day 1 Boxplot:** High inflammatory markers typical of ICU presentations.

**Life Tables**
- Early days show minimal events; most VAP cases appear between Days 5–10.  
- Cumulative hazard slightly higher in Arm 1.

**Event / Censoring Structure**
- Majority of patients are censored due to discharge, LAMA or death—expected in ICU studies.

**Survival Visual Checks**
- KM curves (overall and arm-wise) verify data suitability before modelling.

---

### **6.3 Survival Modelling**
Methods applied:
- Kaplan–Meier survival curves  
- KM comparison by arm  
- Log-Rank test  
- Cox PH model  
- Schoenfeld residual checks

---

## **7️⃣ Python Implementation Structure** 💻

.
├── data/
│ ├── Chlorhexidine Trials.xlsx
│ ├── Data_Dictionary.png
│ ├── Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf
│ ├── Raw Data from Chlorhexidine Trial.xlsx
│
├── results/
│ ├── cox_ph.png
│ ├── cox_summary.png
│ ├── km_by_arm.png
│ ├── km_overall.png
│ ├── ph_TLCD1.png
│ ├── ph_Trial_arm.png
│ ├── ph_age.png
│ ├── ph_apache2.png
│ ├── ph_gender.png
│
├── Chlorhexidine_Trials.ipynb
├── LICENSE
├── README.md

---


---

## **8️⃣ Key Visualizations** 📊

- Life Tables (overall and per-arm)  
- Overall Kaplan–Meier survival curve  
- Stratified KM curves with CI  
- Schoenfeld residual plots  
- Forest-style hazard ratio summary  

---

## **9️⃣ Results & Interpretation** 🧾

### **1. Kaplan–Meier Survival (Overall)**  
<div align="center">
  <img src="results/km_overall.png" width="600">
</div>

VAP-free survival remained above **90%** throughout the 10-day observation. Most patients remained event-free.

---

### **2. Kaplan–Meier by Trial Arm**  
<div align="center">
  <img src="results/km_by_arm.png" width="600">
</div>

- Arm 1 showed slightly more drops in survival (events = 7)  
- Arm 2 appeared flatter with fewer events (events = 2)  
- Visual difference exists, but statistical testing is required.

---

### **3. Log-Rank Test**  
- **p = 0.94**  
- No statistically significant difference between treatment arms.  
- Similar timing of events results in overlapping curves.

---

### **4. Cox Proportional Hazards Model**  
<div align="center">
  <img src="results/cox_summary.png" width="600">
</div>

- TrialArm HR = **0.97**, p = 0.97 → no measurable hazard difference  
- Age, APACHEII, TLC_D1, Gender all have HR ≈ 1.0  
- Model concordance = 0.59

---

### **5. PH Assumption Checks**  
<div align="center">
  <img src="results/cox_ph.png" width="600">
</div>

- All variables show **p > 0.05**  
- No evidence of PH violation  
- Cox model assumptions are valid

---

### **Selected Summary**
- **Day-5 survival:** Arm1 ≈ 0.919 | Arm2 ≈ 0.902  
- **Events:** Arm1 = 6 | Arm2 = 4  
- **TrialArm HR:** 0.97  

---

## **🔟 Discussion** 💬

Both chlorhexidine concentrations demonstrated consistently high VAP-free survival. While 0.20% had fewer raw VAP events, the time-to-event pattern was similar, and formal tests (Log-Rank, Cox PH) did not indicate a statistically significant difference.

All hazard ratios were stable and close to 1.0, and PH checks confirmed that predictor effects remained constant over time. Clinically, these findings align with the understanding that chlorhexidine supports oral hygiene and helps maintain a low VAP incidence, with both concentrations performing effectively.

Survival modelling provided structured insights into timing, hazard behaviour and treatment comparison beyond simple event counts.

---

## **1️⃣1️⃣ Conclusion** ✅

- Both chlorhexidine concentrations provided strong VAP prevention during the observation period.  
- 0.20% showed fewer events numerically, but survival analysis did not demonstrate statistical superiority.  
- Baseline variables (Age, APACHEII, TLC_D1, Gender, TrialArm) were not strong predictors of VAP risk.  
- Survival analysis remains valuable for evaluating treatment performance and informing clinical decisions.

---

## **1️⃣2️⃣ Future Work** 🔭

Future extensions:

- Time-varying covariates (daily TLC or microbial load)  
- Parametric survival models (Weibull, exponential)  
- Machine-learning models (Random Survival Forests, DeepSurv)  
- External validation using ICU datasets (MIMIC)  
- Competing-risk modelling (VAP vs death)

---

### **Contact / Citation**
- Original paper: *Nagesh Vyas, Priya Mathur, Shailesh Jhawar, Akash Prabhune, Pradeep Vimal (2021).*
- Notebook: `Chlorhexidine_Trials.ipynb`  
- Case study PDF: `/data/Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf`

---

**End of README**


## **7️⃣ Python Implementation Structure** 💻

