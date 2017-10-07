---
title: aaaOverview de Azure Application Insights para DevOps | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Application Insights en un entorno de desarrollo Ops."
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>Información general de Application Insights para DevOps

Con [Application Insights](app-insights-overview.md) puede averiguar rápidamente cómo está funcionando su aplicación y cómo se está usando cuando está activa. Si hay un problema, le permite conocer, ayuda a evaluar el impacto de Hola y ayuda a determinar la causa de Hola.

A continuación se muestra una cuenta de un equipo que desarrolla aplicaciones web:

* *"Hace un par de días implementamos una revisión 'secundaria'. No ejecutar un paso de prueba amplia, pero lamentablemente se combina los algún cambio inesperado en la carga de hello, provocando incompatibilidad entre la parte delantera de Hola y back-ends. Inmediatamente, excepciones de servidor aumentaron, que se desencadena la alerta y se estábamos conocen la existencia de la situación de Hola. Unos pocos clics inmediatamente en el portal de Application Insights hello, que obtuvimos suficiente información de toonarrow de pilas de llamadas de excepción problema Hola. Se revierte inmediatamente y limita los daños de Hola. Application Insights ha realizado esta parte de hello devops ciclo muy sencilla y útil."*

En este artículo se siga un equipo en el banco de Fabrikam que desarrolla Hola online de banca toosee de sistema (OBS) cómo Application Insights tooquickly responder toocustomers y realizar actualizaciones.  

equipo de Hello trabaja en un ciclo de DevOps representado en hello siguiente ilustración:

![Ciclo de DevOps](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

Los requisitos son la fuente del trabajo pendiente de desarrollo (lista de tareas). En resumen funcionan sprints, que a menudo entregar software que funciona - normalmente en forma de Hola de mejoras y extensiones de aplicación existente toohello. aplicación de Hello en vivo se actualiza frecuentemente con nuevas características. Mientras está activa, el equipo de Hola supervisa para rendimiento y el uso con la Ayuda de Hola de Application Insights. Estos datos de APM se retroalimentan en su trabajo pendiente de desarrollo.

equipo de Hello utiliza toomonitor de aplicación web en directo Application Insights hello estrechamente para:

* Rendimiento. Desean toounderstand cómo tiempos de respuesta varían según el número de solicitudes; ¿cuánto se sirven CPU, red, discos y otros recursos; y dónde están los cuellos de botella de Hola.
* Errores. Si hay excepciones o errores de solicitud, o si un contador de rendimiento queda fuera del intervalo se encuentra cómodo, Hola equipo necesidades tooknow rápidamente para que pueda tomar la acción.
* Uso. Siempre que se publique una nueva característica, equipo de hello desee tooknow toowhat extensión se usa y, si los usuarios tienen dificultades con él.

Este artículo nos centraremos en la parte de comentarios de Hola del ciclo de hello:

![Detect-Triage-Diagnose](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Detección de disponibilidad insuficiente
Marcela Markova es un desarrollador senior en el equipo OBS hello y toma Hola responsable de supervisar el rendimiento en línea. Configura varias [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md):

* Una prueba de direcciones URL de la página de aterrizaje principal de hello para la aplicación hello, http://fabrikambank.com/onlinebanking/. Establece los criterios de código HTTP 200 y el texto 'Welcome!'. Si se produce un error en esta prueba, hay algo no funciona bien con la red de Hola o servidores de Hola o puede ser un problema de implementación. (O alguien ha cambiado Hola bienvenida! mensaje en la página Hola sin advertencia su conocidos).
* Una prueba de varios paso más profunda, que inicia una sesión y obtiene una lista de cuentas actuales, y donde se comprueban algunos detalles importantes en cada página. Esta prueba comprueba que esa base de datos de cuentas de hello vínculo toohello funciona. Marcela usa un identificador de cliente ficticio: se mantienen algunos de ellos con fines de prueba.

Con estas pruebas configurar, Marcela esté seguro de que ese equipo Hola sabrá rápidamente sobre cualquier interrupción.  

Errores se muestran como puntos rojos en gráfico de prueba de hello web:

![Presentación de las pruebas web que se han ejecutado en hello anterior período](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Pero lo más importante es que una alerta sobre cualquier error se envían por correo electrónico toohello equipo de desarrollo. De esa manera, saberlo antes de que prácticamente todos los clientes de Hola.

## <a name="monitor-performance"></a>Supervisión del rendimiento
En la página de información general de hello en Application Insights, hay un gráfico que muestra una variedad de [mediciones clave](app-insights-web-monitor-performance.md).

![Varias métricas](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

El tiempo de carga de la página del explorador se obtiene de la telemetría enviada directamente desde las páginas web. Tiempo de respuesta de servidor, número de solicitudes de servidor y número de solicitudes con error son todos, medidos en el servidor web de Hola y envía información de tooApplication desde allí.

Marcela es ligeramente interesarán gráfico de respuesta del servidor de Hola. Este gráfico muestra el tiempo medio de hello entre cuando servidor hello recibe una solicitud HTTP de explorador del usuario y, cuando devuelve la respuesta Hola. No es inusual toosee una variación en este gráfico, tal y como se carga en el sistema de hello varía. Pero en este caso, parece que hay toobe una correlación entre los pequeño se eleva Hola recuento de las solicitudes y grande aumenta en el tiempo de respuesta de Hola. Podría indicar que el sistema de hello funciona solo en sus límites.

Abre los gráficos de servidores de hello:

![Varias métricas](./media/app-insights-detect-triage-diagnose/06.png)

No parece que hay toobe ningún inicio de sesión de limitación de recursos, por lo que quizá Hola resaltes en los gráficos de respuesta del servidor de hello son simplemente una coincidencia.

## <a name="set-alerts-toomeet-goals"></a>Establecer alertas toomeet objetivos
Sin embargo, le gustaría que tookeep un ojo en tiempos de respuesta de Hola. Si salen demasiado altos, que desea tooknow sobre él inmediatamente.

Así que establece una [alerta](app-insights-metrics-explorer.md) para conocer los tiempos de respuesta que superen el umbral habitual. Esto le da la seguridad de que obtendrá información si los tiempos de respuesta son lentos.

![Agregar hoja de alertas](./media/app-insights-detect-triage-diagnose/07-alerts.png)

Las alertas se pueden establecer según una amplia variedad de métricas. Por ejemplo, puede recibir mensajes de correo electrónico si se vuelve alto número de excepción de Hola o memoria disponible de hello entra baja, o si se produce un pico en las solicitudes de cliente.

## <a name="stay-informed-with-smart-detection-alerts"></a>Mantenerse informado con las alertas de detección inteligente
El día siguiente, llega una alerta de Application Insights por correo electrónico. Pero, al que lo abre, busca no es alerta de tiempo de respuesta de Hola que ha configurado. En lugar de eso, le indica que se ha producido un aumento repentino de las solicitudes con error; es decir, las solicitudes que han devuelto 500 códigos de error o más.

Las solicitudes con error son que los usuarios han visto un error - normalmente tras una excepción que se produce en el código de hello. Quizás verán un mensaje que dice "Lo sentimos, no pudimos actualizar sus datos ahora" O bien, en el peor de errores absoluto, un volcado de la pila aparece en pantalla del usuario de hello, por cortesía de servidor web de Hola.

Esta alerta es una sorpresa, porque hello última vez que examinando, hello de solicitudes con error fue encouragingly bajo recuento. Un pequeño número de errores es toobe esperado en un servidor ocupado.

También era un poco de una sorpresa por ella porque incluso no tiene tooconfigure esta alerta. Application Insights incluyen Detección inteligente. Ajusta automáticamente el patrón de error habitual de la aplicación tooyour y errores "se acostumbra a" en una página concreta o bajo una carga elevada o las métricas de tooother vinculado. Genera una alarma de hello solo si hay un aumento por encima de lo que incluye tooexpect.

![correo electrónico de diagnóstico proactivo](./media/app-insights-detect-triage-diagnose/21.png)

Se trata de un correo electrónico muy útil. No solo genera una alarma. Esto consigue una gran cantidad de evaluación de errores de Hola y el trabajo de diagnóstico, demasiado.

Muestra cuántos clientes se ven afectados y en qué páginas web u operaciones. Marcela puede decidir si necesita trabajar en el objeto como un simulacro de todo equipo tooget hello, o si puede omitirla hasta que la semana próxima.

correo electrónico de Hello también muestra que se ha producido una excepción determinada y - aún más interesante - ese error Hola está asociado a la base de datos de errores de llamadas tooa determinada. Esto explica por qué error Hola parecía repentinamente incluso aunque el equipo del Marcela no ha implementado recientemente las actualizaciones.

Marcella hace ping líder de Hola de equipo de base de datos de hello basándose en este correo electrónico. Ella se entera de que libere una revisión en hello último media hora; y no es posible que se haya producido un cambio de esquema secundaria...

Por lo tanto problema hello es en hello forma toobeing fijo, incluso antes de investigación de registros y dentro de 15 minutos de la misma que se deriven. Sin embargo, Marcela hace clic en el vínculo de hello tooopen Application Insights. Se abre directamente en una solicitud con error y, puede ver la base de datos de error al llamar a en la lista asociada de Hola de llamadas de dependencia.

![solicitud con error](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Detectar excepciones
Con un poco de la instalación, [excepciones](app-insights-asp-net-exceptions.md) son tooApplication notificado visión automáticamente. También se pueden capturar explícitamente mediante la inserción de llamadas demasiado[TrackException()](app-insights-api-custom-events-metrics.md#trackexception) en código de hello:  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


equipo de Fabrikam Bank Hola ha evolucionado práctica Hola de siempre enviar telemetría produce una excepción, a menos que haya una recuperación obvia.  

De hecho, es incluso más amplio que el que su estrategia: enviar telemetría en todos los casos donde el cliente de hello es frustrado en lo que deseaban toodo, si corresponde tooan excepción en el código de hello o no. Por ejemplo, si sistema de transferencia bancaria entre externa Hola devuelve un mensaje "no se puede completar esta transacción" por algún motivo operativa (ningún error de cliente hello), a continuación, hacen un seguimiento de ese evento.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException es tooreport usado excepciones porque envía una copia de la pila de Hola. TrackEvent es tooreport usado otros eventos. Puede vincular cualquier propiedad que podría resultar útil en el diagnóstico.

Excepciones y eventos aparecen en hello [búsqueda diagnóstico](app-insights-diagnostic-search.md) hoja. Puede profundizar en ellos propiedades adicionales de toosee hello y seguimiento de pila.

![En la búsqueda de diagnóstico, utilice filtros tooshow determinados tipos de datos](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Supervisar de forma proactiva
Marcela no se sienta de brazos cruzados a esperar las alertas. Poco después de cada nueva implementación, echa un vistazo a [tiempos de respuesta](app-insights-web-monitor-performance.md) : ambos Hola figura general y recuentos de tabla Hola de solicitudes más lentas, así como la excepción.  

![Gráfico de tiempo de respuesta y cuadrícula de tiempos de respuesta del servidor.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

Puede evaluar el efecto de rendimiento de Hola de cada implementación normalmente comparar cada semana con hello última. Si hay un aumento repentino, genera con desarrolladores de hello relevante.

## <a name="triage-issues"></a>Problemas de evaluación de errores
Evaluación de prioridades: evaluar la gravedad de Hola y el alcance de un problema - es Hola primer paso después de la detección. ¿Debemos llamamos out equipo Hola a medianoche? ¿O bien, puede dejarse hasta Hola siguiente cómoda intervalo sin trabajo pendiente de hello? Hay algunas cuestiones importantes en la evaluación de errores.

¿Con qué frecuencia está sucediendo? gráficos de Hello en la hoja de información general de hello proporcionan algún problema de tooa de perspectiva. Por ejemplo, Fabrikam aplicación Hola genera alertas de prueba web cuatro una noche. Examinar el gráfico de Hola de mañana Hola, equipo Hola percibirá que había hecho algunos puntos rojos, si sigue la mayoría de las pruebas de hello estuviera verde. Obtención de detalles de gráfico de disponibilidad de hello, resultaba evidente que todos estos problemas intermitentes proceden de ubicación de una prueba. Se trataba obviamente de un problema de red que afectaba a una sola ruta, y es probable que se aclarara por sí solo.  

Por el contrario, un aumento significativo y estable en el gráfico de Hola de recuentos de excepción o tiempos de respuesta Obviamente, es algo toopanic sobre.

Una táctica de evaluación de errores útil es probarlo usted mismo. Si experimenta Hola mismo problema, sabrá que es real.

¿Qué fracción de usuarios se ven afectados? tooobtain una respuesta aproximada, divida la tasa de error de Hola por recuento de sesiones de Hola.

![Gráficos de las solicitudes y sesiones con error](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

Cuando hay lentitud, comparar tabla Hola de solicitudes más lentas responde con frecuencia de uso de Hola de cada página.

¿Qué importancia tiene escenario Hola bloqueado? ¿Se trata de un problema funcional que bloquea un caso de usuario determinado?, ¿tiene mucha importancia? Si los clientes no pueden pagar sus facturas, esto es grave; si no pueden cambiar sus preferencias de color de pantalla, quizás pueda esperar. Hola detalles del evento de Hola o la excepción o identidad de Hola de página lenta hello, indica que los clientes están teniendo problemas.

## <a name="diagnose-issues"></a>Diagnosticar problemas
Un diagnóstico más detallado no es bastante Hola igual a la depuración. Antes de iniciar el seguimiento a través del código de hello, debe tener una idea aproximada de por qué, cuándo y dónde se está produciendo el problema de Hola.

**¿Al ocurrir?**  vista histórica de hello proporciona gráficos de evento y una métrica de hello resulta fácil toocorrelate efectos con las causas posibles. Si hay subidas intermitentes en las tasas de tiempo o de una excepción de respuesta, busque en el número de solicitudes de hello: si alcanza el máximo en hello mismo tiempo, a continuación, parece que un problema de recursos. ¿Necesita tooassign más CPU o memoria? ¿O es una dependencia que no puede administrar la carga de hello?

**¿Somos nosotros?**  Si tiene una disminución repentina en el rendimiento de un determinado tipo de solicitud - por ejemplo cuando Hola cliente espera un extracto de cuenta: no hay una posibilidad podría ser un subsistema externo en lugar de la aplicación web. En el Explorador de métricas, seleccione la tasa de error de dependencia de Hola y las tasas de duración de la dependencia y comparar sus historiales sobre hello más allá de algunas horas o días, y ha detectado un problema de Hola. Si se correlación de cambios, un subsistema externo podría ser tooblame.  

![Gráficos de error de dependencia y la duración de llamadas toodependencies](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Algunos problemas de dependencia lenta son problemas de ubicación geográfica. Fabrikam Bank usa máquinas virtuales de Azure, y descubrieron que habían ubicado sin darse cuenta el servidor web y el servidor de cuentas en distintos países. Migrando uno de ellos, se obtuvo una mejora considerable.

**¿Qué hicimos?** Si el problema de hello no parece toobe una dependencia, y si no estaba siempre existe, puede deberse a un cambio reciente. Hello perspectiva histórica proporciona gráficos de métricas y eventos de hello resulta fácil toocorrelate los cambios repentinos con las implementaciones. Que limita la búsqueda de hello para el problema de Hola.

**¿Qué está ocurriendo?** Algunos problemas se producen sólo en raras ocasiones y pueden ser difícil tootrack hacia abajo probando sin conexión. Error de tootry toocapture Hola todo podemos hacer es cuando se produce en vivo. Puede inspeccionar los volcados de pila hello en los informes de excepción. Además, puede escribir llamadas de seguimiento con su plataforma de registro favorita o con TrackTrace() o TrackEvent().  

Fabrikam tenía un problema intermitente con las transferencias entre cuentas, pero solo con determinados tipos de cuenta. toounderstand mejor lo que estaba sucediendo, insertan llamadas TrackTrace() en determinados puntos clave en el código de hello, asociar el tipo de cuenta de hello como una llamada a tooeach de propiedad. Que hizo fácil toofilter out únicamente los seguimientos en la búsqueda de diagnóstico. También asocian valores de parámetro como llamadas de seguimiento de toohello de propiedades y las medidas.

## <a name="respond-toodiscovered-issues"></a>Responder toodiscovered problemas
Una vez que se ha diagnosticado problema hello, puede realizar un toofix plan lo. Tal vez necesite tooroll volver cambios recientes o quizás se puede seguir adelante y corregirlo. Una vez que se realiza la corrección de hello, Application Insights indica si se realizó correctamente.  

Equipo de desarrollo de Fabrikam Bank tomar una medida de tooperformance enfoque estructurada más de lo que solían toobefore recurrían Application Insights.

* Objetivos de rendimiento en cuanto a medidas específicas establecen en la página de información general de Application Insights de Hola.
* Diseñar las medidas de rendimiento en la aplicación hello desde el principio de hello, como las métricas de Hola que miden el progreso de usuario a través de 'Embudos'.  


## <a name="monitor-user-activity"></a>Supervisar la actividad del usuario
Cuando el tiempo de respuesta es una buena coherencia y hay pocas excepciones, puede mover equipo de desarrollo de hello en toousability. Puede pensar en cómo tooimprove Hola experiencia del usuario y cómo tooencourage más hello de tooachieve usuarios deseado objetivos.

Visión de la aplicación también puede ser usado toolearn hacer lo que los usuarios con una aplicación. Una vez que se ejecuta sin problemas, equipo de hello gustaría tooknow qué características están hello más popular, lo que, como usuarios o que tienen dificultades con, y la frecuencia con que vuelvan. Eso ayudará a establecer prioridades en su próximo trabajo. Y puede planear correcto de hello toomeasure de cada característica como parte del ciclo de desarrollo de Hola. 

Por ejemplo, un viaje de usuario típico a través del sitio web de hello tiene un claro "embudo". Muchos clientes recurren a velocidades de Hola de diferentes tipos de préstamo. Un número más pequeño vaya toofill en forma de expresión de código delimitada de Hola. De aquellos usuarios que tengan una cita, algunos continúe y retire préstamo Hola.

![Recuentos de vistas de página](./media/app-insights-detect-triage-diagnose/12-funnel.png)

Teniendo en cuenta que quitan Hola números mayores de clientes, business Hola puede elaborar cómo tooget más usuarios a través de la parte inferior de toohello de Hola de embudo. En algunos casos, podría haber un error (UX) de la experiencia del usuario: por ejemplo, el botón 'siguiente' hello es toofind de disco duro o instrucciones de hello no son evidentes. Lo más probable, hay más significativos motivos empresariales para incompletas: quizás son demasiado altas tasas de préstamos de Hola.

Cualesquiera motivos hello, datos de hello ayudan Hola equipo a averiguar lo que hacen los usuarios. Seguimiento más llamadas pueden ser inserta toowork más detalles. TrackEvent() puede ser usado toocount ninguna acción del usuario, de detalle de Hola de clics de botón individual, logros toosignificant como buenos resultados un préstamo.

equipo de Hello está obteniendo toohaving usa información acerca de la actividad de usuario. En la actualidad, cada vez que diseñan una nueva característica, calculan cómo obtendrán comentarios de su uso. Diseñan llamadas de seguimiento en función de Hola desde el principio de Hola. Usan características de hello comentarios tooimprove hello en cada ciclo de desarrollo.

[Más información sobre el seguimiento del uso](app-insights-usage-overview.md).

## <a name="apply-hello-devops-cycle"></a>Aplicar ciclo de hello DevOps
Así es cómo un uso de equipo Application Insights individuales no solo toofix emite, pero tooimprove su ciclo de vida de desarrollo. Espero que les haya dado algunas ideas sobre cómo Application Insights puede ayudarle con la administración del rendimiento de sus propias aplicaciones.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Pasos siguientes
Puede comenzar a trabajar de varias maneras, dependiendo de las características de saludo de la aplicación. Seleccione lo que más le convenga:

* [Aplicación web ASP.NET](app-insights-asp-net.md)
* [Aplicación web de Java](app-insights-java-get-started.md)
* [Aplicación web de Node.js](app-insights-nodejs.md)
* Aplicaciones ya implementadas hospedadas en [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md) o [Azure](app-insights-azure.md).
* [Páginas Web](app-insights-javascript.md) -aplicación de una sola página o una página web normal - utilizarse por sí mismo o en tooany de adición de opciones de servidor hello.
* [Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) tootest Hola de la aplicación desde internet público.
