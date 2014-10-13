# Consultation des valeurs possibles d'un énuméré  {#rest:bb13e401-1859-4c73-b299-70b801ed7eb0}

## URL {#rest:e7530c89-82d0-4888-9d1e-3b354476928f}

    GET /api/v1/enums/<famName>/<attrid>/

Récupération des valeurs de l'énuméré de l'attribut `attrid` et de la famille `famName`.

## Content {#rest:d10aa78c-e870-4504-b566-c7f53e137e1a}

Le contenu de la requête est vide.

## Structure de retour {#rest:0fd3954e-3cb5-46d7-b96f-8dd33b44fa5f}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:d562ebc3-3b03-4b6b-a471-855a04a821ba}

La partie `data` contient 3 champs :

1.  `document.data.uri` : URI d'accès à la ressource modifiée;
1.  `document.data.label` : label de l'attribut traduit dans la langue de l'utilisateur;
1.  `document.data.filter` : filtre appliqués à la recherche,
1.  `document.data.enumItems` : tableau d'objets `key`, `label` (traduit dans la langue de l'utilisateur) et filtrés 
suivant les paramètres de filter,

Exemple :

    [javascript]
    {"success" :             true,
        "messages" :         [],
        "data" :             {
            "uri" :       "enums\/ZOO_ANIMAL\/an_sexe",
            "label" :     "sexe",
            "filter" :    {"operator" : "contains", "keyword" : "Masc"},
            "enumItems" : [{"key" : "M", "label" : "Masculin"}]
        },
        "exceptionMessage" : "",
        "headers" :          []
    }

### En cas d'échec {#rest:704f567e-eb1c-4800-bc03-e9076b2fb849}

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Famille non trouvée                            |         404 | API0200    |
| Attribut non trouvé                            |         404 | API0400    |
| Attribut de type non énuméré                   |         403 | API0401    |

Exemple : 

Cas d'erreur de en cas d'attribut non énuméré

    [javascript]
    {"success" :             false,
        "messages" :         [
            {
                "type" :        "error",
                "contentText" : "Attribute \"an_tatouage\" is not an enum (type \"int\") in family \"ZOO_ANIMAL\"",
                "contentHtml" : "",
                "code" :        "API0401",
                "uri" :         "",
                "data" :        null
            }
        ],
        "data" :             null,
        "exceptionMessage" : "Attribute \"an_tatouage\" is not an enum (type \"int\") in family \"ZOO_ANIMAL\"",
        "headers" :          []
    }

## Résultat partiel {#rest:2b3c2de1-4a64-4d07-98b5-ad89f148be3e}

L'attribut peut être retourné avec plus ou moins d'items.

* GET `/documents/1234.json?keyword=<keyword>`
* GET `/documents/1234.json?operator=startswith&keyword=<keyword>`

Les paramètres sont :

* `keyword` : celui-ci correspond au label,
* `operator` : celui-ci correspond à l'opérateur appliqué, deux choix sont possibles :
 * `startswith` : le label commence par le `keyword`,
 * `contains` : le label contient le `keyword`.
