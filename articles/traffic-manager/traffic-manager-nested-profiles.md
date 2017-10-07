---
title: aaaNested perfiles de Traffic Manager | Documentos de Microsoft
description: "Este artículo explica la característica de hello 'Anidado perfiles' de Azure Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>Perfiles anidados del Administrador de tráfico

Traffic Manager incluye una amplia variedad de métodos de enrutamiento de tráfico que le permiten toocontrol cómo Traffic Manager elige qué extremo debe recibir el tráfico de cada usuario final. Para más información, consulte [Métodos de enrutamiento del Administrador de tráfico](traffic-manager-routing-methods.md).

Cada perfil del Administrador de tráfico especifica un único método de enrutamiento del tráfico. Sin embargo, hay escenarios que requieren el enrutamiento del tráfico más sofisticadas de hello enrutamiento proporcionada por un solo perfil de Traffic Manager. Puede anidar ventajas de hello toocombine de los perfiles de Traffic Manager de más de un método de enrutamiento de tráfico. Perfiles anidados permiten toooverride Hola predeterminado Traffic Manager comportamiento toosupport mayor y las implementaciones de aplicaciones más complejas.

Hello en los ejemplos siguientes ilustran cómo toouse anidar perfiles de Traffic Manager en distintos escenarios.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>Ejemplo 1: Enrutamiento de tráfico combinado: de "rendimiento" y "ponderado"

Suponga que ha implementado una aplicación Hola después de regiones de Azure: oeste de Estados Unidos, Europa occidental y Asia oriental. Use del Administrador de tráfico 'Rendimiento' enrutamiento del tráfico método toodistribute tráfico toohello región más cercano toohello usuario.

![Perfil único del Administrador de tráfico][4]

Ahora, suponga que desea tootest un servicio de actualización de tooyour antes de distribuirla más ampliamente. Desea toouse Hola "ponderado" enrutamiento del tráfico método toodirect un pequeño porcentaje de implementación de prueba de tooyour de tráfico. Configurar la implementación de prueba de hello junto con la implementación de producción existente de hello en Europa occidental.

No puede combinar ambos métodos de enrutamiento en un solo perfil. toosupport este escenario, se crea un perfil de Traffic Manager mediante puntos de conexión de hello dos Europa occidental y método hello 'Weighted'-enrutamiento del tráfico. A continuación, agregue este perfil 'child' como un perfil de punto de conexión toohello 'principal'. perfil de Hello principal utiliza todavía Hola método de enrutamiento del tráfico de rendimiento y contiene Hola otras implementaciones globales como los puntos de conexión.

Hola siguiente diagrama muestra en este ejemplo:

![Perfiles anidados del Administrador de tráfico][2]

En esta configuración, el tráfico dirigido a través de perfil primario de hello distribuye normalmente el tráfico entre regiones. En Europa occidental, hello perfil anidado distribuye el tráfico toohello prueba y producción puntos de conexión según los pesos toohello asignados.

Cuando perfil principal de hello usa el método de enrutamiento del tráfico de hello 'Rendimiento', cada punto de conexión debe asignarse una ubicación. ubicación de Hola se asigna al configurar el punto de conexión de Hola. Elija la implementación de tooyour más cercano de hello región de Azure. Hello regiones de Azure son valores de ubicación de hello admitidos Hola tabla de latencia de Internet. Para más información, consulte [Método de enrutamiento de tráfico de rendimiento de Traffic Manager](traffic-manager-routing-methods.md#performance).

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>Ejemplo 2: Supervisión de puntos de conexión en perfiles anidados

Traffic Manager supervisa activamente mantenimiento Hola de cada extremo de servicio. Si un punto de conexión está en mal estado, Administrador de tráfico dirige a los usuarios tooalternative extremos toopreserve Hola disponibilidad de su servicio. Este comportamiento de conmutación por error y supervisión de punto de conexión aplica a los métodos de enrutamiento del tráfico de tooall. Para más información, consulte [Acerca de la supervisión de Traffic Manager](traffic-manager-monitoring.md). La supervisión de puntos de conexión funciona de manera diferente para perfiles anidados. Con perfiles anidados, perfil de hello primario no realiza comprobaciones de estado secundario Hola directamente. En su lugar, el estado de Hola de puntos de conexión del perfil de hello secundario es toocalculate usado Hola estado general del perfil de hello secundario. Esta información de estado se propaga hacia arriba en jerarquía de perfil de hello anidado. Hello perfil principal usa esta toodetermine de mantenimiento agregado si el perfil de toodirect tráfico toohello hijo. Vea hello [preguntas más frecuentes sobre](traffic-manager-FAQs.md#traffic-manager-nested-profiles) para obtener detalles completos sobre supervisión del mantenimiento de perfiles anidados.

Devolver toohello de ejemplo anterior, supongamos que se produce un error en la implementación de producción de hello en Europa occidental. De forma predeterminada, perfil de 'child' hello dirige todas las implementaciones de prueba de toohello de tráfico. Si tampoco se puede realizar la implementación de las pruebas de hello, Hola primario perfil en el que se determina que el perfil de hello hijo no debe recibir el tráfico puesto que todos los extremos secundarios tienen un estado incorrecto. A continuación, perfil principal de hello distribuye tráfico toohello otras regiones.

![Conmutación por error de perfil anidado (comportamiento predeterminado)][3]

Puede que esta solución le satisfaga. O bien, es posible que preocuparse de que todo el tráfico de Europa occidental ahora está quedando toohello implementación de prueba en lugar de un tráfico de subconjunto limitado. Independientemente del estado de Hola de hello probar la implementación, deberá toofail sobre toohello otras regiones cuando se produce un error en la implementación de producción de hello en Europa occidental. tooenable esta conmutación por error, puede especificar parámetros de 'MinChildEndpoints' hello al configurar el perfil de hello hijo como un punto de conexión en el perfil primario de Hola. parámetro Hello determina un mínimo de extremos disponibles en el perfil de hijo Hola Hola. valor predeterminado de Hello es '1'. En este escenario, establezca hello MinChildEndpoints valor too2. Por debajo del umbral, perfil principal de hello considera Hola todo secundario perfil toobe disponible y dirige el tráfico toohello otros puntos de conexión.

Hello en la ilustración siguiente se muestra esta configuración:

![Conmutación por error de perfil anidado con "MinChildEndpoints" = 2][4]

> [!NOTE]
> el método de enrutamiento de tráfico 'Priority' Hello distribuye todo el tráfico tooa único punto de conexión. Por lo tanto, en este caso, no tiene mucho sentido una configuración de MinChildEndpoints distinta de "1" para un perfil secundario.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>Ejemplo 3: Regiones de conmutación por error en orden de prioridad en el enrutamiento de tráfico de "rendimiento"

comportamiento predeterminado de Hello para el método de enrutamiento de tráfico 'Rendimiento' hello es tooavoid diseñada excesiva carga Hola de junto más próximo al punto de conexión y causa una serie de errores en cascada. Cuando se produce un error en un punto de conexión, todo el tráfico que habría le haya dirigido hasta el punto de conexión de toothat es uniformemente distribuidos toohello otros puntos de conexión en todas las regiones.

![Enrutamiento de tráfico de "rendimiento" con conmutación por error predeterminada][5]

Sin embargo, suponga que desee tooWest de conmutación por error de tráfico de hello Europa occidental nos y dirigir solo regiones tooother de tráfico cuando ambos puntos de conexión no están disponibles. Puede crear esta solución mediante un perfil secundario con el método de enrutamiento de tráfico 'Priority' hello.

![Enrutamiento de tráfico de "rendimiento" con conmutación por error preferencial][6]

Puesto que el punto de conexión de hello Europa occidental tiene mayor prioridad que el punto de conexión de hello oeste de Estados Unidos, todo el tráfico se envía el punto de conexión de toohello Europa occidental cuando ambos extremos estén en línea. Si se produce un error en Europa occidental, su tráfico es dirigido tooWest Estados Unidos. Con el perfil de hello anidado, tráfico es dirigido tooEast Asia solo cuando Europa del este y oeste de Estados Unidos producirá un error.

Puede repetir este patrón con todas las regiones. Reemplace los tres extremos en perfil de hello primario con tres perfiles secundarios, cada uno con una secuencia ordenada por prioridad de conmutación por error.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>Ejemplo 4: Controlar el tráfico de 'Rendimiento' enrutamiento entre varios puntos de conexión en hello misma región

Suponga que hello 'Rendimiento' método de enrutamiento del tráfico se utiliza en un perfil que tenga más de un extremo de una región determinada. De forma predeterminada, el tráfico dirigido toothat región se distribuye uniformemente en todos los puntos de conexión disponibles en dicha región.

![Enrutamiento de tráfico de "rendimiento" con distribución del tráfico en la región (comportamiento predeterminado)][7]

En lugar de agregar varios puntos de conexión en Europa Occidental, esos puntos de conexión se incluyen en un perfil secundario independiente. perfil de Hello secundario se agrega a toohello primario como extremo de sólo hello en Europa occidental. configuración de Hello en el perfil de hello hijo puede controlar la distribución de tráfico de hello con Europa occidental habilitando el enrutamiento del tráfico basado en prioridad o ponderado de esa región.

![Enrutamiento de tráfico de "rendimiento" con distribución personalizada del tráfico en la región][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>Ejemplo 5: Configuración de la supervisión por punto de conexión

Supongamos que usa Traffic Manager toosmoothly migrar tráfico desde una local heredado sitio web tooa nueva basada en la nube versión hospedada en Azure. Para sitio heredado de hello, desea toouse Hola portada URI toomonitor el estado del sitio. Pero para la nueva versión en la nube hello, va a implementar una página de supervisión personalizada (ruta de acceso ' / monitor.aspx') que incluye comprobaciones adicionales.

![Supervisión de puntos de conexión del Administrador de tráfico (comportamiento predeterminado)][9]

configuración de supervisión de Hello en un perfil de Traffic Manager aplica los puntos de conexión de tooall dentro de un solo perfil. Con perfiles anidados, utiliza un perfil de diferentes secundario por sitio toodefine diferente de configuración de supervisión.

![Supervisión de puntos de conexión del Administrador de tráfico con configuración por punto de conexión][10]

## <a name="next-steps"></a>Pasos siguientes

Más información sobre los [perfiles de Traffic Manager](traffic-manager-overview.md)

Obtenga información acerca de cómo demasiado[crear un perfil de Traffic Manager](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
