# DAX Formulas

### DAX Formula for Age Group

```dax
=IF([Patient Age]>=70,"70-79",
IF([Patient Age]>=60,"60-69",
IF([Patient Age]>=45,"45-59",
IF([Patient Age]>=30,"30-44",
IF([Patient Age]>=15,"15-29",
IF([Patient Age]>=5,"05-14","0-4"))))))
```

### DAX Formula for Patient Attend Status

```dax
=IF([Patient Waittime]<30,"Within Time","Delay")
```

---

### Other Measures Used in the Data Model

| Measure | Logic | Purpose |
|---|---|---|
| Number of Patients | `DISTINCTCOUNT([Patient Id])` | Daily/period patient volume KPI |
| Average Wait Time | `AVERAGE([Patient Waittime])` | Average minutes to be seen |
| Patient Satisfaction Score | `AVERAGE([Patient Satisfaction Score])` | Average service quality rating (0–10) |
| Admitted vs Not Admitted | `COUNTROWS(FILTER(...))` on `[Patient Admission Flag]` | Admission Status chart |
| % Within Time / % Delay | `DIVIDE(count of status, [Number of Patients])` | Timeliness KPI |
| Patients by Department Referral | `COUNTROWS` grouped by `[Department Referral]` | Referral load chart |
| Patients by Gender | `COUNTROWS` grouped by `[Patient Gender]` | Gender split donut |
