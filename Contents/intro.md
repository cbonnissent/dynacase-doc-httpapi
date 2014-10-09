# API HTTP

## Présentation


L'API HTTP a pour but d'offrir un accès standard aux données de Dynacase.

L'architecture de cette api s'appuie sur une architecture [REST (Representational state transfer)][wikipedia_rest] 
et permet de manipuler les **ressources** Dynacase suivantes :

* Les documents;
* Les familles;
* Les fichiers;
* Les fichiers temporaires.

## Quelques notions de [REST][wikipedia_rest] {#rest:4135ea93-d7ec-4903-b4c1-acb08623dcd5}

L'api présentée dans la suite du document est de type REST et utilise le vocabulaire propre à ces API, ce qui inclut :

## Structure de l'URL

## Structure de l'API {#rest:5883cb06-807a-4b58-8f60-88a0078fbbdd}

La structure est conforme au standard REST.

Les actions du [CRUD][wikipedia_crud] sont implémentées et associées sur les méthodes de HTTP, suivant la liste
d'équivalence suivante :  
  

| Action   | Méthode HTTP  | URL                 | Action effectuée                                                           |
| :-     : | :      : | :                      : |                                                                          : |
| `Create` | `POST`   | `/api/v1/<collection>`      | Créé une nouvelle entité dans la collection et répond avec l'entité        |
| `Read`   | `GET`    | `/api/v1/<collection>`      | Lit le contenu de la collection  et répond avec une liste d'entités        |
| `Read`   | `GET`    | `/api/v1/<collection>/<id>` | Lit l'entité `id` et répond avec l'entité                                  |
| `Update` | `PUT`    | `/api/v1/<collection>`      | Remplace l'intégralité de la collection et répond avec une liste d'entités |
| `Update` | `PUT`    | `/api/v1/<collection>/<id>` | Modifie l'entité `id` de la collection et répond avec l'entité             |
| `Delete` | `DELETE` | `/api/v1/<collection>`      | Supprime l'intégralité de la collection et répond avec une liste d'entités |
| `Delete` | `DELETE` | `/api/v1/<collection>/<id>` | Supprime l'entité `id` de la collection et répond avec l'entité            |

Les accès à l'API HTTP Dynacase se font par l'url `http[s]//<url_du_contexte>/api/v1/`.

## Encodage {#rest:3f228840-491e-4c4d-8d0a-2da3a3934179}

Tous les échanges, entrées et retours de l'API, sont encodés en **UTF-8**.

## Requête {#rest:20d76bcc-4312-48e0-a4f1-ad73b4fe4f9b}

Les éléments de la requête sont les suivants :

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

* dans l'URL : `PUT /api/<ressource>/<identifier>.<type>`

        [http]
        PUT /api/<ressource>/<identifier>.<type>

* dans l'entête HTTP : `accept`.

Actuellement, seul le type `json` est géré.

Le type exprimé dans l'URL est prioritaire sur celui de l'entête HTTP.

### PUT (Mise à jour), POST (Création)

Les données à enregistrer dans la ressource peuvent être envoyées sous 2 formes :

1.  Sous la forme d'un objet JSON (application/json) transmis dans le corps de la requête HTTP,
2.  Sous la forme de variable encodée (x-www-form-urlencoded) transmis dans le code de la requête HTTP.

Les options de mise à jour sont envoyées via des variables sur l'URL.

### GET (Consultation), DELETE (Suppression)

Le corps de la requête est vide.

Les options de consultation, suppression sont envoyées dans l'url à l'aide de variables dans l'URL.

## Retour JSON

 * Consultation du document `212` : `GET` : `/api/v1/documents/212`
 * Suppression du document `IUSER_JEAN_REMI` : `DELETE` : `/api/v1/documents/IUSER_JEAN_REMI`

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

#### Les retours sans erreur {#rest:c52418a7-218f-4794-88a8-f92feb88641d}

Si l'action demandée a été exécutée, le code HTTP 2xx est retourné.

**200**
:  Ressource trouvée
  
**201**
:  Ressource créé

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


#### Les retours d'erreur {#rest:e56e8fcd-13ab-456b-85d3-f9ce9b3c4123}

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

    [php]
    {
       "success" : false, 
       "messages" : [
          {
             "type"        : "error", 
             "contentText" : "Document \"1234\" not found",
             "contentHtml" : "",
             "code"        : "API0010", 
             "uri"         : "http://api.dynacase.org/code/API0010.html",
             "data"        : null
          }
       ],
       "data" : null
    }

## Version de l'API

Dans le cas d'un retour JSON, la structure retournée contient les éléments suivants :

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

## Version de l'API {#rest:4bd0efac-b454-4825-8efe-7dc85019a82c}

Il est nécessaire de préciser la version de l'API pour s'assurer de l'immuabilité
des retours et des entrées. 

La version de l'api peut être indiqué dans l'url :

    /api/v1/documents/1234.json

La version de l'url est le chiffre indiqué après la lettre "v".

## Authentification

L'accès à l'api demande une authentification.

L'utilisation de l'api à l'intérieur d'interface de Dynacase utilise la mécanique d'authentification "classique" 
définie par Dynacase. 

Cette mécanique est décrite dans la [documentation de core][authentification].

## Droit d'accès {#rest:cc9f6059-0ad6-4372-b82a-d5a1ca3ef6f3}

L'accès aux entités est contrôlé par les entités elles-même mais l'utilisation
de l'api est aussi contrôlée de manière générale par l'application "HTTPAPI".

Cette application définit 4 droits (ACL] qui autorisent l'utilisation des méthodes sur les entités :

*   `PUT` : modification d'entités;
*   `POST` : création d'entités;
*   `GET` : consultation d'entités;
*   `DELETE` : suppression d'entités.

## Url ROOT {#rest:845f4024-a0d3-4058-994e-1af20be1a410}

## Droit d'accès


Cette application définit 4 droits qui autorisent l'utilisation des méthodes sur les ressources :

*   `PUT` : modification de ressources
*   `POST` : création de ressources
*   `GET` : consultation de ressources
*   `DELETE` : suppression de ressources

## Url ROOT

L'accès à l'url `/api/` sans autre information affiche une page web indiquant
les différentes ressources mis à disposition.
