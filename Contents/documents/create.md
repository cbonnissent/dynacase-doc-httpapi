# Création d'un document  {#core-ref:97b6c23a-e527-48b8-ab52-b5e869dadce7}

## Url {#core-ref:425df2c9-43bb-4abc-ab8f-a6a21f8f9978}

Création d'un document de la famille `<famName>`

    POST /api/families/<famName>


Exemple :

    POST /api/families/my_cookbook


Note : le nom de la famille est insensible à la casse.


## Content {#core-ref:9b0a3c4e-aef6-40cc-9592-9c443ee9d4eb}

### Format JSON {#core-ref:f1ee92a8-0654-44ce-934a-0688e070b922}

Le contenu de la requête doit contenir une donnée JSON avec la liste des attributs modifiés.

    [php]
    {
      "attributes" : {
          "<attrName>" : {
            "value" : "<newValue>"
          }
      }
    }

Le type de la requête est `application/json`.

Exemple :

    [php]
    {
          "attributes" : {
              "ba_ttle" : {"value" : "Hello world"},
              "ba_desc" : {"value" : "Nice Day"},
    }


Note : Toute donnée additionnelle est ignorée.

Cette forme ne permet pas d'enregistrer directement des fichiers dans le document.

Pour enregistrer le fichier, il est nécessaire de passer par la [ressource
`file`](#core-ref:5797255d-128d-4aa4-9c11-2c8195cca63d) qui retourne un identifiant valide
à utiliser comme valeur d'attribut de type fichier.


### Format urlEncoded {#core-ref:d41e3675-c282-41c7-af91-beb057e942de}

Le contenu de la requête contient la liste des valeurs des attributs à enregistrer.
Chaque variable (POST) est le nom de l'attribut (casse insensible).

Le type de la requête est `application/x-www-form-urlencoded`.

Note : Ce format peut être utilisé directement depuis un formulaire HTML.

Cette forme permet aussi d'enregistrer des fichiers dans le document.

## Structure de retour {#core-ref:807b6da9-dda2-4ab8-bcb9-7acd530f9e39}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:8e1bb239-6ed2-4ad0-992b-db803e68bd00}

La partie `data` contient un champ `document` qui inclut 3 champs :

`document.uri`
:  uri d'accès à la nouvelle ressource

`document.properties`
:  liste des valeurs des propriétés

`document.attributes`
:  liste des valeurs des attributs

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

## Erreurs {#core-ref:02aa0d5a-53e7-4ade-a378-0c2492f27df3}

Les erreur spécifiques à cette requête sont :

Dynacase **API0100** / HTTP **403**
:  Privilège insuffisant pour créer le document de cette famille

Dynacase **API0101** / HTTP **403**
:  Tentative de modification d'un attribut en visibilité I

Dynacase **API0102** / HTTP **404**
:  Famille inconnue

Dynacase **API0103** / HTTP **400**
:  Erreur lors de l'exécution du `preInsert`

Dynacase **API0104** / HTTP **400**
:  Erreur lors de la vérification d'une contrainte
   ... <span class="flag fixme">Informations fournies, attributs et alternatives ? Je pens qu'il faut présenter le retour dans ce cas</span>
   
        [php]
	    ... json retourné ...


Dynacase **API0105** / HTTP **400**
:  Un attribut obligatoire n'est pas valué  
   ... <span class="flag fixme">Comment est identifié l'attribut ? Même remarque que pour le point précédent</span>
   
        [php]
	    ... json retourné ...



Exemple : 
<span class="fixme flag"> Ce n'est pas un exemple, le mot clé `suggests` et, plus généralement, ceux liés aux retours d'erreur doivent être présentés</span>
Cas d'erreur de contrainte

    [php]
    {
      "success" :false,
      "messages" : [
          {
             "type"        : "error", 
             "contentText" : "Constraint error on attribut myattr, myattr2, myattr3",
             "contentHtml" : "",
             "code"        : "API0104", 
             "uri"         : "http://api.dynacase.org/code/API0104.html",
             "data"        : [
                {
                   "attribute" : "myattr", 
                   "label"     : "label de l'attribut", 
                   "error"     : "contrainte non respectée"
                }, {
                   "attribute" : "myattr2", 
                   "label"     : "label de l'attribut", 
                   "index"     : 3, // index si dans un tableau
                   "error"     : "contrainte non respectée"
                }, {
                   "attribute" : "myattr3", 
                   "label"     : "label de l'attribut", 
                   "error"     : "contrainte non respectée",
                   "suggests"  : ["Un", "Deux"] // avec suggestions
                }
             ]
          }
       ]
    }


Cas d'erreur preInsert :

    [php]
    {
       "success" :false,
       "messages" : [
          {
             "type"        : "error", 
             "contentText" : "Reference must be greater than ceil",
             "contentHtml" : "",
             "code"        : "API0103", 
             "uri"         : "http://api.dynacase.org/code/API0103.html",
             "data"        : null
          }
       ]
    }



