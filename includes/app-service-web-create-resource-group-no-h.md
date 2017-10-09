<span data-ttu-id="85ef5-101">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="85ef5-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="85ef5-102">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.</span><span class="sxs-lookup"><span data-stu-id="85ef5-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="85ef5-103">Normalmente crea el recurso hello y grupo de recursos en una región cerca de usted.</span><span class="sxs-lookup"><span data-stu-id="85ef5-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="85ef5-104">ubicaciones de toosee todos los admitidos para las aplicaciones Web de Azure, ejecute hello `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="85ef5-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
