---
title: "Modelos de conectividad de ExpressRoute: conectar tooMicrosoft Azure a través de proveedores de servicios de red, los intercambios y los proveedores de Ethernet | Documentos de Microsoft"
description: "En este artículo se describe diferentes modos de Hola de conectividad entre la red del cliente de Hola y servicios de Microsoft Azure, Office 365 y Dynamics 365. Los clientes pueden usar proveedores MPLS, intercambios de nube y proveedores de Ethernet."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>Modelos de conectividad de ExpressRoute
Puede crear una conexión entre su red local y Hola nube de Microsoft de tres maneras diferentes, [CloudExchange colocalización](#CloudExchange), [conexión Ethernet de punto a punto](#Ethernet)y [(IPVPN) y para cualquier conexión](#IPVPN). Los proveedores de conectividad pueden ofrecer uno o varios modelos de conectividad. Puede trabajar con el modelo de Hola de toopick de proveedor de conectividad que más le convenga.
<br><br>

![Diagrama de modelo de conectividad de ExpressRoute](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Ubicación compartida en un intercambio en la nube
Si está colocado en una instalación con un cambio en la nube, puede ordenar conexiones cruzadas virtual toohello nube de Microsoft a través de exchange de Ethernet del proveedor de hello ubicación compartida. Ubicación compartida proveedores pueden proporcionar conexiones cruzadas de capa 2 o administrado Layer 3 conexiones cruzadas entre la infraestructura de instalación de colocalización de Hola y de nube de Microsoft de Hola.

## <a name="Ethernet"></a>Conexiones Ethernet de punto a punto
Puede conectar su toohello de centros de datos/oficinas locales nube de Microsoft a través de vínculos de Ethernet de punto a punto. Proveedores de Ethernet de punto a punto pueden ofrecer las conexiones de capa 2 o administrar las conexiones de capa 3 entre su sitio y Hola nube de Microsoft.

## <a name="IPVPN"></a>Redes de conexión universal (IPVPN)
Puede integrar la WAN con hello nube de Microsoft. Los proveedores IPVPN (normalmente VPN MPLS) ofrecen conectividad universal entre los centros de datos y las sucursales. Hola Microsoft en la nube puede ser toomake WAN tooyour conectadas entre sí buscar simplemente como otra sucursal. Los proveedores de WAN normalmente ofrecen una conectividad de nivel 3 administrada. Características y capacidades de ExpressRoute son todos los idénticas en todas las de hello por encima de los modelos de conectividad. 

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de las conexiones ExpressRoute y dominios de enrutamiento. Consulte [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).
* Información acerca de las características de ExpressRoute. Vea hello [información general técnica de ExpressRoute](expressroute-introduction.md)
* Busque un proveedor de servicios. Consulte [Asociados de ExpressRoute de Azure y ubicaciones de emparejamiento](expressroute-locations.md).
* Asegúrese de que se cumplen todos los requisitos previos. Consulte [Requisitos previos de ExpressRoute](expressroute-prerequisites.md).
* Consulte los requisitos de toohello para [enrutamiento](expressroute-routing.md), [NAT](expressroute-nat.md), y [QoS](expressroute-qos.md).
* Configure su conexión ExpressRoute.
  * [Creación de un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configuración del enrutamiento](expressroute-howto-routing-portal-resource-manager.md)
  * [Vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-portal-resource-manager.md)
