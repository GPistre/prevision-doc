==================
En cas de problème
==================


Je ne peux pas entraîner de modèles
-----------------------------------


J'ai une notification "erreur" lors de l'entraînement
-----------------------------------------------------


J'ai une notification "erreur" lors de la prédiction
----------------------------------------------------

S'il n'y a pas eu de notification d'erreur pendant l'entraînement, mais que l'upload d'un fichier de
prédiction ne fonctionne pas, l'erreur la plus probable est une différence entre la structure du jeu d'entraînement
et celle du jeu de prédiction.

Assurez vous que :

* Les colonnes ont le même type (int, string, float, ...) dans les deux jeux.
* Toutes les colonnes du jeu d'entraînement sont aussi présentes dans le jeu de prédiction.

