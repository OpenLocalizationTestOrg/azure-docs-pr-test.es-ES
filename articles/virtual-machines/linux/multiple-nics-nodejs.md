---
title: "Creación de una máquina virtual Linux en Azure con varias NIC | Microsoft Docs"
description: "Aprenda a crear una máquina virtual Linux con varias NIC conectadas a ella mediante la CLI de Azure o plantillas de Resource Manager."
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
ms.openlocfilehash: 814825cce61909167a1247a96c17a3ee9c5f2af4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="253ef-103">Creación de una máquina virtual Linux con varias NIC mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="253ef-103">Create a Linux virtual machine with multiple NICs using the Azure CLI 1.0</span></span>
<span data-ttu-id="253ef-104">Puede crear una máquina virtual (VM) en Azure que tenga asociadas varias interfaces de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="253ef-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="253ef-105">Un escenario común es tener distintas subredes para la conectividad front-end y back-end o una red dedicada a una solución de supervisión o copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="253ef-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="253ef-106">En este artículo se proporcionan comandos rápidos para crear una máquina virtual que tiene conectadas varias NIC.</span><span class="sxs-lookup"><span data-stu-id="253ef-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="253ef-107">Para más información, lo que incluye cómo crear varias NIC dentro de sus propios scripts de Bash, lea más sobre la [implementación de máquinas virtuales con varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="253ef-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="253ef-108">Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.</span><span class="sxs-lookup"><span data-stu-id="253ef-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="253ef-109">Cuando crea una máquina virtual, debe asociar varias NIC; no es posible agregar NIC a una máquina virtual existente. con la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="253ef-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM with the Azure CLI 1.0.</span></span> <span data-ttu-id="253ef-110">Puede [agregar varias NIC a una máquina virtual existente con la versión 2.0 de la CLI de Azure](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="253ef-110">You can [add NICs to an existing VM with the Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="253ef-111">También puede [crear una máquina virtual en función de los discos virtuales originales](copy-vm.md) y crear varias NIC mientras implementa la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="253ef-111">You can also [create a VM based on the original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy the VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="253ef-112">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="253ef-112">CLI versions to complete the task</span></span>
<span data-ttu-id="253ef-113">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="253ef-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="253ef-114">[CLI de Azure 1.0](#create-supporting-resources): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="253ef-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="253ef-115">[CLI de Azure 2.0](multiple-nics.md): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="253ef-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="253ef-116">Creación de recursos de apoyo</span><span class="sxs-lookup"><span data-stu-id="253ef-116">Create supporting resources</span></span>
<span data-ttu-id="253ef-117">Asegúrese de haber iniciado sesión en la [CLI de Azure](../../cli-install-nodejs.md) y que usa el modo de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="253ef-117">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="253ef-118">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="253ef-118">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="253ef-119">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="253ef-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="253ef-120">En primer lugar, cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="253ef-120">First, create a resource group.</span></span> <span data-ttu-id="253ef-121">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="253ef-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="253ef-122">Cree una cuenta de almacenamiento que contenga las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="253ef-122">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="253ef-123">En el ejemplo siguiente se crea una cuenta de almacenamiento denominada *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="253ef-123">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="253ef-124">Cree una red virtual para conectar las máquinas virtuales a:</span><span class="sxs-lookup"><span data-stu-id="253ef-124">Create a virtual network to connect your VMs to.</span></span> <span data-ttu-id="253ef-125">En el ejemplo siguiente se crea una red virtual denominada *myVnet* con un prefijo de dirección de *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="253ef-125">The following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="253ef-126">Cree dos subredes de red virtual: una para el tráfico front-end y otra para el tráfico back-end.</span><span class="sxs-lookup"><span data-stu-id="253ef-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="253ef-127">En el ejemplo siguiente se crean dos subredes denominadas *mySubnetFrontEnd* y *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="253ef-127">The following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

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

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="253ef-128">Creación y configuración de varias NIC</span><span class="sxs-lookup"><span data-stu-id="253ef-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="253ef-129">Puede leer información más detallada sobre la [implementación de varias NIC con la CLI de Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), como los scripts del proceso de paso de bucle para crear todas las NIC.</span><span class="sxs-lookup"><span data-stu-id="253ef-129">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="253ef-130">En el ejemplo siguiente se crean dos NIC, denominadas *myNic1* y *myNic2*, una de las cuales se conecta con cada subred:</span><span class="sxs-lookup"><span data-stu-id="253ef-130">The following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting to each subnet:</span></span>

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

<span data-ttu-id="253ef-131">Normalmente también crearía un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) o [un equilibrador de carga](../../load-balancer/load-balancer-overview.md) para administrar y distribuir el tráfico entre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="253ef-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="253ef-132">En el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="253ef-132">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="253ef-133">Enlace las NIC al grupo de seguridad de red mediante `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="253ef-133">Bind your NICs to the Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="253ef-134">En el ejemplo siguiente se enlaza *myNic1* y *myNic2* con *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="253ef-134">The following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="253ef-135">Creación de una máquina virtual y conexión de las NIC</span><span class="sxs-lookup"><span data-stu-id="253ef-135">Create a VM and attach the NICs</span></span>
<span data-ttu-id="253ef-136">Al crear la máquina virtual, ahora especifica varias NIC.</span><span class="sxs-lookup"><span data-stu-id="253ef-136">When creating the VM, you now specify multiple NICs.</span></span> <span data-ttu-id="253ef-137">En lugar de usar `--nic-name` para proporcionar una única NIC, usará `--nic-names` y proporcionará una lista de NIC separadas por coma.</span><span class="sxs-lookup"><span data-stu-id="253ef-137">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="253ef-138">También debe tener cuidado al seleccionar el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="253ef-138">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="253ef-139">Existen límites para el número total de NIC que se pueden agregar a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="253ef-139">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="253ef-140">Más información sobre los [tamaños de máquina virtual Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="253ef-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="253ef-141">En el ejemplo siguiente se muestra cómo especificar varias NIC y, luego, un tamaño de máquina virtual que admita el uso de varias NIC (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="253ef-141">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

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

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="253ef-142">Creación de varias NIC con plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="253ef-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="253ef-143">Las plantillas de Azure Resource Manager emplean archivos JSON declarativos para definir el entorno.</span><span class="sxs-lookup"><span data-stu-id="253ef-143">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="253ef-144">Puede leer la [introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="253ef-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="253ef-145">Las plantillas de Resource Manager ofrecen una manera de crear varias instancias de un recurso durante la implementación; por ejemplo, se pueden crear varias NIC.</span><span class="sxs-lookup"><span data-stu-id="253ef-145">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="253ef-146">Utilizará el comando *copy* para especificar el número de instancias que se crearán:</span><span class="sxs-lookup"><span data-stu-id="253ef-146">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="253ef-147">Más información sobre la [creación de varias instancias mediante *copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="253ef-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="253ef-148">También puede utilizar `copyIndex()` para anexar un número a un nombre de recurso, lo que le permite crear `myNic1`, `myNic2`, etc. A continuación se muestra un ejemplo de cómo anexar el valor de índice:</span><span class="sxs-lookup"><span data-stu-id="253ef-148">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="253ef-149">Puede leer un ejemplo completo de [cómo crear varias NIC con plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="253ef-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="253ef-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="253ef-150">Next steps</span></span>
<span data-ttu-id="253ef-151">Asegúrese de revisar los [tamaños de máquina virtual Linux](sizes.md) al intentar crear una máquina virtual con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="253ef-151">Make sure to review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="253ef-152">Preste atención al número máximo de NIC que admite cada tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="253ef-152">Pay attention to the maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="253ef-153">Recuerde que no se pueden agregar NIC adicionales a una máquina virtual existente; debe crear todas las NIC al implementar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="253ef-153">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span></span> <span data-ttu-id="253ef-154">Tenga cuidado al planear las implementaciones para asegurarse de que dispone de toda la conectividad de red necesaria desde el principio.</span><span class="sxs-lookup"><span data-stu-id="253ef-154">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span></span>

