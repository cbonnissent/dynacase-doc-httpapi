# Consultation d'un fichier {#core-ref:fa90f9f7-0f35-46b3-a09a-b49e6a75ab5d}

## Url {#core-ref:0e06d077-db21-4a00-99bf-f7348acc0205}

    GET /api/documents/<docid>/file/<attrid>

Récupération des informations du fichier de l'attribut `<attrid` du document
`<docid`.

Si l'attribut est multivalué un index est nécessaire.


    GET /api/documents/<docid>/file/<attrid>/<index>

Récupération des informations du  fichier de l'attribut `<attrid` du document
`<docid` à l'index `<index>`.

    GET /api/documents/<docid>/file/<fileid>

Récupération des informations du  fichier `<fileid` du document `<docid`


Exemple :

    GET /api/documents/1234.json



Note : Un fichier qui a été "enlevé" d'un document ne peut plus être téléchargé
depuis ce document.

## Content {#core-ref:f066ebc6-fa25-4a2c-8a7a-e05aa0e8124a}

Le contenu de la requête est vide.

## Structure de retour {#core-ref:258dffeb-97f7-432a-8322-f4dbb1e688eb}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:c6e25941-e31f-450e-957e-117d7d60cde4}

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

### En cas d'échec {#core-ref:752b6ed1-bda0-4ddb-b8cf-d5e9f57250bb}

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


