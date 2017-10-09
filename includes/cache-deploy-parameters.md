
### <a name="cacheskuname"></a>cacheSKUName
nivel de precios de Hola de hello Redis de Azure nueva caché.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

plantilla de Hello define los valores de hello que están permitidos para este parámetro (básico o estándar) y asigna un valor predeterminado (Basic) si no se especifica ningún valor. Basic proporciona un único nodo con varios tamaños disponibles backup too53 GB.
Estándar proporcionan dos nodos principal/réplica que tiene disponible una too53 GB y 99,9% SLA de varios tamaños.

### <a name="cacheskufamily"></a>cacheSKUFamily
familia de Hola para sku de Hola.

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
tamaño de Hola de nueva instancia de caché en Redis de Azure Hola. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


Hola plantilla define los valores de hello permitidas para este parámetro (0, 1, 2, 3, 4, 5 o 6) y asigna un valor predeterminado (1) si no se especifica ningún valor. Los números corresponden los tamaños de caché de toofollowing: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB

