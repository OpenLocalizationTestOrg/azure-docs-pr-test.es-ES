---
title: "aaaApplication visión para servicios de nube de Azure | Documentos de Microsoft"
description: "Supervisión de los roles web y de trabajo de manera eficaz con Application Insights"
services: application-insights
documentationcenter: 
keywords: WAD2AI, Azure Diagnostics
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Application Insights para los Servicios en la nube de Azure
[Application Insights](https://azure.microsoft.com/services/cloud-services/)puede supervisar la disponibilidad, el rendimiento, los errores y el uso de las [aplicaciones de Azure Cloud Services][start] mediante la combinación de datos de los SDK de Application Insights con los datos de [Azure Diagnostics](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) desde Cloud Services. Con los comentarios de Hola que obtendrá acerca del rendimiento de Hola y eficacia de la aplicación Hola comodín, pueda tomar decisiones meditadas sobre la dirección de Hola de diseño de hello en cada ciclo de vida de desarrollo.

![Ejemplo](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Antes de comenzar
Necesitará:

* Una suscripción a [Microsoft Azure](http://azure.com). Inicie sesión con una cuenta Microsoft, que podría tener para Windows, XBox Live u otros servicios en la nube de Microsoft. 
* Herramientas de Microsoft Azure 2.9 o superior
* Herramientas de análisis del desarrollador 7.10 o posterior

## <a name="quick-start"></a>Inicio rápido
Hola toomonitor de forma más rápida y más fácil que su servicio en la nube con Application Insights es toochoose opción al publicar su servicio tooAzure.

![Ejemplo](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Instrumentos de esta opción de los contadores de la aplicación en tiempo de ejecución, lo que le proporciona todos los telemetría Hola necesita toomonitor solicitudes, excepciones y las dependencias en el rol web, así como el rendimiento de los roles de trabajo. Los seguimientos de diagnóstico generados por la aplicación también se envían tooApplication visión.

Si eso es todo lo que necesita, ha terminado. Los siguientes pasos son [ver las métricas de la aplicación](app-insights-metrics-explorer.md), [consultar los datos con Analytics](app-insights-analytics.md) y, quizás, configurar un [panel](app-insights-dashboards.md). Es recomendable tooset seguridad [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) y [agregar páginas de códigos tooyour web](app-insights-javascript.md) toomonitor rendimiento en el Explorador de Hola.

Sin embargo, también puede obtener más opciones:

* Enviar datos de diferentes componentes y recursos de tooseparate de configuraciones de compilación.
* Agregar telemetría personalizada desde su aplicación.

Si estas opciones son de interés tooyou, siga leyendo.

## <a name="sample-application-instrumented-with-application-insights"></a>Aplicación de ejemplo instrumentado con Application Insights
Eche un vistazo a esto [aplicación de ejemplo](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) en el que Application Insights se agrega tooa servicio en la nube con dos roles de trabajo hospedados en Azure. 

La información siguiente le indica cómo tooadapt su propio servicio de nube proyecto Hola igual.

## <a name="plan-resources-and-resource-groups"></a>Planeamiento de recursos y grupos de recursos
telemetría Hola desde la aplicación se almacena, analiza y muestra en un recurso de Azure del tipo Application Insights. 

Grupo de recursos de tooa pertenece cada recurso. Grupos de recursos se usan para administrar los costos, para conceder acceso a los miembros de tooteam, y toodeploy actualizaciones en una única transacción coordinada. Por ejemplo, podría [escribir una secuencia de comandos toodeploy](../azure-resource-manager/resource-group-template-deploy.md) un servicio de nube de Azure y sus recursos en una operación de supervisión de Application Insights.

### <a name="resources-for-components"></a>Recursos para componentes
Hola recomienda esquema es toocreate un recurso independiente para cada componente de la aplicación: es decir, cada rol web y rol de trabajo. Puede analizar por separado cada componente, pero puede crear un [panel](app-insights-dashboards.md) que reúne los gráficos clave Hola de todos los componentes de hello, para que pueda comparar y supervisarlas conjuntamente. 

Un esquema alternativo es telemetría de hello toosend de toohello de rol más de un mismo recurso, pero [agregar un elemento de telemetría de tooeach de propiedades de dimensión](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) que identifica su rol de origen. En este esquema, los gráficos de métricas como excepciones normalmente muestran una agregación de recuentos de Hola de Hola distintos roles, pero puede segmentar gráfico Hola por identificador de rol de hello cuando sea necesario. También se pueden filtrar las búsquedas por hello misma dimensión. Esta alternativa resulta un poco más fácil tooview todo en hello al mismo tiempo, pero también podría provocar confusión toosome entre los roles de Hola.

Telemetría explorador normalmente se incluye en hello mismo recurso como su rol de servidor web.

Colocar los recursos de Application Insights de Hola para distintos componentes de hello en un grupo de recursos. Esto hace fácil toomanage ellos juntos. 

### <a name="separating-development-test-and-production"></a>Separación de desarrollo, prueba y producción
Si está desarrollando eventos personalizados para la característica siguiente mientras está activa la versión anterior de hello, desea toosend Hola desarrollo telemetría tooa Application Insights de recursos independiente. Lo contrario, será difícil toofind la telemetría de prueba entre todos Hola tráfico del sitio de hello en vivo.

tooavoid esta situación, crear recursos independientes para cada configuración de compilación o 'marca' (desarrollo, prueba, producción,...) del sistema. Incluir recursos de Hola para cada configuración de compilación en un grupo de recursos independiente. 

toosend Hola telemetría toohello los recursos adecuados, puede configurar Hola Application Insights SDK para que recoge una clave de instrumentación diferentes dependiendo de la configuración de compilación de Hola. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Creación de un recurso de Application Insights para cada rol
Si ha decidido toocreate un recurso independiente para cada rol - y quizás otro conjunto para cada configuración de compilación -, resulta más fácil toocreate les todo en el portal de Application Insights Hola. (Si crea recursos mucho, también puede [automatizar el proceso de hello](app-insights-powershell.md).

1. Hola [portal de Azure][portal], cree un nuevo recurso de Application Insights. Para el tipo de aplicación, elija la aplicación ASP.NET. 

    ![Haga clic en Nuevo, Application Insights.](./media/app-insights-cloudservices/01-new.png)
2. Observe que cada recurso se identifica por una clave de instrumentación. Puede necesitarlo más adelante si desea toomanually configurar o comprobar la configuración de Hola de hello SDK.

    ![Haga clic en Propiedades, seleccione la clave de hello y presione ctrl + C](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Configuración de Diagnósticos de Azure para cada rol
Establezca esta opción toomonitor su aplicación con Application Insights. Para roles web, proporciona supervisión del rendimiento, alertas y diagnósticos, así como análisis de uso. Para otros roles, puede buscar y supervisar los diagnósticos de Azure, como reiniciar y contadores de rendimiento, llamadas tooSystem.Diagnostics.Trace. 

1. En el Explorador de soluciones de Visual Studio, en &lt;YourCloudService&gt;, Roles, abra las propiedades de Hola de cada rol.
2. En **configuración**, establezca **enviar datos de diagnóstico tooApplication visión** y seleccione Hola adecuado de los recursos de información de la aplicación que creó anteriormente.

Si ha decidido toouse un recurso de Application Insights independiente para cada configuración de compilación, seleccione Configuración de hello en primer lugar.

![En Propiedades de Hola de cada rol de Azure, configurar Application Insights](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Hola efecto insertar las claves de instrumentación de Application Insights en archivos de hello denominados `ServiceConfiguration.*.cscfg`. ([Código de ejemplo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Si desea toovary Hola nivel de información de diagnóstico enviado tooApplication visión, puede hacerlo [mediante la edición de hello `.cscfg` directamente los archivos de](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Instalar SDK de hello en cada proyecto
Esta opción agrega Hola capacidad tooadd personalizado telemetría tooany función de negocio, para obtener un análisis más cerca del proceso de la aplicación se utiliza y realiza.

En Visual Studio, configure Hola Application Insights SDK para cada proyecto de aplicación en la nube.

1. **Roles Web**: haga clic en proyecto de Hola y elija **configurar Application Insights** o **Agregar > telemetría de Application Insights**.

2. **Roles de trabajo**: 
 * Haga clic en proyecto de Hola y seleccione **administrar paquetes de Nuget**.
 * Agregue [Application Insights para servidores de Windows](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/).

    ![Busque "Application Insights"](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Configurar Hola SDK toosend datos toohello recursos de Application Insights.

    En una función de inicio adecuado, establecer clave de instrumentación de Hola de opción de configuración de hello en el archivo de .cscfg de hello:
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Realice esto para cada rol de la aplicación. Vea los ejemplos de hello:
   
   * [Rol web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Rol de trabajo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [Para páginas web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Conjunto hello ApplicationInsights.config archivo toobe siempre copia toohello directorio de salida. 
   
    (En el archivo .config de hello, verá mensajes pidiéndole tooplace Hola clave de instrumentación no existe. Sin embargo, es mejor tooset para aplicaciones de nube desde el archivo de .cscfg Hola. Esto garantiza que ese rol Hola está identificado correctamente en el portal de hello).

#### <a name="run-and-publish-hello-app"></a>Ejecutar y publicar la aplicación hello
Ejecute la aplicación e inicie sesión en Azure. Recursos de Application Insights Hola abierto que creó y podrá ver los puntos de datos individuales que aparecen en [búsqueda](app-insights-diagnostic-search.md), y los datos agregados en [métrica explorador](app-insights-metrics-explorer.md). 

Agregar más de telemetría: vea hello las siguientes secciones se - y, a continuación, publique su tooget en vivo de diagnóstico y uso de comentarios de la aplicación. 

#### <a name="no-data"></a>¿No hay datos?
* Abra hello [búsqueda] [ diagnostic] icono toosee los eventos individuales.
* Utilizar la aplicación de hello, abrir varias páginas para que genere algunos telemetría.
* Espere unos segundos y haga clic en Actualizar.
* Consulte [Solución de problemas][qna].

## <a name="view-azure-diagnostic-events"></a>Visualización de eventos de Azure Diagnostic
Donde hello toofind [diagnósticos de Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) información de Application Insights:

* Los contadores de rendimiento se muestran como métricas personalizadas. 
* Los registros de eventos de Windows se muestran como seguimientos y eventos personalizados.
* Los registros de aplicación, los registros ETW y los registros de infraestructura de diagnóstico aparecen como seguimientos.

contadores de rendimiento de toosee y recuentos de eventos, abra [Explorer métricas](app-insights-metrics-explorer.md) y agregar un nuevo gráfico:

![Datos de Diagnósticos de Azure](./media/app-insights-cloudservices/23-wad.png)

Use [búsqueda](app-insights-diagnostic-search.md) o un [consulta de análisis](app-insights-analytics-tour.md) toosearch a través de saludo diversos registros enviados por diagnósticos de Azure de seguimiento. Por ejemplo, suponga que tiene una excepción no controlada que ha provocado un rol toocrash y reciclaje. Esa información se mostrará en hello aplicación de canal de registro de eventos Windows. Puede usar búsqueda toolook en hello error de registro de eventos de Windows y realizar seguimiento de pila completo de Hola de excepción de Hola. Que le ayudará a encontrar Hola raíz causa del problema de Hola.

![Búsqueda de Diagnósticos de Azure](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Más telemetría
Hola secciones siguientes se muestra cómo tooget telemetría adicionales procedentes de distintos aspectos de la aplicación.

## <a name="track-requests-from-worker-roles"></a>Seguimiento de solicitudes de roles de trabajo
En los roles web, módulo de solicitudes de hello recopila automáticamente datos sobre las solicitudes HTTP. Vea hello [MVCWebRole de ejemplo](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) para obtener ejemplos de cómo puede invalidar el comportamiento de colecciones de hello predeterminado. 

Puede capturar Hola de rendimiento de roles de tooworker de llamadas mediante el seguimiento de ellos en hello igual que las solicitudes HTTP. En Application Insights, tipo de telemetría de solicitud de hello mide una unidad de trabajo de servidor con nombre que se puede programar y puede correctamente o producirá un error por separado. Mientras que las solicitudes HTTP se capturan automáticamente por hello SDK, puede insertar sus propios roles de tooworker de las solicitudes de tootrack de código.

Vea Hola dos ejemplo trabajo roles tooreport instrumentada solicitudes: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) y [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Excepciones
Consulte [Supervisión de excepciones en Application Insights](app-insights-asp-net-exceptions.md) para obtener información acerca de cómo puede recopilar excepciones no controladas de tipos de aplicaciones web diferentes.

rol web de ejemplo de Hola tiene controladores MVC5 y API Web 2. Hello se capturan las excepciones no controladas de hello dos con hello siguientes controladores:

* Configure [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs) [aquí](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) para los controladores MVC5
* Configure [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs) [aquí](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) para los controladores Web API 2

Para los roles de trabajo, hay dos maneras de excepciones de tootrack:

* TrackException(ex)
* Si ha agregado el paquete de NuGet de agente de escucha de seguimiento de hello Application Insights, puede usar **System.Diagnostics.Trace** toolog excepciones. [Ejemplo de código](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Contadores de rendimiento
Hola siguiendo los contadores se recopila de forma predeterminada:

    * \Process(??APP_WIN32_PROC??)\% Tiempo de procesador
    * \Memoria\Bytes disponibles
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec
    * \Process(??APP_WIN32_PROC??)\Private Bytes
    * \Process(??APP_WIN32_PROC??)\IO Data Bytes/sec
    * \Processor(_Total)\% Processor Time

Además, también se recopilan los siguientes contadores para los roles web:

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue

Puede especificar otros contadores de rendimiento de Windows o personalizados editando ApplicationInsights.config [como en este ejemplo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14).

  ![Contadores de rendimiento](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Telemetría correlacionada para roles de trabajo
Resulta una rica experiencia de diagnóstico, puede ver qué led tooa error o una solicitud de una latencia elevada. Con roles web, Hola que SDK se configura automáticamente una correlación entre la telemetría relacionada. Para los roles de trabajo, puede usar un tooset de inicializador de telemetría personalizada un atributo de contexto Operation.Id común para todos los tooachieve de telemetría de hello esto. Esto permite toosee si se produjo el problema de latencia o con errores de hello debido a dependencia tooa o su código, de un vistazo! 

Este es el procedimiento:

* Establece el identificador de la correlación de hello en un CallContext tal como se muestra [aquí](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). En este caso, estamos usando Hola Id. de solicitud como Id. de correlación de Hola
* Agregar una implementación personalizada de TelemetryInitializer, tooset hello Operation.Id toohello correlationId establecido anteriormente. Hay un ejemplo aquí: [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* Agregar a inicializador de telemetría personalizada de Hola. Puede hacerlo en el archivo ApplicationInsights.config de Hola o en el código tal como se muestra [aquí](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

Eso es todo. experiencia del portal Hola está ya dispuesta toohelp que vea telemetría todos los asociados de un vistazo:

![Telemetría correlacionada](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>Telemetría de cliente
[Agregar Hola páginas web de SDK de JavaScript tooyour] [ client] tooget basada en explorador telemetría como recuentos de vista de página, los tiempos de carga de página, las excepciones de la secuencia de comandos y toolet escribe telemetría personalizada en sus secuencias de comandos de la página.

## <a name="availability-tests"></a>Pruebas de disponibilidad
[Configurar las pruebas web] [ availability] toomake seguro de la aplicación permanece en vivo y capacidad de respuesta.

## <a name="display-everything-together"></a>Mostrar todos los elementos juntos
tooget una perspectiva general del sistema, puede hacer que las clave Hola gráficos de supervisión juntos en una [panel](app-insights-dashboards.md). Por ejemplo, puede anclar solicitud hello y recuentos de errores de cada rol. 

Si el sistema usa otros servicios de Azure, como Stream Analytics, incluya también sus gráficos de supervisión. 

Si tiene una aplicación móvil de cliente, insertar algunos eventos personalizados de toosend de código en las operaciones de clave de usuario y crear un [HockeyApp puente](app-insights-hockeyapp-bridge-app.md). Crear consultas en [análisis](app-insights-analytics.md) toodisplay Hola recuentos de eventos y anclarlos toohello panel.

## <a name="example"></a>Ejemplo
[ejemplo de Hola](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) supervisa un servicio que tiene un rol web y dos roles de trabajador.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Excepción "Método no encontrado" en la ejecución en Servicios en la nube de Azure
¿Ha realizado la compilación para .NET 4.6? 4.6 no se admite automáticamente en los roles de Servicios en la nube de Azure. [Instale 4.6 en cada rol](../cloud-services/cloud-services-dotnet-install-dotnet.md) antes de ejecutar la aplicación.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Pasos siguientes
* [Configurar diagnósticos de Azure tooApplication visión de envío](app-insights-azure-diagnostics.md)
* [Automatizar la creación de recursos de Application Insights](app-insights-powershell.md)
* [Automatizar los diagnósticos de Azure](app-insights-powershell-azure-diagnostics.md)
* [Funciones de Azure](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
