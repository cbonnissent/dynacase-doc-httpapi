# Énuméré {#rest:7fe0e66a-c3ce-4315-aff6-fa345eae31da}

Cette collection décrit les [énumérés][doc_enum] de Dynacase. 

## URL {#rest:0d3d4576-b7d3-4480-9b00-03d6d20704fa}

L'url d'accès est : `/api/v1/enums`

## Méthodes {#rest:18b84a9c-9226-4367-870c-2f0737151239}

La collection enums implémentent les éléments suivants :

* Collection : Il n'y a pas d'accès possible directement auprès de la collection documents :

| Action   | URL                     | Action effectuée   |
| :-     : | :                      :| :                : |
| `GET`    | `/api/v1/enums`         | N/A                |
| `POST`   | `/api/v1/enums`         | N/A                |
| `PUT`    | `/api/v1/enums`         | N/A                |
| `DELETE` | `/api/v1/enums`         | N/A                |

* Entité :

| Action   | URL                                   | Action effectuée                                              |
| :-     : | :                                    :| :                                                           : |
| `GET`    | `/api/v1/enums/<famid>/<attrid>`      | [Retourne la définition de l'énuméré attrid][get_enum]        |
| `POST`   | `/api/v1/enums/<famid>/<attrid>`      | N/A                                                           |
| `PUT`    | `/api/v1/enums/<famid>/<attrid>`      | N/A                                                           |
| `DELETE` | `/api/v1/enums/<famid>/<attrid>`      | N/A                                                           |


<!-- links -->
[doc_enum]: http://docs.anakeen.com/dynacase/3.2/dynacase-doc-core-reference/website/book//core-ref:eef3e3ec-2d50-41bd-98e1-cc978f0a5178.html#core-ref:eef3e3ec-2d50-41bd-98e1-cc978f0a5178
[get_enum]: #rest:bb13e401-1859-4c73-b299-70b801ed7eb0