# Historique d'un document  {#rest:01d9b18d-a597-411d-8d8f-a5172b81f60b}

Cette collection décrit les messages de l'historique des documents

## URL  {#rest:670071f5-008d-42e8-bde3-0bcee337ae50}

L'url d'accès est : `/api/v1/documents/<documentId>/history/`

## Méthodes  {#rest:b2b3b00f-6492-4315-aec4-f99956fafd59}

La collection enums implémentent les éléments suivants :

* Collection : 

| Action   | URL                                       | Action effectuée                           |
| :-     : | :                      :                  | :                :                         |
| `GET`    | `/api/v1/documents/<documentId>/history/` | [Liste des messages historique][get_histo] |
| `POST`   | `/api/v1/documents/<documentId>/history/` | N/A                                        |
| `PUT`    | `/api/v1/documents/<documentId>/history/` | N/A                                        |
| `DELETE` | `/api/v1/documents/<documentId>/history/` | N/A                                        |

* Alternative (restriction sur la famille) :

| Action   | URL                                                          | Action effectuée                           |
| :-     : | :                      :                                     | :                :                         |
| `GET`    | `/api/v1/families/<famName>/documents/<documentId>/history/` | [Liste des messages historique][get_histo] |
| `POST`   | `/api/v1/families/<famName>/documents/<documentId>/history/` | N/A                                        |
| `PUT`    | `/api/v1/families/<famName>/documents/<documentId>/history/` | N/A                                        |
| `DELETE` | `/api/v1/families/<famName>/documents/<documentId>/history/` | N/A                                        |


<!-- links -->
[get_histo]: #rest:9ae75dac-8eb5-4fa9-a608-7313b90fe33c