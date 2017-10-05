---
title: "Creación de una red virtual: CLI de Azure 2.0 | Microsoft Docs"
description: Aprenda a crear una red virtual mediante la CLI de Azure 2.0.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="db0c5-103">Creación de una red virtual mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="db0c5-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="db0c5-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="db0c5-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="db0c5-105">Microsoft recomienda crear recursos mediante el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db0c5-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="db0c5-106">Para más información acerca de las diferencias entre los dos modelos, lea el artículo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Descripción de los modelos de implementación de Azure).</span><span class="sxs-lookup"><span data-stu-id="db0c5-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="db0c5-107">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="db0c5-107">CLI versions to complete the task</span></span>
<span data-ttu-id="db0c5-108">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="db0c5-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="db0c5-109">[CLI de Azure 1.0](virtual-networks-create-vnet-cli-nodejs.md): la CLI para los modelos de implementación clásico y de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="db0c5-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="db0c5-110">[CLI de Azure 2.0](#create-a-virtual-network): la CLI de última generación para el modelo de implementación de administración de recursos (este artículo).</span><span class="sxs-lookup"><span data-stu-id="db0c5-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="db0c5-111">También puede crear una red virtual mediante Resource Manager con otras herramientas o crear una red virtual a través del modelo de implementación clásica seleccionando una opción diferente en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="db0c5-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="db0c5-112">Portal</span><span class="sxs-lookup"><span data-stu-id="db0c5-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="db0c5-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db0c5-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="db0c5-114">CLI</span><span class="sxs-lookup"><span data-stu-id="db0c5-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="db0c5-115">Plantilla</span><span class="sxs-lookup"><span data-stu-id="db0c5-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="db0c5-116">Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="db0c5-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="db0c5-117">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="db0c5-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="db0c5-118">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="db0c5-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="db0c5-119">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="db0c5-119">Create a virtual network</span></span>

<span data-ttu-id="db0c5-120">Para crear una red virtual mediante la CLI de Azure 2.0, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="db0c5-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="db0c5-121">Instale y configure la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="db0c5-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="db0c5-122">Cree un grupo de recursos para la red virtual mediante el comando [az group create](/cli/azure/group#create) con los argumentos `--name` y `--location`:</span><span class="sxs-lookup"><span data-stu-id="db0c5-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="db0c5-123">Creación de una red virtual y una subred:</span><span class="sxs-lookup"><span data-stu-id="db0c5-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="db0c5-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="db0c5-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="db0c5-125">Parámetros usados:</span><span class="sxs-lookup"><span data-stu-id="db0c5-125">Parameters used:</span></span>

    - <span data-ttu-id="db0c5-126">`--name TestVNet`: nombre de la red virtual que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="db0c5-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="db0c5-127">`--resource-group TestRG`: el nombre del grupo de recursos que controla el recurso.</span><span class="sxs-lookup"><span data-stu-id="db0c5-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="db0c5-128">`--location centralus`: la ubicación en la que se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="db0c5-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="db0c5-129">`--address-prefix 192.168.0.0/16`: el bloque y prefijo de dirección.</span><span class="sxs-lookup"><span data-stu-id="db0c5-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="db0c5-130">`--subnet-name FrontEnd`: el nombre de la subred.</span><span class="sxs-lookup"><span data-stu-id="db0c5-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="db0c5-131">`--subnet-prefix 192.168.1.0/24`: el bloque y prefijo de dirección.</span><span class="sxs-lookup"><span data-stu-id="db0c5-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="db0c5-132">Para enumerar la información básica que se usará en el comando siguiente, puede enviar una consulta a la red virtual usando un [filtro de consulta](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="db0c5-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="db0c5-133">Lo que genera el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="db0c5-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="db0c5-134">Creación de una subred:</span><span class="sxs-lookup"><span data-stu-id="db0c5-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="db0c5-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="db0c5-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="db0c5-136">Parámetros usados:</span><span class="sxs-lookup"><span data-stu-id="db0c5-136">Parameters used:</span></span>

    - <span data-ttu-id="db0c5-137">`--address-prefix 192.168.2.0/24`: el bloque CIDR de subred.</span><span class="sxs-lookup"><span data-stu-id="db0c5-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="db0c5-138">`--name BackEnd`: el nombre de la nueva subred.</span><span class="sxs-lookup"><span data-stu-id="db0c5-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="db0c5-139">`--resource-group TestRG`: el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="db0c5-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="db0c5-140">`--vnet-name TestVNet`: el nombre de la red virtual propietaria.</span><span class="sxs-lookup"><span data-stu-id="db0c5-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="db0c5-141">Envíe una consulta a las propiedades de la nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="db0c5-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="db0c5-142">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="db0c5-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="db0c5-143">Envíe una consulta a las propiedades de las subredes:</span><span class="sxs-lookup"><span data-stu-id="db0c5-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="db0c5-144">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="db0c5-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="db0c5-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db0c5-145">Next steps</span></span>

<span data-ttu-id="db0c5-146">Aprenda a conectar:</span><span class="sxs-lookup"><span data-stu-id="db0c5-146">Learn how to connect:</span></span>

- <span data-ttu-id="db0c5-147">Una máquina virtual (VM) a una red virtual, para lo cual debería leer el artículo [Creación de una máquina virtual Linux](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="db0c5-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="db0c5-148">En lugar de crear una red virtual y la subred en los pasos de los artículos, puede seleccionar una red virtual y una subred a la que conectar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db0c5-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="db0c5-149">La red virtual a otras redes virtuales. Para ello, lea el artículo [Conexión de redes virtuales](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db0c5-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="db0c5-150">La red virtual a una red local mediante una red privada virtual (VPN) de sitio a sitio o un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="db0c5-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="db0c5-151">Aprenda cómo hacerlo leyendo los artículos [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) (Conexión de una red virtual a una red local mediante una VPN de sitio a sitio) y [Conexión de una red virtual a un circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="db0c5-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>