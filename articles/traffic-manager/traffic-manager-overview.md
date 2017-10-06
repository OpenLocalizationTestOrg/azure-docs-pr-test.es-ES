---
title: aaaWhat es Traffic Manager | Documentos de Microsoft
description: "Este artículo le ayudará a comprender qué es el Administrador de tráfico y, ya sea una opción de enrutamiento de tráfico derecho hello para la aplicación"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Introducción a Traffic Manager

Microsoft Azure Traffic Manager permite distribución de hello toocontrol del tráfico de usuario para los extremos de servicio en distintos centros de datos. Entre los puntos de conexión de servicio compatibles con Traffic Manager, se incluyen máquinas virtuales de Azure, Web Apps y servicios en la nube. También puede utilizar el Administrador de tráfico con puntos de conexión externos, que no forman parte de Azure.

Traffic Manager utiliza toohello Hola sistema de nombres de dominio (DNS) toodirect cliente solicitudes más adecuado extremo en función de un método de enrutamiento del tráfico y el estado de Hola de extremos de Hola. Traffic Manager proporciona una gama de [métodos de enrutamiento del tráfico](traffic-manager-routing-methods.md) y [opciones de supervisión de extremo](traffic-manager-monitoring.md) toosuit otra aplicación necesidades y los modelos de conmutación automática por error. El Administrador de tráfico es resistente toofailure, incluidos los errores de Hola de toda una región de Azure.

## <a name="traffic-manager-benefits"></a>Ventajas de Traffic Manager

Traffic Manager puede ayudarle a:

* **Mejorar la disponibilidad de las aplicaciones esenciales**

    Traffic Manager ofrece alta disponibilidad para las aplicaciones al supervisar los puntos de conexión y proporcionar la conmutación automática por error cuando un punto de conexión deja de funcionar.

* **Mejorar la capacidad de respuesta para las aplicaciones de alto rendimiento**

    Azure permite toorun servicios en la nube o sitios Web en los centros de datos ubicados en todo Hola a todos. El Administrador de tráfico mejora la capacidad de respuesta de aplicación dirigiendo el punto de conexión de tráfico toohello con menor latencia de red hello para el cliente de Hola.

* **Realizar el mantenimiento del servicio sin tiempo de inactividad**

    Puede realizar operaciones de mantenimiento planeado en sus aplicaciones sin tiempo de inactividad. Administrador de tráfico dirige los puntos de conexión de tráfico tooalternative mientras mantenimiento Hola está en curso.

* **Combinar aplicaciones locales y basadas en la nube**

    El Administrador de tráfico admite externo, los extremos de Azure no habilitar toobe utiliza con híbridos en la nube y locales implementaciones, incluidas Hola "ráfaga en la nube," "migrar a la nube," y "conmutación por error a la nube" escenarios.

* **Distribuir el tráfico para implementaciones grandes y complejas**

    Usar [anidados perfiles de Traffic Manager](traffic-manager-nested-profiles.md), métodos de enrutamiento del tráfico puede combinado toocreate sofisticados y Hola de toosupport reglas flexibles debe de las implementaciones más grandes y complejas.

## <a name="how-traffic-manager-works"></a>Cómo funciona Traffic Manager

Azure Traffic Manager permite distribución de hello toocontrol de tráfico a través de los extremos de la aplicación. Un punto de conexión es cualquier servicio accesible desde Internet hospedado dentro o fuera de Azure.

Traffic Manager ofrece dos ventajas principales:

1. Distribución del tráfico según tooone de varias [métodos de enrutamiento de tráfico](traffic-manager-routing-methods.md)
2. [supervisión continua del estado de los puntos de conexión](traffic-manager-monitoring.md) y la conmutación por error automática en caso de error en estos

Cuando un cliente intenta tooconnect tooa servicio, primero debe resolver nombre DNS de Hola Hola tooan IP de dirección de servicio. cliente de Hello, a continuación, conecta el servicio hello tooaccess de toothat IP direcciones.

**Hola toounderstand de punto más importante es que Traffic Manager funciona en el nivel de DNS de Hola.**  Los extremos en función de reglas de hello del método de enrutamiento del tráfico de hello del servicio de administrador de tráfico usa DNS toodirect clientes toospecific. Los clientes conectan toohello seleccionado extremo **directamente**. Traffic Manager no es un proxy ni una puerta de enlace. El Administrador de tráfico no ve tráfico Hola pasar entre el cliente de Hola y el servicio de Hola.

### <a name="traffic-manager-example"></a>Ejemplo de Traffic Manager

Contoso Corp ha desarrollado un nuevo portal para asociados. dirección URL de Hola para este portal es https://partners.contoso.com/login.aspx. aplicación Hello se hospeda en tres regiones de Azure. disponibilidad de tooimprove y maximizar el rendimiento global, utilizan el Administrador de tráfico toodistribute cliente tráfico toohello extremo más cercano disponible.

tooachieve esta configuración, que se completa Hola pasos:

1. Se implementan tres instancias de su servicio. nombres DNS de Hola de estas implementaciones son 'contoso us.cloudapp NET', 'contoso eu.cloudapp .net' y 'contoso asia.cloudapp .net'.
2. Crear un perfil de Traffic Manager, con el nombre 'contoso.trafficmanager.net' y configurar método de hello 'Rendimiento'-enrutamiento del tráfico de toouse entre los extremos de hello tres.
* Configurar su nombre de dominio personal, 'partners.contoso.com' toopoint too'contoso.trafficmanager.net', con un registro CNAME de DNS.

![Configuración de DNS de Traffic Manager][1]

> [!NOTE]
> Al utilizar un dominio personal con Azure Traffic Manager, debe utilizar un toopoint CNAME su nombre de dominio personal dominio nombre tooyour Traffic Manager. Los estándares de DNS no le permiten toocreate un CNAME en hello 'vértice' (o raíz) de un dominio. Por lo tanto no se puede crear un registro CNAME para "contoso.com" (lo que también se conoce como un dominio "desnudo"). Solo se puede crear un registro CNAME para un dominio bajo "contoso.com", como "www.contoso.com". toowork solucionar esta limitación, se recomienda usar un simple solicitudes de toodirect de redirección HTTP nombre alternativo de 'contoso.com' tooan como 'www.contoso.com'.

### <a name="how-clients-connect-using-traffic-manager"></a>Conexión de clientes mediante Traffic Manager

Continuar desde el ejemplo anterior de hello, cuando un cliente solicita Hola página https://partners.contoso.com/login.aspx, cliente hello realiza Hola después de nombre de DNS de pasos tooresolve hello y establecer una conexión:

![Establecimiento de la conexión mediante Traffic Manager][2]

1. cliente de Hello envía una tooits configurado de consultas DNS recursivas DNS servicio tooresolve Hola nombre 'partners.contoso.com'. Un servicio DNS recursivo, a veces denominado servicio "DNS local", no hospeda los dominios DNS directamente. En su lugar, la descarga de cliente hello su trabajo Hola de ponerse en contacto con hello DNS autoritativos diversos servicios entre Hola Internet sea necesario tooresolve un nombre DNS.
2. nombre DNS de hello tooresolve, servicio DNS recursivas Hola busca servidores de nombres de Hola para dominio de 'contoso.com' hello. A continuación, contacta con los registro de DNS de nombres servidores toorequest hello 'partners.contoso.com'. los servidores DNS de contoso.com Hola devuelven Hola registro CNAME que apunte toocontoso.trafficmanager.net.
3. A continuación, el servicio DNS recursivas Hola busca servidores de nombres de Hola para dominio de 'trafficmanager.net' hello, que se proporcionan con hello el servicio Administrador de tráfico de Azure. A continuación, envía una solicitud para toothose registro del DNS de 'contoso.trafficmanager.net' hello servidores DNS.
4. servidores de nombres del Administrador de tráfico de Hola reciban solicitud de saludo. Eligen un punto de conexión en función de:

    - estado de Hello configurado de cada punto de conexión (no se devuelven los puntos de conexión deshabilitados)
    - comprueba el estado actual de Hola de cada punto de conexión, según lo determinado por el estado de administrador de tráfico de Hola. Para más información, consulte [Acerca de la supervisión de Traffic Manager](traffic-manager-monitoring.md).
    - Hola elegida método de enrutamiento de tráfico. Para más información, consulte [Métodos de enrutamiento de Traffic Manager](traffic-manager-routing-methods.md).

5. punto de conexión de Hello elegido se devuelve como otro registro CNAME de DNS. En este caso, supongamos que contoso-us.cloudapp.net se devuelve.
6. A continuación, el servicio DNS recursivas Hola busca servidores de nombres de Hola para dominio de hello 'cloudapp.net'. Pone en contacto con esos hello toorequest de servidores de nombre 'contoso-us.cloudapp .net' registro de DNS. Se devuelve un registro DNS 'A' que contiene la dirección IP de Hola Hola basados en Estados del extremo de servicio.
7. servicio DNS recursivas Hola consolida los resultados de Hola y devuelve a un solo cliente de toohello de respuesta DNS.
8. cliente de Hello recibe resultados DNS de Hola y conecta toohello determinado por dirección IP. Hola cliente conecta extremo de servicio de aplicación toohello directamente, no a través del Administrador de tráfico. Puesto que es un extremo HTTPS, cliente hello realiza el protocolo de enlace SSL/TLS necesario hello y, a continuación, realiza una solicitud HTTP GET para hello ' / login.aspx' página.

servicio DNS recursivas Hola almacena en caché las respuestas DNS de hello recibe. resolución DNS de Hello en dispositivo de cliente hello también almacena en caché el resultado de hello. Almacenamiento en caché permite toobe posterior de las consultas DNS respondida más rápidamente mediante los datos de caché de hello en lugar de consultar otros servidores de nombres. duración de Hola de caché de hello viene determinada por la propiedad 'time-to-live' de (TTL) de Hola de cada registro DNS. Los valores más cortos producen expiración de caché más rápida y, por tanto, más ida y vuelta toohello Traffic Manager servidores de nombres. Valores de mayor significan que puede tardar más tráfico toodirect fuera de un punto de conexión ha fallado. Traffic Manager permite tooconfigure Hola TTL utilizado en toobe de las respuestas de DNS de Traffic Manager como mínimo es 0 segundos y tan alto como 2.147.483.647 segundos (Hola máximo del intervalo compatible con [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), lo que el valor de hello toochoose mejor equilibre las necesidades de saludo de la aplicación.

## <a name="pricing"></a>Precios

Para obtener información de precios, consulte la página de [precios de Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>P+F

Para ver las preguntas más frecuentes sobre Traffic Manager, vea [Preguntas más frecuentes (P+F) sobre Traffic Manager](traffic-manager-FAQs.md).

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre la [supervisión del punto de conexión y la conmutación por error automática](traffic-manager-monitoring.md) de Traffic Manager.

Obtenga más información sobre los [métodos de enrutamiento del tráfico](traffic-manager-routing-methods.md) de Traffic Manager.

Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md) de Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

