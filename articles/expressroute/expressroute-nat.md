---
title: requisitos de aaaNAT para circuitos ExpressRoute | Documentos de Microsoft
description: "En esta página se proporcionan requisitos detallados para configurar y administrar NAT para circuitos ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>Requisitos de NAT ExpressRoute
tooconnect tooMicrosoft servicios en la nube mediante ExpressRoute, podrá necesita tooset y administrar dispositivos NAT. Algunos proveedores de conectividad ofrecen la configuración y administración de NAT como un servicio administrado. Póngase en contacto con su toosee de proveedor de conectividad si ofrece un servicio de este tipo. De lo contrario, debe cumplir los requisitos de toohello descritos a continuación. 

Hola de revisión [ExpressRoute circuitos y dominios de enrutamiento](expressroute-circuit-peerings.md) página tooget una visión general del programa Hola a distintos dominios de enrutamientos. requisitos toomeet Hola dirección IP públicos de Azure público y el emparejamiento de Microsoft, le recomendamos que configure el NAT entre la red y Microsoft. Esta sección proporciona una descripción detallada de la infraestructura NAT de hello que necesita tooset.

## <a name="nat-requirements-for-azure-public-peering"></a>Requisitos de NAT para el emparejamiento público de Azure
Hello Azure ruta de acceso de interconexión pública permite tooconnect tooall servicios hospedados en Azure a través de sus direcciones IP públicas. Se incluyen servicios enumerados en hello [ExpessRoute preguntas más frecuentes sobre](expressroute-faqs.md) y los servicios hospedados por ISV en Microsoft Azure. 

> [!IMPORTANT]
> Servicios de conectividad tooMicrosoft Azure en público emparejamiento siempre se inicia desde la red en la red de Microsoft de Hola. Por lo tanto, no se pueden iniciar sesiones de red de tooyour de servicios de Microsoft Azure a través de ExpressRoute. Si intenta, toothese de paquetes enviados anunciados IP utilizará Hola internet en lugar de ExpressRoute.
> 

El tráfico destinado tooMicrosoft Azure en el emparejamiento público debe ser toovalid SNATed que direcciones IPv4 públicas antes de que entren en red de Microsoft de Hola. Hola figura siguiente proporciona una imagen de alto nivel de cómo se puede establecer Hola NAT hello toomeet por encima de requisito.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>Anuncios de ruta y grupo de direcciones IP NAT
Debe asegurarse de que el tráfico está entrando en hello Azure ruta pública de intercambio de tráfico con la dirección IPv4 pública válida. Microsoft debe ser propiedad de hello toovalidate capaz de hello grupo de direcciones IPv4 NAT con registro enrutamiento regional de Internet (RIR) o por un registro de enrutamiento de Internet (TIR). Una comprobación se realizará en función de hello como número está emparejada con y Hola direcciones IP usadas para hello NAT. Consulte toohello [requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) página para obtener información sobre los registros de enrutamientos.

No hay ninguna restricción en la longitud de Hola de prefijo IP de NAT de hello anunciado a través de este emparejamiento correctamente. Debe supervisar un grupo NAT hello y asegúrese de que no se le faltan de sesiones NAT.

> [!IMPORTANT]
> grupo de IP de NAT de Hello anunciados tooMicrosoft no debe ser anunciado toohello Internet. Esto interrumpirá los servicios de Microsoft de tooother de conectividad.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Requisitos NAT para el emparejamiento de Microsoft
ruta de acceso de emparejamiento de Microsoft Hello le permite conectarse tooMicrosoft los servicios de nube que no se admiten a través de hello Azure ruta de acceso de interconexión pública. lista de Hello de servicios incluye servicios de Office 365, como Exchange Online, SharePoint Online, Skype empresarial y Dynamics 365. Microsoft espera toosupport una conectividad bidireccional en el emparejamiento de Microsoft de Hola. Servicios en la nube el tráfico destinado tooMicrosoft deben ser toovalid SNATed que direcciones IPv4 públicas antes de que entren en red de Microsoft de Hola. El tráfico destinado tooyour red desde los servicios de nube de Microsoft debe estar SNATed en su tooprevent de borde de Internet [enrutamiento asimétrico](expressroute-asymmetric-routing.md). Hola figura siguiente proporciona una perspectiva de alto nivel de cómo Hola NAT debe ser el programa de instalación para el emparejamiento de Microsoft.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Tráfico procedente de su red destinados a tooMicrosoft
* Debe asegurarse de que el tráfico está entrando en hello Microsoft emparejamiento ruta de acceso con una dirección IPv4 pública válida. Microsoft debe ser propietario de hello toovalidate capaz de hello grupo de direcciones IPv4 NAT contra Hola registro regional de enrutamiento internet (RIR) o por un registro de enrutamiento de internet (TIR). Una comprobación se realizará en función de hello como número está emparejada con y Hola direcciones IP usadas para hello NAT. Consulte toohello [requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) página para obtener información sobre los registros de enrutamientos.
* Direcciones IP que usan para hello configuración de interconexión pública de Azure y otros circuitos ExpressRoute no deben ser anunciado tooMicrosoft a través de la sesión BGP Hola. No hay ninguna restricción en la longitud de Hola de prefijo IP de NAT de hello anunciado a través de este emparejamiento correctamente.
  
  > [!IMPORTANT]
  > grupo de IP de NAT de Hello anunciados tooMicrosoft no debe ser anunciado toohello Internet. Esto interrumpirá los servicios de Microsoft de tooother de conectividad.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Tráfico procedente de la red de destino tooyour de Microsoft
* Algunos escenarios requieren Microsoft tooinitiate conectividad tooservice puntos de conexión hospedados dentro de la red. Un ejemplo típico de escenario de hello sería servidores tooADFS de conectividad hospedados en la red de Office 365. En tales casos, debe propagarse prefijos adecuados de la red a Hola emparejamiento de Microsoft. 
* Debe tráfico de Microsoft SNAT en hello borde de Internet para los extremos de servicio dentro de su red tooprevent [enrutamiento asimétrico](expressroute-asymmetric-routing.md). Las solicitudes **y respuestas** con una dirección IP de destino que coincidan con una ruta recibida a través de ExpressRoute siempre se enviarán a través de ExpressRoute. Enrutamiento asimétrico existe si se recibe una solicitud Hola a través de Internet de hello con hello respuesta enviado a través de ExpressRoute. SNATing Hola Microsoft el tráfico entrante en hello borde Internet fuerza respuesta tráfico atrás toohello perimetral de Internet, resolver el problema de Hola.

![Enrutamiento asimétrico con ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Pasos siguientes
* Consulte los requisitos de toohello para [enrutamiento](expressroute-routing.md) y [QoS](expressroute-qos.md).
* Para obtener información sobre los flujos de trabajo, consulte [Flujos de trabajo de aprovisionamiento de circuitos y estados de circuito de ExpressRoute](expressroute-workflows.md).
* Configure su conexión ExpressRoute.
  
  * [Creación de un circuito ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configuración del enrutamiento](expressroute-howto-routing-classic.md)
  * [Vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-classic.md)

