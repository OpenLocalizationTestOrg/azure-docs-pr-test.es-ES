---
title: "aaaControl enrutamiento en una red Virtual de Azure - CLI - clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocontrol enrutamiento en redes virtuales mediante Hola CLI de Azure en el modelo de implementación clásica de Hola"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="431c2-103">Enrutamiento de control y el uso de dispositivos virtuales (clásicos) de uso Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="431c2-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="431c2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="431c2-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="431c2-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="431c2-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="431c2-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="431c2-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="431c2-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="431c2-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="431c2-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="431c2-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="431c2-109">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="431c2-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="431c2-110">También puede [controlar el enrutamiento y usar dispositivos virtuales en el modelo de implementación del Administrador de recursos de hello](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="431c2-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="431c2-111">comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado basándose en el escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="431c2-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="431c2-112">Si desea toorun comandos de hello, que se muestran en este documento, crear se muestra en el entorno de hello [crear una red virtual (clásica) con hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="431c2-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="431c2-113">Crear hello UDR para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="431c2-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="431c2-114">tabla de rutas de hello toocreate y ruta necesarios para una subred de front-end de hello basándose en el escenario de hello anterior, siga los pasos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="431c2-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="431c2-115">Siguiente ejecución Hola comando tooswitch tooclassic modo:</span><span class="sxs-lookup"><span data-stu-id="431c2-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="431c2-116">Salida:</span><span class="sxs-lookup"><span data-stu-id="431c2-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="431c2-117">Ejecute hello después comando toocreate una tabla de rutas de subred de front-end de hello:</span><span class="sxs-lookup"><span data-stu-id="431c2-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="431c2-118">Salida:</span><span class="sxs-lookup"><span data-stu-id="431c2-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="431c2-119">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="431c2-119">Parameters:</span></span>
   
   * <span data-ttu-id="431c2-120">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="431c2-120">**-l (or --location)**.</span></span> <span data-ttu-id="431c2-121">Región de Azure donde hello nuevo NSG se creará.</span><span class="sxs-lookup"><span data-stu-id="431c2-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="431c2-122">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="431c2-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="431c2-123">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="431c2-123">**-n (or --name)**.</span></span> <span data-ttu-id="431c2-124">Nombre de hello nuevo NSG.</span><span class="sxs-lookup"><span data-stu-id="431c2-124">Name for hello new NSG.</span></span> <span data-ttu-id="431c2-125">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="431c2-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="431c2-126">Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="431c2-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="431c2-127">Salida:</span><span class="sxs-lookup"><span data-stu-id="431c2-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="431c2-128">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="431c2-128">Parameters:</span></span>
   
   * <span data-ttu-id="431c2-129">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="431c2-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="431c2-130">Nombre de tabla de rutas de Hola donde se agregará la ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="431c2-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="431c2-131">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="431c2-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="431c2-132">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="431c2-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="431c2-133">Prefijo de dirección de subred de Hola donde los paquetes destinados a.</span><span class="sxs-lookup"><span data-stu-id="431c2-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="431c2-134">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="431c2-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="431c2-135">**-t (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="431c2-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="431c2-136">Tipo de objeto al que se enviará el tráfico.</span><span class="sxs-lookup"><span data-stu-id="431c2-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="431c2-137">Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="431c2-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="431c2-138">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="431c2-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="431c2-139">Dirección IP para el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="431c2-139">IP address for next hop.</span></span> <span data-ttu-id="431c2-140">En este escenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="431c2-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="431c2-141">Siguiente ejecución Hola comando tabla de rutas de hello tooassociate creado con hello **front-end** subred:</span><span class="sxs-lookup"><span data-stu-id="431c2-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="431c2-142">Salida:</span><span class="sxs-lookup"><span data-stu-id="431c2-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="431c2-143">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="431c2-143">Parameters:</span></span>
   
   * <span data-ttu-id="431c2-144">**-t (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="431c2-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="431c2-145">Nombre de red virtual donde se encuentra la subred de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="431c2-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="431c2-146">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="431c2-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="431c2-147">**-n (o --subnet-name**.</span><span class="sxs-lookup"><span data-stu-id="431c2-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="431c2-148">Nombre de tabla de rutas de Hola Hola subred se agregará a.</span><span class="sxs-lookup"><span data-stu-id="431c2-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="431c2-149">En este escenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="431c2-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="431c2-150">Crear hello UDR de subred de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="431c2-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="431c2-151">tabla de rutas de hello toocreate y necesarios para la subred de back-end de hello en función de escenario de hello, Hola completa siguiendo los pasos de ruta:</span><span class="sxs-lookup"><span data-stu-id="431c2-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="431c2-152">Ejecute hello después comando toocreate una tabla de rutas de subred de back-end de hello:</span><span class="sxs-lookup"><span data-stu-id="431c2-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="431c2-153">Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="431c2-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="431c2-154">Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **back-end** subred:</span><span class="sxs-lookup"><span data-stu-id="431c2-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

