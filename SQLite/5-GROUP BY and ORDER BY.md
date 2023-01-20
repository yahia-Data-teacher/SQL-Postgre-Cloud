# 4.GROUP BY and ORDER BY


### 4.1: Getting a count of records

```sql
SELECT count(*) as record_count FROM station_data
```

### 4.2 Getting a count of records with a condition

```sql
SELECT count(*) as record_count FROM station_data
WHERE tornado = 1
```

### 4.3 Getting a count by year

```sql
SELECT year, count(*) as record_count
FROM station_data
WHERE tornado = 1
GROUP BY year
```

### 4.4 Getting a count by year, month

```sql
SELECT year, month, count(*) as record_count
FROM station_data
WHERE tornado = 1
GROUP BY year, month
```

### 4.5 Getting a count by year, month with ordinal index

```sql
SELECT year, month, count(*) as record_count
FROM station_data
WHERE tornado = 1
GROUP BY 1, 2
```

### 4.6 Using ORDER BY

```sql
SELECT year, month, count(*) as record_count
FROM station_data
WHERE tornado = 1
GROUP BY year, month
ORDER BY year, month
```

### 4.7 Using ORDER BY with DESC

```sql
SELECT year, month, count(*) as record_count
FROM station_data
WHERE tornado = 1
GROUP BY year, month
ORDER BY year DESC, month
```

### 4.8 Counting non-null values

```sql
SELECT COUNT(snow_depth) as recorded_snow_depth_count
FROM station_data
```

### 4.9 Average temperature by month since year 2000

```sql
SELECT month, AVG(temperature) as avg_temp
FROM station_data
WHERE year >= 2000
GROUP BY month
```

### 4.10 Average temperature (with rounding) by month since year 2000


```sql
SELECT month, round(AVG(temperature),2) as avg_temp
FROM station_data
WHERE year >= 2000
GROUP BY month
```

### 4.11 Sum of snow depth

```sql
SELECT year, SUM(snow_depth) as total_snow
FROM station_data
WHERE year >= 2005
GROUP BY year
```

### 4.12 Multiple aggregations

```sql
SELECT year,
SUM(snow_depth) as total_snow,
SUM(precipitation) as total_precipitation,
MAX(precipitation) as max_precipitation

FROM station_data
WHERE year >= 2005
GROUP BY year
```

### EXERCISES
Flip to slides


### 4.13 Using HAVING

You cannot use WHERE on aggregations. This will result in an error.

```sql
SELECT year,
SUM(precipitation) as total_precipitation
FROM station_data
WHERE total_precipitation > 30
GROUP BY year
```

You can however, use HAVING.

```sql
SELECT year,
SUM(precipitation) as total_precipitation
FROM station_data
GROUP BY year
HAVING total_precipitation > 30
```




### 4.14 Getting Distinct values

You can get DISTINCT values for one or more columns

```sql
SELECT DISTINCT station_number FROM station_data
```

You can also get distinct combinations of values for multiple columns

```sql
SELECT DISTINCT station_number, year FROM station_data
```
