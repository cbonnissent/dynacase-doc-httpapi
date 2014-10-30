# Liste des vues d'un document {#rest:033c1b91-2622-413d-9b39-f39700185f84}

## URL  {#rest:a2f90358-24fa-479f-a65a-3b77975219bc}

    GET /api/v1/documents/<documentId>/views/

Récupére la liste des vues applicable pour l'utilisateur en cours du dernier documents applicable `<documentId>`.

## Content  {#rest:19a741b8-8585-46b2-9184-5657471007aa}

Le contenu de la requête est vide.

## Structure de retour  {#rest:0a496954-bc77-4595-be41-f69a265b3967}

Le retour est une donnée JSON.

### En cas de réussite :  {#rest:4b5f97e1-67b4-4b61-96c8-d2a7bc0eff7b}

    [javascript]
    {
        "success": true,
        "messages": [],
        "data": {
            "uri": "http://dynacase.dev:8081/api/v1/documents/MY_DOC/views/",
            "views": [
                {
                    "viewId": "edit_extern",
                    "label": "Vue d'édition externe",
                    "mode" : "edition",
                    "order" : 100,
                    "uri": "http://dynacase.dev:8081/api/v1/documents/MY_DOC/views/edit_extern.json"
                },
                {
                    "viewId": "edit_intern",
                    "label": "Vue d'édition interne",
                    "mode" : "edition",
                    "order" : 200,
                    "uri": "http://dynacase.dev:8081/api/v1/documents/MY_DOC/views/edit_intern.json"
                },
                {
                    "viewId": "consult_extern",
                    "label": "Vue de consultation externe",
                    "mode" : "consultation",
                    "order" : 100,
                    "uri": "http://dynacase.dev:8081/api/v1/documents/MY_DOC/views/consult_extern.json"
                },
                {
                    "viewId": "consult_intern",
                    "label": "Vue de consultation interne",
                    "mode" : "consultation",
                    "order" : 200,
                    "uri": "http://dynacase.dev:8081/api/v1/documents/MY_DOC/views/consult_intern.json"
                },
            ]
        }
    }

L'api retourne la liste de vues (`views`) applicable pour l'utilisateur en cours chacun des éléments contient :
 
* l'URI permettant d'accéder à la liste des valeurs,
* le label de la vue dans la langue de l'utilisateur,
* le nom logique de la vue,
* le type de vue (consultation ou edition),
* ordre d'application de la vue.


### En cas d'échec  {#rest:a806a5da-3ace-41a0-9979-6d91029f61ea}

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Document non trouvée                           |         404 | API0220    |

Exemple : 




## Filtres  {#rest:d257bfd3-ec72-4202-9cad-c799066a1092}

### Slice {#rest:dc682a0c-c9b2-497d-aae6-e4df21fa598b}

Cette option indique le nombre de valeur maximum à retourner.

Exemple :

    GET /api/v1/documents/MY_DOC/views/?slice=10

### Offset {#rest:5bb670b5-7265-4aad-9a54-39597dd46f96}

Index à partir duquel, les énumérés sont retournées.

Exemple: 

    GET /api/v1/documents/MY_DOC/views/?slice=2&offset=7
