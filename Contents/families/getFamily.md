# Propriétés d'une famille {#rest:6b195156-0cda-47c8-9a9a-04ec13562c9a}

## URL {#rest:b79ed7d5-2340-4e7b-9563-bd4d784f0e6a}

    GET /api/v1/families/<famName>

Récupération de la ressource décrivant la famille `<famName>`.

Exemple :

    GET /api/v1/families/my_cookbook

<span class="flag inline nota-bene"></span> Le nom de la famille est insensible à la casse.

## Content {#rest:27aa08ee-2108-47d1-90ba-e7c4cf4f608f}

Le contenu de la requête est vide.

## Structure de retour {#rest:cd937f64-a71c-4001-9e1b-55d7ca1893da}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:5bff5070-dd45-4bdf-a921-dd2a81d8b865}

La partie `data` contient 2 champs :

1.  `uri` : URI préférentielle d'accès à la ressource;
1.  `document.properties` : liste des valeurs des propriétés;

Exemple :

    [javascript]
    {
        "success": true,
        "messages": [],
        "data": {
            "document": {
                "properties": {
                    "id": 1065,
                    "title": "Articles",
                    "icon": "resizeimg.php?img=Images%2Farticle.png&size=24",
                    "initid": 1065,
                    "name": "MY_ARTICLE",
                    "revision": 0
                },
                "uri": "http://localhost/tmp32/api/v1/families/MY_ARTICLE.json"
            }
        }
    }


### En cas d'échec {#rest:bf7906b7-9690-44ec-8156-7a1cbb536486}

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Privilège insuffisant pour accéder au document |         403 | CRUD0201   |
| Document supprimé                              |         404 | CRUD0108   |
| Propriété demandé inexistante                  |         400 |            |
| Attribut demandé inexistant                    |         400 |            |

Exemple : 

Cas d'erreur de privilège

    [javascript]
    {"success" :             false,
        "messages" :         [
            {
                "type" :        "error",
                "contentText" : "Document \"1051\" access deny : Pas de privil\u00e8ge view pour le document famille [1051]",
                "contentHtml" : "",
                "code" :        "API0201",
                "uri" :         "",
                "data" :        null
            }
        ],
        "data" :             null,
        "exceptionMessage" : "Document \"1051\" access deny : Pas de privil\u00e8ge view pour le document famille [1051]"
    }

## Résultat partiel {#rest:789802cd-80ee-4b1d-92a2-eaa49da90046}

La ressource peut être retournée avec plus ou moins d'information.

* GET /api/v1/families/1234.json?fields=document.properties
* GET /api/v1/families/1234.json?fields=document.properties.id,document.properties.title,document.attributes
* GET /api/v1/families/1234.json?fields=document.properties.id,document.properties.title,document.attributes.my_exemple
* GET /api/v1/families/1234.json?fields=document.properties.id,document.properties.title,document.attributes,family.structure

Par défaut : `fields=document.properties`

|            fields            |               Signification                |                      Remarques                      |
| ---------------------------- | ------------------------------------------ | --------------------------------------------------- |
| `document.properties`        | Récupère les propriétés données par défaut | "id", "title", "icon", "initid", "name", "revision" |
| `document.properties.<prop>` | Récupère la propriété indiquée             |                                                     |
| `family.structure`           | Récupère la structure de la famille        |                                                     |