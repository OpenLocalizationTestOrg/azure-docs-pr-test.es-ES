Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *westeurope* ubicación.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

toosee hello las ubicaciones disponibles, ejecute hello `az appservice list-locations` comando. Generalmente crea recursos en una región cercana.
