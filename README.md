# **Survival Analysis of Chlorhexidine Trial Outcomes Using Python** 🧪📈

This project is based on a real clinical trial case study titled  
**“Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash with 0.12 percent and 0.2 percent Concentration on Incidence of VAP”**  
published in *Annals of International Medical and Dental Research, Vol (7), Issue (3) 2021*.  
The complete article is included in this repository as **Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf**.  
(If needed locally use: `/data/Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf`)

This repository reproduces and interprets **time-to-VAP (Ventilator-Associated Pneumonia)** outcomes using classical Survival Analysis methods in Python. All results, tables, and plots are generated via the **Chlorhexidine_Trials.ipynb** / .

---

## **1️⃣ Project Title**  
**Survival Analysis of Chlorhexidine Trial Outcomes Using Python**

---

## **2️⃣ Project Summary** ✍️

This project analyses patient-level data from a randomized controlled trial comparing **0.12% vs 0.20% chlorhexidine** mouthwash for preventing Ventilator-Associated Pneumonia (VAP) in mechanically ventilated ICU patients.

- **Outcome:** time (days) until VAP (event = 1) with censoring for discharge, death, or LAMA (event = 0).  
- **Why survival analysis:** follow-up times vary and many patients are censored, so time-to-event methods are required.  
- **Learning outcomes:** Kaplan–Meier estimation, Log-Rank test, Cox Proportional Hazards modelling, Schoenfeld residuals, and clinical interpretation.

---

## **3️⃣ Dataset Description** 📚

- **Source:** Hospital-based randomized controlled trial, 140 patients randomized to two arms (0.12% vs 0.20% chlorhexidine).  
- **Working data:** cleaned dataset derived from `Raw Data form Chlorhexidine Trial.xlsx`.

### **Core variables**
| Column | Description | Type |
| ------ | ----------- | ---- |
| Age | Age in years | Continuous |
| Gender | Male / Female | Categorical |
| TrialArm_num | 1 = 0.12%, 2 = 0.20% | Categorical |
| APACHEII | Severity score | Continuous |
| TLC_D1 | Day-1 leukocyte count | Continuous |
| time | Time to VAP / censor | Continuous |
| event | 1 = VAP, 0 = NO VAP | Binary |

---

## **4️⃣ Problem Statement** ❓

Key clinical questions this project answers:

1. Does chlorhexidine 0.20% reduce the hazard of developing VAP compared to 0.12%?  
2. Is VAP-free survival different between the two treatment arms?  
3. Do baseline predictors — Age, APACHE II, TLC Day 1, Gender — influence time to VAP?  
4. Do survival curves differ by arm when tested with the Log-Rank test?  
5. What is the clinical interpretation of hazard ratios from a Cox PH model?

---

## **5️⃣ Objectives** 🎯

1. Data cleaning and preprocessing  
2. Exploratory Data Analysis (EDA) and baseline summary statistics  
3. Estimate survival curves (Kaplan–Meier) overall and by arm  
4. Compare groups using the Log-Rank test  
5. Fit a Cox Proportional Hazards model and report hazard ratios  
6. Check proportional hazards assumptions (Schoenfeld residuals)  
7. Produce clear visualizations and clinical interpretation

---

## **6️⃣ Methodology** 🛠️

### **6.1 Data Preparation**
- Column names cleaned (e.g., `APACHE II Score` → `APACHEII`, `TLC Day 1` → `TLC_D1`).  
- Encoded `TrialArm` and `Gender` to numeric/dummies for modelling.  
- Ensured `time` and `event` are numeric and suitable for survival objects.  
- **Model variables used:** `time`, `event`, `Age`, `APACHEII`, `TLC_D1`, `TrialArm_num`, `Gender_binary`.

**Handling missing values**  
- Missing values in `APACHEII` and `TLC_D1` were imputed using the **median** of each column.  
- Median was chosen because it is robust to outliers and preserves central tendency for skewed clinical measures.

---

### **6.2 Exploratory Data Analysis (EDA)** 🔍

The exploratory steps performed in the analysis include:

**Baseline summary**
- Total N = 106 (after dataset filtering), Events (VAP) = 10  
- Mean Age ≈ 47.6 (SD 17.3)  
- APACHEII mean ≈ 16.9 (SD 6.5)  
- TLC Day1 mean ≈ 15,216 (SD 7,270)  
- Arm1 n = 61, Arm2 n = 45  
- Male n = 93, Female n = 13  
- Mean follow-up time ≈ 5.7 days

**Visual exploration**
- **1. Age Distribution (Histogram)** – wide adult range, no extreme clustering.  
- **2. APACHE II Score Distribution (Histogram)** – most patients between 10–20.  
- **3. TLC Day 1 (Boxplot)** – elevated white cell counts with some high-value outliers, central tendency consistent with ICU inflammatory response.  

**Life tables**
- Life tables computed overall and per-arm show that early time points have few events; events appear mostly between days 5–10. Arm 1 shows slightly higher cumulative hazard vs Arm 2.

**Event / Censoring structure**
- The dataset contains many censored observations (discharge, LAMA, death), which is expected for ICU treatment episodes.

**Survival visual checks**
- Kaplan–Meier curves (overall and by arm) with confidence intervals were plotted as part of EDA.

Purpose: confirm data structure, variable distributions, and readiness for survival modelling.

---

### **6.3 Survival Modelling**
Applied methods:
- Overall Kaplan–Meier survival curve  
- KM curves stratified by treatment arm  
- Log-Rank test (Arm 1 vs Arm 2)  
- Cox Proportional Hazards model (multivariable)  
- Schoenfeld residuals and PH assumption checks

---

## **7️⃣ Python Implementation Structure** 💻

.
├── data/
│   ├── Chlorhexidine Trials.xlsx
│   ├── Data_Dictionary.png
│   ├── Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf
│   ├── Raw Data from Chlorhexidine Trial.xlsx
│
├── results/
│   ├── cox_ph.png
│   ├── cox_summary.png
│   ├── km_by_arm.png
│   ├── km_overall.png
│   ├── ph_TLCD1.png
│   ├── ph_Trial_arm.png
│   ├── ph_age.png
│   ├── ph_apache2.png
│   ├── ph_gender.png
│
├── Chlorhexidine_Trials.ipynb
├── LICENSE
├── README.md


---

## **8️⃣ Key Visualizations** 📊

- Life tables (overall and per-arm)  
- Overall Kaplan–Meier survival curve  
- Kaplan–Meier curves by treatment arm (with CI)  
- Schoenfeld residual plots for PH checks  
- Forest-style table of hazard ratios

---

## **9️⃣ Results & Interpretation** 🧾

### **1. Kaplan–Meier Survival (Overall)**  
<div align="center">
  <img src="results/km_overall.png" width="600" alt="Overall KM">
</div>

Overall VAP-free survival remains high (≈ >90%) over the observed follow-up (≤10 days). Most patients remain event-free.

---

### **2. Kaplan–Meier by Trial Arm**  
<div align="center">
  <img src="results/km_by_arm.png" width="600" alt="KM by arm">
</div>

- Arm 1 (0.12%): more drops in the curve (raw events = 7)  
- Arm 2 (0.20%): flatter curve (raw events = 2)  
- Visual trend favors 0.20%, but statistical tests are needed for confirmation.

---

### **3. Log-Rank Test**  
- **p = 0.94** — no statistical difference in time-to-VAP between arms.  
- Explanation: low number of events and similar timing lead KM curves to overlap despite count differences.

---

### **4. Cox Proportional Hazards (Multivariable)**  
<div align="center">
  <img src="results/cox_summary.png" width="600" alt="Cox summary">
</div>

- Model: N = 106, Events = 10  
- **TrialArm HR = 0.97 (p = 0.97)** → no detectable hazard difference between 0.12% and 0.20%.  
- Other variables (Age, APACHEII, TLC_D1, Gender) have HRs near 1.0 and are not significant (p > 0.45).  
- Model concordance ≈ 0.59 (slightly better than chance).

**Bottom line:** No statistically significant predictors of VAP in the fitted model.

---

### **5. Proportional Hazards Assumption**  
<div align="center">
  <img src="results/cox_ph.png" width="600" alt="PH checks">
</div>

- Schoenfeld residuals were examined for each covariate.  
- **All variables show p > 0.05** in PH tests — no evidence of PH violation.  
- The Cox model assumptions are therefore acceptable.

---

### **Summary Table (Selected)**

- **Survival @ Day 5:** Arm1 ≈ 0.919 | Arm2 ≈ 0.902  
- **Events (VAP):** Arm1 = 6 | Arm2 = 4 (counts after dataset filtering)  
- **Cox TrialArm HR:** 0.97 (no meaningful effect)

---

## **🔟 Discussion** 💬

The analysis provides a practical view of VAP risk over the observed period. Both chlorhexidine concentrations maintained high VAP-free survival. While the 0.20% arm shows fewer raw VAP events, time-to-event patterns and survival curves are similar, and the formal tests (Log-Rank and Cox) do not show a statistically significant difference.

The Cox model reports hazard ratios close to 1 for all baseline variables, and Schoenfeld residuals confirm stable effects over time. These results are in line with clinical expectations that chlorhexidine supports oral hygiene and contributes to maintaining low VAP incidence; in this dataset, both strengths perform similarly when considering time-to-event patterns.

Survival modelling helped quantify timing, hazards, and group comparisons beyond raw counts, offering a structured interpretation of treatment effect and patient trajectories.

---

## **1️⃣1️⃣ Conclusion** ✅

- Both chlorhexidine strengths support good VAP-free survival during the observation window.  
- The 0.20% arm shows fewer raw VAP events; however, survival analysis (KM, log-rank, Cox) does not demonstrate a statistically significant improvement in time-to-VAP.  
- No single baseline predictor (Age, APACHE II, TLC Day 1, Gender, TrialArm) emerged as a strong determinant of time-to-VAP in the fitted model.  
- Survival models are valuable for assessing treatment performance over time and for informing clinical interpretation.

---

## **1️⃣2️⃣ Future Work** 🔭

Potential next steps to expand the analysis:

- Add time-varying covariates (daily microbial load, TLC).  
- Fit parametric survival models (Weibull, exponential) for alternative inference.  
- Try machine-learning survival methods (Random Survival Forests, DeepSurv).  
- Validate findings on external ICU datasets (eg. MIMIC).  
- Consider competing-risk frameworks (VAP vs death).

---

### Contact / Citation
- Original trial paper: *Nagesh Vyas, Priya Mathur, Shailesh Jhawar, Akash Prabhune, Pradeep Vimal (2021).*  
- script: `Chlorhexidine_Trials.ipynb` 
- Case study PDF local path : `/data/Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash.pdf`

---

**End of README**
