---
title: Control del enrutamiento y las aplicaciones virtuales con la CLI de Azure 1.0 | Microsoft Docs
description: "Obtenga información sobre cómo controlar el enrutamiento y las aplicaciones virtuales con la CLI de Azure 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="f9e7c-103">Creación de rutas definidas por el usuario (UDR) en la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f9e7c-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9e7c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9e7c-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="f9e7c-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f9e7c-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="f9e7c-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="f9e7c-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="f9e7c-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="f9e7c-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="f9e7c-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="f9e7c-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="f9e7c-109">Cree aplicaciones virtuales y enrutamiento personalizado con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f9e7c-110">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="f9e7c-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="f9e7c-111">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="f9e7c-112">[CLI de Azure 1.0](#Create-the-UDR-for-the-front-end-subnet): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="f9e7c-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f9e7c-113">[CLI de Azure 2.0](virtual-network-create-udr-arm-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="f9e7c-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="f9e7c-114">En los siguientes comandos de CLI de Azure de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="f9e7c-115">Si desea ejecutar los comandos tal y como aparecen en este documento, cree primero el entorno de prueba mediante la implementación de [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="f9e7c-116">Creación de la ruta definida por el usuario para la subred front-end</span><span class="sxs-lookup"><span data-stu-id="f9e7c-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="f9e7c-117">Para crear la tabla de rutas y la ruta necesaria para la subred front-end según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="f9e7c-118">Ejecute el comando siguiente para crear una tabla de rutas para la subred front-end:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="f9e7c-119">Salida:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="f9e7c-120">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-120">Parameters:</span></span>
   
   * <span data-ttu-id="f9e7c-121">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="f9e7c-122">Nombre del grupo de recursos donde se creará el UDR.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="f9e7c-123">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="f9e7c-124">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-124">**-l (or --location)**.</span></span> <span data-ttu-id="f9e7c-125">Región de Azure donde se creará el UDR nuevo.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="f9e7c-126">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="f9e7c-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-127">**-n (or --name)**.</span></span> <span data-ttu-id="f9e7c-128">Nombre del UDR nuevo.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-128">Name for the new UDR.</span></span> <span data-ttu-id="f9e7c-129">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="f9e7c-130">Ejecute el comando siguiente para crear una ruta en la tabla de rutas para enviar todo el tráfico destinado a la subred back-end (192.168.2.0/24) a la VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f9e7c-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="f9e7c-131">Salida:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="f9e7c-132">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-132">Parameters:</span></span>
   
   * <span data-ttu-id="f9e7c-133">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="f9e7c-134">Nombre de la tabla de rutas a la que se agregará la ruta.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="f9e7c-135">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="f9e7c-136">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="f9e7c-137">Prefijo de dirección de la subred a la que se destinan los paquetes.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="f9e7c-138">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="f9e7c-139">**-y (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="f9e7c-140">Tipo de objeto al que se enviará el tráfico.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="f9e7c-141">Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="f9e7c-142">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="f9e7c-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="f9e7c-143">Dirección IP para el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-143">IP address for next hop.</span></span> <span data-ttu-id="f9e7c-144">En este escenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="f9e7c-145">Ejecute el comando siguiente para asociar la tabla de rutas que se ha creado anteriormente a la subred **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="f9e7c-146">Salida:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="f9e7c-147">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-147">Parameters:</span></span>
   
   * <span data-ttu-id="f9e7c-148">**-e (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="f9e7c-149">Nombre de la red virtual donde se encuentra la subred.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="f9e7c-150">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="f9e7c-151">Creación de la ruta definida por el usuario para la subred back-end</span><span class="sxs-lookup"><span data-stu-id="f9e7c-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="f9e7c-152">Para crear la tabla de rutas y la ruta necesaria para la subred back-end según el escenario anterior, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="f9e7c-153">Ejecute el comando siguiente para crear una tabla de rutas para la subred back-end:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="f9e7c-154">Ejecute el comando siguiente para crear una ruta en la tabla de rutas para enviar todo el tráfico destinado a la subred front-end (192.168.1.0/24) a la VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f9e7c-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="f9e7c-155">Ejecute el comando siguiente para asociar la tabla de rutas a la subred **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="f9e7c-156">Habilitación del reenvío IP en FW1</span><span class="sxs-lookup"><span data-stu-id="f9e7c-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="f9e7c-157">Para habilitar el reenvío IP en la NIC que ha usado **FW1**, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="f9e7c-158">Ejecute el comando siguiente y observe el valor de **Habilitar reenvío IP**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="f9e7c-159">Se debe establecer en *false*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="f9e7c-160">Salida:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="f9e7c-161">Ejecute el comando siguiente para habilitar el reenvío IP:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="f9e7c-162">Salida:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="f9e7c-163">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="f9e7c-163">Parameters:</span></span>
   
   * <span data-ttu-id="f9e7c-164">**-f (o --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="f9e7c-165">*true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="f9e7c-165">*true* or *false*.</span></span>

