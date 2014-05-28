# API HTTP

## Présentation


L'API HTTP a pour but d'offrir un accès standard aux données de Dynacase.


L'architecture de cette api s'appuie sur une architecture REST.

De part cette architecture, l'api permet de manipuler des **ressources**.

Les ressources manipulables par l'api sont :

*   Le document (document unitaire et collection de document)
*   Les utilisateurs
*   Les familles (structure et configuration)
*   La poubelle
*   Les fichiers


## Structure de l'URL

L'url d'accès à l'api de Dynacase comment par `/api/`. Cela permet d'identifier
explicitement l'usage de l'api et permet de contrôler et de paramétrer plus
simplement l'accès à l'api.

Il est alors possible de créer un domaine virtuel pour accéder à l'api
"http://api.mydomain.org" par exemple.


|                   url                    |                                                        signification                                                        |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `GET /api/<ressource>/ `                 | Liste des éléments de la ressource                                                                                          |
| `POST /api/<ressource>/`                 | Création d'un nouvel élément de la ressource                                                                                |
| `PUT /api/<ressource>/`                  | Modification en masse des éléments de la ressource                                                                          |
| `DELETE /api/<ressource>/`               | Suppression de tous les éléments de la ressource                                                                            |
|                                          |                                                                                                                             |
| `GET /api/<ressource>/<id>[.<type>]?`    | Information sur l'élément identifié par "id". Le type de retour est donnée par l'extension. L'extension par défaut est JSON |
| `POST /api/<ressource>/<id>[.<type>]? `  | **NON SIGNIFICATIF**                                                                                                        |
| `PUT /api/<ressource>/<id>[.<type>]?`    | Mise à jour de l'élément identifié par "id".                                                                                |
| `DELETE /api/<ressource>/<id>[.<type>]?` | Suppression  de l'élément identifié par "id".                                                                               |
|                                          |                                                                                                                             |
|                                          |                                                                                                                             |



## Les entrées

Toutes les entrées doivent être encodé en **UTF-8**.

### PUT (Mise à jour), POST (Création)

Un ordre "POST" indique une création de ressource.

Les données à enregistrer dans la ressource peuvent être envoyées sous 2 formes :

1.  Sous la forme d'un objet JSON (application/json)
2.  Sous la forme de variable encodée (x-www-form-urlencoded)

Les options de mise à jour sont envoyées dans l'url à l'aide variable "GET".

### GET (Consultation), DELETE (Suppression)

Le corps de la requête est vide.

Les options de consultation sont envoyées dans l'url à l'aide de variables.

## Retour JSON

Dans le cas d'un retour JSON la structure retournée contient les éléments suivants :

    [php]
    {
        "success" : true, // false ou true
        "messages" : [{
            "type" : "warning", // niveau du message
            "contentText" : "once upon a time",
            "contentHtml" : "",
            "code" : "", // code identifiant la catégorie du message
            "uri" : "", // url d'accès à la page web correspondant à l'erreur
            "data" : {}  // données supplémentaires
            }],
        "data" : {} // données demandées par la requête
        
    }

Ce retour est envoyé quelque soit le résultat de la requête.

## Les retours sans erreur

Si l'action demandée a été exécutée le code HTTP 200 est retourné.

| Http Statut |   Signification   |
| ----------- | ----------------- |
|         200 | Ressource trouvée |
|         201 | Ressource créée   |
|             |                   |


Le type de retour est soit précisé dans l'url soit dans le header HTTP ("accept").
Le type de l'url est prioritaire au header.

Exemple de retour :

    [php]
    {
        "success" : true, // false ou true
        "messages" : [],
        "data" : {
            "document" : {
                    "properties" : {
                        "id" : 1224,
                        "title" : "Hello world"
                    },
                    "attributes" : {
                        "ba_ttle" : {"value" : "Hello world"},
                        "ba_desc" : {"value" : "Nice Day"},
                    }
              }
        }
    }



## Les retours d'erreur

Si l'action demandée n'a pas pu aboutir un code HTTP 4xx est retourné.

| Http Statut |               Cause                |
| ----------- | ---------------------------------- |
|         404 | Ressource non trouvée              |
|         403 | Ressource protégé (accès interdit) |
|         400 | Données d'entrées invalides        |
|             |                                    |


Si l'action n'est pas implémenté le code 501 est retourné

| Http Statut |      Cause      |
| ----------- | --------------- |
|         501 | Not implemented |
|             |                 |

Exemple de retour :

Cas d'un 404.

    [php]
    {
        "success" : false, 
        "messages" : [{
            "type" : "error", 
            "contentText" : "Document \"1234\" not found",
            "contentHtml" : "",
            "code" : "API0010", 
            "uri" : "http://api.dynacase.org/code/API0010.html",
            "data" : null
            }],
        "data" : null
    }

## Version de l'API

L'API peut varier suivant les différentes versions.

Il est possible de préciser la version de l'API pour s'assurer de l'immuabilité
des retours et des entrées. 

S'il n'y a pas de version définie, la dernière version sera appliquée.

La version est indiquée dans le header HTTP de l'envoi de la requête :

    X-Api-Version: 1.0

La réponse envoi aussi systématiquement la version dans le header HTTP.


*Variante* : la version de l'api peut être indiqué dans l'url :

    /api/v1/documents/1234.json

La version de l'url est le chiffre indiqué après la lettre "v".

## Authentification

L'accès à l'api demande une authentification.

L'utilisation de l'api à l'intérieur d'interface de Dynacase utilise
l'authentification "classique" définie par Dynacase. L'utilisateur étant déjà
authentifié, aucune authentification supplémentaire n'est requise.

L'api accédée de façon externe peut utiliser l'authentification HTTP Basic.

    $ curl -u "username" https://www.example.net/api/

L'api supporte aussi l'authentification par "OAuth2" à l'aide d'un jeton. 

    $ curl -H "Authorization: token OAUTH-TOKEN" https://www.example.net/api/

ou 

    $curl https://www.example.net/api/?access_token=OAUTH-TOKEN

## Droit d'accès

L'accès au ressource est contrôlé par la ressource elle-même mais l'utilisation
de l'api est aussi contrôlé de manière générale par l'application "HTTPAPI".

Cette application définie 4 droits qui autorisent l'accès aux ressources :

*   `PUT` : Droit de lancer des requêtes de modification de ressources
*   `POST` : Droit de lancer des requêtes de création de ressources
*   `GET` : Droit de lancer des requêtes de consultation de ressources
*   `DELETE` :Droit de lancer des requêtes de suppression de ressources

## Url ROOT

L'accès à l'url `/api/` sans autre information affiche une page web indiquant
les différentes ressources mis à disposition.
