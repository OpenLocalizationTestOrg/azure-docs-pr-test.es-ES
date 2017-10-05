---
title: "Uso de DNS interno para la resolución de nombre de máquina virtual en Azure | Microsoft Docs"
description: "Uso de DNS interno para la resolución de nombre de máquina virtual en Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: bfba2cf38a0624e8480a32bf153f391d820da5a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="4ca55-103">Uso de DNS interno para la resolución de nombre de máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="4ca55-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="4ca55-104">Este artículo muestra cómo establecer nombres de DNS internos estáticos para máquinas virtuales Linux mediante tarjetas NIC virtuales (VNic) y los nombres de etiqueta DNS.</span><span class="sxs-lookup"><span data-stu-id="4ca55-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="4ca55-105">Los nombres de DNS estáticos se utilizan para los servicios de infraestructura permanente como un servidor de compilación Jenkins, que se usa para este documento o un servidor de Git.</span><span class="sxs-lookup"><span data-stu-id="4ca55-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="4ca55-106">Los requisitos son:</span><span class="sxs-lookup"><span data-stu-id="4ca55-106">The requirements are:</span></span>

* <span data-ttu-id="4ca55-107">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="4ca55-107">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="4ca55-108">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ca55-108">[SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="4ca55-109">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="4ca55-109">CLI versions to complete the task</span></span>
<span data-ttu-id="4ca55-110">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="4ca55-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="4ca55-111">[CLI de Azure 1.0](#quick-commands): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="4ca55-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="4ca55-112">[CLI de Azure 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="4ca55-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="4ca55-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="4ca55-113">Quick commands</span></span>

<span data-ttu-id="4ca55-114">Si necesita realizar rápidamente la tarea, en la siguiente sección se detallan los comandos necesarios.</span><span class="sxs-lookup"><span data-stu-id="4ca55-114">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="4ca55-115">Se puede encontrar información más detallada y contexto para cada paso en el resto del documento, [comenzando aquí](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="4ca55-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="4ca55-116">Requisitos previos: grupo de recursos, red virtual, NSG con SSH entrante, subred.</span><span class="sxs-lookup"><span data-stu-id="4ca55-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="4ca55-117">Creación de VNic con un nombre de DNS interno estático</span><span class="sxs-lookup"><span data-stu-id="4ca55-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="4ca55-118">La marca de la CLI de `-r` sirve para configurar la etiqueta de DNS, que proporciona el nombre de DNS estático de VNic.</span><span class="sxs-lookup"><span data-stu-id="4ca55-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-the-vm-into-the-vnet-nsg-and-connect-the-vnic"></a><span data-ttu-id="4ca55-119">Implementación de la máquina virtual en la red virtual y NSG, y conexión de VNic</span><span class="sxs-lookup"><span data-stu-id="4ca55-119">Deploy the VM into the VNet, NSG and, connect the VNic</span></span>

<span data-ttu-id="4ca55-120">`-N` se conecta VNic a la nueva máquina virtual durante la implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="4ca55-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="4ca55-121">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="4ca55-121">Detailed walkthrough</span></span>

<span data-ttu-id="4ca55-122">Una integración completa continua y una infraestructura de implementación continua (CiCd) en Azure requiere que determinados servidores sean servidores estáticos o de larga duración.</span><span class="sxs-lookup"><span data-stu-id="4ca55-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span>  <span data-ttu-id="4ca55-123">Se recomienda que los recursos de Azure como las redes virtuales (vNet) y los grupos de seguridad de red (NSG) sean estáticos y de larga duración que se implementan con poca frecuencia.</span><span class="sxs-lookup"><span data-stu-id="4ca55-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="4ca55-124">Una vez que se ha implementado una red virtual, se puede volver a utilizar con nuevas implementaciones sin efectos adversos para la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="4ca55-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="4ca55-125">La adición a esta red estática de un R Serverepositorio de Git y un servidor de automatización Jenkins proporciona CiCd a los entornos de desarrollo o prueba.</span><span class="sxs-lookup"><span data-stu-id="4ca55-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span></span>  

<span data-ttu-id="4ca55-126">Los nombres de DNS internos solo pueden resolverse dentro de una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ca55-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="4ca55-127">Dado que los nombres de DNS son internos, no pueden resolverse en Internet exterior, lo que proporciona una seguridad adicional a la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="4ca55-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="4ca55-128">_Reemplace los ejemplos por su propia nomenclatura._</span><span class="sxs-lookup"><span data-stu-id="4ca55-128">_Replace any examples with your own naming._</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="4ca55-129">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4ca55-129">Create the Resource group</span></span>

<span data-ttu-id="4ca55-130">Se precisa un grupo de recursos para organizar todo lo que se va a crear en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4ca55-130">A Resource Group is needed to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="4ca55-131">Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ca55-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="4ca55-132">Crear la red virtual</span><span class="sxs-lookup"><span data-stu-id="4ca55-132">Create the VNet</span></span>

<span data-ttu-id="4ca55-133">El primer paso es crear una red virtual en la que iniciar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4ca55-133">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="4ca55-134">La red virtual contiene una subred para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4ca55-134">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="4ca55-135">Para más información, consulte [Creación de una red virtual usando la CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ca55-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="4ca55-136">Crear el NSG</span><span class="sxs-lookup"><span data-stu-id="4ca55-136">Create the NSG</span></span>

<span data-ttu-id="4ca55-137">La subred se crea de forma subyacente a un grupo de seguridad de red existente, por lo que crearemos el grupo antes de crear la subred.</span><span class="sxs-lookup"><span data-stu-id="4ca55-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="4ca55-138">Los grupos de seguridad de red de Azure equivalen a un firewall en la capa de red.</span><span class="sxs-lookup"><span data-stu-id="4ca55-138">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="4ca55-139">Para más información sobre los grupos de seguridad de red de Azure, consulte [Creación de grupos de seguridad de red en la CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ca55-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="4ca55-140">Agregar regla de permiso de SSH entrante</span><span class="sxs-lookup"><span data-stu-id="4ca55-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="4ca55-141">La máquina virtual Linux debe tener acceso desde Internet por lo que es necesaria una regla que permita el tráfico entrante en el puerto 22 que pase a través de la red y vaya al puerto 22 de la máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="4ca55-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="4ca55-142">Agregar una subred a la red virtual</span><span class="sxs-lookup"><span data-stu-id="4ca55-142">Add a subnet to the VNet</span></span>

<span data-ttu-id="4ca55-143">Las máquinas virtuales dentro de la red virtual deben estar ubicadas en una subred.</span><span class="sxs-lookup"><span data-stu-id="4ca55-143">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="4ca55-144">Cada red virtual puede tener varias subredes.</span><span class="sxs-lookup"><span data-stu-id="4ca55-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="4ca55-145">Cree la subred y asóciela con el grupo de seguridad de red para le agregue un firewall.</span><span class="sxs-lookup"><span data-stu-id="4ca55-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="4ca55-146">Ahora, la subred ya se agregó dentro de la red virtual y se asoció con el grupo de seguridad de red y la regla de este.</span><span class="sxs-lookup"><span data-stu-id="4ca55-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="4ca55-147">Creación de nombres de DNS estáticos</span><span class="sxs-lookup"><span data-stu-id="4ca55-147">Creating static DNS names</span></span>

<span data-ttu-id="4ca55-148">Azure es muy flexible, pero para utilizar nombres de DNS para la resolución de nombres de máquinas virtuales, debe crearlos como tarjetas de red virtual (VNic) con el etiquetado de DNS.</span><span class="sxs-lookup"><span data-stu-id="4ca55-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="4ca55-149">Las VNic son importantes ya que se pueden reutilizar conectándolas a diferentes máquinas virtuales, lo que hace que las VNic sean un recurso estático mientras que las máquinas virtuales pueden ser temporales.</span><span class="sxs-lookup"><span data-stu-id="4ca55-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="4ca55-150">Mediante el uso del etiquetado de DNS, se pueden habilitar la resolución de nombre simple desde otras máquinas virtuales en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="4ca55-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span>  <span data-ttu-id="4ca55-151">El uso de nombres que se resuelven permite que otras máquinas virtuales tengan acceso al servidor de automatización mediante el nombre de DNS `Jenkins` o el servidor de Git como `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="4ca55-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  <span data-ttu-id="4ca55-152">Cree una VNic y asóciela a la subred que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="4ca55-152">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="4ca55-153">Implemente la máquina virtual en la red virtual y el grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="4ca55-153">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="4ca55-154">Ahora tenemos una red virtual, una subred dentro de esa red virtual y un grupo de seguridad de red que actúa como un firewall para proteger nuestra subred bloqueando todo el tráfico entrante excepto el del puerto 22 para SSH.</span><span class="sxs-lookup"><span data-stu-id="4ca55-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="4ca55-155">Ahora se puede implementar la máquina virtual dentro de esta infraestructura de red existente.</span><span class="sxs-lookup"><span data-stu-id="4ca55-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="4ca55-156">Mediante la CLI de Azure y el comando `azure vm create`, se implementa la máquina virtual Linux en el grupo de recursos de Azure, la red virtual, la subred y la VNic ya existentes.</span><span class="sxs-lookup"><span data-stu-id="4ca55-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="4ca55-157">Para más información sobre el uso de la CLI para implementar una máquina virtual completa, consulte [Creación de un entorno de Linux completo mediante la CLI de Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ca55-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="4ca55-158">Mediante el uso de los marcadores CLI para llamar a los recursos existentes, se indica a Azure que implemente la máquina virtual dentro de la red existente.</span><span class="sxs-lookup"><span data-stu-id="4ca55-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="4ca55-159">Permítanos insistir en que una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ca55-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4ca55-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ca55-160">Next steps</span></span>
* [<span data-ttu-id="4ca55-161">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="4ca55-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4ca55-162">Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4ca55-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
