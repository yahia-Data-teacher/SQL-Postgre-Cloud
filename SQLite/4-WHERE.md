## Dans cette partie nous allons travailler avec la base de données :  weather_stations.db



- ### Sélectionner la base de donnée  weather_stations.db sur BDHub.io .

- ### Double cliquer sur weather_stations.db > visualise


![a](https://user-images.githubusercontent.com/78825764/213731610-a6216cd3-60f9-407a-b320-f8ebac7ff753.jpg)

- ### Voilà ! C'est ici où vous allez éxecuter les requetes de cette partie .

# 3.WHERE

### 3.1: Getting year 2010 records

```sql
SELECT * FROM station_data
WHERE year = 2010;
```

### 3.2: Getting non-2010 records

```sql
SELECT * FROM station_data
WHERE year != 2010;
```

```sql
SELECT * FROM station_data
WHERE year <> 2010;
```

### 3.3: Getting records between 2005 and 2010

```sql
SELECT * FROM station_data
WHERE year BETWEEN 2005 AND 2010
```

### 3.4: Using `AND`

```sql
SELECT * FROM station_data
WHERE year >= 2005 AND year <= 2010
```

### 3.5: Exclusive Range

This will get the years between 2005 and 2010, but exclude 2005 and 2010

```sql
SELECT * FROM station_data
WHERE year > 2005 AND year < 2010
```

### 3.6: Using `OR`

```sql
SELECT * FROM station_data
WHERE MONTH = 3
OR MONTH = 6
OR MONTH = 9
OR MONTH = 12
```

### 3.7: Using `IN`

```sql
SELECT * FROM station_data
WHERE MONTH IN (3,6,9,12);
```

### 3.8: Using `NOT IN`

```sql
SELECT * FROM station_data
WHERE MONTH NOT IN (3,6,9,12);
```

### 3.9: Using Modulus

The modulus will perform division but return the remainder. So a remainder of 0 means the two numbers divide evenly.

```sql
SELECT * FROM station_data
WHERE MONTH % 3 = 0;
```

### 3.10: Using `WHERE` on TEXT

```sql
SELECT * FROM station_data
WHERE report_code = '513A63'
```

### 3.11: Using `IN` with text

```sql
SELECT * FROM station_data
WHERE report_code IN ('513A63','1F8A7B','EF616A')
```

### 3.12: Using `length()` function

```sql
SELECT * FROM station_data
WHERE length(report_code) != 6
```

### 3.13A: Using `LIKE` for any characters

```sql
SELECT * FROM station_data
WHERE report_code LIKE 'A%';
```

### 3.13B: Using Regular Expressions


If you are familiar with regular expressions, you can use those to identify and qualify text patterns.

```sql
SELECT * FROM STATION_DATA
WHERE report_code REGEXP '^A.*$'
```

### 3.14: Using `LIKE` for one character

```sql
SELECT * FROM station_data
WHERE report_code LIKE 'B_C%';
```

>For `LIKE`, `%` is used in a different context than modulus `%`

### 3.15: True Booleans 1

```sql
SELECT * FROM station_data
WHERE tornado = 1 AND hail = 1;
```

### 3.16: True Booleans 2

```sql
SELECT * FROM station_data
WHERE tornado AND hail
```

### 3.17: False Booleans 1

```sql
SELECT * FROM station_data
WHERE tornado = 0 AND hail = 1;
```

### 3.18: False Booleans 2

```sql
SELECT * FROM station_data
WHERE NOT tornado AND hail;
```

### 3.19: Handling `NULL`

A `NULL` is an absent value. It is not zero, empty text ' ', or any value. It is blank.

To check for a null value:

```sql
SELECT * FROM station_data
WHERE snow_depth IS NULL;
```


### 3.20: Handling `NULL` in conditions

Nulls will not qualify with any condition that doesn't explicitly handle it.

```sql
SELECT * FROM station_data
WHERE precipitation <= 0.5;
```

If you want to include nulls, do this:

```sql
SELECT * FROM station_data
WHERE precipitation IS NULL OR precipitation <= 0.5;
```

You can also use a `coalesce()` function to turn a null value into a default value, if it indeed is null.

This will treat all null values as a 0.

```sql
SELECT * FROM station_data
WHERE coalesce(precipitation, 0) <= 0.5;
```

### 3.21: Combining `AND` and `OR`

Querying for sleet or snow

Problematic. What belongs to the `AND` and what belongs to the `OR`?

```sql
SELECT * FROM station_data
WHERE rain = 1 AND temperature <= 32
OR snow_depth > 0;
```

You must group up the sleet condition in parenthesis so it is treated as one unit.

```sql
SELECT * FROM station_data
WHERE (rain = 1 AND temperature <= 32)
OR snow_depth > 0;
```
