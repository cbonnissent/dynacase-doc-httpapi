# Résumé de l'API {#rest:39742615-6b36-4b23-8449-3a9019b9afa8}

## Carte de l'api {#rest:cf8c475b-1ea5-474d-bc74-f5902f9d00fb}

|  Type  |                           URL                                         |               Implanté               |                       Signification                        |
| ------ | --------------------------------------------------------------------  | ------------------------------------ | ---------------------------------------------------------- |
| GET    | */api/v1/documents/*                                                  | Future version                       | Liste de documents                                         |
| PUT    | */api/v1/documents/*                                                  | N/A                                  | N/A                                                        |
| POST   | */api/v1/documents/*                                                  | N/A                                  | N/A                                                        |
| DELETE | */api/v1/documents/*                                                  | N/A                                  | N/A                                                        |
|        |                                                                       |                                      |                                                            |
| GET    | **/api/v1/documents/&lt;docid&gt;**                                   | Oui                                  | [Récupération d'un document][GETDOC]                       |
| PUT    | **/api/v1/documents/&lt;docid&gt;**                                   | Oui                                  | [Mise à jour d'un document][PUTDOC]                        |
| POST   | **/api/v1/documents/&lt;docid&gt;**                                   | N/A                                  | N/A                                                        |
| DELETE | **/api/v1/documents/&lt;docid&gt;**                                   | Oui                                  | [Mise à la poubelle d'un document][DELDOC]                 |
|        |                                                                       |                                      |                                                            |
| GET    | */api/v1/documents/&lt;docid&gt;/history/*                            | Oui                                  | [Récupération des messages d'historique][get_histo]        |
| PUT    | */api/v1/documents/&lt;docid&gt;/history/*                            | N/A                                  | N/A                                                        |
| POST   | */api/v1/documents/&lt;docid&gt;/history/*                            | Future version                       | Ajout d'un message d'historique                            |
| DELETE | */api/v1/documents/&lt;docid&gt;/history/*                            | N/A                                  | N/A                                                        |
|        |                                                                       |                                      |                                                            |
| GET    | */api/v1/documents/&lt;docid&gt;/revisions/*                          | Oui                                  | [Liste des révisions d'un document][list_revision]         |
| PUT    | */api/v1/documents/&lt;docid&gt;/revisions/*                          | N/A                                  | N/A                                                        |
| POST   | */api/v1/documents/&lt;docid&gt;/revisions/*                          | N/A                                  | N/A                                                        |
| DELETE | */api/v1/documents/&lt;docid&gt;/revisions/*                          | N/A                                  | N/A                                                        |
|        |                                                                       |                                      |                                                            |
| GET    | **/api/v1/documents/&lt;docid&gt;/revisions/&lt;revisionNumber&gt;**  | Oui                                  | [Révision `<revisionNumber>`][get_revision]              |
| PUT    | **/api/v1/documents/&lt;docid&gt;/revisions/&lt;revisionNumber&gt;**  | N/A                                  | N/A                                                        |
| POST   | **/api/v1/documents/&lt;docid&gt;/revisions/&lt;revisionNumber&gt;**  | N/A                                  | N/A                                                        |
| DELETE | **/api/v1/documents/&lt;docid&gt;/revisions/&lt;revisionNumber&gt;**  | N/A                                  | N/A                                                        |
|        |                                                                       |                                      |                                                            |
| GET    | */api/v1/families/*                                                   | Future version                       | Liste des familles                                         |
| PUT    | */api/v1/families/*                                                   | N/A                                  | N/A                                                        |
| POST   | */api/v1/families/*                                                   | Future version                       | Création d'une nouvelle famille                            |
| DELETE | */api/v1/families/*                                                   | N/A                                  | N/A                                                        |
|        |                                                                       |                                      |                                                            |
| GET    | **/api/v1/families/&lt;family&gt;**                                   | Oui                                  | [Consultation du document décrivant la famille][GET_FAM]   |
| PUT    | **/api/v1/families/&lt;family&gt;**                                   | Future version                       | Modification de la configuration de la famille             |
| POST   | **/api/v1/families/&lt;family&gt;**                                   | N/A                                  | N/A                                                        |
| DELETE | **/api/v1/families/&lt;family&gt;**                                   | Future version                       | Suppression de la famille et des documents associés        |
|        |                                                                       |                                      |                                                            |
| GET    | */api/v1/families/&lt;family&gt;/documents/*                          | Future version                       | Liste des documents de cette famille                       |
| PUT    | */api/v1/families/&lt;family&gt;/documents/*                          | Future version                       | Modification en masse de documents de cette famille        |
| POST   | */api/v1/families/&lt;family&gt;/documents/*                          | Oui                                  | [Création d'un document de cette famille][POSTDOC]         |
| DELETE | */api/v1/families/&lt;family&gt;/documents/*                          | Future version                       | Mise à la poubelle en masse de documents de cette famille  |
|        |                                                                       |                                      |                                                            |
| GET    | **/api/v1/families/&lt;family&gt;/documents/&lt;docid&gt;**           | Oui                                  | [Récupération d'un document de la famille][GETDOC]         |
| PUT    | **/api/v1/families/&lt;family&gt;/documents/&lt;docid&gt;**           | Oui                                  | [Mise à jour d'un document de la famille][PUTDOC]          |
| POST   | **/api/v1/families/&lt;family&gt;/documents/&lt;docid&gt;**           | N/A                                  | N/A (Création d'un document avec un identifiant donné)     |
| DELETE | **/api/v1/families/&lt;family&gt;/documents/&lt;docid&gt;**           | Oui                                  | [Suppression d'un document de la famille][DELDOC]          |
|        |                                                                       |                                      |                                                            |
| GET    | **/api/v1/families/&lt;family&gt;/enumerates/&lt;docid&gt;**          | Oui                                  | [Récupération de la liste des valeurs][get_enum]           |
| PUT    | **/api/v1/families/&lt;family&gt;/enumerates/&lt;docid&gt;**          | Future version                       | Modification d'une valeur de la liste des énumérés         |
| POST   | **/api/v1/families/&lt;family&gt;/enumerates/&lt;docid&gt;**          | Future version                       | Ajout d'une valeur à la liste d'énumérés                   |
| DELETE | **/api/v1/families/&lt;family&gt;/enumerates/&lt;docid&gt;**          | Future version                       | Suppression définitivement d'un document mis à la poubelle |
|        |                                                                       |                                      |                                                            |
| GET    | */api/v1/files/*                                                      | N/A                                  | N/A                                                        |
| PUT    | */api/v1/files/*                                                      | N/A                                  | N/A                                                        |
| POST   | */api/v1/files/*                                                      | Oui                                  | [Création d'un fichier temporaire][POSTFILE]               |
| DELETE | */api/v1/files/*                                                      | Future version                       | Suppression d'un fichier temporaire                        |
|        |                                                                       |                                      |                                                            |
| GET    | */api/v1/trash/*                                                      | Future version                       | Liste des documents de la poubelle                         |
| PUT    | */api/v1/trash/*                                                      | N/A                                  | N/A                                                        |
| POST   | */api/v1/trash/*                                                      | N/A                                  | N/A                                                        |
| DELETE | */api/v1/trash/*                                                      | Future version                       | Supprime définitivement les documents de la poubelle       |
|        |                                                                       |                                      |                                                            |
| GET    | **/api/v1/trash/&lt;docid&gt;**                                       | Oui                                  | [Récupération d'un document mis à la poubelle][trash_doc]  |
| PUT    | **/api/v1/trash/&lt;docid&gt;**                                       | N/A                                  | N/A (Création d'un document supprimé)                      |
| POST   | **/api/v1/trash/&lt;docid&gt;**                                       | N/A                                  | N/A (Modification d'un document supprimé)                  |
| DELETE | **/api/v1/trash/&lt;docid&gt;**                                       | Future version                       | Suppression définitivement d'un document mis à la poubelle |
|        |                                                                       |                                      |                                                            |
              

Légende :

* Les URL en *italique* font références à des collections,
* Les URL en **gras** font références à des entités,

<span class="flag inline nota-bene"></span> Les entrées documents de famillies et de trash possède aussi les sous-collections :

* history,
* revisions.


<span class="flag inline nota-bene"></span> Les entrées en Future version sont prévues pour une implémentation future 
mais non présentes dans la version courante de l'API.

<!--links-->

[GET_FAM]: #rest:6b195156-0cda-47c8-9a9a-04ec13562c9a
[POSTDOC]: #rest:e769b476-0033-407c-b453-4e8466e09975
[GETDOC]: #rest:1d7b939f-d5fc-4b57-b33f-d216913efc22
[PUTDOC]: #rest:db2cb01a-7325-4f78-8cec-ceac9858caf2
[DELDOC]: #rest:3358b3bd-bdf6-44ef-b1d7-438f8eb21067

[POSTFILE]: #rest:5797255d-128d-4aa4-9c11-2c8195cca63d
[trash_doc]: #rest:52be10c1-9f46-456b-a22f-24909386567f
[get_enum]: #rest:bb13e401-1859-4c73-b299-70b801ed7eb0
[get_histo]: #rest:9ae75dac-8eb5-4fa9-a608-7313b90fe33c
[list_revision]: #rest:2dd5afbe-1d3d-4830-8241-c93077d88430
[get_revision]: #rest:eb7b6954-0945-4f02-8e10-16e69729c529
