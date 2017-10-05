---
title: "Creación de una red virtual (Azure PowerShell) | Microsoft Docs"
description: "Obtenga información sobre cómo crear una red virtual mediante PowerShell."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e7072ddf51570d46578111e2e392e3cbea53f2aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="65a2b-103">Creación de una red virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="65a2b-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="65a2b-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="65a2b-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="65a2b-105">Microsoft recomienda crear recursos mediante el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65a2b-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="65a2b-106">Para más información acerca de las diferencias entre los dos modelos, lea el artículo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Descripción de los modelos de implementación de Azure).</span><span class="sxs-lookup"><span data-stu-id="65a2b-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="65a2b-107">En este artículo se describe cómo crear una red virtual con el modelo de implementación de Resource Manager mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65a2b-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="65a2b-108">También puede crear una red virtual mediante Resource Manager con otras herramientas o crear una red virtual a través del modelo de implementación clásica seleccionando una opción diferente en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="65a2b-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="65a2b-109">Portal</span><span class="sxs-lookup"><span data-stu-id="65a2b-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="65a2b-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65a2b-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="65a2b-111">CLI</span><span class="sxs-lookup"><span data-stu-id="65a2b-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="65a2b-112">Plantilla</span><span class="sxs-lookup"><span data-stu-id="65a2b-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="65a2b-113">Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="65a2b-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="65a2b-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="65a2b-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="65a2b-115">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="65a2b-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="65a2b-116">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="65a2b-116">Create a virtual network</span></span>

<span data-ttu-id="65a2b-117">Para crear una red virtual mediante PowerShell, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="65a2b-117">To create a virtual network using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="65a2b-118">Instale y configure Azure PowerShell siguiendo los pasos del artículo [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65a2b-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="65a2b-119">Si es necesario, cree un nuevo grupo de recursos, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="65a2b-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="65a2b-120">En este escenario, cree un grupo de recursos denominado *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="65a2b-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="65a2b-121">Para más información acerca de los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65a2b-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="65a2b-122">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="65a2b-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="65a2b-123">Cree una red virtual denominada *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="65a2b-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="65a2b-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="65a2b-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="65a2b-125">Almacene el objeto de red virtual en una variable:</span><span class="sxs-lookup"><span data-stu-id="65a2b-125">Store the virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="65a2b-126">Puede combinar los pasos 3 y 4 si ejecuta `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="65a2b-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="65a2b-127">Agregue una subred a la nueva variable de red virtual:</span><span class="sxs-lookup"><span data-stu-id="65a2b-127">Add a subnet to the new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="65a2b-128">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="65a2b-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="65a2b-129">Repita el paso 5 anterior para cada subred que quiera crear.</span><span class="sxs-lookup"><span data-stu-id="65a2b-129">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="65a2b-130">El siguiente comando crea la subred *BackEnd* para el escenario:</span><span class="sxs-lookup"><span data-stu-id="65a2b-130">The following command creates the *BackEnd* subnet for the scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="65a2b-131">Aunque cree subredes, actualmente solo existen en la variable local que se usa para recuperar la red virtual creada en el paso 4 anterior.</span><span class="sxs-lookup"><span data-stu-id="65a2b-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="65a2b-132">Para guardar los cambios en Azure, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="65a2b-132">To save the changes to Azure, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="65a2b-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="65a2b-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="65a2b-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65a2b-134">Next steps</span></span>

<span data-ttu-id="65a2b-135">Aprenda a conectar:</span><span class="sxs-lookup"><span data-stu-id="65a2b-135">Learn how to connect:</span></span>

- <span data-ttu-id="65a2b-136">Una máquina virtual (VM) a una red virtual, para lo cual debería leer el artículo [Creación de una máquina virtual Windows](../virtual-machines/virtual-machines-windows-ps-create.md).</span><span class="sxs-lookup"><span data-stu-id="65a2b-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="65a2b-137">En lugar de crear una red virtual y la subred en los pasos de los artículos, puede seleccionar una red virtual y una subred a la que conectar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65a2b-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="65a2b-138">La red virtual a otras redes virtuales. Para ello, lea el artículo [Conexión de redes virtuales](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="65a2b-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="65a2b-139">La red virtual a una red local mediante una red privada virtual (VPN) de sitio a sitio o un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="65a2b-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="65a2b-140">Aprenda cómo hacerlo mediante los artículos [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) (Conexión de una red virtual a una red local mediante una VPN de sitio a sitio) y [Vinculación de una red virtual a un circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="65a2b-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
