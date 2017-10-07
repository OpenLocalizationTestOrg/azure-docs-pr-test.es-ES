---
title: dispositivos de enrutamiento y virtual aaaControl utilizando Hola 2.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocontrol dispositivos de enrutamiento y virtual utilizando Hola 2.0 de CLI de Azure."
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
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="3b789-103">Crear rutas definidas por el usuario (UDR) mediante Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3b789-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b789-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b789-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="3b789-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3b789-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="3b789-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="3b789-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="3b789-107">PowerShell: implementación clásica</span><span class="sxs-lookup"><span data-stu-id="3b789-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="3b789-108">CLI: implementación clásica</span><span class="sxs-lookup"><span data-stu-id="3b789-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3b789-109">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="3b789-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="3b789-110">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="3b789-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="3b789-111">[Azure 1.0 de CLI](virtual-network-create-udr-arm-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola</span><span class="sxs-lookup"><span data-stu-id="3b789-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="3b789-112">[Azure 2.0 CLI](#Create-the-UDR-for-the-front-end-subnet) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="3b789-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="3b789-113">comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado basándose en el escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="3b789-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="3b789-114">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de hello implementando [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), haga clic en **implementar tooAzure**, reemplace los valores de parámetros predeterminados de Hola Si fuera necesario y siga las instrucciones de hello en Hola portal.</span><span class="sxs-lookup"><span data-stu-id="3b789-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="3b789-115">Crear hello UDR para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="3b789-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="3b789-116">tabla de rutas de hello toocreate y ruta necesarios para una subred de front-end de hello basándose en el escenario de hello anterior, siga los pasos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="3b789-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="3b789-117">Crear una tabla de rutas de subred de front-end de hello con hello [crear tabla de rutas de red az](/cli/azure/network/route-table#create) comando:</span><span class="sxs-lookup"><span data-stu-id="3b789-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="3b789-118">Salida:</span><span class="sxs-lookup"><span data-stu-id="3b789-118">Output:</span></span>

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

2. <span data-ttu-id="3b789-119">Cree una ruta que envía todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toohello **FW1** máquina virtual (192.168.0.4) con hello [crear ruta de tabla de rutas de red az](/cli/azure/network/route-table/route#create) comando:</span><span class="sxs-lookup"><span data-stu-id="3b789-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="3b789-120">Salida:</span><span class="sxs-lookup"><span data-stu-id="3b789-120">Output:</span></span>

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
    <span data-ttu-id="3b789-121">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="3b789-121">Parameters:</span></span>

    * <span data-ttu-id="3b789-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="3b789-122">**--route-table-name**.</span></span> <span data-ttu-id="3b789-123">Nombre de tabla de rutas de Hola donde se agregará la ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b789-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="3b789-124">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="3b789-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="3b789-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="3b789-125">**--address-prefix**.</span></span> <span data-ttu-id="3b789-126">Prefijo de dirección de subred de Hola donde los paquetes destinados a.</span><span class="sxs-lookup"><span data-stu-id="3b789-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="3b789-127">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="3b789-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="3b789-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="3b789-128">**--next-hop-type**.</span></span> <span data-ttu-id="3b789-129">Tipo de objeto al que se enviará el tráfico.</span><span class="sxs-lookup"><span data-stu-id="3b789-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="3b789-130">Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="3b789-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="3b789-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="3b789-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="3b789-132">Dirección IP para el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="3b789-132">IP address for next hop.</span></span> <span data-ttu-id="3b789-133">En este escenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="3b789-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="3b789-134">Ejecute hello [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update) tabla de enrutamiento de comandos tooassociate Hola creada anteriormente con hello **front-end** subred:</span><span class="sxs-lookup"><span data-stu-id="3b789-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="3b789-135">Salida:</span><span class="sxs-lookup"><span data-stu-id="3b789-135">Output:</span></span>

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

    <span data-ttu-id="3b789-136">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="3b789-136">Parameters:</span></span>
    
    * <span data-ttu-id="3b789-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="3b789-137">**--vnet-name**.</span></span> <span data-ttu-id="3b789-138">Nombre de red virtual donde se encuentra la subred de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3b789-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="3b789-139">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="3b789-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="3b789-140">Crear hello UDR de subred de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="3b789-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="3b789-141">Hola toocreate tabla de rutas y necesarios para la subred de back-end de hello en función de hello escenario anterior, Hola completa siguiendo los pasos de ruta:</span><span class="sxs-lookup"><span data-stu-id="3b789-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="3b789-142">Ejecute hello después comando toocreate una tabla de rutas de subred de back-end de hello:</span><span class="sxs-lookup"><span data-stu-id="3b789-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="3b789-143">Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3b789-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="3b789-144">Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **back-end** subred:</span><span class="sxs-lookup"><span data-stu-id="3b789-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="3b789-145">Habilitación del reenvío IP en FW1</span><span class="sxs-lookup"><span data-stu-id="3b789-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="3b789-146">reenvío de IP tooenable Hola NIC que se utiliza por **FW1**completa Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3b789-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="3b789-147">Ejecute hello [show de nic de red az](/cli/azure/network/nic#show) comando con un hello de toodisplay JMESPATH filtro actual **Habilitar reenvío de ip** valor **reenvío IP habilitar**.</span><span class="sxs-lookup"><span data-stu-id="3b789-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="3b789-148">Se debe establecer demasiado*false*.</span><span class="sxs-lookup"><span data-stu-id="3b789-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="3b789-149">Salida:</span><span class="sxs-lookup"><span data-stu-id="3b789-149">Output:</span></span>

        false

2. <span data-ttu-id="3b789-150">Ejecute hello después de reenvío de IP de tooenable de comando:</span><span class="sxs-lookup"><span data-stu-id="3b789-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="3b789-151">Puede examinar la consola de toohello transmitido por secuencias de salida de hello, o simplemente volver a probar para saludo específico **enableIpForwarding** valor:</span><span class="sxs-lookup"><span data-stu-id="3b789-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="3b789-152">Salida:</span><span class="sxs-lookup"><span data-stu-id="3b789-152">Output:</span></span>

        true

    <span data-ttu-id="3b789-153">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="3b789-153">Parameters:</span></span>

    <span data-ttu-id="3b789-154">**--ip-forwarding**: *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="3b789-154">**--ip-forwarding**: *true* or *false*.</span></span>

