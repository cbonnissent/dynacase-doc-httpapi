# Consultation d'un document  {#rest:1d7b939f-d5fc-4b57-b33f-d216913efc22}

## URL canonique {#rest:0e462204-b355-4e5a-81f2-4cf75cef3162}

    GET /api/v1/documents/<documentId>

Récupération de la dernière révision du document ayant l'identifiant `<documentId>`. 

L'extension ".json" peut être ajoutée pour expliciter le format de sortie.

Exemple :

    GET /api/v1/documents/1234.json

<span class="flag inline nota-bene"></span> L'identifiant ajouté peut-être soit :

* `initid`, `id de révision`, `lastid` du document,
* `name` : nom logique du document.

Dans tous les cas le document retourné est le dernier de sa lignée documentaire.

<span class="flag inline nota-bene"></span> Si vous souhaitez accéder à une révision précise du document, il faut utiliser
la collection [`/api/v1/documents/<documentId>/revisions/`][revision].

## Content {#rest:eac550a1-85ef-47d2-a28d-38f4604f4662}

Le contenu de la requête est vide.

## Structure de retour {#rest:c56944fc-8676-4114-aa60-e2ce4a63ef44}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:38df8680-739a-4120-872c-9e7bf7879029}

La partie `data` contient 3 champs :

1.  `document.uri` : uri d'accès à la ressource modifiée
1.  `document.properties` : liste des valeurs des propriétés
1.  `document.attributes` : liste des valeurs des attributs

Exemple :

    [javascript]
    {"success" :             true,
        "messages" :         [],
        "data" :             {
            "document" : {
                "uri" :        "api/v1/documents\/1057.json",
                "properties" : {
                    "title" :     "La culture des perles",
                    "state" :     null,
                    "name" :      null,
                    "icon" :      "resizeimg.php?img=Images%2Fdoc.png&size=32",
                    "fromname" :  "MY_ARTICLE",
                    [...]
                },
                "attributes" : {
                    "my_title" :            {"value" : "La culture des perles", "displayValue" : "La culture des perles"},
                    "my_description" :          {"value" : "Sur les bords de la rivière...", "displayValue" : "Sur les bords de la rivière..."},
                    "my_annexes" : [],
                    [...]
                }
            }
        }
    }

<span class="flag inline nota-bene"></span> 
Les valeurs retournées correspondent aux valeur de la vue de consultation
par défaut.

<span class="flag inline nota-bene"></span> Les attributs en visibilité "I" dans
la vue de consultation par défaut ne sont pas retournés. Leur existence n'est
pas dévoilée ni dans les données ni dans la structure.

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
| `document.properties`              | Récupère l'ensemble des propriétés "visibles"                | "state", "fromname", "id", "postitid", "initid", "locked", "revision", "wid", "cvid", "profid", "fromid", "owner", "domainid" |
| `document.properties.<prop>`       | Récupère la propriété indiquée                               |                                                                                                                               |
| `document.attributes`              | Récupère les valeurs et les valeurs affichable des attributs |                                                                                                                               |
| `document.attributes.<id>`         | Récupère la valeur d'un attribut particulier                 |                                                                                                                               |
| `document.family.structure`        | Récupère la structure de la famille                          |                                                                                                                               |

## Cache {#rest:02ea72c5-6bbf-4d63-ba31-2c3b33b68e51}

Dans le cadre du [cache][cache], le `Etag` est calculé à l'aide des éléments
suivants :

* identifiant du document,
* date de dernière modification,
* identifiant de l'utilisateur,
* identifiant des droits portés sur le document (vecteur de droits),
* langue sélectionnée.

L'ensemble de ces éléments sont concaténés et ensuite le [sha1][sha1] de cette
concaténation consitue le `Etag`.

## Autres URL d'accès {#rest:19b1ec4a-ddf2-4d5f-b24e-a4b3fdec3d26}

Vous pouvez aussi accéder à cette ressource via :

    GET /api/v1/families/<famName>/documents/<documentId>

Récupération de la dernière révision du document de la famille `<famName>` ayant
l'identifiant `<documentId>`.

<span class="flag inline nota-bene"></span> La différence entre les collection
`families` et `documents` est que pour la collection
`families/<famName>/documents/` l'identifiant doit être dans la famille indiquée
pour être retourné sinon une erreur 404 (ressource non trouvée) est retournée.

<span class="flag inline nota-bene"></span> Un document "supprimé" peut être 
récupéré via l'url [trash][trash].

<span class="flag inline nota-bene"></span> Les documents accédés via les
collections `families/<famName>/documents/` et `trash` possèdent aussi les sous-
collections :

* `history`,
* `revisions`.

[trash]: #rest:52be10c1-9f46-456b-a22f-24909386567
[cache]: #rest:804f8d68-acfa-4a35-bb41-27b2a27c14dc
[sha1]: https://fr.wikipedia.org/wiki/SHA-1
[revision]: #rest:eb7b6954-0945-4f02-8e10-16e69729c529