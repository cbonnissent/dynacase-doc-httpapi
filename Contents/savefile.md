# Modification d'un fichier  {#core-ref:4bd2f27b-8457-403e-be9b-8ff036f15b0f}

## Url {#core-ref:0d6666fa-77fd-4299-9205-c7a7659ee4b5}



    PUT /api/file/<fileid>

Modification d'un fichier temporaire. Le fichier temporaire est remplacé.

La référence retournée peut être insérée comme valeur dans un attribut de type
file ou  image. Dans ce cas lors de l'enregistrement du document, le fichier
temporaire sera déplacé dans le vault.

    PUT /api/documents/<docid>/file/<attrid>

Modification d'un fichier du vault. La référence au fichier dans l'attribut
reste inchangé.

Note : l'attribut doit être mono-valué.

Note : Le hook `postStore` du document est appelé.

    PUT /api/documents/<docid>/file/<attrid>/<index>

Modification d'un fichier du vault. La référence au fichier dans l'attribut
reste inchangé.

Note : la ressource `families` peut aussi être utilisée à la place de
`documents`.


## Content {#core-ref:5ef1a224-5b25-4ffd-92c1-00af7f570de7}

### Format RAW {#core-ref:b5153f49-e840-4b31-8ee8-afedf31f84ad}

Le contenu de la requête doit contenir le contenu du fichier.

Le type de la requête est fonction du type de fichier envoyé

### Format urlEncoded {#core-ref:38978d61-6a1b-455e-b1d3-dc5a6ce0c38a}

Le contenu de la requête contient une variable (type file) contenant le contenu
du fichier

    -----------------------------70122309720638098951066485136 
    Content-Disposition: form-data; name="fi_file"; filename="drakkar.jpeg" 
    Content-Type: image/jpeg

Le type de la requête est `application/x-www-form-urlencoded`.

Note : Ce format peut être utilisé directement depuis un formulaire HTML.


## Structure de retour {#core-ref:1d64b9e5-fbc6-4f29-99d1-accfa9fe90cb}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:128a888e-a46f-430c-9276-6fa62402d600}

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

Exemple :


Modification dans un document

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






### En cas d'échec {#core-ref:42ceb481-6692-4afb-b2e7-54a19f5731a4}

Les raisons d'échecs spécifiques à cette requête sont 

|                             Raison                             | Status HTTP | Error Code |
| -------------------------------------------------------------- | ----------- | ---------- |
| Privilège insuffisant pour insérer le fichier dans le document |         403 | API0106    |
| Tentative de modification d'un attribut en visibilité I        |         403 | API0101    |
| Famille inconnue                                               |         404 | API0102    |
| preInsert erreur                                               |         400 | API0103    |
| Erreur de contrainte                                           |         400 | API0104    |
| Plus d'espace disponible                                       |         507 | API0200    |
|                                                                |             |            |

Exemple : 

Cas d'erreur de contrainte


    [php]
    {
      "success" :false,
      "messages" : [{
            "type" : "error", 
            "contentText" : "Need acl \"edit\" to insert file",
            "contentHtml" : "",
            "code" : "API0106", 
            "uri" : "http://api.dynacase.org/code/API0106.html",
            "data" : null
            }],
    }

