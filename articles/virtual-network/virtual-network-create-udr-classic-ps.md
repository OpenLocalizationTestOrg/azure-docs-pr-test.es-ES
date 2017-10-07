---
title: "aaaControl enrutamiento en una red Virtual de Azure - PowerShell - clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocontrol enrutamiento en redes virtuales mediante PowerShell | Clásico"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="74e58-103">Control del enrutamiento y uso de aplicaciones virtuales (clásico) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="74e58-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="74e58-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="74e58-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="74e58-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="74e58-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="74e58-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="74e58-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="74e58-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="74e58-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="74e58-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="74e58-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="74e58-109">Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico.</span><span class="sxs-lookup"><span data-stu-id="74e58-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="74e58-110">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="74e58-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="74e58-111">Puede ver la documentación de Hola para distintas herramientas seleccionando una opción de la parte superior de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="74e58-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="74e58-112">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="74e58-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="74e58-113">ejemplo Hello Azure PowerShell siguientes comandos de esperan un entorno simple ya creado se basa en el escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="74e58-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="74e58-114">Si desea toorun comandos de hello, que se muestran en este documento, crear se muestra en el entorno de hello [crear una red virtual (clásica) mediante PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="74e58-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="74e58-115">Crear hello UDR para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="74e58-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="74e58-116">tabla de rutas de hello toocreate y ruta necesarios para una subred de front-end de hello basándose en el escenario de hello anterior, siga los pasos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="74e58-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="74e58-117">Ejecute hello después comando toocreate una tabla de rutas de subred de front-end de hello:</span><span class="sxs-lookup"><span data-stu-id="74e58-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="74e58-118">Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="74e58-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="74e58-119">Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **front-end** subred:</span><span class="sxs-lookup"><span data-stu-id="74e58-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="74e58-120">Crear hello UDR de subred de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="74e58-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="74e58-121">tabla de rutas de hello toocreate y ruta sea necesario para la copia de Hola finalizar una subred basándose en el escenario de hello, siga Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="74e58-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="74e58-122">Ejecute hello después comando toocreate una tabla de rutas de subred de back-end de hello:</span><span class="sxs-lookup"><span data-stu-id="74e58-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="74e58-123">Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="74e58-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="74e58-124">Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **back-end** subred:</span><span class="sxs-lookup"><span data-stu-id="74e58-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="74e58-125">Habilitar el reenvío IP en hello FW1 VM</span><span class="sxs-lookup"><span data-stu-id="74e58-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="74e58-126">reenvío de IP tooenable en hello FW1 VM, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="74e58-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="74e58-127">Ejecute hello siguiendo el estado del comando toocheck Hola de reenvío IP:</span><span class="sxs-lookup"><span data-stu-id="74e58-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="74e58-128">Siguiente ejecución Hola comando tooenable el reenvío IP para hello *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="74e58-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
