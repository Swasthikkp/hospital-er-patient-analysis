# 🏥 Manasa Nursing Home — Emergency Room Patient Analysis Dashboard

An end-to-end Power BI-style analytics project (built in Excel Power Query + Power Pivot) analyzing two years of Emergency Room visits for **Manasa Nursing Home**, a fictional Karnataka-based hospital adapted from a standard "Hospital Emergency Room Patients" analysis template for local, native context (patient names, community/religion field, and hospital branding localized to Karnataka).

![Dashboard](docs/screenshots/dashboard.png)

---

## 📌 Purpose

We need to create a Hospital Emergency Room Analysis Dashboard to improve efficiency and provide useful insights, helping stakeholders monitor, analyze, and make better decisions for managing patients and improving services.

Full detail: [`docs/02_purpose_of_project.md`](docs/02_purpose_of_project.md)

---

## 🛠️ Tools Used

- **Microsoft Excel** — Power Query (ETL/data cleaning), Power Pivot (data modeling), DAX (calculated columns & measures)
- **Python (pandas)** — independent data-cleaning reproduction and statistical validation
- **GitHub** — version control & project documentation

---

## 🔁 Project Workflow

Executed as a structured pipeline from requirement gathering through to insight generation. Full breakdown: [`docs/01_project_steps.md`](docs/01_project_steps.md)

Business Requirement Gathering → Understanding of Data → Data Connection (Power Query) → Data Cleaning & Quality Check → Creating Calendar Table → Data Modeling (Power Pivot) → Adding Required Columns (DAX) → Creating Pivots & Dashboard Layout → Charts Development & Formatting → Dashboard/Report Development → Insights Generation.

---

## 📋 KPIs & Charts

- **Number of Patients**, **Average Wait Time**, and **Patient Satisfaction Score** — each as a card with a daily area sparkline. Full spec: [`docs/03_kpi_requirements.md`](docs/03_kpi_requirements.md)
- **Charts:** Patient Admission Status, Patient Age Distribution, Timeliness (% seen within 30 min), Gender Analysis, Department Referrals. Full spec: [`docs/04_charts_to_create.md`](docs/04_charts_to_create.md)

---

## 🧮 Data Modeling — Calendar Table & DAX

- Calendar table formula (Power Query): [`docs/05_calendar_table_formula.md`](docs/05_calendar_table_formula.md)
- Age Group, Patient Attend Status, and all core measures (DAX): [`docs/06_dax_formulas.md`](docs/06_dax_formulas.md)
- Full data cleaning steps (Power Query + pandas reproduction): [`docs/07_data_cleaning.md`](docs/07_data_cleaning.md)

---

## 🗂️ Repository Structure

```
manasa-nursing-home-er-analysis/
├── README.md
├── dashboard/
│   └── Hospital_Emergency_Room_Patients_Analysis.xlsx   # Power Query + Power Pivot + Dashboard
├── data/
│   ├── raw/
│   │   └── Manasa_Nursing_Home_ER_Uncleaned.csv          # Original, uncleaned export
│   └── cleaned/
│       └── Manasa_Nursing_Home_ER_Cleaned.csv            # Cleaned + feature-engineered (pandas)
└── docs/
    ├── 01_project_steps.md
    ├── 02_purpose_of_project.md
    ├── 03_kpi_requirements.md
    ├── 04_charts_to_create.md
    ├── 05_calendar_table_formula.md
    ├── 06_dax_formulas.md
    ├── 07_data_cleaning.md
    └── screenshots/
        └── dashboard.png                                  # Final dashboard result
```

---

## 🧹 Data Cleaning Summary

| Issue | Detail | Fix |
|---|---|---|
| Duplicate column | `Patient Admission Flag.1` was an exact copy of `Patient Admission Flag` | Dropped |
| Inconsistent gender labels | 46 rows used `Male`/`Female` instead of `M`/`F` | Standardized to `M`/`F` |
| Missing department referral | 5,400 of 9,216 rows (~58.6%) blank | Filled as `"None"` (ER-only visit, no specialist referral) |
| Text dates | `Patient Admission Date` stored as text (`DD-MM-YYYY HH:MM`) | Parsed to datetime |
| Missing satisfaction scores | 6,699 of 9,216 rows (~72.7%) blank | **Left as null** — not imputed, to avoid distorting the KPI |
| Derived fields | Age band and timeliness flag needed for charts | Added `Age Group` and `Patient Attend Status` columns |

Full details: [`docs/07_data_cleaning.md`](docs/07_data_cleaning.md)

---

## 💡 Key Insights

- **Timeliness is the biggest operational gap.** Only **38.3%** of patients were seen within the 30-minute target — **61.7% experienced a delay**. This is the single most actionable finding in the dataset.
- **Admissions are a near-even split** — 50.0% admitted vs. 50.0% not admitted — meaning roughly half of ER visits are being handled and discharged without inpatient admission.
- **Satisfaction data is thin and mediocre.** Only ~27% of visits (2,517 of 9,216) have a captured satisfaction score, and the average sits at **4.99 / 10** — a middling score even before accounting for the ~73% of visits with no feedback at all.
- **Delayed patients report lower satisfaction** — 4.93/10 vs. 5.10/10 for patients seen within time — confirming wait time is a direct driver of perceived service quality.
- **~59% of ER volume never involves a specialist referral** (5,400 "None" cases, on top of General Practice's 1,840), suggesting a large share of visits may be lower-acuity, primary-care-level cases sitting in the same queue as urgent cases.
- **Renal referrals are small in volume (86) but high in acuity** — highest admission rate (53.5%) and *lowest* satisfaction (4.57/10) of any department, flagging it as a small but high-friction group.
- **Gastroenterology has the highest satisfaction** (5.80/10) despite one of the longer average wait times (35.8 min) — worth studying what that department does differently in patient communication/experience.
- **Patient demographics are broad, not concentrated** — near-even gender split (51% M / 49% F) and a fairly flat age distribution across all bands (0–79), so improvements need to be system-wide rather than targeted at one demographic.
- **Arrival volume is close to flat across months and hours of the day** in this dataset — real-world EDs typically show clear evening/weekend peaks, so this is worth flagging as a synthetic-data characteristic rather than a genuine "no rush hour" finding once this template is applied to real hospital data.

---

## 🚀 Recommendations for the Hospital

1. **Introduce a fast-track / low-acuity lane** for the ~59% of visits with no specialist referral, so they don't compete for the same queue slots as urgent, referral-bound cases — the highest-leverage fix for the 61.7% delay rate.
2. **Set and track a weekly "% seen within 30 minutes" target**, drilling into which days/shifts drive the delays rather than treating it as a single static number.
3. **Expand satisfaction survey capture.** With only 27% response coverage, the satisfaction KPI isn't representative — a simple post-visit prompt (SMS/kiosk) would make this metric trustworthy enough to act on.
4. **Prioritize service-quality review in Renal and Orthopedics** — both combine high patient volume/acuity with below-average satisfaction, so small process fixes there (communication, wait transparency) will have outsized impact.
5. **Treat wait-time reduction as the primary satisfaction lever** — since delay correlates directly with lower scores, these don't need to be run as two separate initiatives.

## 🔧 Possible Extensions to This Project

- Add a rolling 7-day average trend line for wait time and satisfaction to smooth daily noise.
- Add a "Satisfaction Response Rate" KPI card so viewers can see how much of the satisfaction number is backed by actual data vs. missing.
- Add drill-through from the department referral chart to a patient-level detail table.
- Once applied to real hospital data, add an hour-of-day / day-of-week heatmap to support shift staffing decisions.

---

## 👤 Author

**Swasthik K P**
📧 kpswasthik2004@gmail.com · [LinkedIn](https://linkedin.com/in/swasthik-k-p-7b927b377) · [GitHub](https://github.com/Swasthikkp)

*Note: This project uses a synthetic dataset localized with Karnataka-context names, community/religion fields, and hospital branding for portfolio purposes. It does not represent a real patient population or real hospital.*
