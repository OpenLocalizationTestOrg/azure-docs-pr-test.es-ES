---
title: puertas de enlace de red virtual de ExpressRoute de aaaAbout | Documentos de Microsoft
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
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="d03e3-103">Acerca de las puertas de enlace de red virtual para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d03e3-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="d03e3-104">Se utiliza una puerta de enlace de red virtual toosend el tráfico de red entre redes virtuales de Azure y las ubicaciones en local.</span><span class="sxs-lookup"><span data-stu-id="d03e3-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="d03e3-105">Cuando configure una conexión ExpressRoute, debe crear y configurar una puerta de enlace de red virtual y una conexión de puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="d03e3-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="d03e3-106">Al crear una puerta de enlace de red virtual, se especifican varios valores de configuración.</span><span class="sxs-lookup"><span data-stu-id="d03e3-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="d03e3-107">Una de las opciones de hello necesario especifica si se utilizará la puerta de enlace de hello para el tráfico VPN de sitio a sitio o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d03e3-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="d03e3-108">En el modelo de implementación del Administrador de recursos de hello, saludo es '-el GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="d03e3-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="d03e3-109">Cuando se envía el tráfico de red en una conexión privada, se utiliza el tipo de puerta de enlace de hello 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="d03e3-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="d03e3-110">También es una puerta de enlace de ExpressRoute de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="d03e3-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="d03e3-111">Cuando el tráfico de red se envía cifrado a través de Hola red pública de Internet, utilice el tipo de puerta de enlace de hello 'Vpn'.</span><span class="sxs-lookup"><span data-stu-id="d03e3-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="d03e3-112">Se trata de una puerta de enlace VPN de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="d03e3-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="d03e3-113">Las conexiones de sitio a sitio, de punto a sitio y de red virtual a red virtual utilizan una puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="d03e3-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="d03e3-114">Cada red virtual tiene una única puerta de enlace de red virtual por cada tipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d03e3-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="d03e3-115">Por ejemplo, puede tener una puerta de enlace de una red virtual que use -GatewayType Vpn y otra que use -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d03e3-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="d03e3-116">En este artículo se centra en la puerta de enlace de red virtual de hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d03e3-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="d03e3-117"><a name="gwsku"></a>SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="d03e3-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="d03e3-118">Si desea que tooupgrade su tooa de puerta de enlace más eficaz SKU de puerta de enlace en la mayoría de los casos puede usar Hola cmdlet de PowerShell 'Resize-AzureRmVirtualNetworkGateway'.</span><span class="sxs-lookup"><span data-stu-id="d03e3-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="d03e3-119">Esto funcionará para SKU de alto rendimiento y las actualizaciones tooStandard.</span><span class="sxs-lookup"><span data-stu-id="d03e3-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="d03e3-120">Sin embargo, tendrá una tooupgrade toohello UltraPerformance SKU, puerta de enlace de toorecreate Hola.</span><span class="sxs-lookup"><span data-stu-id="d03e3-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="d03e3-121"><a name="aggthroughput"></a>Rendimiento agregado estimado por SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="d03e3-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="d03e3-122">Hello tabla siguiente muestran tipos de puerta de enlace de Hola y el rendimiento agregado estimado Hola.</span><span class="sxs-lookup"><span data-stu-id="d03e3-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="d03e3-123">Esta tabla aplica tooboth Hola Administrador de recursos y modelos de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="d03e3-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="d03e3-124">Rendimiento de la aplicación depende de varios factores, como la latencia de hello-to-end, y número de Hola de tráfico flujos Hola aplicación abre.</span><span class="sxs-lookup"><span data-stu-id="d03e3-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="d03e3-125">números de Hola Hola tabla representan hello como límite superior que la aplicación hello pueda theorectically lograr en un entorno ideal.</span><span class="sxs-lookup"><span data-stu-id="d03e3-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="d03e3-126"><a name="resources"></a>API de REST y cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d03e3-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="d03e3-127">Para recursos técnicos adicionales y requisitos de sintaxis específica cuando se usa la API de REST y cmdlets de PowerShell para las configuraciones de puerta de enlace de red virtual, vea Hola siguientes páginas:</span><span class="sxs-lookup"><span data-stu-id="d03e3-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="d03e3-128">**Clásico**</span><span class="sxs-lookup"><span data-stu-id="d03e3-128">**Classic**</span></span> | <span data-ttu-id="d03e3-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="d03e3-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="d03e3-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d03e3-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="d03e3-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d03e3-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="d03e3-132">API DE REST</span><span class="sxs-lookup"><span data-stu-id="d03e3-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="d03e3-133">API DE REST</span><span class="sxs-lookup"><span data-stu-id="d03e3-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="d03e3-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d03e3-134">Next steps</span></span>
<span data-ttu-id="d03e3-135">Consulte [Información técnica de ExpressRoute](expressroute-introduction.md) para más información sobre configuraciones de conexión disponibles.</span><span class="sxs-lookup"><span data-stu-id="d03e3-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

