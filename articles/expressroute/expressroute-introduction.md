---
title: "Información general de ExpressRoute: Ampliar su tooAzure de red local a través de una conexión privada | Documentos de Microsoft"
description: "Esta introducción técnica de ExpressRoute explica cómo una conexión ExpressRoute funciona tooextend su tooAzure de red local a través de una conexión privada."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>Información general sobre ExpressRoute
Microsoft Azure ExpressRoute le permite ampliar sus redes locales en hello nube de Microsoft a través de una conexión privada que se realiza mediante un proveedor de conectividad. Con ExpressRoute, puede establecer conexiones tooMicrosoft servicios en la nube, como Microsoft Azure, Office 365 y Dynamics 365.

La conectividad puede ser desde una red de conectividad universal (IP VPN), una red Ethernet de punto a punto, o una conexión cruzada virtual a través de un proveedor de conectividad en una instalación de ubicación compartida. Las conexiones ExpressRoute no pasan por hello Internet pública. Esto permite toooffer las conexiones de ExpressRoute, más confiabilidad, velocidades más rápidas, latencias más bajas y mayor seguridad que las típicas conexiones a través de Internet de Hola. Para obtener información acerca de cómo tooconnect su tooMicrosoft de red con ExpressRoute, consulte [modelos de conectividad de ExpressRoute](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Ventajas principales

* Conectividad de capa 3 entre su red local y Hola Microsoft Cloud a través de un proveedor de conectividad. La conectividad puede ser desde una red de conectividad universal (IP VPN), una red Ethernet de punto a punto, o una conexión cruzada virtual a través de un intercambio de Ethernet.
* Servicios de nube de conectividad tooMicrosoft en todas las regiones de región geopolíticos Hola.
* Servicios de tooMicrosoft de conectividad global en todas las regiones con el complemento de premium de ExpressRoute.
* Enrutamiento dinámico entre la red y Microsoft a través de protocolos estándar del sector (BGP).
* Redundancia integrada en todas las ubicaciones de configuración entre pares para una mayor confiabilidad.
* El tiempo de actividad de conexión [SLA](https://azure.microsoft.com/support/legal/sla/).
* Compatibilidad con QoS de Skype para la empresa.

Para obtener más información, vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).

## <a name="features"></a>Características

### <a name="layer-3-connectivity"></a>Conectividad de nivel 3
Microsoft utiliza sector estándar dinámica enrutamiento protocol (BGP) tooexchange enruta entre su red local, las instancias de Azure y Microsoft direcciones públicas.  Establecemos varias sesiones BGP con su red para perfiles de tráfico diferentes. Pueden encontrar más detalles en hello [ExpressRoute circuito y dominios de enrutamiento](expressroute-circuit-peerings.md) artículo.

### <a name="redundancy"></a>Redundancia
Cada circuito ExpressRoute consta de dos conexiones tootwo Microsoft Enterprise enrutadores perimetrales (MSEEs) del proveedor de conectividad de Hola / su red perimetral. Microsoft requiere conexión dual de BGP de proveedor de conectividad de Hola / su lado: una tooeach MSEE. Puede elegir no toodeploy dispositivos redundantes / Ethernet circuitos en su extremo. Sin embargo, los proveedores de conectividad usan tooensure dispositivos redundantes que las conexiones se entregan tooMicrosoft de forma redundante. Una configuración de conectividad de capa 3 redundante es un requisito para nuestro [SLA](https://azure.microsoft.com/support/legal/sla/) toobe válido.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Servicios de conectividad tooMicrosoft en la nube
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Las conexiones ExpressRoute habilitar toohello de acceso siguientes servicios:

* Servicios de Microsoft Azure
* Servicios de Microsoft Office 365
* Microsoft Dynamics 365

Puede visitar hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) página para obtener una lista detallada de servicios admitidos a través de ExpressRoute.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Regiones de tooall de conectividad dentro de una región geopolíticas
Puede conectarse tooMicrosoft en uno de nuestros [ubicaciones emparejamiento](expressroute-locations.md) y tener acceso tooall regiones dentro de la región geopolíticos Hola. 

Por ejemplo, si conectados tooMicrosoft en Ámsterdam a través de ExpressRoute, tiene servicios de nube de Microsoft access tooall hospedados en Europa del Norte y Europa occidental. Vea hello [ExpressRoute asociados y las ubicaciones de emparejamiento](expressroute-locations.md) artículo para obtener información general de las regiones geopolíticas de hello, las áreas de la nube de Microsoft asociadas y correspondientes ubicaciones de emparejamiento de ExpressRoute.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Conectividad global con el complemento ExpressRoute Premium
Puede habilitar la conectividad del complemento característica tooextend de hello ExpressRoute premium a través de límites geopolíticos. Por ejemplo, si está conectado tooMicrosoft en Ámsterdam a través de ExpressRoute, tendrán servicios de nube de Microsoft access tooall hospedados en todas las regiones a través de Hola a todos (se excluyen las nubes nacionales). Puede tener acceso a los servicios implementados en Sudamérica o Australia Hola igual que tiene acceso a Hola Norte y regiones de Europa occidental.

### <a name="rich-connectivity-partner-ecosystem"></a>Ecosistema de socios de conectividad enriquecida
ExpressRoute tiene un ecosistema de proveedores de conectividad y asociados integradores de sistema en constante crecimiento. Puede hacer referencia a toohello [ExpressRoute ubicaciones y proveedores](expressroute-locations.md) artículo para obtener información más reciente de Hola.

### <a name="connectivity-toonational-clouds"></a>Nubes de toonational de conectividad
Microsoft administra entornos de nube aislados para regiones geopolíticas y segmentos de clientes especiales. Consulte toohello [ExpressRoute ubicaciones y proveedores](expressroute-locations.md) página para obtener una lista de nubes nacionales y proveedores.

### <a name="bandwidth-options"></a>Opciones de ancho de banda
Puede comprar los circuitos ExpressRoute para una amplia gama de anchos de banda. A continuación se enumera la lista de anchos de banda admitidos. Ser toocheck seguro con la lista de Hola de toodetermine de proveedor de conectividad de anchos de banda admitidos que proporcionan.

* 50 Mbps
* 100 Mbps
* 200 Mbps
* 500 Mbps
* 1 Gbps
* 2 Gbps
* 5 Gbps
* 10 Gbps

### <a name="dynamic-scaling-of-bandwidth"></a>Escalado dinámico del ancho de banda
Puede aumentar el ancho de banda del circuito de ExpressRoute de hello (de mejor forma posible) sin necesidad de tootear hacia abajo las conexiones. 

### <a name="flexible-billing-models"></a>Modelos flexibles de facturación
Puede elegir el modelo de facturación que mejor le convenga. Elegir entre los modelos de facturación de hello enumerados a continuación. Para obtener más información, vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).

* **Datos ilimitados**. Hola circuito de ExpressRoute se cobra según una cuota mensual y todas las transferencias de datos entrantes y salientes se incluye de forma gratuita de forma gratuita. 
* **Datos medidos**. Hola circuito de ExpressRoute se cobra según una cuota mensual. Todas las transferencias de datos de entrada son gratuitas. Las transferencias de datos de salida se cobran de acuerdo a un precio por GB de transferencia de datos. Las tasas de transferencia de datos varían según la región.
* **Complemento ExpressRoute Premium**. premium de Hello ExpressRoute es un complemento sobre Hola circuito de ExpressRoute. complemento de Hello ExpressRoute premium proporciona Hola siguientes capacidades: 
  * Límites de ruta mayor para Azure pública y Azure emparejamiento privado de 4.000 too10 de rutas, 000 rutas.
  * Conectividad global para los servicios. Un circuito de ExpressRoute creado en cualquier región (excepto las nubes nacionales) tendrán acceso tooresources en ninguna otra región de Hola a todos. Por ejemplo, un circuito ExpressRoute aprovisionado en Silicon Valley puede acceder a una red virtual creada en Europa occidental .
  * Aumento del número de vínculos de red virtual por circuito de ExpressRoute de límite mayor de 10 tooa, según el ancho de banda de Hola de circuito de Hola.

## <a name="faq"></a>P+F

Para las preguntas más frecuentes sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).

## <a name="next-steps"></a>Pasos siguientes

* Información acerca de los [Modelos de conectividad de ExpressRoute](expressroute-connectivity-models.md).
* Obtenga información acerca de las conexiones ExpressRoute y dominios de enrutamiento. Consulte [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).
* Busque un proveedor de servicios. Consulte [Asociados de ExpressRoute de Azure y ubicaciones de emparejamiento](expressroute-locations.md).
* Asegúrese de que se cumplen todos los requisitos previos. Consulte [Requisitos previos de ExpressRoute](expressroute-prerequisites.md).
* Consulte los requisitos de toohello para [enrutamiento](expressroute-routing.md), [NAT](expressroute-nat.md), y [QoS](expressroute-qos.md).
* Configure su conexión ExpressRoute.
  * [Creación de un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configuración del emparejamiento de un circuito ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
  * [Conectarse a un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-portal-resource-manager.md)
* Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md) de Azure.
