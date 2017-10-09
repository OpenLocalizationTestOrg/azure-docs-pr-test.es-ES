---
title: "aaaDeploy máquinas virtuales de Linux en la red existente con 1.0 de CLI de Azure | Documentos de Microsoft"
description: "¿Cómo toodeploy una VM de Linux en una red Virtual existente mediante Hola 1.0 de CLI de Azure"
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
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="24ea8-103">¿Cómo toodeploy una máquina virtual de Linux en una red Virtual de Azure existente con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="24ea8-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="24ea8-104">Este artículo muestra cómo toodeploy toouse 1.0 de CLI de Azure una máquina virtual (VM) en una red Virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="24ea8-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="24ea8-105">Hola requisitos son:</span><span class="sxs-lookup"><span data-stu-id="24ea8-105">hello requirements are:</span></span>

- <span data-ttu-id="24ea8-106">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="24ea8-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="24ea8-107">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="24ea8-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="24ea8-108">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="24ea8-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="24ea8-109">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="24ea8-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="24ea8-110">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="24ea8-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="24ea8-111">[Azure 2.0 CLI](deploy-linux-vm-into-existing-vnet-using-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="24ea8-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="24ea8-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="24ea8-112">Quick Commands</span></span>

<span data-ttu-id="24ea8-113">Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios.</span><span class="sxs-lookup"><span data-stu-id="24ea8-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="24ea8-114">Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="24ea8-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="24ea8-115">Requisitos previos: grupo de recursos, red virtual, NSG con SSH entrante, subred.</span><span class="sxs-lookup"><span data-stu-id="24ea8-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="24ea8-116">Reemplace los ejemplos por su propia configuración.</span><span class="sxs-lookup"><span data-stu-id="24ea8-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="24ea8-117">Implementar Hola VM en la infraestructura de red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="24ea8-117">Deploy hello VM into hello virtual network infrastructure</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="24ea8-118">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="24ea8-118">Detailed walkthrough</span></span>

<span data-ttu-id="24ea8-119">Activos de Azure como Hola redes virtuales y grupos de seguridad de red deben ser estáticos y larga duración recursos que rara vez se implementan.</span><span class="sxs-lookup"><span data-stu-id="24ea8-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="24ea8-120">Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa.</span><span class="sxs-lookup"><span data-stu-id="24ea8-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="24ea8-121">Imagine que una red virtual es un conmutador de red de hardware tradicional.</span><span class="sxs-lookup"><span data-stu-id="24ea8-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="24ea8-122">No tendrá tooconfigure hardware completamente nuevo cambiar con cada implementación.</span><span class="sxs-lookup"><span data-stu-id="24ea8-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="24ea8-123">Con una red virtual configurada correctamente, puede seguir el toodeploy nuevos servidores en esa red virtual una y otra vez con pocos, si lo hay, cambios necesarios durante la vigencia de Hola de hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="24ea8-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="24ea8-124">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="24ea8-124">Create hello resource group</span></span>

<span data-ttu-id="24ea8-125">En primer lugar, cree una tooorganize de grupo de recursos todo lo que cree en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="24ea8-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="24ea8-126">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24ea8-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="24ea8-127">Crear red virtual de hello</span><span class="sxs-lookup"><span data-stu-id="24ea8-127">Create hello VNet</span></span>

<span data-ttu-id="24ea8-128">Hola primer paso es toobuild Hola a las máquinas virtuales en un toolaunch de red virtual.</span><span class="sxs-lookup"><span data-stu-id="24ea8-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="24ea8-129">Hola red virtual contiene una subred para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="24ea8-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="24ea8-130">Para obtener más información sobre redes virtuales de Azure, consulte [crear una red virtual mediante el uso de hello CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="24ea8-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="24ea8-131">Crear grupo de seguridad de red de Hola</span><span class="sxs-lookup"><span data-stu-id="24ea8-131">Create hello network security group</span></span>

<span data-ttu-id="24ea8-132">subred de Hola se compila detrás de un grupo de seguridad de red existente por lo que crear grupo de seguridad de red de hello antes de subred Hola.</span><span class="sxs-lookup"><span data-stu-id="24ea8-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="24ea8-133">Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola.</span><span class="sxs-lookup"><span data-stu-id="24ea8-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="24ea8-134">Para obtener más información sobre los grupos de seguridad de red de Azure, vea [cómo grupos de seguridad de red de toocreate Hola CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="24ea8-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="24ea8-135">Agregar regla de permiso de SSH entrante</span><span class="sxs-lookup"><span data-stu-id="24ea8-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="24ea8-136">Hola VM necesita acceso de hello internet para que una regla que permita el puerto de entrada 22 tráfico toobe pasa a través de la red de hello tooport 22 en hello VM es necesario.</span><span class="sxs-lookup"><span data-stu-id="24ea8-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="24ea8-137">Agregar una red virtual de toohello de subred</span><span class="sxs-lookup"><span data-stu-id="24ea8-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="24ea8-138">Las máquinas virtuales de hello red virtual deben estar ubicadas en una subred.</span><span class="sxs-lookup"><span data-stu-id="24ea8-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="24ea8-139">Cada red virtual puede tener varias subredes.</span><span class="sxs-lookup"><span data-stu-id="24ea8-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="24ea8-140">Crear una subred de Hola y asocie al grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="24ea8-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="24ea8-141">Hola subred ahora se agregaron dentro de la red virtual de Hola y asociado a la regla y el grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="24ea8-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="24ea8-142">Agregar una subred de toohello VNic</span><span class="sxs-lookup"><span data-stu-id="24ea8-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="24ea8-143">Tarjetas de red virtual (VNics) son importantes tal y como se puede reutilizar conectándolos toodifferent las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="24ea8-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="24ea8-144">Este enfoque conserva Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal.</span><span class="sxs-lookup"><span data-stu-id="24ea8-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="24ea8-145">Cree un VNic y asociarla a la subred de hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="24ea8-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="24ea8-146">Implementar Hola VM en la red virtual de Hola y NSG</span><span class="sxs-lookup"><span data-stu-id="24ea8-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="24ea8-147">Ahora tiene una red virtual y subred dentro de esa red virtual y un grupo de seguridad de red actúan de subred de hello tooprotect bloqueando todo el tráfico entrante excepto el puerto 22 de SSH.</span><span class="sxs-lookup"><span data-stu-id="24ea8-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="24ea8-148">Hola VM ahora pueden implementarse dentro de esta infraestructura de red existente.</span><span class="sxs-lookup"><span data-stu-id="24ea8-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="24ea8-149">Mediante Hola CLI de Azure y Hola `azure vm create` comando hello Linux VM está implementado toohello grupo de recursos de Azure, red virtual, subred y VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="24ea8-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="24ea8-150">Para obtener más información sobre el uso de hello CLI toodeploy una máquina virtual completa, consulte [crear un entorno completo de Linux mediante Hola CLI de Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="24ea8-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

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

<span data-ttu-id="24ea8-151">Mediante el uso de hello CLI marcas toocall recursos existentes, indicar hello toodeploy Azure VM dentro de la red existente Hola.</span><span class="sxs-lookup"><span data-stu-id="24ea8-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="24ea8-152">Una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="24ea8-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="24ea8-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24ea8-153">Next steps</span></span>

* [<span data-ttu-id="24ea8-154">Usar un toocreate de plantilla una implementación específica de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="24ea8-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="24ea8-155">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="24ea8-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="24ea8-156">Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="24ea8-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
