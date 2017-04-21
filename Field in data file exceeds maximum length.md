# Field in data file exceeds maximum length
## Symptom
When SQL Loader a field DESC_COLUMN with around 400 characters. SQL Loader prompt error Field in data file exceeds maximum length though data type defined in table is varchar2(4000).
## Analyze
The default datatype in SQLLDR is char(255). Simply code:
```SQLLDR
DESC_COLUMN CHAR(4000) NULLIF DESC_COLUMN=BLANKS
```
so that SQLLDR can allocate enough buffer to hold it.
