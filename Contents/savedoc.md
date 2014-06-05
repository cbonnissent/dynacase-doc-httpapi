# Modification d'un document  {#core-ref:2d248523-ddf4-4654-bd5d-6e5af3b5056d}

## Url {#core-ref:d8e16308-ddc2-4847-bbf7-6195abb4ba6d}

Modification d'un document de la famille `<famName>`

    PUT /api/families/<famName>/<id>

ou

    PUT /api/documents/<id>

Modification du document <id>

Exemple :

    PUT /api/documents/1234.json


Note : la différence entre la ressources `families` et `documents` est que
l'identifiant doit être dans la famille indiqué pour être modifié sinon une
erreur 404 (ressource non trouvée) sera retournée.

L'identifiant du document peut être son nom logique, son identifiant numérique.
L'identifiant numérique peut référencer n'importe quelle révision du document. 
Dans tous les cas, la modification porte sur la dernière révision du document.

## Content {#core-ref:c215cb73-d27f-4044-9385-68d21f35c7b3}

### Format JSON {#core-ref:6a3a0d32-caea-4cc1-aeb0-f3fba2923e89}

Le contenu de la requête doit contenir une donnée JSON avec la liste des attributs modifiés.

    [php]
    {
       "attributes" : {
          "<attrName>" : {
             "value" : "<newValue>"
          }
       }
    }
Le type de la requête est `application/json`.<span class="flag fixme">Est-ce utile ?</span>

Exemple :

    [php]
    {
       "attributes" : {
          "ba_title" : { "value" : "Hello world" },
          "ba_desc"  : { "value" : "Nice Day" }
       }
    }


Note : Toute donnée additionnelle sera ignorée.

### Format urlEncoded {#core-ref:e9dd728c-1737-4694-a326-842edfd80187}

<span class="flag fixme">Déjà dit lors de la création. C'est a priori un fonctionnement général, à remonter au chapitre de présentation de l'API</span>

Le contenu de la requête contient la liste des valeurs d'attributs à enregistrer.
Chaque variable (PUT) est le nom de l'attribut (casse insensible).

Le type de la requête est `application/x-www-form-urlencoded`.

Note : Ce format peut être utilisé directement depuis un formulaire HTML.

Cette forme permet aussi d'enregistrer des fichiers dans le document.

## Structure de retour {#core-ref:e98d49ba-4bb2-4b82-9ae2-6c778a2cf8c9}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:764f8c44-20bb-4b92-a407-6cbaf2bc8652}

La partie `data` contient 3 champs :


`document.uri`
:  uri d'accès à la ressource modifiée

`document.properties`
:  liste des valeurs des propriétés

`document.attributes`
:  liste des valeurs des attributs

`changes`
:  liste des attributs modifiés, avec les anciennes et nouvelles valeurs<span class="flag fixme">Ça sert à quoi ?</span>

Exemple :

    [php]
    {
       "success"  : "true",
       "messages" : [ ],
       "data"     : {
          "document"   : {
             "uri"        : "http;//www.example.org/api/documents/1256",
             "properties" : { 
                "id"     : "1256",
                "title"  : "Hello world",
                "locked" : "0",
                   ....
             },
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
          },
          "changes" : {
              "my_name" : { "before" : "Dupont", "after" : "Dupond" }, 
              "my_date" : { "before" : "",       "after" : "2012-02-22" }
          }
       }
    }

### En cas d'échec {#core-ref:1439da9e-919c-4b32-9242-bd18ad2a487a}

<span class="fixme flag">À reprendre en précisant les retours selon la cas d'erreur.
Si cela fait doublon avec les pages [Error API0106](http://api.dynacase.org/code/API0106.html) pourquoi ne pas mettre simplement un lien ?</span>

Les raisons d'échecs spécifiques à cette requête sont 

|                          Raison                         | Status HTTP | Error Code |
| ------------------------------------------------------- | ----------- | ---------- |
| Privilège insuffisant pour modifier le document         |         403 | API0106    |
| Tentative de modification d'un attribut en visibilité I |         403 | API0101    |
| Document supprimé                                       |         403 | API0108    |
| Document verrouillé                                     |         403 | API0109    |
| preUpdate erreur                                        |         400 | API0107    |
| Erreur de contrainte                                    |         400 | API0104    |
| Attribut obligatoire vide                               |         400 | API0105    |
|                                                         |             |            |

Exemple : 

Cas d'erreur de privilège

    [php]
    {
       "success"  : "false",
       "messages" : [
       {
             "type"        : "error", 
             "contentText" : "Need acl \"edit\" to modify the document",
             "contentHtml" : "",
             "code"        : "API0106", 
             "uri"         : "http://api.dynacase.org/code/API0106.html",
             "data"        : null
          }
       ]
    }

