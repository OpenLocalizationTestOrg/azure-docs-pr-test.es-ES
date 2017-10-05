---
title: "Máquina virtual con varias direcciones IP mediante la CLI de Azure 1.0 | Microsoft Docs"
description: "Aprenda a asignar varias direcciones IP a una máquina virtual con la CLI de Azure 1.0 | Resource Manager."
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
ms.openlocfilehash: 9f085dfa1fe4db36d58cb976bb550a46bf241ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-azure-cli-10"></a><span data-ttu-id="3e8b1-103">Asignación de varias direcciones IP a máquinas virtuales mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="3e8b1-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="3e8b1-104">En este artículo se describe cómo crear una máquina virtual con el modelo de implementación de Azure Resource Manager mediante la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span></span> <span data-ttu-id="3e8b1-105">No se pueden asignar varias direcciones IP a los recursos creados mediante el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="3e8b1-106">Para información acerca de los modelos de implementación de Azure, lea el artículo [Understand deployment models](../resource-manager-deployment-model.md) (Descripción de los modelos de implementación).</span><span class="sxs-lookup"><span data-stu-id="3e8b1-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="3e8b1-107"><a name = "create"></a>Creación de una máquina virtual con varias direcciones IP</span><span class="sxs-lookup"><span data-stu-id="3e8b1-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="3e8b1-108">Puede completar esta tarea mediante la CLI de Azure 1.0 (en este artículo) o la [CLI de Azure 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3e8b1-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="3e8b1-109">En los pasos siguientes se explica cómo crear una VM de ejemplo con varias direcciones IP, tal como se describe en el escenario.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="3e8b1-110">Cambie los nombres de variable los y tipos de direcciones IP según sea necesario para la implementación.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="3e8b1-111">Instale y configure la CLI de Azure 1.0 siguiendo los pasos del artículo [Instalación de la CLI de Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e inicie sesión en la cuenta de Azure con el comando `azure-login`.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span></span>

2. <span data-ttu-id="3e8b1-112">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="3e8b1-113">Cree una red virtual:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="3e8b1-114">Cree una subred en la red virtual:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-114">Create a subnet in the virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="3e8b1-115">Cree una cuenta de almacenamiento para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-115">Create  a storage account for the VM.</span></span> <span data-ttu-id="3e8b1-116">Antes de ejecutar el siguiente comando, reemplace *mystorageaccount* por un nombre único.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-116">Before running the following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="3e8b1-117">El nombre debe ser único en Azure:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-117">The name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="3e8b1-118">Cree las configuraciones de IP, una NIC y asigne las configuraciones de IP a la NIC.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span></span> <span data-ttu-id="3e8b1-119">Puede agregar, quitar o cambiar las configuraciones según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-119">You can add, remove, or change the configurations as necessary.</span></span> <span data-ttu-id="3e8b1-120">En el escenario se describen las siguientes configuraciones:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-120">The following configurations are described in the scenario:</span></span>

    <span data-ttu-id="3e8b1-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="3e8b1-121">**IPConfig-1**</span></span>

    <span data-ttu-id="3e8b1-122">Escriba los comandos siguientes para crear:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-122">Enter the commands that follow to create:</span></span>

    - <span data-ttu-id="3e8b1-123">Un recurso de dirección IP pública con una dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="3e8b1-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="3e8b1-124">Una NIC, asignando un dirección IP pública y una dirección IP privada estática.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-124">A NIC, assigning the public IP address and a static private IP address to it.</span></span>
    
    <span data-ttu-id="3e8b1-125">Reemplace *mypublicdns* por un nombre que sea único dentro de la ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="3e8b1-126">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="3e8b1-127">Para más información sobre los precios de las direcciones IP, lea la página [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="3e8b1-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="3e8b1-128">Existe un límite para el número de direcciones IP públicas que pueden usarse dentro de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="3e8b1-129">Para más información sobre los límites, lea el artículo sobre los [límites de Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="3e8b1-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="3e8b1-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="3e8b1-130">**IPConfig-2**</span></span>

     <span data-ttu-id="3e8b1-131">Escriba los comandos siguientes para crear un nuevo recurso de dirección IP pública y una nueva configuración de IP con una dirección IP pública estática y una dirección IP privada estática:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="3e8b1-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="3e8b1-132">**IPConfig-3**</span></span>

    <span data-ttu-id="3e8b1-133">Escriba los comandos siguientes para crear una configuración de IP con una dirección IP privada estática y ninguna dirección IP no pública:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="3e8b1-134">Aunque este artículo asigna todas las configuraciones de IP a una NIC única, también puede asignar varias configuraciones de IP a una NIC en una VM.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span></span> <span data-ttu-id="3e8b1-135">Para aprender a crear una VM con varias NIC, lea el artículo Implementación de máquinas virtuales con varias NIC mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="3e8b1-136">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="3e8b1-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="3e8b1-137">Para cambiar el tamaño de VM a Estándar DS2 v2, por ejemplo, simplemente agregue la siguiente propiedad `--vm-size Standard_DS3_v2` al comando `azure vm create` en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="3e8b1-138">Escriba el siguiente comando para ver la NIC y las configuraciones de IP asociadas:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-138">Enter the following command to view the NIC and the associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="3e8b1-139">Agregue al sistema operativo de la máquina virtual la dirección IP privada siguiendo las instrucciones de la sección [Incorporación de direcciones IP a un sistema operativo de la VM](#os-config) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="3e8b1-140"><a name="add"></a>Incorporación de direcciones IP a una VM</span><span class="sxs-lookup"><span data-stu-id="3e8b1-140"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="3e8b1-141">Puede agregar más direcciones IP públicas y privadas a una NIC existente completando los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="3e8b1-142">Los ejemplos se crean en el [escenario](#Scenario) descrito en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-142">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="3e8b1-143">Abra la CLI de Azure y complete los pasos restantes de esta sección dentro de una sola sesión de CLI.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="3e8b1-144">Si todavía no tiene la CLI de Azure instalada y configurada, complete los pasos del artículo [Instalación de la CLI de Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="3e8b1-145">Complete los pasos de una de las secciones siguientes, según sus requisitos:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-145">Complete the steps in one of the following sections, based on your requirements:</span></span>

    - <span data-ttu-id="3e8b1-146">**Incorporación de una dirección IP privada**</span><span class="sxs-lookup"><span data-stu-id="3e8b1-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="3e8b1-147">Para agregar una dirección IP privada a una NIC, debe crear una configuración de IP mediante el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span></span> <span data-ttu-id="3e8b1-148">La dirección estática debe ser una dirección no utilizada para la subred.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-148">The static address must be an unused address for the subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="3e8b1-149">Cree tantas configuraciones como sea necesario mediante nombres de configuración únicos y direcciones IP privadas (para las configuraciones con direcciones IP estáticas).</span><span class="sxs-lookup"><span data-stu-id="3e8b1-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="3e8b1-150">**Incorporación de una dirección IP pública**</span><span class="sxs-lookup"><span data-stu-id="3e8b1-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="3e8b1-151">Se agrega una dirección IP pública mediante la asociación a una nueva configuración de IP o una configuración de IP existente.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="3e8b1-152">Complete los pasos de una de las secciones siguientes, según sea preciso.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-152">Complete the steps in one of the sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="3e8b1-153">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="3e8b1-154">Para más información sobre los precios de las direcciones IP, lea la página [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="3e8b1-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="3e8b1-155">Existe un límite para el número de direcciones IP públicas que pueden usarse dentro de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="3e8b1-156">Para más información sobre los límites, lea el artículo sobre los [límites de Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="3e8b1-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="3e8b1-157">**Asociación del recurso a una nueva configuración de IP**</span><span class="sxs-lookup"><span data-stu-id="3e8b1-157">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="3e8b1-158">Siempre que agregue una dirección IP pública en una nueva configuración de IP, también debe agregar una dirección IP privada, porque todas las configuraciones de IP deben tener una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="3e8b1-159">Puede agregar un recurso de dirección IP pública existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="3e8b1-160">Para crear uno nuevo, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-160">To create a new one, enter the following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="3e8b1-161">Para crear una nueva configuración de IP con una dirección IP privada estática y el recurso de dirección IP pública *myPublicIP3*, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="3e8b1-162">**Asociación del recurso a una nueva configuración de IP existente**</span><span class="sxs-lookup"><span data-stu-id="3e8b1-162">**Associate the resource to an existing IP configuration**</span></span>

        <span data-ttu-id="3e8b1-163">Solo se puede asociar un recurso de dirección IP pública a una configuración de IP que ya no tiene asociado uno.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="3e8b1-164">Puede determinar si una configuración de IP tiene una dirección IP pública asociada escribiendo el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="3e8b1-165">Busque una línea similar a la que aparece después de IPConfig-3 en la salida devuelta:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="3e8b1-166">Puesto que la columna **IP pública** para *IpConfig-3* está en blanco, ningún recurso de dirección IP pública está asociado actualmente a ella.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="3e8b1-167">Puede agregar un recurso de dirección IP pública existente a IpConfig-3 o escribir el siguiente comando para crear uno:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="3e8b1-168">Escriba el siguiente comando para asociar el recurso de dirección IP pública a la configuración de IP existente llamada *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="3e8b1-169">Vea las direcciones IP privadas y los recursos de dirección IP pública asignados a la NIC escribiendo el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="3e8b1-170">La salida devuelta será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e8b1-170">The returned output is similar to the following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="3e8b1-171">Agregue al sistema operativo de la VM las direcciones IP privadas que agregó a la NIC siguiendo las instrucciones de la sección [Incorporación de direcciones IP a un sistema operativo de la VM](#os-config) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="3e8b1-172">No agregue las direcciones IP públicas al sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3e8b1-172">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
