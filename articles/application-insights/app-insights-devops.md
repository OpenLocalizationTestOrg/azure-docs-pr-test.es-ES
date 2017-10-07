---
title: "aaaWeb supervisión de rendimiento de aplicaciones - visión de la aplicación de Azure | Documentos de Microsoft"
description: "Cómo se integra Application Insights en hello devOps ciclo"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Diagnósticos detallados para servicios y aplicaciones web con Application Insights
## <a name="why-do-i-need-application-insights"></a>¿Por qué necesito Application Insights?
Application Insights supervisa la ejecución de la aplicación web. Indica los errores y problemas de rendimiento y le ayuda a analizar el modo en que los clientes usan las aplicaciones. Funciona con aplicaciones que se ejecutan en varias plataformas (ASP.NET, J2EE, Node.js,...) y se hospeda en hello en la nube o local. 

![Aspectos de la complejidad de saludo de la entrega de aplicaciones web](./media/app-insights-devops/010.png)

Resulta esencial toomonitor una moderna aplicación mientras se está ejecutando. Lo más importante, desea toodetect errores para llevar a cabo la mayoría de los clientes. También desea toodiscover y corregir problemas de rendimiento que, aunque no grave, quizás ralentizan las operaciones o causar algún inconveniente tooyour a los usuarios. Y cuando el sistema de Hola está realizando la satisfacción tooyour, desea tooknow qué usuarios Hola hacen con él: ¿son mediante la característica más reciente de hello? ¿Les funcionan bien?

Aplicaciones web modernas se desarrollan en un ciclo de entrega continua: la versión de una característica nueva o mejora, Observe también cómo funciona para los usuarios de hello; Planear siguiente incremento de Hola de desarrollo basado en esa información. Una parte fundamental de este ciclo es la fase de observación de Hola. Visión de aplicación proporciona Hola herramientas toomonitor una aplicación web para el rendimiento y uso.

aspecto más importante de Hola de este proceso es un diagnóstico más detallado y diagnóstico. Si se produce un error en la aplicación hello, se han perdido el negocio. Hola rol principal de un marco de trabajo supervisión, por tanto, es toodetect errores forma confiable, notificar inmediatamente y toopresent que con información de hello precisó de problema de hello toodiagnose. Esto es exactamente lo que hace Application Insights.

### <a name="where-do-bugs-come-from"></a>¿De dónde proceden los errores?
Los errores de los sistemas web proceden normalmente de problemas de configuración o de interacciones incorrectas entre sus muchos componentes. ¿Hola primera tarea cuando se realiza para un incidente de sitio en vivo, por tanto, es tooidentify lugar Hola problema hello: qué componente o la relación es la causa de hello?

Algunos de nosotros, los más veteranos, podemos recordar una época más sencilla en la que un programa informático se ejecutaba en un equipo. los desarrolladores de Hello harían probarlo minuciosamente antes de enviarlo; y podría tener enviado, vea rara vez o pensar nuevo. los usuarios de Hello tendrían tooput con errores residual de Hola durante muchos años. 

Ahora, las cosas son muy diferentes. La aplicación tiene una gran cantidad de diferentes dispositivos toorun en, y puede ser difícil tooguarantee Hola mismo comportamiento en cada uno de ellos. Hospedaje de aplicaciones en la nube de hello significa que se pueden corregir rápidamente, pero también significa expectativa hello y competencia continua de nuevas características a intervalos frecuentes. 

En estas condiciones, hello solo tookeep de manera que es un control estricto de número de errores de hello automatiza pruebas unitarias. Sería imposible toomanually volver a probar todo el contenido de cada entrega. Prueba unitaria es ahora una parte común de hello el proceso de compilación. Ayuda de las herramientas como hello Xamarin Test Cloud proporcionando las pruebas en varias versiones de explorador de IU automatizada. Estas pruebas regímenes nos permiten toohope esa tasa de Hola de errores que se encuentran dentro de una aplicación puede mantenerse tooa mínimo.

Las aplicaciones web típicas tienen muchos componentes activos. En el cliente de toohello de suma (en una aplicación de explorador o dispositivo) y el servidor web de hello, hay procesamiento sustancial de back-end de toobe probable. Quizás Hola back-end es una canalización de componentes, o una colección de piezas colaborar más flexible. Y muchos de ellos no estarán bajo su control, y son servicios externos de los que depende.

En configuraciones de este tipo, puede ser difícil y uneconomical tootest, o prevé, cada modo de error posibles, distinto de Hola live propio sistema. 

### <a name="questions-"></a>Preguntas...
Algunas preguntas que hacemos cuando desarrollamos un sistema web:

* ¿Se bloqueará mi aplicación? 
* ¿Qué ha sucedido exactamente? -Si se produjo un error de una solicitud, deseo tooknow cómo llegó hasta allí. Necesitamos un seguimiento de eventos...
* ¿Es mi aplicación lo suficientemente rápida? ¿Durante cuánto tiempo tarda toorespond tootypical solicitudes?
* ¿Puede cargar Hola Hola de identificador de servidor? ¿Cuando aumenta la tasa de Hola de solicitudes, el tiempo de respuesta de hello mantenga constante?
* La capacidad de respuesta son mis dependencias - Hola API de REST, las bases de datos y otros componentes que llama a la aplicación. ¿En particular, si el sistema de hello es lento, es el componente o, estoy obteniendo lentitud de otra persona?
* ¿Está mi aplicación activa o inactiva? ¿Se puede ver desde mundo Hola? Quiero saber si se detiene....
* ¿Cuál es la causa de hello? ¿Produjo error de hello en el componente o una dependencia? ¿Es un problema de comunicación?
* ¿Cuántos usuarios están afectados? ¿Si tengo tootackle de más de un problema, que es más importante de hello?

## <a name="what-is-application-insights"></a>¿Qué es Application Insights?
![Flujo de trabajo básico de Application Insights](./media/app-insights-devops/020.png)

1. Application Insights instrumenta la aplicación y envía la telemetría sobre él mientras se está ejecutando la aplicación hello. Puede generar Hola Application Insights SDK en la aplicación hello, o puede aplicar Instrumental en tiempo de ejecución. método anterior de Hello es más flexible, tal y como se puede agregar sus propios módulos regulares toohello de telemetría.
2. telemetría Hola se envía el portal de Application Insights toohello, donde se almacenan y procesan. (Aunque Application Insights se hospeda en Microsoft Azure, puede supervisar cualquier aplicación web, no solo las de Azure).
3. telemetría Hola se presenta tooyou en forma de Hola de gráficos y tablas de eventos.

Hay dos tipos principales de telemetría: instancias agregadas y sin formato. 

* Por ejemplo, los datos de instancia incluyen un informe de una solicitud que ha recibido la aplicación web. Puede buscar e inspeccionar Hola detalles de una solicitud mediante la herramienta de búsqueda de hello en el portal de Application Insights Hola. instancia de Hello podría incluir datos como cuánto tiempo la aplicación tardó toorespond toohello solicitud, así como Hola dirección URL solicitada, ubicación aproximada del cliente de Hola y otros datos.
* Datos agregados incluyen recuentos de eventos por unidad de tiempo, por lo que puede comparar la tasa de Hola de solicitudes con tiempos de respuesta de Hola. También incluyen los promedios de las métricas, como los tiempos de respuesta de solicitud.

Hola categorías principales de datos son:

* Las solicitudes tooyour aplicación (normalmente las solicitudes HTTP), con datos en la dirección URL, el tiempo de respuesta y el éxito o error.
* Dependencias: llamadas de REST y SQL realizadas por la aplicación, también con identificador URI, tiempos de respuesta y éxito.
* Excepciones, que incluyen seguimientos de pila.
* Datos de vista de página, que proceden de los exploradores de los usuarios de Hola.
* Métricas, como contadores de rendimiento, y métricas escritas por usted mismo. 
* Eventos personalizados que puede utilizar los eventos del negocio tootrack
* Seguimientos de registros usados para la depuración.

## <a name="case-study-real-madrid-fc"></a>Caso práctico: Real Madrid C.F.
Hola servicio web de [Real Madrid fútbol Club](http://www.realmadrid.com/) actúa aproximadamente 450 millones ventiladores alrededor de Hola a todos. Ventiladores acceso tanto a través de los exploradores web y Hola aplicaciones móviles de Club. No solo reservan entradas, sino que también acceden a información y a clips de vídeo sobre resultados, jugadores y próximos partidos. Pueden realizar búsquedas con filtros, como el número de goles marcados. También hay medios toosocial de vínculos. experiencia de usuario de Hello altamente personalizada y se ha diseñado como un ventiladores de tooengage de comunicación bidireccional.

Hola solución [es un sistema de servicios y aplicaciones en Microsoft Azure](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx). La escalabilidad es un requisito clave: el tráfico es variable y puede alcanzar volúmenes elevados antes y durante los partidos.

Madrid para Real, es rendimiento del sistema de vital toomonitor Hola. Visión de la aplicación de Azure proporciona una vista completa en todo el sistema de hello, garantizar un nivel de confianza y alto de servicio. 

Hola Club también obtiene una descripción detallada de los ventiladores: donde estén (solo el 3% están en España), ¿qué interés tienen en reproductores, resultados anteriores y próximos juegos y cómo responden los resultados de toomatch.

La mayoría de estos datos de telemetría se recopilan automáticamente sin el código agregado, lo que simplifica la solución de Hola y reduce la complejidad operativa.  Para el Real Madrid, Application Insights trata con 3800 millones de puntos de datos de telemetría al mes.

Madrid real utiliza Hola Power BI módulo tooview su telemetría.

![Vistas de telemetría de Application Insights en Power BI](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>Detección inteligente
[Proactive diagnostics](app-insights-proactive-diagnostics.md) es una característica reciente. Sin ninguna configuración especial por parte del usuario, Application Insights detecta y le avisa automáticamente de cualquier aumento en la tasa de errores en la aplicación. Es lo suficientemente inteligente como tooignore un fondo de errores ocasionales y también se eleva que son proporcionados simplemente tooa aumento en las solicitudes. Por ejemplo, si se produce un error en uno de los servicios de Hola que depende de, o si Hola nueva compilación que acaba de implementar no funciona tan bien, a continuación, podrá saberlo tan pronto como se observa el correo electrónico. (Y hay webhooks para que pueda desencadenar otras aplicaciones).

Otro aspecto de esta característica realiza un análisis exhaustivo diario de la telemetría, buscando patrones poco habituales de rendimiento que están toodiscover de disco duro. Por ejemplo, puede encontrar un rendimiento lento asociado a una zona geográfica determinada, o a una versión de explorador determinada.

En ambos casos, Hola alerta no solo indica Hola síntomas que se detecte, pero también proporciona datos que necesita toohelp diagnosticar Hola problema, tales como los informes de excepción correspondiente.

![Correo electrónico procedente de diagnóstico proactivo](./media/app-insights-devops/030.png)

El cliente Samtec afirmaba: "Durante una migración reciente de características, nos encontramos con una base de datos no escalada lo suficiente que estaba llegando al límite de sus recursos y ocasionando tiempos de espera. Las alertas de detección automático llegó a través literalmente tal y como se estábamos clasificación de problema de hello, muy prácticamente en tiempo real que se anuncia. Esta alerta junto con las alertas de la plataforma Windows Azure de hello nos ayudaron a casi al instante corregir el problema de Hola. Tiempo de inactividad total < 10 minutos".

## <a name="live-metrics-stream"></a>Secuencia de métricas en directo
Implementar la compilación más reciente de hello puede ser una experiencia ansiosa. Si hay algún problema, desea tooknow sobre ellos inmediatamente, por lo que puede revertir si es necesario. La secuencia de métricas activas le proporciona métricas claves con una latencia de aproximadamente un segundo.

![Métricas activas](./media/app-insights-devops/040.png)

Y le permite inspeccionar inmediatamente una muestra de los errores o excepciones.

![Eventos de error en vivo](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>Mapa de aplicación
Asignación de la aplicación detecta automáticamente la topología de la aplicación, para presentar información de rendimiento de hello situadas encima, toolet identificar fácilmente los cuellos de botella de rendimiento y flujos de problemáticos en su entorno distribuido. Permite toodiscover las dependencias de aplicación en los servicios de Azure. Puede evaluar problema Hola comprender si está relacionada con el código o dependencias relacionadas con y desde un único lugar profundizar diagnóstico relacionados con experiencia. Por ejemplo, la aplicación puede tener errores debido a una degradación del tooperformance de nivel de SQL. Con la asignación de la aplicación, puede ver de forma inmediata y profundizar Hola Asesor de índices de SQL o información de consultas de la experiencia.

![Mapa de aplicación](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Application Insights Analytics
Con [Analytics](app-insights-analytics.md), puede escribir consultas arbitrarias en un lenguaje avanzado, tipo SQL.  Diagnosticar a través de la pila de toda aplicación Hola resulta sencillo conectarse varias perspectivas y puede pedir Hola preguntas adecuadas toocorrelate rendimiento del servicio con métricas empresariales y la experiencia del cliente. 

Puede consultar todas las métricos datos sin formato almacenados en el portal de Hola y la instancia de telemetría. lenguaje de Hello incluye filtro, combinación, agregación y otras operaciones. Puede calcular campos y realizar análisis estadísticos. Dispone de visualizaciones tanto gráficas como tabulares.

![Gráfico de consultas y resultados de Analytics](./media/app-insights-devops/025.png)

Por ejemplo, es fácil:

* Segmentar los datos de rendimiento por parte del cliente de capas toounderstand su experiencia de solicitud de la aplicación.
* Buscar códigos de error específicos o nombres de eventos personalizado durante las investigaciones del sitio activo.
* Profundizar en uso de la aplicación hello de clientes concretos toounderstand cómo se adquieren y adoptadas características.
* Realizar un seguimiento de las sesiones y tiempos de respuesta para usuarios específicos tooenable compatibilidad y soporte técnico cliente instantánea de tooprovide de los equipos de operaciones.
* Determinar la aplicación de uso frecuente características tooanswer característica priorización preguntas.

Cliente DNN dice: "Application Insights nos ha proporcionado con hello falta parte de la ecuación de Hola para ser capaz de toocombine, ordenación, consulta y filtrar los datos según sea necesario. Permitir que nuestro equipo toouse su propios toofind imaginación y experiencia datos con un lenguaje de consulta eficaces nos ha permitido toofind visión y solucionar problemas que incluso no sabemos que ha surgido. Un gran número de respuestas interesantes proceden de preguntas de Hola a partir de *' se pregunte si...'.*"

## <a name="development-tools-integration"></a>Integración de herramientas de desarrollo
### <a name="configuring-application-insights"></a>Configuración de Application Insights
Visual Studio y Eclipse tengan herramientas tooconfigure Hola correcto SDK paquetes para proyecto de Hola que esté desarrollando. Hay un tooadd de comando de menú Application Insights.

Si se encontrara toobe con un marco de registro de seguimiento como System.Diagnostics.Trace, NLog o Log4N, a continuación, que obtuvo Hola opción toosend Hola registros tooApplication visión junto con hello otro telemetría, para que fácilmente puede correlacionar los seguimientos de hello con las solicitudes , las llamadas de dependencia y las excepciones.

### <a name="search-telemetry-in-visual-studio"></a>Telemetría de búsqueda en Visual Studio
Al desarrollar y depurar una característica, puede ver y buscar Hola telemetría directamente en Visual Studio mediante Hola mismo Buscar instalaciones como en el portal web de Hola.

Y cuando visión de la aplicación inicia una excepción, puede ver el punto de datos de hello en Visual Studio y saltar código relevante toohello recta.

![Búsqueda de Visual Studio](./media/app-insights-devops/060.png)

Durante la depuración, tiene telemetría de hello opción tookeep hello en el equipo de desarrollo, verlo en Visual Studio, pero sin enviar toohello portal. Esta opción local evita mezclar la depuración con la telemetría de producción.

### <a name="build-annotations"></a>Anotaciones de compilación
Si utiliza Visual Studio Team Services toobuild e implementar la aplicación, las anotaciones de implementación se mostrarán en los gráficos en el portal de Hola. Si la versión más reciente tenía ningún efecto en las métricas de hello, resulta obvio.

![Anotaciones de compilación](./media/app-insights-devops/070.png)

### <a name="work-items"></a>Elementos de trabajo
Cuando se genera una alerta, Application Insights puede crear automáticamente un elemento de trabajo en su sistema de seguimiento de trabajos.

## <a name="but-what-about"></a>Pero, ¿y qué sucede con...?
* [Privacidad y almacenamiento](app-insights-data-retention-privacy.md) : la telemetría se mantiene en servidores seguros de Azure.
* Rendimiento - impacto hello es muy bajo. la telemetría se procesa por lotes.
* [Precios](app-insights-pricing.md) : puede comenzar de forma gratuita y continuar así mientras el volumen sea bajo.


## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Pasos siguientes
Empezar a usar Application Insights es fácil. Opciones de Hello principales son:

* Instrumentar una aplicación web ya en ejecución. Esto proporciona todos los telemetría de rendimiento integrados de Hola. Está disponible para [Java](app-insights-java-live.md) y [servidores IIS](app-insights-monitor-performance-live-website-now.md), así como para [Azure Web Apps](app-insights-azure.md).
* Instrumentar el proyecto durante el desarrollo. Puede hacerlo para aplicaciones de [ASP.NET](app-insights-asp-net.md) o [Java](app-insights-java-get-started.md), así como para [Node.js](app-insights-nodejs.md) y [otros tipos](app-insights-platforms.md). 
* Instrumentar [cualquier página web](app-insights-javascript.md) agregando un fragmento de código corto.

