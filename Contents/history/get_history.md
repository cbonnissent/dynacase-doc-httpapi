# Consultation des messages historique {#rest:9ae75dac-8eb5-4fa9-a608-7313b90fe33c}
## URL  {#rest:24535176-2898-4d2b-8d54-57caf7efc7f1}

    GET /api/v1/documents/<documentId>/history/

Récupération de l'historique d'un document ayant
l'identifiant `<documentId>`.

ou

    GET /api/v1/families/<famName>/documents/<documentId>/history/

Récupération de l'historique d'un document de la famille `<famName>` ayant
l'identifiant `<documentId>`.



## Content  {#rest:a3c6ab8a-a46f-4afc-8f9d-7066d7d141c1}

Le contenu de la requête est vide.

## Structure de retour  {#rest:e8d2e341-2cbe-4009-ad97-8a0b07245b09}

Le retour est une donnée JSON.

### En cas de réussite :  {#rest:0c60cc1d-4fe7-45fa-b655-980c6c673167}
    
La partie `data` contient les éléments suivants :


|   Clef  |               Description                |                                              Exemple                                               |
| ------- | ---------------------------------------- | -------------------------------------------------------------------------------------------------- |
| history | Liste des caractéristiques des révisions | [{documentId:13514, uri:api/v1/documents/7120/revisions/3, title:Document de test, fixed:false,…}] |
| filter: | Filtre utilisé                           | {slice:-1, offset:0, revision:3}                                                                   |
|         |                                          |                                                                                                    |

Chaque élément de l'historique `history` contient la structure suivante :

|      Clef     |            Description            |                                      Exemple                                       |
| ------------- | --------------------------------- | ---------------------------------------------------------------------------------- |
| documentId    | Identifiant numérique du document | 13514                                                                              |
| fixed:        | Indique si le document est figé   | false                                                                              |
| messages:     | Tableaux des messages             | [{uid:1, uname:O'reilly Master, date:2014-10-16 13:58:56, level:2, code:MODIFY,…}] |
| revision:     | Numéro de la version              | 3                                                                                  |
| revisionDate: | Date de la révision               | "2014-10-16 13:58:56"                                                              |
| state:        | État de la révision               | "zoo_realised"                                                                     |
| stateColor:   | Couleur de l'état                 | "#8870FF"                                                                          |
| stateLabel:   | Libelle de l'état                 | "Réalisé"                                                                          |
| title:        | Titre de la révision              | "Alberta"                                                                          |
| uri:          | Uri d'accès à la révision         | "api/v1/documents/7120/revisions/3"                                                |
| version:      | Version de la révision            | null                                                                               |

Chaque message contient la structure suivante :

|   Clef   |                       Description                        |                 Exemple                  |
| -------- | -------------------------------------------------------- | ---------------------------------------- |
| code     | Code du message                                          | "MODIFY"                                 |
| comment: | Message textuel                                          | "modification Pays, Propriétaire actuel" |
| date:    | Date d'enregistrement du message                         | "2014-10-16 13:58:56"                    |
| level:   | Niveau du message                                        | 4                                        |
| uid:     | Identifiant de l'utilisateur ayant enregistré le message | "2014-10-16 13:58:56"                    |
| uname:   | Nom de l'utilisateur ayant enregistré le message         | "Jean Martin"                            |
|          |                                                          |                                          |

Les niveaux (`level`) correspondent aux criticités suivantes :

| Level | Criticité |            Description             |
| ----- | --------- | ---------------------------------- |
|     1 | NOTICE    | Message d'information mineur       |
|     2 | INFO      | Message d'information (par défaut) |
|     4 | MESSAGE   | Message important                  |
|     8 | WARNING   | Avertissement                      |
|    16 | ERROR     | Erreur                             |
|       |           |                                    |

Exemple :


    GET api/v1/document/7120/history/

    [javascript]
    {"success" :             true,
        "messages" :         [],
        "data" :             
        filters: {
            offset: 0
            revision: -1
            slice: 2
        }
        history :[
           {
                documentId: 13514
                fixed: false
                messages: [{code: "MODIFY"
                            comment: "modification Pays, Propriétaire actuel"
                            date: "2014-10-16 13:58:56"
                            level: 2
                            uid: "123"
                            uname: "Jean Martin"}]
                revision: 3
                revisionDate: "2014-10-16 13:58:56"
                state: "zoo_realised"
                stateColor: "#8870FF"
                stateLabel: "Réalisé"
                title: "Alberta"
                uri: "api/v1/documents/7120/revisions/3"
                version: null
            },
           {
                documentId: 13513
                fixed: true
                messages: [{uid:"123", 
                            uname:"Jean Martin", 
                            date:"2014-10-16 13:58:33", 
                            level:4, 
                            code:"REVISION",…},…]
                revision: 2
                revisionDate: "2014-10-16 12:58:33"
                state: "zoo_realised"
                stateColor: "#8870FF"
                stateLabel: "Réalisé"
                title: "Boris"
                uri: "api/v1/documents/7120/revisions/2"
                version: null
            }, ...
            ]
        "exceptionMessage" : "",
        "headers" :          []
    }

### En cas d'échec  {#rest:b32007bd-500e-46ca-8734-85af9be2ccc0}

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Famille non trouvée                            |         404 | API0220    |
| Document non trouvé                            |         404 | API0200    |

Exemple : 

Cas d'erreur en cas de document non trouvé

    [javascript]
    data: null
    exceptionMessage: "Document "135214" not found"
    headers: []
    messages: 
     [{
        code: "API0200"
        contentHtml: ""
        contentText: "Document "135214" not found"
        data: null
        type: "error"
        uri: ""
      },{
        type:message, contentText:You can consult ?app=HTTPAPI_V1 to have info on the API,…}
        code: ""
        contentHtml: "You can consult <a href="?app=HTTPAPI_V1">the REST page</a> to have info on the API"
        contentText: "You can consult ?app=HTTPAPI_V1 to have info on the API"
        data: null
        type: "message"
        uri: ""
     }]
    success: false





## Filtres  {#rest:a882873e-dcb1-4866-a7dc-2de45a15aa00}

### slice

indique le nombre de révision maximum à retourner. 

Les révisions sont ordonnées par numéro décroissant, de la plus récente à la
plus ancienne.

Exemple : les 10 dernières révisions

    GET api/v1/document/1234/history/?slice=10

## offset

Index à partir duquel, les révisions sont retournées.

Exemple: Les révisions de 7 à 10.

    GET api/v1/document/1234/history/?slice=2&offset=7

## revision

Retourner l'historique d'une révision précise.

Exemple : Retourner la révision 3 

    GET api/v1/document/1234/history/?revision=3

La première révision porte le n°0.