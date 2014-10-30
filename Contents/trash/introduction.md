# Document : Supprimé {#rest:d65c99b2-7f57-478a-9f76-bcc33aa6bea8}

Cette collection décrit les [documents][doc_document] de Dynacase supprimés. 

## URL {#rest:bcc4ab0b-a9d3-43c4-adc2-2ceb7ab2689e}

L'url d'accès est : `/api/v1/trash`

## Méthodes {#rest:b23f5636-f2e4-4b5d-99d1-0ca90a03ca9c}

La collection trash implémente les éléments suivants :

* Collection : Il n'y a pas d'accès possible directement auprès de la collection :

| Action   | URL                     | Action effectuée   |
| :-     : | :                      :| :                : |
| `GET`    | `/api/v1/trash`         | N/A                |
| `POST`   | `/api/v1/trash`         | N/A                |
| `PUT`    | `/api/v1/trash`         | N/A                |
| `DELETE` | `/api/v1/trash`         | N/A                |

* Entité :

| Action   | URL                       | Action effectuée                            |
| :-     : | :                        :| :                                   :       |
| `GET`    | `/api/v1/trash/<id>`      | [Retourne le document `id`][trash_doc]      |
| `POST`   | `/api/v1/trash/<id>`      | N/A                                         |
| `PUT`    | `/api/v1/trash/<id>`      | N/A                                         |
| `DELETE` | `/api/v1/trash/<id>`      | N/A                                         |


<!-- links -->
[doc_document]: http://docs.anakeen.com/dynacase/3.2/dynacase-doc-core-reference/website/book/core-ref:e01bf76d-481b-41fd-ac64-167a68d34c55.html#core-ref:67929e29-abef-437c-88a3-7f43647c60ff
[trash_doc]: #rest:52be10c1-9f46-456b-a22f-24909386567f
