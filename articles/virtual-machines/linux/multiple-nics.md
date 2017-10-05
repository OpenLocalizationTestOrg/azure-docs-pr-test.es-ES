---
title: "Creación de una máquina virtual Linux en Azure con varias NIC | Microsoft Docs"
description: "Aprenda a crear una máquina virtual Linux con varias NIC conectadas a ella mediante la CLI de Azure 2.0 o las plantillas de Resource Manager."
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
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="fc073-103">Cómo crear una máquina virtual Linux en Azure con red varias tarjetas de interfaz de red</span><span class="sxs-lookup"><span data-stu-id="fc073-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="fc073-104">Puede crear una máquina virtual (VM) en Azure que tenga asociadas varias interfaces de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="fc073-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="fc073-105">Un escenario común es tener distintas subredes para la conectividad front-end y back-end o una red dedicada a una solución de supervisión o copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fc073-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="fc073-106">En este artículo describe cómo crear una máquina virtual con varias NIC asociadas a ella y cómo agregar o quitar las NIC de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="fc073-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="fc073-107">Para más información, lo que incluye cómo crear varias NIC dentro de sus propios scripts de Bash, lea más sobre la [implementación de máquinas virtuales con varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fc073-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="fc073-108">Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.</span><span class="sxs-lookup"><span data-stu-id="fc073-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="fc073-109">En este artículo se describe cómo crear una máquina virtual con varias NIC con la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="fc073-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="fc073-110">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fc073-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="fc073-111">Creación de recursos de apoyo</span><span class="sxs-lookup"><span data-stu-id="fc073-111">Create supporting resources</span></span>
<span data-ttu-id="fc073-112">Instale la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fc073-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="fc073-113">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="fc073-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fc073-114">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fc073-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="fc073-115">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fc073-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fc073-116">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="fc073-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="fc073-117">Cree la red virtual con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="fc073-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="fc073-118">En el ejemplo siguiente se crea una red virtual denominada *myVnet* y una subred *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="fc073-118">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="fc073-119">Cree una subred para el tráfico de back-end con [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="fc073-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="fc073-120">En el ejemplo siguiente se crea una subred denominada *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="fc073-120">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="fc073-121">Cree un grupo de seguridad de red con [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="fc073-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="fc073-122">En el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="fc073-122">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="fc073-123">Creación y configuración de varias NIC</span><span class="sxs-lookup"><span data-stu-id="fc073-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="fc073-124">Creación de dos NIC con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="fc073-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="fc073-125">En el ejemplo siguiente se crean dos NIC, denominadas *myNic1* y *myNic2*, conectadas al grupo de seguridad de red, con una NIC conectada con cada subred:</span><span class="sxs-lookup"><span data-stu-id="fc073-125">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="fc073-126">Creación de una máquina virtual y conexión de las NIC</span><span class="sxs-lookup"><span data-stu-id="fc073-126">Create a VM and attach the NICs</span></span>
<span data-ttu-id="fc073-127">Cuando cree la máquina virtual, especifique las NIC creadas con `--nics`.</span><span class="sxs-lookup"><span data-stu-id="fc073-127">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="fc073-128">También debe tener cuidado al seleccionar el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc073-128">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="fc073-129">Existen límites para el número total de NIC que se pueden agregar a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc073-129">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="fc073-130">Más información sobre los [tamaños de máquina virtual Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="fc073-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="fc073-131">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fc073-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fc073-132">En el ejemplo siguiente se crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="fc073-132">The following example creates a VM named *myVM*:</span></span>

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

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="fc073-133">Adición de una NIC a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fc073-133">Add a NIC to a VM</span></span>
<span data-ttu-id="fc073-134">Los pasos anteriores crean una máquina virtual con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="fc073-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="fc073-135">También puede agregar varias NIC a una máquina virtual existente con la versión 2.0 de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc073-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="fc073-136">Cree otra NIC con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="fc073-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="fc073-137">En el ejemplo siguiente se crea una NIC denominada *myNic3* conectada a la subred de back-end y al grupo de seguridad de red creado en los pasos anteriores:</span><span class="sxs-lookup"><span data-stu-id="fc073-137">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="fc073-138">Para agregar una NIC a una máquina virtual existente, en primer lugar desasigne la máquina virtual con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="fc073-138">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="fc073-139">En el ejemplo siguiente se desasigna la máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="fc073-139">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fc073-140">Agregue la NIC con [az vm nic add](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="fc073-140">Add the NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="fc073-141">En el ejemplo siguiente se agrega *myNic3* a *myVM*:</span><span class="sxs-lookup"><span data-stu-id="fc073-141">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="fc073-142">Inicie la máquina virtual con [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="fc073-142">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="fc073-143">Eliminación de una NIC de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fc073-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="fc073-144">Para quitar una NIC de una máquina virtual existente, en primer lugar desasigne la máquina virtual con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="fc073-144">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="fc073-145">En el ejemplo siguiente se desasigna la máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="fc073-145">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fc073-146">Quite la NIC con [az vm nic remove](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="fc073-146">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="fc073-147">En el ejemplo siguiente se quita *myNic3* de *myVM*:</span><span class="sxs-lookup"><span data-stu-id="fc073-147">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="fc073-148">Inicie la máquina virtual con [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="fc073-148">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="fc073-149">Creación de varias NIC con plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc073-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="fc073-150">Las plantillas de Azure Resource Manager emplean archivos JSON declarativos para definir el entorno.</span><span class="sxs-lookup"><span data-stu-id="fc073-150">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="fc073-151">Puede leer la [introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc073-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="fc073-152">Las plantillas de Resource Manager ofrecen una manera de crear varias instancias de un recurso durante la implementación; por ejemplo, se pueden crear varias NIC.</span><span class="sxs-lookup"><span data-stu-id="fc073-152">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="fc073-153">Utilizará el comando *copy* para especificar el número de instancias que se crearán:</span><span class="sxs-lookup"><span data-stu-id="fc073-153">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="fc073-154">Más información sobre la [creación de varias instancias mediante *copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fc073-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="fc073-155">También puede utilizar `copyIndex()` para anexar un número a un nombre de recurso, lo que le permite crear `myNic1`, `myNic2`, etc. A continuación se muestra un ejemplo de cómo anexar el valor de índice:</span><span class="sxs-lookup"><span data-stu-id="fc073-155">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="fc073-156">Puede leer un ejemplo completo de [cómo crear varias NIC con plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="fc073-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc073-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc073-157">Next steps</span></span>
<span data-ttu-id="fc073-158">Revise los [tamaños de máquina virtual Linux](sizes.md) al intentar crear una máquina virtual con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="fc073-158">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="fc073-159">Preste atención al número máximo de NIC que admite cada tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc073-159">Pay attention to the maximum number of NICs each VM size supports.</span></span> 