# Famille : Énuméré {#rest:dbffbc8d-dc7a-4f9f-88f2-c3b8bedaef99}

Cette collection décrit les [énumérés][doc_enum] de Dynacase. 

## URL {#rest:c017bd55-0699-47c3-ae65-edd85413b3b3}

L'url d'accès est : `/api/v1/families/<famName>/enumerates/`

## Méthodes {#rest:f55c6681-b62a-45c1-ac61-ffd552eda60c}

La sous-collection enumerates implémente les éléments suivants :

* Collection : Il n'y a pas d'accès possible directement auprès de la collection `documents` :

| Action   | URL                                               | Action effectuée                                                   |
| :-     : | :                                                :| :                                                                : |
| `GET`    | `/api/v1/families/<famName>/enumerates/`          | Liste des attributs énumérés (pas encore implémenté)               |
| `POST`   | `/api/v1/families/<famName>/enumerates/`          | N/A                                                                |
| `PUT`    | `/api/v1/families/<famName>/enumerates/`          | N/A                                                                |
| `DELETE` | `/api/v1/families/<famName>/enumerates/`          | N/A                                                                |

* Entité :

| Action   | URL                                                    | Action effectuée                                              |
| :-     : | :                                                     :| :                                                           : |
| `GET`    | `/api/v1/families/<famName>/enumerates/<attrid>`       | [Retourne la définition de l'énuméré attrid][get_enum]        |
| `POST`   | `/api/v1/families/<famName>/enumerates/<attrid>`       | N/A                                                           |
| `PUT`    | `/api/v1/families/<famName>/enumerates/<attrid>`       | N/A                                                           |
| `DELETE` | `/api/v1/families/<famName>/enumerates/<attrid>`       | N/A                                                           |


<!-- links -->
[doc_enum]: http://docs.anakeen.com/dynacase/3.2/dynacase-doc-core-reference/website/book//core-ref:eef3e3ec-2d50-41bd-98e1-cc978f0a5178.html#core-ref:eef3e3ec-2d50-41bd-98e1-cc978f0a5178
[get_enum]: #rest:bb13e401-1859-4c73-b299-70b801ed7eb0