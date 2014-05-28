# État de l'api



|  Type  |                        URL                        |               Implanté              |                 Signification                 |
| ------ | ------------------------------------------------- | ----------------------------------- | --------------------------------------------- |
| GET    | /api/documents/                                   | <span class="apiNo">NO</span>       | Liste de documents                            |
| PUT    | /api/documents/                                   | <span class="apiNo">NO</span>       | Modification en masse de documents            |
| POST   | /api/documents/                                   | <span class="apiNever">NEVER</span> | Création d'un document quelconque             |
| DELETE | /api/documents/                                   | <span class="apiNo">NO</span>       | Mise à la poubelle en masse de documents      |
|        | <span class="greyLine" >&nbsp;</span>             |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/families/                                    | <span class="apiNo">NO</span>       | Liste des familles                            |
| PUT    | /api/families/                                    | <span class="apiNo">NO</span>       | Modification en masse de familles             |
| POST   | /api/families/                                    | <span class="apiNo">NO</span>       | Création de familles                          |
| DELETE | /api/families/                                    | <span class="apiNo">NO</span>       | Suppression de familles                       |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/families/&lt;family&gt;                      | <span class="apiNo">NO</span>       | Liste de document de la famille               |
| PUT    | /api/families/&lt;family&gt;                      | <span class="apiNo">NO</span>       | Modification en masse de documents            |
| POST   | /api/families/&lt;family&gt;                      | <span class="apiTodo">TODO</span>   | Création d'un document de la famille          |
| DELETE | /api/families/&lt;family&gt;                      | <span class="apiNo">NO</span>       | Mise à la poubelle en masse de documents      |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/documents/&lt;docid&gt;                      | <span class="apiTodo">TODO</span>   | Récupération d'un document                    |
| PUT    | /api/documents/&lt;docid&gt;                      | <span class="apiTodo">TODO</span>   | Mise à jour d'un document                     |
| POST   | /api/documents/&lt;docid&gt;                      | <span class="apiNever">NEVER</span> | Création d'un document avec un identifiant    |
| DELETE | /api/documents/&lt;docid&gt;                      | <span class="apiTodo">TODO</span>   | Mise à la poubelle d'un document              |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">TODO</span>   | Récupération d'un document d'une famille      |
| PUT    | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">TODO</span>   | Mise à jour d'un document d'une famille       |
| POST   | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">TODO</span>   | Création d'un document d'une famille          |
| DELETE | /api/families/&lt;family&gt;/&lt;docid&gt;        | <span class="apiTodo">TODO</span>   | Suppression d'un document d'une famille       |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/files                                        | <span class="apiNever">NEVER</span> | Liste des fichiers temporaires                |
| PUT    | /api/files                                        | <span class="apiNo">NO</span>       | Modification d'un fichier temporaire          |
| POST   | /api/files                                        | <span class="apiTodo">TODO</span>   | Création d'un fichier temporaire              |
| DELETE | /api/files                                        | <span class="apiNo">NO</span>       | Suppression d'un fichier temporaire           |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiNo">NO</span>       | Information d'un fichier d'un document        |
| PUT    | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiNo">NO</span>       | Modification d'un fichier d'un document       |
| POST   | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiTodo">TODO</span>   | Création d'un fichier d'un document           |
| DELETE | /api/documents/&lt;docid&gt;/files/&lt;attrid&gt; | <span class="apiNo">NO</span>       | Suppression d'un fichier d'un document        |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/trash/                                       | <span class="apiNo">NO</span>       | Liste document de la poubelle                 |
| PUT    | /api/trash/                                       | <span class="apiNo">NO</span>       | Modifie en masse les documents de la poubelle |
| POST   | /api/trash/                                       | <span class="apiNever">NEVER</span> | Créer un document dans la poubelle            |
| DELETE | /api/trash/                                       | <span class="apiNo">NO</span>       | Supprime les documents de la poubelle         |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    | /api/trash/&lt;docid&gt;                          | <span class="apiNo">NO</span>       | Récupération d'un document mis à la poubelle  |
| PUT    | /api/trash/&lt;docid&gt;                          | <span class="apiNo">NO</span>       | Modification d'un document mis à la poubelle  |
| POST   | /api/trash/&lt;docid&gt;                          | <span class="apiNever">NEVER</span> | Création d'un document mis à la poubelle      |
| DELETE | /api/trash/&lt;docid&gt;                          | <span class="apiNo">NO</span>       | Suppression d'un document mis à la poubelle   |
|        | <span class="greyLine" >&nbsp;</span>                         |                                     | <span class="greyLine" >&nbsp;</span>                     |
| GET    |                                                   |                                     |                                               |
| PUT    |                                                   |                                     |                                               |
| POST   |                                                   |                                     |                                               |
| DELETE |                                                   |                                     |                                               |
|        |                                                   |                                     |                                               |
|        |                                                   |                                     |                                               |