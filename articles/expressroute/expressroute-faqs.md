---
title: "Preguntas más frecuentes de ExpressRoute aaaAzure | Documentos de Microsoft"
description: "Hola preguntas más frecuentes de ExpressRoute contiene información sobre admite servicios de Azure, costo, datos y las conexiones, SLA, proveedores y ubicaciones, ancho de banda y detalles técnicos adicionales."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>P+F de ExpressRoute

## <a name="what-is-expressroute"></a>¿Qué es ExpressRoute?

ExpressRoute es un servicio de Azure que permite crear conexiones privadas entre los centros de datos de Microsoft y la infraestructura local o en una instalación de coubicación. Las conexiones ExpressRoute no pasan por hello Internet pública y ofrecen una mayor seguridad, confiabilidad y velocidades superiores a reducir las latencias que las típicas conexiones a través de Internet de Hola.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>¿Cuáles son las ventajas de Hola de usar ExpressRoute y conexiones de red privada?

Las conexiones ExpressRoute no pasan por hello Internet pública. Ofrecen mayor seguridad, confiabilidad y velocidades, con latencias coherentes y menor que las típicas conexiones a través de Internet de Hola. En algunos casos, utilizando los datos de tootransfer de ExpressRoute las conexiones entre dispositivos locales y Azure puede producir ventajas económicas considerables.

### <a name="where-is-hello-service-available"></a>¿Dónde está disponible el servicio de hello?

Consulte esta página para la ubicación del servicio y la disponibilidad: [Asociados y ubicaciones de ExpressRoute](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>¿Cómo se puede usar ExpressRoute tooconnect tooMicrosoft si no tengo asociaciones con uno de los partners de hello operadores de ExpressRoute?

Puede seleccionar un operador regional y terrenos tooone de las conexiones Ethernet de exchange Hola admitida ubicaciones del proveedor. A continuación, puede consultarla con Microsoft en la ubicación del proveedor de Hola. Compruebe hello en la última sección de [ExpressRoute socios y ubicaciones](expressroute-locations.md) toosee si su proveedor de servicios se encuentra en cualquiera de las ubicaciones de exchange Hola. A continuación, puede solicitar un circuito de ExpressRoute a través de hello servicio proveedor tooconnect tooAzure.

### <a name="how-much-does-expressroute-cost"></a>¿Cuánto cuesta ExpressRoute?

Para obtener más información sobre los precios, consulte [Información sobre el precio](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>¿Si tengo que pagar por un circuito ExpressRoute de un ancho de banda determinado, Hola conexión VPN que contrate con mi proveedor de servicios de red ha toobe Hola misma velocidad?

No. Puede adquirir una conexión VPN de cualquier velocidad de su proveedor de servicios. Sin embargo, su tooAzure de conexión es ancho de banda de la circuito de ExpressRoute de toohello limitado que adquiera.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>¿Si tengo que pagar por un circuito de ExpressRoute de un ancho de banda determinado, es necesario Hola capacidad tooburst seguridad toohigher velocidades si es necesario?

Sí. Circuitos ExpressRoute están configurado tooallow tooburst tootwo horas Hola límite de ancho de banda adquirido sin coste adicional. Póngase en contacto con su toosee de proveedor de servicios si ellos admiten esta capacidad.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>¿Puedo usar Hola mismo privada conexión con la red virtual y otros servicios de Azure de red al mismo tiempo?

Sí. Un circuito de ExpressRoute, una vez configurado, le permite tooaccess servicios dentro de una red virtual y otros servicios de Azure simultáneamente. Conectar redes de toovirtual a través de la ruta de intercambio de tráfico privado hello y tooother servicios a través de la ruta de acceso de interconexión pública Hola.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>¿ExpressRoute ofrece un contrato de nivel de servicio (SLA)?

Para obtener información, vea hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) página.

## <a name="supported-services"></a>Servicios admitidos

ExpressRoute admite [tres dominios de enrutamiento](expressroute-circuit-peerings.md) para diversos tipos de servicios.

### <a name="private-peering"></a>Emparejamiento privado

* Virtual Networks, que incluye todas las máquinas virtuales y servicios en la nube.

### <a name="public-peering"></a>Emparejamiento público

* Power BI
* Dynamics 365 for Finance and Operations (conocido anteriormente como Dynamics AX Online)
* La mayoría de hello Azure servicios, con hello después algunas excepciones:
  * CDN
  * Pruebas de carga de Visual Studio Team Services
  * Multi-Factor Authentication
  * Traffic Manager

### <a name="microsoft-peering"></a>Emparejamiento de Microsoft

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Aplicaciones de Dynamics 365 Customer Engagement (anteriormente conocidas como CRM Online)
  * Dynamics 365 for Sales
  * Dynamics 365 for Customer Service
  * Dynamics 365 for Field Service
  * Dynamics 365 for Project Service

## <a name="data-and-connections"></a>Datos y conexiones

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>¿Hay límites en la cantidad de Hola de datos que se pueden transferir mediante ExpressRoute?

No se establece un límite de cantidad de Hola de transferencia de datos. Consulte demasiado[detalles de precios](https://azure.microsoft.com/pricing/details/expressroute/) para obtener información sobre las tasas de ancho de banda.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>¿Qué velocidades de conexión son compatibles con ExpressRoute?

Ofertas de ancho de banda compatibles:

50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, 10 Gbps

### <a name="which-service-providers-are-available"></a>¿Qué proveedores de servicio están disponibles?

Vea [ExpressRoute socios y ubicaciones](expressroute-locations.md) lista de Hola de proveedores de servicios y ubicaciones.

## <a name="technical-details"></a>Detalles técnicos

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>¿Cuáles son los requisitos técnicos de Hola para conectar mi tooAzure de ubicación local?

Consulte la [página de requisitos previos de ExpressRoute](expressroute-prerequisites.md) para conocer los requisitos.

### <a name="are-connections-tooexpressroute-redundant"></a>¿Son tooExpressRoute conexiones redundantes?

Sí. Cada circuito de ExpressRoute tiene un par redundante de entre conexiones configuradas tooprovide alta disponibilidad.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>¿Se pierde conectividad si se produce un error en uno de mis vínculos de ExpressRoute?

No se perderá conectividad si uno de hello entre las conexiones se produce un error. Una conexión redundante es la carga de hello toosupport disponible de la red. Asimismo, puede crear varios circuitos en un otro emparejamiento ubicación tooachieve resistencia a errores.

### <a name="onep2plink"></a>¿Si no estoy comparte ubicación en un intercambio de nube y mi proveedor de servicios ofrece una conexión punto a punto, es necesario tooorder dos conexiones físicas entre mi red local y Microsoft?

Si su proveedor de servicios puede establecer dos circuitos virtuales de Ethernet a través de la conexión física hello, solo se necesita una conexión física. Hello conexión física (por ejemplo, una fibra óptica) se termina en un nivel 1 (L1) dispositivo (consulte la imagen de hello). circuitos virtuales de Hello dos Ethernet se etiquetan con diferentes identificadores de VLAN, uno para el circuito principal de hello y otro para hello secundaria. Los identificadores de VLAN están en encabezado de Ethernet de hello 802.1Q externa. encabezado de Ethernet de Hello 802.1Q interna (no mostrado) está asignada tooa específico [dominio de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>¿Puedo extender una de Mis tooAzure de VLAN mediante ExpressRoute?

No. No admitimos ampliaciones de conectividad de la capa 2 en Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>¿Se puede disponer de más de un circuito ExpressRoute en mi suscripción?

Sí. Puede disponer de más de un circuito ExpressRoute en su suscripción. límite de Hello predeterminado se establece too10. Puede ponerse en contacto con límite de Microsoft Support tooincrease hello, si es necesario.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>¿Es posible tener circuitos ExpressRoute de otros proveedores de servicios?

Sí. Puede tener circuitos ExpressRoute de muchos otros proveedores de servicios. Cada circuito ExpressRoute estará asociado solo a un proveedor de servicios. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>¿Puedo tener varios circuitos ExpressRoute en hello misma ubicación?

Sí. Puede tener varios circuitos ExpressRoute, con Hola igual o proveedores de servicio diferente en Hola misma ubicación. Sin embargo, no se puede vincular más de un toohello de circuito de ExpressRoute mismo virtual de red de hello misma ubicación.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>¿Cómo conecto mi circuito de ExpressRoute de tooan de redes virtuales

pasos básicos de Hello son:

* Establecer un circuito ExpressRoute y tener el proveedor de servicios de hello habilitarla.
* Usted, o proveedor de hello, debe configurar el emparejamiento de BGP de hello (s).
* Vínculo de circuito de ExpressRoute de toohello de red virtual de Hola.

Para obtener más información, vea [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>¿Hay límites de conectividad para mi circuito ExpressRoute?

Sí. Hola [ExpressRoute socios y ubicaciones](expressroute-locations.md) artículo proporciona información general sobre los límites de conectividad de Hola por un circuito ExpressRoute. Conectividad de un circuito de ExpressRoute es limitado tooa única región geopolíticos. Conectividad puede ser regiones geopolíticas toocross expandido habilitando la característica premium de hello ExpressRoute.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>¿Puedo vincular toomore a una red virtual tooan circuito de ExpressRoute?

Sí. Puede tener too10 las conexiones de redes virtuales en un circuito de ExpressRoute estándar e instalación too100 en un [circuito de ExpressRoute de premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>Tengo varias suscripciones a Azure que contienen redes virtuales. ¿Puedo conectar redes virtuales que están en el circuito de ExpressRoute único de suscripciones independientes tooa?

Sí. Puede autorizar la too10 otro toouse de las suscripciones de Azure un circuito ExpressRoute único. Este límite puede aumentarse al habilitar la característica premium de hello ExpressRoute.

Para obtener más información, vea [Uso compartido de un circuito ExpressRoute a través de varias suscripciones](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>¿Son redes virtuales toohello conectado mismo circuito aislada entre sí?

No. Desde un enrutamiento toohello vinculado de redes virtuales todas las perspectivas mismo circuito ExpressRoute forman parte del mismo dominio de enrutamiento de Hola y no están aisladas entre sí. Si es necesitan distribuir aislamiento, deberá toocreate un circuito ExpressRoute independiente.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>¿Puedo tener un toomore de red virtual conectado a un circuito de ExpressRoute?

Sí. Puede vincular una única red virtual con seguridad de circuitos ExpressRoute de toofour. Se deben solicitar mediante cuatro [ubicaciones de ExpressRoute](expressroute-locations.md) diferentes.

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>¿Acceso Hola Internet desde Mis circuitos tooExpressRoute conectado de redes virtuales?

Sí. Si no ha anunciado rutas predeterminadas (0.0.0.0/0) o prefijos de rutas de Internet a través de la sesión BGP de hello, puede conectarse toohello Internet desde un circuito de ExpressRoute de tooan de red virtual conectada.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>¿Puedo bloquear Internet conectividad toovirtual redes conectadas tooExpressRoute circuitos?

Sí. Puede anunciar tooblock de rutas (0.0.0.0/0) de forma predeterminada todas las máquinas de toovirtual de conectividad de Internet implementan en una red virtual y enrutan todo el tráfico de salida a través del circuito de ExpressRoute de Hola.

Si anunciar rutas predeterminadas, se fuerza tooservices de tráfico que ofrece sobre pública local tooyour atrás emparejamiento (por ejemplo, el almacenamiento de Azure y base de datos SQL). Deberá tooconfigure su tooAzure de tráfico de tooreturn enrutadores a través de la ruta de acceso de interconexión pública Hola o de hello Internet.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>¿Puede redes virtuales vinculadas toohello mismo circuito ExpressRoute hablar tooeach otros?

Sí. Máquinas virtuales implementadas en redes virtuales toohello conectado mismo circuito ExpressRoute puede comunicarse entre sí.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>¿Se puede usar conectividad de sitio a sitio para redes virtuales junto con ExpressRoute?

Sí. ExpressRoute puede coexistir con las VPN de sitio a sitio.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>¿Puedo mover una red virtual de configuración de sitio a sitio / point-to-site toouse ExpressRoute?

Sí. Deberá toocreate una puerta de enlace de ExpressRoute dentro de la red virtual. Hay un breve tiempo de inactividad asociado con el proceso de Hola.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>¿Por qué es una dirección IP pública asociada con la puerta de enlace de ExpressRoute de hello en una red virtual?

se utiliza la dirección IP pública Hola interno solo para administración. Esta dirección IP pública no está expuesto toohello Internet y no constituye un riesgo de seguridad de la red virtual.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>¿Qué necesito tooconnect tooAzure almacenamiento a través de ExpressRoute?

Debe establecer un circuito ExpressRoute y configurar rutas para el intercambio de tráfico público.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>¿Hay límites en el número de Hola de rutas que puedo anunciar?

Sí. Se aceptan los prefijos de ruta too4000 para el nivel privado y 200 de mismo nivel pública y emparejamiento de Microsoft. Puede aumentar este too10 000 rutas para el intercambio de tráfico privado si habilita la característica premium de hello ExpressRoute.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>¿Existen restricciones en los intervalos IP que puedo anunciar durante la sesión BGP Hola?

No se aceptan los prefijos privados (RFC1918) en hello pública y la sesión BGP de emparejamiento de Microsoft.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>¿Qué ocurre si superan los límites BGP Hola?

Se quitarán las sesiones BGP. Se restablecerán una vez que el recuento del prefijo de hello esté por debajo del límite de Hola.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>¿Qué es hello BGP de ExpressRoute mantenga tiempo? ¿Se puede ajustar?

tiempo de espera de Hello es 180. mensajes de mantenimiento de saludo se envían cada 60 segundos. La configuración estos se fijan en hello lado de Microsoft que no se puede cambiar. Es posible que se tooconfigure diferentes temporizadores y parámetros de la sesión BGP Hola se negociará según corresponda.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Una vez que anunciar Hola predeterminada (0.0.0.0/0) de la ruta toomy las redes virtuales, no se puede activar Windows ejecutándose en mi máquinas virtuales de Azure. ¿Cómo tooI solucionar este problema?

Hola pasos reconocerle Azure solicitud de activación de hello:

1. Establecer el emparejamiento público de hello para el circuito de ExpressRoute.
2. Realizar una búsqueda DNS y buscar la dirección IP de Hola de **kms.core.windows.net**
3. Hello servicio de administración de claves debe reconocer esa solicitud de activación de hello procede de Azure y honor Hola solicitud. Realice uno de hello después de tres tareas:

   * En la red local, Hola enrutar el tráfico había destinado a Hola dirección IP que obtuvo en el paso 2 tooAzure atrás a través de emparejamiento público de Hola.
   * Tener su NSP proveedor precisa pin Hola tráfico atrás tooAzure a través de emparejamiento público de Hola.
   * Crear una ruta definida por el usuario esa dirección IP de Hola de puntos que tenga Internet como un próximo salto y aplicarlo subredes toohello donde son estas máquinas virtuales.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>¿Puedo cambiar el ancho de banda de Hola de un circuito ExpressRoute?

Sí, puede tratar de ancho de banda de tooincrease Hola del circuito de ExpressRoute en hello portal de Azure, o mediante PowerShell. Si hay capacidad disponible en el puerto físico hello en el que se creó el circuito, el cambio se realiza correctamente. 

Si se produce un error en el cambio, esto significa que hay suficiente capacidad restante en el puerto actual de Hola y deberá toocreate un nuevo circuito de ExpressRoute con mayor ancho de banda de hello, o que no hay ninguna capacidad adicional en esa ubicación, en cuyo caso no podrá ancho de banda de hello tooincrease. 

También tendrá toofollow con su tooensure de proveedor de conectividad que actualizan los aceleradores de hello dentro de su aumento de ancho de banda de redes toosupport Hola. Sin embargo, no es posible, reducir ancho de banda de Hola del circuito de ExpressRoute. Ha toocreate un nuevo circuito de ExpressRoute con bajo ancho de banda y eliminar el circuito antiguo Hola.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>¿Cómo se cambia el ancho de banda de Hola de un circuito ExpressRoute?

Puede actualizar el ancho de banda de Hola de circuito de ExpressRoute de hello mediante el cmdlet de PowerShell o API de REST de Hola.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>¿Qué es ExpressRoute Premium?

ExpressRoute premium es una colección de hello siguientes características:

* Aumentar el límite de la tabla de enrutamiento de 4000 rutas too10, 000 rutas para el intercambio de tráfico privado.
* Aumentar el número de redes virtuales que pueden estar conectado toohello circuito de ExpressRoute (el valor predeterminado es 10). Para obtener más información, vea hello [ExpressRoute límites](#limits) tabla.
* Conectividad tooOffice 365 y Dynamics 365.
* Conectividad global a través de la red principal de Microsoft de Hola. Ahora podrá vincular una red virtual en una región geopolítica con un circuito ExpressRoute en otra región.<br>
    **Ejemplos:**

    *  Puede vincular una red virtual que creó en Europa occidental tooan circuito de ExpressRoute creado en Silicon Valley. 
    *  En el emparejamiento público de hello, se anuncian prefijos de otras regiones geopolíticas tal que pueda conectarse a, por ejemplo, SQL Azure en Europa occidental de un circuito en Silicon Valley.


### <a name="limits"></a>El número de redes virtuales ¿puedo vincular circuito de ExpressRoute de tooan si habilito la premium de ExpressRoute?

Hello tablas siguientes muestran los límites de ExpressRoute de Hola y el número de Hola de redes virtuales por circuito de ExpressRoute:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>¿Cómo habilito ExpressRoute Premium?

Las características premium ExpressRoute pueden habilitarse cuando está habilitada la característica de Hola y pueden cerrarse mediante la actualización de estado del circuito de Hola. Puede habilitar ExpressRoute premium en el momento de creación de circuito, o puede llamar a la API de REST de Hola o cmdlet de PowerShell.

### <a name="how-do-i-disable-expressroute-premium"></a>¿Cómo deshabilito ExpressRoute Premium?

Puede deshabilitar ExpressRoute premium mediante una llamada a cmdlet de PowerShell o API de REST de Hola. Debe asegurarse de que ha escalado los límites de conectividad necesidades toomeet Hola predeterminado antes de deshabilitar premium de ExpressRoute. Si la utilización de la escala más allá de los límites predeterminados de hello, toodisable ExpressRoute premium de hello solicitud produce un error.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>¿Elegir características Hola que deseo de conjunto de características de hello premium?

No. No se puede elegir características Hola. Habilitaremos todas las características cuando active ExpressRoute Premium.

### <a name="how-much-does-expressroute-premium-cost"></a>¿Cuánto cuesta ExpressRoute Premium?

Consulte demasiado[detalles de precios](https://azure.microsoft.com/pricing/details/expressroute/) para lograr un costo.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>¿Tengo que pagar por ExpressRoute premium además toostandard cargos de ExpressRoute?

Sí. Se aplican cargos de premium de ExpressRoute encima de los cargos de circuito de ExpressRoute y cargos requeridos por el proveedor de conectividad de Hola.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute para Office 365 y Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>¿Cómo creo un tooconnect de circuito de ExpressRoute servicios tooOffice 365 y Dynamics 365?

1. Hola de revisión [página de requisitos previos de ExpressRoute](expressroute-prerequisites.md) toomake que cumple los requisitos de Hola.
2. tooensure que necesita la conectividad se cumplen, revise la lista de Hola de proveedores de servicios y las ubicaciones de hello [ExpressRoute socios y ubicaciones](expressroute-locations.md) artículo.
3. Planee los requisitos de capacidad revisando [Planificación de red y ajuste de rendimiento de Office 365](http://aka.ms/tune/).
4. Siga los pasos de hello enumerados en tooset de flujos de trabajo de Hola la conectividad [ExpressRoute flujos de trabajo de aprovisionamiento del circuito y Estados del circuito](expressroute-workflows.md).

> [!IMPORTANT]
> Asegúrese de que ha habilitado el complemento de ExpressRoute premium al configurar los servicios de conectividad tooOffice 365 y Dynamics 365.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>¿Necesito tooenable Azure pública emparejamiento tooconnect tooOffice 365 servicios y Dynamics 365?

No, solo necesita tooenable Peering Microsoft. TooAzure de tráfico de autenticación AD se envía a través de Microsoft Peering. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>¿Pueden admitir mi circuitos ExpressRoute existentes connectivity tooOffice 365 services y Dynamics 365?

Sí. El circuito de ExpressRoute existente puede ser configurado toosupport conectividad tooOffice 365 services. Asegúrese de que dispone de suficientes servicios de tooOffice 365 tooconnect de capacidad y que ha habilitado el complemento de premium. [Planificación de red y ajuste del rendimiento de Office 365](http://aka.ms/tune/) le ayudará a planificar sus necesidades de conectividad. Además, vea [Creación y modificación de un circuito ExpressRoute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>¿A qué servicios de Office 365 se puede acceder a través de la conexión ExpressRoute?

Consulte demasiado[intervalos de direcciones IP y las direcciones URL de Office 365](http://aka.ms/o365endpoints) página para obtener una lista actualizada de servicios admitidos a través de ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>¿Cuánto cuesta ExpressRoute para servicios de Office 365 y Dynamics 365?

Servicios de Office 365 y Dynamics 365 requieren premium complemento toobe habilitado. Vea hello [página de detalles de precios](https://azure.microsoft.com/pricing/details/expressroute/) de costes.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>¿En qué regiones es compatible ExpressRoute para Office 365?

Vea [Asociados de ExpressRoute y ubicaciones](expressroute-locations.md) para obtener más información.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>¿Puedo acceder a Office 365 sobre Hola Internet, incluso si se ha configurado ExpressRoute para mi organización?

Sí. Los puntos de conexión de Office 365 servicio son accesibles a través de Internet, Hola incluso si se ha configurado ExpressRoute para la red. Si está en una ubicación que esté configurado tooconnect tooOffice 365 servicios a través de ExpressRoute, se conectará a través de ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>¿Puedo acceder a servicios de Office 365 US Government Community (GCC) a través de un circuito de ExpressRoute de Azure Gobierno de EE. UU.?

Sí. Los puntos de conexión de servicio de Office 365 GCC son accesibles a través de hello Azure US Government ExpressRoute. Sin embargo, se primera necesidad tooopen compatibilidad vale en Hola prefijos de hello tooprovide portal Azure piensa tooadvertise tooMicrosoft. Los servicios GCC 365 tooOffice de conectividad se establecerán después de que se resuelve la incidencia de soporte técnico de Hola. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>¿Se puede acceder a Dynamics 365 for Operations (antes conocido como Dynamics AX Online) mediante una conexión ExpressRoute?

Sí. [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) se hospeda en Azure. Puede habilitar pares públicos de Azure en su tooit tooconnect de circuito de ExpressRoute.

## <a name="route-filters-for-microsoft-peering"></a>Filtros de ruta para el emparejamiento de Microsoft

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>¿Estoy encendido de emparejamiento de Microsoft para hello primera vez, qué rutas se vea?

No verá ninguna. Deberá tooattach un filtro tooyour circuito toostart prefijo de anuncios de ruta. Para consultar las instrucciones, vea [Configuración de filtros de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>Activa en el emparejamiento de Microsoft y ahora estoy tooselect tratar de Exchange Online, pero es darme un error que no estoy toodo autorizado se.

Cuando se usan filtros de ruta, cualquier cliente puede activar el emparejamiento de Microsoft. Sin embargo, para consumir servicios de Office 365, necesitará tooget autorizado por Office 365.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>¿Necesita autorización tooget para activar Dynamics 365 a través de emparejamiento de Microsoft?

No, no necesita autorización para Dynamics 365. Puede crear una regla y seleccionar la comunidad de Dynamics 365 sin autorización.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Ya tengo un emparejamiento de Microsoft, ¿cómo puedo aprovechar los filtros de ruta?

Puede crear un filtro de ruta, seleccione Hola servicios que desee toouse, adjunta Hola emparejamiento de Microsoft de tooyour de filtro. Para consultar las instrucciones, vea [Configuración de filtros de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>Tengo Microsoft emparejamiento en una ubicación, ahora estoy tratando de tooenable en otra ubicación y no se ven todos los prefijos.

* Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft, incluso si no se definen los filtros de ruta.

* Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito. No verá los prefijos de forma predeterminada.
