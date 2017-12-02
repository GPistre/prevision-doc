=====
L'API
=====

Prevision.io offre la possibilité de faire des prévisions unitaires par call d’API. Pour ce faire, il faut se
rendre dans la page « Clé API » en cliquant sur le bouton :

.. image:: _static/images/api_button_fr.png
   :scale: 100 %
   :alt: alternate text
   :align: center

L’écran se présente sous la forme d’un tableau dans lequel vous pouvez générer des clé d’API qui
seront communiquées à des applications tierces et qui permettront le dialogue avec la plateforme
Prevision.io

Le tableau récapitule les projets exposés, le nombre d’utilisations de l’API ainsi que le token permettant
de faire l’appel à distance. Il vous est possible de supprimer les clés en cliquant sur le bouton
correspondant.

Pour générer une nouvelle clé, il vous suffit de choisir un projet dans la liste déroulante et de cliquer
sur le bouton « Générer ». La nouvelle clé s’affiche alors dans le champs texte juste sous le nom du
modèle.

En plus, nous vous proposons un exemple au format JSON sur le format de l’API. Vous pouvez utiliser
ce template pour vous aider à configurer vos appels dans vos applications tierces : il vous suffira de
remplacer les valeurs des variables et d’exécuter une requête POST.

Utilisation de l'API
--------------------

Afin de pouvoir utiliser les API fournies par l’écran précédent, il faut noter les 3 éléments :

* URL de la requête POST
* TOKEN généré par l’écran
* Requête au format JSON généré par l’écran

Attention : l’URL, le TOKEN et le JSON sont différents pour chaque projet !
L’URL à laquelle la requête doit être formatée comme suit :

``api/predictUnit/<data_train>?slug=<owner>``

Qu’il faudra prendre soin de compléter en fonction de l’environnement.
Pour les instances cloud il faut préfixer cette requête par : ``https://prevision.io/``
Pour les instances on-premise il faut préfixer cette requête par : ``http`` ou ``https://url_prevision/``

Exemple : ``https://prevision.io/api/predictUnit/data_train?slug=prevision``

Où le nom du projet est ``data_train``

Le TOKEN généré par l’application doit être inséré en lieu et place de <TOKEN> dans le JSON.
Ainsi, la requête proposée :

.. code-block:: javascript

    {
       "token": "<YOUR TOKEN>",
       "owner": "prevision",
       "features": {
          "ID": 10,
          "lat": 47.56,
          "long": -122.21
           }
    }


Doit devenir après avoir manuellement inséré le TOKEN :

.. code-block:: javascript

   {
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VfY2FzZSI6ImRhdGFfdHJhaW4iLCJvd25lciI6InByZXZpc2lvbiIsImlhdCI6MTUxMjE0OTQ0MDAxNCwiZXhwIjoxNTE5OTI1NDQwLCJpc3MiOiJwcmV2aXNpb24uaW8ifQ.X-sW9A0GuwWUhLnKtbf-8MxFn47jb6mscOdJfF3ptbE",
      "owner": "prevision",
      "features": {
      "ID": 10,
      "lat": 47.56,
      "long": -122.21
      }
   }

Maintenant, il ne reste plus qu’à envoyer ce JSON à l’adresse indiquée précédemment pour que
Prevision.io traite la demande et vous renvoie un JSON de réponse ressemblant à :

.. code-block:: javascript

   {
      "status": "EOK",
      "prediction": {
         "ID": 10,
         "TARGET": 502002.71875
         },
      "err_msg": "No error. Here is the preds"
   }