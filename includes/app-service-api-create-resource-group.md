<span data-ttu-id="fa454-101">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fa454-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="fa454-102">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="fa454-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="fa454-103">Para ver las ubicaciones disponibles, ejecute el comando `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="fa454-103">To see the available locations, run the `az appservice list-locations` command.</span></span> <span data-ttu-id="fa454-104">Generalmente crea recursos en una región cercana.</span><span class="sxs-lookup"><span data-stu-id="fa454-104">You generally create resources in a region near you.</span></span>
