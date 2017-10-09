---
title: una VM de Linux en Azure con varias NIC aaaCreate | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una VM de Linux con varias NIC había conectado tooit mediante plantillas de hello Azure CLI 2.0 o administrador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="65a47-103">¿Cómo toocreate una máquina virtual de Linux en Azure con red varias tarjetas de interfaz</span><span class="sxs-lookup"><span data-stu-id="65a47-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="65a47-104">Puede crear una máquina virtual (VM) de Azure que tiene varios tooit de interfaces (NIC) que están conectados de red virtual.</span><span class="sxs-lookup"><span data-stu-id="65a47-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="65a47-105">Un escenario común es toohave subredes diferentes para la conectividad de front-end y back-end o una red dedicada tooa supervisión o una solución de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="65a47-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="65a47-106">Este artículo se detalla cómo toocreate una máquina virtual con varias NIC conectado tooit y cómo NIC tooadd o quitar de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="65a47-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="65a47-107">Para obtener información detallada, incluyendo cómo toocreate varios NIC dentro de su propio Bash secuencias de comandos, obtenga más información sobre [implementar máquinas virtuales de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="65a47-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="65a47-108">Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.</span><span class="sxs-lookup"><span data-stu-id="65a47-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="65a47-109">Este artículo detalla cómo toocreate una VM con varias NIC con Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="65a47-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="65a47-110">También puede realizar estos pasos con hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="65a47-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="65a47-111">Creación de recursos de apoyo</span><span class="sxs-lookup"><span data-stu-id="65a47-111">Create supporting resources</span></span>
<span data-ttu-id="65a47-112">Hola de instalación más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="65a47-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="65a47-113">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="65a47-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="65a47-114">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="65a47-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="65a47-115">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="65a47-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="65a47-116">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="65a47-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="65a47-117">Crear red virtual de hello con [crear red virtual de red az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="65a47-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="65a47-118">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* y subred denominada *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="65a47-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="65a47-119">Crear una subred para el tráfico de back-end de hello con [crear subredes de red virtual de red az](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="65a47-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="65a47-120">Hello en el ejemplo siguiente se crea una subred denominada *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="65a47-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="65a47-121">Cree un grupo de seguridad de red con [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="65a47-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="65a47-122">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="65a47-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="65a47-123">Creación y configuración de varias NIC</span><span class="sxs-lookup"><span data-stu-id="65a47-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="65a47-124">Creación de dos NIC con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="65a47-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="65a47-125">Hello en el ejemplo siguiente se crea dos NIC, denominadas *myNic1* y *myNic2*conectados grupo de seguridad de red de hello, con una NIC conectan tooeach subred:</span><span class="sxs-lookup"><span data-stu-id="65a47-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="65a47-126">Crear una máquina virtual y adjuntar Hola NIC</span><span class="sxs-lookup"><span data-stu-id="65a47-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="65a47-127">Cuando creas Hola de máquina virtual, especifique Hola NIC creadas con `--nics`.</span><span class="sxs-lookup"><span data-stu-id="65a47-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="65a47-128">También debe tootake cuidado al seleccionar Hola tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65a47-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="65a47-129">No hay límite para el número total de Hola de NIC que se puede agregar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="65a47-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="65a47-130">Más información sobre los [tamaños de máquina virtual Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="65a47-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="65a47-131">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="65a47-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="65a47-132">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="65a47-132">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="65a47-133">Agregar un tooa NIC virtual</span><span class="sxs-lookup"><span data-stu-id="65a47-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="65a47-134">los pasos anteriores de Hello crean una máquina virtual con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="65a47-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="65a47-135">También puede agregar tooan NIC existente VM con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="65a47-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="65a47-136">Cree otra NIC con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="65a47-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="65a47-137">Hello en el ejemplo siguiente se crea una NIC denominada *myNic3* conectado toohello subred de back-end y el grupo de seguridad de red creado en los pasos anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="65a47-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="65a47-138">tooadd una NIC tooan VM existente, primero desasignar Hola VM con [az vm desasignar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="65a47-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="65a47-139">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="65a47-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="65a47-140">Agregar Hola NIC con [agregar nic de vm az](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="65a47-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="65a47-141">Agrega Hello en el ejemplo siguiente se *myNic3* demasiado*myVM*:</span><span class="sxs-lookup"><span data-stu-id="65a47-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="65a47-142">Iniciar Hola VM con [inicio de vm az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="65a47-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="65a47-143">Eliminación de una NIC de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="65a47-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="65a47-144">tooremove una NIC de una máquina virtual existente, en primer lugar desasignar Hola VM con [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="65a47-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="65a47-145">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="65a47-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="65a47-146">Quitar Hola NIC con [az vm nic quitar](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="65a47-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="65a47-147">Quita de Hello en el ejemplo siguiente se *myNic3* de *myVM*:</span><span class="sxs-lookup"><span data-stu-id="65a47-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="65a47-148">Iniciar Hola VM con [inicio de vm az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="65a47-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="65a47-149">Creación de varias NIC con plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65a47-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="65a47-150">Plantillas de administrador de recursos de Azure utilizan declarativa toodefine de archivos JSON en su entorno.</span><span class="sxs-lookup"><span data-stu-id="65a47-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="65a47-151">Puede leer la [introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65a47-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="65a47-152">Plantillas del Administrador de recursos proporcionan una manera toocreate varias instancias de un recurso durante la implementación, como la creación de varias NIC.</span><span class="sxs-lookup"><span data-stu-id="65a47-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="65a47-153">Usa *copia* número de hello toospecify de toocreate de instancias:</span><span class="sxs-lookup"><span data-stu-id="65a47-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="65a47-154">Más información sobre la [creación de varias instancias mediante *copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="65a47-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="65a47-155">También puede usar un `copyIndex()` toothen anexar un nombre de recurso tooa número, que le permite toocreate `myNic1`, `myNic2`, etc. Hola continuación muestra un ejemplo de anexar el valor de índice de hello:</span><span class="sxs-lookup"><span data-stu-id="65a47-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="65a47-156">Puede leer un ejemplo completo de [cómo crear varias NIC con plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="65a47-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65a47-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65a47-157">Next steps</span></span>
<span data-ttu-id="65a47-158">Revisión [tamaños de VM de Linux](sizes.md) al tratar de toocreating una máquina virtual con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="65a47-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="65a47-159">Pagar el número máximo de toohello de atención de NIC es compatible con el tamaño de cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65a47-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
