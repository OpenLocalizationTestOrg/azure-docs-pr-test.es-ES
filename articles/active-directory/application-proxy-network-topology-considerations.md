---
title: "Consideraciones sobre la topología aaaNetwork cuando se utiliza el Proxy de aplicación de Azure Active Directory | Documentos de Microsoft"
description: "Se tratan las consideraciones de la topología de red al utilizar el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Consideraciones sobre la topología de red al utilizar el Proxy de aplicación de Azure Active Directory

En este artículo se explican las consideraciones de la topología de red al utilizar el Proxy de aplicación de Azure Active Directory (Azure AD) para la publicación y el acceso a las aplicaciones de forma remota.

## <a name="traffic-flow"></a>Flujo de tráfico

Cuando se publica una aplicación a través de Proxy de aplicación de Azure AD, el tráfico desde las aplicaciones de hello usuarios toohello fluye a través de tres conexiones:

1. usuario de Hola conecta las pública extremo de servicio del Proxy de aplicación de Azure AD de toohello en Azure
2. Hola servicio Proxy de aplicación conecta el conector del Proxy de aplicación de toohello
3. conector del Proxy de aplicación Hola conecta la aplicación de destino toohello

![Diagrama que muestra el flujo de tráfico de aplicación de usuario tootarget](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Ubicación del inquilino y el servicio de Proxy de aplicación

Cuando se registra para un inquilino de Azure AD, región Hola del inquilino de viene determinada por país de Hola que especifique. Cuando se habilita el Proxy de aplicación, instancias de servicio de Proxy de aplicación hello para el inquilino se elegido o creadas en hello mismo región que el inquilino de Azure AD o tooit región más cercana de Hola.

Por ejemplo, si la región del inquilino de Azure AD es hello (unión), todos los conectores de Proxy de aplicación utilice instancias de servicio en los centros de datos de Azure en hello Europa. Cuando a los usuarios acceso aplicaciones publican, su tráfico pasa a través de instancias de servicio de Proxy de aplicación hello en esta ubicación.

## <a name="considerations-for-reducing-latency"></a>Consideraciones para reducir la latencia

Todas las soluciones de proxy introducirán latencia en la conexión de red. Con independencia de qué proxy o una solución VPN elige como solución de acceso remoto, siempre incluye un conjunto de servidores habilitar hello tooinside de conexión de la red corporativa.

Las organizaciones suelen incluir puntos de conexión de servidor en su red perimetral. Con el Proxy de aplicación de Azure AD, sin embargo, el tráfico fluye a través del servicio de proxy de hello en nube de Hola mientras conectores Hola residen en la red corporativa. No se requiere red perimetral.

las secciones siguientes se Hola contienen toohelp sugerencias adicionales reducir aún más la latencia. 

### <a name="connector-placement"></a>Colocación del conector

Proxy de aplicación elige ubicación Hola de instancias, en función de la ubicación del inquilino. Sin embargo, obtendrá toodecide donde tooinstall conector de hello, lo que le otorga Hola características de latencia de consumo de energía toodefine Hola del tráfico de red.

Al configurar el servicio de Proxy de aplicación Hola, pregunte al Hola siguientes preguntas:

* ¿Dónde se encuentra la aplicación hello?
* ¿Dónde están mayoría de los usuarios que tienen acceso a la aplicación hello encuentra?
* ¿Dónde se encuentra la instancia de Proxy de aplicación Hola?
* ¿Ya tiene una red dedicada conexión tooAzure los centros de datos configurado como ExpressRoute de Azure o una VPN similar?

conector Hello tiene toocommunicate con Azure y las aplicaciones (pasos 2 y 3 en el diagrama de flujo de tráfico de hello), por lo que Hola colocación de afecta a conector de Hola Hola la latencia de esas dos conexiones. Al evaluar la selección de ubicación de Hola de conector de hello, tenga en Hola de cuenta siguientes puntos:

* Si desea toouse de la delegación limitada de Kerberos (KCD) para el inicio de sesión único, a continuación, el conector de hello necesita un centro de datos de línea de visión tooa. Además, el servidor de conector de hello tiene Unidos a un dominio de toobe.  
* En caso de duda, instalar aplicación hello conector de más de cerca toohello.

### <a name="general-approach-toominimize-latency"></a>Latencia de toominimize enfoque general

Puede minimizar la latencia de Hola de tráfico de hello-to-end mediante la optimización de cada conexión de red. Cada conexión se puede optimizar mediante uno de estos modos:

* Reduciendo la distancia de hello entre dos extremos de Hola de salto de Hola.
* Elegir hello tootraverse de red apropiado. Por ejemplo, recorrer una red privada en lugar de hello Internet pública puede ser más rápido, debido a vínculos toodedicated.

Si tiene un vínculo dedicado ExpressRoute o VPN entre Azure y la red corporativa, puede que desee toouse que.

## <a name="focus-your-optimization-strategy"></a>Centrar la estrategia de optimización

No hay poco que puede realizar la conexión de hello toocontrol entre los usuarios y el servicio Proxy de aplicación Hola. Los usuarios pueden tener acceso a las aplicaciones desde una red doméstica, una cafetería u otro país. En su lugar, puede optimizar las conexiones de Hola de servicio de Proxy de aplicación Hola toohello Proxy de aplicación conectores toohello aplicaciones. Considere la posibilidad de incorporar Hola siguiendo patrones en su entorno.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Modelo 1: Put Hola conector toohello Cerrar aplicación

Aplicación de destino de cierre toohello lugar Hola conector en red de cliente de Hola. Esta configuración minimiza el paso 3 en el diagrama de la topología de hello, porque el conector Hola y aplicación son similares. 

Si el conector tiene un controlador de dominio de línea de visión toohello, este patrón es ventajoso. La mayoría de nuestros clientes lo usa, puesto que funciona bien para la mayoría de los escenarios. Este patrón también puede combinarse con el tráfico de 2 toooptimize patrón entre servicio Hola y Hola del conector.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Patrón 2: sacar partido de ExpressRoute con el emparejamiento público

Si tiene ExpressRoute configurado con el emparejamiento público, puede usar una conexión ExpressRoute hello más rápida para el tráfico entre el Proxy de aplicación y el conector de Hola. Conector de Hello todavía está en la red, toohello Cerrar aplicación.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Patrón 3: sacar partido de ExpressRoute con el emparejamiento privado

Si tiene una configuración de VPN o ExpressRoute dedicada con emparejamiento privado entre Azure y la red corporativa, tiene otra opción. En esta configuración, la red virtual de hello en Azure normalmente se considera como una extensión de la red corporativa de Hola. Por lo que puede instalar el conector de Hola Hola centro de datos de Azure y cumplir los requisitos de latencia baja de Hola de conexión de conector para aplicación Hola.

La latencia no se ve comprometida porque el tráfico está fluyendo por una red dedicada. También obtendrá mejorada latencia de conector de servicio de Proxy de aplicación porque está instalado el conector de hello en una ubicación del inquilino de Azure AD de centro de datos Azure cerrar tooyour.

![Diagrama que muestra el conector instalado en un centro de datos de Azure](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Otros enfoques

Aunque el enfoque Hola de este artículo es colocación del conector, también puede cambiar selección de ubicación de Hola de hello aplicación tooget mejor latencia.

Las organizaciones están cambiando sus redes a entornos hospedados cada vez con más frecuencia. Esto les permite tooplace sus aplicaciones en un entorno hospedado que también forma parte de su red corporativa y seguir siendo dentro de dominio Hola. En este caso, los patrones de Hola se describe en secciones anteriores de hello pueden ser toohello aplicado nueva ubicación de la aplicación. Si se plantea esta opción, consulte [Servicios de dominio de Azure Active Directory](../active-directory-domain-services/active-directory-ds-overview.md).

Además, considere la posibilidad de organizar sus conectores mediante [grupos de conectores](active-directory-application-proxy-connectors.md) tootarget aplicaciones que se encuentran en diferentes ubicaciones y redes. 

## <a name="common-use-cases"></a>Casos de uso comunes

En esta sección, se abordan algunos de los escenarios habituales. Suponga que Hola inquilino de Azure AD (y, por tanto, el extremo de servicio proxy) se encuentra en Estados Unidos (US) Hola. Hello aspectos descritos en estos casos de uso también se aplican las regiones tooother mundo Hola.

Para estos escenarios, se llama "salto" a cada una de las conexiones y les asignamos un número para facilitar el análisis:

- **Saltar 1**: toohello servicio Proxy de aplicación de usuario
- **Saltar 2**: conector del Proxy de aplicación de servicio toohello Proxy de aplicación
- **Saltar 3**: aplicación de destino de Proxy de aplicación conector toohello 

### <a name="use-case-1"></a>Caso de uso 1

**Escenario:** aplicación hello está en red de una organización en hello nosotros, con usuarios de hello misma región. No ExpressRoute o VPN existe entre hello centro de datos de Azure y la red corporativa de Hola.

**Recomendación:** patrón de seguimiento 1, explicado en la sección anterior de Hola. Para mejorar la latencia, considere la posibilidad de usar ExpressRoute, si es necesario.

Se trata de un modelo simple. Optimizar saltos 3 mediante la colocación de conector de hello cerca de la aplicación hello. También es una opción natural, porque el conector Hola normalmente se instala con línea de visión toohello aplicación y toohello tooperform KCD las operaciones de datacenter.

![Diagrama que muestra que los usuarios, proxy, conector y aplicación aparecen en hello nos](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Caso de uso 2

**Escenario:** aplicación hello está en red de una organización en hello nosotros, con usuarios que se reparten globalmente. No ExpressRoute o VPN existe entre hello centro de datos de Azure y la red corporativa de Hola.

**Recomendación:** patrón de seguimiento 1, explicado en la sección anterior de Hola. 

Una vez más, patrón común de hello toooptimize salto es 3, donde colocar conector Hola cerca de la aplicación hello. Salto 3 no es normalmente caro, si es todo dentro Hola misma región. Sin embargo, salto 1 puede resultar más costoso dependiendo de dónde esté el usuario hello, porque los usuarios a través de Hola a todos deben tener acceso a la instancia de Proxy de aplicación Hola Hola Estados Unidos. Merece la pena mencionar que cualquier solución de proxy tendrá similares características con respecto a los usuarios que se reparten por todo el mundo.

![Diagrama que muestra que los usuarios están repartidos global, pero app, conector y proxy de Hola Hola EE. UU.](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Caso de uso 3

**Escenario:** aplicación hello está en la red de una organización en hello nos. ExpressRoute con emparejamiento público existe entre la red corporativa hello y Azure.

**Recomendación:** seguir los patrones de 1 y 2, que se explica en la sección anterior de Hola.

En primer lugar, coloque el conector de hello lo más cerca posible toohello aplicación. A continuación, sistema de hello usa automáticamente ExpressRoute de salto 2. 

Si el vínculo de ExpressRoute de hello usa emparejamiento público, el tráfico de hello entre el proxy de Hola y el conector de hello fluye a través de ese vínculo. El salto 2 tiene la latencia optimizada.

![Diagrama que muestra ExpressRoute entre el conector y proxy de Hola](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Caso de uso 4

**Escenario:** aplicación hello está en la red de una organización en hello nos. ExpressRoute con intercambio de tráfico privado existe entre la red corporativa hello y Azure.

**Recomendación:** seguimiento patrón 3, explicado en la sección anterior de Hola.

Coloque el conector de hello en hello centro de datos de Azure que está conectado toohello la red corporativa a través de ExpressRoute de emparejamiento privado. 

Conector de Hello puede colocarse en hello centro de datos de Azure. Puesto que el conector de hello todavía tiene una aplicación de línea de visión toohello y datacenter de Hola a través de la red privada de hello, salto 3 sigue estando optimizado. Además, el salto 2 se optimiza aún más.

![Diagrama que muestra el conector de hello en un centro de datos de Azure y ExpressRoute entre la aplicación y el conector de Hola](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Caso de uso 5

**Escenario:** aplicación hello está en la red de una organización en hello Europa, con la instancia de Proxy de aplicación Hola y la mayoría de los usuarios en hello nos.

**Recomendación:** conector de hello lugar cerca de la aplicación hello. Como los usuarios de Estados Unidos tienen acceso a una instancia de Proxy de aplicación que se produce a toobe Hola misma región, salto 1 no es demasiado caro. El salto 3 se optimiza. Considere el uso de ExpressRoute toooptimize salto 2. 

![Diagrama que muestra los usuarios y el proxy en hello Estados Unidos, con el conector de Hola y aplicación Hola Europa](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

También puede considerar la utilización de alguna otra variante en esta situación. Si hay mayoría de los usuarios en la organización de Hola Hola nos, lo más probable es que la red extiende toohello nosotros también. Colocar el conector de Hola Hola EE. UU. y utilizar la aplicación de toohello de línea de red corporativa interna de hello dedicado en hello Europa. De esta forma se optimizan los saltos 2 y 3.

![Diagrama que muestra los usuarios, el proxy y el conector en hello Estados Unidos, aplicación Hola Europa](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Pasos siguientes

- [Habilitación del proxy de la aplicación](active-directory-application-proxy-enable.md)
- [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md)
- [Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md)
- [Solucionar los problemas que tiene con el Proxy de aplicación](active-directory-application-proxy-troubleshoot.md)
