## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>de una máquina virtual

Crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando. 

Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* y crea las claves de SSH si aún no existen en una ubicación de la clave predeterminada. toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Cuando se ha creado la VM de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo. Tome nota de hello `publicIpAddress`. Esta dirección es hello tooaccess usa máquinas virtuales.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a>Apertura del puerto 80 para el tráfico web 

De forma predeterminada, solo se permiten conexiones mediante SSH con las máquinas virtuales Linux implementadas en Azure. Ya que esta máquina virtual va toobe un servidor web, necesita tooopen puerto 80 de hello internet. Hola de uso [az de vm abrir puerto](/cli/azure/vm#open-port) comando tooopen hello deseado puerto.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>Conexión SSH con la máquina virtual


Si aún no sabe Hola dirección IP pública de la máquina virtual, ejecute hello [lista de ip pública de red az](/cli/azure/network/public-ip#list) comando:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola. Sustituya la dirección IP pública correcta del saludo de la máquina virtual. En este ejemplo, es la dirección IP de hello *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

