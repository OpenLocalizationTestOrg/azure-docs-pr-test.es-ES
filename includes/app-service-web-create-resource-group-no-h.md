<span data-ttu-id="c0f46-101">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c0f46-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="c0f46-102">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="c0f46-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="c0f46-103">Generalmente se crean el grupo de recursos y los recursos en una región cercana.</span><span class="sxs-lookup"><span data-stu-id="c0f46-103">You generally create your resource group and the resources in a region near you.</span></span> <span data-ttu-id="c0f46-104">Para ver todas las ubicaciones admitidas para aplicaciones web de Azure, ejecute el comando `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="c0f46-104">To see all supported locations for Azure Web Apps, run the `az appservice list-locations` command.</span></span> 