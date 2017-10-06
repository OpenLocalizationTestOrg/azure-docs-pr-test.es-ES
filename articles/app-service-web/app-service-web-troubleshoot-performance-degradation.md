---
title: "rendimiento de la aplicación web aaaSlow en el servicio de aplicaciones | Documentos de Microsoft"
description: "Este artículo lo ayuda a solucionar los problemas de rendimiento reducido en las aplicaciones web de Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "rendimiento de aplicaciones web, aplicación lenta, aplicaciones lentas"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Solucionar los problemas de rendimiento reducido de aplicaciones web en Azure App Service
Este artículo lo ayuda a solucionar los problemas de rendimiento reducido en las aplicaciones web de [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, también puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Get Support**.

## <a name="symptom"></a>Síntoma
Al examinar la aplicación web de hello, Hola páginas carga lenta y a veces, tiempo de espera.

## <a name="cause"></a>Causa
Con frecuencia este problema se debe a problemas en el nivel de la aplicación, como, por ejemplo:

* Solicitudes de redes que tardan mucho tiempo
* Consultas de código de aplicación o base de datos que no son eficaces
* Aplicaciones que hacen un uso elevado de memoria y CPU
* aplicación bloqueado debido a tooan (excepción)

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas
El procedimiento de solución de problemas se puede dividir en tres tareas distintas, en orden secuencial:

1. [Observación y supervisión del comportamiento de la aplicación](#observe)
2. [Recopilación de datos](#collect)
3. [Mitigar el problema de Hola](#mitigate)

[Azure App Service Web Apps](/services/app-service/web/) ofrece diversas opciones en cada paso.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Observación y supervisión del comportamiento de la aplicación
#### <a name="track-service-health"></a>Seguimiento del estado del servicio
Cada vez que hay una interrupción del servicio o una degradación del rendimiento, Microsoft Azure lo anuncia. Puede realizar el seguimiento del estado de saludo del servicio de hello en hello [portal de Azure](https://portal.azure.com/). Para más información, consulte [Track service health](../monitoring-and-diagnostics/insights-service-health.md) (Seguimiento del estado del servicio).

#### <a name="monitor-your-web-app"></a>Supervisión de la aplicación web
Esta opción permite toofind out si la aplicación está teniendo problemas. En la hoja de la aplicación web, haga clic en hello **solicitudes y errores** icono. Hola **métrica** hoja muestra todas las métricas de hello puede agregar.

Algunas de las métricas de Hola que podría interesarle toomonitor para su aplicación web son

* Espacio de trabajo de memoria promedio
* Tiempo medio de respuesta
* Tiempo de CPU
* Espacio de trabajo de memoria
* Solicitudes

![supervisar el rendimiento de aplicaciones web](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

Para más información, consulte:

* [Supervisión de Aplicaciones web en Servicio de aplicaciones de Azure](web-sites-monitor.md)
* [Recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>estado de extremo web
Si está ejecutando la aplicación web en hello **estándar** tarifa, aplicaciones Web le permite supervisar los dos puntos de conexión desde tres ubicaciones geográficas.

La supervisión de extremo configura pruebas web desde ubicaciones distribuidas geográficamente que prueban el tiempo de respuesta y el tiempo activo de direcciones URL web. prueba de Hola realiza una operación HTTP GET en tiempo de respuesta de hello web URL toodetermine hello y tiempo de actividad de cada ubicación. Cada ubicación configurada ejecuta una prueba cada cinco minutos.

El tiempo activo se supervisa a través de códigos de respuesta de HTTP y el tiempo de respuesta se mide en milisegundos. Se produce un error en una prueba de supervisión si Hola código de respuesta HTTP es igual o mayor que too400 o si la respuesta de hello tiene más de 30 segundos. Considera que un punto de conexión está disponible si se realizan correctamente las pruebas de supervisión de todos los Hola especificado ubicaciones.

tooset, configúrelo, consulte [supervisa las aplicaciones de servicio de aplicaciones de Azure](web-sites-monitor.md).

Consulte también [Mantenimiento de Sitios web de Azure activos y supervisión de puntos de conexión: con Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) para ver un vídeo sobre la supervisión de los puntos de conexión.

#### <a name="application-performance-monitoring-using-extensions"></a>Supervisión del rendimiento de la aplicación mediante el uso de extensiones
También puede supervisar el rendimiento de la aplicación mediante las *extensiones de sitio*.

Cada aplicación de servicio de aplicaciones web proporciona un extremo de administración extensible que permite toouse un conjunto eficaz de herramientas que se implementan como extensiones de sitio. Entre las extensiones se incluyen: 

- Editores de código fuente como [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx). 
- Herramientas de administración de recursos conectados como una base de datos de MySQL conectado tooa web app.

[Azure Application Insights](/services/application-insights/) y [New Relic](/marketplace/partners/newrelic/newrelic/) son dos de las extensiones de sitio que están disponibles de supervisión de rendimiento de Hola. toouse New Relic, instalar a un agente en tiempo de ejecución. toouse visión de la aplicación de Azure, se vuelve a generar el código con un SDK, y también puede instalar una extensión que proporciona acceso a los datos tooadditional. Hola SDK le permite escribir un uso de código toomonitor Hola y el rendimiento de la aplicación con más detalle.

toouse Application Insights, consulte [supervisar el rendimiento en aplicaciones web](../application-insights/app-insights-web-monitor-performance.md).

vea toouse New Relic, [nueva administración de rendimiento de aplicaciones de Relic en Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).

<a name="collect" />

### <a name="2-collect-data"></a>2. Recopilación de datos
entorno de las aplicaciones Web de Hello proporciona funcionalidad de diagnóstico para registrar información de servidor web de Hola y de aplicación web de hello. información de Hola se divide en diagnóstico de servidor web y application diagnostics.

#### <a name="enable-web-server-diagnostics"></a>Habilitar diagnósticos del servidor web
Puede habilitar o deshabilitar Hola siguientes tipos de registros:

* **Registro de errores detallado** : registra información detallada de errores para códigos de estado HTTP que indican un problema (código de estado 400 o superior). Esto puede contener información que puede ayudar a determinar por qué servidor de hello devolvió el código de error de Hola.
* **Error de seguimiento de solicitudes con** -información detallada sobre las solicitudes con error, incluidos un seguimiento de hello IIS componentes utilizados tooprocess Hola solicitud y la hora de hello realizada en cada componente. Esto puede resultar útil si está tratando de rendimiento de la aplicación web tooimprove o aislar la causa de un error específico de HTTP.
* **Registro del servidor Web** -obtener información acerca de las transacciones HTTP mediante el formato de archivo de registro extendido W3C de Hola. Esto es útil al determinar las métricas de aplicación general de web, como el número de Hola de las solicitudes administradas o cuántas solicitudes provienen de una dirección IP específica.

#### <a name="enable-application-diagnostics"></a>Habilitar diagnósticos de la aplicación
Hay varias opciones toocollect aplicación datos de rendimiento de aplicaciones Web, generar perfiles de la aplicación en vivo desde Visual Studio o modificar su toolog de código de aplicación más información y seguimientos. Puede elegir las opciones de hello basándose en el nivel de acceso toohello aplicación y lo que ha observado de hello herramientas de supervisión.

##### <a name="use-application-insights-profiler"></a>Uso de Application Insights Profiler
Puede habilitar Hola el generador de perfiles de aplicación visión toostart capturar seguimientos detallados de rendimiento. Puede tener acceso a los seguimientos capturados una toofive cuando necesite tooinvestigate problemas hace días ha sucedido en hello anterior. Puede elegir esta opción siempre que haya recursos de la aplicación de acceso toohello web Application Insights en el portal de Azure.

El generador de perfiles de aplicación visión proporciona estadísticas en tiempo de respuesta para cada llamada de web y los seguimientos que indica qué línea de código ha causado Hola lentitud. A veces hello aplicación de servicio de aplicaciones es lento, ya no se escribe cierto código en un rendimiento forma. Por ejemplo, código secuencial que se puede ejecutar en paralelo y contenciones de bloqueo de base de datos no deseadas. Quitar estos cuellos de botella en el código de hello aumenta el rendimiento de la aplicación hello, pero son toodetect disco duro sin configurar registros y seguimientos elaborados. seguimientos de Hello recopilados por el generador de perfiles de aplicación visión ayuda a identificar las líneas de Hola de código que ralentiza la aplicación hello y superar este desafío para las aplicaciones de servicio de aplicaciones.

 Para más información, consulte [Generación de perfiles de aplicaciones web activas de Azure con Application Insights](../application-insights/app-insights-profiler.md).

##### <a name="use-remote-profiling"></a>Uso de la generación remota de perfiles
En Azure App Service, se pueden generar perfiles de forma remota de aplicaciones web, aplicaciones de API y WebJobs. Elija esta opción si tiene recursos de aplicación web de acceso toohello y sabrá cómo tooreproduce Hola problema o si sabe exactamente Hola ocurre problema de rendimiento de Hola de intervalo de tiempo.

Generación de perfiles remota es útil si Hola el uso de CPU del proceso de hello es alto y el proceso se está ejecutando más lentamente de lo esperado, o latencia Hola de solicitudes HTTP que es mayor de lo normal, puede generar perfiles de su proceso y obtener tooanalyze de pilas de llamadas de hello CPU muestreo remotamente Hola actividad de proceso y las rutas de acceso activas de código.

Para más información, consulte [Compatibilidad con la generación remota de perfiles en Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).

##### <a name="set-up-diagnostic-traces-manually"></a>Establecimiento manual de los seguimientos de diagnóstico
Si tiene código de fuente de la aplicación web de acceso toohello, diagnósticos de la aplicación habilita la información de toocapture generado por una aplicación web. Las aplicaciones de ASP.NET pueden usar hello `System.Diagnostics.Trace` el registro de diagnósticos de aplicación de clase toolog información toohello. Sin embargo, deberá toochange Hola código y volver a implementar la aplicación. Este método es recomendable si la aplicación se ejecuta en un entorno de prueba.

Para obtener instrucciones detalladas sobre cómo la aplicación para el registro, consulte el tooconfigure [habilitar el registro de diagnósticos para aplicaciones web en el servicio de aplicaciones de Azure](web-sites-enable-diagnostic-log.md).

#### <a name="use-hello-azure-app-service-support-portal"></a>Usar el portal de soporte técnico de servicio de aplicaciones de Azure Hola
Aplicaciones Web proporciona Hola capacidad tootroubleshoot problemas relacionados tooyour web app examinando los registros, registros de eventos, los volcados de proceso HTTP y más. Puede tener acceso a toda esta información con nuestro Portal de soporte técnico en **http://&lt;Nombre de la aplicación>.scm.azurewebsites.net/Support**.

portal de soporte técnico de servicio de aplicaciones de Azure de Hello proporciona tres pestañas independientes tres pasos de un escenario de solución de problemas comunes de Hola de toosupport:

1. Observación del comportamiento actual
2. Analizar la recopilación de información de diagnóstico y ejecución Hola analizadores integrados
3. Mitigación

Si el problema de saludo se está realizando ahora mismo, haga clic en **analizar** > **diagnósticos** > **diagnosticar ahora** toocreate una sesión de diagnóstico para usted, que recopila registros de HTTP, registros del Visor de eventos, volcados de memoria, registros de errores PHP e informe de proceso PHP.

Una vez que se recopilan los datos de hello, portal de soporte técnico de Hola ejecuta un análisis de datos de Hola y proporciona un informe HTML.

En caso de que desea que toodownload Hola datos, de forma predeterminada, se almacenaría en la carpeta de D:\home\data\DaaS Hola.

Para obtener más información sobre el portal de soporte técnico de servicio de aplicaciones de Azure de hello, consulte [tooSupport nuevas actualizaciones extensión del sitio para los sitios Web de Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Usar hello Kudu consola de depuración
El servicio Web Apps incluye una consola de depuración que puede usar para depurar, explorar o cargar archivos, e incluye también puntos de conexión JSON para obtener información sobre su entorno. Esta consola se denomina hello *Kudu consola* o hello *SCM panel* de la aplicación web.

Se puede tener acceso a este panel va toohello vínculo **https://&lt;el nombre de la aplicación >.scm.azurewebsites.net/**.

Algunos de los aspectos de Hola que Kudu ofrece son:

* Configuración del entorno de la aplicación
* transmisión de registro
* Volcado de diagnóstico
* Depuración de la consola en la que puede ejecutar cmdlets de Powershell y comandos básicos de DOS.

Otra característica útil de Kudu es que, en caso de que la aplicación es producir excepciones de primera oportunidad, puede usar Kudu y volcados de memoria de hello SysInternals herramienta Procdump toocreate. Estos archivos de volcado de memoria son instantáneas de proceso de Hola y a menudo le permitirá más complicados solucionar problemas relacionados con la aplicación web.

Para obtener más información sobre las características disponibles en Kudu, consulte [Herramientas de Azure Websites Team Services que debe conocer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Mitigar el problema de Hola
#### <a name="scale-hello-web-app"></a>Aplicación web de escala hello
En el servicio de aplicación de Azure, para aumentar el rendimiento y la capacidad, puede ajustar la escala de hello en el que se ejecuta la aplicación. El escalado de una aplicación web implica dos acciones relacionadas: cambiar la tooa del plan de servicio de aplicaciones más alto nivel de precios y configurar ciertas opciones de configuración una vez que haya cambiado toohello cuanto mayor sea el nivel de precios.

Para obtener más información sobre el escalado, consulte [Escalado de una aplicación web en Azure App Service](web-sites-scale.md).

Además, puede elegir toorun su aplicación en más de una instancia. El escalado no solo le proporciona una mayor capacidad de procesamiento, sino también algo de tolerancia a errores. Si el proceso de hello deja de funcionar en una instancia, hello otras instancias continuar tooserve las solicitudes.

Puede establecer Hola escalado toobe Manual o automático.

#### <a name="use-autoheal"></a>Uso de AutoHeal
AutoHeal recicla el proceso de trabajo de hello para la aplicación en función de la configuración que elija (como los cambios de configuración, las solicitudes, límites de memoria o el tiempo de hello es necesario tooexecute una solicitud). La mayoría de casos de hello, reciclar el proceso de hello es hello toorecover de manera más rápida de un problema. Aunque siempre puede reiniciar una aplicación Hola desde web directamente en hello portal de Azure, AutoHeal lo hace automáticamente por usted. Todo lo que necesita toodo es agregar algunos de los desencadenadores en el archivo web.config de la raíz de hello para la aplicación web. Esta configuración podría funcionar en hello mismo forma incluso si la aplicación no es una aplicación. NET.

Para obtener más información, consulte [Recuperación automática de Sitios web de Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Reiniciar la aplicación web de Hola
El reinicio es a menudo hello toorecover de manera más sencilla de problemas puntuales. En hello [portal de Azure](https://portal.azure.com/), en la hoja de la aplicación web, dispone de hello opciones toostop o reiniciar la aplicación.

 ![Reinicie los problemas de rendimiento de toosolve de aplicación web](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

También puede administrar la aplicación web con Azure Powershell. Para obtener más información, vea [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).
