---
title: Control del enrutamiento y las aplicaciones virtuales con la CLI de Azure 2.0 | Microsoft Docs
description: "Obtenga información sobre cómo controlar el enrutamiento y las aplicaciones virtuales con la CLI de Azure 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: e5d9519998346619093f443b740c8904283f76e8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-20"></a><span data-ttu-id="425e7-103">Creación de rutas definidas por el usuario (UDR) en la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="425e7-103">Create User-Defined Routes (UDR) using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="425e7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="425e7-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="425e7-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="425e7-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="425e7-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="425e7-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="425e7-107">PowerShell: implementación clásica</span><span class="sxs-lookup"><span data-stu-id="425e7-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="425e7-108">CLI: implementación clásica</span><span class="sxs-lookup"><span data-stu-id="425e7-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="425e7-109">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="425e7-109">CLI versions to complete the task</span></span> 

<span data-ttu-id="425e7-110">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="425e7-110">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="425e7-111">[CLI de Azure 1.0](virtual-network-create-udr-arm-cli-nodejs.md): la CLI para los modelos de implementación clásico y de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="425e7-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="425e7-112">[CLI de Azure 2.0](#Create-the-UDR-for-the-front-end-subnet): la CLI de última generación para el modelo de implementación de administración de recursos (este artículo).</span><span class="sxs-lookup"><span data-stu-id="425e7-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="425e7-113">En los siguientes comandos de CLI de Azure de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="425e7-113">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="425e7-114">Si desea ejecutar los comandos tal y como aparecen en este documento, cree primero el entorno de prueba mediante la implementación de [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="425e7-114">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="425e7-115">Creación de la ruta definida por el usuario para la subred front-end</span><span class="sxs-lookup"><span data-stu-id="425e7-115">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="425e7-116">Para crear la tabla de rutas y la ruta necesaria para la subred front-end según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="425e7-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="425e7-117">Cree una tabla de rutas para la subred front-end con el comando [az network route-table create](/cli/azure/network/route-table#create):</span><span class="sxs-lookup"><span data-stu-id="425e7-117">Create a route table for the front-end subnet with the [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="425e7-118">Salida:</span><span class="sxs-lookup"><span data-stu-id="425e7-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="425e7-119">Cree una ruta que envíe todo el tráfico destinado a la subred back-end (192.168.2.0/24) a la máquina virtual **FW1** (192.168.0.4) con el comando [az network route-table route create](/cli/azure/network/route-table/route#create):</span><span class="sxs-lookup"><span data-stu-id="425e7-119">Create a route that sends all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4) using the [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="425e7-120">Salida:</span><span class="sxs-lookup"><span data-stu-id="425e7-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="425e7-121">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="425e7-121">Parameters:</span></span>

    * <span data-ttu-id="425e7-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="425e7-122">**--route-table-name**.</span></span> <span data-ttu-id="425e7-123">Nombre de la tabla de rutas a la que se agregará la ruta.</span><span class="sxs-lookup"><span data-stu-id="425e7-123">Name of the route table where the route will be added.</span></span> <span data-ttu-id="425e7-124">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="425e7-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="425e7-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="425e7-125">**--address-prefix**.</span></span> <span data-ttu-id="425e7-126">Prefijo de dirección de la subred a la que se destinan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="425e7-126">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="425e7-127">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="425e7-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="425e7-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="425e7-128">**--next-hop-type**.</span></span> <span data-ttu-id="425e7-129">Tipo de objeto al que se enviará el tráfico.</span><span class="sxs-lookup"><span data-stu-id="425e7-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="425e7-130">Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="425e7-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="425e7-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="425e7-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="425e7-132">Dirección IP para el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="425e7-132">IP address for next hop.</span></span> <span data-ttu-id="425e7-133">En este escenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="425e7-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="425e7-134">Ejecute el comando [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) para asociar la tabla de rutas creada anteriormente a la subred **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="425e7-134">Run the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="425e7-135">Salida:</span><span class="sxs-lookup"><span data-stu-id="425e7-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="425e7-136">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="425e7-136">Parameters:</span></span>
    
    * <span data-ttu-id="425e7-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="425e7-137">**--vnet-name**.</span></span> <span data-ttu-id="425e7-138">Nombre de la red virtual donde se encuentra la subred.</span><span class="sxs-lookup"><span data-stu-id="425e7-138">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="425e7-139">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="425e7-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="425e7-140">Creación de la ruta definida por el usuario para la subred back-end</span><span class="sxs-lookup"><span data-stu-id="425e7-140">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="425e7-141">Para crear la tabla de rutas y la ruta necesaria para la subred back-end según el escenario anterior, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="425e7-141">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="425e7-142">Ejecute el comando siguiente para crear una tabla de rutas para la subred back-end:</span><span class="sxs-lookup"><span data-stu-id="425e7-142">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="425e7-143">Ejecute el comando siguiente para crear una ruta en la tabla de rutas para enviar todo el tráfico destinado a la subred front-end (192.168.1.0/24) a la VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="425e7-143">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="425e7-144">Ejecute el comando siguiente para asociar la tabla de rutas a la subred **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="425e7-144">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="425e7-145">Habilitación del reenvío IP en FW1</span><span class="sxs-lookup"><span data-stu-id="425e7-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="425e7-146">Para habilitar el reenvío IP en la NIC que ha usado **FW1**, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="425e7-146">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="425e7-147">Ejecutar el comando [az network nic show](/cli/azure/network/nic#show) con un filtro JMESPATH para mostrar el valor actual **enable-ip-forwarding** de **Habilitar reenvío IP**.</span><span class="sxs-lookup"><span data-stu-id="425e7-147">Run the [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter to display the current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="425e7-148">Se debe establecer en *false*.</span><span class="sxs-lookup"><span data-stu-id="425e7-148">It should be set to *false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="425e7-149">Salida:</span><span class="sxs-lookup"><span data-stu-id="425e7-149">Output:</span></span>

        false

2. <span data-ttu-id="425e7-150">Ejecute el comando siguiente para habilitar el reenvío IP:</span><span class="sxs-lookup"><span data-stu-id="425e7-150">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="425e7-151">Puede examinar la salida que se transmite a la consola de o simplemente vuelva a probar el valor **enableIpForwarding** específico:</span><span class="sxs-lookup"><span data-stu-id="425e7-151">You can examine the output streamed to the console, or just retest for the specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="425e7-152">Salida:</span><span class="sxs-lookup"><span data-stu-id="425e7-152">Output:</span></span>

        true

    <span data-ttu-id="425e7-153">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="425e7-153">Parameters:</span></span>

    <span data-ttu-id="425e7-154">**--ip-forwarding**: *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="425e7-154">**--ip-forwarding**: *true* or *false*.</span></span>

