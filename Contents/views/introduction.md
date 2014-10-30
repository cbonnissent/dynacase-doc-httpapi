# Document : Vues {#rest:6af5f3ad-9b14-4f22-8c90-355017841157}

Cette collection décrit les vues des [documents][doc_document]. 

Une vue est composée de :

* un ensemble de valeur d'attributs,
* un ensemble de visibilités pour ces attributs.

## URL {#rest:3e41317a-d9a2-4377-8f90-a1ac254893e5}

L'url d'accès est : `/api/v1/documents/<documentId>/views/`

## Méthodes {#rest:fce5d4a4-baf1-4689-b1c2-5a072e74a457}

La sous-collection views implémente les éléments suivants :

* Collection :

| Action   | URL                                             | Action effectuée                                                            |
| :-     : | :                                              :| :                                                                         : |
| `GET`    | `/api/v1/documents/<documentId>/views/`         | [Retourne la liste des vues applicable pour le `<documentId>`][list_view]   |
| `POST`   | `/api/v1/documents/<documentId>/views/`         | N/A                                                                         |
| `PUT`    | `/api/v1/documents/<documentId>/views/`         | N/A                                                                         |
| `DELETE` | `/api/v1/documents/<documentId>/views/`         | N/A                                                                         |

* Entité :

| Action   | URL                                                 | Action effectuée                                                 |
| :-     : | :                                                  :| :                                                              : |
| `GET`    | `/api/v1/documents/<documentId>/views/<vewId>`      | [Retourne la vue `vewId` document `documentId` ][get_view]       |
| `POST`   | `/api/v1/documents/<documentId>/views/<vewId>`      | N/A                                                              |
| `PUT`    | `/api/v1/documents/<documentId>/views/<vewId>`      | N/A                                                              |
| `DELETE` | `/api/v1/documents/<documentId>/views/<vewId>`      | N/A                                                              |


<!-- links -->
[doc_document]: http://docs.anakeen.com/dynacase/3.2/dynacase-doc-core-reference/website/book/core-ref:e01bf76d-481b-41fd-ac64-167a68d34c55.html#core-ref:67929e29-abef-437c-88a3-7f43647c60ff
[get_view]: #rest:a2055321-27c0-4e15-b9c4-e4cfe2ff445a
[list_view]: #rest:033c1b91-2622-413d-9b39-f39700185f84