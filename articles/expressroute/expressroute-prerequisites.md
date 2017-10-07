---
title: "aaaPrerequisites para la adopción de ExpressRoute de Azure | Documentos de Microsoft"
description: "Esta página proporciona una lista de toobe requisitos cumplido antes de que puede solicitar un circuito de ExpressRoute de Azure."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>Requisitos previos y lista de comprobación de ExpressRoute
en la nube tooconnect tooMicrosoft servicios mediante ExpressRoute, necesita tooverify ese Hola según los requisitos enumerados en las secciones siguientes de Hola se cumplieron.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Cuenta de Azure
* Una cuenta de Microsoft Azure válida y activa Esta cuenta es necesaria tooset seguridad Hola circuito de ExpressRoute. Los circuitos ExpressRoute son recursos que hay dentro de las suscripciones de Azure. Una suscripción de Azure es un requisito, incluso si la conectividad está limitado de los servicios de nube de Microsoft de Azure toonon, como servicios de Office 365 y Dynamics 365.
* Una suscripción activa de Office 365 (si usa los servicios de Office 365). Para obtener más información, vea hello [requisitos específicos de Office 365](#office-365-specific-requirements) sección de este artículo.

## <a name="connectivity-provider"></a>Proveedor de conectividad

* Puede trabajar con un [asociado de conectividad de ExpressRoute](expressroute-locations.md#partners) tooconnect toohello nube de Microsoft. Se puede configurar una conexión entre la red local y Microsoft de [tres maneras](expressroute-introduction.md).
* Si el proveedor no es un asociado de conectividad de ExpressRoute, todavía puede conectarse toohello de nube de Microsoft a través de un [proveedor de exchange en la nube](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Requisitos de red
* **Conectividad redundante**: no hay ningún requisito de redundancia en la conectividad física entre usted y su proveedor. Microsoft requiere redundancia toobe de sesiones BGP configure entre enrutadores de Microsoft y los enrutadores de emparejamiento de hello, aunque sólo tenga [exchange de nube de una conexión física tooa](expressroute-faqs.md#onep2plink).
* **Enrutamiento**: dependiendo de cómo se conecte toohello Microsoft Cloud, usted o su proveedor necesita tooset y administrar sesiones BGP de Hola para [dominios de enrutamiento](expressroute-circuit-peerings.md). Algunos proveedores de conectividad Ethernet o proveedores de intercambio en la nube pueden ofrecer administración BGP como un servicio de valor añadido.
* **NAT**: Microsoft solo acepta direcciones IP públicas a través de emparejamiento de Microsoft. Si utiliza direcciones IP privadas en la red local, o el proveedor necesidad tootranslate Hola privada direcciones IP toohello las direcciones IP públicas [utilizando Hola NAT](expressroute-nat.md).
* **QoS**: Skype Empresarial cuenta con varios servicios (por ejemplo, voz, vídeo o texto) que requieren un tratamiento diferenciado de QoS. Usted y el proveedor deben seguir hello [requisitos de QoS](expressroute-qos.md).
* **Seguridad de red**: considere la posibilidad de [seguridad de red](../best-practices-network-security.md) al conectarse toohello Microsoft Cloud a través de ExpressRoute.

## <a name="office-365"></a>Office 365
Si tiene previsto tooenable Office 365 en ExpressRoute, revise Hola después de documentos para obtener más información acerca de los requisitos de Office 365.

* [Información general de ExpressRoute para Office 365](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Enrutamiento con ExpressRoute para Office 365](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Direcciones URL e intervalos de direcciones IP de Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Planes de red y ajuste del rendimiento para Office 365](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Herramientas y calculadoras de ancho de banda de red](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Integración de Office 365 con entornos locales](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Vídeos sobre el aprendizaje avanzado de ExpressRoute en Office 365](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Si tiene previsto tooenable Dynamics 365 ExpressRoute, revise Hola después de documentos para obtener más información acerca de Dynamics 365

* [Documento técnico de Dynamics 365 y ExpressRoute](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [Direcciones URL de Dynamics 365](https://support.microsoft.com/kb/2655102) e [Intervalos de direcciones IP](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).
* Encuentre un proveedor de conectividad ExpressRoute. Consulte [Asociados de ExpressRoute de Azure y ubicaciones de emparejamiento](expressroute-locations.md).
* Consulte toorequirements para [enrutamiento](expressroute-routing.md), [NAT](expressroute-nat.md), y [QoS](expressroute-qos.md).
* Configure su conexión ExpressRoute.
  * [Creación de un circuito ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configuración del enrutamiento](expressroute-howto-routing-classic.md)
  * [Vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-classic.md)
