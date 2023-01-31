#SQL : PostgreSQL

##Installer PG Admin

Pour la formation njous allons utiliser PostgreSQL et son outil d'administration PG Admin
https://www.pgadmin.org/

##DML : la manipulation des données

##Sélectionner des données :
```
SELECT {{ column [ AS alias],... }} FROM {{ schema.table }} WHERE {{ condition }}
```

### Opérateur  de condition
* `=`	Egalité strict
* `>`	Supérieur
* `<`	Inférieur
* `>=`	Supérieur ou égale
* `<=`	Inférieur ou égale
* `<>` ou `!=`	Différent
* `AND`	Ajouté une condition
* `OR`	Condition altérnative
* `IN`	Si présent dans une liste
* `BETWEEN $ AND $`	Compris entre
* `LIKE`	Utiliser pour comparé des chaine de caractère
* `IS NULL`	Si la valeur est null
* `NOT`	Inversé n'importe quelle condition

### Pattern de chaine :
```
'abc' LIKE 'abc'    true
'abc' LIKE 'a%'     true
'abc' LIKE '_b_'    true
'abc' LIKE 'c'      false

```

https://www.postgresql.org/docs/current/functions-matching.html

NDlr6542

### Fonctions génériques

```
COALESCE({{ argument_1, argument_2, … }});
--- renvoi le première argument qi n'est pas `NULL`
```

```
SUM({{ column }});
--- aggregat de somme, necessite group by ou colonne unique
```

```
COUNT({{ column }});
--- aggregat de somme, necessite group by ou colonne unique
```
```
MAX({{ column }});
--- valeur maximum, necessite group by ou colonne unique
```

```
MIN({{ column }});
--- valeur minimum, necessite group by ou colonne unique
```

```
SUBSTRING({{ column }} [from <str_pos>] [for <ext_char>])
--- utiliser une partie d'un texte
```
```
REPLACE({{ column }} [search value] [result value])
--- remplace toute les occurences d'un texte
```

```
LTRIM | RTRIM | BTRIM({{ column }})
--- suppirmer les espaces de début et de fin
```
```
SELECT REGEXP_REPLACE({{ column }}, {{ expression }}, {{  argument }});
--- utiliser un regex
```

### GROUP BY

### ORDER BY

### LIMIT

### JOINTURES

INNER JOIN renvoi que les valeur qui trouve une relation
LEFT JOIN renvoi que la table source et les donnée lié
RIGHT JOIN renvoi que la table appelée et lie les donnée de la table source
FULL OUTER JOIN renvoi toutes les donnée des deux table

Utilisation de IS NULL

### Utiliser CASE
```
SELECT title,
       length,
       CASE
           WHEN length> 0
                AND length <= 50 THEN 'Short'
           WHEN length > 50
                AND length <= 120 THEN 'Medium'
           WHEN length> 120 THEN 'Long'
       END duration
FROM film
ORDER BY title;
```

##Insérer des données :

```
INSERT INTO {{ schema.table }} {{ column,...}} VALUES {{ data,... }};
```

```
INSERT INTO {{ schema.table }}
SELECT * FROM items WHERE {{ condition }};
```

```
INSERT INTO {{ schema.table }} {{ column,... }}
SELECT {{ column,... }} from {{ schema.table }} where {{ condition }};
```

##Modifier des données existantes :

```
UPDATE table SET opération WHERE condition
```

##Supprimer des données :

```
DELETE FROM {{ schema.table }} WHERE {{ condition }}
```

##DDL : la définition des données

###Table 

####Création d'une table
```
CREATE TABLE {{ schema.table }} ({{ column type, contraint, ... }});

```

####Type de contrainte
```
CONSTRAINT {{ title }} PRIMARY KEY ({{ column }});

CONSTRAINT {{ title }} FOREIGN KEY ({{ column }}) 
		REFERENCES {{ foreign_schema.foreign_table }} ({{ foreign_column }}) 
    MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;

```
#####Match

* MATCH SIMPLE : si au moins une colonne de référence est nulle, alors la ligne de la table de référence passe la vérification de contrainte. Si toutes les colonnes de référence ne sont pas nulles, la ligne réussit la vérification de contrainte si et seulement s'il existe une ligne de la table référencée qui correspond à toutes les colonnes de référence.

* MATCH PARTIAL : si toutes les colonnes de référence sont nulles, alors la ligne de la table de référence passe la vérification de contrainte. Si au moins une colonne de référence n'est pas nulle, la ligne réussit la vérification de contrainte si et seulement s'il existe une ligne de la table référencée qui correspond à toutes les colonnes de référence non nulles.

* MATCH FULL: si toutes les colonnes de référence sont nulles, alors la ligne de la table de référence passe la vérification de contrainte. Si toutes les colonnes de référence ne sont pas nulles, la ligne réussit la vérification de contrainte si et seulement s'il existe une ligne de la table référencée qui correspond à toutes les colonnes de référence. Si une colonne de référence est nulle et qu'une autre colonne de référence n'est pas nulle, la ligne de la table de référence viole la vérification des contraintes.

##### Actions quand le parent est mis à jour ou supprimer

* NO ACTION :
* SET NULL :

###Modier une table
```
ALTER TABLE IF EXISTS test.users ADD CONSTRAINT uniq_email UNIQUE (email);
```

###Créer un index
```
CREATE INDEX {{ index_title }} ON {{ schema.table }} ( {{ column }} );
```

###Créer une séquence

```
CREATE SEQUENCE {{ sequence_title }};

```



##DCL : les autorisations

```
CREATE USER "usrname" with paswword "password"
```

```
CREATE ROLE role;
```

##Gerer les droits d'un rôle

Attribuer des droits à un rôle
```
GRANT {{ action }} ON {{ element }} TO role/user;

//actions
ALL PRIVILEGES | SELECT | INSERT | UPDATE | DELETE | TRUNCATE | REFERENCES | TRIGGER

//element
TABLE | SEQUENCE | DATABASE | SCHEMA
```
supprimer des droits à un rôle
```
REVOKE {{ action }} ON {{ element }} TO {{ role }};
```

```
GRANT role TO role;
```

##TCL : le contrôle des transactions



