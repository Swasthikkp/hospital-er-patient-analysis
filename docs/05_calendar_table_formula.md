# Calendar Table Formula

An independent date table was created in Power Query, then loaded into the data model and marked as a Date Table to support time intelligence (daily trend sparklines on all three KPIs).

```
= List.Dates(#date(2023,01,01), 731, #duration(1,0,0,0))
```

- **Start date:** `01-01-2023`
- **Number of dates:** `731` (2 full years)
- **Step:** `1 day`
