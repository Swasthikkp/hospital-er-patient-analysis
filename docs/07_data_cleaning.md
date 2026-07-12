# Data Cleaning Steps

Applied in Power Query before modeling, and reproduced independently in pandas for `data/cleaned/Manasa_Nursing_Home_ER_Cleaned.csv` (see note below):

1. Removed the duplicate `Patient Admission Flag.1` column (exact copy of `Patient Admission Flag`).
2. Standardized `Patient Gender` values — `Male` → `M`, `Female` → `F` (46 rows had the long form).
3. Filled blank `Department Referral` with `"None"` to represent ER-only visits with no specialist referral (5,400 rows / ~58.6% of records).
4. Parsed `Patient Admission Date` from text (`DD-MM-YYYY HH:MM`) into a proper datetime.
5. Trimmed stray whitespace on all text columns.
6. Derived `Age Group` and `Patient Attend Status` columns using the DAX logic in [`06_dax_formulas.md`](06_dax_formulas.md).
7. Left `Patient Satisfaction Score` nulls (6,699 rows / ~72.7%) untouched rather than imputed — satisfaction was only captured for a subset of visits, and filling it would distort the KPI.

> **Note:** The `.xlsx` file cleans and models the data inside Excel via Power Query — there's no separate cleaned CSV exported from it. The `data/cleaned/` file in this repo is an independent pandas reproduction of the same cleaning logic, provided so the transformation steps are transparent and reviewable without opening Excel.
