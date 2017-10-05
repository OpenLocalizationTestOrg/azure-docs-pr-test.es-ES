---
title: Acerca de las puertas de enlace de red virtual de ExpressRoute | Microsoft Docs
description: Conozca sobre las puertas de enlace de red virtual para ExpressRoute.
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="f9456-103">Acerca de las puertas de enlace de red virtual para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f9456-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="f9456-104">Una puerta de enlace de red virtual se usa para enviar tráfico de red entre redes virtuales y ubicaciones locales de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9456-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="f9456-105">Cuando configure una conexión ExpressRoute, debe crear y configurar una puerta de enlace de red virtual y una conexión de puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="f9456-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="f9456-106">Al crear una puerta de enlace de red virtual, se especifican varios valores de configuración.</span><span class="sxs-lookup"><span data-stu-id="f9456-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="f9456-107">Uno de los valores de configuración necesarios especifica si la puerta de enlace se usará para el tráfico de Express Route o de VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="f9456-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="f9456-108">En el modelo de implementación de Resource Manager, el valor es '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="f9456-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="f9456-109">Cuando se envíe el tráfico de red en una conexión privada, use el tipo de puerta de enlace "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="f9456-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="f9456-110">Esto también se conoce como puerta de enlace de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9456-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="f9456-111">Cuando envíe el tráfico de red cifrado a través de una conexión a Internet pública, use el tipo de puerta de enlace "VPN".</span><span class="sxs-lookup"><span data-stu-id="f9456-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="f9456-112">Esto se conoce como puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="f9456-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="f9456-113">Las conexiones de sitio a sitio, de punto a sitio y de red virtual a red virtual utilizan una puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="f9456-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="f9456-114">Cada red virtual tiene una única puerta de enlace de red virtual por cada tipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f9456-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="f9456-115">Por ejemplo, puede tener una puerta de enlace de una red virtual que use -GatewayType Vpn y otra que use -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9456-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="f9456-116">Este artículo se centra en la puerta de enlace de red virtual de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9456-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="f9456-117"><a name="gwsku"></a>SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="f9456-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="f9456-118">Si desea actualizar la puerta de enlace a una SKU de puerta de enlace más eficaz, en la mayoría de los casos puede usar el cmdlet de PowerShell Resize-AzureRmVirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="f9456-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="f9456-119">Esto funcionará para las actualizaciones de SKU Standard y HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="f9456-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="f9456-120">Sin embargo, para actualizar a la SKU UltraPerformance, debe volver a crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f9456-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="f9456-121"><a name="aggthroughput"></a>Rendimiento agregado estimado por SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="f9456-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="f9456-122">En la tabla siguiente se muestran los tipos de puerta de enlace y el rendimiento agregado estimado.</span><span class="sxs-lookup"><span data-stu-id="f9456-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="f9456-123">Esta tabla se aplica a los modelos de implementación del Administrador de recursos y clásico.</span><span class="sxs-lookup"><span data-stu-id="f9456-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="f9456-124">El rendimiento de la aplicación depende de varios factores, como la latencia de extremo a extremo y el número de flujos de tráfico de abre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9456-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="f9456-125">Los números de la tabla representan el límite superior que teóricamente la aplicación puede alcanzar en un entorno ideal.</span><span class="sxs-lookup"><span data-stu-id="f9456-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="f9456-126"><a name="resources"></a>API de REST y cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9456-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="f9456-127">Para más información sobre recursos técnicos y requisitos de sintaxis específicos al usar API de REST y cmdlets de PowerShell para configuraciones de puerta de enlace de red virtual, consulte las páginas siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9456-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="f9456-128">**Clásico**</span><span class="sxs-lookup"><span data-stu-id="f9456-128">**Classic**</span></span> | <span data-ttu-id="f9456-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="f9456-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="f9456-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9456-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="f9456-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9456-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="f9456-132">API DE REST</span><span class="sxs-lookup"><span data-stu-id="f9456-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="f9456-133">API DE REST</span><span class="sxs-lookup"><span data-stu-id="f9456-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="f9456-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9456-134">Next steps</span></span>
<span data-ttu-id="f9456-135">Consulte [Información técnica de ExpressRoute](expressroute-introduction.md) para más información sobre configuraciones de conexión disponibles.</span><span class="sxs-lookup"><span data-stu-id="f9456-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

