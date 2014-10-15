# Extension de l'API REST {#rest:50aff82b-8921-42ff-81b1-69a1a0103d98}

L'extension de l'API REST passe par deux éléments : 

* une classe de CRUD : celle-ci fournit les 4 méthodes du CRUD et retourne les valeurs.
* une inscription dans la liste des API existantes.

## Classe de CRUD {#rest:651043a1-f290-466e-977f-d39a195a1195}

Les classes de CRUD étendent la classe `\Dcp\HttpApi\V1\Crud` et doivent implémenter les méthodes suivantes :

* `create` : création d'une entité,
* `read` : récupération d'une entité,
* `update` : mise à jour d'une entité,
* `delete` : suppression d'une entité.

La classe fournit aussi deux autres méthodes que vous pouvez surcharger :

* `setParameters` : cette méthode reçoit les paramètres extraits par le routeur de l'url d'appel (voir [enregistrement CRUD][save_CRUD]),
ces paramètres sont ensuite mis à disposition dans le tableau `parameters`,
* `execute` : cette méthode est celle qui est exécutée par le routeur une fois la classe CRUD identifiée.

## Enregistrement CRUD {#rest:7466f89c-87de-4dbe-89af-fdc2db37b9a4}

La nouvelle classe de CRUD doit ensuite être enregistrée auprès de l'application `HTTPAPI_V1`, ceci se fait via le
paramètre applicatif `CUSTOM_CRUD_CLASS`.

Ce paramètre doit contenir un tableau encodé en JSON semblable à :

    [javascript]
    [
        {
            "order" : 100,
            "class" : "\\Dcp\\HttpApi\\V1\\DocumentCrud",
            "regExp" : "/^\\/documents\\/?(?P<identifier>[^\\/]*)$/",
            "description" : "Documents",
            "canonicalURL" : "documents/<documentId>"
        },
        {
            "order" : 100,
             "class" : "\\Dcp\\HttpApi\\V1\\FamilyCrud",
             "regExp" : "/^\\/families\\/(?P<identifier>[^\\/]*)\\/?$/",
             "description" : "Families",
             "canonicalURL" : "families/<familyId>"
         },
        {
            "order" : 200,
            "class" : "\\Dcp\\HttpApi\\V1\\FamilyDocumentCrud",
            "regExp" : "/^\\/families\\/(?P<familyId>[^\\/]*)\\/documents\\/(?P<identifier>[^\\/]*)$/",
            "description" : "Documents of the family <familyId>",
            "canonicalURL" : "families/<familyId>/documents/<documentId>"
        },
        {
            "order" : 100,
            "class" : "\\Dcp\\HttpApi\\V1\\Trash",
            "regExp" : "/^\\/trash\\/?(?P<identifier>[^\\/]*)$/",
            "description" : "Deleted documents",
            "canonicalURL" : "trash/<documentId>"
        },
        {
            "order" : 100,
            "class" : "\\Dcp\\HttpApi\\V1\\EnumCrud",
            "regExp" : "/^\\/enums\\/(?P<familyId>[^\\/]*)\\/(?P<identifier>[^\\/]*)$/",
            "description" : "Enumerate",
            "canonicalURL" : "enums/<familyId>/<attributeIdentifier>/"
        }
    ]

Ce tableau contient des objets contenant chacun :

* `regExp` : une expression régulière, celle-ci est exécutée sur l'URL d'appel (sans la partie `api/v1/`) si l'expression
régulière est validée la route est considérée comme valide,
* `order` : un ordre d'exécution si plusieurs route de même ordre sont valides, c'est celle ayant le order le plus élevé
qui est sélectionnée,
* `class` : identifiant d'une classe de type `CRUD` qui est exécutée si la route est sélectionnée,
* `description` (optionnel) : chaîne de caractères non traduites décrivant la ressource (cette clef est utilisée dans la page par défaut de l'API),
* `canonicalURL` (optionnel) : URL d'accès à la ressources (cette clef est utilisée dans la page par défaut de l'API).

Il est à noter que si vous ajoutez une route à égalité avec une route `system` (liste ci-dessus) (regexp positive et order égal),
alors c'est la route `custom` qui est sélectionnée.

[save_CRUD]: #rest:651043a1-f290-466e-977f-d39a195a1195