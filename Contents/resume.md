# État de l'api {#core-ref:cf8c475b-1ea5-474d-bc74-f5902f9d00fb}



|  Type  |                        URL                        |                Implanté               |                             Signification                             |
| ------ | ------------------------------------------------- | ------------------------------------- | --------------------------------------------------------------------- |
| GET    | /api/documents/                                   | <span class="apiNo">NO</span>         | Liste de documents                                                    |
| PUT    | /api/documents/                                   | <span class="apiNo">NO</span>         | Modification en masse de documents                                    |
| POST   | /api/documents/                                   | <span class="apiNever">NEVER</span>   | Création d'un document quelconque                                     |
| DELETE | /api/documents/                                   | <span class="apiNo">NO</span>         | Mise à la poubelle en masse de documents                              |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/families/                                    | <span class="apiNo">NO</span>         | Liste des familles                                                    |
| PUT    | /api/families/                                    | <span class="apiNo">NO</span>         | Modification en masse de familles                                     |
| POST   | /api/families/                                    | <span class="apiNo">NO</span>         | Création de familles                                                  |
| DELETE | /api/families/                                    | <span class="apiNo">NO</span>         | Suppression de familles                                               |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/families/&lt;family&gt;                      | <span class="apiNo">NO</span>         | Liste de document de la famille                                       |
| PUT    | /api/families/&lt;family&gt;                      | <span class="apiNo">NO</span>         | Modification en masse de documents                                    |
| POST   | /api/families/&lt;family&gt;                      | <span class="apiTodo">TODO</span>     | [Création d'un document de la famille][POSTDOC]                       |
| DELETE | /api/families/&lt;family&gt;                      | <span class="apiNo">NO</span>         | Mise à la poubelle en masse de documents                              |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/documents/&lt;docid&gt;                      | <span class="apiTodo">TODO</span>     | [Récupération d'un document][GETDOC]                                  |
| PUT    | /api/documents/&lt;docid&gt;                      | <span class="apiTodo">TODO</span>     | [Mise à jour d'un document][PUTDOC]                                   |
| POST   | /api/documents/&lt;docid&gt;                      | <span class="apiNever">NEVER</span>   | Création d'un document avec un identifiant                            |
| DELETE | /api/documents/&lt;docid&gt;                      | <span class="apiTodo">TODO</span>     | [Mise à la poubelle d'un document][DELDOC]                            |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">TODO</span>     | [Récupération d'un document d'une famille][GETDOC]                    |
| PUT    | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">TODO</span>     | [Mise à jour d'un document d'une famille][PUTDOC]                     |
| POST   | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">NEVER</span>    | Création d'un document d'une famille                                  |
| DELETE | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">TODO</span>     | [Suppression d'un document d'une famille avec un identifiant][DELDOC] |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/files                                        | <span class="apiNever">NEVER</span>   | Liste des fichiers temporaires                                        |
| PUT    | /api/files                                        | <span class="apiNo">NO</span>         | Modification d'un fichier temporaire                                  |
| POST   | /api/files                                        | <span class="apiTodo">TODO</span>     | [Création d'un fichier temporaire][POSTFILE]                          |
| DELETE | /api/files                                        | <span class="apiNo">NO</span>         | Suppression d'un fichier temporaire                                   |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiNo">NO</span>         | [Information d'un fichier d'un document][GETFILE]                     |
| PUT    | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiNo">NO</span>         | [Modification d'un fichier d'un document][PUTFILE]                    |
| POST   | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiTodo">TODO</span>     | [Création d'un fichier d'un document][POSTFILE]                       |
| DELETE | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiNo">NO</span>         | [Suppression d'un fichier d'un document][DELFILE]                     |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/trash/                                       | <span class="apiNo">NO</span>         | Liste document de la poubelle                                         |
| PUT    | /api/trash/                                       | <span class="apiNo">NO</span>         | Modifie en masse les documents de la poubelle                         |
| POST   | /api/trash/                                       | <span class="apiNever">NEVER</span>   | Créer un document dans la poubelle                                    |
| DELETE | /api/trash/                                       | <span class="apiNo">NO</span>         | Supprime les documents de la poubelle                                 |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    | /api/trash/&lt;docid&gt;                          | <span class="apiNo">NO</span>         | Récupération d'un document mis à la poubelle                          |
| PUT    | /api/trash/&lt;docid&gt;                          | <span class="apiNo">NO</span>         | Modification d'un document mis à la poubelle                          |
| POST   | /api/trash/&lt;docid&gt;                          | <span class="apiNever">NEVER</span>   | Création d'un document mis à la poubelle                              |
| DELETE | /api/trash/&lt;docid&gt;                          | <span class="apiNo">NO</span>         | Suppression d'un document mis à la poubelle                           |
|        | <span class="greyLine" >&nbsp;</span>             | <span class="greyLine" >&nbsp;</span> | <span class="greyLine" >&nbsp;</span>                                 |
| GET    |                                                   |                                       |                                                                       |
| PUT    | [oto][POSTDOC]                                    |                                       |                                                                       |
| POST   |                                                   |                                       |                                                                       |
| DELETE |                                                   |                                       |                                                                       |
|        |                                                   |                                       |                                                                       |
|        |                                                   |                                       |                                                                       |



<!--links-->

[POSTDOC]: #core-ref:97b6c23a-e527-48b8-ab52-b5e869dadce7
[GETDOC]: #core-ref:3fc0b4b4-149c-42a8-91b2-96799d668b9b
[PUTDOC]: #core-ref:2d248523-ddf4-4654-bd5d-6e5af3b5056d
[DELDOC]: #core-ref:85b9c9f2-cb76-4d07-9525-ec90af2561e2

[POSTFILE]: #core-ref:5797255d-128d-4aa4-9c11-2c8195cca63d
[GETFILE]: #core-ref:fa90f9f7-0f35-46b3-a09a-b49e6a75ab5d
[PUTFILE]: #core-ref:4bd2f27b-8457-403e-be9b-8ff036f15b0f
[DELFILE]: #core-ref:06a16210-db4a-494b-923d-5c8d70f88a66

