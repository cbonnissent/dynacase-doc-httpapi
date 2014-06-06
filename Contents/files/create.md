# Création d'un fichier  {#core-ref:5797255d-128d-4aa4-9c11-2c8195cca63d}

## Url {#core-ref:a1848339-b8df-412e-8cdb-9497d33dff42}

Création d'un fichier
:  

    POST /api/file

Ce fichier n'est pas dans le vault.
<div class="flag fixme">
Ceci pose un problème. Contrairement à des fichiers dans le Vault, ces fichiers temporaires ne seraient pas accessibles sur des architectures composées de plusieurs serveurs applicatifs. Pourquoi ne pas les créer dans le Vault (orphelin) ?
</div>
Il est stocké dans le répertoire temporaire et est supprimé lors du nettoyage des
fichiers temporaires.

Utilisation du fichier dans un document
:  L'identifiant du fichier retourné est utilisé pour valoriser un attribut de type
file ou  image. 

    POST /api/documents/<docid>/file/<attrid>



Ajout d'un fichier dans un document
:  Il est possible de créer un fichier et de l'associer à un document par une requête unique.


    POST /api/documents/<docid>/file/<attrid>[/<index>]

Le fichier est créé dans le Vault et est utilisé pour valoriser l'attribut `<attrid>` du document `<docid>`.

Si l'attribut `<attrid>` est multi-valué, l'index `<index>` est précisé.

<span class="flag fixme">préciser comment on remplace un index existant et comment on ajoute un index.</span>


<span class="flag inline nota-bene"></span> Le hook `postStore` du document est appelé.

<span class="flag inline nota-bene"></span> La ressource `families` peut aussi être utilisée à la place de
`documents`. 


## Content {#core-ref:10b0d2f6-4475-4ed9-99af-226f3955f4c7}

### Format RAW {#core-ref:5f1e437e-5696-4d71-bde1-71a57511933b}

Le contenu de la requête doit contenir le contenu du fichier.<span class="flag fixme">comment ?</span>

Le type de la requête est fonction du type de fichier envoyé.<span class="flag fixme">pas compris ?</span>

### Format urlEncoded {#core-ref:e6ab017f-713b-4642-8073-136abcddcb77}

Le contenu de la requête contient une variable (type file) contenant le contenu
du fichier

    -----------------------------70122309720638098951066485136 
    Content-Disposition: form-data; name="fi_file"; filename="drakkar.jpeg" 
    Content-Type: image/jpeg
    ...

Le type de la requête est `application/x-www-form-urlencoded`.

<span class="flag inline nota-bene"></span> Ce format peut être utilisé directement depuis un formulaire HTML.


## Structure de retour {#core-ref:f7ffab19-822b-4e69-b1d9-02901f9f5ead}

Le retour est une donnée JSON.

### En cas de réussite : {#core-ref:1532452f-7bfb-4e88-be80-4b00524b1d4d}

La partie `data` contient un objet `file` :


1.  `file.uri` : uri d'accès à la nouvelle ressource
1.  `file.reference` : référence pouvant être utilisant comme valeur <span class="flag fixme">Pourquoi pas file.id et identifiant de fichier ? </span>
     dans un attribut de type file ou  image. 
1.  `file.size` : Taille du fichier en octets
1.  `file.fileName` : Nom du fichier (basename)
1.  `file.mime` : Type mime (système)
1.  `file.cdate` : Date de création
1.  `file.mdate` : Date de modification
1.  `file.downloadUrl` : Url de téléchargement du fichier

Exemple, insertion dans un document
:   

    [php]
    {
       "success"  : "true",
       "messages" : [ ],
       "data"     : {
          "file" : {
             "uri"         : "http;//www.example.org/api/documents/1234/files/1256",
             "mime"        : "image/jpeg",
             "size"        : 567538,
             "cdate"       : "2014-07-23T23:43:23",
             "mdate"       : "2014-07-23T23:43:23",
             "fileName"    : "monimage.jpeg"
             "reference"   : "image/jpeg|1256|monimage.jpg",
             "downloadUrl" : "http;//www.example.org/file/1234/1256/-1/fi_file/monimage.jpeg"
          }
       }
    }


Exemple, création d'un fichier temporaire
:  


    [php]
    {
       "success"  : "true",
       "messages" : [ ],
       "data"     : {
          "file" : {
             "uri"         : "http;//www.example.org/api/files/yduiehidezhi",
             "mime"        : "image/jpeg",
             "size"        : 567538,
             "cdate"       : "2014-07-23T23:43:23",
             "mdate"       : "2014-07-23T23:43:23",
             "fileName"    : "monimage.jpeg"
             "reference"   : "file://tmp/yduiehidezhi",
             "downloadUrl" : null
          }
       }
    }

Le fichier temporaire ne peut pas être téléchargé.<span class="flag fixme">Pourquoi ?</span>


### En cas d'échec {#core-ref:c97d3fb9-aefb-46a1-ac11-0d8646a0c7ac}

Les erreurs spécifiques à cette requête sont :

Dynacase **API0106** / HTTP **403**
:  Privilège insuffisant pour insérer le fichier dans le document

Dynacase **API0102** / HTTP **404**
:  Famille inconnue

Dynacase **API0101** / HTTP **403**
:  Tentative de modification d'un attribut en visibilité I

Dynacase **API0103** / HTTP **400**
:  Erreur lors du `preInsert`

Dynacase **API0104** / HTTP **400**
:  Erreur lors du contrôle d'une contrainte

Dynacase **API0200** / HTTP **500**
:  Pas d'espace suffisant pour le stockage du fichier


Exemple, cas d'erreur de contrainte
:  

    [php]
    {
       "success" : "false",
       "messages" : [
          {
             "type"        : "error", 
             "contentText" : "Need acl \"edit\" to insert file",
             "contentHtml" : "",
             "code"        : "API0106", 
             "uri"         : "http://api.dynacase.org/code/API0106.html",
             "data"        : "null"
          }
       ]
    }

