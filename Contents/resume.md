# Résumé de l'API {#rest:39742615-6b36-4b23-8449-3a9019b9afa8}

## Carte de l'api {#rest:cf8c475b-1ea5-474d-bc74-f5902f9d00fb}

|  Type  |                        URL                              |               Implanté              |                             Signification                             |
| ------ | -------------------------------------------------       | ----------------------------------- | --------------------------------------------------------------------- |
| GET    | /api/v1/documents/                                      | <span class="apiTodo">Not yet</span>| Liste de documents                                                    |
| PUT    | /api/v1/documents/                                      | N/A                                 | N/A                                                                   |
| POST   | /api/v1/documents/                                      | N/A                                 | N/A                                                                   |
| DELETE | /api/v1/documents/                                      | N/A                                 | N/A                                                                   |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/documents/&lt;docid&gt;                         | Oui                                 | [Récupération d'un document][GETDOC]                                  |
| PUT    | /api/v1/documents/&lt;docid&gt;                         | Oui                                 | [Mise à jour d'un document][PUTDOC]                                   |
| POST   | /api/v1/documents/&lt;docid&gt;                         | N/A                                 | N/A                                                                   |
| DELETE | /api/v1/documents/&lt;docid&gt;                         | Oui                                 | [Mise à la poubelle d'un document][DELDOC]                            |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/families/                                       | <span class="apiTodo">Not yet</span>| Liste des familles                                                    |
| PUT    | /api/v1/families/                                       | N/A                                 | N/A                                                                   |
| POST   | /api/v1/families/                                       | <span class="apiTodo">Not yet</span>| Création d'une nouvelle famille                                       |
| DELETE | /api/v1/families/                                       | N/A                                 | N/A                                                                   |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/families/&lt;family&gt;                         | Oui                                 | [Consultation du document décrivant la famille][GET_FAM]              |
| PUT    | /api/v1/families/&lt;family&gt;                         | <span class="apiTodo">Not yet</span>| Modification de la configuration de la famille                        |
| POST   | /api/v1/families/&lt;family&gt;                         | N/A                                 | N/A                                                                   |
| DELETE | /api/v1/families/&lt;family&gt;                         | <span class="apiTodo">Not yet</span>| Suppression de la famille et des documents associés                   |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/families/&lt;family&gt;/documents/              | <span class="apiTodo">Not yet</span>| Liste des documents de cette famille                                  |
| PUT    | /api/v1/families/&lt;family&gt;/documents/              | <span class="apiTodo">Not yet</span>| Modification en masse de documents de cette famille                   |
| POST   | /api/v1/families/&lt;family&gt;/documents/              | Oui                                 | [Création d'un document de cette famille][POSTDOC]                    |
| DELETE | /api/v1/families/&lt;family&gt;/documents/              | <span class="apiTodo">Not yet</span>| Mise à la poubelle en masse de documents de cette famille             |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/families/&lt;family&gt;/documents/&lt;docid&gt; | Oui                                 | [Récupération d'un document de la famille][GETDOC]                    |
| PUT    | /api/v1/families/&lt;family&gt;/documents/&lt;docid&gt; | Oui                                 | [Mise à jour d'un document de la famille][PUTDOC]                     |
| POST   | /api/v1/families/&lt;family&gt;/documents/&lt;docid&gt; | N/A                                 | N/A                                                                   |
| DELETE | /api/v1/families/&lt;family&gt;/documents/&lt;docid&gt; | Oui                                 | [Suppression d'un document de la famille][DELDOC]                     |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/files/                                          | N/A                                 | N/A                                                                   |
| PUT    | /api/v1/files/                                          | <span class="apiTodo">Not yet</span>| Modification d'un fichier temporaire                                  |
| POST   | /api/v1/files/                                          | Oui                                 | [Création d'un fichier temporaire][POSTFILE]                          |
| DELETE | /api/v1/files/                                          | <span class="apiTodo">Not yet</span>| Suppression d'un fichier temporaire                                   |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/trash/                                          | <span class="apiTodo">Not yet</span>| Liste document de la poubelle                                         |
| PUT    | /api/v1/trash/                                          | <span class="apiTodo">Not yet</span>| Modifie en masse les documents de la poubelle                         |
| POST   | /api/v1/trash/                                          | N/A                                 | N/A                                                                   |
| DELETE | /api/v1/trash/                                          | <span class="apiTodo">Not yet</span>| Supprime définitivement les documents de la poubelle                  |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/trash/&lt;docid&gt;                             | Oui                                 | [Récupération d'un document mis à la poubelle][trash_doc]             |
| PUT    | /api/v1/trash/&lt;docid&gt;                             | N/A                                 | N/A                                                                   |
| POST   | /api/v1/trash/&lt;docid&gt;                             | N/A                                 | N/A                                                                   |
| DELETE | /api/v1/trash/&lt;docid&gt;                             | <span class="apiTodo">Not yet</span>| Suppression définitivement d'un document mis à la poubelle            |
|        |                                                         |                                     |                                                                       |
| GET    | /api/v1/enums/&lt;family&gt;/&lt;docid&gt;              | Oui                                 | [Récupération de la liste des valeurs][get_enum]                      |
| PUT    | /api/v1/enums/&lt;family&gt;/&lt;docid&gt;              | <span class="apiTodo">Not yet</span>| Modification d'une valeur de la liste des énumérés                    |
| POST   | /api/v1/enums/&lt;family&gt;/&lt;docid&gt;              | <span class="apiTodo">Not yet</span>| Ajout d'une valeur à la liste d'énumérés                              |
| DELETE | /api/v1/enums/&lt;family&gt;/&lt;docid&gt;              | <span class="apiTodo">Not yet</span>| Suppression définitivement d'un document mis à la poubelle            |

<span class="flag inline nota-bene"></span> Les entrées en <span class="apiTodo">Not yet</span> sont prévues
pour une implémentation future mais non présentes dans la version courante de l'API.


<!--links-->

[GET_FAM]: #rest:6b195156-0cda-47c8-9a9a-04ec13562c9a

[POSTDOC]: #rest:e769b476-0033-407c-b453-4e8466e09975
[GETDOC]: #rest:1d7b939f-d5fc-4b57-b33f-d216913efc22
[PUTDOC]: #rest:db2cb01a-7325-4f78-8cec-ceac9858caf2
[DELDOC]: #rest:3358b3bd-bdf6-44ef-b1d7-438f8eb21067

[POSTFILE]: #rest:5797255d-128d-4aa4-9c11-2c8195cca63d
[trash_doc]: #rest:52be10c1-9f46-456b-a22f-24909386567f
[get_enum]: #rest:bb13e401-1859-4c73-b299-70b801ed7eb0
