---
title: 'Redes de Azure Stack: diferencias y consideraciones'
description: Aprenda sobre las diferencias y consideraciones al trabajar con redes en Azure Stack.
services: azure-stack
keywords: 
author: ScottNapolitan
ms.author: victorh
ms.date: 08/02/2017
ms.topic: article
ms.service: azure-stack
ms.openlocfilehash: 12a557d2d1184c2191683956e263558cc3a474b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="considerations-for-azure-stack-networking"></a>Consideraciones para las redes de Azure Stack

Redes en la pila de Azure proporcionan muchas características Hola que buscar en Azure, con algunas diferencias que debe conocer antes de empezar a implementar.


Este artículo proporciona información general de hello consideraciones únicas para las redes y sus características en la pila de Azure. toolearn acerca de alto nivel diferencias entre la pila de Azure y Azure, vea hello [clave consideraciones](azure-stack-considerations.md) tema.


## <a name="cheat-sheet-networking-differences"></a>Hoja de referencia rápida: diferencias de servicios de red

|Servicio | Característica | Azure (global) | Azure Stack |
| --- | --- | --- | --- |
| DNS | DNS multiinquilino | Compatible| Todavía no se admite|
| |Registros AAAA de DNS|Compatible|No compatible|
| |Zonas DNS por suscripción|100 (valor predeterminado)<br>Puede aumentarse a petición.|100|
| |Conjuntos de registros DNS por zona|5000 (valor predeterminado)<br>Puede aumentarse a petición.|5000|
||Servidores de nombres para la delegación de zona|Azure proporciona cuatro servidores de nombres para cada zona de usuario (inquilino) que se crea.|Azure Stack proporciona dos servidores de nombres para cada zona de usuario (inquilino) que se crea.|
| Red virtual|Emparejamiento de redes virtuales de Azure|Conectar dos redes virtuales en hello misma región a través de la red troncal de Azure de Hola.|Todavía no se admite|
| |Direcciones IPv6|Puede asignar una dirección IPv6 como parte del programa Hola a [configuración de la interfaz de red](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface-addresses#ip-address-versions).|Se admite solo IPv4.|
|Puertas de enlace de VPN|Puerta de enlace de VPN de punto a sitio|Compatible|Todavía no se admite|
| |Puerta de enlace de VNET a VNET|Compatible|Todavía no se admite|
| |SKU de puerta de enlace de VPN|Compatibilidad con SKU básicas, GW1, GW2, GW3, alto rendimiento estándar, ultra alto rendimiento. |Compatibilidad con SKU básicas, estándar y de alto rendimiento.|
|Equilibrador de carga|Direcciones IP públicas IPv6|Equilibrador de carga de soporte técnico para asignar un tooa de dirección IP pública de IPv6.|Se admite solo IPv4.|
|Network Watcher|Funciones de supervisión de red de inquilinos de Network Watcher|Compatible|Todavía no se admite|
|CDN|Perfiles de Content Delivery Network|Compatible|Todavía no se admite|
|puerta de enlace de aplicaciones|Equilibrio de carga de nivel 7|Compatible|Todavía no se admite|
|Administrador de tráfico|Dirija el tráfico entrante para obtener un rendimiento y una confiabilidad óptimos de las aplicaciones.|Compatible|Todavía no se admite|
|ExpressRoute|Configurar un servicios en la nube tooMicrosoft conexión privada y rápida de la instalación local de infraestructura o la colocación.|Compatible|Soporte técnico para la conexión de circuito de Express Route tooan de pila de Azure.|

## <a name="next-steps"></a>Pasos siguientes

[DNS en Azure Stack](azure-stack-dns.md)
