# Consultation d'un document 

## Url

    GET /api/families/<famName>/<id>

Récupération d'un document de la famille `<famName>` ayant l'identifiant `<id>`

ou

    GET /api/documents/<id>

Récupération du document `<id>`

L'extension ".json" peut être ajoutée pour expliciter le format de sortie.

Exemple :

    GET /api/documents/1234.json


Note : la différence entre la ressources `families` et `documents` est que
l'identifiant doit être dans la famille indiquée pour être modifié sinon une
erreur 404 (ressource non trouvée) sera retournée.

L'identifiant du document peut être son nom logique, son identifiant numérique.

L'identifiant numérique permet de référencer une révision précise du document.
Le nom logique fait toujours référence à la dernière révision du document.


Note : Un document "supprimé" ne peut pas être récupéré.

## Content

Le contenu de la requête est vide.

## Structure de retour

Le retour est une donnée JSON.

### En cas de réussite :

La partie `data` contient 2 champs :

1.  `document.uri` : uri d'accès à la ressource modifiée
1.  `document.properties` : liste des valeurs des propriétés
2.  `document.attributes` : liste des valeurs des attributs


Les attributs en visibilité "I" ne sont pas retournés. Leur existence n'est pas
dévoilée ni dans les données ni dans la structure.

Exemple :

    [php]
    {
      "success" :true,
      "messages" : [],
      "data" : {
        "document" : {
            "uri" : "http;//www.example.org/api/documents/1256",
            "properties" : { 
               "id" : 1256,
               "title" : "Hello world",
               "locked" : 0,
               ....
             }
            "attributes" : { 
              "ba_title" : {
                  "value" : "Hello world"
                  "displayValue" : "Hello world"
              },
              "ba_cost" : {
                  "value" : 234
                  "displayValue" : "234.00 €"
              }
            }
          }
      }
    }

### En cas d'échec

Les raisons d'échecs spécifiques à cette requête sont 

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


## Résultat partiel

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