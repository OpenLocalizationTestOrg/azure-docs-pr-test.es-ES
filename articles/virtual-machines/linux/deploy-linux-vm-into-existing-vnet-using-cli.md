---
title: "aaaDeploy máquinas virtuales de Linux en la red existente con 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una máquina virtual de Linux en una red Virtual existente mediante Hola 2.0 de CLI de Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="1fd58-103">¿Cómo toodeploy una máquina virtual de Linux en una red Virtual de Azure existente con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1fd58-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="1fd58-104">Este artículo muestra cómo toouse Hola toodeploy 2.0 de CLI de Azure a una máquina virtual (VM) en una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="1fd58-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="1fd58-105">Hola requisitos son:</span><span class="sxs-lookup"><span data-stu-id="1fd58-105">hello requirements are:</span></span>

- <span data-ttu-id="1fd58-106">[una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="1fd58-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="1fd58-107">[archivos de clave SSH pública y privada](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="1fd58-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

<span data-ttu-id="1fd58-108">También puede realizar estos pasos con hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1fd58-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="1fd58-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="1fd58-109">Quick Commands</span></span>
<span data-ttu-id="1fd58-110">Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios.</span><span class="sxs-lookup"><span data-stu-id="1fd58-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="1fd58-111">Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="1fd58-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="1fd58-112">toocreate este entorno personalizado, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1fd58-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1fd58-113">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="1fd58-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1fd58-114">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1fd58-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="1fd58-115">**Requisitos previos:** grupo de recursos de Azure, red virtual y subred, grupo de seguridad de red con SSH entrante y una tarjeta de interfaz de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1fd58-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="1fd58-116">Implementar Hola VM en la infraestructura de red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1fd58-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="1fd58-117">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="1fd58-117">Detailed walkthrough</span></span>

<span data-ttu-id="1fd58-118">Los recursos de Azure, como las redes virtuales y los grupos de seguridad de red, deben ser recursos estáticos y de larga duración que se implementen con poca frecuencia.</span><span class="sxs-lookup"><span data-stu-id="1fd58-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="1fd58-119">Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa.</span><span class="sxs-lookup"><span data-stu-id="1fd58-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="1fd58-120">Piense en una red virtual como un conmutador de red tradicionales de hardware: no tendría tooconfigure hardware completamente nuevo cambiar con cada implementación.</span><span class="sxs-lookup"><span data-stu-id="1fd58-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="1fd58-121">Con una red virtual configurada correctamente, puede continuar toodeploy nuevas máquinas virtuales en la red virtual una y otra vez con pocas, si lo hay, cambios necesario durante la vigencia de Hola de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd58-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="1fd58-122">toocreate este entorno personalizado, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1fd58-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1fd58-123">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="1fd58-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1fd58-124">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1fd58-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="1fd58-125">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="1fd58-125">Create hello resource group</span></span>

<span data-ttu-id="1fd58-126">En primer lugar, cree una tooorganize de grupo de recursos de Azure todo lo que cree en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fd58-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="1fd58-127">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fd58-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1fd58-128">Crear grupo de recursos de hello con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1fd58-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1fd58-129">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="1fd58-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="1fd58-130">Crear red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1fd58-130">Create hello virtual network</span></span>

<span data-ttu-id="1fd58-131">Permite generar un hello toolaunch de red virtual de Azure VM en.</span><span class="sxs-lookup"><span data-stu-id="1fd58-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="1fd58-132">Para obtener más información sobre redes virtuales, vea [crear una red virtual mediante el uso de hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1fd58-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="1fd58-133">Crear red virtual de hello con [crear red virtual de red az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="1fd58-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="1fd58-134">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* y subred denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="1fd58-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="1fd58-135">Crear grupo de seguridad de red de Hola</span><span class="sxs-lookup"><span data-stu-id="1fd58-135">Create hello network security group</span></span>

<span data-ttu-id="1fd58-136">Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd58-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="1fd58-137">Para obtener más información sobre los grupos de seguridad de red, consulte [cómo grupos de seguridad de red de toocreate en hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1fd58-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="1fd58-138">Crear grupo de seguridad de red de hello con [crear az red nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="1fd58-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="1fd58-139">Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1fd58-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="1fd58-140">Agregar regla de permiso de SSH entrante</span><span class="sxs-lookup"><span data-stu-id="1fd58-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="1fd58-141">Hola VM necesita acceso de hello internet, por lo que una regla que permita el puerto de entrada 22 tráfico toobe pasa a través de la red de hello tooport 22 en hello VM es necesario.</span><span class="sxs-lookup"><span data-stu-id="1fd58-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="1fd58-142">Agregar una regla de entrada para el grupo de seguridad de red de hello con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="1fd58-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="1fd58-143">Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="1fd58-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="1fd58-144">Asociar el grupo de seguridad de red de hello subred toohello</span><span class="sxs-lookup"><span data-stu-id="1fd58-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="1fd58-145">reglas del grupo de seguridad de red de Hello pueden ser aplicada tooa subred o una interfaz de red virtual específica.</span><span class="sxs-lookup"><span data-stu-id="1fd58-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="1fd58-146">Permite adjuntar Hola seguridad grupo tooour subred.</span><span class="sxs-lookup"><span data-stu-id="1fd58-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="1fd58-147">Asociar el grupo de seguridad de red de subred toohello con [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="1fd58-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="1fd58-148">Agregar una subred de toohello de tarjeta de interfaz de red virtual</span><span class="sxs-lookup"><span data-stu-id="1fd58-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="1fd58-149">Tarjetas de interfaz de red virtual (VNics) son importantes tal y como se puede reutilizar conectándolos toodifferent las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1fd58-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="1fd58-150">Volver a utilizar este permite tookeep Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal.</span><span class="sxs-lookup"><span data-stu-id="1fd58-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="1fd58-151">Crear un VNic y asociarla a la subred de hello con [crear nic de red az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="1fd58-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="1fd58-152">Hello en el ejemplo siguiente se crea un VNic denominado *myNic*:</span><span class="sxs-lookup"><span data-stu-id="1fd58-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="1fd58-153">Implementar Hola VM en la infraestructura de red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1fd58-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="1fd58-154">Ahora tiene una red virtual y subred y una subred de hello red tooprotect de grupo de seguridad bloqueando todo el tráfico entrante excepto el puerto 22 de SSH.</span><span class="sxs-lookup"><span data-stu-id="1fd58-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="1fd58-155">Hola VM ahora pueden implementarse dentro de esta infraestructura de red existente.</span><span class="sxs-lookup"><span data-stu-id="1fd58-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="1fd58-156">Creee la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1fd58-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1fd58-157">Para obtener más información sobre Hola marcas toouse con hello Azure CLI 2.0 toodeploy una máquina virtual completa, consulte [crear un entorno completo de Linux mediante el uso de hello Azure CLI](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="1fd58-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="1fd58-158">Hola de ejemplo siguiente crea una máquina virtual mediante discos de Azure administrados.</span><span class="sxs-lookup"><span data-stu-id="1fd58-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="1fd58-159">Estos discos se controlan mediante la plataforma Windows Azure hello y no requieren ningún toostore los preparativos o ubicación ellos.</span><span class="sxs-lookup"><span data-stu-id="1fd58-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="1fd58-160">Para más información acerca de los discos administrados, consulte [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md) (Introducción a los discos administrados de Azure).</span><span class="sxs-lookup"><span data-stu-id="1fd58-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="1fd58-161">Si desea que los discos toouse no administrado, vea la nota adicional de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="1fd58-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="1fd58-162">Si usa Azure Managed Disks, omita este paso.</span><span class="sxs-lookup"><span data-stu-id="1fd58-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="1fd58-163">Si desea que los discos toouse no administrado, deberá hello tooadd siguientes parámetros adicionales toohello continuar comando toocreate no administrada de discos en la cuenta de almacenamiento de hello denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="1fd58-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="1fd58-164">Mediante el uso de hello CLI marcas toocall recursos existentes, indicar hello toodeploy Azure VM dentro de la red existente Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd58-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="1fd58-165">Una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd58-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="1fd58-166">En este ejemplo, no cree y asignar una toohello de dirección IP pública VNic, por lo que esta máquina virtual no es accesible públicamente sobre Hola Internet.</span><span class="sxs-lookup"><span data-stu-id="1fd58-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="1fd58-167">Para obtener más información, consulte [crear una máquina virtual con una dirección IP pública estática con hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1fd58-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fd58-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1fd58-168">Next steps</span></span>
<span data-ttu-id="1fd58-169">Para obtener más información acerca de las formas toocreate virtual máquinas en Azure, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1fd58-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="1fd58-170">Usar un toocreate de plantilla una implementación específica de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1fd58-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="1fd58-171">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="1fd58-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="1fd58-172">Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1fd58-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
