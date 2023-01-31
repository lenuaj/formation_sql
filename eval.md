# Evaluation SQL

## DDL

##### Table films
* id : unique clé primaire
* nom
* année de sortie
* genre : clé etrangère nullable
* societe de production : clé etrangère suppression cascade
* réalisateur : clé etrangère nullable
* entrées
* budget 

##### Table acteurs
* id : unique clé primaire
* nom
* prenom
* nationalite
* date de naissance

##### Table réalisateurs
* id : unique clé primaire
* nom
* prenom
* nationelite
* date de naissance

##### Table genres
* id : unique clé primaire
* nom 
* description

##### Table sociétés de production
* id : unique clé primaire
* nom
* pays

##### Table relationnel entre film et acteur
* id_acteur : clé etrangère cascade
* id_film : clé etrangère cascade

##### Vue détail filmographie par acteur
* id acteur
* prenom acteur
* nom acteur
* nom du film
* année du film
  * ordonner par année

##### Vue detail filmographie par realisateur
* id realisateur
* nom realisateur
* prenom realisateur
* nom du film
* année du film
  * ordonner par année

##### Vue entrées réalisées par société de production
* id société
* nom
* total entrées de tous les films
  * ordonner par nombre d'entrées

## DML

##### Inserer des données
* 5 films, societe de production, réalisateur, acteurs principaux, genre

##### (ddl) Ajouter une colonne à la table acteur
* page wikipedia

##### Mettre à jour des données
* ajouter les pages wikipedia des acteurs

##### Supprimer une société de production dont le nom contient 'Century' et tous les films associés



