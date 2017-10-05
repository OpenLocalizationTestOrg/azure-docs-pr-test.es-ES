---
title: "Control de enrutamiento en Azure Virtual Network - CLI - Clásico | Microsoft Docs"
description: "Aprenda cómo controlar el enrutamiento en redes virtuales mediante la CLI de Azure en el modelo de implementación clásico"
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
ms.openlocfilehash: 8fcb98723e7e872c932908e3456dc8680deb0901
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-the-azure-cli"></a><span data-ttu-id="471af-103">Control del enrutamiento y uso de aplicaciones virtuales (clásico) mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="471af-103">Control routing and use virtual appliances (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="471af-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="471af-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="471af-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="471af-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="471af-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="471af-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="471af-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="471af-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="471af-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="471af-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="471af-109">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="471af-109">This article covers the classic deployment model.</span></span> <span data-ttu-id="471af-110">También puede [controlar el enrutamiento y el uso de aplicaciones virtuales en el modelo de implementación del Administrador de recursos](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="471af-110">You can also [control routing and use virtual appliances in the Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="471af-111">En los siguientes comandos de CLI de Azure de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="471af-111">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="471af-112">Si desea ejecutar los comandos según aparecen en este documento, cree primero el entorno mostrado en la [creación de una red virtual (clásico) mediante la CLI de Azure](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="471af-112">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using the Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="471af-113">Creación de la ruta definida por el usuario para la subred front-end</span><span class="sxs-lookup"><span data-stu-id="471af-113">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="471af-114">Para crear la tabla de rutas y la ruta necesaria para la subred front-end según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="471af-114">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="471af-115">Ejecute el siguiente comando para cambiar al modo clásico:</span><span class="sxs-lookup"><span data-stu-id="471af-115">Run the following command to switch to classic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="471af-116">Salida:</span><span class="sxs-lookup"><span data-stu-id="471af-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="471af-117">Ejecute el siguiente comando para crear una tabla de rutas para la subred front-end:</span><span class="sxs-lookup"><span data-stu-id="471af-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="471af-118">Salida:</span><span class="sxs-lookup"><span data-stu-id="471af-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="471af-119">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="471af-119">Parameters:</span></span>
   
   * <span data-ttu-id="471af-120">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="471af-120">**-l (or --location)**.</span></span> <span data-ttu-id="471af-121">Región de Azure donde se creará la red virtual.</span><span class="sxs-lookup"><span data-stu-id="471af-121">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="471af-122">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="471af-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="471af-123">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="471af-123">**-n (or --name)**.</span></span> <span data-ttu-id="471af-124">Nombre del nuevo grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="471af-124">Name for the new NSG.</span></span> <span data-ttu-id="471af-125">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="471af-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="471af-126">Ejecute el siguiente comando para crear una ruta en la tabla de rutas para enviar todo el tráfico destinado a la subred back-end (192.168.2.0/24) a la máquina virtual **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="471af-126">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="471af-127">Salida:</span><span class="sxs-lookup"><span data-stu-id="471af-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="471af-128">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="471af-128">Parameters:</span></span>
   
   * <span data-ttu-id="471af-129">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="471af-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="471af-130">Nombre de la tabla de rutas a la que se agregará la ruta.</span><span class="sxs-lookup"><span data-stu-id="471af-130">Name of the route table where the route will be added.</span></span> <span data-ttu-id="471af-131">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="471af-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="471af-132">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="471af-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="471af-133">Prefijo de dirección de la subred a la que se destinan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="471af-133">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="471af-134">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="471af-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="471af-135">**-t (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="471af-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="471af-136">Tipo de objeto al que se enviará el tráfico.</span><span class="sxs-lookup"><span data-stu-id="471af-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="471af-137">Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="471af-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="471af-138">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="471af-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="471af-139">Dirección IP para el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="471af-139">IP address for next hop.</span></span> <span data-ttu-id="471af-140">En este escenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="471af-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="471af-141">Ejecute el siguiente comando para asociar la tabla de rutas que se ha creado a la subred **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="471af-141">Run the following command to associate the route table created with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="471af-142">Salida:</span><span class="sxs-lookup"><span data-stu-id="471af-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="471af-143">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="471af-143">Parameters:</span></span>
   
   * <span data-ttu-id="471af-144">**-t (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="471af-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="471af-145">Nombre de la red virtual donde se encuentra la subred.</span><span class="sxs-lookup"><span data-stu-id="471af-145">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="471af-146">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="471af-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="471af-147">**-n (o --subnet-name**.</span><span class="sxs-lookup"><span data-stu-id="471af-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="471af-148">Nombre de la subred a la que se agregará la tabla de rutas.</span><span class="sxs-lookup"><span data-stu-id="471af-148">Name of the subnet the route table will be added to.</span></span> <span data-ttu-id="471af-149">En este escenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="471af-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="471af-150">Creación de la ruta definida por el usuario para la subred back-end</span><span class="sxs-lookup"><span data-stu-id="471af-150">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="471af-151">Para crear la tabla de rutas y la ruta necesarias para la subred back-end según el escenario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="471af-151">To create the route table and route needed for the back-end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="471af-152">Ejecute el siguiente comando para crear una tabla de rutas para la subred back-end:</span><span class="sxs-lookup"><span data-stu-id="471af-152">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="471af-153">Ejecute el comando siguiente para crear una ruta en la tabla de rutas para enviar todo el tráfico destinado a la subred front-end (192.168.1.0/24) a la VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="471af-153">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="471af-154">Ejecute el siguiente comando para asociar la tabla de rutas a la subred **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="471af-154">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

