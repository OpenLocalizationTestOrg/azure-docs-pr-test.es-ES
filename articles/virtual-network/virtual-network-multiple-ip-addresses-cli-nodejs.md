---
title: aaaVM con varias direcciones IP con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooassign varias direcciones IP tooa máquina virtual usando Hola 1.0 de CLI de Azure | Administrador de recursos."
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="7bad0-103">Asignar varias direcciones IP máquinas toovirtual mediante Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7bad0-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="7bad0-104">Este artículo explica cómo toocreate una máquina virtual (VM) a través de modelo de implementación de Azure Resource Manager de hello mediante Hola 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bad0-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="7bad0-105">No se puede asignar tooresources que se creó mediante el modelo de implementación clásica de Hola a varias direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="7bad0-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="7bad0-106">más información acerca de los modelos de implementación de Azure, lea hello toolearn [comprender los modelos de implementación](../resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="7bad0-107"><a name = "create"></a>Creación de una máquina virtual con varias direcciones IP</span><span class="sxs-lookup"><span data-stu-id="7bad0-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="7bad0-108">Puede completar esta tarea mediante hello Azure CLI 1.0 (en este artículo) o hello [CLI de Azure 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7bad0-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="7bad0-109">pasos de Hola que siguen explican cómo toocreate aborda un máquina virtual con varias IP de ejemplo, tal y como se describe en el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bad0-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="7bad0-110">Cambie los nombres de variable los y tipos de direcciones IP según sea necesario para la implementación.</span><span class="sxs-lookup"><span data-stu-id="7bad0-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="7bad0-111">Instalar y configurar hello Azure CLI 1.0 por hello siguiente pasos en hello [instalar y configurar hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo e inicie sesión en su cuenta de Azure con hello `azure-login` comando.</span><span class="sxs-lookup"><span data-stu-id="7bad0-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="7bad0-112">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="7bad0-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="7bad0-113">Cree una red virtual:</span><span class="sxs-lookup"><span data-stu-id="7bad0-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="7bad0-114">Crear una subred de red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="7bad0-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="7bad0-115">Crear una cuenta de almacenamiento para VM Hola.</span><span class="sxs-lookup"><span data-stu-id="7bad0-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="7bad0-116">Antes de ejecutar Hola siguiente comando, reemplace *mystorageaccount* con un nombre único.</span><span class="sxs-lookup"><span data-stu-id="7bad0-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="7bad0-117">nombre de Hello debe ser único en Azure:</span><span class="sxs-lookup"><span data-stu-id="7bad0-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="7bad0-118">Crear configuraciones de IP, una NIC de Hola y asignar Hola IP configuraciones toohello equipo NIC.</span><span class="sxs-lookup"><span data-stu-id="7bad0-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="7bad0-119">Puede agregar, quitar o cambiar las configuraciones de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7bad0-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="7bad0-120">Hola siguiendo configuraciones se describe en el escenario de hello:</span><span class="sxs-lookup"><span data-stu-id="7bad0-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="7bad0-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="7bad0-121">**IPConfig-1**</span></span>

    <span data-ttu-id="7bad0-122">Escriba los comandos de Hola que siguen toocreate:</span><span class="sxs-lookup"><span data-stu-id="7bad0-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="7bad0-123">Un recurso de dirección IP pública con una dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="7bad0-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="7bad0-124">Una NIC, asignación de dirección IP pública de Hola y un estático tooit de dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="7bad0-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="7bad0-125">Reemplace *mypublicdns* con un nombre que sea único dentro de hello ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bad0-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="7bad0-126">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="7bad0-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="7bad0-127">toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="7bad0-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="7bad0-128">Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="7bad0-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="7bad0-129">toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="7bad0-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="7bad0-130">**IPConfig-2**</span></span>

     <span data-ttu-id="7bad0-131">Un nuevo recurso de dirección IP público y una nueva configuración de IP con una dirección IP pública estática y una dirección IP privada estática, escriba Hola después toocreate de comandos:</span><span class="sxs-lookup"><span data-stu-id="7bad0-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="7bad0-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="7bad0-132">**IPConfig-3**</span></span>

    <span data-ttu-id="7bad0-133">Escriba Hola después comandos toocreate una configuración de IP con una dirección IP privada estática y ninguna dirección IP pública:</span><span class="sxs-lookup"><span data-stu-id="7bad0-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="7bad0-134">Aunque este artículo asigna todos los tooa de configuraciones de IP única NIC, también puede asignar varias IP configuraciones tooany NIC en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7bad0-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="7bad0-135">toolearn cómo leer de una máquina virtual con varias NIC toocreate Hola crear una máquina virtual con varias NIC el artículo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="7bad0-136">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="7bad0-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="7bad0-137">toochange Hola v2 de tooStandard DS2 de tamaño de máquina virtual, por ejemplo, basta con agregar Hola después de la propiedad `--vm-size Standard_DS3_v2` toohello `azure vm create` comando en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="7bad0-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="7bad0-138">Escriba Hola después comando tooview hello NIC y Hola asociados configuraciones IP:</span><span class="sxs-lookup"><span data-stu-id="7bad0-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="7bad0-139">Sistema operativo de la VM de toohello las direcciones IP privada de agregar Hola siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="7bad0-140"><a name="add"></a>Agregar tooa de direcciones IP virtual</span><span class="sxs-lookup"><span data-stu-id="7bad0-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="7bad0-141">Puede agregar adicionales pública y privada IP direcciones tooan existente NIC siguiendo los pasos de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="7bad0-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="7bad0-142">ejemplos de Hello parten de hello [escenario](#Scenario) descrito en este artículo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="7bad0-143">Abra completa hello restantes pasos de esta sección dentro de una sola sesión CLI y CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bad0-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="7bad0-144">Si aún no tiene la CLI de Azure instalado y configurado, Hola completa los pasos de hello [instalar y configurar hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo e inicie sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bad0-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="7bad0-145">Complete los pasos de hello en una de las siguientes secciones, según sus requisitos de hello:</span><span class="sxs-lookup"><span data-stu-id="7bad0-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="7bad0-146">**Incorporación de una dirección IP privada**</span><span class="sxs-lookup"><span data-stu-id="7bad0-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="7bad0-147">tooadd una tooa de dirección IP privada NIC, debe crear una configuración de IP mediante el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bad0-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="7bad0-148">dirección estática Hola debe ser una dirección no utilizada para la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bad0-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="7bad0-149">Cree tantas configuraciones como sea necesario mediante nombres de configuración únicos y direcciones IP privadas (para las configuraciones con direcciones IP estáticas).</span><span class="sxs-lookup"><span data-stu-id="7bad0-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="7bad0-150">**Incorporación de una dirección IP pública**</span><span class="sxs-lookup"><span data-stu-id="7bad0-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="7bad0-151">Se agrega una dirección IP pública asociando tooeither una nueva configuración de IP o una configuración de IP existente.</span><span class="sxs-lookup"><span data-stu-id="7bad0-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="7bad0-152">Complete los pasos de hello en una de las secciones de Hola que siguen, como sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7bad0-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="7bad0-153">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="7bad0-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="7bad0-154">toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="7bad0-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="7bad0-155">Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="7bad0-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="7bad0-156">toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="7bad0-157">**Asociar Hola recursos tooa nueva configuración de IP**</span><span class="sxs-lookup"><span data-stu-id="7bad0-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="7bad0-158">Siempre que agregue una dirección IP pública en una nueva configuración de IP, también debe agregar una dirección IP privada, porque todas las configuraciones de IP deben tener una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="7bad0-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="7bad0-159">Puede agregar un recurso de dirección IP pública existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="7bad0-160">toocreate uno nuevo, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7bad0-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="7bad0-161">toocreate una nueva configuración de IP con una dirección IP privada estática y Hola asociados *myPublicIP3* IP pública recurso Dirección, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7bad0-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="7bad0-162">**Asociar la configuración de IP existente de hello recursos tooan**</span><span class="sxs-lookup"><span data-stu-id="7bad0-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="7bad0-163">Configuración de IP de tooan asociado que ya no tiene asociado sólo puede ser un recurso de dirección IP público.</span><span class="sxs-lookup"><span data-stu-id="7bad0-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="7bad0-164">Puede determinar si una configuración de IP tiene una dirección IP pública asociada mediante la especificación de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7bad0-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="7bad0-165">Busque un toohello similar de la línea que aparece más adelante para IPConfig-3 en hello devolvía los resultados:</span><span class="sxs-lookup"><span data-stu-id="7bad0-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="7bad0-166">Desde hello **IP pública** columna para *IpConfig-3* está en blanco, ningún recurso de dirección IP pública está asociada actualmente tooit.</span><span class="sxs-lookup"><span data-stu-id="7bad0-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="7bad0-167">Puede agregar una existente pública IP dirección recursos tooIpConfig-3, o escriba Hola después toocreate comando uno:</span><span class="sxs-lookup"><span data-stu-id="7bad0-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="7bad0-168">Escriba el siguiente comando con el nombre por la configuración de IP existente de recursos toohello de dirección IP pública de tooassociate Hola de hello *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="7bad0-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="7bad0-169">Ver direcciones IP privadas de Hola y Hola pública IP dirección recursos asignado toohello NIC escribiendo Hola el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7bad0-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="7bad0-170">Hola devuelve el resultado será similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="7bad0-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="7bad0-171">Agregar direcciones IP privadas Hola que se ha agregado el sistema operativo la VM de toohello NIC toohello siguiendo las instrucciones de Hola Hola [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="7bad0-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="7bad0-172">No agregue el sistema de operativo para toohello el público direcciones IP Hola.</span><span class="sxs-lookup"><span data-stu-id="7bad0-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
