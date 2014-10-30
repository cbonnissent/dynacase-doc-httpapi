# Consultation d'une vue d'un document  {#rest:a2055321-27c0-4e15-b9c4-e4cfe2ff445a}

## URL canonique {#rest:7937101b-1716-4831-a316-c266fb23fd55}

    GET /api/v1/documents/<documentId>/views/<viewId>

Consultation de la dernière révision du document ayant l'identifiant `<documentId>` dans la vue `<viewId>`. 

L'extension ".json" peut être ajoutée pour expliciter le format de sortie.

Exemple :

    GET /api/v1/documents/<documentId>/views/<viewId>.json

<span class="flag inline nota-bene"></span> L'identifiant ajouté peut-être soit :

* l'`initid` du document,
* le nom logique du document.

Dans tous les cas le document retourné est le dernier de sa lignée documentaire.

<span class="flag inline nota-bene"></span> Tout document possède au moins deux vues :

* une vue par défaut de consultation : `#consultView`,
* une vue par défaut d'édition : `#editionView`.

Ces vues sont soit :

* si le document n'a pas de contrôle de vue, les valeurs des attributs et les visibilités par défaut,
* si le document a un contrôle de vue, les valeurs des attributs et les visibilités de la vue dont l'utilisateur possède les droits.

## Content {#rest:89e19b25-4974-4e46-bbc4-2b128224acb2}

Le contenu de la requête est vide.

## Structure de retour {#rest:a0e91e60-b582-4266-81ba-65b4a93a5c84}

Le retour est une donnée JSON.

### En cas de réussite : {#rest:36417436-0159-4a2e-a452-db5b13007d81}

La partie `data` contient plusieurs champs :

1.  `view.uri` : uri d'accès à la ressource modifiée
1.  `document.properties` : liste des valeurs des propriétés
1.  `view.attributes` : liste des valeurs des attributs
1.  `view.structure` : structure du document (liste des attributs encadrants et non encadrants avec leur visibilités)

Exemple :




### En cas d'échec {#rest:f969045d-a236-4350-b25d-177fb64268a9}

Les raisons d'échecs spécifiques à cette requête sont 

|                     Raison                     | Status HTTP | Error Code |
| ---------------------------------------------- | ----------- | ---------- |
| Document non trouvé                            |         404 | API0200    |
| Privilège insuffisant pour accéder au document |         403 | API0201    |
| Document supprimé                              |         404 | API0219    |
| Propriété demandée inexistante                 |         400 | API0202    |
| Attribut demandé inexistant                    |         400 | API0218    |

Exemple : 

Cas d'erreur de document non trouvé


## Résultat partiel {#rest:e3714425-5b3d-4d35-8ca6-ba2a578e44fa}

Le document peut être retourné avec plus ou moins d'information.

* GET /documents/1234/views/external_view.json?fields=document.properties
* GET /documents/1234/views/external_view.json?fields=document.properties.id,document.properties.title,view.attributes
* GET /documents/1234/views/external_view.json?fields=document.properties.id,document.properties.title,view.attributes.my_exemple
* GET /documents/1234/views/external_view.json?fields=document.properties.id,document.properties.title,view.attributes,view.structure

Par défaut : `fields=document.properties,view.attributes,view.struture`

|           fields                   |                        Signification                         |                                                           Remarques                                                           |
| ---------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| `document.properties`              | Récupère l'ensemble des propriétés "visibles"                | "state", "fromname", "id", "postitid", "initid", "locked", "revision", "wid", "cvid", "profid", "fromid", "owner", "domainid" |
| `document.properties.<prop>`       | Récupère la propriété indiquée                               |                                                                                                                               |
| `view.attributes`                  | Récupère les valeurs et les valeurs affichable des attributs |                                                                                                                               |
| `view.attributes.<id>`             | Récupère la valeur d'un attribut particulier                 |                                                                                                                               |
| `view.structure`                   | Récupère la structure de la vue                              |                                                                                                                               |

## Cache {#rest:17b709ce-5360-481c-a2e9-c20b135edd88}

Dans le cadre du [cache][cache], le `Etag` est calculé à l'aide des éléments suivants :

* identifiant du document,
* date de dernière modification,
* identifiant de l'utilisateur,
* identifiant des droits portés sur le document (vecteur de droits),
* langue sélectionnée.

L'ensemble de ces éléments sont concaténés et ensuite le [sha1][sha1] de cette concaténation consitue le `Etag`.

## Autres URL d'accès {#rest:55b07008-4bc2-44a0-aa44-0119d9905f4b}

Vous pouvez aussi accéder à cette ressources via :

    GET /api/v1/families/<famName>/documents/<documentId>/views/<viewId>

Récupération de la dernière révision du document de la famille `<famName>`  ayant l'identifiant `<documentId>` dans la vue `<viewId>`.

<span class="flag inline nota-bene"></span> La différence entre les collection `families` et `documents` est que pour
la collection `families/<famName>/documents/` l'identifiant doit être dans la famille indiquée pour être retourné sinon une
erreur 404 (ressource non trouvée) est retournée.

<span class="flag inline nota-bene"></span> Un document "supprimé" peut être récupéré via l'url [trash][trash].

<span class="flag inline nota-bene"></span> Les documents accédés via les collections `families/<famName>/documents/` et `trash` possèdent aussi les sous-collections :

* `history`,
* `revisions`.

[trash]: #rest:52be10c1-9f46-456b-a22f-24909386567
[cache]: #rest:804f8d68-acfa-4a35-bb41-27b2a27c14dc
[sha1]: https://fr.wikipedia.org/wiki/SHA-1
[revision]: #rest:eb7b6954-0945-4f02-8e10-16e69729c529