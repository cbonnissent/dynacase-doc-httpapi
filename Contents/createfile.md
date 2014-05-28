# Création d'un fichier 

## Url



    POST /api/file

Création d'un fichier temporaire. Ce fichier n'est pas dans le vault. Il est
stocké dans le répertoire temporaire et est supprimé lors du nettoyage des
fichiers temporaires.

La référence retournée peut être insérée comme valeur dans un attribut de type
file ou  image. Dans ce cas lors de l'enregistrement du document, le fichier
temporaire sera déplacé dans le vault.

    POST /api/documents/<docid>/file/<attrid>

Création d'un fichier dans le vault et insertion de celui-ci dans l'attribut.

    POST /api/documents/<docid>/file/<attrid>?index=<index>

Création d'un fichier dans le vault  et insertion de celui-ci dans l'attribut à
l'index indiqué pour les attributs multivalués.




## Content

### Format RAW

Le contenu de la requête doit contenir le contenu du fichier.

Le type de la requête est fonction du type de fichier envoyé

### Format urlEncoded

Le contenu de la requête contient une variable (type file) contenant le contenu
du fichier

    -----------------------------70122309720638098951066485136 
    Content-Disposition: form-data; name="fi_file"; filename="drakkar.jpeg" 
    Content-Type: image/jpeg

Le type de la requête est `application/x-www-form-urlencoded`.

Note : Ce format peut être utilisé directement depuis un formulaire HTML.


## Structure de retour

Le retour est une donnée JSON.

### En cas de réussite :

La partie `data` contient un champ `document` qui inclut 3 champs :

1.  `file.uri` : uri d'accès à la nouvelle ressource
1.  `file.reference` : référence pouvant être utilisant comme valeur
     dans un attribut de type file ou  image. 
1.  `file.size` : Taille du fichier en octets
1.  `file.fileName` : Nom du fichier (basename)
1.  `file.mime` : Type mime (système)
1.  `file.cdate` : Date de création
1.  `file.mdate` : Date de modification

Exemple :


Insertion dans un document

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
          "mdate" : "2014-07-23T23:43:23",
          "fileName" : "monimage.jpeg"
          "reference" : "image/jpeg|1256|monimage.jpg"
        }
      }
    }


Création d'un fichier temporaire :


    [php]
    {
      success :true,
      messages : [],
      data : {
        "file" : {
          "uri" : "http;//www.example.org/api/files/yduiehidezhi",
          "mime" : "image/jpeg",
          "size" : 567538,
          "cdate" : "2014-07-23T23:43:23",
          "mdate" : "2014-07-23T23:43:23",
          "fileName" : "monimage.jpeg"
          "reference" : "file://tmp/yduiehidezhi"
        }
      }
    }




### En cas d'échec

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

