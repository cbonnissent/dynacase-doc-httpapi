# Suppression d'un document 

## Url

    DELETE /api/families/<famName>/<id>

Suppression d'un document de la famille `<famName>` ayant l'identifiant `<id>`

ou

    DELETE /api/documents/<id>

Suppression du document `<id>`

L'extension ".json" peut être ajoutée pour expliciter le format de sortie.

Exemple :

    DELETE /api/documents/1234.json

La suppression donne l'ordre de mettre le document dans la poubelle.

L'identifiant du document peut être son nom logique, son identifiant numérique.

Toute la lignée documentaire du document est mis à la poubelle.

La suppression "physique" n'est pas possible.

## Content

Le contenu de la requête est vide.

## Structure de retour

Le retour est une donnée JSON.

### En cas de réussite :

La partie `data` contient 1 champ :

1.  `document.uri` : uri d'accès à la ressource supprimé


Les attributs en visibilité "I" ne sont pas retournés. Leur existence n'est pas
dévoilée ni dans les données ni dans la structure.

Un document mis à la poubelle n'est plua accessible pas la ressource `documents`
mais reste accessible par la ressource `trash`.


Exemple :

    [php]
    {
      "success" :true,
      "messages" : [],
      "data" : {
        "document" : {
            "uri" : "http;//www.example.org/api/trash/1256"
          }
      }
    }

### En cas d'échec

Les raisons d'échecs spécifiques à cette requête sont 

|                      Raison                      | Status HTTP | Error Code |
| ------------------------------------------------ | ----------- | ---------- |
| Privilège insuffisant pour supprimer au document |         403 | API0011    |
| Document déjà supprimé                           |         403 | API0108    |

Exemple : 

Cas d'erreur de privilège

    [php]
    {
      "success" :false,
      "messages" : [{
            "type" : "error", 
            "contentText" : "Need acl \"DELETE\" to access to the document",
            "contentHtml" : "",
            "code" : "API0011", 
            "uri" : "http://api.dynacase.org/code/API0011.html",
            "data" : null
            }],
    }


