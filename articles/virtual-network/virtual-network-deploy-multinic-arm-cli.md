---
title: "aaaCreate una máquina virtual con varias NIC - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con varias NIC con Hola 2.0 de CLI de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="93866-103">Crear una máquina virtual con varias NIC con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="93866-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="93866-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="93866-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="93866-105">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="93866-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="93866-106"><a name="create"></a>Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="93866-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="93866-107">Puede completar esta tarea mediante Hola CLI de Azure 2.0 (en este artículo) o hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="93866-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="93866-108">Hola valores en "" para recursos de creación de variables de hello en los pasos de Hola que sigan con la configuración del escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="93866-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="93866-109">Cambiar los valores de hello, según corresponda para su entorno.</span><span class="sxs-lookup"><span data-stu-id="93866-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="93866-110">Instalar hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) si no se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="93866-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="93866-111">Crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux siguiendo los pasos de Hola Hola [crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93866-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="93866-112">Desde un shell de comandos, inicio de sesión con el comando hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="93866-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="93866-113">Crear Hola VM mediante la ejecución de script de Hola que sigue en un equipo Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="93866-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="93866-114">script de Hola crea un grupo de recursos, una red virtual (VNet) con dos subredes, dos NIC y una máquina virtual con hello dos NIC conectado tooit.</span><span class="sxs-lookup"><span data-stu-id="93866-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="93866-115">Uno de hello NIC conectado tooone subred y se asigna una dirección IP estática pública y privada.</span><span class="sxs-lookup"><span data-stu-id="93866-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="93866-116">Hello otro NIC está conectado toohello otra subred y se le asigna una dirección IP privada estática y ninguna dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="93866-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="93866-117">Hola NIC, la dirección IP pública, la red virtual y recursos de máquina virtual deben existir en hello igual ubicación y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="93866-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="93866-118">Aunque recursos hello no tienen todas tooexist Hola mismo grupo de recursos, en la siguiente secuencia de comandos lo hacen de Hola.</span><span class="sxs-lookup"><span data-stu-id="93866-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

<span data-ttu-id="93866-119">Además toocreating una máquina virtual con dos NIC, crea el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="93866-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="93866-120">Una prima única administra disco de forma predeterminada, pero tiene otras opciones para el tipo de disco de Hola que se puede crear.</span><span class="sxs-lookup"><span data-stu-id="93866-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="93866-121">Hola de lectura [crear una VM de Linux con hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="93866-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="93866-122">Una red virtual con dos subredes y una única dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="93866-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="93866-123">Como alternativa, puede usar una red virtual, una subred, una NIC o una dirección IP pública *existentes*.</span><span class="sxs-lookup"><span data-stu-id="93866-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="93866-124">toolearn cómo toouse existentes recursos de red en lugar de crear recursos adicionales, escriba `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="93866-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="93866-125"><a name = "validate"></a>Validación de la creación de máquinas virtuales y NIC</span><span class="sxs-lookup"><span data-stu-id="93866-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="93866-126">Escriba el comando hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee una lista de recursos de hello creado por el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="93866-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="93866-127">Debería haber seis recursos Hola devolvía los resultados: dos NIC, un disco, una dirección IP pública, una red virtual y una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="93866-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="93866-128">Escriba el comando hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="93866-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="93866-129">Hola devolvía los resultados, anote el valor de Hola de **IpAddress** y ese valor Hola de **PublicIpAllocationMethod** es *estático*.</span><span class="sxs-lookup"><span data-stu-id="93866-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="93866-130">Antes de ejecutar el siguiente comando de hello, quitar hello <>, reemplace *nombre de usuario* con nombre de Hola que usó para hello **nombre de usuario** variable en el script de Hola y reemplazar *ipAddress* con hello **ipAddress** del paso anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="93866-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="93866-131">Siguiente ejecución Hola comando tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="93866-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="93866-132">Una vez conectado toohello máquina virtual, ejecute hello `sudo ifconfig` comando toosee *eth0* y *eth1* interfaces.</span><span class="sxs-lookup"><span data-stu-id="93866-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="93866-133">Cada NIC se ha asignado Hola privadas direcciones IP estáticas especificadas en el script de Hola por servidores DHCP de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="93866-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="93866-134">Hello direcciones IP y MAC asignadas toohello NIC no cambian hasta que se eliminó la MV de Hola.</span><span class="sxs-lookup"><span data-stu-id="93866-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="93866-135">Se recomienda no cambiar una dirección IP dentro de un sistema operativo, tal y como puede deshabilitar el equipo de toohello de conectividad.</span><span class="sxs-lookup"><span data-stu-id="93866-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="93866-136">Las direcciones IP públicas no aparecen en el sistema operativo de hello, tal como están tooand traducido de dirección de red de dirección IP privada de Hola por hello infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="93866-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="93866-137"><a name= "clean-up"></a>Quitar Hola VM y recursos asociados</span><span class="sxs-lookup"><span data-stu-id="93866-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="93866-138">Se recomienda que elimine recursos de hello creados en este ejercicio, si no usa en producción.</span><span class="sxs-lookup"><span data-stu-id="93866-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="93866-139">Los recursos de máquina virtual, dirección IP pública y disco incurren en gastos, cuando se están aprovisionando.</span><span class="sxs-lookup"><span data-stu-id="93866-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="93866-140">recursos de hello tooremove creados durante este ejercicio, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="93866-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="93866-141">recursos de hello tooview en grupo de recursos de hello, ejecute hello `az resource list --resource-group Multi-NIC-VM` comando.</span><span class="sxs-lookup"><span data-stu-id="93866-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="93866-142">Confirme que no hay recursos en grupo de recursos de hello, que no sea de recursos de hello creados por script de Hola en este artículo.</span><span class="sxs-lookup"><span data-stu-id="93866-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="93866-143">toodelete todos los recursos creados en este ejercicio, ejecute hello `az group delete --name Multi-NIC-VM` comando.</span><span class="sxs-lookup"><span data-stu-id="93866-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="93866-144">comando de Hello elimina el grupo de recursos de Hola y contiene todos los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="93866-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93866-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="93866-145">Next steps</span></span>

<span data-ttu-id="93866-146">Tráfico de red puede fluir tooand de hello que crea la VM en este artículo.</span><span class="sxs-lookup"><span data-stu-id="93866-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="93866-147">Puede definir reglas entrantes y salientes en un NSG limitan el tráfico de Hola que puede fluir tooand desde cada interfaz de red, cada subred o ambos.</span><span class="sxs-lookup"><span data-stu-id="93866-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="93866-148">más información acerca de los NSG, leer hello toolearn [información general NSG](virtual-networks-nsg.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="93866-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
