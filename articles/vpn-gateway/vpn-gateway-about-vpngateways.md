---
title: "Información general sobre la puerta de enlace VPN: Crear conexiones de VPN entre entornos redes virtuales tooAzure | Documentos de Microsoft"
description: "Esta información general sobre la puerta de enlace VPN explica Hola formas tooconnect tooAzure redes virtuales mediante una conexión VPN a través de Internet de Hola. Se incluyen los diagramas de las configuraciones de conexión básica."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>Acerca de Puerta de enlace de VPN

Una puerta de enlace VPN es un tipo de puerta de enlace de red virtual que envía tráfico no cifrado a través de una conexión pública tooan ubicación local. También puede utilizar el tráfico de toosend cifrado de las puertas de enlace VPN entre redes virtuales de Azure a través de red de Microsoft de Hola. toosend cifrado el tráfico de red entre su red virtual de Azure y el sitio local, debe crear una puerta de enlace VPN para la red virtual.

Cada red virtual puede tener sólo una puerta de enlace VPN, sin embargo, puede crear varias de las conexiones toohello misma puerta de enlace VPN. Un ejemplo de esto es una configuración de conexión multisitio. Cuando crea varios toohello conexiones misma puerta de enlace VPN, todos los túneles VPN, incluidas Point-to-Site VPN, ancho de banda de Hola de recurso compartido que está disponible para la puerta de enlace de Hola.

### <a name="whatis"></a>¿Qué es una puerta de enlace de red virtual?

Una puerta de enlace de red virtual se compone de dos o más máquinas virtuales que están implementadas subred específica tooa llamado hello GatewaySubnet. las máquinas virtuales que se encuentran en hello GatewaySubnet se crean al crear puerta de enlace de red virtual de Hola Hola. Puerta de enlace de red virtual las máquinas virtuales son tablas de enrutamiento configurado toocontain y puerta de enlace de toohello específico de servicios de puerta de enlace. No se puede configurar directamente hello las máquinas virtuales que forman parte de la puerta de enlace de red virtual de Hola y nunca debe implementar toohello GatewaySubnet de recursos adicionales.

Cuando se crea una puerta de enlace de red virtual con el tipo de puerta de enlace de hello 'Vpn', crea un tipo específico de puerta de enlace de red virtual que cifra el tráfico; una puerta de enlace VPN. Una puerta de enlace VPN puede tardar hasta too45 minutos toocreate. Esto se debe hello las máquinas virtuales de puerta de enlace VPN de Hola se están implementado toohello GatewaySubnet y configurado con las opciones de Hola que especificó. Hola SKU de puerta de enlace que seleccione determina cómo eficaz hello las máquinas virtuales son.

## <a name="gwsku"></a>SKU de puerta de enlace

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>Configuración de una instancia de VPN Gateway

Una conexión de puerta de enlace de VPN se basa en varios recursos con una configuración específica. La mayoría de los recursos de hello puede configurarse por separado, aunque se deben configurar en un orden determinado en algunos casos.

### <a name="settings"></a>Configuración

configuración de Hola que eligió para cada recurso es crítico toocreating una conexión correcta. Para más información sobre los recursos individuales y la configuración de VPN Gateway, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md). artículo de Hello contiene toohelp información comprender tipos de puerta de enlace, tipos de VPN, tipos de conexión, subredes de puerta de enlace, las puertas de enlace de red local y otras configuraciones recursos que puede que desee tooconsider.

### <a name="tools"></a>Herramientas de implementación

Puede empezar a crear y configurar los recursos mediante una herramienta de configuración, como Hola portal de Azure. Más adelante puede decidir tooswitch tooanother herramienta, como PowerShell, tooconfigure recursos adicionales, o modificar los recursos existentes cuando sea aplicable. Actualmente, no se puede configurar cada recurso y la configuración del recurso en hello portal de Azure. instrucciones de Hello en los artículos de Hola para cada topología de conexión especifican cuando se necesita una herramienta de configuración específico. 

### <a name="models"></a>Modelo de implementación

Cuando se configura una puerta de enlace VPN, pasos de Hola que seguir dependen de modelo de implementación de hello usa toocreate la red virtual. Por ejemplo, si ha creado la red virtual mediante el modelo de implementación clásica de hello, utilizar instrucciones de Hola y las instrucciones de implementación clásica de hello toocreate de modelo y configuración la configuración de puerta de enlace VPN. Para más información sobre los modelos de implementación, consulte [Descripción de los modelos de implementación clásica y de Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="diagrams"></a>Diagramas de la topología de conexión

Es importante tooknow que hay distintas configuraciones disponibles para las conexiones de puerta de enlace VPN. Necesita toodetermine configuración que mejor se adapte a sus necesidades. En las secciones de Hola a continuación, puede ver diagramas de topología y obtener información sobre Hola siguiendo las conexiones de puerta de enlace VPN: hello las secciones siguientes contiene las tablas que lista:

* Modelo de implementación disponible
* Herramientas de configuración disponibles
* Vínculos que llevan directamente tooan artículo, si está disponible

Utilice Hola diagramas y descripciones toohelp Hola seleccione conexión topología toomatch sus requisitos. Hello diagramas muestran Hola topologías principales de la línea de base, pero es posible toobuild configuraciones más complejas con diagramas de hello como guía.

## <a name="s2smulti"></a>Sitio a sitio y multisitio (túnel VPN de IPsec/IKE)

### <a name="S2S"></a>De sitio a sitio

Una conexión de puerta de enlace de VPN de sitio a sitio (S2S) es una conexión a través de un túnel VPN IPsec/IKE (IKEv1 o IKEv2). Una conexión de S2S requiere una VPN dispositivo situado en local que tiene un tooit dirección asignada de IP pública y no se encuentra detrás de un dispositivo NAT. Se pueden utilizar conexiones S2S para las configuraciones híbridas y entre locales.   

![Ejemplo de conexión de sitio a sitio de Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Multisitio

Este tipo de conexión es una variación de hello conexión de sitio a sitio. Crear más de una conexión VPN de la puerta de enlace de red virtual, normalmente conectando toomultiple sitios locales. Cuando trabaje con varias conexiones, debe usar una VPN de tipo RouteBased (conocida como puerta de enlace dinámica al trabajar con redes virtuales clásicas). Dado que cada red virtual solo puede tener una puerta de enlace VPN, todas las conexiones a través de puerta de enlace de hello comparten el ancho de banda disponible de Hola. A menudo, esto se llama conexión "multisitio".

![Ejemplo de conexión multisitio de Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Modelos de implementación y métodos para conexiones de sitio a sitio y multisitio

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Punto a sitio (VPN a través de SSTP)

Una puerta de enlace VPN de punto a sitio (P2S) le permite crear una red virtual de tooyour de conexión segura desde un equipo cliente individual. Las conexiones de VPN de sitio a punto son útiles cuando se desea tooconnect tooyour red virtual desde una ubicación remota, como cuando trabajan a distancia desde casa o una conferencia. Una VPN P2S también es un toouse solución útil en lugar de una VPN de sitio a sitio cuando hay solo unos clientes que necesitan tooconnect tooa red virtual. 

A diferencia de las conexiones S2S, las conexiones P2S no necesitan una dirección IP pública local ni dispositivos VPN. Se pueden utilizar con conexiones de S2S a través de conexiones de P2S Hola misma puerta de enlace VPN, siempre y cuando todos los requisitos de configuración de Hola para las conexiones son compatibles.

Usa P2S Hola Secure Socket de protocolo de túnel (SSTP), que es un protocolo VPN basada en SSL. Se establece una conexión VPN P2S, empiece por equipo de cliente de Hola.

![Ejemplo de conexión de punto a sitio de Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Métodos y modelos de implementación disponibles para conexiones de punto a sitio

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>Conexiones de red virtual a red virtual (túnel VPN de IPsec/IKE)

Conectar una red virtual (VNet a VNet) tooanother de red virtual es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE. Incluso puede combinar la comunicación de red virtual a red virtual con configuraciones de conexión multisitio. Esto permite establecer topologías de red que combinen la conectividad entre entornos con la conectividad entre redes virtuales.

Hola redes virtuales que se conecta puede ser:

* Hola mismo o en distintas regiones
* Hola suscripciones iguales o distintas 
* Hola modelos de implementación de la misma o distintas

![Azure ejemplo de conexión de red virtual de puerta de enlace de VPN tooVNet](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Conexiones entre modelos de implementación

Actualmente, Azure tiene dos modelos de implementación: el clásico y el de Resource Manager. Si lleva un tiempo usando Azure, es probable que tenga máquinas virtuales de Azure y roles de instancia que se ejecuten en una red virtual clásica. Es posible que sus máquinas virtuales e instancias de roles más recientes se estén ejecutando en una red virtual creada en Resource Manager. Puede crear una conexión entre Hola redes virtuales tooallow recursos hello en toocommunicate de una red virtual directamente con los recursos de otra.

### <a name="vnet-peering"></a>Emparejamiento de VNET

Es posible que pueda toouse la conexión de toocreate de emparejamiento de VNet siempre y cuando la red virtual cumple determinados requisitos. El emparejamiento de VNET no utiliza una puerta de enlace de red virtual. Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Modelos de implementación y métodos para conexiones de red virtual a red virtual

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (conexión privada dedicada)

Microsoft Azure ExpressRoute le permite ampliar sus redes locales en hello nube de Microsoft a través de una conexión privada dedicada que se realiza mediante un proveedor de conectividad. Con ExpressRoute, puede establecer conexiones tooMicrosoft servicios en la nube, como Microsoft Azure, Office 365 y CRM Online. La conectividad puede ser desde una red de conectividad universal (IP VPN), una red Ethernet de punto a punto, o una conexión cruzada virtual a través de un proveedor de conectividad en una instalación de ubicación compartida.

Las conexiones ExpressRoute no pasan por hello Internet pública. Esto permite toooffer las conexiones de ExpressRoute, más confiabilidad, velocidades más rápidas, latencias más bajas y mayor seguridad que las típicas conexiones a través de Internet de Hola.

Una conexión de ExpressRoute no utiliza una instancia de VPN Gateway, aunque lo use una puerta de enlace de red virtual como parte de su configuración obligatoria. En una conexión ExpressRoute, puerta de enlace de red virtual de Hola se configura con el tipo de puerta de enlace de hello 'ExpressRoute', en lugar de 'Vpn'. Para obtener más información sobre ExpressRoute, consulte hello [información general técnica de ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="coexisting"></a>Conexiones de sitio a sitio y de ExpressRoute coexistentes

ExpressRoute es una conexión directa y dedicada desde la WAN (no a través de Internet pública de Hola) tooMicrosoft servicios, incluido Azure. VPN de sitio a sitio tráfico viajan cifrará a través de hello Internet pública. Está tooconfigure capaz de conexiones VPN de sitio a sitio y ExpressRoute para la misma red virtual hello tiene varias ventajas.

Puede configurar una VPN de sitio a sitio como una ruta de acceso seguro de conmutación por error para ExpressRoute o usar VPN de sitio a sitio tooconnect toosites que no forman parte de la red, pero que están conectados a través de ExpressRoute. Tenga en cuenta que esta configuración requiere dos puertas de enlace de red virtual para Hola misma red virtual, uno con hello 'Vpn' de tipo de puerta de enlace y Hola sí mediante el tipo de puerta de enlace de hello 'ExpressRoute'.

![Ejemplo de conexiones coexistentes en ExpressRoute y VPN Gateway](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>Métodos y modelos de implementación disponibles para conexiones S2S y ExpressRoute

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Precios

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

Para más información acerca de las SKU de puerta de enlace para VPN Gateway, consulte [SKU de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="faq"></a>P+F

Para las preguntas más frecuentes acerca de la puerta de enlace VPN, consulte hello [preguntas más frecuentes de puerta de enlace de VPN](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Pasos siguientes

- Planee la configuración de puerta de enlace de VPN. Consulte [Planeamiento y diseño de VPN Gateway](vpn-gateway-plan-design.md).
- Hola de vista [preguntas más frecuentes de puerta de enlace de VPN](vpn-gateway-vpn-faq.md) para obtener información adicional.
- Hola de vista [subscripciones y límites de servicio](../azure-subscription-service-limits.md#networking-limits).
- Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md) de Azure.
