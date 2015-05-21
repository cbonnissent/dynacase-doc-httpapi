# Récupérer la liste des étapes  {#rest:af743cfe-c089-4706-a5fb-a131f68020d2}
## URL   {#rest:2dcd6047-0e9a-4bb2-b0f8-874bee17320b}

    GET /api/v1/documents/<documentId>/workflows/states/

Récupération des étapes suivantes possibles du document `documentId`.

Les étapes possibles sont les étapes qui ont une transition pour rejoindre
l'étape suivante et dont l'utilisateur a les privilège pour passer la transition.

Si la méthode [m0][m0] d'une transition, retourne un message, l'étape suivante
sera retournée en indiquant l'erreur.

Le paramètre optionnel `allStates=1` permet de retourner toutes les étapes même
celles qui n'ont pas de transition.

Exemple :

    GET /api/v1/documents/my_document/workflows/states/


## Content   {#rest:e4915ac8-fb6f-40e5-ba61-d5f402de7089}

Le contenu de la requête est vide.

## Structure de retour   {#rest:997018db-1e1e-4200-9f16-917f73206a52}

Le retour est une donnée JSON.

### En cas de réussite :   {#rest:758cb729-068f-4757-9c37-9821233d6a36}

La partie `data` contient :

1.  `uri` : URI préférentielle d'accès à la ressource;
1.  `states` : Liste des états
    1.  `id` : identifiant de l'état,
    1.  `label` : intitulé de l'état (localisé en fonction de la langue de l'utilisateur) 
    1.  `activity` : intitulé de l'activité (localisé en fonction de la langue de l'utilisateur) 
    1.  `displayValue` : intitulé calculé en fonction des valeurs de "activity" et "label"
    1.  `color` : code couleur (#RRGGBB) associé à l'état
    1.  `uri` : URI d'accès à l'état
    1.  `transition` : transition qui emmène à cet étape ("null" si pas de transition possible)
        1.  `uri` : uri de la transition
        1.  `label` : libellé de la transition
        1.  `error` : message de la méthode [m0][m0]

Exemple :

    [javascript]
    {
        "success": true,
        "messages": [],
        "data": {
            "uri": "./api/v1/documents/61120/workflows/states/",
            "states": [
                {
                    "id": "my_transmited",
                    "label": "Transmis",
                    "activity": "Vérification de l'adoption",
                    "displayValue": "Vérification de l'adoption",
                    "color": "#A8E5FF",
                    "uri": "./api/v1/documents/61120/workflows/states/my_transmited",
                    "transition": {
                        "uri": "./api/v1/documents/61120/workflows/transitions/my_Ttransmited",
                        "label": "Transmettre le dossier",
                        "error": ""
                    }
                }
            ]
        }
    }

### En cas d'échec   {#rest:fbf45270-2026-4504-80d2-14314ec9278f}

Les raisons d'échecs spécifiques à cette requête sont 

|            Raison           |       Status HTTP        | Error Code |
| --------------------------- | ------------------------ | ---------- |
| Pas de cycle de vie associé | 404 No workflow detected | CRUD0227   |

Exemple : 


    [javascript]
    {
        "success": false,
        "messages": [
            {
                "type": "error",
                "contentText": "No associated workflow for document \"9567\"",
                "code": "CRUD0227"
            }
        ],
        "data": null,
        "exceptionMessage": "No associated workflow for document \"9567\""
    }

<!-- links -->
[m0]:   http://docs.anakeen.com/dynacase/3.2/dynacase-doc-core-reference/website/book/core-ref:b8824399-f17d-4007-adde-8a7433939273.html#core-ref:391f603e-b23a-44e8-aa14-47b4ab1fd03b "Méthode m0"