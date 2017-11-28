---
title: 'Control del enrutamiento y las aplicaciones virtuales en Azure: PowerShell | Microsoft Docs'
description: "Obtenga información sobre cómo controlar el enrutamiento y las aplicaciones virtuales con PowerShell."
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
ms.openlocfilehash: 3ab24f193c74449ae7414b4ea0675c0aae0211f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="51ab1-103">Creación de rutas definidas por el usuario (UDR) con PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ab1-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="51ab1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ab1-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="51ab1-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="51ab1-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="51ab1-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="51ab1-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="51ab1-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="51ab1-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="51ab1-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="51ab1-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="51ab1-109">Antes de trabajar con recursos de Azure, es importante comprender que Azure tiene actualmente dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="51ab1-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="51ab1-110">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ab1-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="51ab1-111">Puede ver la documentación de las distintas herramientas haciendo clic en las fichas en la parte superior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="51ab1-111">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span>
>

<span data-ttu-id="51ab1-112">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="51ab1-112">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="51ab1-113">También puede [crear rutas definidas por el usuario en el modelo de implementación clásico](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="51ab1-113">You can also [create UDRs in the classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="51ab1-114">En los siguientes comandos de PowerShell de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="51ab1-114">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="51ab1-115">Si desea ejecutar los comandos tal y como aparecen en este documento, cree primero el entorno de prueba mediante la implementación de [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="51ab1-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="51ab1-116">Creación de la ruta definida por el usuario para la subred front-end</span><span class="sxs-lookup"><span data-stu-id="51ab1-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="51ab1-117">Para crear la tabla de rutas y la ruta necesaria para la subred front-end según el escenario anterior, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="51ab1-117">To create the route table and route needed for the front-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="51ab1-118">Cree una ruta que se use para enviar todo el tráfico destinado a la subred back-end (192.168.2.0/24) para enrutarse a la aplicación virtual **FW1** (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="51ab1-118">Create a route used to send all traffic destined to the back-end subnet (192.168.2.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="51ab1-119">Cree una tabla de rutas denominada **UDR-FrontEnd** en la región **westus** que contenga la ruta.</span><span class="sxs-lookup"><span data-stu-id="51ab1-119">Create a route table named **UDR-FrontEnd** in the **westus** region that contains the route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="51ab1-120">Cree una variable que contenga la red virtual donde está la subred.</span><span class="sxs-lookup"><span data-stu-id="51ab1-120">Create a variable that contains the VNet where the subnet is.</span></span> <span data-ttu-id="51ab1-121">En nuestro escenario, la red virtual se llama **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="51ab1-121">In our scenario, the VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="51ab1-122">Asocie la tabla de ruta creada anteriormente a la subred **FrontEnd** .</span><span class="sxs-lookup"><span data-stu-id="51ab1-122">Associate the route table created above to the **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="51ab1-123">La salida del comando anterior muestra el contenido del objeto de configuración de red virtual, que solo existe en el equipo donde se ejecuta PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51ab1-123">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="51ab1-124">Debe ejecutar el cmdlet **AzureVirtualNetwork Set** para guardar esta configuración en Azure.</span><span class="sxs-lookup"><span data-stu-id="51ab1-124">You need to run the **Set-AzureVirtualNetwork** cmdlet to save these settings to Azure.</span></span>
    > 

5. <span data-ttu-id="51ab1-125">Guarde la nueva configuración de subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ab1-125">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="51ab1-126">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="51ab1-126">Expected output:</span></span>
   
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

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="51ab1-127">Creación de la ruta definida por el usuario para la subred back-end</span><span class="sxs-lookup"><span data-stu-id="51ab1-127">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="51ab1-128">Para crear la tabla de rutas y la ruta necesaria para la subred back-end según el escenario anterior, siga los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="51ab1-128">To create the route table and route needed for the back-end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="51ab1-129">Cree una ruta que se use para enviar todo el tráfico destinado a la subred front-end (192.168.1.0/24) para enrutarse a la aplicación virtual **FW1** (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="51ab1-129">Create a route used to send all traffic destined to the front-end subnet (192.168.1.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="51ab1-130">Cree una tabla de rutas denominada **UDR-BackEnd** en la región **uswest** que contenga la ruta que se ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="51ab1-130">Create a route table named **UDR-BackEnd** in the **uswest** region that contains the route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="51ab1-131">Asocie la tabla de ruta creada anteriormente a la subred **BackEnd** .</span><span class="sxs-lookup"><span data-stu-id="51ab1-131">Associate the route table created above to the **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="51ab1-132">Guarde la nueva configuración de subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="51ab1-132">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="51ab1-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="51ab1-133">Expected output:</span></span>
   
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

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="51ab1-134">Habilitación del reenvío IP en FW1</span><span class="sxs-lookup"><span data-stu-id="51ab1-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="51ab1-135">Para habilitar el reenvío IP en la NIC usada por **FW1**, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="51ab1-135">To enable IP forwarding in the NIC used by **FW1**, follow the steps below.</span></span>

1. <span data-ttu-id="51ab1-136">Cree una variable que contenga la configuración de la NIC usada por FW1.</span><span class="sxs-lookup"><span data-stu-id="51ab1-136">Create a variable that contains the settings for the NIC used by FW1.</span></span> <span data-ttu-id="51ab1-137">En nuestro escenario, la NIC se llama **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="51ab1-137">In our scenario, the NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="51ab1-138">Habilite el reenvío IP y guarde la configuración de NIC.</span><span class="sxs-lookup"><span data-stu-id="51ab1-138">Enable IP forwarding, and save the NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="51ab1-139">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="51ab1-139">Expected output:</span></span>
   
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

