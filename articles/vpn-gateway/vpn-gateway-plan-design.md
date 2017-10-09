---
title: "Planeamiento y diseño de conexiones entre sitios locales: Azure VPN Gateway | Microsoft Docs"
description: "Obtenga información acerca del planeamiento y diseño de VPN Gateway para conexiones entre sitios locales, híbridos y entre redes virtuales"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>Planeamiento y diseño de VPN Gateway

Planear y diseñar configuraciones entre sitios locales y entre redes virtuales puede resultar simple o complejo, según las necesidades de la red. Este artículo le guía a través de las consideraciones de diseño y planeamiento básicas.

## <a name="planning"></a>Planeamiento

### <a name="compare"></a>Opciones de conectividad entre locales

Si desea que tooconnect local de forma segura sitios tooa de red virtual, por lo que tiene tres toodo de maneras diferentes: sitio a sitio, punto a sitio y ExpressRoute. Comparar conexiones entre entornos diferentes de Hola que están disponibles. opción de Hola que elija puede depender de diversas consideraciones, como:

* ¿Qué tipo de rendimiento requiere la solución?
* ¿Desea toocommunicate sobre Hola red pública de Internet a través de VPN segura, o a través de una conexión privada?
* ¿Tiene un toouse disponible de dirección IP pública?
* ¿Piensa toouse un dispositivo VPN? Si es así, ¿es compatible?
* ¿Va a conectar solo algunos equipos o desea establecer una conexión persistente para su sitio?
* ¿Qué tipo de puerta de enlace VPN es necesario para la solución de hello desea toocreate?
* ¿Qué SKU de puerta de enlace se debe usar?

### <a name="planningtable"></a>Tabla de planeación

Hello en la tabla siguiente puede ayudarle a decidir la mejor opción de conectividad hello para la solución.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>SKU de puerta de enlace

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>Flujo de trabajo

Hello siguiente lista se describen Hola flujo de trabajo común para la conectividad de la nube:

1. Diseño y plan de que espacios de la dirección de Hola de topología y la lista de conectividad para todas las redes desean tooconnect.
2. Cree una red virtual de Azure. 
3. Crear una puerta de enlace VPN para la red virtual de Hola.
4. Crear y configurar las redes de tooon locales de las conexiones u otras redes virtuales (según sea necesario).
5. Cree y configure una conexión de punto a sitio para su puerta de enlace de Azure VPN Gateway (según sea necesario).

## <a name="design"></a>Diseño
### <a name="topologies"></a>Topologías de conexión

Comience por mirar diagramas Hola Hola [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md) artículo. artículo de Hello contiene diagramas básicos, modelos de implementación de Hola para cada topología y las herramientas de implementación disponibles hello toodeploy puede usar la configuración.

### <a name="designbasics"></a>Conceptos básicos del diseño

Hola siguientes secciones describe conceptos básicos de puerta de enlace VPN de Hola. 

#### <a name="servicelimits"></a>Límites de servicios de red

Desplácese por hello tablas tooview [límites de servicios de red](../azure-subscription-service-limits.md#networking-limits). límites de Hello mencionados pueden afectar a su diseño.

#### <a name="subnets"></a>Acerca de las subredes

Al crear conexiones, debe tener en cuenta los intervalos de subred. Los intervalos de direcciones de subred no se pueden superponer. Una subred que se superpone es cuando una ubicación local o de red virtual contiene hello contiene el mismo espacio de direcciones que Hola a otra ubicación. Esto significa que necesita a los ingenieros de red para su toocarve de redes de instalaciones locales fuera de un intervalo para toouse para la IP de Azure direccionamiento espacio/subredes. Necesita espacio de direcciones que no se está utilizando en red de hello en instalaciones locales.

También es importante evitar las subredes superpuestas cuando se trabaja con conexiones entre redes virtuales. Si se superponen las subredes y una dirección IP existe en el envío de Hola y redes virtuales de destino, las conexiones de red virtual a red virtual producirá un error. Azure no puede enrutar Hola datos toohello otra VNet como dirección de destino de hello forma parte de hello envío de red virtual.

Las puertas de enlace de VPN requieren una subred específica llamada subred de puerta de enlace. Todas las subredes de puerta de enlace deben denominarse GatewaySubnet toowork correctamente. Asegúrese de no tooname la subred de puerta de enlace de otro nombre y no implementar máquinas virtuales o la subred de puerta de enlace de toohello nada. Consulte [Subredes de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsub).

#### <a name="local"></a>Acerca de las puertas de enlace de red local

puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local. En el modelo de implementación clásica de hello, puerta de enlace de red local de hello es tooas que se hace referencia un sitio de red Local. Cuando se configura una puerta de enlace de red local, asígnele un nombre, especifique la dirección IP pública de hello de dispositivo VPN de hello local y especificar los prefijos de dirección de Hola que estén en la ubicación local de Hola. Azure examina prefijos de dirección de destino de hello para el tráfico de red, consulta configuración Hola que ha especificado para la puerta de enlace de red local de Hola y enruta paquetes según corresponda. Puede modificar los prefijos de direcciones de hello según sea necesario. Para más información, consulte [Puertas de enlace de red](vpn-gateway-about-vpn-gateway-settings.md#lng).

#### <a name="gwtype"></a>Acerca de los tipos de puerta de enlace

Seleccionar tipo de puerta de enlace correcto de hello para la topología es fundamental. Si selecciona un tipo incorrecto hello, la puerta de enlace no funcionará correctamente. tipo de puerta de enlace de Hello especifica cómo se conecta Hola puerta de enlace y un valor de configuración necesarios para el modelo de implementación del Administrador de recursos de Hola.

tipos de puerta de enlace de Hello son:

* VPN
* ExpressRoute

#### <a name="connectiontype"></a>Acerca de los tipos de conexión

Cada configuración requiere un tipo de conexión específico. tipos de conexión de Hello son:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>Acerca de los tipos de VPN

Cada configuración requiere un tipo específico de VPN específico. Si combina dos configuraciones, como la creación de una conexión de sitio a sitio y un toohello de conexión de punto a sitio misma red virtual, debe usar un tipo VPN que cumple los requisitos de conexión.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Hello en las tablas siguientes muestran Hola VPN tipo tal y como se asigna la configuración de conexión de tooeach. Asegúrese de hello seguro de tipo VPN para la configuración de Hola de coincidencias de puerta de enlace que desea toocreate. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>Dispositivos VPN para conexiones de sitio a sitio

conexión de tooconfigure un sitio a sitio, independientemente del modelo de implementación, debe Hola siguientes elementos:

* Un dispositivo VPN compatible con Azure VPN Gateway.
* Una dirección IP IPv4 pública que no se encuentre detrás de un NAT.

Necesita experiencia toohave configurar el dispositivo VPN, o bien pedirle a alguien que puede configurar automáticamente dispositivos de Hola.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>Considerar el enrutamiento de túnel forzado

La tunelización forzada se puede configurar en la mayoría de las configuraciones. Forzada permite redirigir o "forzar" todos los vinculado a Internet tráfico tooyour back-ubicación de local a través de un túnel VPN de sitio a sitio para inspección y auditoría de túnel. Se trata de un requisito de seguridad crítico en la mayoría de las directivas de las empresas de TI. 

Sin la tunelización forzada, tráfico de Internet desde las máquinas virtuales en Azure atravesará siempre desde la infraestructura de red de Azure directamente out toohello Internet, sin Hola opción tooallow se tooinspect o auditoría tráfico Hola. Acceso de Internet no autorizado puede provocar potencialmente la divulgación de tooinformation u otros tipos de infracciones de seguridad.

Ambos modelos de implementación permiten configurar una conexión de tunelización forzada mediante distintas herramientas. Para obtener más información, consulte [Configuración de la tunelización forzada](vpn-gateway-forced-tunneling-rm.md).

**Diagrama de tunelización forzada**

![Diagrama de tunelización forzada de Azure VPN Gateway](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>Pasos siguientes

Vea hello [preguntas más frecuentes de puerta de enlace de VPN](vpn-gateway-vpn-faq.md) y [acerca de la puerta de enlace VPN](vpn-gateway-about-vpngateways.md) artículos para toohelp de información más con el diseño.

Para obtener más información acerca de la configuración de puerta de enlace específica, consulte [Acerca de la configuración de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md).