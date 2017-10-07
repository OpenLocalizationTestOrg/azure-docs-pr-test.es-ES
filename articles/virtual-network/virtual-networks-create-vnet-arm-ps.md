---
title: aaaCreate una red virtual - PowerShell de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate a virtual de red con PowerShell."
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
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="b82ea-103">Creación de una red virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b82ea-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="b82ea-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="b82ea-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="b82ea-105">Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b82ea-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="b82ea-106">Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="b82ea-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="b82ea-107">Este artículo explica cómo toocreate una red virtual a través de la implementación del Administrador de recursos de hello modelar con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b82ea-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="b82ea-108">También puede crear una red virtual mediante el Administrador de recursos con otras herramientas o crear una red virtual a través del modelo de implementación clásica de hello seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="b82ea-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b82ea-109">Portal</span><span class="sxs-lookup"><span data-stu-id="b82ea-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="b82ea-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b82ea-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="b82ea-111">CLI</span><span class="sxs-lookup"><span data-stu-id="b82ea-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="b82ea-112">Plantilla</span><span class="sxs-lookup"><span data-stu-id="b82ea-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="b82ea-113">Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="b82ea-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="b82ea-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="b82ea-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="b82ea-115">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="b82ea-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="b82ea-116">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="b82ea-116">Create a virtual network</span></span>

<span data-ttu-id="b82ea-117">toocreate una red virtual con PowerShell, Hola completa siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="b82ea-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="b82ea-118">Instalar y configurar Azure PowerShell, siguiendo los pasos de Hola Hola [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="b82ea-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="b82ea-119">Si es necesario, cree un nuevo grupo de recursos, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b82ea-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="b82ea-120">En este escenario, cree un grupo de recursos denominado *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="b82ea-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="b82ea-121">Para más información acerca de los grupos de recursos, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b82ea-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="b82ea-122">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="b82ea-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="b82ea-123">Cree una red virtual denominada *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="b82ea-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="b82ea-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="b82ea-124">Expected output:</span></span>

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
4. <span data-ttu-id="b82ea-125">Almacenar objetos de red virtual de hello en una variable:</span><span class="sxs-lookup"><span data-stu-id="b82ea-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="b82ea-126">Puede combinar los pasos 3 y 4 si ejecuta `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="b82ea-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="b82ea-127">Agregue una variable de red virtual nueva subred toohello:</span><span class="sxs-lookup"><span data-stu-id="b82ea-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="b82ea-128">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="b82ea-128">Expected output:</span></span>
   
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

6. <span data-ttu-id="b82ea-129">Repita el paso 5 anterior para cada subred que desee toocreate.</span><span class="sxs-lookup"><span data-stu-id="b82ea-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="b82ea-130">Hello siguiente comando crea hello *back-end* subred para el escenario de hello:</span><span class="sxs-lookup"><span data-stu-id="b82ea-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="b82ea-131">Aunque se crean subredes, actualmente solo existen en Hola tooretrieve uso de variable local Hola red virtual se crea en el paso 4 anterior.</span><span class="sxs-lookup"><span data-stu-id="b82ea-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="b82ea-132">tooAzure toosave Hola cambios, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="b82ea-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="b82ea-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="b82ea-133">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="b82ea-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b82ea-134">Next steps</span></span>

<span data-ttu-id="b82ea-135">Obtenga información acerca de cómo tooconnect:</span><span class="sxs-lookup"><span data-stu-id="b82ea-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="b82ea-136">Una red virtual de máquina virtual (VM) tooa leyendo hello [crear una VM de Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="b82ea-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="b82ea-137">En lugar de crear una red virtual y la subred en los pasos de Hola de artículos de hello, puede seleccionar una red virtual existente y la subred tooconnect una máquina virtual a.</span><span class="sxs-lookup"><span data-stu-id="b82ea-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="b82ea-138">Hola redes virtuales de red virtual tooother leyendo hello [conectar redes virtuales](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="b82ea-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="b82ea-139">Hola tooan de red virtual local de la red mediante una red privada virtual (VPN) de sitio a sitio o el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b82ea-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="b82ea-140">Obtenga información acerca de cómo leyendo hello [conectar una red de red virtual tooan local mediante una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) y [vincular un circuito de ExpressRoute de red virtual tooan](../expressroute/expressroute-howto-linkvnet-arm.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="b82ea-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
