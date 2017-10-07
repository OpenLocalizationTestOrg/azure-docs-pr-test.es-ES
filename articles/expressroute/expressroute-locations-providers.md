---
title: 'Ubicaciones y proveedores de conectividad: Azure ExpressRoute | Microsoft Docs'
description: "Este artículo ofrece una introducción detallada de ubicaciones donde se ofrecen los servicios y cómo tooconnect tooAzure regiones. Se ordenan por ubicación."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: feb67da3-5abc-4acb-bad4-f78e3c541ded
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: kaanan
ms.openlocfilehash: 838d52701d177aa7f13e845b7bde66d07b5efed6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-partners-and-peering-locations"></a>Asociados de ExpressRoute y ubicaciones de emparejamiento

> [!div class="op_single_selector"]
> * [Ubicaciones por proveedor](expressroute-locations.md)
> * [Proveedores por ubicación](expressroute-locations-providers.md)


tablas de Hello en este artículo proporcionan información sobre proveedores de conectividad de ExpressRoute, ExpressRoute geográfico, servicios de nube de Microsoft compatibles a través de ExpressRoute y ExpressRoute integradores de sistemas (SIs).

## <a name="partners"></a>Proveedores de conectividad ExpressRoute
ExpressRoute es compatible con todas las ubicaciones y regiones de Azure. Hola siguiente mapa proporciona una lista de regiones de Azure y las ubicaciones de ExpressRoute. Ubicaciones de ExpressRoute, consulte toothose donde Microsoft homólogos con varios proveedores de servicio.

![Mapa de ubicación][0]

Tendrá acceso a los servicios tooAzure en todas las regiones dentro de una región geopolíticas si había conectado tooat lo menos una ubicación de ExpressRoute dentro de la región geopolíticos Hola. 

### <a name="azure-regions-tooexpressroute-locations-within-a-geopolitical-region"></a>Ubicaciones de las regiones de Azure tooExpressRoute dentro de una región geopolíticas
Hello en la tabla siguiente proporciona una asignación de regiones de Azure tooExpressRoute ubicaciones dentro de una región geopolíticas.

| **Región geopolítica** | **Regiones de Azure** | **Ubicaciones de ExpressRoute** |
| --- | --- | --- |
| **Norteamérica** |Este de EE. UU., oeste de EE. UU., este de EE. UU. 2, oeste de EE.UU. 2, centro de EE. UU., centro-sur de EE. UU., centro-norte de EE. UU., centro-oeste de EE. UU., centro de Canadá y este de Canadá |Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Ángeles, Miami, Nueva York, San Antonio, Seattle, Silicon Valley, Washington DC, Montreal, Ciudad de Quebec, Toronto |
| **Sudamérica** |Sur de Brasil |São Paulo |
| **Europa** |Europa del Norte, Europa Occidental, Oeste de Reino Unido, Sur de Reino Unido |Ámsterdam, Dublín, Londres, Newport(Wales)+, París |
| **Asia** |Este de Asia y Sudeste de Asia |Hong Kong y Singapur |
| **Japón** |Oeste de Japón y Este de Japón |Osaka, Tokyo |
| **Australia** |Este de Australia y Sudeste de Australia |Melbourne, Sidney |
| **India** |India occidental, India central, India del Sur |Chennai, Mumbai |
| **Corea del Sur** |Corea Central, Corea del Sur |Busan, Seúl |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>Regiones y límites geopolíticos para nubes nacionales
tabla de Hello siguiente proporciona información en las regiones y límites geopolíticos para nubes nacionales.

| **Región geopolítica** | **Regiones de Azure** | **Ubicaciones de ExpressRoute** |
| --- | --- | --- |
| **Nube del gobierno de Estados Unidos** |Iowa Gob. EE. UU., Virginia Gob. EE. UU., centro de US DoD, este de US DoD  |Chicago, Dallas, Nueva York, Seattle, Silicon Valley, Washington D.C. |
| **China** |Este de China, Norte de China |Beijing, Shanghai |
| **Alemania** |Centro de Alemania, Alemania oriental |Berlín+, Fráncfort |

No se admite la conectividad entre las regiones geopolíticas en estándar hello ExpressRoute SKU. Necesitará tooenable hello ExpressRoute premium complemento toosupport la conectividad global. No se admiten los entornos de nube de toonational de conectividad. Puede trabajar con su proveedor de conectividad si surge tal necesidad.

## <a name="locations"></a>Ubicaciones del proveedor de conectividad

Hello tabla siguiente muestran ubicaciones de conectividad y de saludo proveedores de servicios para cada ubicación. Si desea que los proveedores de servicios de tooview y ubicaciones de hello para el que pueda prestar el servicio, consulte [ubicaciones de proveedor de servicios](expressroute-locations.md#locations). 


### <a name="production-azure"></a>Azure para producción
| **Ubicación** | **Proveedores de servicios** |
| --- | --- |
| **Ámsterdam** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, euNetworks, GÉANT, InterCloud, Internet Solutions - Cloud Connect, Interxion, KPN, Level 3 Communications, Megaport, Orange, Tata Communications, TeleCity Group, Telefonica, Telenor, Verizon, Zayo Group |
| **Atlanta** |Equinix |
| **Busán** |LG CNS |
| **Chennai** | Airtel+, Global CloudXchange (GCX), SIFY, Tata Communications |
| **Chicago** |AT&T NetBond, Comcast, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group |
| **Dallas** |Aryaka Networks, AT&T NetBond, Cologix, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group+ |
| **Denver** |CoreSite |
| **Dublín** |Colt, Interxion, Telecity Group |
| **Hong Kong** |Aryaka Networks, British Telecom, China Telecom Global, Equinix, Megaport, Orange, PCCW Global Limited, Tata Communications y Verizon |
| **Las Vegas** |Level 3 Communications+ y Megaport |
| **Londres** |AT&T NetBond, British Telecom, Colt, Equinix, InterCloud, Internet Solutions - Cloud Connect, Interxion, Jisc, Level 3 Communications, Megaport, MTN, NTT Communications, Orange, Tata Communications, Telecity Group, Telehouse - KDDI, Telenor, Verizon, Vodafone, Zayo Group+ |
| **Los Ángeles** |CoreSite, Equinix, Megaport, NTT y Zayo Group |
| **Melbourne** |AARNet, Equinix, Megaport, NEXTDC y Telstra Corporation |
| **Miami** |C3ntro+, Megaport, Neutrona Networks |
| **Montreal** |Bell Canada y Cologix |
| **Mumbai (Bombay)** |Airtel+, Sify, Tata Communications |
| **Nueva York** |CoreSite, Equinix, Megaport y Zayo Group |
| **Newport (Gales)** |Datos de última generación |
| **Osaka** |Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, NTT SmartConnect, Softbank |
| **París** |Colt, Interxion, Equinix, Orange |
| **Quebec ciudad** | Megaport |
| **San Antonio** |Megaport |
| **São Paulo** |Ascenty Data Centers+, Equinix, Level 3 Communications, Neutrona Networks, Telefonica, UOLDIVEO |
| **Seattle** |Equinix, Level 3 Communications y Megaport |
| **Seúl** |KINX, LG CNS, Sejong Telecom |
| **Silicon Valley** |Aryaka Networks, AT&T NetBond, British Telecom, CenturyLink+, Comcast, Console, Equinix, Level 3 Communications, Megaport, Orange, Tata Communications, Verizon, Zayo Group |
| **Singapur** |Aryaka Networks, AT&T NetBond, British Telecom, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, SingTel, Tata Communications y Verizon |
| **Sidney** |AARNet, AT&T NetBond, British Telecom, Equinix, Megaport, NEXTDC, Orange, Telstra Corporation y Verizon |
| **Tokio** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, Softbank, Verizon |
| **Toronto** |AT&T NetBond, Bell Canada, Cologix, Console, Equinix, Megaport, Telus, Zayo Group |
| **Washington DC** |Aryaka Networks, AT&T NetBond, British Telecom, Comcast, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, Tata Communications, Verizon, Zayo Group |

 **+** indica próximamente

### <a name="national-cloud-environments"></a>Entornos de nube nacionales

### <a name="us-government-cloud"></a>Nube del gobierno de Estados Unidos
| **Ubicación** | **Proveedores de servicios** |
| --- | --- |
| **Chicago** |AT&T NetBond, Equinix, Level 3 Communications y Verizon |
| **Dallas** |Equinix, Megaport y Verizon |
| **Nueva York** |Equinix, Level 3 Communications+ y Verizon |
| **Silicon Valley** | Equinix, Level 3 Communications |
| **Seattle** | Equinix |
| **Washington DC** |AT&T NetBond, Equinix, Level 3 Communications y Verizon |

### <a name="china"></a>China
| **Ubicación** | **Proveedores de servicios** |
| --- | --- |
| **Beijing** |China Telecom |
| **Shanghai** |China Telecom |

más información, consulte toolearn [ExpressRoute en China](http://www.windowsazure.cn/home/features/expressroute/)

### <a name="germany"></a>Alemania
| **Ubicación** | **Proveedores de servicios** |
| --- | --- |
| **Berlín** |Colt+, e-shelter, Megaport+, T-Systems |
| **Fráncfort** |Colt, Equinix e Interxion |

## <a name="c1partners"></a>Conectividad a través de proveedores de intercambio
Si su proveedor de conectividad no aparece en la lista de las secciones anteriores, puede crear una conexión.

* Póngase en contacto con su toosee de proveedor de conectividad si están conectado tooany de intercambios de hello en tabla Hola anterior. Puede comprobar siguientes de hello vínculos toogather obtener más información acerca de los servicios ofrecidos por los proveedores de exchange. Varios proveedores de conectividad ya están conectados tooEthernet intercambios.
  * [Cologix](http://www.cologix.com/)
  * [Console](https://www.consoleconnect.com/partners/cloudsaas/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [InterXion](http://www.interxion.com/)
  * [NextDC](http://www.nextdc.com/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* Indique a su proveedor de conectividad ampliar la ubicación de intercambio de tráfico de red toohello de elección.
  * Asegúrese de que su proveedor de conectividad amplíe la conectividad con una alta disponibilidad para que no haya ningún punto único de error.
* Solicitar un circuito de ExpressRoute con exchange hello como el proveedor de conectividad tooconnect tooMicrosoft.
  * Siga los pasos de [crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) tooset la conectividad.

## <a name="c1partners"></a>Conectividad a través de proveedores de servicios
| **Ubicación** | **Exchange** | **Proveedores de conectividad** |
| --- | --- | --- |
| **Ámsterdam** | Equinix y Telecity | Eurofiber , Fastweb S.p.A y Nianet |
| **Chicago** | Equinix | Lightower, Windstream |
| **Dallas** | Equinix, Megaport | C3ntro Telecom, Cox Business, Data Foundry, Transtelco |
| **Fráncfort** | Telecity | Nianet y QSC AG |
| **Hong Kong** | Equinix | Macroview Telecom |
| **Londres** | Equinix, euNetworks y Telecity | Bezeq International Ltd., Epsilon, Exponential E, HSO, NexGen Networks, Tamares Telecom, Zain |
| **Los Ángeles** | Equinix |Transtelco |
| **Madrid** | Level3 | Zertia |
| **Montreal** | Cologix y Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Zirro |
| **Nueva York** |Equinix, Megaport | Altice Business, Lightower, Webair |
| **Seattle** |Equinix | Alaska Communications |
| **Silicon Valley** |Equinix | Cox Business, Windstream |
| **Singapur** |Equinix |1CLOUDSTAR, Epsilon Telecommunications Limited, LGA Telecom, United Information Highway (UIH) |
| **Slough** | Equinix | HSO|
| **Sidney** | Megaport | Macquarie Telecom Group|
| **Tokio** | Equinix | ARTERIA Networks Corporation, BroadBand Tower, Inc. |
| **Toronto** | Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Thinktel, Zirro|
| **Washington DC** |Equinix | Altice Business, Gtt Communications Inc, Epsilon, Lightower, Masergy, Windstream |

## <a name="expressroute-system-integrators"></a>Integradores de sistemas de ExpressRoute
Habilitación de toofit conectividad privada que pueden resultar complicado sus necesidades, basados en la escala de saludo de la red. Puede trabajar con cualquiera de los integradores de hello enumerados en hello después de la tabla tooassist se con tooExpressRoute de incorporación.

| **Continente** | **Integradores de sistemas** |
| --- | --- |
| **Asia** |Avanade Inc. y OneAs1a |
| **Australia** | Ensyst, IT Consultancy, MOQdigital, Vigilant.IT |
| **Europa** |Avanade Inc., Altogee, Bright Skies GmbH, Inframon, MSG Services, New Signature, Nelite, Orange Networks, sol-tec |
| **Norteamérica** |Avanade Inc., Equinix Professional Services, FlexManage, Perficient, Presidio |
| **Sudamérica** |Avanade Inc. |
## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).
* Asegúrese de que se cumplen todos los requisitos previos. Consulte [Requisitos previos de ExpressRoute](expressroute-prerequisites.md).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Mapa de ubicación"
