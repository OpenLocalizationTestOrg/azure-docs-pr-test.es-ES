---
title: aaaAzure red directrices de infraestructura - Linux | Documentos de Microsoft
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para la implementación de una red virtual en los servicios de infraestructura de Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7ebd5da-3c62-45e8-ad90-6c73a37ebeb1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3f49b135b1f9bca3fd463e9ff27299fb97908c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a>Directrices de infraestructura de red de Azure para máquinas virtuales Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

En este artículo se centra en hello descripción necesarios pasos de una red virtual dentro de Azure y la conectividad entre entornos locales existentes de planeación.

## <a name="implementation-guidelines-for-virtual-networks"></a>Directrices de implementación para las redes virtuales
Decisiones:

* ¿Qué tipo de red virtual ¿necesita toohost su infraestructura o la carga de trabajo de TI (solo en la nube o entre entornos)?
* Para las redes virtuales entre entornos, ¿cuánto espacio de direcciones de ¿necesita subredes de hello toohost y las máquinas virtuales ahora y para la expansión razonable en hello futuras?
* ¿Va toocreate centralizada redes virtuales o crea redes virtuales individuales para cada grupo de recursos?

Tareas:

* Defina el espacio de direcciones de Hola para hello redes virtuales toobe creado.
* Definir conjunto de Hola de subredes y espacio de direcciones de Hola para cada uno.
* Para las redes virtuales entre locales, definir conjunto de Hola de espacios de direcciones de red local para ubicaciones de local de Hola que Hola a las máquinas virtuales en tooreach de necesidad de red virtual de Hola.
* Trabajar con redes equipo tooensure Hola adecuado el enrutamiento se configura al crear a local entre entornos redes virtuales.
* Crear red virtual de hello con la convención de nomenclatura.

## <a name="virtual-networks"></a>Redes virtuales
Las redes virtuales son necesarios toosupport comunicaciones entre máquinas virtuales (VM). Puede definir subredes, direcciones IP personalizadas, configuración de DNS, filtrado de seguridad y equilibrio de carga, al igual que con redes físicas. Mediante el uso de un [puerta de enlace VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) o [circuito de Express Route](../../expressroute/expressroute-introduction.md), puede conectar redes locales de tooyour de redes virtuales de Azure. Lea más sobre [redes virtuales y sus componentes](../../virtual-network/virtual-networks-overview.md).

Al utilizar grupos de recursos, tendrá flexibilidad para diseñar los componentes de red virtual. Las máquinas virtuales pueden conectarse a redes toovirtual fuera de su propio grupo de recursos. Un enfoque de diseño común sería toocreate centralizada de grupos de recursos que contienen la infraestructura de red de núcleos que puede ser administrada por un equipo común. Las máquinas virtuales y sus aplicaciones implementan tooseparate grupos de recursos. Este enfoque permite el acceso propietarios de aplicaciones de grupo de recursos de toohello que contiene sus máquinas virtuales sin tener que abrir la configuración de acceso toohello de hello más ancho virtual recursos de red.

## <a name="site-connectivity"></a>Conectividad de sitio
### <a name="cloud-only-virtual-networks"></a>Redes virtual solo en la nube
Si los equipos y usuarios locales no requieren tooVMs de conectividad en curso en una red virtual de Azure, el diseño de red virtual es sencillo:

![Diagrama de red virtual básico solo en la nube](./media/infrastructure-networking-guidelines/vnet01.png)

Este enfoque está destinado a cargas de trabajo con conexión a Internet, como un servidor web basado en Internet. Puede administrar estas máquinas virtuales mediante SSH o conexiones VPN de punto a sitio.

Dado que no se conectan red de tooyour local, redes virtuales solo Azure pueden usar cualquier parte del espacio de direcciones IP privadas de Hola. espacio de direcciones de Hello puede ser Hola mismo espacio privado que se encuentra en usar local.

### <a name="cross-premises-virtual-networks"></a>Redes virtuales entre locales
Si los equipos y usuarios locales requieren tooVMs de conectividad en curso en una red virtual de Azure, crear una red virtual entre entornos. Conectar hello tooyour local red virtual con una ExpressRoute o una conexión de VPN de sitio a sitio.

![Diagrama de red virtual local](./media/infrastructure-networking-guidelines/vnet02.png)

En esta configuración, Hola red virtual de Azure es básicamente una extensión en la nube de su red local.

Dado que se conectan tooyour red local, redes virtuales deben utilizar una parte del espacio de direcciones de hello usado por su organización, que es único entre entornos. En hello mismo modo que diferentes ubicaciones corporativa se le asignó una subred IP específica, Azure se convierte en otra ubicación como ampliar la red.

tooallow tootravel de paquetes de la red de local de tooyour de red virtual entre locales, debe configurar conjunto Hola de prefijos de direcciones locales pertinentes como parte de la definición de red local de hello para la red virtual de Hola. Dependiendo de la dirección de hello espacio de hello hello y red conjunto de virtuales relevantes local ubicaciones, puede haber varios prefijos de direcciones de red local Hola.

Puede convertir una red virtual de red virtual solo en la nube tooa entre entornos, pero lo más probable es que requiere toore IP su espacio de direcciones de red virtual y los recursos de Azure. Por lo tanto, considere detenidamente si una red virtual debe red local de toobe tooyour conectado cuando se asigna una subred IP.

## <a name="subnets"></a>Subredes
Las subredes permiten tooorganize recursos que están relacionados, ya sea lógicamente (por ejemplo, una subred para las máquinas virtuales relacionados toohello misma aplicación), o físicamente (por ejemplo, una subred por grupo de recursos). o bien emplear técnicas de aislamiento de subred para ofrecer mayor seguridad.

Para las redes virtuales entre locales, debe diseñar subredes con hello mismas convenciones que utilizan para recursos locales. **Azure siempre utiliza Hola tres primeras direcciones IP Hola del espacio de direcciones para cada subred**. número de hello toodetermine de direcciones necesarias para la subred de hello, iniciar contando Hola número de máquinas virtuales que necesite ahora. Calcular el crecimiento futuro y, a continuación, usar hello después de tamaño de tabla toodetermine Hola de subred Hola.

| Número de máquinas virtuales necesario | Número de bits de host necesarios | Tamaño de subred Hola |
| --- | --- | --- |
| 1-3 |3 |/29 |
| 4-11 |4 |/28 |
| 12-27 |5 |/27 |
| 28-59 |6 |/26 |
| 60-123 |7 |/25 |

> [!NOTE]
> Para las subredes locales normal, número máximo de Hola de direcciones de host para una subred con los bits de host de n es 2<sup> n </sup> : 2. Para una subred de Azure, número máximo de Hola de direcciones de host para una subred con los bits de host de n es 2<sup> n </sup> – 5 (2 y 3 para las direcciones de Hola que Azure utiliza en cada subred).
> 
> 

Si elige un tamaño de subred es demasiado pequeño, tiene toore IP y volver a implementar las máquinas virtuales de hello en la subred de Hola.

## <a name="network-security-groups"></a>Grupos de seguridad de red
Puede aplicar filtrado tráfico de toohello de reglas que fluye a través de las redes virtuales mediante el uso de grupos de seguridad de red. Puede compilar toosecure de reglas de filtrado granular el entorno de red virtual, controlar entrantes y salientes tráfico, origen y destino intervalos IP, permitida puertos, etcetera. Grupos de seguridad de red puede ser toosubnets aplicado dentro de una red virtual o directamente tooa proporcionado la interfaz de red virtual. Es recomendable toohave cierto nivel de grupo de seguridad de red filtran el tráfico en las redes virtuales. Lea más sobre [Grupos de seguridad de red](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Componentes de red adicionales
Al igual que con una infraestructura de red física local, las redes virtuales de Azure pueden contener más que subredes y direcciones IP. Al diseñar la infraestructura de aplicación, puede que desee tooincorporate algunos de estos componentes adicionales:

* [Puertas de enlace VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -conectar redes virtuales de Azure tooother virtual de Azure redes o conectar las redes locales de tooon a través de una conexión VPN de sitio a sitio. Para disfrutar de una conectividad específica y segur, implemente conexiones ExpressRoute. También puede proporcionar a los usuarios acceso directo con conexiones VPN de punto a sitio.
* [Equilibrador de carga](../../load-balancer/load-balancer-overview.md) : proporciona equilibrio de carga del tráfico para el tráfico interno y externo, como se desee.
* [Puerta de enlace de aplicaciones](../../application-gateway/application-gateway-introduction.md) : HTTP equilibrio de carga en el nivel de aplicación Hola, proporciona algunas ventajas adicionales para las aplicaciones web en lugar de implementar Hola equilibrador de carga de Azure.
* [El Administrador de tráfico](../../traffic-manager/traffic-manager-overview.md) - basado en el DNS distribución toodirect los usuarios finales toohello más cercano disponible extremo de la aplicación, lo cual permite un toohost el tráfico de la aplicación fuera de los centros de datos de Azure en regiones diferentes.

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

