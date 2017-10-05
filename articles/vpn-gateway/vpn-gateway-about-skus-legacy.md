---
title: SKU de puerta de enlace de red virtual de Azure heredada | Microsoft Docs
description: SKU de puerta de enlace de red virtual antigua
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="b68ef-103">Trabajo con SKU de puerta de enlace de red virtual (SKU antiguas)</span><span class="sxs-lookup"><span data-stu-id="b68ef-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="b68ef-104">Este artículo contiene información sobre las SKU de puerta de enlace de red virtual heredadas (antiguas).</span><span class="sxs-lookup"><span data-stu-id="b68ef-104">This article contains information about the legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="b68ef-105">Las SKU heredadas siguen funcionando en ambos modelos de implementación para las puertas de enlace de VPN ya creadas.</span><span class="sxs-lookup"><span data-stu-id="b68ef-105">The legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="b68ef-106">Las puertas de enlace de VPN clásicas siguen usando las SKU heredadas para puertas de enlace existentes y para nuevas puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="b68ef-106">Classic VPN gateways continue to use the legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="b68ef-107">Al crear nuevas puertas de enlace de VPN de Resource Manager, use las nuevas SKU de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b68ef-107">When creating new Resource Manager VPN gateways, use the new gateway SKUs.</span></span> <span data-ttu-id="b68ef-108">Para más información sobre las nuevas SKU, vea [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="b68ef-108">For information about the new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="b68ef-109"><a name="gwsku"></a>SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="b68ef-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="b68ef-110"><a name="agg"></a>Rendimiento agregado estimado por SKU</span><span class="sxs-lookup"><span data-stu-id="b68ef-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="b68ef-111"><a name="config"></a>Configuraciones admitidas por el tipo de VPN y SKU</span><span class="sxs-lookup"><span data-stu-id="b68ef-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="b68ef-112"><a name="resize"></a>Cambio de tamaño de una puerta de enlace (cambio de SKU de puerta de enlace)</span><span class="sxs-lookup"><span data-stu-id="b68ef-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="b68ef-113">Puede cambiar el tamaño de una SKU de puerta de enlace dentro de la misma familia de la SKU.</span><span class="sxs-lookup"><span data-stu-id="b68ef-113">You can resize a gateway SKU within the same SKU family.</span></span> <span data-ttu-id="b68ef-114">Por ejemplo, si tiene una SKU Estándar, puede cambiar a una SKU HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="b68ef-114">For example, if you have a Standard SKU, you can resize to a HighPerformance SKU.</span></span> <span data-ttu-id="b68ef-115">No se puede cambiar el tamaño de las puertas de enlace de VPN entre las familias de SKU antiguas y las nuevas.</span><span class="sxs-lookup"><span data-stu-id="b68ef-115">You can't resize your VPN gateways between the old SKUs and the new SKU families.</span></span> <span data-ttu-id="b68ef-116">Por ejemplo, no se puede pasar de una SKU Estándar a una SKU VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="b68ef-116">For example, you can't go from a Standard SKU to a VpnGw2 SKU.</span></span> 

<span data-ttu-id="b68ef-117">Para cambiar el tamaño de una SKU de puerta de enlace del modelo de implementación clásica, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b68ef-117">To resize a gateway SKU for the classic deployment model, use the following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="b68ef-118">Para cambiar el tamaño de una SKU de puerta de enlace del modelo de implementación de Resource Manager, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b68ef-118">To resize a gateway SKU for the Resource Manager deployment model, use the following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="b68ef-119"><a name="migrate"></a>Migración a las nuevas SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="b68ef-119"><a name="migrate"></a>Migrate to the new gateway SKUs</span></span>

<span data-ttu-id="b68ef-120">Si está trabajando con el modelo de implementación de Resource Manager, puede migrar a las nuevas SKU de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="b68ef-120">If you are working with the Resource Manager deployment model, you can migrate to the new gateway SKUS.</span></span> <span data-ttu-id="b68ef-121">Si está trabajando con el modelo de implementación clásica, no puede migrar a las nuevas SKU, sino que debe seguir usando las SKU heredadas.</span><span class="sxs-lookup"><span data-stu-id="b68ef-121">If you are working with the classic deployment model, you can't migrate to the new SKUs and must instead continue to use the legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b68ef-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b68ef-122">Next steps</span></span>

<span data-ttu-id="b68ef-123">Para más información acerca de las nuevas SKU de puerta de enlace, consulte [SKU de puerta de enlace](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="b68ef-123">For more information about the new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="b68ef-124">Para más información sobre los valores de configuración, vea [Acerca de la configuración de la puerta de enlace de VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b68ef-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>