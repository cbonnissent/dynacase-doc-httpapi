# Suppression d'un document  {#core-ref:85b9c9f2-cb76-4d07-9525-ec90af2561e2}

## Url {#core-ref:99be046e-1858-4ffe-85a0-ab749c731265}

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

## Content {#core-ref:38a48a16-04f5-46ee-9d1d-20084cc5e680}

Le contenu de la requête est vide.

## Structure de retour {#core-ref:e093814e-4a9b-47c2-a8fe-190d5c25a4ae}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:75978575-35f5-4417-8895-83ba287e0286}

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

### En cas d'échec {#core-ref:d37dbd6c-bf8b-4430-985b-cbe86e8263c5}

Les raisons d'échecs spécifiques à cette requête sont 

|                      Raison                      | Status HTTP | Error Code |
| ------------------------------------------------ | ----------- | ---------- |
| Privilège insuffisant pour supprimer le document |         403 | API0011    |
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


