---
title: aaaOverview de configuraciones de alta disponibilidad con puertas de enlace de VPN de Azure | Documentos de Microsoft
description: "En este artículo se proporciona información general sobre las opciones de configuración de alta disponibilidad mediante instancias de Azure VPN Gateway."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Conectividad de alta disponibilidad entre locales y de red virtual a red virtual
En este artículo se proporciona información general sobre las opciones de configuración de alta disponibilidad para la conectividad entre locales y de red virtual a red virtual con instancias de Azure VPN Gateway.

## <a name = "activestandby"></a>Acerca de la redundancia de Azure VPN Gateway
Cada instancia de Azure VPN Gateway consta de dos instancias en una configuración activa-en espera. Para cualquier mantenimiento planeado o no planeada interrupción que se produce instancias activas de toohello, instancia de hello en espera se ocupe automáticamente (conmutación por error) y reanudar Hola VPN S2S o las conexiones de red virtual a red virtual. cambiar Hola producirá una breve interrupción. Para el mantenimiento planeado, se debe restaurar la conectividad de hello dentro de 10 segundos de too15. Para problemas no planeados, recuperar la conexión Hola será mayor, sobre too1 minuto 1 y una mitad minutos en el peor de los casos Hola. Para P2S cliente conexiones toohello puerta de enlace VPN, se desconectará las conexiones de P2S de Hola y Hola usuarios necesitan tooreconnect desde equipos de cliente de Hola.

![Activa-en espera](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Conectividad entre entornos locales de alta disponibilidad
tooprovide mejor disponibilidad para su entre locales las conexiones, hay un par de opciones disponibles:

* Varios dispositivos VPN locales
* Azure VPN Gateway activa-activa
* Combinación de ambos

### <a name = "activeactiveonprem"></a>Varios dispositivos VPN locales
Puede usar varios dispositivos VPN de su local red tooconnect tooyour puerta de enlace VPN, como se muestra en hello siguiente diagrama:

![Varias VPN locales](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Esta configuración proporciona varios túneles activos de hello mismos VPN de Azure puerta de enlace tooyour local dispositivos Hola misma ubicación. Existen algunos requisitos y restricciones:

1. Debe toocreate varias conexiones VPN de S2S de su tooAzure de dispositivos VPN. Cuando se conectan a varios dispositivos VPN de hello mismo de red local tooAzure, deberá toocreate la puerta de enlace de red local uno para cada dispositivo VPN y una conexión de la puerta de enlace de red local del toohello de puerta de enlace VPN de Azure.
2. puertas de enlace de red local de Hello correspondiente tooyour los dispositivos VPN deben tener direcciones IP públicas únicas Hola propiedad "GatewayIpAddress".
3. Se necesita BGP para esta configuración. Cada puerta de enlace de red local que representa un dispositivo VPN debe tener una dirección IP del elemento del mismo nivel BGP única especificada en la propiedad de "BgpPeerIpAddress" Hola.
4. campo de propiedad de Hello AddressPrefix en cada puerta de enlace de red local no debe solaparse. Debe especificar "BgpPeerIpAddress" hello en /32 formato CIDR en el campo de AddressPrefix hello, por ejemplo, 10.200.200.254/32.
5. Debe utilizar BGP tooadvertise Hola mismos prefijos de hello mismo de red local puerta de enlace de VPN de Azure de tooyour de prefijos y tráfico de Hola se reenviarán a través de estos túneles simultáneamente.
6. Cada conexión se cuenta para el número máximo de Hola de túneles para la puerta de enlace de VPN de Azure, 10 para Basic y SKU estándar y 30 para HighPerformance SKU. 

En esta configuración, puerta de enlace de VPN de Azure de Hola aún está en modo de espera activa, Hola así mismo comportamiento de conmutación por error y breve interrupción todavía se realizará como se describe [anteriormente](#activestandby). Sin embargo, esta configuración protege contra errores o interrupciones en la red local y los dispositivos VPN.

### <a name="active-active-azure-vpn-gateway"></a>Azure VPN Gateway activa-activa
Ahora puede crear una puerta de enlace de VPN de Azure en una configuración activo / activo, donde ambas instancias de puerta de enlace de hello de que las máquinas virtuales, se establecerán que VPN S2S túnel de dispositivo VPN de tooyour local, como se muestra hello después crear un diagrama de:

![Activo-activo](./media/vpn-gateway-highlyavailable/active-active.png)

En esta configuración, cada instancia de puerta de enlace de Azure tendrá una dirección IP pública única y cada una, establecerá un dispositivo VPN IPsec/IKE S2S VPN túnel tooyour local especificado en la puerta de enlace de red local y la conexión. Tenga en cuenta que ambos túneles VPN son realmente parte del programa Hola misma conexión. Todavía se necesita tooconfigure su tooaccept de dispositivo VPN local o establecer dos VPN S2S túneles toothose dos VPN de Azure puerta de enlace las direcciones IP públicas.

Porque no hay instancia de Azure de la puerta de enlace de hello en configuración activo / activo, tráfico de Hola desde la red virtual de Azure tooyour local red se enrutará a través de los túneles al mismo tiempo, incluso si el dispositivo VPN local puede favorecer un túnel de sobre Hola otro. Tenga en cuenta si Hola atravesará siempre el mismo flujo TCP o UDP Hola mismo túnel o ruta de acceso, a menos que se produce un evento de mantenimiento en una de las instancias de Hola.

Cuando un mantenimiento planificado o evento no planeado ocurre la instancia de puerta de enlace de tooone, túnel de IPsec de Hola desde esa instancia tooyour local se desconectará el dispositivo VPN. Hello las rutas correspondientes en los dispositivos VPN deben quitarse o retiradas automáticamente para que se cambiará el tráfico de hello sobre toohello otro túnel de IPsec activa. En hello parte de Azure, cambiar Hola realizará automáticamente de instancias activas de hello afectado instancia toohello.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Redundancia doble: puertas de enlace de VPN activas-activas para redes locales y Azure
opción más fiable de Hello es puertas de enlace de toocombine Hola activo / activo en su red y en Azure, como se muestra en el siguiente diagrama de Hola.

![Redundancia doble](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Aquí crear y configurar la puerta de enlace de VPN de Azure de hello en una configuración activo / activo y crear dos puertas de enlace de red local y dos conexiones para los dos VPN dispositivos locales como se describió anteriormente. resultado de Hello es una conectividad de malla completa de 4 túneles IPsec entre la red virtual de Azure y la red local.

Todas las puertas de enlace y túneles estén activos Hola parte de Azure, por lo que será el tráfico de hello repartidos en todos los 4 túneles al mismo tiempo, aunque cada TCP o UDP flujo tendrá nuevo seguimiento Hola mismo túnel Hola de ruta de acceso de parte de Azure. Aunque al distribuir el tráfico de hello, verá ligeramente mejor rendimiento a través de túneles de IPsec de hello, objetivo principal de Hola de esta configuración es de alta disponibilidad. Y debido toohello naturaleza estadística de propagación de hello, resulta difícil tooprovide medida de hello en el tráfico de aplicación diferentes condiciones afectará al rendimiento agregado de Hola.

Esta topología requiere dos puertas de enlace de red local y par de hello toosupport de dos conexiones de los dispositivos VPN locales y BGP es necesario tooallow Hola dos conexiones toohello misma red local. Estos requisitos son Hola igual como hello [anteriormente](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Conectividad de alta disponibilidad de red virtual a red virtual a través de instancias de Azure VPN Gateway
Hello misma configuración activo / activo también puede aplicar las conexiones de red virtual a red virtual tooAzure. Puede crear puertas de enlace VPN de activo / activo para ambas redes virtuales y conectarlos hello tooform juntos mismo completa de la malla conectividad de 4 túneles entre Hola dos redes virtuales, como se muestra en hello diagrama a continuación:

![De red virtual a red virtual](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Esto garantiza que siempre hay un par de túneles entre dos redes virtuales Hola para cualquier evento de mantenimiento planeado, lo que proporciona disponibilidad aún mejor. Aunque hello misma topología para la conectividad entre entornos requiere dos conexiones, topología de red virtual a red virtual de hello mostrado anteriormente tendrá sólo una conexión para cada puerta de enlace. Además, BGP es opcional, a menos que el enrutamiento del tránsito sobre Hola conexión de red virtual a red virtual es necesario.

## <a name="next-steps"></a>Pasos siguientes
Vea [configuración activo / activo VPN las puertas de enlace para las conexiones de red virtual a red virtual y entre entornos](vpn-gateway-activeactive-rm-powershell.md) para las conexiones de red virtual a red virtual y pasos tooconfigure de activo / activo entre entornos.

