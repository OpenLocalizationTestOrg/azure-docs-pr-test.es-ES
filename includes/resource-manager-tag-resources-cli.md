<span data-ttu-id="83e77-101">Para agregar una etiqueta a un grupo de recursos, use el **conjunto de grupos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="83e77-101">To add a tag to a resource group, use **azure group set**.</span></span> <span data-ttu-id="83e77-102">Si el grupo de recursos no tiene etiquetas, pase la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="83e77-102">If the resource group does not have any existing tags, pass in the tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="83e77-103">Las etiquetas se actualizan en conjunto.</span><span class="sxs-lookup"><span data-stu-id="83e77-103">Tags are updated as a whole.</span></span> <span data-ttu-id="83e77-104">Si desea agregar una etiqueta a un grupo de recursos que ya tiene etiquetas, pase todas las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="83e77-104">If you want to add a tag to a resource group that has existing tags, pass all the tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="83e77-105">Los recursos de un grupo de recursos no heredan las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="83e77-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="83e77-106">Para agregar una etiqueta a un recurso, use el **conjunto de recursos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="83e77-106">To add a tag to a resource, use **azure resource set**.</span></span> <span data-ttu-id="83e77-107">Pase el número de versión de API para el tipo de recurso al que está agregando la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="83e77-107">Pass the API version number for the resource type that you are adding the tag to.</span></span> <span data-ttu-id="83e77-108">Si necesita recuperar la versión de API, utilice el siguiente comando con el proveedor de recursos para el tipo que se va a establecer:</span><span class="sxs-lookup"><span data-stu-id="83e77-108">If you need to retrieve the API version, use the following command with the resource provider for the type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="83e77-109">En los resultados, busque el tipo de recurso que desee.</span><span class="sxs-lookup"><span data-stu-id="83e77-109">In the results, look for the resource type you want.</span></span>

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

<span data-ttu-id="83e77-110">Ahora, proporcione esa versión de API, el nombre del grupo de recursos, el nombre del recurso, el tipo de recurso y el valor de etiqueta como parámetros.</span><span class="sxs-lookup"><span data-stu-id="83e77-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="83e77-111">Las etiquetas existen directamente en los recursos y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="83e77-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="83e77-112">Para ver las etiquetas existentes, obtenga un grupo de recursos y sus recursos con **azure group show**.</span><span class="sxs-lookup"><span data-stu-id="83e77-112">To see the existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="83e77-113">Que devuelve metadatos sobre el grupo de recursos, incluidas las etiquetas aplicadas al mismo.</span><span class="sxs-lookup"><span data-stu-id="83e77-113">Which returns metadata about the resource group, including any tags applied to it.</span></span>

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

<span data-ttu-id="83e77-114">Para ver las etiquetas de un recurso específico, use **azure resource show**.</span><span class="sxs-lookup"><span data-stu-id="83e77-114">You view the tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="83e77-115">Para recuperar todos los recursos con un valor de etiqueta, utilice:</span><span class="sxs-lookup"><span data-stu-id="83e77-115">To retrieve all the resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="83e77-116">Para recuperar todos los grupos de recursos con un valor de etiqueta, utilice:</span><span class="sxs-lookup"><span data-stu-id="83e77-116">To retrieve all the resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="83e77-117">Puede ver las etiquetas existentes en su suscripción con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="83e77-117">You can view the existing tags in your subscription with the following command:</span></span>

```azurecli
azure tag list
```
