---
title: "aaaCreate una máquina virtual con una dirección pública estática de IP - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con una estática pública IP dirección utilizando hello Azure interfaz de línea de comandos (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="7f220-103">Crear una máquina virtual con una dirección IP pública estática con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7f220-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f220-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7f220-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="7f220-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f220-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="7f220-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7f220-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="7f220-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7f220-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="7f220-108">Plantilla</span><span class="sxs-lookup"><span data-stu-id="7f220-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="7f220-109">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="7f220-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="7f220-110">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f220-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="7f220-111">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f220-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="7f220-112"><a name = "create"></a>Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="7f220-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="7f220-113">Puede completar esta tarea mediante Hola CLI de Azure 2.0 (en este artículo) o hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7f220-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="7f220-114">Hola valores en "" para recursos de creación de variables de hello en los pasos de Hola que sigan con la configuración del escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f220-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="7f220-115">Cambiar los valores de hello, según corresponda para su entorno.</span><span class="sxs-lookup"><span data-stu-id="7f220-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="7f220-116">Instalar hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) si no se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="7f220-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="7f220-117">Crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux siguiendo los pasos de Hola Hola [crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f220-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="7f220-118">Desde un shell de comandos, inicio de sesión con el comando hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="7f220-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="7f220-119">Crear Hola VM mediante la ejecución de script de Hola que sigue en un equipo Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="7f220-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="7f220-120">Hola Azure dirección IP pública, la red virtual, la interfaz de red y recursos de máquina virtual deben existir en hello igual ubicación.</span><span class="sxs-lookup"><span data-stu-id="7f220-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="7f220-121">Aunque recursos hello no tienen todas tooexist Hola mismo grupo de recursos, en la siguiente secuencia de comandos lo hacen de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f220-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

<span data-ttu-id="7f220-122">Además toocreating una máquina virtual, el script de Hola crea:</span><span class="sxs-lookup"><span data-stu-id="7f220-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="7f220-123">Una prima única administra disco de forma predeterminada, pero tiene otras opciones para el tipo de disco de Hola que se puede crear.</span><span class="sxs-lookup"><span data-stu-id="7f220-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="7f220-124">Hola de lectura [crear una VM de Linux con hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7f220-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="7f220-125">Una red virtual, una subred, una NIC y recursos de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="7f220-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="7f220-126">Como alternativa, puede usar una red virtual, una subred, una NIC o una dirección IP pública *existentes*.</span><span class="sxs-lookup"><span data-stu-id="7f220-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="7f220-127">toolearn cómo toouse existentes recursos de red en lugar de crear recursos adicionales, escriba `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="7f220-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="7f220-128"><a name = "validate"></a>Validación de la creación de máquinas virtuales y de dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="7f220-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="7f220-129">Escriba el comando hello `az resource list --resouce-group IaaSStory --output table` toosee una lista de recursos de hello creado por el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f220-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="7f220-130">Debería haber cinco recursos Hola devolvía los resultados: interfaz, disco, dirección IP pública, red virtual y una máquina virtual de la red.</span><span class="sxs-lookup"><span data-stu-id="7f220-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="7f220-131">Escriba el comando hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="7f220-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="7f220-132">Hola devolvía los resultados, anote el valor de Hola de **IpAddress** y ese valor Hola de **PublicIpAllocationMethod** es *estático*.</span><span class="sxs-lookup"><span data-stu-id="7f220-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="7f220-133">Antes de ejecutar el siguiente comando de hello, quitar hello <>, reemplace *nombre de usuario* con nombre de Hola que usó para hello **nombre de usuario** variable en el script de Hola y reemplazar *ipAddress* con hello **ipAddress** del paso anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="7f220-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="7f220-134">Siguiente ejecución Hola comando tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="7f220-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="7f220-135"><a name= "clean-up"></a>Quitar Hola VM y recursos asociados</span><span class="sxs-lookup"><span data-stu-id="7f220-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="7f220-136">Se recomienda que elimine recursos de hello creados en este ejercicio, si no usa en producción.</span><span class="sxs-lookup"><span data-stu-id="7f220-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="7f220-137">Los recursos de máquina virtual, dirección IP pública y disco incurren en gastos, cuando se están aprovisionando.</span><span class="sxs-lookup"><span data-stu-id="7f220-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="7f220-138">recursos de hello tooremove creados durante este ejercicio, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="7f220-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="7f220-139">recursos de hello tooview en grupo de recursos de hello, ejecute hello `az resource list --resource-group IaaSStory` comando.</span><span class="sxs-lookup"><span data-stu-id="7f220-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="7f220-140">Confirme que no hay recursos en grupo de recursos de hello, que no sea de recursos de hello creados por script de Hola en este artículo.</span><span class="sxs-lookup"><span data-stu-id="7f220-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="7f220-141">toodelete todos los recursos creados en este ejercicio, ejecute hello `az group delete -n IaaSStory` comando.</span><span class="sxs-lookup"><span data-stu-id="7f220-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="7f220-142">comando de Hello elimina el grupo de recursos de Hola y contiene todos los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f220-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f220-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f220-143">Next steps</span></span>

<span data-ttu-id="7f220-144">Tráfico de red puede fluir tooand de hello que crea la VM en este artículo.</span><span class="sxs-lookup"><span data-stu-id="7f220-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="7f220-145">Puede definir reglas entrantes y salientes en un NSG limitan el tráfico de Hola que puede fluir tooand de interfaz de red de hello, subred hello o ambos.</span><span class="sxs-lookup"><span data-stu-id="7f220-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="7f220-146">más información acerca de los NSG, leer hello toolearn [información general NSG](virtual-networks-nsg.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="7f220-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
