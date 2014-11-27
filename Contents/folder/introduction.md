# Répertoire {#rest:5dda257a-b6b2-4cef-ac04-6d42d59154a9}

Cette collection décrit les répertoires de Dynacase. 

Un répertoire est un document permettant de stocker un ensemble de documents.

## URL {#rest:8b2a3860-c482-4f0e-8d15-04f495b67e72}

L'url d'accès est : `/api/v1/folders`

## Méthodes {#rest:ff2321ab-3b4e-4837-84aa-5c67f4f4c8aa}

La collection searches implémente les éléments suivants :

* Collection : Il n'y a pas d'accès possible directement auprès de la collection :

| Action   | URL                         | Action effectuée                                          |
| :-     : | :                          :| :                                                       : |
| `GET`    | `/api/v1/folders/`          | [Liste des répertoires][folders_collection]               |
| `POST`   | `/api/v1/folders/`          | N/A                                                       |
| `PUT`    | `/api/v1/folders/`          | N/A                                                       |
| `DELETE` | `/api/v1/folders/`          | N/A                                                       |

<span class="flag inline nota-bene"></span> Une recherche étant un document Dynacase, la création d'une nouvelle 
répertoire passe par l'utilisation de l'entrée `families/DIR/documents/`.

* Entité :

| Action   | URL                            | Action effectuée                               |
| :-     : | :                             :| :                                  :           |
| `GET`    | `/api/v1/folders/<id>/`       | [Contenu de du répertoire `id`][folders_content]|
| `POST`   | `/api/v1/folders/<id>/`       | N/A                                             |
| `PUT`    | `/api/v1/folders/<id>/`       | N/A                                             |
| `DELETE` | `/api/v1/folders/<id>/`       | N/A                                             |


<!-- links -->

[folders_collection]: #rest:b3f83d12-4ea7-44e2-8509-1145d05003d6
[folders_content]: #rest:f3e3869b-4dcf-40ee-9733-3f4b57e2386f
