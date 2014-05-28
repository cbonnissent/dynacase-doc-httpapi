# Suppression d'un fichier 

## Url



    DELETE /api/file/<fileid>

Suppression d'un fichier temporaire. Le fichier temporaire est supprimé.

La référence retournée peut être insérée comme valeur dans un attribut de type
file ou  image. Dans ce cas lors de l'enregistrement du document, le fichier
temporaire sera déplacé dans le vault.

    DELETE /api/documents/<docid>/file/<attrid>

Suppression d'un fichier du vault. La référence au fichier est supprimé aussi.

Note : l'attribut doit être mono-valué.

Note : Le hook `postStore` du document est appelé.

    DELETE /api/documents/<docid>/file/<attrid>/<index>

Suppression d'un fichier du vault. La référence au fichier dans l'attribut
 est supprimé aussi.
 
Note : la ressource `families` peut aussi être utilisée à la place de
`documents`.


## Content

Aucun.


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

Exemple :


Suppression dans un document

    [php]
    {
      success :true,
      messages : [],
      data : null
        
      
    }


### En cas d'échec

Les raisons d'échecs spécifiques à cette requête sont 

|                      Raison                     | Status HTTP | Error Code |
| ----------------------------------------------- | ----------- | ---------- |
| Privilège insuffisant pour modifier le document |         403 | API0011    |


Exemple : 

Cas d'erreur de privilège

    [php]
    {
      "success" :false,
      "messages" : [{
            "type" : "error", 
            "contentText" : "Need acl \"edit\" to access to the document",
            "contentHtml" : "",
            "code" : "API0011", 
            "uri" : "http://api.dynacase.org/code/API0011.html",
            "data" : null
            }],
    }