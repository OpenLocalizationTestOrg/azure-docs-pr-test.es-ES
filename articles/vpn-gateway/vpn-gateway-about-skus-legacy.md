---
title: puerta de enlace de red virtual de Azure de aaaLegacy SKU | Documentos de Microsoft
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
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="45b98-103">Trabajo con SKU de puerta de enlace de red virtual (SKU antiguas)</span><span class="sxs-lookup"><span data-stu-id="45b98-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="45b98-104">Este artículo contiene información sobre Hola heredado (antiguo) red virtual puerta de enlace de SKU.</span><span class="sxs-lookup"><span data-stu-id="45b98-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="45b98-105">heredado de Hello SKU seguirán funcionan en ambos modelos de implementación para las puertas de enlace VPN que se han creado.</span><span class="sxs-lookup"><span data-stu-id="45b98-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="45b98-106">Puertas de enlace VPN clásicos continuar toouse Hola SKU heredadas, las puertas de enlace existentes tanto para nuevas puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="45b98-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="45b98-107">Al crear nueva de administrador de recursos de VPN puertas de enlace, use Hola nueva puerta de enlace SKU.</span><span class="sxs-lookup"><span data-stu-id="45b98-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="45b98-108">Para obtener información acerca de hello SKU nueva, vea [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="45b98-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="45b98-109"><a name="gwsku"></a>SKU de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="45b98-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="45b98-110"><a name="agg"></a>Rendimiento agregado estimado por SKU</span><span class="sxs-lookup"><span data-stu-id="45b98-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="45b98-111"><a name="config"></a>Configuraciones admitidas por el tipo de VPN y SKU</span><span class="sxs-lookup"><span data-stu-id="45b98-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="45b98-112"><a name="resize"></a>Cambio de tamaño de una puerta de enlace (cambio de SKU de puerta de enlace)</span><span class="sxs-lookup"><span data-stu-id="45b98-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="45b98-113">Puede cambiar el tamaño de un SKU de puerta de enlace en hello misma familia SKU.</span><span class="sxs-lookup"><span data-stu-id="45b98-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="45b98-114">Por ejemplo, si tiene una SKU estándar, puede cambiar el tamaño de tooa HighPerformance SKU.</span><span class="sxs-lookup"><span data-stu-id="45b98-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="45b98-115">No se puede cambiar el tamaño de la VPN de puertas de enlace entre SKU antiguas de Hola y Hola nuevas familias de SKU.</span><span class="sxs-lookup"><span data-stu-id="45b98-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="45b98-116">Por ejemplo, no se puede ir desde un tooa SKU estándar VpnGw2 SKU.</span><span class="sxs-lookup"><span data-stu-id="45b98-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="45b98-117">tooresize una SKU de puerta de enlace para el modelo de implementación clásica de hello, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="45b98-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="45b98-118">tooresize un SKU de puerta de enlace de hello modelo de implementación del Administrador de recursos, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="45b98-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="45b98-119"><a name="migrate"></a>Migrar toohello nueva puerta de enlace SKU</span><span class="sxs-lookup"><span data-stu-id="45b98-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="45b98-120">Si está trabajando con el modelo de implementación del Administrador de recursos de hello, puede migrar toohello nueva puerta de enlace SKU.</span><span class="sxs-lookup"><span data-stu-id="45b98-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="45b98-121">Si está trabajando con el modelo de implementación clásica de hello, no se pueden migrar toohello SKU nuevo y en su lugar, debe seguir toouse Hola SKU heredadas.</span><span class="sxs-lookup"><span data-stu-id="45b98-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="45b98-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45b98-122">Next steps</span></span>

<span data-ttu-id="45b98-123">Para obtener más información acerca de Hola nuevo SKU de puerta de enlace, vea [SKU de puerta de enlace](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="45b98-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="45b98-124">Para más información sobre los valores de configuración, vea [Acerca de la configuración de la puerta de enlace de VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="45b98-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>