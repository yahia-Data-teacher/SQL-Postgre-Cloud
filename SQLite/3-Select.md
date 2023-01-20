# Dans cette partie nous allons travailler avec la base de données :  rexon_metals.db

- ### Sélectionner la base de donnée  rexon_metals.db sur BDHub.io .

- ### Double cliquer sur rexon_metals.db 

![a](https://user-images.githubusercontent.com/78825764/213727063-7b9f18d9-f159-4962-b1cb-c596a115594a.jpg)

- ### Vous pouvez ici voir les différents table dans la base de donnée rexon_metals.db


![a](https://user-images.githubusercontent.com/78825764/213727208-c25a509d-9701-4241-b963-eff0953dbcf0.jpg)

- ### Maintenant , pour pouvoir écrire et éxecuter des requetes sqlite aller sur visualise :

![a](https://user-images.githubusercontent.com/78825764/213727865-83d3a246-8530-4f16-80ee-d795dae82770.jpg)

- ### Voilà ! Ici vous pouvez essayer des requete sqlite :

![a](https://user-images.githubusercontent.com/78825764/213728130-437c862d-a7be-4d7d-a4fb-714ed0aae8af.jpg)

# SELECT() :

### 2.1: Selecting all columns

```sql
SELECT * FROM CUSTOMER;
```
- Voilà comment vous pouvez exécuter des requetes sur BDHub.io :

![a](https://user-images.githubusercontent.com/78825764/213730201-6fa6d9ab-a6db-46ee-b43f-ae3d69fc15c6.jpg)


To limit the number of records returned, use a LIMIT. To limit the results to just 2 records:

```sql
SELECT * FROM CUSTOMER LIMIT 2;
```

### 2.2: Selecting specific columns

```sql
SELECT CUSTOMER_ID, NAME FROM CUSTOMER;
```

### 2.3: Expressions

First, select everything from `PRODUCT`

```sql
SELECT * FROM PRODUCT;
```

You can use expressions by declaring a `TAXED_PRICE`. This is not a column, but rather something that is calculated every time this query is executed.

```sql
SELECT PRODUCT_ID,
DESCRIPTION,
PRICE,
PRICE * 1.07 AS TAXED_PRICE
FROM PRODUCT;
```

> In SQliteStudio, you can hit CTRL + SPACE on Windows and Linux to show an autocomplete box with available fields. For Mac, you will need to enable that configuration in preferences.

You can also use aliases to declare an `UNTAXED_PRICE` column off the `PRICE`, without any expression.

```sql
SELECT PRODUCT_ID,
DESCRIPTION,
PRICE as UNTAXED_PRICE,
PRICE * 1.07 AS TAXED_PRICE
FROM PRODUCT;
```

**SWITCH TO SLIDES** FOR MATHEMATICAL OPERATORS

### 2.4: Using `round()` Function

```sql
SELECT PRODUCT_ID,
DESCRIPTION,
PRICE,
round(PRICE * 1.07, 2) AS TAXED_PRICE

FROM PRODUCT;
```

### 2.5: Text Concatenation

You can slap a dollar sign to our result using concatenation.

```sql
SELECT PRODUCT_ID,
DESCRIPTION,
PRICE AS UNTAXED_PRICE,
'$' || round(PRICE * 1.07, 2) AS TAXED_PRICE
FROM PRODUCT;
```

You can merge text via concatenation. For instance, you can concatenate two fields and put a comma and space ` ,` in between.

```sql
SELECT NAME,
CITY || ', ' || STATE AS LOCATION
FROM CUSTOMER;
```

You can concatenate several fields to create an address.

```sql
SELECT NAME,
STREET_ADDRESS || ' ' || CITY || ', ' || STATE || ' ' || ZIP AS SHIP_ADDRESS
FROM CUSTOMER;
```

This works with any data types, like numbers, texts, and dates. Also note that some platforms use `concat()` function instead of double pipes `||`

**SWITCH TO SLIDES** FOR EXERCISE


## 2.6: Comments

To make a comments in SQL, use commenting dashes or blocks:

```sql
-- this is a comment

/*
This is a
multiline comment
*/
```
