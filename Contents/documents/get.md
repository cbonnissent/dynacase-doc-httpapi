# Consultation d'un document  {#core-ref:3fc0b4b4-149c-42a8-91b2-96799d668b9b}

## Url {#core-ref:f837fece-9f4e-4314-8668-64371a1c8d48}

Récupération du document l'identifiant `<id>`

    GET /api/families/<famName>/<id>

ou

    GET /api/documents/<id>

Exemple :

    GET /api/documents/1234.json


La différence entre la ressources `families` et `documents` est que
l'identifiant doit être de la famille indiquée sinon une erreur 404
(ressource non trouvée) est retournée.

L'identifiant du document peut être son nom logique, son identifiant numérique.

L'identifiant numérique permet de référencer une révision précise du document.
Le nom logique fait toujours référence à la dernière révision du document.

Note : Un document «supprimé» ne peut pas être récupéré.

## Content {#core-ref:fb4fe4a5-500f-4aef-8a12-5e2ef58fad23}

Le contenu de la requête est vide.

## Structure de retour {#core-ref:fb97f93b-920e-4604-b497-b8cfc32ed8a0}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:815970b5-c92e-4aad-b2d0-9c81655b9a81}

La partie `data` contient 2 champs :

`document.uri`
:  uri d'accès à la ressource consulté

`document.properties`
: liste des propriétés

`document.attributes`
: liste des attributs


Les attributs en visibilité "I" ne sont pas retournés. Leur existence n'est pas
dévoilée ni dans les données ni dans la structure.

Exemple :

    [php]
    {
       "success"  : "true",
       "messages" : [ ],
       "data" : {
          "document" : {
             "uri"        : "http;//www.example.org/api/documents/1256",
             "properties" : { 
                "id"     : 1256,
                "title"  : "Hello world",
                "locked" : 0,
                ....
             }
             "attributes" : { 
                "ba_title" : {
                  "value"        : "Hello world",
                  "displayValue" : "Hello world"
                },
                "ba_cost" : {
                  "value"        : "234",
                  "displayValue" : "234.00 €"
                }
             }
          }
       }
    }

### En cas d'échec {#core-ref:e73420e8-b6d1-4b71-849f-5316cb38e2d5}

Les raisons d'échecs spécifiques à cette requête sont 
<span class="fixme flag">À reprendre en précisant les retours selon la cas d'erreur.
Si cela fait doublon avec les pages [Error API0106](http://api.dynacase.org/code/API0106.html) pourquoi ne pas mettre simplement un lien ?</span>


|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Privilège insuffisant pour accéder au document |         403 | API0010    |
| Document supprimé                              |         404 | API0108    |
| Propriété demandé inexistante                  |         400 |            |
| Attribut demandé inexistant                    |         400 |            |

Exemple : 

Cas d'erreur de privilège

    [php]
    {
      "success" :false,
      "messages" : [{
            "type" : "error", 
            "contentText" : "Need acl \"view\" to access to the document",
            "contentHtml" : "",
            "code" : "API0106", 
            "uri" : "http://api.dynacase.org/code/API0106.html",
            "data" : null
            }],
    }


## Résultat partiel {#core-ref:d20b1df7-e888-4214-9359-7b633b96d91c}

Le document peut être retourné avec plus ou moins d'information.

* GET /documents/1234.json?fields=properties
* GET /documents/1234.json?fields=property.id,property.title,attributes
* GET /documents/1234.json?fields=property.id,property.title,attributes.values
* GET /documents/1234.json?fields=property.id,property.title,attribute.my_exemple
* GET /documents/1234.json?fields=property.id,property.title,attributes,family.structure


Par défaut : `fields=properties,attributes`

|           fields          |                        Signification                         |                                                           Remarques                                                           |
| ------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| `properties`              | Récupère l'ensemble des propriétés "visible"                 | "state", "fromname", "id", "postitid", "initid", "locked", "revision", "wid", "cvid", "profid", "fromid", "owner", "domainid" |
| `property.<prop>`         | Récupère la propriété indiqué                                |                                                                                                                               |
| `attributes`              | Récupère les valeurs et les valeurs affichable des attributs |                                                                                                                               |
| `attributes.value`        | Récupère les valeurs brutes                                  |                                                                                                                               |
| `attributes.displayValue` | Récupère les valeurs affichables                             | Les données nécessaires à l'affichage (variant suivent le type d'attribut)                                                    |
| `attribute.<id>`          | Récupère la valeur d'un attribut particulier                 | Utilise le champs  `attributes.value` et `attributes.displayValue` pour restreindre à la valeur affiché                       |
| `family.structure`        | Récupère la structure de la famille                          |                                                                                                                               |
