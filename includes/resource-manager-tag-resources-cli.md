<span data-ttu-id="a3f26-101">usar tooadd un grupo de recursos de etiqueta tooa, **del conjunto de grupos de azure**.</span><span class="sxs-lookup"><span data-stu-id="a3f26-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="a3f26-102">Si el grupo de recursos de hello no tiene las etiquetas existentes, pasar etiqueta Hola.</span><span class="sxs-lookup"><span data-stu-id="a3f26-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="a3f26-103">Las etiquetas se actualizan en conjunto.</span><span class="sxs-lookup"><span data-stu-id="a3f26-103">Tags are updated as a whole.</span></span> <span data-ttu-id="a3f26-104">Si desea tooadd un grupo de recursos de tooa de etiqueta con las etiquetas existentes, pase todas las etiquetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3f26-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="a3f26-105">Los recursos de un grupo de recursos no heredan las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="a3f26-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="a3f26-106">tooadd un recurso de tooa etiqueta, utilice **conjunto de recursos de azure**.</span><span class="sxs-lookup"><span data-stu-id="a3f26-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="a3f26-107">Pasar Hola número de versión de API para el tipo de recurso de Hola que va a agregar la etiqueta de Hola a.</span><span class="sxs-lookup"><span data-stu-id="a3f26-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="a3f26-108">Si necesita tooretrieve Hola API versión, usar hello siguiente comando con el proveedor de recursos de hello para el tipo de hello que esté configurando:</span><span class="sxs-lookup"><span data-stu-id="a3f26-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="a3f26-109">En los resultados de hello, buscar el tipo de recurso de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="a3f26-109">In hello results, look for hello resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="a3f26-110">Ahora, proporcione esa versión de API, el nombre del grupo de recursos, el nombre del recurso, el tipo de recurso y el valor de etiqueta como parámetros.</span><span class="sxs-lookup"><span data-stu-id="a3f26-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="a3f26-111">Las etiquetas existen directamente en los recursos y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3f26-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="a3f26-112">toosee las etiquetas existentes hello, obtener un grupo de recursos y sus recursos con **mostrar grupo azure**.</span><span class="sxs-lookup"><span data-stu-id="a3f26-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="a3f26-113">Que devuelve los metadatos sobre el grupo de recursos de hello, incluido cualquier tooit etiquetas aplicadas.</span><span class="sxs-lookup"><span data-stu-id="a3f26-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="a3f26-114">Ver etiquetas de Hola para un recurso determinado mediante **mostrar recursos de azure**.</span><span class="sxs-lookup"><span data-stu-id="a3f26-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="a3f26-115">tooretrieve todos los recursos de hello con un valor de etiqueta, utilice:</span><span class="sxs-lookup"><span data-stu-id="a3f26-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="a3f26-116">tooretrieve todos los grupos de recursos de hello con un valor de etiqueta, utilice:</span><span class="sxs-lookup"><span data-stu-id="a3f26-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="a3f26-117">Puede ver las etiquetas existentes hello en su suscripción con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a3f26-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
