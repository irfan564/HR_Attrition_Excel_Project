# Formulas used (explained)

**Helper columns on the Data sheet**
- LeftFlag: `=IF(Attrition="Yes",1,0)` turns Yes/No into 1/0 so leavers can be summed.
- AgeBand / TenureBand: nested `IF` tests, each band checked from lowest to highest.
- IncomeBand: nested `IF` against quartile cut-offs on the Settings sheet (`=QUARTILE(MonthlyIncome range, 1/2/3)`).
- LowSatFlag: `=IF(OR(JobSatisfaction<=2, WorkLifeBalance<=2),"Yes","No")`.

**KPIs**
- Employees: `=COUNTA(EmployeeNumber range)`
- Leavers: `=SUM(LeftFlag range)`
- Attrition rate: leavers / employees
- Average income of leavers: `=AVERAGEIFS(MonthlyIncome, Attrition, "Yes")`

**Analysis tables**
- Headcount: `=COUNTIFS(field range, group)`
- Leavers: `=SUMIFS(LeftFlag range, field range, group)`
- Rate: `=IFERROR(leavers/headcount, 0)` (IFERROR avoids a divide-by-zero error)
- Gap vs company: group rate minus company rate

**Dashboard**
- Department explorer: `=INDEX(column, MATCH(selected department, department list, 0))` (a lookup, like XLOOKUP but works in every Excel version).
- Key findings: text built with `&` and `TEXT(value,"0.0%")`; highest and lowest groups use `MAX`/`MIN` with `INDEX`/`MATCH`.
