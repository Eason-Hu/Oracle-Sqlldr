# SQLLDR data to column starts with digit
## Symptom
ORA-00907 will be prompt when sqlldr data to a table whose column name starts with digit.
> ORA-00907: missing right parenthesis

## Analyze
> https://www.experts-exchange.com/questions/26394655/ORA-00907-Error-while-loading-data-into-table-using-sqlldr.html

I believe this is a 'feature/bug' in SQL*Loader. Oracle really doesn't support column names starting with a number.

You got around that by using double quotes on the column name. This also forces the column into being case-sensitive. Everywhere you will EVER use that column_name you will always need to supply the double quotes.

I don't think sql*Loader was ever designed to handle this. I've tried every 'trick' I can think of to get it working and cannot find a way around it.

I strongly encourage you to change the column name to start with a letter and remove the double quotes.

If you still want to move ahead with that column name, you should open an SR with Oracle to see if they can get it working.

## Solution
Use boundfiller function introduced after Oracle 9i
```sqlldr
(
  col1        "decode(trim(:col1), 'N A.', NULL, trim(:col1))" ,
  field2      boundfiller,
  col3        "decode(trim(:col3), 'N A', NULL, trim(REGEXP_REPLACE(:col3 , ',', '')))",
  "144A_col2" "decode(trim(:field2), 'N A.', NULL, trim(:field2))"
)
```
