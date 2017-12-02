==============
Pour commencer
==============

A quoi sert Prevision.io ?
--------------------------

A partir de données d'apprentissage, la plateforme Prevision.io permet d'entraîner automatiquement des modèles de machine learning et des ensembles
et de les déployer pour obtenir des prédictions à travers une interface web ou une API REST.

Pour plus d'informations, vous pouvez consulter la FAQ (FAQ link) ou nous contacter directement.


Entraîner un modèle avec Prevision.io
-------------------------------------

Pour explorer les fonctionnalités de la plateforme, nous allons créer un projet avec un
un jeu de données public relativement simple.

On peut trouver le jeu de données "Bank Marketing Dataset" sur le site de l'université d'Irvine :
https://archive.ics.uci.edu/ml/machine-learning-databases/00222/

Les données
~~~~~~~~~~~


+------+--------------+----------+-------------------+---------+------+----------+----------+----------+-----+
|  age | job          | marital  | education         | housing | loan | duration | campaign | previous | y   |
+======+==============+==========+===================+=========+======+==========+==========+==========+=====+
| 41   | blue-collar  | divorced | basic.4y          | yes     | no   | 1575     | 1        | 0        | yes |
+------+--------------+----------+-------------------+---------+------+----------+----------+----------+-----+
| 38   | admin.       | married  | high.school       | no      | no   | 165      | 2        | 0        | no  |
+------+--------------+----------+-------------------+---------+------+----------+----------+----------+-----+
| 49   | entrepreneur | married  | university.degree | yes     | no   | 1042     | 1        | 0        | yes |
+------+--------------+----------+-------------------+---------+------+----------+----------+----------+-----+
| 38   | technician   | single   | university.degree | no      | yes  | 20       | 1        | 0        | no  |
+------+--------------+----------+-------------------+---------+------+----------+----------+----------+-----+
| 31   | admin.       | divorced | high.school       | no      | no   | 246      | 1        | 0        | no  |
+------+--------------+----------+-------------------+---------+------+----------+----------+----------+-----+

L'objectif du problème est de prédire quels clients de cette banque
vont le plus probablement acheter le produit proposé, en apprenant à partir des achats passés.
La variable représentant le fait que les clients ont acheté le produit est "y", et sera donc la cible.

Voici ce dont vous devez vous soucier avant de lancer un projet sur la plateforme :

* D'avoir un véritable problème de Machine Learning supervisé,
c'est à dire un jeu de données contenant une colonne que l'on souhaite prédire.
Dans le cas présent, la colonne ne contient que deux valeurs "yes" et "no", et c'est
donc un problème de classification binaire. Si vous souhaitez traiter un problème de
régression (prédiction d'une variable continue) ou de multi-classification,
des sections spécifiques y sont consacrées.

Concernant les données, la plateforme s'occupera de tout le reste,
et traitera les
valeurs manquantes, l'encodage des variables catégorielles,
une transformation du texte (TF-IDF, word2vec, etc...), la normalisation
des valeurs numériques et l'extraction des composants des dates détectées.


Créer un projet
~~~~~~~~~~~~~~~

-------------------------
 Importer un fichier .csv
-------------------------

What does it look like ?

* This is a bulleted list.
* It has two items, the second
  item uses two lines.

-----------------------------
 Importer une base de données
-----------------------------


Suivre l'avancement et les performances du projet
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
What does it look like ?

* This is a bulleted list.
* It has two items, the second
  item uses two lines.


Prédire avec le projet
~~~~~~~~~~~~~~~~~~~~~~

-------------------------------
 En batch, avec l'interface web
-------------------------------

What does it look like ?

* This is a bulleted list.
* It has two items, the second
  item uses two lines.

----------------------------------
 Avec l'API de prediction unitaire
----------------------------------

What does it look like ?

* This is a bulleted list.
* It has two items, the second
  item uses two lines.

