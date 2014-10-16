# Suppression d'un document  {#rest:3358b3bd-bdf6-44ef-b1d7-438f8eb21067}

## URL {#rest:f992edec-ca5c-4fa1-b829-f88d9e17347d}

    DELETE /api/v1/families/<famName>/documents/<id>

Suppression d'un document de la famille `<famName>` ayant l'identifiant `<id>`

ou

    DELETE /api/v1/documents/<id>

Suppression du document `<id>`

L'extension ".json" peut être ajoutée pour expliciter le format de sortie.

Exemple :

    DELETE /api/v1/documents/1234.json

La suppression donne l'ordre de mettre le document dans la poubelle.

L'identifiant du document peut être son nom logique, son identifiant numérique.

Toute la lignée documentaire du document est mise à la poubelle.

La suppression "physique" (réelle suppression de la ligne en base de données) n'est pas possible.

## Content {#rest:dd7728aa-309c-42f1-a496-9172a929be9f}

Le contenu de la requête est vide.

## Structure de retour {#rest:70a8207a-abd0-498c-b788-48b86a274c3a}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:305ab52d-2313-4594-b524-736875acd1b6}

La partie `data` contient 1 champ :

La partie `data` contient 3 champs :

1.  `document.uri` : uri d'accès à la ressource supprimée;
1.  `document.properties` : liste des valeurs des propriétés du document supprimé;
2.  `document.attributes` : liste des valeurs des attributs du document supprimé.

Les attributs en visibilité "I" ne sont pas retournés. Leur existence n'est pas
dévoilée ni dans les données ni dans la structure.

Un document mis à la poubelle n'est plus accessible via la ressource `documents`
mais reste accessible par la ressource `trash`.

Exemple :

    [javascript]
    {"success" :             true,
        "messages" :         [],
        "data" :             {
            "document" : {
                "uri" :        "api\/v1\/trash\/1057.json",
                "properties" : {
                    "title" :     "[123",
                    [...]
                },
                "attributes" : {
                    "test_all_element_title" : {"value" : "[123", "displayValue" : "[123"},
                    [...]
                }
            }
        },
        "exceptionMessage" : ""
    }

### En cas d'échec {#rest:0e94bbdd-2051-436e-af38-fe718a1e87ee}

Les raisons d'échecs spécifiques à cette requête sont 

|                      Raison                      | Status HTTP | Error Code |
| ------------------------------------------------ | ----------- | ---------- |
| Privilège insuffisant pour supprimer le document |         403 | API0216    |
| Erreur lors de la suppression                    |         400 | API0215    |
| Document déjà supprimé                           |         404 | API0219    |

Exemple : 

Cas d'erreur de privilège

    [javascript]
    {"success" :             false,
        "messages" :         [
            {
                "type" :        "error",
                "contentText" : "Document \"1057\" deleted",
                "contentHtml" : "",
                "code" :        "API0219",
                "uri" :         "",
                "data" :        null
            }
        ],
        "data" :             null,
        "exceptionMessage" : "Document \"1057\" deleted"
    }

