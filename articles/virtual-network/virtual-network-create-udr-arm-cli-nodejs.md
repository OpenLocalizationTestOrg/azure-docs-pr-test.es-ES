---
title: dispositivos de enrutamiento y virtual aaaControl utilizando Hola 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocontrol dispositivos de enrutamiento y virtual utilizando Hola 1.0 de CLI de Azure."
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
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="78ec1-103">Crear rutas definidas por el usuario (UDR) mediante Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="78ec1-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="78ec1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="78ec1-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="78ec1-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="78ec1-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="78ec1-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="78ec1-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="78ec1-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="78ec1-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="78ec1-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="78ec1-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="78ec1-109">Creación de una ruta personalizada y aparatos virtuales mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="78ec1-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="78ec1-110">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="78ec1-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="78ec1-111">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="78ec1-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="78ec1-112">[Azure 1.0 de CLI](#Create-the-UDR-for-the-front-end-subnet) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="78ec1-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="78ec1-113">[Azure 2.0 CLI](virtual-network-create-udr-arm-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="78ec1-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="78ec1-114">comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado basándose en el escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="78ec1-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="78ec1-115">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de hello implementando [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), haga clic en **implementar tooAzure**, reemplace los valores de parámetros predeterminados de Hola Si fuera necesario y siga las instrucciones de hello en Hola portal.</span><span class="sxs-lookup"><span data-stu-id="78ec1-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="78ec1-116">Crear hello UDR para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="78ec1-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="78ec1-117">tabla de rutas de hello toocreate y ruta necesarios para una subred de front-end de hello basándose en el escenario de hello anterior, siga los pasos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="78ec1-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="78ec1-118">Ejecute hello después comando toocreate una tabla de rutas de subred de front-end de hello:</span><span class="sxs-lookup"><span data-stu-id="78ec1-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="78ec1-119">Salida:</span><span class="sxs-lookup"><span data-stu-id="78ec1-119">Output:</span></span>
   
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
   
    <span data-ttu-id="78ec1-120">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="78ec1-120">Parameters:</span></span>
   
   * <span data-ttu-id="78ec1-121">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="78ec1-122">Nombre del grupo de recursos de Hola donde se creará hello UDR.</span><span class="sxs-lookup"><span data-stu-id="78ec1-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="78ec1-123">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="78ec1-124">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-124">**-l (or --location)**.</span></span> <span data-ttu-id="78ec1-125">Región de Azure donde hello UDR nuevo se creará.</span><span class="sxs-lookup"><span data-stu-id="78ec1-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="78ec1-126">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="78ec1-127">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-127">**-n (or --name)**.</span></span> <span data-ttu-id="78ec1-128">Nombre de hello UDR nuevo.</span><span class="sxs-lookup"><span data-stu-id="78ec1-128">Name for hello new UDR.</span></span> <span data-ttu-id="78ec1-129">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="78ec1-130">Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="78ec1-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="78ec1-131">Salida:</span><span class="sxs-lookup"><span data-stu-id="78ec1-131">Output:</span></span>
   
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
   
    <span data-ttu-id="78ec1-132">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="78ec1-132">Parameters:</span></span>
   
   * <span data-ttu-id="78ec1-133">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="78ec1-134">Nombre de tabla de rutas de Hola donde se agregará la ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="78ec1-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="78ec1-135">En este escenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="78ec1-136">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="78ec1-137">Prefijo de dirección de subred de Hola donde los paquetes destinados a.</span><span class="sxs-lookup"><span data-stu-id="78ec1-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="78ec1-138">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="78ec1-139">**-y (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="78ec1-140">Tipo de objeto al que se enviará el tráfico.</span><span class="sxs-lookup"><span data-stu-id="78ec1-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="78ec1-141">Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="78ec1-142">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="78ec1-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="78ec1-143">Dirección IP para el próximo salto.</span><span class="sxs-lookup"><span data-stu-id="78ec1-143">IP address for next hop.</span></span> <span data-ttu-id="78ec1-144">En este escenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="78ec1-145">Siguiente ejecución Hola comando tabla de rutas de hello tooassociate creada anteriormente con hello **front-end** subred:</span><span class="sxs-lookup"><span data-stu-id="78ec1-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="78ec1-146">Salida:</span><span class="sxs-lookup"><span data-stu-id="78ec1-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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
   
    <span data-ttu-id="78ec1-147">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="78ec1-147">Parameters:</span></span>
   
   * <span data-ttu-id="78ec1-148">**-e (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="78ec1-149">Nombre de red virtual donde se encuentra la subred de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="78ec1-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="78ec1-150">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="78ec1-151">Crear hello UDR de subred de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="78ec1-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="78ec1-152">Hola toocreate tabla de rutas y necesarios para la subred de back-end de hello en función de hello escenario anterior, Hola completa siguiendo los pasos de ruta:</span><span class="sxs-lookup"><span data-stu-id="78ec1-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="78ec1-153">Ejecute hello después comando toocreate una tabla de rutas de subred de back-end de hello:</span><span class="sxs-lookup"><span data-stu-id="78ec1-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="78ec1-154">Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="78ec1-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="78ec1-155">Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **back-end** subred:</span><span class="sxs-lookup"><span data-stu-id="78ec1-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="78ec1-156">Habilitación del reenvío IP en FW1</span><span class="sxs-lookup"><span data-stu-id="78ec1-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="78ec1-157">reenvío de IP tooenable Hola NIC que se utiliza por **FW1**completa Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="78ec1-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="78ec1-158">Ejecutar comando de Hola que sigue y observe el valor de Hola para **reenvío IP habilitar**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="78ec1-159">Se debe establecer demasiado*false*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="78ec1-160">Salida:</span><span class="sxs-lookup"><span data-stu-id="78ec1-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
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
2. <span data-ttu-id="78ec1-161">Ejecute hello después de reenvío de IP de tooenable de comando:</span><span class="sxs-lookup"><span data-stu-id="78ec1-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="78ec1-162">Salida:</span><span class="sxs-lookup"><span data-stu-id="78ec1-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
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
   
    <span data-ttu-id="78ec1-163">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="78ec1-163">Parameters:</span></span>
   
   * <span data-ttu-id="78ec1-164">**-f (o --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="78ec1-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="78ec1-165">*true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="78ec1-165">*true* or *false*.</span></span>

