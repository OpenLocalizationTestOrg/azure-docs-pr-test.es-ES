---
title: "Preguntas más frecuentes acerca de Azure ExpressRoute | Microsoft Docs"
description: "P+F de ExpressRoute contiene información sobre servicios de Azure compatibles, costes, datos y conexiones, SLA, proveedores y ubicaciones, ancho de banda e información técnica adicional."
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
ms.openlocfilehash: 39b79dce555ba1b57f48ca2b431c13b1c1e4d90b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-faq"></a>P+F de ExpressRoute

## <a name="what-is-expressroute"></a>¿Qué es ExpressRoute?

ExpressRoute es un servicio de Azure que permite crear conexiones privadas entre los centros de datos de Microsoft y la infraestructura local o en una instalación de coubicación. Las conexiones ExpressRoute no se realizan sobre una conexión a Internet pública, ofrecen una mayor confiabilidad, seguridad y velocidad con una menor latencia que las conexiones a Internet típicas.

### <a name="what-are-the-benefits-of-using-expressroute-and-private-network-connections"></a>¿Cuáles son las ventajas de usar ExpressRoute y conexiones de red privada?

Las conexiones ExpressRoute no pasan por la red pública de Internet. Ofrecen una mayor confiabilidad, seguridad y velocidad con una latencia menor y más coherente que las conexiones a Internet típicas. En algunos casos, el uso de conexiones ExpressRoute para transferir datos entre los dispositivos locales y Azure también puede aportar beneficios económicos importantes.

### <a name="where-is-the-service-available"></a>¿Dónde está disponible el servicio?

Consulte esta página para la ubicación del servicio y la disponibilidad: [Asociados y ubicaciones de ExpressRoute](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-to-connect-to-microsoft-if-i-dont-have-partnerships-with-one-of-the-expressroute-carrier-partners"></a>¿Cómo puedo usar ExpressRoute para conectarme a Microsoft si no tengo asociaciones con uno de los socios de operadores de ExpressRoute?

Puede seleccionar un operador regional y conexiones Ethernet por tierra a una de las ubicaciones del proveedor de intercambio compatible. A continuación, puede explorar con Microsoft en la ubicación del proveedor. Compruebe la última sección de [Asociados y ubicaciones de ExpressRoute](expressroute-locations.md) para ver si su proveedor de servicio está presente en cualquiera de las ubicaciones de Exchange. A continuación, puede solicitar un circuito ExpressRoute a través del proveedor de servicio para conectarse a Azure.

### <a name="how-much-does-expressroute-cost"></a>¿Cuánto cuesta ExpressRoute?

Para obtener más información sobre los precios, consulte [Información sobre el precio](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-the-vpn-connection-i-purchase-from-my-network-service-provider-have-to-be-the-same-speed"></a>Si pago por un circuito ExpressRoute de un ancho de banda determinado, ¿la conexión VPN que adquiero de mi proveedor de servicios de red debe tener la misma velocidad?

No. Puede adquirir una conexión VPN de cualquier velocidad de su proveedor de servicios. Sin embargo, la conexión a Azure se limitará al ancho de banda de circuito ExpressRoute que compre.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-the-ability-to-burst-up-to-higher-speeds-if-necessary"></a>Si pago por un circuito ExpressRoute de un ancho de banda determinado, ¿puedo aumentar la velocidad si quiero?

Sí. Los circuitos ExpressRoute están configurados para aumentar hasta dos veces el límite de ancho de banda adquirido sin coste adicional. Consulte con su proveedor de servicios para ver si son compatibles con esta capacidad.

### <a name="can-i-use-the-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>¿Es posible usar la misma conexión de red privada con Red virtual y otros servicios de Azure simultáneamente?

Sí. Un circuito ExpressRoute, una vez configurado, le permitirá acceder a los servicios de una red virtual y a otros servicios de Azure simultáneamente. Se conectará a redes virtuales a través de la ruta de acceso de emparejamiento privado y a otros servicios a través de la ruta de acceso de emparejamiento público.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>¿ExpressRoute ofrece un contrato de nivel de servicio (SLA)?

Para más información, vea la página del [contrato de nivel de servicio de ExpressRoute](https://azure.microsoft.com/support/legal/sla/).

## <a name="supported-services"></a>Servicios admitidos

ExpressRoute admite [tres dominios de enrutamiento](expressroute-circuit-peerings.md) para diversos tipos de servicios.

### <a name="private-peering"></a>Emparejamiento privado

* Virtual Networks, que incluye todas las máquinas virtuales y servicios en la nube.

### <a name="public-peering"></a>Emparejamiento público

* Power BI
* Dynamics 365 for Finance and Operations (conocido anteriormente como Dynamics AX Online)
* La mayoría de los servicios de Azure salvo algunas excepciones siguientes:
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

### <a name="are-there-limits-on-the-amount-of-data-that-i-can-transfer-using-expressroute"></a>¿Hay límites en la cantidad de datos que se puede transferir mediante ExpressRoute?

No se establece un límite sobre la cantidad de transferencia de datos. Consulte [Información de precios](https://azure.microsoft.com/pricing/details/expressroute/) para obtener información sobre las tasas de ancho de banda.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>¿Qué velocidades de conexión son compatibles con ExpressRoute?

Ofertas de ancho de banda compatibles:

50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, 10 Gbps

### <a name="which-service-providers-are-available"></a>¿Qué proveedores de servicio están disponibles?

Consulte [Asociados y ubicaciones de ExpressRoute](expressroute-locations.md) para obtener la lista de proveedores de servicios y ubicaciones.

## <a name="technical-details"></a>Detalles técnicos

### <a name="what-are-the-technical-requirements-for-connecting-my-on-premises-location-to-azure"></a>¿Cuáles son los requisitos técnicos para la conexión de mi ubicación local a Azure?

Consulte la [página de requisitos previos de ExpressRoute](expressroute-prerequisites.md) para conocer los requisitos.

### <a name="are-connections-to-expressroute-redundant"></a>¿Son las conexiones a ExpressRoute redundantes?

Sí. Cada circuito ExpressRoute tiene un par redundante de conexiones cruzadas configuradas para proporcionar una alta disponibilidad.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>¿Se pierde conectividad si se produce un error en uno de mis vínculos de ExpressRoute?

No perderá conectividad si se produce un error en una de las conexiones cruzadas. Una conexión redundante está disponible para admitir la carga de la red. Asimismo, puede crear varios circuitos en una ubicación de emparejamiento diferente para lograr resistencia frente a errores.

### <a name="onep2plink"></a>Si no estoy en una ubicación compartida en un intercambio en la nube y mi proveedor de servicios ofrece una conexión punto a punto, ¿necesito solicitar dos conexiones físicas entre mi red local y Microsoft?

Si su proveedor de servicios puede establecer dos circuitos virtuales de Ethernet sobre la conexión física, solo necesita una conexión física. La conexión física (por ejemplo, una fibra óptica) se termina en un dispositivo de capa 1 (L1) (consulte la imagen). Los dos circuitos virtuales de Ethernet se etiquetan con id. de VLAN distintos, uno para el circuito principal y otro para el secundario. Esos id. de VLAN están en el encabezado Ethernet 802.1Q externo. El encabezado Ethernet 802.1Q interno (que no se muestra) está asignado a un [dominio de enrutamiento ExpressRoute](expressroute-circuit-peerings.md) específico.

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-to-azure-using-expressroute"></a>¿Puedo extender una de mis VLAN a Azure mediante ExpressRoute?

No. No admitimos ampliaciones de conectividad de la capa 2 en Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>¿Se puede disponer de más de un circuito ExpressRoute en mi suscripción?

Sí. Puede disponer de más de un circuito ExpressRoute en su suscripción. El límite predeterminado se establece en 10. Puede ponerse en contacto con Soporte técnico de Microsoft para aumentar el límite si es necesario.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>¿Es posible tener circuitos ExpressRoute de otros proveedores de servicios?

Sí. Puede tener circuitos ExpressRoute de muchos otros proveedores de servicios. Cada circuito ExpressRoute estará asociado solo a un proveedor de servicios. 

### <a name="can-i-have-multiple-expressroute-circuits-in-the-same-location"></a>¿Puede haber varios circuitos ExpressRoute en la misma ubicación?

Sí. Puede haber varios circuitos ExpressRoute, con los mismos o distintos proveedores de servicio, en la misma ubicación. Sin embargo, no puede vincular más de un circuito ExpressRoute a la misma red virtual desde la misma ubicación.

### <a name="how-do-i-connect-my-virtual-networks-to-an-expressroute-circuit"></a>¿Cómo conecto mis redes virtuales a un circuito ExpressRoute?

Los pasos básicos son:

* Establecer un circuito ExpressRoute y que el proveedor de servicios lo habilite.
* Usted o el proveedor deben configurar los emparejamientos BGP.
* Vincular la red virtual al circuito ExpressRoute.

Para obtener más información, vea [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>¿Hay límites de conectividad para mi circuito ExpressRoute?

Sí. El artículo [Asociados y ubicaciones de ExpressRoute](expressroute-locations.md) proporciona una visión general de los límites de conectividad para un circuito ExpressRoute. La conectividad de un circuito ExpressRoute está limitada a una única región geopolítica. La conectividad puede ampliarse a regiones geopolíticas cruzadas habilitando la característica Premium de ExpressRoute.

### <a name="can-i-link-to-more-than-one-virtual-network-to-an-expressroute-circuit"></a>¿Se puede vincular más de una red virtual a un circuito ExpressRoute?

Sí. Puede haber hasta 10 conexiones de redes virtuales en un circuito ExpressRoute estándar y hasta 100 en un [circuito ExpressRoute premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-to-a-single-expressroute-circuit"></a>Tengo varias suscripciones a Azure que contienen redes virtuales. ¿Es posible conectar redes virtuales de diferentes suscripciones a un solo circuito ExpressRoute?

Sí. Puede autorizar hasta otras 10 suscripciones de Azure para usar un único circuito ExpressRoute. Este límite puede aumentarse al habilitar la característica Premium de ExpressRoute.

Para obtener más información, vea [Uso compartido de un circuito ExpressRoute a través de varias suscripciones](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-to-the-same-circuit-isolated-from-each-other"></a>¿Las redes virtuales se conectan al mismo circuito aislado entre sí?

No. Todas las redes virtuales vinculadas al mismo circuito ExpressRoute forman parte del mismo dominio de enrutamiento y no están aisladas entre sí desde una perspectiva de enrutamiento. Si necesita aislamiento de rutas, deberá crear un circuito ExpressRoute independiente.

### <a name="can-i-have-one-virtual-network-connected-to-more-than-one-expressroute-circuit"></a>¿Se puede conectar una red virtual a más de un circuito ExpressRoute?

Sí. Puede vincular una única red virtual única con hasta cuatro circuitos ExpressRoute. Se deben solicitar mediante cuatro [ubicaciones de ExpressRoute](expressroute-locations.md) diferentes.

### <a name="can-i-access-the-internet-from-my-virtual-networks-connected-to-expressroute-circuits"></a>¿Es posible obtener acceso a Internet desde mis redes virtuales conectadas a circuitos ExpressRoute?

Sí. Si no ha anunciado rutas predeterminadas (0.0.0.0/0) o prefijos de rutas de Internet a través de la sesión BGP, podrá conectarse a Internet desde una red virtual vinculada a un circuito ExpressRoute.

### <a name="can-i-block-internet-connectivity-to-virtual-networks-connected-to-expressroute-circuits"></a>¿Es posible bloquear la conectividad a Internet a redes virtuales conectadas a circuitos ExpressRoute?

Sí. Puede anunciar rutas predeterminadas (0.0.0.0/0) para bloquear toda la conectividad de Internet a las máquinas virtuales implementadas en una red virtual y enrutar todo el tráfico de salida a través del circuito de ExpressRoute.

Si anuncia rutas predeterminadas, forzaremos el tráfico a los servicios ofrecidos a través del emparejamiento público (por ejemplo, Azure Storage y Base de datos SQL) de nuevo a sus instalaciones. Tendrá que configurar los enrutadores para devolver el tráfico a Azure a través de la ruta de acceso de emparejamiento público o Internet.

### <a name="can-virtual-networks-linked-to-the-same-expressroute-circuit-talk-to-each-other"></a>¿Las redes virtuales vinculadas al mismo circuito ExpressRoute pueden comunicarse entre sí?

Sí. Las máquinas virtuales implementadas en redes virtuales conectadas al mismo circuito ExpressRoute pueden comunicarse entre sí.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>¿Se puede usar conectividad de sitio a sitio para redes virtuales junto con ExpressRoute?

Sí. ExpressRoute puede coexistir con las VPN de sitio a sitio.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-to-use-expressroute"></a>¿Es posible mover una red virtual de una configuración de sitio a sitio/punto a sitio para usar ExpressRoute?

Sí. Tendrá que crear una puerta de enlace de ExpressRoute dentro de la red virtual. Habrá un breve tiempo de inactividad asociado al proceso.

### <a name="why-is-there-a-public-ip-address-associated-with-the-expressroute-gateway-on-a-virtual-network"></a>¿Por qué hay una dirección IP pública asociada a la puerta de enlace de ExpressRoute en una red virtual?

La dirección IP pública se usa solo para la administración interna. Esta dirección IP pública no está expuesta a Internet y no constituye un riesgo de seguridad de la red virtual.

### <a name="what-do-i-need-to-connect-to-azure-storage-over-expressroute"></a>¿Qué es necesario para conectarse a Almacenamiento de Azure a través de ExpressRoute?

Debe establecer un circuito ExpressRoute y configurar rutas para el intercambio de tráfico público.

### <a name="are-there-limits-on-the-number-of-routes-i-can-advertise"></a>¿Hay límites en el número de rutas que puedo anunciar?

Sí. Aceptamos hasta 4000 prefijos de enrutamientos para el intercambio privado y 200 de cada para el intercambio público y de Microsoft. Puede aumentarlo a 10.000 enrutamientos para el intercambio privado si habilita la característica Premium en ExpressRoute.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-the-bgp-session"></a>¿Existen restricciones en los intervalos IP que puedo anunciar durante la sesión BGP?

No se aceptan prefijos privados (RFC1918) en la sesión BGP entre pares públicos y de Microsoft.

### <a name="what-happens-if-i-exceed-the-bgp-limits"></a>¿Qué ocurre si supero los límites de BGP?

Se quitarán las sesiones BGP. Se restablecerán una vez que el recuento del prefijo esté por debajo del límite.

### <a name="what-is-the-expressroute-bgp-hold-time-can-it-be-adjusted"></a>¿Cuál es el tiempo de espera de BGP de ExpressRoute? ¿Se puede ajustar?

El tiempo de espera es 180. Los mensajes de Keep-Alive se envían cada 60 segundos. Hay configuración fija en el lado de Microsoft que no se puede cambiar. Es posible configurar temporizadores diferentes y los parámetros de la sesión BGP se negociarán según corresponda.

### <a name="after-i-advertise-the-default-route-00000-to-my-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-to-i-fix-this"></a>Después de anunciar la ruta predeterminada (0.0.0.0/0) a mis redes virtuales, no se puede activar Windows en las máquinas virtuales de Azure. ¿Cómo lo soluciono?

Los pasos siguientes ayudarán a Azure a reconocer la solicitud de activación:

1. Establezca el intercambio público para el circuito de ExpressRoute.
2. Realice una búsqueda DNS y busque la dirección IP de **kms.core.windows.net**
3. El Servicio de administración de claves debe reconocer que la solicitud de activación procede de Azure y seguir la solicitud. Realice una de las siguientes tres tareas:

   * En la red local, enrute el tráfico destinado a la dirección IP (obtenida en el paso 2) a Azure mediante el intercambio de tráfico público.
   * Haga que el proveedor NSP devuelva el tráfico a Azure a través de la interconexión pública.
   * Cree una ruta definida por el usuario que señale a esa dirección IP que tiene Internet como un próximo salto y aplíquela a las subredes que se encuentran estas máquinas virtuales.

### <a name="can-i-change-the-bandwidth-of-an-expressroute-circuit"></a>¿Es posible cambiar el ancho de banda de un circuito ExpressRoute?

Sí, puede intentar aumentar el ancho de banda del circuito ExpressRoute en Azure Portal o mediante PowerShell. Si el puerto físico en el que se creó el circuito tiene capacidad disponible, el cambio se realizará correctamente. 

Si el cambio no se realiza correctamente, significa que no queda capacidad en el puerto actual y que es preciso crear un circuito ExpressRoute nuevo con mayor ancho de banda O que no hay capacidad adicional en dicha ubicación, en cuyo caso no se podrá aumentar el ancho de banda. 

También tendrá que realizar un seguimiento con su proveedor de conectividad para asegurarse de que actualizan los aceleradores en sus redes para admitir el aumento del ancho de banda. Sin embargo, no se puede reducir el ancho de banda de su circuito ExpressRoute. Tendrá que crear un nuevo circuito ExpressRoute con menor ancho de banda y eliminar el circuito anterior.

### <a name="how-do-i-change-the-bandwidth-of-an-expressroute-circuit"></a>¿Cómo se cambia el ancho de banda de un circuito ExpressRoute?

Puede actualizar el ancho de banda del circuito ExpressRoute mediante el cmdlet de PowerShell o la API de REST.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>¿Qué es ExpressRoute Premium?

ExpressRoute Premium es una colección de las siguientes características:

* Aumento del límite de la tabla de enrutamiento de 4000 rutas a 10 000 rutas para el emparejamiento privado.
* Mayor número de redes virtuales que puede conectarse al circuito ExpressRoute (el valor predeterminado es 10). Para más información, consulte la tabla [Límites de ExpressRoute](#limits).
* Conectividad con Office 365 y Dynamics 365.
* Conectividad global a través de la red principal de Microsoft. Ahora podrá vincular una red virtual en una región geopolítica con un circuito ExpressRoute en otra región.<br>
    **Ejemplos:**

    *  Puede vincular una red virtual creada en Europa occidental a un circuito ExpressRoute creado en Silicon Valley. 
    *  En el emparejamiento público, los prefijos de otras regiones geopolíticas se anuncian de forma que sea posible conectarse, por ejemplo, a SQL Azure en Europa occidental desde un circuito en Silicon Valley.


### <a name="limits"></a>¿Cuántas redes virtuales puedo vincular a un circuito ExpressRoute si habilito ExpressRoute Premium?

Las tablas siguientes muestran los límites de ExpressRoute y el número de redes virtuales por circuito de ExpressRoute:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>¿Cómo habilito ExpressRoute Premium?

Las características de ExpressRoute Premium pueden habilitarse cuando la característica está habilitada y se puede apagar actualizando el estado del circuito. Puede habilitar ExpressRoute Premium en tiempo de creación de circuito o puede llamar al cmdlet de PowerShell o a la API de REST.

### <a name="how-do-i-disable-expressroute-premium"></a>¿Cómo deshabilito ExpressRoute Premium?

Puede deshabilitar ExpressRoute Premium si llama a la API de REST o al cmdlet de PowerShell. Debe asegurarse de que ha escalado sus necesidades de conectividad para cumplir con los límites predeterminados antes de deshabilitar ExpressRoute premium. Se producirá un error en la solicitud para deshabilitar ExpressRoute Premium si se realiza la escalación de uso más allá de los límites predeterminados.

### <a name="can-i-pick-and-choose-the-features-i-want-from-the-premium-feature-set"></a>¿Puedo elegir y seleccionar las características que quiero del conjunto de características Premium?

Nº No puede seleccionar las características. Habilitaremos todas las características cuando active ExpressRoute Premium.

### <a name="how-much-does-expressroute-premium-cost"></a>¿Cuánto cuesta ExpressRoute Premium?

Consulte [Información de precios](https://azure.microsoft.com/pricing/details/expressroute/) para ver el coste.

### <a name="do-i-pay-for-expressroute-premium-in-addition-to-standard-expressroute-charges"></a>¿Debo pagar ExpressRoute Premium además de la tarifa de ExpressRoute Standard?

Sí. Las tarifas de ExpressRoute Premium se aplican a las tarifas de circuito ExpressRoute y a las tarifas que precisa el proveedor de conectividad de mayor nivel.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute para Office 365 y Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-to-connect-to-office-365-services-and-dynamics-365"></a>¿Cómo se puede crear un circuito ExpressRoute para conectarse a servicios de Office 365 y Dynamics 365?

1. Revise la [página de requisitos previos de ExpressRoute](expressroute-prerequisites.md) para asegurarse de que se cumplen los requisitos.
2. Revise la lista de proveedores de servicios y las ubicaciones en el artículo [Asociados y ubicaciones de ExpressRoute](expressroute-locations.md) para asegurarse de que se cumplen sus necesidades de conectividad.
3. Planee los requisitos de capacidad revisando [Planificación de red y ajuste de rendimiento de Office 365](http://aka.ms/tune/).
4. Siga los pasos indicados en los flujos de trabajo para configurar la conectividad: [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md).

> [!IMPORTANT]
> Asegúrese de que habilitó el complemento de ExpressRoute premium al configurar la conectividad con los servicios de Office 365 y Dynamics 365.
> 
> 

### <a name="do-i-need-to-enable-azure-public-peering-to-connect-to-office-365-services-and-dynamics-365"></a>¿Es necesario habilitar emparejamientos públicos de Azure para conectarse a los servicios de Office 365 y Dynamics 365?

No, solo necesita habilitar Emparejamiento de Microsoft. El tráfico de autenticación a Azure AD se enviará a través de Emparejamiento de Microsoft. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-to-office-365-services-and-dynamics-365"></a>¿Pueden mis circuitos ExpressRoute existentes ser compatibles con la conectividad a los servicios de Office 365 y Dynamics 365?

Sí. El circuito ExpressRoute existente puede configurarse para admitir conectividad con los servicios de Office 365. Asegúrese de que tiene suficiente capacidad para conectarse a servicios de Office 365 y de que habilitó el complemento premium. [Planificación de red y ajuste del rendimiento de Office 365](http://aka.ms/tune/) le ayudará a planificar sus necesidades de conectividad. Además, vea [Creación y modificación de un circuito ExpressRoute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>¿A qué servicios de Office 365 se puede acceder a través de la conexión ExpressRoute?

Consulte la página [URL de Office 365 e intervalos de direcciones IP](http://aka.ms/o365endpoints) para obtener una lista actualizada de los servicios compatibles con ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>¿Cuánto cuesta ExpressRoute para servicios de Office 365 y Dynamics 365?

Servicios de Office 365 y Dynamics 365 requiere que el complemento premium esté habilitado. Consulte la [página de detalles de precios](https://azure.microsoft.com/pricing/details/expressroute/) para conocer los costos.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>¿En qué regiones es compatible ExpressRoute para Office 365?

Vea [Asociados de ExpressRoute y ubicaciones](expressroute-locations.md) para obtener más información.

### <a name="can-i-access-office-365-over-the-internet-even-if-expressroute-was-configured-for-my-organization"></a>¿Es posible obtener acceso a Office 365 por Internet incluso si ExpressRoute se ha configurado ExpressRoute para mi organización?

Sí. Es posible obtener acceso a los extremos de servicio de Office 365 a través de Internet a pesar de que se haya configurado ExpressRoute para su red. Si está en una ubicación que está configurada para conectarse a servicios de Office 365 a través de ExpressRoute, se conectará a través de ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>¿Puedo acceder a servicios de Office 365 US Government Community (GCC) a través de un circuito de ExpressRoute de Azure Gobierno de EE. UU.?

Sí. Los puntos de conexión de servicio de Office 365 GCC son accesibles a través de ExpressRoute de Azure Gobierno de EE. UU. Sin embargo, primero debe abrir una incidencia de soporte técnico en Azure Portal para proporcionar los prefijos que se van a anunciar a Microsoft. La conectividad a los servicios de Office 365 GCC se establecerá después de resolver la incidencia de soporte técnico. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>¿Se puede acceder a Dynamics 365 for Operations (antes conocido como Dynamics AX Online) mediante una conexión ExpressRoute?

Sí. [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) se hospeda en Azure. Puede habilitar el emparejamiento público de Azure en su circuito de ExpressRoute para conectarse a él.

## <a name="route-filters-for-microsoft-peering"></a>Filtros de ruta para el emparejamiento de Microsoft

### <a name="i-am-turning-on-microsoft-peering-for-the-first-time-what-routes-will-i-see"></a>Estoy activando el emparejamiento de Microsoft por primera vez, ¿qué rutas veré?

No verá ninguna. Tiene que adjuntar un filtro de ruta para el circuito para iniciar los anuncios de prefijo. Para consultar las instrucciones, vea [Configuración de filtros de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-to-select-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-to-do-it"></a>He activado el emparejamiento de Microsoft y ahora estoy intentando seleccionar Exchange Online, pero se genera un error que indica que no estoy autorizado para hacerlo.

Cuando se usan filtros de ruta, cualquier cliente puede activar el emparejamiento de Microsoft. Sin embargo, para consumir servicios de Office 365, debe obtener aún una autorización de Office 365.

### <a name="do-i-need-to-get-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>¿Es necesario obtener autorización para activar Dynamics 365 a través del emparejamiento de Microsoft?

No, no necesita autorización para Dynamics 365. Puede crear una regla y seleccionar la comunidad de Dynamics 365 sin autorización.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Ya tengo un emparejamiento de Microsoft, ¿cómo puedo aprovechar los filtros de ruta?

Puede crear un filtro de ruta, seleccionar los servicios que desee usar y adjuntar el filtro al emparejamiento de Microsoft. Para consultar las instrucciones, vea [Configuración de filtros de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-to-enable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>Tengo un emparejamiento de Microsoft en una ubicación, ahora estoy intentando habilitarlo en otra ubicación y no veo los prefijos.

* Se anunciarán todos los prefijos de servicio para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron antes del 1 de agosto de 2017, incluso si no se definen filtros de ruta.

* No se anunciará ningún prefijo para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron el 1 de agosto de 2017 o con posterioridad, hasta que se asocie un filtro de ruta al circuito. No verá los prefijos de forma predeterminada.
