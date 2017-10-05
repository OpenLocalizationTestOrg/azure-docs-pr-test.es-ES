---
title: "Implementación de máquinas virtuales Linux en una red existente con la CLI de Azure 1.0 | Microsoft Docs"
description: "Implementación de una máquina virtual Linux en una red virtual existente mediante la CLI de Azure 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="cfcb5-103">Implementación de una máquina virtual Linux en una red virtual de Azure existente mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="cfcb5-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="cfcb5-104">En este artículo se muestra cómo usar la CLI de Azure 1.0 para implementar una máquina virtual (VM) en una red virtual (VNet) existente.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="cfcb5-105">Los requisitos son:</span><span class="sxs-lookup"><span data-stu-id="cfcb5-105">The requirements are:</span></span>

- <span data-ttu-id="cfcb5-106">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="cfcb5-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="cfcb5-107">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="cfcb5-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="cfcb5-108">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="cfcb5-108">CLI versions to complete the task</span></span>
<span data-ttu-id="cfcb5-109">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="cfcb5-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="cfcb5-110">[CLI de Azure 1.0](#quick-commands): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="cfcb5-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="cfcb5-111">[CLI de Azure 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="cfcb5-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="cfcb5-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="cfcb5-112">Quick Commands</span></span>

<span data-ttu-id="cfcb5-113">Si necesita realizar rápidamente la tarea, en la siguiente sección se detallan los comandos necesarios.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="cfcb5-114">Se puede encontrar información más detallada y contexto para cada paso en el resto del documento, [comenzando aquí](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="cfcb5-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="cfcb5-115">Requisitos previos: grupo de recursos, red virtual, NSG con SSH entrante, subred.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="cfcb5-116">Reemplace los ejemplos por su propia configuración.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="cfcb5-117">Implementación de la máquina virtual en la infraestructura de la red virtual</span><span class="sxs-lookup"><span data-stu-id="cfcb5-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="cfcb5-118">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="cfcb5-118">Detailed walkthrough</span></span>

<span data-ttu-id="cfcb5-119">Los recursos de Azure, como las redes virtuales y los grupos de seguridad de red, deben ser recursos estáticos y de larga duración que se implementen en raras ocasiones.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="cfcb5-120">Una vez que se ha implementado una red virtual, se puede volver a utilizar con nuevas implementaciones sin efectos adversos para la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="cfcb5-121">Imagine que una red virtual es un conmutador de red de hardware tradicional.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="cfcb5-122">No sería preciso configurar un conmutador nuevo en cada implementación.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="cfcb5-123">Con una red virtual configurada correctamente, podemos seguir implementando nuevos servidores en esa red virtual una y otra vez con pocos, en caso de que haya, cambios necesarios durante la vida útil de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="cfcb5-124">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cfcb5-124">Create the resource group</span></span>

<span data-ttu-id="cfcb5-125">En primer lugar, creará un grupo de recursos para organizar todo lo que vaya a crear en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="cfcb5-126">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfcb5-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="cfcb5-127">Crear la red virtual</span><span class="sxs-lookup"><span data-stu-id="cfcb5-127">Create the VNet</span></span>

<span data-ttu-id="cfcb5-128">El primer paso es crear una red virtual en la que iniciar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="cfcb5-129">La red virtual contiene una subred para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="cfcb5-130">Para más información, consulte [Creación de una red virtual usando la CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cfcb5-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="cfcb5-131">Creación del grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="cfcb5-131">Create the network security group</span></span>

<span data-ttu-id="cfcb5-132">La subred se crea detrás de un grupo de seguridad de red existente, de modo que cree primero el grupo de seguridad de red y después la subred.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="cfcb5-133">Los grupos de seguridad de red de Azure equivalen a un firewall en el nivel de red.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="cfcb5-134">Para más información sobre los grupos de seguridad de red de Azure, consulte [Creación de grupos de seguridad de red en la CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cfcb5-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="cfcb5-135">Agregar regla de permiso de SSH entrante</span><span class="sxs-lookup"><span data-stu-id="cfcb5-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="cfcb5-136">La máquina virtual debe tener acceso desde Internet por lo que es necesario una regla que permita que el tráfico entrante en el puerto 22 pase por la red y vaya al puerto 22 de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="cfcb5-137">Agregar una subred a la red virtual</span><span class="sxs-lookup"><span data-stu-id="cfcb5-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="cfcb5-138">Las máquinas virtuales dentro de la red virtual deben estar ubicadas en una subred.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="cfcb5-139">Cada red virtual puede tener varias subredes.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="cfcb5-140">Cree la subred y asóciela con el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="cfcb5-141">La subred se agrega ahora dentro de la red virtual asociada con la regla y el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="cfcb5-142">Incorporación de un VNic a la subred</span><span class="sxs-lookup"><span data-stu-id="cfcb5-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="cfcb5-143">Las tarjetas de interfaz de red virtual (VNics) son importantes porque las puede reutilizar conectándolas a diferentes máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="cfcb5-144">En este enfoque la vNic se mantiene como recurso estático mientras que las máquinas virtuales pueden ser temporales.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="cfcb5-145">Cree una VNic y asóciela a la subred que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="cfcb5-146">Implemente la máquina virtual en la red virtual y el grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="cfcb5-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="cfcb5-147">Ahora tiene una red virtual y una subred dentro de ella, además de un grupo de seguridad de red que sirve para proteger la subred al bloquear todo el tráfico de entrada, excepto el del puerto 22 para SSH.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="cfcb5-148">Ahora se puede implementar la máquina virtual dentro de esta infraestructura de red existente.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="cfcb5-149">Mediante la CLI de Azure y el comando `azure vm create`, se implementa la máquina virtual Linux en el grupo de recursos de Azure, la red virtual, la subred y la VNic ya existentes.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="cfcb5-150">Para más información sobre el uso de la CLI para implementar una máquina virtual completa, consulte [Creación de un entorno de Linux completo mediante la CLI de Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="cfcb5-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="cfcb5-151">Por medio de marcadores de CLI para llamar a los recursos existentes, se indica a Azure que implemente la máquina virtual dentro de la red existente.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="cfcb5-152">Una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="cfcb5-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="cfcb5-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cfcb5-153">Next steps</span></span>

* [<span data-ttu-id="cfcb5-154">Uso de una plantilla de Azure Resource Manager para crear una implementación específica</span><span class="sxs-lookup"><span data-stu-id="cfcb5-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="cfcb5-155">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="cfcb5-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="cfcb5-156">Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cfcb5-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
