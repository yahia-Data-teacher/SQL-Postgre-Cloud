# DISTINCT et GROUP BY

6.1 Obtenir les différents noms dans la table **employees**.

Même résultat : Obtenir le prénom (first name) dans la table **employees** et regrouper par prénom.
```sql
SELECT first_name
FROM employees
GROUP BY first_name;
```

6.2 Combien de noms différents peut-on trouver dans la table employees ?

6.3 Combien de prénoms différents peut-on trouver dans la table employees ?

6.4 Combien de prénoms différents peut-on trouver dans la table employees ?

6.5 Combien de prénoms différents y a-t-il dans la table employees ? et ordonner par prénom en ordre décroissant ?

6.6 Combien de départements différents y a-t-il dans la base de données employees ? Indice : Utilisez la table dept_emp

6.7 Récupérer une liste de combien d'employés gagnent plus de 80 000 $ et combien ils gagnent. Renommer la 2ème colonne en emps_with_same_salary ?
