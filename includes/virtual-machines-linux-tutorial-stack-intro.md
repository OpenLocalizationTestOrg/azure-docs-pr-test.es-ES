## <a name="create-a-resource-group"></a><span data-ttu-id="b8bd9-101">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b8bd9-101">Create a resource group</span></span>

<span data-ttu-id="b8bd9-102">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="b8bd9-103">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b8bd9-104">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="b8bd9-105">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b8bd9-105">Create a virtual machine</span></span>

<span data-ttu-id="b8bd9-106">Crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="b8bd9-107">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* y crea las claves de SSH si aún no existen en una ubicación de la clave predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="b8bd9-108">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="b8bd9-109">Cuando se ha creado la VM de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="b8bd9-110">Tome nota de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="b8bd9-111">Esta dirección es hello tooaccess usa máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-111">This address is used tooaccess hello VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="b8bd9-112">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="b8bd9-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="b8bd9-113">De forma predeterminada, solo se permiten conexiones mediante SSH con las máquinas virtuales Linux implementadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="b8bd9-114">Ya que esta máquina virtual va toobe un servidor web, necesita tooopen puerto 80 de hello internet.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="b8bd9-115">Hola de uso [az de vm abrir puerto](/cli/azure/vm#open-port) comando tooopen hello deseado puerto.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="b8bd9-116">Conexión SSH con la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b8bd9-116">SSH into your VM</span></span>


<span data-ttu-id="b8bd9-117">Si aún no sabe Hola dirección IP pública de la máquina virtual, ejecute hello [lista de ip pública de red az](/cli/azure/network/public-ip#list) comando:</span><span class="sxs-lookup"><span data-stu-id="b8bd9-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="b8bd9-118">Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="b8bd9-119">Sustituya la dirección IP pública correcta del saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="b8bd9-120">En este ejemplo, es la dirección IP de hello *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="b8bd9-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

