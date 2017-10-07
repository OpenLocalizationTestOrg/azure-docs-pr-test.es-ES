---
title: "Consideraciones de aaaPerformance para el Administrador de tráfico de Azure | Documentos de Microsoft"
description: "Comprender el rendimiento en el Administrador de tráfico y cómo tootest rendimiento del sitio Web al usar el Administrador de tráfico"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Consideraciones de rendimiento sobre el Administrador de tráfico

En esta página se explican las consideraciones de rendimiento relacionadas con el uso de Administrador de tráfico. Considere la posibilidad de hello siguiendo el escenario:

Tiene instancias de su sitio Web en hello oesteee. UU. y regiones de Asia oriental. Una de las instancias de hello error en comprobación de estado de hello para la sonda de administrador de tráfico de Hola. Tráfico de la aplicación es la región correcto toohello dirigido. Se esperaba esta conmutación por error, pero el rendimiento puede ser un problema en función de la latencia de Hola de tráfico de hello ahora viaja tooa distantes región.

## <a name="performance-considerations-for-traffic-manager"></a>Consideraciones de rendimiento sobre el Administrador de tráfico

Hola solo impacto sobre el rendimiento de Traffic Manager puede tener en su sitio Web es búsqueda DNS de saludo inicial. Una solicitud DNS para el nombre de Hola de su perfil de Traffic Manager se controla por servidor de raíz de DNS de Microsoft hello esa zona trafficmanager.net de Hola de hosts. Traffic Manager se rellena y se actualiza periódicamente, servidores de raíz DNS de Microsoft hello basados en directiva de Traffic Manager de Hola y los resultados de sondeo de Hola. Incluso durante la búsqueda DNS inicial de hello, no hay consultas DNS se envían tooTraffic Manager.

El Administrador de tráfico se compone de varios componentes: servidores, un servicio de API, capa de almacenamiento de Hola y un punto de conexión de servicio de supervisión de los nombres de DNS. Si se produce un error en un componente del servicio Administrador de tráfico, no hay ningún efecto en el nombre DNS de hello asociado a tu perfil de Traffic Manager. registros de Hello en los servidores DNS de Microsoft hello permanecen sin cambios. Sin embargo, la supervisión de puntos de conexión y la actualización de DNS no se llevan a cabo. Por lo tanto, Traffic Manager no es capaz de tooupdate DNS toopoint tooyour conmutación por error sitio, si el sitio primario se queda inactivo.

La resolución de nombres DNS es rápida y los resultados se almacenan en la memoria caché. velocidad de Hola Hola inicial de búsqueda de DNS depende de hello cliente de Hola de servidores DNS que se utiliza para la resolución de nombre. Por lo general, un cliente puede completar una búsqueda de DNS en aproximadamente 50 ms. se almacenan en caché los resultados de Hola de búsqueda de hello dure Hola Hola DNS Time-to-live (TTL). TTL de Traffic Manager del saludo predeterminado es 300 segundos.

El tráfico NO fluye a través del Administrador de tráfico. Una vez completada la búsqueda DNS de Hola, cliente hello tiene una dirección IP para una instancia de su sitio web. cliente de Hola conecta directamente toothat dirección y no pasa a través del Administrador de tráfico. Hola directiva de Traffic Manager que elija no influye en el rendimiento de DNS de Hola. Sin embargo, un método de enrutamiento de rendimiento puede afectar negativamente al experiencia con la aplicación hello. Por ejemplo, si la directiva redirija el tráfico de América del Norte tooan instancia hospedada en Asia, latencia de red de Hola para esas sesiones puede ser un problema de rendimiento.

## <a name="measuring-traffic-manager-performance"></a>Medición del rendimiento de Traffic Manager

Hay varios sitios Web que puede usar toounderstand rendimiento de Hola y el comportamiento de un perfil de Traffic Manager. Muchos de ellos son gratuitos, pero pueden tener limitaciones. Algunos sitios ofrecen supervisión mejorada y elaboración de informes por una cuota.

herramientas de Hello en estos sitios medir las latencias de DNS y mostrar hello resolver direcciones IP para ubicaciones de los clientes alrededor de Hola a todos. La mayoría de estas herramientas no almacenan en caché los resultados de DNS de Hola. Por lo tanto, las herramientas de hello muestran búsqueda DNS completa Hola cada vez que se ejecuta una prueba. Cuando se prueba desde su propio cliente, solo experimentar rendimiento de búsqueda DNS completo de hello una vez durante la duración del período de vida de Hola.

## <a name="sample-tools-toomeasure-dns-performance"></a>Rendimiento de DNS de ejemplo herramientas toomeasure

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS ofrece muchas herramientas de rendimiento. herramienta de comparación de DNS de Hola puede mostrarle el tiempo que tarda tooresolve el nombre DNS y cómo compara tooother proveedores de servicios DNS.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Una de las herramientas más sencillas de hello es WebSitePulse. Escriba el tiempo de resolución DNS de hello URL toosee, el primer Byte, el último Byte y otras estadísticas de rendimiento. Puede elegir entre tres ubicaciones de prueba diferentes. En este ejemplo, verá que primera ejecución de hello muestra que la búsqueda de DNS toma s 0.204.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Dado que Hola se almacenan en caché de resultados, segunda prueba de Hola para Hola misma búsqueda DNS de Hola de punto de conexión de Traffic Manager tarda 0.002 seg.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [CA App Synthetic Monitor](https://asm.ca.com/en/checkit.php)

    Conocido anteriormente como herramienta de sitio Web de comprobación Watchmouse hello, este sitio mostrarle Hola resolución DNS de tiempo simultáneamente en varias regiones geográficas. Escriba el tiempo de resolución DNS de hello URL toosee, el tiempo de conexión y velocidad desde varias ubicaciones geográficas. Utilice este toosee prueba qué servicio hospedado se devuelve para las diferentes ubicaciones alrededor de Hola a todos.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    Esta herramienta proporciona estadísticas de rendimiento para cada elemento de una página web. Hola pestaña página análisis muestra hello de porcentaje de tiempo invertido en la búsqueda de DNS.

* [What's My DNS?](http://www.whatsmydns.net/)

    Este sitio hace una búsqueda de DNS desde 20 distintas ubicaciones y muestra los resultados de hello en un mapa.

* [Dig Web Interface](http://www.digwebinterface.com)

    Este sitio muestra información de DNS más detallada, incluidos los registros A y CNAME. Asegúrese de que se active hello 'colorear salida' y 'Estadísticas' en las opciones y seleccione 'All' en los servidores de nombres.

## <a name="next-steps"></a>Pasos siguientes

[Información acerca de los métodos de enrutamiento del tráfico del Administrador de tráfico](traffic-manager-routing-methods.md)

[Pruebe la configuración del Administrador de tráfico](traffic-manager-testing-settings.md)

[Operaciones del Administrador de tráfico (referencia de la API de REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlets del Administrador de tráfico de Azure](http://go.microsoft.com/fwlink/p/?LinkId=400769)

