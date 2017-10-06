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
# <a name="about-virtual-network-gateways-for-expressroute"></a>Acerca de las puertas de enlace de red virtual para ExpressRoute
Se utiliza una puerta de enlace de red virtual toosend el tráfico de red entre redes virtuales de Azure y las ubicaciones en local. Cuando configure una conexión ExpressRoute, debe crear y configurar una puerta de enlace de red virtual y una conexión de puerta de enlace de red virtual.

Al crear una puerta de enlace de red virtual, se especifican varios valores de configuración. Una de las opciones de hello necesario especifica si se utilizará la puerta de enlace de hello para el tráfico VPN de sitio a sitio o ExpressRoute. En el modelo de implementación del Administrador de recursos de hello, saludo es '-el GatewayType'.

Cuando se envía el tráfico de red en una conexión privada, se utiliza el tipo de puerta de enlace de hello 'ExpressRoute'. También es una puerta de enlace de ExpressRoute de tooas que se hace referencia. Cuando el tráfico de red se envía cifrado a través de Hola red pública de Internet, utilice el tipo de puerta de enlace de hello 'Vpn'. Se trata de una puerta de enlace VPN de tooas que se hace referencia. Las conexiones de sitio a sitio, de punto a sitio y de red virtual a red virtual utilizan una puerta de enlace de VPN.

Cada red virtual tiene una única puerta de enlace de red virtual por cada tipo de puerta de enlace. Por ejemplo, puede tener una puerta de enlace de una red virtual que use -GatewayType Vpn y otra que use -GatewayType ExpressRoute. En este artículo se centra en la puerta de enlace de red virtual de hello ExpressRoute.

## <a name="gwsku"></a>SKU de puerta de enlace
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Si desea que tooupgrade su tooa de puerta de enlace más eficaz SKU de puerta de enlace en la mayoría de los casos puede usar Hola cmdlet de PowerShell 'Resize-AzureRmVirtualNetworkGateway'. Esto funcionará para SKU de alto rendimiento y las actualizaciones tooStandard. Sin embargo, tendrá una tooupgrade toohello UltraPerformance SKU, puerta de enlace de toorecreate Hola.

### <a name="aggthroughput"></a>Rendimiento agregado estimado por SKU de puerta de enlace
Hello tabla siguiente muestran tipos de puerta de enlace de Hola y el rendimiento agregado estimado Hola. Esta tabla aplica tooboth Hola Administrador de recursos y modelos de implementación clásica.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Rendimiento de la aplicación depende de varios factores, como la latencia de hello-to-end, y número de Hola de tráfico flujos Hola aplicación abre. números de Hola Hola tabla representan hello como límite superior que la aplicación hello pueda theorectically lograr en un entorno ideal. 
> 
>

## <a name="resources"></a>API de REST y cmdlets de PowerShell
Para recursos técnicos adicionales y requisitos de sintaxis específica cuando se usa la API de REST y cmdlets de PowerShell para las configuraciones de puerta de enlace de red virtual, vea Hola siguientes páginas:

| **Clásico** | **Resource Manager** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [API DE REST](https://msdn.microsoft.com/library/jj154113.aspx) |[API DE REST](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Pasos siguientes
Consulte [Información técnica de ExpressRoute](expressroute-introduction.md) para más información sobre configuraciones de conexión disponibles. 

