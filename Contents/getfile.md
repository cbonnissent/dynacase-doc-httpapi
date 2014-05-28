# Consultation d'un fichier

## Url

    GET /api/documents/<docid>/file/<attrid>

Récupération des informations du fichier de l'attribut `<attrid` du document `<docid`.

Si l'attribut est multivalué un index est nécessaire.


    GET /api/documents/<docid>/file/<attrid>/<index>

Récupération des informations du  fichier de l'attribut `<attrid` du document `<docid` à l'index
`<index>`.

    GET /api/documents/<docid>/file/<fileid>

Récupération des informations du  fichier `<fileid` du document `<docid`


Exemple :

    GET /api/documents/1234.json



Note : Un fichier qui a été "enlevé" d'un document ne peut plus être téléchargé
depuis ce document.

## Content

Le contenu de la requête est vide.

## Structure de retour

Le retour est une donnée JSON.

### En cas de réussite :

La partie `data` contient un champ `file` qui inclut les champs suivants :

1.  `file.uri` : uri d'accès à la nouvelle ressource
1.  `file.reference` : référence pouvant être utilisant comme valeur
     dans un attribut de type file ou  image. 
1.  `file.size` : Taille du fichier en octets
1.  `file.fileName` : Nom du fichier (basename)
1.  `file.mime` : Type mime (système)
1.  `file.cdate` : Date de création
1.  `file.mdate` : Date de modification
1.  `file.downloadUrl` : Url de téléchargement du fichier



Les attributs en visibilité "I" ne sont pas retournés. Leur existence n'est pas
dévoilée ni dans les données ni dans la structure.

Exemple :

    [php]
    {
      success :true,
      messages : [],
      data : {
        "file" : {
          "uri" : "http;//www.example.org/api/documents/1234/files/1256",
          "mime" : "image/jpeg",
          "size" : 567538,
          "cdate" : "2014-07-23T23:43:23",
          "mdate" : "2014-07-24T06:13:02",
          "fileName" : "monimage.jpeg"
          "reference" : "image/jpeg|1256|monimage.jpg",
          "downloadUrl" : "http;//www.example.org/file/1234/1256/-1/fi_file/monimage.jpeg"
        }
      }
    }

### En cas d'échec

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Privilège insuffisant pour accéder au document |         403 | API0010    |
| Document supprimé                              |         404 | API0108    |
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