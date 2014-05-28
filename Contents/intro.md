# API HTTP

## Présentation


L'API HTTP a pour but d'offrir un accès standard aux données de Dynacase.

L'architecture de cette api s'appuie sur une architecture REST et permet de manipuler les **ressources** Dynacase :

Les ressources manipulables par l'api sont :

* Les documents 
* Les collections <span class="flag rfi"></span>
* Les utilisateurs <span class="flag rfi"></span>
* Les familles (structure et configuration) <span class="flag rfi"></span>
* La poubelle <span class="flag rfi"></span>
* Les fichiers <span class="flag rfi"></span>
* Les cycles <span class="flag rfi"></span>
* Les profils <span class="flag rfi"></span>
* ...


## Structure de l'URL

Tout les accès à l'API HTTP Dynacase se font par L'url `//url.access.dynacase.votre.domaine/api/`. 

Cela permet d'identifier
explicitement l'usage de l'api et permet de contrôler et de paramétrer plus
simplement l'accès à l'api.
<span class="flag fixme"> controle et parametre : comment ? je pense que soit on explique comment (c'est specifique à notre API) soit on supprime cette phrase (c'est comme toutes les API HTTP)</span>


<span class="flag inline fixme">à déplacer dans un § spécifique</span>Il est alors possible de créer un domaine virtuel pour accéder à l'api
"http://api.mydomain.org" par exemple.

Lecture
:   

    [http]
    GET /api/<ressource>

Obtention des éléments d'une ressource

Création
:   

    [http]
    POST /api/<ressource>

Création d'un nouvel élément de la ressource

Modification
:   

    [http]
    PUT /api/<ressource>

Modification des éléments de la ressources

Suppression
:   

    [http]
    DELETE /api/<ressource>

Suppression des éléments de la ressources

Lecture d'un élément
:   

    [http]
    GET /api/<ressource>/<identifier>

Obtention de l'élément désigné par `<indentifier>`.

Modification d'un élément
:   

    [http]
    PUT /api/<ressource>/<identifier>

Modification de l'élément désigné par `<indentifier>`.


Suppression d'un élément
:   

    [http]
    PUT /api/<ressource>/<identifier>

## Encodage

Toutes les échanges, entrées et retours de l'API, sont encodés en **UTF-8**.

## Les entrées


### Type de retour attendu

Le type de retour attendu (format) est précisé soit :

* dans l'URL

        [http]
        PUT /api/<ressource>/<identifier>.<type>

* dans l'entête HTTP : `accept`.

Actuellement, seul le type `json` est géré.

Le type de l'url est prioritaire au header.

### PUT (Mise à jour), POST (Création)

Les données à enregistrer dans la ressource peuvent être envoyées sous 2 formes :

1.  Sous la forme d'un objet JSON (application/json)
2.  Sous la forme de variable encodée (x-www-form-urlencoded)

Les options de mise à jour sont envoyées via des variables sur l'URL.

### GET (Consultation), DELETE (Suppression)

Le corps de la requête est vide.

Les options de consultation sont envoyées dans l'url à l'aide de variables.

## Retour JSON

Dans le cas d'un retour JSON la structure retournée contient les éléments suivants :

    [php]
    {
        "success" : true,       // false ou true
        "messages" : [{
            "type" : "warning", // type de message error, userMessage, warning, notice, notification
            "contentText" : "once upon a time",
            "contentHtml" : "",
            "code" : "",        // code identifiant la catégorie du message
            "uri" : "",         // url d'accès à la page web correspondant à l'erreur
            "data" : { }        // données supplémentaires
            }],
        "data" : {}             // données demandées par la requête
        
    }
    
Ce retour est envoyé quelque soit le résultat de la requête, y compris en cas d'erreur.

## Les retours sans erreur

Si l'action demandée a été exécutée le code HTTP 2xx est retourné.

**200**
:  Ressource trouvée
  
**201**
:  Ressource créé


Exemple de retour :

    [json]
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

**400**
:  Données en entrée invalides

**403**
:  Ressource protégée (accès interdit)

**404**
:  Ressource non trouvée

**501**
:  La méthode demandée n'est pas disponible sur cette ressource

**507**
:  Espace de stockage insuffisant sur le serveur


Exemple de retour, cas d'un 404 :

    [json]
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

Il est possible de préciser la version de l'API pour s'assurer de l'immuabilité
des retours et des entrées. 

S'il n'y a pas de version définie, la dernière version est utilisée.

La version est indiquée dans le header HTTP de l'envoi de la requête :

    X-DCP-Api-Version: 1

La réponse envoie systématiquement la version dans le header HTTP.


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

L'api supporte aussi l'authentification par "OAuth2" à l'aide d'un jeton. <span class="flag rfi"></span>

    $ curl -H "Authorization: token OAUTH-TOKEN" https://www.example.net/api/

ou 

    $curl https://www.example.net/api/?access_token=OAUTH-TOKEN

## Droit d'accès

L'accès aux ressources est contrôlé par les ressources elles-même mais l'utilisation
de l'api est aussi contrôlé de manière générale par l'application "HTTPAPI".

Cette application définit 4 droits qui autorisent l'utilisation des méthodes sur les ressources :

*   `PUT` : modification de ressources
*   `POST` : création de ressources
*   `GET` : consultation de ressources
*   `DELETE` : suppression de ressources

## Url ROOT

L'accès à l'url `/api/` sans autre information affiche une page web indiquant
les différentes ressources mis à disposition.
