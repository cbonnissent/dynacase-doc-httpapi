# Consultation d'un document  {#rest:1d7b939f-d5fc-4b57-b33f-d216913efc22}

## URL {#rest:0e462204-b355-4e5a-81f2-4cf75cef3162}

    GET /api/v1/families/<famName>/documents/<id>

Récupération d'un document de la famille `<famName>` ayant l'identifiant `<id>`.

ou

    GET /api/v1/documents/<id>

Récupération du document `<id>`.

L'extension ".json" peut être ajoutée pour expliciter le format de sortie.

Exemple :

    GET /api/v1/documents/1234.json

Note : la différence entre la ressources `families` et `documents` est que
l'identifiant doit être dans la famille indiquée pour être modifié sinon une
erreur 404 (ressource non trouvée) est retournée.

L'identifiant du document peut être son nom logique, son identifiant numérique.

L'identifiant numérique permet de référencer une révision précise du document.
Le nom logique fait toujours référence à la dernière révision du document.

Note : Un document "supprimé" peut être récupéré via l'url [trash][trash].

## Content {#rest:eac550a1-85ef-47d2-a28d-38f4604f4662}

Le contenu de la requête est vide.

## Structure de retour {#rest:c56944fc-8676-4114-aa60-e2ce4a63ef44}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:38df8680-739a-4120-872c-9e7bf7879029}

La partie `data` contient 3 champs :

1.  `document.uri` : uri d'accès à la ressource modifiée
1.  `document.properties` : liste des valeurs des propriétés
1.  `document.attributes` : liste des valeurs des attributs

Les attributs en visibilité "I" ne sont pas retournés. Leur existence n'est pas
dévoilée ni dans les données ni dans la structure.

Exemple :

    [javascript]
    {"success" :             true,
        "messages" :         [],
        "data" :             {
            "document" : {
                "uri" :        "api\/v1\/documents\/1057.json",
                "properties" : {
                    "title" :     "[123",
                    "state" :     null,
                    "name" :      null,
                    "icon" :      "resizeimg.php?img=Images%2Fdoc.png&size=32",
                    "fromname" :  "TEST_ALL_ELEMENT",
                    [...]
                },
                "attributes" : {
                    "test_all_element_title" :            {"value" : "[123", "displayValue" : "[123"},
                    "test_all_element_account" :          {"value" : null, "displayValue" : null},
                    "test_all_element_account_multiple" : [],
                    [...]
                }
            }
        },
        "exceptionMessage" : ""
    }

### En cas d'échec {#rest:d136a95c-04f0-4822-aef4-f2e32c1d2694}

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Document non trouvé                            |         404 | API0200    |
| Privilège insuffisant pour accéder au document |         403 | API0201    |
| Document supprimé                              |         404 | API0219    |
| Propriété demandée inexistante                 |         400 | API0202    |
| Attribut demandé inexistant                    |         400 | API0218    |

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

## Résultat partiel {#rest:789802cd-80ee-4b1d-92a2-eaa49da90046}

Le document peut être retourné avec plus ou moins d'information.

* GET /documents/1234.json?fields=document.properties
* GET /documents/1234.json?fields=document.properties.id,document.properties.title,document.attributes
* GET /documents/1234.json?fields=document.properties.id,document.properties.title,document.attributes.my_exemple
* GET /documents/1234.json?fields=document.properties.id,document.properties.title,document.attributes,family.structure

Par défaut : `fields=document.properties,document.attributes`

|           fields                   |                        Signification                         |                                                           Remarques                                                           |
| ---------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| `document.properties`              | Récupère l'ensemble des propriétés "visible"                 | "state", "fromname", "id", "postitid", "initid", "locked", "revision", "wid", "cvid", "profid", "fromid", "owner", "domainid" |
| `document.properties.<prop>`       | Récupère la propriété indiquée                               |                                                                                                                               |
| `document.attributes`              | Récupère les valeurs et les valeurs affichable des attributs |                                                                                                                               |
| `document.attributes.<id>`         | Récupère la valeur d'un attribut particulier                 |                                                                                                                               |
| `document.family.structure`        | Récupère la structure de la famille                          |                                                                                                                               |

[trash]: #rest:52be10c1-9f46-456b-a22f-24909386567