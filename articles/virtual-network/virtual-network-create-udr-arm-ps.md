---
title: 'dispositivos de enrutamiento y virtual aaaControl de Azure: PowerShell | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toocontrol aparatos de enrutamiento y virtual mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="8de9f-103">Creación de rutas definidas por el usuario (UDR) con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8de9f-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8de9f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8de9f-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="8de9f-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8de9f-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="8de9f-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="8de9f-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="8de9f-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="8de9f-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="8de9f-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="8de9f-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="8de9f-109">Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico.</span><span class="sxs-lookup"><span data-stu-id="8de9f-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="8de9f-110">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8de9f-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="8de9f-111">Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8de9f-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="8de9f-112">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8de9f-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="8de9f-113">También puede [crear UDRs en el modelo de implementación clásica de hello](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8de9f-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="8de9f-114">ejemplo de Hola PowerShell comandos siguientes esperan un entorno simple ya creado se basa en escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="8de9f-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="8de9f-115">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de hello implementando [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), haga clic en **implementar tooAzure**, reemplace los valores de parámetros predeterminados de Hola Si fuera necesario y siga las instrucciones de hello en Hola portal.</span><span class="sxs-lookup"><span data-stu-id="8de9f-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="8de9f-116">Crear hello UDR para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="8de9f-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="8de9f-117">tabla de rutas de hello toocreate y ruta sea necesario para la subred de front-end de hello basándose en escenario de hello anteriormente, Hola completa siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="8de9f-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="8de9f-118">Crear un toosend ruta usa todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toobe enruta toohello **FW1** dispositivo virtual (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="8de9f-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="8de9f-119">Crear una tabla de ruta denominada **UDR-front-end** en hello **oesteee. UU.** una región que contiene la ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8de9f-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="8de9f-120">Cree una variable que contenga Hola donde es la subred de Hola de red virtual.</span><span class="sxs-lookup"><span data-stu-id="8de9f-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="8de9f-121">En nuestro escenario, hello red virtual se denomina **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="8de9f-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="8de9f-122">Tabla de rutas de hello asocia creada anteriormente toohello **front-end** subred.</span><span class="sxs-lookup"><span data-stu-id="8de9f-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="8de9f-123">resultado de Hello en comando hello anterior muestra contenido hello para el objeto de configuración de red virtual de hello, que solo existe en el equipo de Hola donde se ejecuta PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8de9f-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="8de9f-124">Necesita hello toorun **AzureVirtualNetwork conjunto** cmdlet toosave estos tooAzure de configuración.</span><span class="sxs-lookup"><span data-stu-id="8de9f-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="8de9f-125">Guarde la nueva configuración de subred hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="8de9f-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="8de9f-126">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="8de9f-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="8de9f-127">Crear hello UDR de subred de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="8de9f-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="8de9f-128">tabla de rutas de hello toocreate y ruta necesarios para la subred de back-end de hello en función de hello escenario anterior, siga los pasos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="8de9f-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="8de9f-129">Crear un toosend ruta usa todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toobe enrutan toohello **FW1** dispositivo virtual (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="8de9f-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="8de9f-130">Crear una tabla de ruta denominada **UDR-back-end** en hello **oesteee** una región que contiene la ruta de hello creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8de9f-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="8de9f-131">Tabla de rutas de hello asocia creada anteriormente toohello **back-end** subred.</span><span class="sxs-lookup"><span data-stu-id="8de9f-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="8de9f-132">Guarde la nueva configuración de subred hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="8de9f-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="8de9f-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="8de9f-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="8de9f-134">Habilitación del reenvío IP en FW1</span><span class="sxs-lookup"><span data-stu-id="8de9f-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="8de9f-135">reenvío de IP tooenable Hola NIC que se utiliza por **FW1**, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="8de9f-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="8de9f-136">Cree una variable que contiene la configuración de Hola de hello NIC que se utiliza por FW1.</span><span class="sxs-lookup"><span data-stu-id="8de9f-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="8de9f-137">En nuestro escenario, hello NIC se denomina **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="8de9f-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="8de9f-138">Habilitar el reenvío IP y guardar la configuración de NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="8de9f-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="8de9f-139">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="8de9f-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

