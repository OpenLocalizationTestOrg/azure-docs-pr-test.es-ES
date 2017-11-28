---
title: "aaaDeploy máquinas virtuales de Linux en la red existente con el portal de Azure | Documentos de Microsoft"
description: Implementar una VM de Linux en una red Virtual de Azure existente mediante el portal de Hola.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="41c8d-103">¿Cómo toodeploy una máquina virtual de Linux en una red Virtual de Azure existente con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="41c8d-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="41c8d-104">Este artículo muestra cómo toodeploy una máquina virtual (VM) en una red virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="41c8d-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="41c8d-105">Los recursos de Azure como redes virtuales y grupos de seguridad de red deben ser recursos estáticos y de larga duración que rara vez se implementen.</span><span class="sxs-lookup"><span data-stu-id="41c8d-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="41c8d-106">Una vez que se ha implementado una red virtual, se puede ser reutilizada por reimplementaciones constantes sin ninguna infraestructura de toohello afectará de forma negativa.</span><span class="sxs-lookup"><span data-stu-id="41c8d-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="41c8d-107">Pensar en una red virtual como tradicional modificador de red de hardware: no tendría tooconfigure hardware completamente nuevo cambiar con cada implementación.</span><span class="sxs-lookup"><span data-stu-id="41c8d-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="41c8d-108">Con una red virtual configurada correctamente, puede seguir el toodeploy nuevos servidores en esa red virtual una y otra vez con pocos, si lo hay, cambios necesarios durante la vigencia de Hola de hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="41c8d-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="41c8d-109">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="41c8d-109">Create hello resource group</span></span>

<span data-ttu-id="41c8d-110">En primer lugar, cree una tooorganize de grupo de recursos todo lo que cree en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="41c8d-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="41c8d-111">Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41c8d-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="41c8d-113">Crear red virtual de hello</span><span class="sxs-lookup"><span data-stu-id="41c8d-113">Create hello VNet</span></span>

<span data-ttu-id="41c8d-114">A continuación, compile un hello toolaunch de red virtual las máquinas virtuales en.</span><span class="sxs-lookup"><span data-stu-id="41c8d-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="41c8d-115">Hola red virtual contiene una subred y está asociado con el grupo de seguridad de red de Hola a esta subred en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="41c8d-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="41c8d-117">Agregar una subred de toohello VNic</span><span class="sxs-lookup"><span data-stu-id="41c8d-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="41c8d-118">Tarjetas de red virtual (VNics) son importantes que pueda conectarse toodifferent las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="41c8d-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="41c8d-119">Este enfoque conserva Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal.</span><span class="sxs-lookup"><span data-stu-id="41c8d-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="41c8d-120">Cree un VNic y asociarla a la subred de hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="41c8d-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="41c8d-122">Crear grupo de seguridad de red de Hola</span><span class="sxs-lookup"><span data-stu-id="41c8d-122">Create hello network security group</span></span>

<span data-ttu-id="41c8d-123">Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola.</span><span class="sxs-lookup"><span data-stu-id="41c8d-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="41c8d-124">Para más información sobre los grupos de seguridad de red, consulte [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="41c8d-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="41c8d-126">Agregar regla de permiso de SSH entrante</span><span class="sxs-lookup"><span data-stu-id="41c8d-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="41c8d-127">Hola VM necesita acceso de hello internet, por lo que una regla que permita el puerto de entrada 22 tráfico toobe pasa a través de la red de hello tooport 22 en Hola se crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41c8d-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="41c8d-129">Asociar NSG Hola subred Hola</span><span class="sxs-lookup"><span data-stu-id="41c8d-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="41c8d-130">Con hello red virtual y subred Hola creado, asociar el grupo de seguridad de red de hello subred Hola.</span><span class="sxs-lookup"><span data-stu-id="41c8d-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="41c8d-131">Los grupos de seguridad de red se pueden asociar con una subred entera o una VNic individual.</span><span class="sxs-lookup"><span data-stu-id="41c8d-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="41c8d-132">Con el firewall Hola filtran el tráfico en el nivel de subred de hello, todos los VNics y hello las máquinas virtuales dentro de la subred de hello están protegidos por grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="41c8d-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="41c8d-133">Hello otro enfoque es Hola grupo de seguridad de red que se está asociada a solo un VNic único y la protección de una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41c8d-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="41c8d-135">Implementar Hola VM en la red virtual de Hola y NSG</span><span class="sxs-lookup"><span data-stu-id="41c8d-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="41c8d-136">Uso de hello portal de Azure, Hola VM de Linux es implementado toohello grupo de recursos de Azure, red virtual, subred y VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="41c8d-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="41c8d-138">Mediante el uso de recursos existentes de hello toochoose portal, indique a hello toodeploy Azure VM dentro de la red existente Hola.</span><span class="sxs-lookup"><span data-stu-id="41c8d-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="41c8d-139">Una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="41c8d-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="41c8d-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41c8d-140">Next steps</span></span>

* [<span data-ttu-id="41c8d-141">Usar un toocreate de plantilla una implementación específica de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="41c8d-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="41c8d-142">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="41c8d-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="41c8d-143">Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="41c8d-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
