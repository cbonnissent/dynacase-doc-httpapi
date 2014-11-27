# Création d'un fichier  {#rest:5797255d-128d-4aa4-9c11-2c8195cca63d}

## Url {#rest:a1848339-b8df-412e-8cdb-9497d33dff42}

Création d'un fichier
:  

    POST /api/v1/temporaryFiles/

Ce fichier est temporairement stocké dans le vault. 
S'il n'est pas associé à un document, le fichier temporaire est supprimé au bout d'une période définie par le 
paramètre `CORE_TMPDIR_MAXAGE` .

## Content {#rest:10b0d2f6-4475-4ed9-99af-226f3955f4c7}

### Format urlEncoded {#rest:e6ab017f-713b-4642-8073-136abcddcb77}

Le contenu de la requête contient une variable (type file) contenant le contenu
du fichier

    -----------------------------70122309720638098951066485136 
    Content-Disposition: form-data; name="fi_file"; filename="my_file.jpeg" 
    Content-Type: image/jpeg
    ...

Le type de la requête est `application/x-www-form-urlencoded`.

<span class="flag inline nota-bene"></span> Ce format peut être utilisé directement depuis un formulaire HTML.


## Structure de retour {#rest:f7ffab19-822b-4e69-b1d9-02901f9f5ead}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:1532452f-7bfb-4e88-be80-4b00524b1d4d}

La partie `data` contient un objet `file` :


1.  `file.uri` : uri d'accès à la nouvelle ressource
1.  `file.reference` : référence pouvant être utilisant comme valeur
     dans un attribut de type file ou  image. 
1.  `file.size` : Taille du fichier en octets
1.  `file.fileName` : Nom du fichier (basename)
1.  `file.mime` : Type mime (système)
1.  `file.cdate` : Date de création
1.  `file.mdate` : Date de modification
1.  `file.downloadUrl` : Url de téléchargement du fichier

Exemple, création d'un fichier temporaire
:   

    [php]
    {"success" :             true,
        "messages" :         [],
        "data" :             {
            "file" : {
                "id" :           "14",
                "mime" :         "image\/jpeg",
                "size" :         "45860",
                "thumbnailUrl" : "resizeimg.php?img=vaultid=14&size=48",
                "reference" :    "image\/jpeg|14|BeMZfJLCAAAcUqj.jpg",
                "cdate" :        "2014-10-13 11:40:12",
                "downloadUrl" :  "file\/0\/14\/-\/-1\/BeMZfJLCAAAcUqj.jpg?cache=no&inline=no",
                "iconUrl" :      "resizeimg.php?img=Images\/mime-image.png&size=20",
                "fileName" :     "BeMZfJLCAAAcUqj.jpg"
            }
        },
        "exceptionMessage" : "",
        "headers" :          []
    }

## Utilisation {#rest:0bea83bb-6137-4ba3-af1f-24bcc864f005}

Une fois le fichier ajouté, vous pouvez l'associer à un document en le valuant comme tout autre attribut en utilisant 
soit la [création de document][create_document], soit la [modification de document][update_doc].

C'est la propriété `reference` que vous devez affecter à la valeur de l'attribut fichier.

[update_doc]: #rest:db2cb01a-7325-4f78-8cec-ceac9858caf2
[create_document]: #rest:e769b476-0033-407c-b453-4e8466e09975