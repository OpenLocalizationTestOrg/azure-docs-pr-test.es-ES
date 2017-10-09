
### <a name="cacheskuname"></a><span data-ttu-id="8147e-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="8147e-101">cacheSKUName</span></span>
<span data-ttu-id="8147e-102">nivel de precios de Hola de hello Redis de Azure nueva caché.</span><span class="sxs-lookup"><span data-stu-id="8147e-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

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

<span data-ttu-id="8147e-103">plantilla de Hello define los valores de hello que están permitidos para este parámetro (básico o estándar) y asigna un valor predeterminado (Basic) si no se especifica ningún valor.</span><span class="sxs-lookup"><span data-stu-id="8147e-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="8147e-104">Basic proporciona un único nodo con varios tamaños disponibles backup too53 GB.</span><span class="sxs-lookup"><span data-stu-id="8147e-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="8147e-105">Estándar proporcionan dos nodos principal/réplica que tiene disponible una too53 GB y 99,9% SLA de varios tamaños.</span><span class="sxs-lookup"><span data-stu-id="8147e-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="8147e-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="8147e-106">cacheSKUFamily</span></span>
<span data-ttu-id="8147e-107">familia de Hola para sku de Hola.</span><span class="sxs-lookup"><span data-stu-id="8147e-107">hello family for hello sku.</span></span>

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


### <a name="cacheskucapacity"></a><span data-ttu-id="8147e-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="8147e-108">cacheSKUCapacity</span></span>
<span data-ttu-id="8147e-109">tamaño de Hola de nueva instancia de caché en Redis de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="8147e-109">hello size of hello new Azure Redis Cache instance.</span></span> 

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


<span data-ttu-id="8147e-110">Hola plantilla define los valores de hello permitidas para este parámetro (0, 1, 2, 3, 4, 5 o 6) y asigna un valor predeterminado (1) si no se especifica ningún valor.</span><span class="sxs-lookup"><span data-stu-id="8147e-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="8147e-111">Los números corresponden los tamaños de caché de toofollowing: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="8147e-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

