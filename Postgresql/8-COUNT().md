# COUNT()

7.1 Combien d'employés compte l'entreprise ?

7.2 Y a-t-il un employé sans prénom ?  

7.3 Combien d'enregistrements y a-t-il dans la table **salaries** ?

7.4 Combien de contrats annuels d'une valeur supérieure ou égale à 100.000 $ ont été enregistrés dans le tableau **salaries** ?

7.5 Combien de fois avons-nous payé des salaires à des employés ?

Cela devrait donner le même résultat que ci-dessus:

```sql
SELECT COUNT(from_date)
FROM salaries;
```
