---
title: "aaaUsing resolución en Azure de nombres DNS internos para la máquina virtual | Documentos de Microsoft"
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
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="845b2-103">Uso de DNS interno para la resolución de nombre de máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="845b2-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="845b2-104">Este artículo muestra cómo tooset nombres de DNS interno estático para máquinas virtuales Linux mediante tarjetas NIC Virtual (VNic) y los nombres de etiqueta DNS.</span><span class="sxs-lookup"><span data-stu-id="845b2-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="845b2-105">Los nombres de DNS estáticos se utilizan para los servicios de infraestructura permanente como un servidor de compilación Jenkins, que se usa para este documento o un servidor de Git.</span><span class="sxs-lookup"><span data-stu-id="845b2-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="845b2-106">Hola requisitos son:</span><span class="sxs-lookup"><span data-stu-id="845b2-106">hello requirements are:</span></span>

* <span data-ttu-id="845b2-107">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="845b2-107">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="845b2-108">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="845b2-108">[SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="845b2-109">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="845b2-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="845b2-110">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="845b2-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="845b2-111">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="845b2-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="845b2-112">[Azure 2.0 CLI](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="845b2-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="845b2-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="845b2-113">Quick commands</span></span>

<span data-ttu-id="845b2-114">Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios.</span><span class="sxs-lookup"><span data-stu-id="845b2-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="845b2-115">Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="845b2-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="845b2-116">Requisitos previos: grupo de recursos, red virtual, NSG con SSH entrante, subred.</span><span class="sxs-lookup"><span data-stu-id="845b2-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="845b2-117">Creación de VNic con un nombre de DNS interno estático</span><span class="sxs-lookup"><span data-stu-id="845b2-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="845b2-118">Hola `-r` cli marca indica que etiqueta de configuración Hola DNS, que proporciona Hola nombre DNS estático Hola VNic.</span><span class="sxs-lookup"><span data-stu-id="845b2-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="845b2-119">Implementar Hola VM en Hola de red virtual, NSG y, cuando conectan Hola VNic</span><span class="sxs-lookup"><span data-stu-id="845b2-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="845b2-120">Hola `-N` conecta Hola VNic toohello nueva máquina virtual durante Hola implementación tooAzure.</span><span class="sxs-lookup"><span data-stu-id="845b2-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="845b2-121">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="845b2-121">Detailed walkthrough</span></span>

<span data-ttu-id="845b2-122">Una integración completa continua y la implementación continua (CiCd) una infraestructura en Azure requiere determinados servidores de toobe servidores estáticos o de larga duración.</span><span class="sxs-lookup"><span data-stu-id="845b2-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="845b2-123">Se recomienda que los activos de Azure como hello las redes virtuales (redes virtuales) y grupos de seguridad de red (NSG), debe ser estáticos y larga duración recursos que rara vez se implementan.</span><span class="sxs-lookup"><span data-stu-id="845b2-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="845b2-124">Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa.</span><span class="sxs-lookup"><span data-stu-id="845b2-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="845b2-125">Agregar red estática toothis un Git servidor de repositorio y un servidor de automatización de Jenkins entrega CiCd tooyour entornos de prueba o desarrollo.</span><span class="sxs-lookup"><span data-stu-id="845b2-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="845b2-126">Los nombres de DNS internos solo pueden resolverse dentro de una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="845b2-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="845b2-127">Dado que los nombres DNS de hello son internos, no son toohello puede resolver fuera de internet, proporciona la infraestructura de toohello de seguridad adicional.</span><span class="sxs-lookup"><span data-stu-id="845b2-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="845b2-128">_Reemplace los ejemplos por su propia nomenclatura._</span><span class="sxs-lookup"><span data-stu-id="845b2-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="845b2-129">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="845b2-129">Create hello Resource group</span></span>

<span data-ttu-id="845b2-130">Un grupo de recursos es necesario tooorganize todo el contenido se crea en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="845b2-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="845b2-131">Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="845b2-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="845b2-132">Crear red virtual de hello</span><span class="sxs-lookup"><span data-stu-id="845b2-132">Create hello VNet</span></span>

<span data-ttu-id="845b2-133">Hola primer paso es toobuild Hola a las máquinas virtuales en un toolaunch de red virtual.</span><span class="sxs-lookup"><span data-stu-id="845b2-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="845b2-134">Hola red virtual contiene una subred para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="845b2-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="845b2-135">Para obtener más información sobre redes virtuales de Azure, consulte [crear una red virtual mediante el uso de hello CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="845b2-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="845b2-136">Crear hello NSG</span><span class="sxs-lookup"><span data-stu-id="845b2-136">Create hello NSG</span></span>

<span data-ttu-id="845b2-137">Hola subred se basa detrás de un grupo de seguridad de red existente de modo que creamos hello NSG antes de hello subred.</span><span class="sxs-lookup"><span data-stu-id="845b2-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="845b2-138">Los NSG Azure son firewall tooa equivalente en la capa de red Hola.</span><span class="sxs-lookup"><span data-stu-id="845b2-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="845b2-139">Para obtener más información sobre los NSG de Azure, vea [cómo toocreate NSG en Hola CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="845b2-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="845b2-140">Agregar regla de permiso de SSH entrante</span><span class="sxs-lookup"><span data-stu-id="845b2-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="845b2-141">Hola Linux VM necesita acceso de Hola se necesita internet para que una regla que permita el puerto de entrada tráfico 22 toobe pasa a través de la red de hello tooport 22 en hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="845b2-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="845b2-142">Agregar una red virtual de toohello de subred</span><span class="sxs-lookup"><span data-stu-id="845b2-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="845b2-143">Las máquinas virtuales de hello red virtual deben estar ubicadas en una subred.</span><span class="sxs-lookup"><span data-stu-id="845b2-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="845b2-144">Cada red virtual puede tener varias subredes.</span><span class="sxs-lookup"><span data-stu-id="845b2-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="845b2-145">Crear una subred de Hola y asocie subred Hola Hola NSG tooadd una subred de toohello de firewall.</span><span class="sxs-lookup"><span data-stu-id="845b2-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="845b2-146">Hola subred ahora se agregaron dentro de la red virtual de Hola y asociada con hello NSG y regla NSG Hola.</span><span class="sxs-lookup"><span data-stu-id="845b2-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="845b2-147">Creación de nombres de DNS estáticos</span><span class="sxs-lookup"><span data-stu-id="845b2-147">Creating static DNS names</span></span>

<span data-ttu-id="845b2-148">Azure es muy flexible, pero toouse para nombres DNS para la resolución de nombres de las máquinas virtuales, debe toocreate como Virtual tarjetas (VNics) con DNS etiquetado de red.</span><span class="sxs-lookup"><span data-stu-id="845b2-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="845b2-149">VNics son importantes como poder reutilizarlos conectándolos toodifferent máquinas virtuales, lo que mantiene Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal.</span><span class="sxs-lookup"><span data-stu-id="845b2-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="845b2-150">Mediante el uso de DNS etiquetado en hello VNic, estamos tooenable capaz de resolución de nombres sencillos de otras máquinas virtuales en hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="845b2-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="845b2-151">Uso de nombres que se resuelven permite otro servidor de automatización de las máquinas virtuales tooaccess Hola por nombre DNS de Hola `Jenkins` u Hola Git server como `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="845b2-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="845b2-152">Crear un VNic y asócielo con hello que subred creada en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="845b2-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="845b2-153">Implementar Hola VM en la red virtual de Hola y NSG</span><span class="sxs-lookup"><span data-stu-id="845b2-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="845b2-154">Ahora tenemos una red virtual, una subred dentro de esa red virtual y un NSG actúa como un firewall tooprotect nuestro subred bloqueando todo el tráfico entrante excepto el puerto 22 de SSH.</span><span class="sxs-lookup"><span data-stu-id="845b2-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="845b2-155">Hola VM ahora pueden implementarse dentro de esta infraestructura de red existente.</span><span class="sxs-lookup"><span data-stu-id="845b2-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="845b2-156">Mediante Hola CLI de Azure y Hola `azure vm create` comando hello Linux VM está implementado toohello grupo de recursos de Azure, red virtual, subred y VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="845b2-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="845b2-157">Para obtener más información sobre el uso de hello CLI toodeploy una máquina virtual completa, consulte [crear un entorno completo de Linux mediante Hola CLI de Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="845b2-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

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

<span data-ttu-id="845b2-158">Mediante el uso de hello CLI marcas toocall recursos existentes, se ordena hello toodeploy Azure VM dentro de la red existente Hola.</span><span class="sxs-lookup"><span data-stu-id="845b2-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="845b2-159">tooreiterate, una vez que se han implementado una red virtual y subred, puede dejarse como recursos estáticos o permanentes dentro de su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="845b2-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="845b2-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="845b2-160">Next steps</span></span>
* [<span data-ttu-id="845b2-161">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="845b2-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="845b2-162">Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="845b2-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
