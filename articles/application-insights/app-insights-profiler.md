---
title: aplicaciones web en directo de aaaProfiling en Azure con Application Insights | Documentos de Microsoft
description: "Identificar la ruta de acceso activa hello en el código de servidor web con un generador de perfiles de baja."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Introducción a la supervisión de aplicaciones web de Azure con Application Insights

*Esta característica de Application Insights está en GA para App Services y en versión preliminar para Compute.*

Averiguar cuánto tiempo se invierte en cada método de la aplicación web en directo mediante el uso de hello herramienta de generación de perfiles de [Azure Application Insights](app-insights-overview.md). Muestra perfiles detallados de solicitudes en vivo que han sido atendidas por la aplicación y resalta hello 'ruta de acceso activa' que está usando Hola mayor parte del tiempo. Selecciona automáticamente ejemplos con distintos tiempos de respuesta. Generador de perfiles de Hello usa la sobrecarga de toominimize de diversas técnicas.

Hello profiler actualmente funciona para ASP.NET web aplicaciones que se ejecutan en los servicios de aplicación de Azure, en al menos Hola Basic nivel de precios. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Habilitar el generador de perfiles de Hola

Instale [Application Insights](app-insights-asp-net.md) en el código. Si ya está instalado, asegúrese de que tiene la versión más reciente de Hola. (toodo, haga clic en el proyecto en el Explorador de soluciones y elija Administrar paquetes NuGet. Seleccione Actualizaciones y actualice todos los paquetes). Vuelva a implementar la aplicación.

*¿Usa ASP.NET Core? [Haga clic aquí](#aspnetcore).*

En [https://portal.azure.com](https://portal.azure.com), abra el recurso de Application Insights de hello para la aplicación web. Abra **Rendimiento** y haga clic en **Habilitar Application Insights Profiler**.

![Haga clic en el banner de hello enable generador de perfiles][enable-profiler-banner]

O bien, siempre puede pulsar **configurar** tooview estado, habilitar o deshabilitar Hola generador de perfiles.

![En la hoja de rendimiento de hello, haga clic en configurar][performance-blade]

Las aplicaciones web que se configuran con Application Insights se muestran en la Configurar. Siga el agente de Profiler de Hola de instrucciones tooinstall si es necesario. Si no hay ninguna aplicación web configurada con Application Insights aún, haga clic en *Agregar aplicaciones vinculadas*.

Hola de uso *habilitar el generador de perfiles* o *deshabilitar el generador de perfiles* botones en hello configurar hoja toocontrol Hola generador de perfiles en todas las aplicaciones web vinculado.



![Hoja Configurar][linked app services]

profiler hello toostop o reinicio de una instancia de servicio de aplicaciones individual, le resultará **Hola recursos de servicio de aplicaciones**, en **trabajos Web**. toodelete lo, busque **extensiones**.

![Deshabilitación de Profiler para los trabajos web][disable-profiler-webjob]

Recomendamos que posea Hola Profiler habilitado en todos los toodiscover de aplicaciones web cualquier rendimiento emite tan pronto como sea posible.

Si utiliza la aplicación web de WebDeploy toodeploy cambios tooyour, asegúrese de que excluir hello **App_Data** carpeta se eliminen durante la implementación. En caso contrario, hello la extensión del generador de perfiles se eliminarán archivos próxima vez que implemente tooAzure de aplicación web de Hola.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Uso de Profiler con máquinas virtuales de Azure y recursos de Compute (versión preliminar)

Cuando se [habilita Application Insights para Azure App Service en tiempo de ejecución](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler está disponible automáticamente (Si está habilitado Application Insights para el recurso de hello, tendrá que tooupdate toohello va versión a través de hello **configurar** asistente.)

Hay un [versión de vista previa de hello generador de perfiles para los recursos de proceso de Azure](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>límites

retención de datos de Hello predeterminado es 5 días. La ingesta máxima por día es de 10 GB.

No hay ningún cargo de servicio del generador de perfiles de Hola. Se debe hospedar la aplicación web en al menos Hola nivel básico de servicios de aplicaciones.

## <a name="viewing-profiler-data"></a>Visualización de datos del generador de perfiles

Abra la hoja de rendimiento de Hola y desplácese hacia abajo en la lista de operaciones de toohello.




![Columna de ejemplos de la hoja Rendimiento de Application Insights][performance-blade-examples]

Hola columnas en tabla de hello son:

* **Recuento de** -Hola número de estas solicitudes de intervalo de tiempo de Hola de hoja de Hola.
* **Mediana** -Hola típico tarda la aplicación toorespond tooa solicitud. La mitas de todas las respuestas fueron más rápidas.
* **95.° percentil** el 95 % de las respuestas fueron más rápidas. Si esta cifra es muy diferente de mediana de hello, puede haber un problema intermitente con la aplicación. (También es posible que se explique por una característica de diseño, como el almacenamiento en caché).
* **Ejemplos** -un icono indica que ese generador de perfiles de hello ha capturado los seguimientos de pila para esta operación.

Haga clic en Explorador de seguimiento de hello ejemplos icono tooopen Hola. Hola explorador muestra varios ejemplos que Hola generador de perfiles ha capturado, clasificados por tiempo de respuesta.

Seleccione un tooshow muestra un desglose de nivel de código de tiempo había invertido en solicitud Hola que se ejecuta.

![Explorador de seguimiento de Application Insights][trace-explorer]

**Mostrar la ruta de acceso activa** abre Hola mayor nodo de hoja, o al menos un cierre. En la mayoría de los casos, este nodo será un cuello de botella de rendimiento de tooa adyacentes.



* **Etiqueta**: nombre de Hola de función hello o evento. árbol de Hello muestra una combinación de código y eventos que se produjeron (por ejemplo, eventos SQL y http). evento superior Hola representa Hola general duración de la solicitud.
* **Transcurrido**: intervalo de tiempo de hello entre el inicio de Hola de operación de Hola y de finalización de Hola.
* **Cuando**: se muestra cuando se estaba ejecutando Hola/eventos de funciones en las funciones de tooother de relación.

## <a name="how-tooread-performance-data"></a>¿Cómo tooread los datos de rendimiento

Generador de perfiles de servicio de Microsoft usa una combinación de rendimiento de hello tooanalyze método e instrumentación de la aplicación de muestreo.
Cuando la colección detallada está en curso, ejemplos de generador de perfiles de servicio Hola puntero de instrucción de cada una de las CPU de la máquina de hello en cada milisegundo.
Cada ejemplo captura la pila de llamadas completa de hello del subproceso de hello ejecutando actualmente, lo que proporciona información detallada y útil acerca de qué que subproceso estaba haciendo en ambos altos y bajos niveles de abstracción. Generador de perfiles de servicio también recopila eventos como eventos de cambio de contexto, eventos TPL y correlación de actividad de grupo de subprocesos eventos tootrack y causalidad.

pila de llamadas de Hola se muestra en la vista de escala de tiempo de hello es resultado de hello de Hola por encima de muestreo y la instrumentación. Dado que cada ejemplo captura la pila de llamadas completa de hello del subproceso de hello, incluye código de hello .NET framework, así como otros marcos de trabajo que hacen referencia.

### <a id="jitnewobj"></a>Asignación de objetos (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1` son funciones auxiliares dentro de .NET Framework que asignan memoria del montón administrado. `clr!JIT\_New` se invoca cuando se asigna un objeto. `clr!JIT\_Newarr1` se invoca cuando se asigna una matriz de objetos. Estas dos funciones suelen ser muy rápidas y deben tardar una cantidad relativamente pequeña de tiempo. Si ve `clr!JIT\_New` o `clr!JIT\_Newarr1` tardar una cantidad considerable de tiempo en la escala de tiempo, es una indicación de que el código de hello se puede asignar muchos objetos y consumir gran cantidad de memoria.

### <a id="theprestub"></a>Carga de código (`clr!ThePreStub`)
`clr!ThePreStub`es una función auxiliar dentro de .NET framework que prepara Hola código tooexecute para hello primera vez. Suele incluir, pero sin limitarse a ello, compilación JIT (Just-In-Time). Para cada método de C#, `clr!ThePreStub` debe invocarse al menos una vez durante la duración de Hola de un proceso.

Si ve `clr!ThePreStub` lleva cantidad considerable de tiempo para una solicitud, indica que la solicitud es Hola primera de ellas que se ejecuta ese método y la hora de Hola para tooload de tiempo de ejecución de .NET framework que el método es significativo. Puede considerar un proceso de preparación que se ejecute esa parte del código de hello antes de que los usuarios obtener acceso a él, o puede ejecutar NGen en los ensamblados.

### <a id="lockcontention"></a>Contención de bloqueo (`clr!JITutil\_MonContention` o `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`o `clr!JITutil\_MonEnterWorker` indicar Hola actual subproceso espera un toobe bloqueo liberado. Suele presentarse cuando se ejecuta una instrucción de bloqueo de C#, se invoca el método Monitor.Enter o se invoca un método con el atributo MethodImplOptions.Synchronized. Contención de bloqueo se produce normalmente cuando un subproceso adquiere un bloqueo, y el subproceso B intenta hello tooacquire mismo bloquear antes de que un subproceso lo libera.

### <a id="ngencold"></a>Carga de código (`[COLD]`)
Si contiene el nombre del método hello `[COLD]`, como `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, significa que en tiempo de ejecución de hello .NET framework se está ejecutando código no optimizado por <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">optimización guiada por perfiles</a> para hello primera vez. Para cada método, debería aparecer como máximo una vez durante la duración de Hola de proceso de Hola.

Si la carga de código tiene gran cantidad de tiempo para una solicitud, indica que la solicitud es Hola primera tooexecute un hello no optimizada parte del método hello. También puede considerar calentamiento en un proceso que ejecuta esa parte del código de hello antes de que los usuarios obtener acceso a él.

### <a id="httpclientsend"></a>Envío de solicitud HTTP
Métodos como `HttpClient.Send` indicar código de hello está esperando un toocomplete de solicitud HTTP.

### <a id="sqlcommand"></a>Operación de base de datos
Método como SqlCommand.Execute indica que el código de hello está esperando un toocomplete de operación de base de datos.

### <a id="await"></a>En espera (`AWAIT\_TIME`)
`AWAIT\_TIME`indica el código de hello está esperando que otro toocomplete de tarea. Suele producirse con la instrucción "await"de C#. Cuando hace Hola código C# 'await', desenreda hello subprocesos y devuelve el grupo de subprocesos de control toohello y no hay ningún subproceso que está bloqueado esperando hello 'await' toofinish. Sin embargo, lógicamente Hola subprocesos que se espera hello 'bloqueado en' espera Hola operación toocomplete. La `AWAIT\_TIME` indica el tiempo de hello bloqueada esperando Hola tarea toocomplete.

### <a id="block"></a>Tiempo de bloqueo
`BLOCKED_TIME`indica el código de hello está esperando que otro toobe de recursos disponible, por ejemplo, esperando un objeto de sincronización, esperando un toobe subproceso disponible o en espera de una solicitud toofinish.

### <a id="cpu"></a>Tiempo de CPU
Hola CPU está ocupado ejecutando instrucciones de Hola.

### <a id="disk"></a>Tiempo de disco
aplicación Hello está realizando operaciones de disco.

### <a id="network"></a>Tiempo de red
aplicación Hello está realizando operaciones de red.

### <a id="when"></a>Columna Cuándo
Se trata de una visualización de cómo recopiladas para un nodo de muestras INCLUSIVAS Hola varían con el tiempo. intervalo total de saludo de solicitud de saludo se divide en 32 depósitos de tiempo y muestras inclusivas de Hola para ese nodo se acumulen en los depósitos de 32. Cada depósito se representa luego como una barra cuyo alto representa un valor escalado. Para nodos que están marcados `CPU_TIME` o `BLOCKED_TIME`, o donde hay una relación obvia de consumo de un recurso (cpu, disco, subprocesos), Hola barra representa consumiendo uno de esos recursos durante el período de Hola de tiempo de ese cubo. Con estas métricas puede conseguir más del 100 % si consume varios recursos. Por ejemplo, si por término medio usa dos CPU a lo largo de un intervalo, consigue el 200 %.


## <a id="troubleshooting"></a>Solución de problemas

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>¿Cómo se puede saber si Application Insights Profiler se está ejecutando?

Generador de perfiles de Hola se ejecuta como un trabajo web continuo en la aplicación Web. Puede abrir el recurso de aplicación Web de hello en https://portal.azure.com y comprobar el estado de "ApplicationInsightsProfiler" en la hoja de WebJobs de Hola. Si no está en ejecución, abra **registros** toofind más.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>¿Por qué no puedo encontrar los ejemplos de la pila aunque se ejecute el generador de perfiles de Hola?

Aquí tiene algunas cosas que puede comprobar.

1. Asegúrese de que el plan de App Service web es de nivel Básico o superior.
2. Asegúrese de que la Aplicación web tiene habilitado el SDK 2.2 Beta y superior de Application Insights.
3. Asegúrese de que la aplicación Web tiene la configuración de APPINSIGHTS_INSTRUMENTATIONKEY de hello con hello usa la misma clave de instrumentación con Application Insights SDK.
4. Asegúrese de que la Aplicación web se ejecuta en .Net Framework 4.6.
5. Si es una aplicación de ASP.NET Core, también compruebe [dependencias necesarias de hello](#aspnetcore).

Después de que se inicia el generador de perfiles de hello, hay un período de preparación corto al generador de perfiles de hello activamente recopila varios seguimientos de rendimiento. Después de eso, el generador de perfiles de hello recopila seguimientos de rendimiento de dos minutos en cada hora.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Yo usaba Azure Service Profiler. ¿Qué problema tooit?  

Cuando se habilita Application Insights Profiler, se deshabilita el agente Azure Service Profiler.

### <a id="double-counting"></a>Doble recuento de subprocesos paralelos

En algunos Hola casos métrica de tiempo total en el Visor de la pila de hello es mayor que la duración real de saludo de solicitud de Hola.

Esto puede suceder cuando hay dos o más subprocesos que funcionan en paralelo asociados a una solicitud. tiempo total de subprocesos de Hello, a continuación, es mayor que el tiempo transcurrido Hola. En muchos casos, puede estar esperando un subproceso Hola otro toocomplete. Hola Visor intentos toodetect esto y omite wait no interesa hello, pero genera errores en lado de Hola de transmisión demasiado elevado en lugar de omisión de lo que puede ser información crítica.  

Cuando se ve subprocesos paralelos en los seguimientos, debe toodetermine que subprocesos esperan para que pueda determinar la ruta crítica de Hola para solicitud de saludo. En la mayoría de los casos, subproceso de Hola que rápidamente pasa a un estado de espera simplemente está esperando Hola otros subprocesos. Concentrarse en Hola otros y omitir el tiempo de hello en subprocesos en espera Hola.

### <a id="issue-loading-trace-in-viewer"></a>No hay datos de generación de perfiles

1. Si los datos de hello está tratando de tooview es anterior a un par de semanas, pruebe a limitar el filtro de tiempo e inténtelo de nuevo.

2. Compruebe que no haya servidores proxy o firewall bloquea la toohttps://gateway.azureserviceprofiler.net acceso.

3. Compruebe que Hola Hola Application Insights clave de instrumentación que se usa en la aplicación es igual como Hola ha habilitado la generación de perfiles con el recurso de Application Insights. clave de Hola suele ser ApplicationInsights.config, pero también puede encontrarse en web.config o app.config.

### <a name="error-report-in-hello-profiling-viewer"></a>Informe de errores en hello Visor de generación de perfiles

Presentar una incidencia de soporte técnico desde el portal de Hola. Incluya Hola Id. de correlación del mensaje de error de Hola.

## <a name="manual-installation"></a>Instalación manual

Al configurar el generador de perfiles de hello, hello realizado las siguientes actualizaciones son la configuración de la aplicación Web toohello. Puede hacerlo manualmente si el entorno lo requiere; por ejemplo, si la aplicación se ejecuta en una instancia de Azure App Service Environment (ASE):

1. En la hoja de control de la aplicación de hello web, abra la configuración.
2. Establecer ".Net Framework versión" toov4.6.
3. Establecer tooOn "Always On".
4. Agregar configuración de la aplicación "__APPINSIGHTS_INSTRUMENTATIONKEY__" y el conjunto Hola valor toohello misma clave de instrumentación utilizando Hola SDK.
5. Abra Herramientas avanzadas.
6. Haga clic en "Ir" sitio Web de tooopen hello Kudu.
7. En el sitio Web de Kudu de hello, seleccione "Las extensiones de sitio".
8. Instale "__Application Insights__" desde la galería.
9. Reinicie la aplicación web de hello.

## <a id="aspnetcore"></a>Compatibilidad con ASP.NET Core

Aplicación de ASP.NET Core necesita tooinstall 2.1.0-beta6 de paquete de Microsoft.ApplicationInsights.AspNetCore Nuget o superior toowork con hello generador de perfiles. Ya no se admiten las versiones inferiores de hello después de 6/27/2017.

## <a name="next-steps"></a>Pasos siguientes

* [Trabajo con Application Insights en Visual Studio](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
