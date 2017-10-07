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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Trabajo con SKU de puerta de enlace de red virtual (SKU antiguas)

Este artículo contiene información sobre Hola heredado (antiguo) red virtual puerta de enlace de SKU. heredado de Hello SKU seguirán funcionan en ambos modelos de implementación para las puertas de enlace VPN que se han creado. Puertas de enlace VPN clásicos continuar toouse Hola SKU heredadas, las puertas de enlace existentes tanto para nuevas puertas de enlace. Al crear nueva de administrador de recursos de VPN puertas de enlace, use Hola nueva puerta de enlace SKU. Para obtener información acerca de hello SKU nueva, vea [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>SKU de puerta de enlace

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>Rendimiento agregado estimado por SKU

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>Configuraciones admitidas por el tipo de VPN y SKU

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Cambio de tamaño de una puerta de enlace (cambio de SKU de puerta de enlace)

Puede cambiar el tamaño de un SKU de puerta de enlace en hello misma familia SKU. Por ejemplo, si tiene una SKU estándar, puede cambiar el tamaño de tooa HighPerformance SKU. No se puede cambiar el tamaño de la VPN de puertas de enlace entre SKU antiguas de Hola y Hola nuevas familias de SKU. Por ejemplo, no se puede ir desde un tooa SKU estándar VpnGw2 SKU. 

tooresize una SKU de puerta de enlace para el modelo de implementación clásica de hello, Hola de uso siguiente comando:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize un SKU de puerta de enlace de hello modelo de implementación del Administrador de recursos, utilice Hola siguiente comando:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Migrar toohello nueva puerta de enlace SKU

Si está trabajando con el modelo de implementación del Administrador de recursos de hello, puede migrar toohello nueva puerta de enlace SKU. Si está trabajando con el modelo de implementación clásica de hello, no se pueden migrar toohello SKU nuevo y en su lugar, debe seguir toouse Hola SKU heredadas.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de Hola nuevo SKU de puerta de enlace, vea [SKU de puerta de enlace](vpn-gateway-about-vpngateways.md#gwsku).

Para más información sobre los valores de configuración, vea [Acerca de la configuración de la puerta de enlace de VPN](vpn-gateway-about-vpn-gateway-settings.md).