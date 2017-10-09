---
title: aaaVM con varias direcciones IP con hello 2.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooassign varias direcciones IP tooa máquina virtual usando Hola 2.0 de CLI de Azure | Administrador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="63592-103">Asignar varias direcciones IP de máquinas de toovirtual mediante Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="63592-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="63592-104">Este artículo explica cómo toocreate una máquina virtual (VM) a través de modelo de implementación de Azure Resource Manager de hello mediante Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="63592-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="63592-105">No se puede asignar tooresources que se creó mediante el modelo de implementación clásica de Hola a varias direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="63592-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="63592-106">más información acerca de los modelos de implementación de Azure, lea hello toolearn [comprender los modelos de implementación](../resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="63592-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="63592-107"><a name = "create"></a>Creación de una máquina virtual con varias direcciones IP</span><span class="sxs-lookup"><span data-stu-id="63592-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="63592-108">Puede completar esta tarea mediante Hola CLI de Azure 2.0 (en este artículo) o hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="63592-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="63592-109">Cambiar los valores de hello, según corresponda para su entorno.</span><span class="sxs-lookup"><span data-stu-id="63592-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="63592-110">pasos de Hola que siguen explican cómo toocreate aborda un máquina virtual con varias IP de ejemplo, tal y como se describe en el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="63592-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="63592-111">Cambie los valores de variable entre "" y los tipos de direcciones IP según sea necesario para la implementación.</span><span class="sxs-lookup"><span data-stu-id="63592-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="63592-112">Instalar hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) si no se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="63592-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="63592-113">Crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux siguiendo los pasos de Hola Hola [crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63592-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="63592-114">Desde un shell de comandos, inicio de sesión con el comando hello `az login` y seleccione la suscripción de Hola que use.</span><span class="sxs-lookup"><span data-stu-id="63592-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="63592-115">Crear Hola VM mediante la ejecución de script de Hola que sigue en un equipo Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="63592-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="63592-116">script de Hola crea un grupo de recursos, una red virtual (VNet), una NIC con tres configuraciones de IP y una máquina virtual con hello dos NIC conectadas tooit.</span><span class="sxs-lookup"><span data-stu-id="63592-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="63592-117">Hola NIC, la dirección IP pública, la red virtual y recursos de máquina virtual deben existir en hello igual ubicación y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="63592-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="63592-118">Aunque recursos hello no tienen todas tooexist Hola mismo grupo de recursos, en la siguiente secuencia de comandos lo hacen de Hola.</span><span class="sxs-lookup"><span data-stu-id="63592-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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
```

<span data-ttu-id="63592-119">Además toocreating una máquina virtual con una NIC con 3: configuraciones IP, el script de Hola crea:</span><span class="sxs-lookup"><span data-stu-id="63592-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="63592-120">Una prima única administra disco de forma predeterminada, pero tiene otras opciones para el tipo de disco de Hola que se puede crear.</span><span class="sxs-lookup"><span data-stu-id="63592-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="63592-121">Hola de lectura [crear una VM de Linux con hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="63592-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="63592-122">Una red virtual con una subred y dos direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="63592-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="63592-123">Como alternativa, puede usar una red virtual, una subred, una NIC o una dirección IP pública *existentes*.</span><span class="sxs-lookup"><span data-stu-id="63592-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="63592-124">toolearn cómo toouse existentes recursos de red en lugar de crear recursos adicionales, escriba `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="63592-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="63592-125">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="63592-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="63592-126">toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="63592-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="63592-127">Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="63592-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="63592-128">toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="63592-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="63592-129">Después de crea Hola VM, escriba Hola `az network nic show --name MyNic1 --resource-group myResourceGroup` configuración de NIC de comando tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="63592-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="63592-130">Escriba hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview una lista de configuraciones de IP de hello asociados toohello equipo NIC.</span><span class="sxs-lookup"><span data-stu-id="63592-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="63592-131">Sistema operativo de la VM de toohello las direcciones IP privada de agregar Hola siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="63592-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="63592-132"><a name="add"></a>Agregar tooa de direcciones IP virtual</span><span class="sxs-lookup"><span data-stu-id="63592-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="63592-133">Puede agregar adicionales pública y privada IP direcciones tooan existente NIC siguiendo los pasos de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="63592-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="63592-134">ejemplos de Hello parten de hello [escenario](#Scenario) descrito en este artículo.</span><span class="sxs-lookup"><span data-stu-id="63592-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="63592-135">Abra un shell de comandos y Hola completa restante pasos de esta sección dentro de una sola sesión.</span><span class="sxs-lookup"><span data-stu-id="63592-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="63592-136">Si aún no tiene la CLI de Azure instalado y configurado, Hola completa los pasos de hello [instalación de CLI de Azure 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour de artículo y de inicio de sesión de cuenta de Azure con hello `az-login` comando.</span><span class="sxs-lookup"><span data-stu-id="63592-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="63592-137">Complete los pasos de hello en una de las siguientes secciones, según sus requisitos de hello:</span><span class="sxs-lookup"><span data-stu-id="63592-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="63592-138">**Incorporación de una dirección IP privada**</span><span class="sxs-lookup"><span data-stu-id="63592-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="63592-139">tooadd una tooa de dirección IP privada NIC, debe crear una configuración de IP mediante el comando hello que sigue.</span><span class="sxs-lookup"><span data-stu-id="63592-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="63592-140">dirección IP estática de Hello debe ser una dirección no utilizada para la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="63592-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="63592-141">Cree tantas configuraciones como sea necesario mediante nombres de configuración únicos y direcciones IP privadas (para las configuraciones con direcciones IP estáticas).</span><span class="sxs-lookup"><span data-stu-id="63592-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="63592-142">**Incorporación de una dirección IP pública**</span><span class="sxs-lookup"><span data-stu-id="63592-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="63592-143">Se agrega una dirección IP pública asociando tooeither una nueva configuración de IP o una configuración de IP existente.</span><span class="sxs-lookup"><span data-stu-id="63592-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="63592-144">Complete los pasos de hello en una de las secciones de Hola que siguen, como sea necesario.</span><span class="sxs-lookup"><span data-stu-id="63592-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="63592-145">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="63592-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="63592-146">toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="63592-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="63592-147">Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="63592-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="63592-148">toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="63592-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="63592-149">**Asociar Hola recursos tooa nueva configuración de IP**</span><span class="sxs-lookup"><span data-stu-id="63592-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="63592-150">Siempre que agregue una dirección IP pública en una nueva configuración de IP, también debe agregar una dirección IP privada, porque todas las configuraciones de IP deben tener una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="63592-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="63592-151">Puede agregar un recurso de dirección IP pública existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="63592-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="63592-152">toocreate uno nuevo, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="63592-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="63592-153">toocreate una nueva configuración de IP con una dirección IP privada estática y Hola asociados *myPublicIP3* IP pública recurso Dirección, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="63592-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="63592-154">**Configuración de IP existente de hello asociar recursos tooan** un recurso de dirección IP público sólo puede ser la configuración de IP tooan asociado que ya no tiene asociado.</span><span class="sxs-lookup"><span data-stu-id="63592-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="63592-155">Puede determinar si una configuración de IP tiene una dirección IP pública asociada mediante la especificación de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="63592-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="63592-156">Salida que se devuelve:</span><span class="sxs-lookup"><span data-stu-id="63592-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="63592-157">Desde hello **PublicIpAddressId** columna para *IpConfig-3* espacio en blanco en hello resultado, ningún recurso de dirección IP pública está asociada actualmente tooit.</span><span class="sxs-lookup"><span data-stu-id="63592-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="63592-158">Puede agregar una existente pública IP dirección recursos tooIpConfig-3, o escriba Hola después toocreate comando uno:</span><span class="sxs-lookup"><span data-stu-id="63592-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="63592-159">Escriba el siguiente comando con el nombre por la configuración de IP existente de recursos toohello de dirección IP pública de tooassociate Hola de hello *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="63592-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="63592-160">Direcciones IP privadas de vista Hola y Hola pública una dirección IP Id. de recurso asignados toohello NIC escribiendo Hola el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="63592-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="63592-161">Salida que se devuelve:</span><span class="sxs-lookup"><span data-stu-id="63592-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="63592-162">Agregar direcciones IP privadas Hola que se ha agregado el sistema operativo la VM de toohello NIC toohello siguiendo las instrucciones de Hola Hola [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="63592-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="63592-163">No agregue el sistema de operativo para toohello el público direcciones IP Hola.</span><span class="sxs-lookup"><span data-stu-id="63592-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
