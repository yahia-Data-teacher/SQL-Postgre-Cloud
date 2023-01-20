# CASE Statements

### 5.1 Categorizing Wind Speed

You can use a `CASE` statement to turn a column value into another value based on conditions. For instance, we can turn different `wind_speed` ranges into `HIGH`, `MODERATE`, and `LOW` categories.

```sql
SELECT report_code, year, month, day, wind_speed,

CASE
   WHEN wind_speed >= 40 THEN 'HIGH'
   WHEN wind_speed >= 30 THEN 'MODERATE'
   WHEN wind_speed >= 0 THEN 'LOW'
   ELSE 'N/A'
END as wind_severity

FROM station_data
ORDER by wind_speed DESC;
```

### 5.2 More Efficient Way To Categorize Wind Speed

We can actually omit `AND wind_speed < 40` from the previous example because each `WHEN`/`THEN` is evaluated from top-to-bottom. The first one it finds to be true is the one it will go with, and stop evaluating subsequent conditions.

```sql
SELECT report_code, year, month, day, wind_speed,

CASE
   WHEN wind_speed >= 40 THEN 'HIGH'
   WHEN wind_speed >= 30 THEN 'MODERATE'
   ELSE 'LOW'
END as wind_severity

FROM station_data
```

### 5.3 Using CASE with GROUP BY

We can use `GROUP BY` in conjunction with a `CASE` statement to slice data in more ways, such as getting the record count by `wind_severity`.

```sql
SELECT 

CASE
   WHEN wind_speed >= 40 THEN 'HIGH'
   WHEN wind_speed >= 30 THEN 'MODERATE'
   WHEN wind_speed >= 0 THEN 'LOW'
   ELSE 'N/A'
END AS wind_severity,
COUNT(*)  AS record_count
FROM station_data
GROUP BY wind_severity;
```

Also, some wind_speed values are NULL, so without an `ELSE` any records that do not meet a condition will turn out to be NULL. 

```sql 
SELECT 

CASE
   WHEN wind_speed >= 40 THEN 'HIGH'
   WHEN wind_speed >= 30 THEN 'MODERATE'
   WHEN wind_speed >= 0 THEN 'LOW'
 
END AS wind_severity,
COUNT(*)  AS record_count
FROM station_data
GROUP BY wind_severity;
```

### 5.4 "Zero/Null" Case Trick

There is really no way to create multiple aggregations with different conditions unless you know a trick with the `CASE` statement. If you want to find two total precipitation, with and without tornado precipitations, for each year and month, you have to do separate queries.

**Tornado Precipitation**
```sql
SELECT year, month,
SUM(precipitation) as tornado_precipitation
FROM station_data
WHERE tornado = 1
AND year >= 1990
GROUP BY year, month
```

**Non-Tornado Precipitation**
```sql
SELECT year, month,
SUM(precipitation) as non_tornado_precipitation
FROM station_data
WHERE tornado = 0
AND year >= 1990
GROUP BY year, month
```

But you can use a single query using a `CASE` statement that sets a value to 0 if the condition is not met. That way it will not impact the sum.

```sql
SELECT year, month,
SUM(CASE WHEN tornado = 1 THEN precipitation ELSE 0 END) as tornado_precipitation,
SUM(CASE WHEN tornado = 0 THEN precipitation ELSE 0 END) as non_tornado_precipitation

FROM station_data
WHERE year >= 1990

GROUP BY year, month
```

Many folks who are not aware of the zero/null case trick will resort to derived tables (not covered in this class but covered in _Advanced SQL for Data Analysis_), which adds an unnecessary amount of effort and mess.

```sql
SELECT t.year,
t.month,
t.tornado_precipitation,
non_t.non_tornado_precipitation

FROM (
    SELECT year, month,
    SUM(precipitation) as tornado_precipitation
    FROM station_data
    WHERE tornado = 1
    AND year >= 1990
    GROUP BY year, month
) t

INNER JOIN

(
    SELECT year, month,
    SUM(precipitation) as non_tornado_precipitation
    FROM station_data
    WHERE tornado = 0
    AND year >= 1990
    GROUP BY year, month
) non_t
```

### 5.5 Using Null in a CASE to conditionalize MIN/MAX

Since `NULL` is ignored in SUM, MIN, MAX, and other aggregate functions, you can use it in a `CASE` statement to conditionally control whether or not a value should be included in that aggregation.

For instance, we can split up max precipitation when a tornado was present vs not present.

```sql
SELECT year,
MAX(CASE WHEN tornado = 0 THEN precipitation ELSE NULL END) as max_non_tornado_precipitation,
MAX(CASE WHEN tornado = 1 THEN precipitation ELSE NULL END) as max_tornado_precipitation
FROM station_data
WHERE year >= 1990
GROUP BY year
```

*Switch to slides for exercise*


### Exercise 5.1

SELECT  the report_code, year, quarter, and temperature, where a “quarter” is “Q1”, “Q2”, “Q3”, or “Q4” reflecting months 1-3, 4-6, 7-9, and 10-12 respectively.

**ANSWER:**

```sql
SELECT

report_code,
year,

CASE
    WHEN month BETWEEN 1 and 3 THEN 'Q1'
    WHEN month BETWEEN 4 and 6 THEN 'Q2'
    WHEN month BETWEEN 7 and 9 THEN 'Q3'
    WHEN month BETWEEN 10 and 12 THEN 'Q4'
END as quarter,

temperature

FROM STATION_DATA
```

### Exercise 5.2

Get the average temperature by quarter and month, where a “quarter” is “Q1”, “Q2”, “Q3”, or “Q4” reflecting months 1-3, 4-6, 7-9, and 10-12 respectively.

**ANSWER**

```sql
SELECT
year,

CASE
    WHEN month BETWEEN 1 and 3 THEN 'Q1'
    WHEN month BETWEEN 4 and 6 THEN 'Q2'
    WHEN month BETWEEN 7 and 9 THEN 'Q3'
    WHEN month BETWEEN 10 and 12 THEN 'Q4'
END as quarter,

AVG(temperature) as avg_temp

FROM STATION_DATA
GROUP BY 1,2
```
