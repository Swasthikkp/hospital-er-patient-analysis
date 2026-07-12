# Data Cleaning Steps (Power Query)

Cleaning and quality checks were performed inside Excel using **Power Query**, before the data was loaded into the Power Pivot model. This mirrors the "Data Cleaning and Data Quality Check Using Power Query" step in the project workflow.

Steps applied to `data/raw/Manasa_Nursing_Home_ER_Uncleaned.csv`:

1. Removed the duplicate `Patient Admission Flag.1` column (exact copy of `Patient Admission Flag`).
2. Standardized inconsistent `Patient Gender` values (`Male`/`Female` entries mixed in with `M`/`F`) to a single format.
3. Handled blank `Department Referral` values, representing ER-only visits with no specialist referral.
4. Converted `Patient Admission Date` from text into a proper date/time type.
5. Trimmed stray whitespace on text columns.
6. Added the `Age Group` and `Patient Attend Status` calculated columns (see [`06_dax_formulas.md`](06_dax_formulas.md)) for use in the age distribution and timeliness charts.

The cleaned, modeled result lives inside the Power Query/Power Pivot layer of `dashboard/Hospital_Emergency_Room_Patients_Analysis.xlsx` — open the file and check the Queries pane to see every step as an auditable list of applied transformations.
