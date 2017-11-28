---
title: "aaaUse resolución con hello Azure CLI 2.0 de nombres DNS internos para la máquina virtual | Documentos de Microsoft"
description: "Cómo red virtual toocreate tarjetas de interfaz y usar DNS interno para la resolución de nombres de máquina virtual en Azure con hello 2.0 de CLI de Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="b4dd5-103">Creación de tarjetas de interfaz de red virtual y uso de DNS interno para la resolución de nombres de máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="b4dd5-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="b4dd5-104">Este artículo muestra cómo de nombres DNS internos estáticos del tooset para máquinas virtuales de Linux con virtual red tarjetas de interfaz (vNics) y los nombres de etiqueta DNS con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="b4dd5-105">También puede realizar estos pasos con hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b4dd5-106">Los nombres de DNS estáticos se utilizan para los servicios de infraestructura permanente como un servidor de compilación Jenkins, que se usa para este documento o un servidor de Git.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="b4dd5-107">Hola requisitos son:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-107">hello requirements are:</span></span>

* <span data-ttu-id="b4dd5-108">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="b4dd5-108">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="b4dd5-109">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-109">[SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="quick-commands"></a><span data-ttu-id="b4dd5-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="b4dd5-110">Quick commands</span></span>
<span data-ttu-id="b4dd5-111">Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="b4dd5-112">Obtener más información y el contexto de cada paso se encuentran en el resto de saludo del documento de hello, [a partir de aquí](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="b4dd5-113">tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b4dd5-114">Requisitos previos: grupo de recursos, red virtual y subred, grupo de seguridad de red con SSH entrante.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="b4dd5-115">Creación de una tarjeta de interfaz de red virtual con un nombre DNS interno estático</span><span class="sxs-lookup"><span data-stu-id="b4dd5-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="b4dd5-116">Crear Hola vNic con [crear nic de red az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b4dd5-117">Hola `--internal-dns-name` marca CLI es para la etiqueta de configuración Hola DNS, que proporciona Hola estático nombre DNS para la tarjeta de interfaz de red virtual (vNic) de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="b4dd5-118">Hello en el ejemplo siguiente se crea un vNic denominado `myNic`, se conecta toohello `myVnet` red virtual y crea un registro de nombre DNS interno denominado `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="b4dd5-119">Implementar una máquina virtual y conéctese Hola vNic</span><span class="sxs-lookup"><span data-stu-id="b4dd5-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="b4dd5-120">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b4dd5-121">Hola `--nics` marca conecta Hola vNic toohello VM durante Hola implementación tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="b4dd5-122">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con discos de Azure administrados y adjuntará Hola vNic denominado `myNic` de hello anterior paso:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b4dd5-123">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="b4dd5-123">Detailed walkthrough</span></span>

<span data-ttu-id="b4dd5-124">Una integración completa continua y la implementación continua (CiCd) una infraestructura en Azure requiere determinados servidores de toobe servidores estáticos o de larga duración.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="b4dd5-125">Se recomienda que los activos de Azure como Hola redes virtuales y grupos de seguridad de red son estáticos y larga duración recursos que rara vez se implementan.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="b4dd5-126">Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="b4dd5-127">Posteriormente, puede agregar un servidor de repositorio de Git o un servidor de automatización Jenkins entrega CiCd toothis red virtual para los entornos de desarrollo o de prueba.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="b4dd5-128">Los nombres de DNS internos solo pueden resolverse dentro de una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="b4dd5-129">Dado que los nombres DNS de hello son internos, no son toohello puede resolver fuera de internet, proporciona la infraestructura de toohello de seguridad adicional.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="b4dd5-130">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b4dd5-131">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `myNic` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="b4dd5-132">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="b4dd5-132">Create hello resource group</span></span>
<span data-ttu-id="b4dd5-133">Primero, cree el grupo de recursos de hello con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b4dd5-134">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="b4dd5-135">Crear red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="b4dd5-135">Create hello virtual network</span></span>

<span data-ttu-id="b4dd5-136">Hola siguiente paso es toobuild Hola a las máquinas virtuales en un toolaunch de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="b4dd5-137">red virtual de Hello contiene una subred para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="b4dd5-138">Para obtener más información sobre redes virtuales de Azure, consulte [crear una red virtual mediante el uso de hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="b4dd5-139">Crear red virtual de hello con [crear red virtual de red az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b4dd5-140">Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet` y subred denominada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="b4dd5-141">Crear grupo de seguridad de red de hello</span><span class="sxs-lookup"><span data-stu-id="b4dd5-141">Create hello Network Security Group</span></span>
<span data-ttu-id="b4dd5-142">Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="b4dd5-143">Para obtener más información acerca de los grupos de seguridad de red, consulte [cómo toocreate NSG en hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="b4dd5-144">Crear grupo de seguridad de red de hello con [crear az red nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="b4dd5-145">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="b4dd5-146">Agregar un tooallow de regla de entrada SSH</span><span class="sxs-lookup"><span data-stu-id="b4dd5-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="b4dd5-147">Agregar una regla de entrada para el grupo de seguridad de red de hello con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="b4dd5-148">Hello en el ejemplo siguiente se crea una regla denominada `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="b4dd5-149">Asociar subredes Hola Hola grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="b4dd5-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="b4dd5-150">subred de hello tooassociate con hello grupo de seguridad de red, usar [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="b4dd5-151">Hello en el ejemplo siguiente se asocia nombre de subred de hello `mySubnet` con hello grupo de seguridad de red denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="b4dd5-152">Crear la tarjeta de interfaz de red virtual de Hola y nombres DNS estáticos</span><span class="sxs-lookup"><span data-stu-id="b4dd5-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="b4dd5-153">Azure es muy flexible, pero toouse para nombres DNS para la resolución de nombre de máquina virtual, debe tarjetas de interfaz de red virtual de toocreate (vNics) que se incluye una etiqueta DNS.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="b4dd5-154">vNics son importantes como poder reutilizarlos conectándolas a máquinas virtuales de toodifferent durante el ciclo de vida de hello infraestructura.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="b4dd5-155">Este enfoque conserva vNic Hola como un recurso estático mientras hello las máquinas virtuales puede ser temporal.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="b4dd5-156">Mediante el uso de DNS etiquetado de hello vNic, estamos tooenable capaz de resolución de nombres sencillos de otras máquinas virtuales en hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="b4dd5-157">Uso de nombres que se resuelven permite otro servidor de automatización de las máquinas virtuales tooaccess Hola por nombre DNS de Hola `Jenkins` u Hola Git server como `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="b4dd5-158">Crear Hola vNic con [crear nic de red az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b4dd5-159">Hello en el ejemplo siguiente se crea un vNic denominado `myNic`, se conecta toohello `myVnet` red virtual denominada `myVnet`y crea un registro de nombre DNS interno denominado `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="b4dd5-160">Implementar Hola VM en la infraestructura de red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="b4dd5-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="b4dd5-161">Ahora tenemos una red virtual y subred, un grupo de seguridad de red que actúe como un firewall tooprotect nuestro subred bloqueando todo el tráfico entrante excepto el 22 de puerto para SSH y un vNic.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="b4dd5-162">Ahora se puede implementar la máquina virtual dentro de esta infraestructura de red existente.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="b4dd5-163">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b4dd5-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b4dd5-164">Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con discos de Azure administrados y adjuntará Hola vNic denominado `myNic` de hello anterior paso:</span><span class="sxs-lookup"><span data-stu-id="b4dd5-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="b4dd5-165">Mediante el uso de hello CLI marcas toocall recursos existentes, se ordena hello toodeploy Azure VM dentro de la red existente Hola.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="b4dd5-166">tooreiterate, una vez que se han implementado una red virtual y subred, puede dejarse como recursos estáticos o permanentes dentro de su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4dd5-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b4dd5-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4dd5-167">Next steps</span></span>
* [<span data-ttu-id="b4dd5-168">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="b4dd5-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b4dd5-169">Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b4dd5-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
