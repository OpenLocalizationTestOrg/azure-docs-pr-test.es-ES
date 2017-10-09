Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Normalmente crea el recurso hello y grupo de recursos en una región cerca de usted. ubicaciones de toosee todos los admitidos para las aplicaciones Web de Azure, ejecute hello `az appservice list-locations` comando. 
