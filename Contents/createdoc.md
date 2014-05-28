# Création d'un document  {#core-ref:97b6c23a-e527-48b8-ab52-b5e869dadce7}

## Url {#core-ref:425df2c9-43bb-4abc-ab8f-a6a21f8f9978}

    POST /api/families/<famName>


Création d'un document de la famille `<famName>`

Exemple :

    POST /api/families/my_cookbook


Note : le nom de la famille est insensible à la casse.


## Content {#core-ref:9b0a3c4e-aef6-40cc-9592-9c443ee9d4eb}

### Format JSON {#core-ref:f1ee92a8-0654-44ce-934a-0688e070b922}

Le contenu de la requête doit contenir une donnée JSON avec la liste des attributs modifiés.

    {
      "attributes" : {
          <attrName> : {
            value : <newValue>
          }
      }
    }

Le type de la requête est `application/json`.

Exemple :

    {
          "attributes" : {
              "ba_ttle" : {"value" : "Hello world"},
              "ba_desc" : {"value" : "Nice Day"},
    }


Note : Toute donnée additionnelle sera ignorée.

Cette forme ne permet pas d'enregistrer directement des fichiers dans le document.

Pour enregistrer le fichier, il sera nécessaire de passer par la ressource
`file` qui retournera un identifiant valide qui pourra être utilisé comme valeur
d'attribut de type fichier.


### Format urlEncoded {#core-ref:d41e3675-c282-41c7-af91-beb057e942de}

Le contenu de la requête contient la liste des valeurs d'attributs à enregistrer.
Chaque variable (POST) est le nom de l'attribut (casse insensible).

Le type de la requête est `application/x-www-form-urlencoded`.

Note : Ce format peut être utilisé directement depuis un formulaire HTML.

Cette forme permet aussi d'enregistrer des fichiers dans le document.

## Structure de retour {#core-ref:807b6da9-dda2-4ab8-bcb9-7acd530f9e39}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:8e1bb239-6ed2-4ad0-992b-db803e68bd00}

La partie `data` contient un champ `document` qui inclut 3 champs :

1.  `document.uri` : uri d'accès à la nouvelle ressource
1.  `document.properties` : liste des valeurs des propriétés
1.  `document.attributes` : liste des valeurs des attributs

Exemple :

    [php]
    {
      success :true,
      messages : [],
      data : {
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
                    "displayValue : "Hello world"
                },
                "ba_cost" : {
                    "value" : 234
                    "displayValue : "234.00 €"
                }
              }
            }
      }
    }

### En cas d'échec {#core-ref:02aa0d5a-53e7-4ade-a378-0c2492f27df3}

Les raisons d'échecs spécifiques à cette requête sont 

|                             Raison                            | Status HTTP | Error Code |
| ------------------------------------------------------------- | ----------- | ---------- |
| Privilège insuffisant pour créer le document de cette famille |         403 | API0100    |
| Tentative de modification d'un attribut en visibilité I       |         403 | API0101    |
| Famille inconnue                                              |         404 | API0102    |
| preInsert erreur                                              |         400 | API0103    |
| Erreur de contrainte                                          |         400 | API0104    |
| Attribut obligatoire vide                                     |         400 | API0105    |
|                                                               |             |            |

Exemple : 

Cas d'erreur de contrainte

    [json]
    {
      "success" :false,
      "messages" : [{
            "type" : "error", 
            "contentText" : "Constraint error on attribut myattr, myattr2, myattr3",
            "contentHtml" : "",
            "code" : "API0104", 
            "uri" : "http://api.dynacase.org/code/API0104.html",
            "data" : [
                      { attribute : "myattr", 
                        label : "label de l'attribut", 
                        error : "contrainte non respectée"},
                      { attribute : "myattr2", 
                        label : "label de l'attribut", 
                        index : 3, // index si dans un tableau
                         error : "contrainte non respectée"} 
                      { attribute : "myattr3", 
                        label : "label de l'attribut", 
                        error : "contrainte non respectée",
                        suggests : ["Un", "Deux"]}, // avec suggestions
                   ]
            }],
    }


Cas d'erreur preInsert :

    {
      "success" :false,
      "messages" : [{
            "type" : "error", 
            "contentText" : "Reference must be greater than ceil",
            "contentHtml" : "",
            "code" : "API0103", 
            "uri" : "http://api.dynacase.org/code/API0103.html",
            "data" : null
            }],
    }



