---
title: una VM de Linux en Azure con varias NIC aaaCreate | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una VM de Linux con varias NIC había conectado tooit mediante plantillas de CLI de Azure o el Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="f8dbd-103">Crear una máquina virtual Linux con varias NIC con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f8dbd-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="f8dbd-104">Puede crear una máquina virtual (VM) de Azure que tiene varios tooit de interfaces (NIC) que están conectados de red virtual.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="f8dbd-105">Un escenario común es toohave subredes diferentes para la conectividad de front-end y back-end o una red dedicada tooa supervisión o una solución de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="f8dbd-106">Este artículo proporciona comandos rápidos toocreate una máquina virtual con varias tooit NIC conectadas.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="f8dbd-107">Para obtener información detallada, incluyendo cómo toocreate varios NIC dentro de su propio Bash secuencias de comandos, obtenga más información sobre [implementar máquinas virtuales de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f8dbd-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="f8dbd-108">Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="f8dbd-109">Debe adjuntar varios NIC cuando cree una máquina virtual: no se puede agregar tooan NIC existente VM con hello 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="f8dbd-110">También puede [agregar tooan NIC existente VM con hello Azure CLI 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="f8dbd-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="f8dbd-111">También puede [crear una máquina virtual en función de los discos virtuales original de hello](copy-vm.md) y cree varios NIC como implementar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f8dbd-112">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="f8dbd-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="f8dbd-113">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="f8dbd-114">[Azure 1.0 de CLI](#create-supporting-resources) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="f8dbd-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f8dbd-115">[Azure 2.0 CLI](multiple-nics.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="f8dbd-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="f8dbd-116">Creación de recursos de apoyo</span><span class="sxs-lookup"><span data-stu-id="f8dbd-116">Create supporting resources</span></span>
<span data-ttu-id="f8dbd-117">Asegúrese de que dispone de hello [CLI de Azure](../../cli-install-nodejs.md) iniciado la sesión y utilizar el modo de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="f8dbd-118">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f8dbd-119">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="f8dbd-120">En primer lugar, cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-120">First, create a resource group.</span></span> <span data-ttu-id="f8dbd-121">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="f8dbd-122">Crear un toohold de cuenta de almacenamiento de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="f8dbd-123">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="f8dbd-124">Crear una red virtual tooconnect las máquinas virtuales se.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="f8dbd-125">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con un prefijo de dirección de *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="f8dbd-126">Cree dos subredes de red virtual: una para el tráfico front-end y otra para el tráfico back-end.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="f8dbd-127">Hello en el ejemplo siguiente se crea dos subredes, denominados *mySubnetFrontEnd* y *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="f8dbd-128">Creación y configuración de varias NIC</span><span class="sxs-lookup"><span data-stu-id="f8dbd-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="f8dbd-129">Encontrará más detalles acerca de [implementar varios NIC con hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), incluidos secuencias de comandos de proceso de Hola de bucle a través de toocreate todas las NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="f8dbd-130">Hello en el ejemplo siguiente se crea dos NIC, denominadas *myNic1* y *myNic2*, con una NIC conectan tooeach subred:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="f8dbd-131">Normalmente se crea también un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) o [equilibrador de carga](../../load-balancer/load-balancer-overview.md) toohelp administrar y distribuir el tráfico entre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="f8dbd-132">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="f8dbd-133">Enlazar el grupo de seguridad de red de NIC toohello mediante `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="f8dbd-134">enlaza Hello en el ejemplo siguiente se *myNic1* y *myNic2* con *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="f8dbd-135">Crear una máquina virtual y adjuntar Hola NIC</span><span class="sxs-lookup"><span data-stu-id="f8dbd-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="f8dbd-136">Al crear Hola VM, ahora especificar varios NIC.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="f8dbd-137">En su lugar mediante `--nic-name` tooprovide una sola NIC, en su lugar use `--nic-names` y proporcionar una lista separada por comas de NIC.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="f8dbd-138">También debe tootake cuidado al seleccionar Hola tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="f8dbd-139">No hay límite para el número total de Hola de NIC que se puede agregar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="f8dbd-140">Más información sobre los [tamaños de máquina virtual Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="f8dbd-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="f8dbd-141">Hello en el ejemplo siguiente se muestra cómo toospecify varios NIC y, a continuación, en una máquina virtual cambia el tamaño que admite el uso de varias NIC (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="f8dbd-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="f8dbd-142">Creación de varias NIC con plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8dbd-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="f8dbd-143">Plantillas de administrador de recursos de Azure utilizan declarativa toodefine de archivos JSON en su entorno.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="f8dbd-144">Puede leer la [introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8dbd-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f8dbd-145">Plantillas del Administrador de recursos proporcionan una manera toocreate varias instancias de un recurso durante la implementación, como la creación de varias NIC.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="f8dbd-146">Usa *copia* número de hello toospecify de toocreate de instancias:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="f8dbd-147">Más información sobre la [creación de varias instancias mediante *copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f8dbd-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="f8dbd-148">También puede usar un `copyIndex()` toothen anexar un nombre de recurso tooa número, que le permite toocreate `myNic1`, `myNic2`, etc. Hola continuación muestra un ejemplo de anexar el valor de índice de hello:</span><span class="sxs-lookup"><span data-stu-id="f8dbd-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="f8dbd-149">Puede leer un ejemplo completo de [cómo crear varias NIC con plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="f8dbd-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8dbd-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8dbd-150">Next steps</span></span>
<span data-ttu-id="f8dbd-151">Asegúrese de que tooreview [tamaños de VM de Linux](sizes.md) al tratar de toocreating una máquina virtual con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="f8dbd-152">Pagar el número máximo de toohello de atención de NIC es compatible con el tamaño de cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="f8dbd-153">Recuerde que no se puede agregar tooan de NIC adicional existentes de la máquina virtual, debe crear todas las NIC de hello al implementar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="f8dbd-154">Tenga cuidado al planear la toomake de las implementaciones que dispone de conectividad de red de todos los Hola necesario desde el principio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8dbd-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

