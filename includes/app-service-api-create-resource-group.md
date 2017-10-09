<span data-ttu-id="7bd39-101">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="7bd39-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="7bd39-102">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.</span><span class="sxs-lookup"><span data-stu-id="7bd39-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="7bd39-103">toosee hello las ubicaciones disponibles, ejecute hello `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="7bd39-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="7bd39-104">Generalmente crea recursos en una región cercana.</span><span class="sxs-lookup"><span data-stu-id="7bd39-104">You generally create resources in a region near you.</span></span>
