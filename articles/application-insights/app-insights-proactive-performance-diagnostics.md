---
title: "aaaSmart - detección de anomalías de rendimiento | Documentos de Microsoft"
description: "Application Insights realiza un análisis inteligente de la telemetría de su aplicación y le advierte de los posibles problemas. Esta característica no necesita ninguna configuración."
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>Detección inteligente: anomalías de rendimiento

[Application Insights](app-insights-overview.md) automáticamente analiza el rendimiento de saludo de la aplicación web y puede avisarle sobre posibles problemas. Podría estar leyendo este artículo porque ha recibido una de nuestras notificaciones de detección inteligente.

Esta característica no requiere ninguna configuración especial, tan solo ajustar los parámetros de la aplicación para Application Insights (en [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md) o [Node.js](app-insights-nodejs.md), así como en el [código de la página web](app-insights-javascript.md)). Se activará cuando la aplicación genera suficientes datos de telemetría.

## <a name="when-would-i-get-a-smart-detection-notification"></a>¿Cuándo recibiría una notificación de detección inteligente?

Visión de la aplicación ha detectado que el rendimiento de saludo de la aplicación ha disminuido en una de estas maneras:

* **Degradación de tiempo de respuesta** -se ha iniciado la aplicación responde toorequests más lentamente que antes. cambio de Hello puede haber sido rápido, por ejemplo porque no había una regresión en la implementación más reciente. También podría haber sido gradual, probablemente debido a una fuga de memoria. 
* **Degradación de la duración de dependencia** -la aplicación realiza llamadas API de REST de tooa, base de datos u otra dependencia. dependencia de Hello responde más lentamente que antes.
* **Patrón de un rendimiento lento** -la aplicación aparece toohave emitirá un rendimiento que está afectando a sólo algunas solicitudes. Por ejemplo, las páginas se cargan mucho más lentamente en un tipo de explorador que en otros, o las solicitudes se atienden de una forma más lenta desde un servidor concreto. En la actualidad, nuestros algoritmos examinan tiempos de carga de página, tiempos de respuesta de solicitud y tiempos de respuesta de dependencia.  

Detección inteligente requiere al menos 8 días de telemetría en un volumen factible en orden tooestablish una línea de base de rendimiento normal. Por lo tanto, después de que la aplicación se haya estado ejecutando durante ese periodo, se generará una notificación cuando se produzca un problema significativo.


## <a name="does-my-app-definitely-have-a-problem"></a>Entonces, ¿mi aplicación tiene un problema?

No, una notificación no significa que la aplicación tenga un problema. Es simplemente una sugerencia relacionada con algo que conviene toolook en forma más estrecha.

## <a name="how-do-i-fix-it"></a>¿Cómo puedo corregirlo?

las notificaciones de Hello incluir información de diagnóstico. Este es un ejemplo:


![Este es un ejemplo de detección de degradación del tiempo de respuesta del servidor](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **Evaluación de errores**. notificación de Hello muestra el número de usuarios o cuántas operaciones se ven afectadas. Esto puede ayudarle a asignar un problema de toohello de prioridad.
2. **Ámbito**. ¿Problema de hello afecta a todo el tráfico, o solo algunas páginas? ¿Está restringido de TI tooparticular exploradores o ubicaciones? Esta información puede obtenerse de notificación de Hola.
3. **Diagnóstico**. A menudo, información de diagnóstico de hello en la notificación de hello sugerirá naturaleza Hola de problema de Hola. Por ejemplo, si el tiempo de respuesta se ralentiza cuando la velocidad de solicitudes es alta, el problema podría estar en que su servidor o dependencias están sobrecargadas. 

    De lo contrario, abra hoja de rendimiento de hello en Application Insights. Allí encontrará los datos de [Profiler](app-insights-profiler.md). Si se detectan excepciones, también puede intentar hello [depurador instantánea](app-insights-snapshot-debugger.md).



## <a name="configure-email-notifications"></a>Configuración de notificaciones de correo electrónico

Las notificaciones de detección inteligentes se habilita de forma predeterminada y se envían toothose con [sus propietarios, contribuidores y lectores de tener acceso a recursos de Application Insights toohello](app-insights-resources-roles-access-control.md). toochange esto, haga clic en **configurar** en Hola notificación por correo electrónico o se abre la configuración de detección inteligente en Application Insights. 
  
  ![Configuración de Detección inteligente](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * Puede usar hello **cancelar la suscripción** vínculo en toostop de correo electrónico de detección inteligente de Hola recibir notificaciones de correo electrónico de Hola.

Mensajes de correo electrónico acerca de las anomalías de rendimiento de las detecciones inteligentes son correo electrónico de tooone limitado al día por recurso de Application Insights. se enviará correo electrónico de Hello solo si hay al menos un problema nuevo que se ha detectado ese día. No obtendrá repeticiones de ningún mensaje. 

## <a name="faq"></a>P+F

* *¿Entonces están mirando mis datos?*
  * No. servicio de Hello es completamente automático. Solo se reciben las notificaciones de Hola. Sus datos son [privados](app-insights-data-retention-privacy.md).
* *¿Se analizan todos los datos de hello recopilados por Application Insights?*
  * No en este momento. Actualmente, analizamos el tiempo de respuesta de la solicitud, el tiempo de respuesta de dependencia y el tiempo de carga de la página. En un futuro analizaremos más métricas.

* ¿En qué tipos de aplicación funciona?
  * Se detecta estos degradación en cualquier aplicación que genera la telemetría de hello adecuado. Si instaló Application Insights en su aplicación web, el seguimiento de las solicitudes y las dependencias se realiza automáticamente. Pero en servicios back-end u otras aplicaciones, si se hubiera insertado llamadas demasiado[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) o [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), detección inteligente funcionará en hello igual manera.

* *¿Puedo crear mis propias reglas de detección de anomalías o personalizar las existentes?*

  * Aún no, pero puede realizar lo siguiente:
    * [Configurar alertas](app-insights-alerts.md) que le indiquen cuándo una métrica cruza un umbral.
    * [Exportar telemetría](app-insights-export-telemetry.md) tooa [base de datos](app-insights-code-sample-export-sql-stream-analytics.md) o [tooPowerBI](app-insights-export-power-bi.md), donde se puede analizar usted mismo.
* *¿Con qué frecuencia se lleva a cabo análisis Hola?*

  * Ejecutamos analysis Hola diariamente de telemetría de Hola de hello anterior día (día completo en la zona horaria UTC).
* *¿Sustituye esto a las [alertas de métricas](app-insights-alerts.md)?*
  * No.  No asigne toodetecting cada comportamiento que podría considerar anómala.


* *¿Si no hacer nada en respuesta tooa notificación, obtendrá un aviso?*
  * No, obtendrá un mensaje sobre cada problema solo una vez. Si persiste el problema de Hola se actualizará en hello que detección inteligente fuente hoja.
* *He perdido el correo electrónico de Hola. ¿Dónde puedo encontrar las notificaciones de hello en el portal de hello?*
  * En información general de Application Insights hello de la aplicación, haga clic en hello **detección inteligente** icono. Se le toofind capaz de que realizar copias de todas las notificaciones de los días de too90.

## <a name="how-can-i-improve-performance"></a>¿Cómo puedo mejorar el rendimiento?
Las respuestas lenta pero no lo consiguió son uno de frustraciones más grandes de Hola para los usuarios del sitio web, como se indicó en su propia experiencia. Por lo tanto, es importante tooaddress Hola problemas.

### <a name="triage"></a>Evaluación de errores
En primer lugar, ¿es realmente importante? Si una página siempre está tooload lenta, pero sólo un 1% de los usuarios del sitio tienen alguna vez toolook en él, puede que tenga más importante toothink cosas sobre. En Hola otra parte, si solo 1% de los usuarios para abrirlo, pero produce excepciones cada vez, lo que podría ser conveniente investigar.

Utilizar la instrucción de impacto de hello (usuarios afectados o % de tráfico) como directriz general, pero tenga en cuenta que no es todo Hola. Recopilar otro tooconfirm evidencia.

Considere la posibilidad de parámetros de Hola de problema de Hola. Si es dependiente de la ubicación, configure [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) que incluyan la región: simplemente puede que haya problemas de red en esa área.

### <a name="diagnose-slow-page-loads"></a>Diagnostico de cargas de página lentas
¿Dónde está el problema de hello? ¿Es toorespond lento del servidor de hello, es muy larga de página de Hola o explorador hello tiene toodo una gran cantidad de trabajo toodisplay?

Abra la hoja de métricas de exploradores de Hola. Hola segmentada visualización del explorador página carga tiempo de muestra que se va tiempo Hola. 

* Si **tiempo de solicitud de envío** es alto, ya sea servidor hello responde lentamente o solicitud de hello es una publicación con una gran cantidad de datos. Mire hello [las métricas de rendimiento](app-insights-web-monitor-performance.md#metrics) tooinvestigate los tiempos de respuesta.
* Configurar [seguimiento de dependencias](app-insights-asp-net-dependencies.md) toosee si es la lentitud de hello debido tooexternal servicios o la base de datos.
* Si predomina la **recepción de respuesta** , la página y sus elementos dependientes (JavaScript, CSS, imágenes y demás, excluyendo los datos cargados de forma asincrónica) son largos. Configurar un [prueba de disponibilidad](app-insights-monitor-web-app-availability.md), y ser seguro tooset elementos dependientes de hello opción tooload. Cuando se obtienen algunos resultados, abrir detalle Hola de un resultado y expándalo toosee Hola tiempos de varios archivos de carga.
* Un **Tiempo de procesamiento del cliente** alto sugiere que los scripts se ejecutan con lentitud. Si motivo hello no es obvio, considere la posibilidad de agregar código de control de tiempo y enviar veces de hello en las llamadas de trackMetric.

### <a name="improve-slow-pages"></a>Mejora de páginas lentas
Hay un servidor web repleto de consejos sobre cómo mejorar las respuestas del servidor y los tiempos de carga de página, por lo que no intentaremos toorepeat todas aquí. Estas son algunas sugerencias que probablemente ya sabe sobre tooget simplemente está pensando en:

* Lenta cargar debido a los archivos de gran tamaño: cargar secuencias de comandos de Hola y otras partes de forma asincrónica. Use la agrupación de scripts. Salto de página principal de hello en widgets que cargan sus datos por separado. No enviar HTML antiguo sin formato para tablas de gran tamaño: usar una secuencia de comandos toorequest Hola de datos como JSON u otro formato compacto y luego rellenar tabla hello en su lugar. No hay marcos excelente toohelp con todo esto. (Lo que también implican grandes scripts, por supuesto.)
* Reducir las dependencias de servidor: considere la posibilidad de hello ubicaciones geográficas de sus componentes. Por ejemplo, si usa Azure, asegurarse de que servidor web de Hola y de base de datos de Hola Hola misma región. ¿Es posible que consultas las consultas recuperen más información de la que necesitan? ¿Podría ayudar el almacenamiento en caché o el procesamiento por lotes?
* Problemas de capacidad: mirar las métricas de servidor hello de tiempos de respuesta y solicitud de cuenta. Si los tiempos de respuesta presentan picos desproporcionados en recuentos de solicitud, es probable que se está tirando en exceso de los servidores.


## <a name="server-response-time-degradation"></a>Degradación del tiempo de respuesta del servidor

notificación de degradación de tiempo de respuesta de Hello indica lo siguiente:

* tiempo de respuesta de Hello en comparación con toonormal tiempo de respuesta para esta operación.
* El número de usuarios afectados.
* Tiempo medio de respuesta y tiempo de respuesta de percentil 90 para esta operación en el día de Hola de detección de Hola y 7 días antes. 
* Número de esta operación solicitudes en el día de Hola de detección de Hola y 7 días antes de.
* La correlación entre la degradación en esta operación y las degradaciones en las dependencias relacionadas. 
* Vínculos toohelp diagnosticar el problema de Hola.
  * Realiza un seguimiento de Profiler toohelp ver dónde se dedica tiempo de funcionamiento (vínculo de hello está disponible si se han recopilado ejemplos del seguimiento de generador de perfiles para esta operación durante el período de detección de hello). 
  * Los informes de rendimiento del Explorador de métrica, donde puede segmentar y desglosar los filtros o intervalos de tiempo de esta operación.
  * Buscar este llama tooview propiedades llamadas específicas.
  * Informes de error: si contar > 1 Esto significa que hubo errores en esta operación que puede haber contribuido tooperformance degradación.

## <a name="dependency-duration-degradation"></a>Degradación de la duración de la dependencia

Aplicación moderna más adoptar el enfoque de diseño de servicios micro, lo que en muchos casos conduce tooheavy confiabilidad en los servicios externos. Por ejemplo, si la aplicación se basa en la plataforma de algunos datos o incluso si crea su propio bot servicio se retransmitirá probablemente en algunos tooenable de proveedor de servicios cognitivos su toointeract bots de maneras más usuarios y algunos datos almacenan servicio para Hola de bot toopull respuestas de.  

Notificación de degradación de dependencia de ejemplo:

![Este es un ejemplo de detección de degradación de la duración de la dependencia](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

Observe que le indica:

* duración de Hello en comparación con toonormal tiempo de respuesta para esta operación
* El número de usuarios afectados.
* Duración media y duración de percentil 90 para esta dependencia en el día de Hola de detección de Hola y 7 días antes de
* Número de dependencia llama en día Hola de detección de Hola y 7 días antes de
* Toohelp vínculos diagnosticar el problema de Hola
  * Informes de rendimiento del Explorador de métrica de esta dependencia.
  * Llamadas de búsqueda de esta dependencia tooview propiedades de llamadas
  * Los informes de error - si recuento > 1 significa que no hubo errores dependencia llama durante la detección de Hola período que puede haber contribuido tooduration degradación. 
  * Abra Análisis con las consultas que calculan el número y la duración de esta dependencia.  

## <a name="smart-detection-of-slow-performing-patterns"></a>Detección inteligente de los patrones de rendimiento lento 

Application Insights busca los problemas de rendimiento que podrían afectar solo a algunos de sus usuarios, o bien exclusivamente a sus usuarios en algunos casos. Por ejemplo, una notificación de si las páginas de su aplicación se cargan más lentamente en un tipo de explorador que en otros, o de si las solicitudes se atienden de una forma más lenta desde un servidor determinado. También puede detectar problemas asociados con combinaciones de propiedades, como los clientes que usan un determinado sistema operativo y experimentan cargas lentas de página.  

Las anomalías como estas son muy difícil toodetect inspeccionando datos Hola, pero son más frecuentes que piense. A menudo, solo se muestran cuando se quejan los clientes. En ese momento, es demasiado tarde: usuarios Hola afectado ya están desactivando tooyour competidores.

En la actualidad, nuestra algoritmos mire tiempos de carga de página, tiempos de respuesta de solicitud en el servidor de Hola y tiempos de respuesta de dependencia.  

No tiene tooset los umbrales o configurar las reglas. Aprendizaje automático y algoritmos de minería de datos son patrones anormal de toodetect usado.

![De alerta de correo electrónico de hello, haga clic en hello vínculo tooopen Hola informe de diagnóstico de Azure](./media/app-insights-proactive-performance-diagnostics/03.png)

* **Cuando** muestra se ha detectado el problema de hello tiempo Hola.
* **Qué** describe:

  * problema de Hello detectado;
  * características Hola de hello configuran de eventos que se encuentran muestra el comportamiento de problema de Hola.
* tabla de Hello compara el conjunto de bajo rendimiento de hello con un comportamiento promedio de todos los demás eventos Hola.

Haga clic en hello vínculos tooopen métrica explorador y busque en los informes relevantes, filtrados en tiempo de Hola y propiedades de hello lenta realizar conjunto.

Modificar Hola tiempo intervalo y los filtros tooexplore Hola telemetría.

## <a name="next-steps"></a>Pasos siguientes
Estas herramientas de diagnóstico le ayudarán a inspeccionar telemetría Hola desde su aplicación:

* [Generador de perfiles](app-insights-profiler.md) 
* [Depurador de instantáneas](app-insights-snapshot-debugger.md)
* [Analytics](app-insights-analytics-tour.md)
* [Diagnóstico de análisis inteligente](app-insights-analytics-diagnostics.md)

Las detecciones inteligentes son completamente automáticas. ¿Pero quizás le gustaría tooset algunas alertas más?

* [Alertas de métricas configuradas manualmente](app-insights-alerts.md)
* [Pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md)
