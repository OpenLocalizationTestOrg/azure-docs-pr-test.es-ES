---
title: aaaAzure ExpressRoute circuitos y dominios de enrutamiento | Documentos de Microsoft
description: "Esta página proporciona una visión general de circuitos ExpressRoute y dominios de enrutamiento de Hola."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>Circuitos ExpressRoute y dominios de enrutamiento
 Debe solicitar un *circuito de ExpressRoute* tooconnect su tooMicrosoft de infraestructura local a través de un proveedor de conectividad. Hola figura siguiente proporciona una representación lógica de conectividad entre la WAN y Microsoft.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>Circuitos ExpressRoute
Un *circuito ExpressRoute* representa una conexión lógica entre la infraestructura local y los servicios en la nube de Microsoft a través de un proveedor de conectividad. Puede solicitar varios circuitos ExpressRoute. Puede ser cada circuito en Hola mismo o en distintas regiones, y puede ser local tooyour conectado a través de proveedores de conectividad distinto. 

Circuitos ExpressRoute no asignan a entidades físicas tooany. Un circuito se identifica de forma única mediante un GUID estándar denominado clave de servicio (s-key). clave de servicio de Hello es Hola único dato de información que se intercambia entre Microsoft, proveedor de conectividad de Hola y usted. Hola s-key no es un secreto por motivos de seguridad. Hay una asignación 1:1 entre un circuito ExpressRoute y Hola s-key.

Un circuito de ExpressRoute puede tener hasta toothree independientes emparejamientos: Azure privada público, Azure y Microsoft. Cada emparejamiento es un par de sesiones de BGP independientes configuradas cada una de ellas de forma redundante para una alta disponibilidad. Hay una asignación 1 (1 <= N <= 3) entre un circuito ExpressRoute y los dominios de enrutamiento. Un circuito ExpressRoute puede tener uno, dos o los tres emparejamientos habilitados por circuito ExpressRoute.

Cada circuito tiene un ancho de banda fijo (50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 10 Gbps) y proveedor de conectividad tooa asignadas y una ubicación de emparejamiento. ancho de banda de Hola que seleccione se comparte entre todos los emparejamientos de hello para el circuito de Hola. 

### <a name="quotas-limits-and-limitations"></a>Cuotas, límites y limitaciones
Se aplican límites y cuotas predeterminados para cada circuito ExpressRoute. Consulte toohello [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md) página para obtener información actualizada acerca de las cuotas.

## <a name="expressroute-routing-domains"></a>Dominios de enrutamiento de ExpressRoute
Un circuito ExpressRoute tiene asociados varios dominios de enrutamiento: público de Azure, privado de Azure y Microsoft. Cada uno de los dominios de enrutamiento de hello es configurado de forma idéntica en un par de enrutadores (en activo / activo o compartir la carga configuración) para lograr alta disponibilidad. Servicios de Azure se clasifican como *público Azure* y *privada Azure* toorepresent Hola esquemas de direccionamiento IP.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Emparejamiento privado
Servicios, principalmente las máquinas virtuales (IaaS) de proceso de Azure y servicios en la nube (PaaS), que se implementan en una red virtual pueden estar conectados a través de dominio de emparejamiento privado Hola. dominio de emparejamiento privado Hola se considera toobe una extensión de confianza de la red principal en Microsoft Azure. Puede configurar una conectividad bidireccional entre la red principal y las redes virtuales de Azure (VNet). Este emparejamiento le permite conectar máquinas de toovirtual y servicios directamente en sus direcciones IP privadas en la nube.  

Puede conectar más de una red virtual toohello emparejamiento dominio privado. Hola de revisión [página de preguntas más frecuentes sobre](expressroute-faqs.md) para obtener información sobre los límites y limitaciones. Puede visitar hello [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md) página para obtener información actualizada acerca de los límites.  Consulte toohello [enrutamiento](expressroute-routing.md) página para obtener información detallada sobre la configuración de enrutamiento.

### <a name="public-peering"></a>Emparejamiento público
Se ofrecen servicios como Azure Storage, SQL Databases, y Websites en direcciones IP públicas. Privada puede conectarse tooservices hospedados en direcciones IP públicas, incluidas a direcciones VIP de sus servicios en la nube, a través de dominio de enrutamiento emparejamiento público Hola. Puede conectar Hola pública DMZ tooyour de emparejamiento dominio y conectar tooall Azure Hola de servicios en sus direcciones IP públicas desde la WAN sin necesidad de tooconnect a través de internet. 

Conectividad siempre se inicia desde la WAN tooMicrosoft Azure servicios. Servicios de Microsoft Azure no será capaz de tooinitiate conexiones en la red a través de este dominio de enrutamiento. Cuando se habilita el emparejamiento público, será capaz de tooconnect tooall Azure servicios. No podrá tooselectively servicios de selección para el que se anunciar rutas a. Puede revisar Hola lista de prefijos se anuncia tooyou a través de este emparejamiento hello [intervalos de IP de centro de datos de Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653) página. página de Hola se actualiza semanalmente.

Puede definir filtros de ruta personalizados dentro de sus tooconsume solo hello las rutas de red que necesita. Consulte toohello [enrutamiento](expressroute-routing.md) página para obtener información detallada sobre la configuración de enrutamiento. 

Vea hello [página de preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más información sobre servicios compatibles a través de dominio de enrutamiento emparejamiento público Hola. 

### <a name="microsoft-peering"></a>Emparejamiento de Microsoft
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Conectividad tooall otros servicios en línea de Microsoft (por ejemplo, servicios de Office 365) será a través de emparejamiento de Microsoft de Hola. Se permiten una conectividad bidireccional entre los servicios de nube WAN y Microsoft a través de dominio de enrutamiento emparejamiento de Microsoft de Hola. Debe conectar los servicios de nube tooMicrosoft sólo a través de direcciones IP públicas que pertenecen a usted o su proveedor de conectividad y debe cumplir las reglas de tooall Hola definido. Vea hello [requisitos previos de ExpressRoute](expressroute-prerequisites.md) página para obtener más información.

Vea hello [página de preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más información sobre servicios compatibles, los costos y detalles de configuración. Vea hello [ubicaciones de ExpressRoute](expressroute-locations.md) página para obtener información sobre la lista de Hola de proveedores de conectividad que ofrece soporte técnico de emparejamiento de Microsoft.

## <a name="routing-domain-comparison"></a>Comparación de dominios de enrutamiento
Hola tabla siguiente comparan tres dominios de enrutamiento Hola.

|  | **Emparejamiento privado** | **Emparejamiento público** | **Emparejamiento de Microsoft** |
| --- | --- | --- | --- |
| **Número máximo de prefijos admitidos por emparejamiento** |4000 de forma predeterminada, 10.000 con ExpressRoute Premium |200 |200 |
| **Intervalos de direcciones IP admitidas** |Cualquier dirección IPv4 válida de la WAN. |Direcciones IPv4 públicas propiedad suya o de su proveedor de conectividad. |Direcciones IPv4 públicas propiedad suya o de su proveedor de conectividad. |
| **Requisitos del número de sistema autónomo (AS)** |Números de sistema autónomo (AS) públicos y privados Debe poseer Hola pública como número si elige toouse uno. |Números de sistema autónomo (AS) públicos y privados Sin embargo, debe comprobar la titularidad de las direcciones IP públicas. |Números de sistema autónomo (AS) públicos y privados Sin embargo, debe comprobar la titularidad de las direcciones IP públicas. |
| **Direcciones IP de la interfaz de enrutamiento** |Direcciones IP públicas y de RFC1918 |Tooyou registrado en los registros de enrutamientos de direcciones de IP pública. |Tooyou registrado en los registros de enrutamientos de direcciones de IP pública. |
| **Compatibilidad con Hash MD5** |Sí |Sí |Sí |

Puede elegir tooenable uno o varios de los dominios de enrutamiento de hello como parte de su circuito de ExpressRoute. Puede elegir toohave todos los dominios de enrutamiento Hola ponerlos en Hola VPN mismo si desea que toocombine en un único dominio de enrutamiento. También puede colocar en dominios de enrutamientos diferentes, el diagrama de toohello similar. Hola recomienda configuración es que emparejamiento privado está conectado directamente red principal de toohello y Hola pública y vínculos de emparejamiento de Microsoft son DMZ tooyour conectado.

Si elige toohave todas las sesiones de emparejamiento tres, debe tener tres pares de sesiones de BGP (un par para cada tipo de intercambio de tráfico). pares de sesión BGP Hola proporcionan un vínculo de alta disponibilidad. Si se va a conectar mediante proveedores de conectividad de capa 2, será responsable de configurar y administrar el enrutamiento. Encontrará más revisando hello [flujos de trabajo](expressroute-workflows.md) para configurar ExpressRoute.

## <a name="next-steps"></a>Pasos siguientes
* Busque un proveedor de servicios. Consulte [Ubicaciones y proveedores de servicios de ExpressRoute](expressroute-locations.md).
* Asegúrese de que se cumplen todos los requisitos previos. Consulte [Requisitos previos de ExpressRoute](expressroute-prerequisites.md).
* Configure su conexión ExpressRoute.
  * [Creación y administración de circuitos ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configuración del enrutamiento (emparejamiento) para los circuitos ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)

