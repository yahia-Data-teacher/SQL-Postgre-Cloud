# Create Table in ElephantSQL :

- Double cliquer sue l'instance que vous avez créer: 

![a](https://user-images.githubusercontent.com/78825764/213692578-ef424bcc-e6a6-4ead-aed2-366041f79bd6.jpg)

- Allez à Browser :


![a](https://user-images.githubusercontent.com/78825764/213692914-a90c44c4-de8e-413e-8bb2-3ca2bf84b780.jpg)

- Et Voilà , c'est ici où on va écrire nos requetes SQL :

![a](https://user-images.githubusercontent.com/78825764/213693338-7905dc2c-d868-4c25-94e7-17dd8d9690c6.jpg)


# Syntaxe PostgreSQL CREATE TABLE

- Une base de données relationnelle se compose de plusieurs tables liées.

- Pour créer une nouvelle table, vous utilisez l'instruction CREATE TABLE
- Voici une illustration de la syntaxe de base de l'instruction CREATE TABLE :

```
CREATE TABLE [IF NOT EXISTS] table_name (
   column1 datatype(length) column_contraint,
   column2 datatype(length) column_contraint,
   column3 datatype(length) column_contraint,
   table_constraints
);
```

- PostgreSQL inclut les column_contraint suivantes :

- **NOT NULL**  - garantit que les valeurs d'une colonne ne peuvent pas être NULL.
- **UNIQUE** – garantit que les valeurs d'une colonne sont uniques dans toutes les lignes d'une même table.
- **PRIMARY KEY** - une colonne de clé primaire identifie de manière unique les lignes d'une table. Une table peut avoir une et une seule clé primaire. La contrainte de clé primaire permet de définir la clé primaire d'une table.
- **CHECK** – une CHECKcontrainte garantit que les données doivent satisfaire une expression booléenne.
- **FOREIGN KEY** - garantit que les valeurs d'une colonne ou d'un groupe de colonnes d'une table existent dans une colonne ou un groupe de colonnes d'une autre table. Contrairement à la clé primaire, une table peut avoir plusieurs clés étrangères.



# Exemples PostgreSQL CREATE TABLE
- Nous allons créer une nouvelle table appelée accountsqui a les colonnes suivantes :

![image](https://user-images.githubusercontent.com/78825764/213690535-df883203-43d6-46dc-8614-6efb727216c4.png)

  - user_id – clé primaire
  - nom d'utilisateur - unique et non nul
  - mot de passe - non nul
  - email – unique et non nul
  - created_on – non nul
  - dernier_login – null
  

  L'instruction suivante crée la table accounts :
  ```
CREATE TABLE accounts (
	user_id serial PRIMARY KEY,
	username VARCHAR ( 50 ) UNIQUE NOT NULL,
	password VARCHAR ( 50 ) NOT NULL,
	email VARCHAR ( 255 ) UNIQUE NOT NULL,
	created_on TIMESTAMP NOT NULL,
        last_login TIMESTAMP 
);
```
- Copier et coller cette requete dans SQL Browser de ElephantSQL , puis cliquer sur execute :

![a](https://user-images.githubusercontent.com/78825764/213693917-ac80dbaf-cf0f-4552-a137-ac931e56cec2.jpg)

- Vous pouvez vérifier que votre tableau a bien été créer sur STATS :


![a](https://user-images.githubusercontent.com/78825764/213694682-5206af2b-ad45-43f1-a890-ae86a20a9dd0.jpg)

- ### A vous de jouer maintenant !
- Creer la table roles comme on a fait pour la table accounts :

![image](https://user-images.githubusercontent.com/78825764/213691140-adefc0bf-df48-42b4-96f8-d39249806e6e.png)

 
