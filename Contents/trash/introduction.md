# Documents supprimés {#rest:7fe0e66a-c3ce-4315-aff6-fa345eae31da}

Cette collection décrit les [documents][doc_document] de Dynacase supprimés. 

## URL {#rest:0d3d4576-b7d3-4480-9b00-03d6d20704fa}

L'url d'accès est : `/api/v1/trash`

## Méthodes {#rest:18b84a9c-9226-4367-870c-2f0737151239}

La collection trash implémentent les éléments suivants :

* Collection : Il n'y a pas d'accès possible directement auprès de la collection documents :

| Action   | URL                     | Action effectuée   |
| :-     : | :                      :| :                : |
| `GET`    | `/api/v1/trash`         | N/A                |
| `POST`   | `/api/v1/trash`         | N/A                |
| `PUT`    | `/api/v1/trash`         | N/A                |
| `DELETE` | `/api/v1/trash`         | N/A                |

* Entité :

| Action   | URL                       | Action effectuée                            |
| :-     : | :                        :| :                                   :       |
| `GET`    | `/api/v1/trash/<id>`      | [Retourne le document `id`][get_enum]        |
| `POST`   | `/api/v1/trash/<id>`      | N/A                                         |
| `PUT`    | `/api/v1/trash/<id>`      | N/A                                         |
| `DELETE` | `/api/v1/trash/<id>`      | N/A                                         |


<!-- links -->
[doc_document]: http://docs.anakeen.com/dynacase/3.2/dynacase-doc-core-reference/website/book/core-ref:e01bf76d-481b-41fd-ac64-167a68d34c55.html#core-ref:67929e29-abef-437c-88a3-7f43647c60ff
[trash_doc]: #rest:52be10c1-9f46-456b-a22f-24909386567f
