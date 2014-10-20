# Consultation de la liste des révisions d'un document {#rest:2dd5afbe-1d3d-4830-8241-c93077d88430}

## URL {#rest:4665a788-c584-4805-b638-3b40c33c281d}

    GET /api/v1/documents/<documentId>/revisions/

Récupération de la liste des révisions du document `<documentId>`.

L'identifiant du document peut être son nom logique, son identifiant numérique.

Note : Une révision d'un document "supprimé" peut être récupéré via l'url [trash][trash] en suivant le même mécanisme.

    GET /api/v1/trash/1234/revisions/

## Content {#rest:91384551-3ae9-4d97-8c70-0c81ab64bdfa}

Le contenu de la requête est vide.

## Structure de retour {#rest:d9f3ca39-11e2-4131-966a-034352f34ca7}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:e5b9222e-c8ef-433b-91fc-45efc59575a3}

La partie `data` contient une liste de documents révisés contenant par entrée :

1.  `title` : le titre de la révision;
1.  `uri` : l'uri d'accès de la révision;
1.  `documentId` : l'identifiant ou nom logique de la révision.

Exemple :

    [javascript]
    {"success" :             true,
        "messages" :         [],
        "data" :             [
            {
                "title" :      "AU_231pp",
                "documentId" : 1537,
                "uri" :        "http:\/\/dynacase.dev:8081\/api\/v1\/documents\/1505\/revisions\/2.json"
            },
            {
                "title" :      "AU_231pp",
                "documentId" : 1506,
                "uri" :        "http:\/\/dynacase.dev:8081\/api\/v1\/documents\/1505\/revisions\/1.json"
            },
            {
                "title" :      "AU_231",
                "documentId" : 1505,
                "uri" :        "http:\/\/dynacase.dev:8081\/api\/v1\/documents\/1505\/revisions\/0.json"
            }
        ],
        "exceptionMessage" : ""
    }

### En cas d'échec {#rest:5bfa051d-e3a4-4263-8589-f392a1257e2d}

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Document non trouvé                            |         404 | API0200    |

Exemple : 

Cas d'erreur de document non trouvé

    [javascript]
    {"success" :             false,
        "messages" :         [
            {
                "type" :        "error",
                "contentText" : "Document \"1200\" not found",
                "contentHtml" : "",
                "code" :        "API0200",
                "uri" :         "",
                "data" :        null
            }
        ],
        "data" :             null,
        "exceptionMessage" : "Document \"1200\" not found"
    }

## Cache {#rest:8d9d9dee-4e67-4881-aa4c-b490be94505e}

Dans le cadre du [cache][cache], le `Etag` est calculé à l'aide des éléments suivants :

* date de dernière modification du document,
* identifiant de l'utilisateur,
* identifiant des droits portés sur le document (vecteur de droits),
* langue sélectionnée.

L'ensemble de ces éléments sont concaténés et ensuite le [sha1][sha1] de cette concaténation consitue le `Etag`.

[trash]: #rest:52be10c1-9f46-456b-a22f-24909386567
[cache]: #rest:804f8d68-acfa-4a35-bb41-27b2a27c14dc
[sha1]: https://fr.wikipedia.org/wiki/SHA-1