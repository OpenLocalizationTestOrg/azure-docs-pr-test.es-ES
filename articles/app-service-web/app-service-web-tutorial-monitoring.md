---
title: "una aplicación Web aaaMonitor | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset la supervisión en la aplicación Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>Supervisión de App Service
Este tutorial le guía a través de la supervisión de la aplicación y con problemas de toosolve de herramientas de hello integradas de la plataforma cuando se producen.

En cada sección de este documento se abarca una característica específica. Uso de características de hello juntas permite:
- Identificar problemas en la aplicación.
- Determinar cuándo se debe problema Hola con la plataforma de código o hello.
- Restringir origen Hola problema de hello en el código.
- Depuración y corregir el problema de Hola.

## <a name="before-you-begin"></a>Antes de empezar
- Necesita una aplicación Web toomonitor y siga Hola que se describen los pasos.
    - Puede crear una aplicación siguiendo los pasos de hello descritos en hello [crear una aplicación ASP.NET en Azure con la base de datos SQL](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.

- Si desea tootry out **depuración remota** de la aplicación, necesita Visual Studio.
    - Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello libre [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).
    - Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.

## <a name="metrics"></a>Paso 1: Visualización de métricas
**Las métricas** son toounderstand útil:
- Estado de la aplicación
- Rendimiento de la aplicación
- Consumo de recursos

Cuando se investiga un problema de aplicación, revisar las métricas es un buen lugar toostart. Portal de Azure tiene una forma rápida toovisually inspeccionar las métricas de saludo de la aplicación con **Monitor Azure**.

Las métricas proporcionan una vista histórica de varias agregaciones clave para la aplicación. Para cualquier aplicación hospedada en el servicio de aplicaciones, debe supervisar la aplicación Web de Hola y Hola plan de servicio de aplicaciones.

> [!NOTE]
> Un plan de servicio de aplicaciones representa colección de Hola de toohost recursos físicos que usan las aplicaciones. Todas las aplicaciones tooan servicio de aplicaciones plan recurso compartido Hola recursos asignan definido por dicha permitiéndole toosave costo al hospedar varias aplicaciones.
>
> Los planes de App Service definen lo siguiente:
> * Región: Europa del Norte, este de EE. UU., Sudeste Asiático, etc.
> * Tamaño de la instancia: pequeño, mediano, grande, etc.
> * Recuento de escala: una, dos, tres instancias, etc.
> * SKU: Gratis, Compartido, Básico, Estándar, Premium, etc.

métricas de tooreview para la aplicación Web, vaya toohello **Introducción** hoja de aplicación hello desea toomonitor. En ella, puede ver un gráfico de las métricas de la aplicación en forma de **icono Monitoring** (Supervisión). Haga clic en tooedit de mosaico de Hola y configurar qué tooview métricas y Hola toodisplay de intervalo de tiempo.

Por hoja de recursos de hello predeterminada proporciona una vista para las solicitudes de aplicación hello y errores de hello última hora.
![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Como puede ver en el ejemplo de Hola, tenemos una aplicación que se va a generar muchos **errores del servidor HTTP**. gran volumen de Hola de errores es el primer indicio de hello necesitamos tooinvestigate esta aplicación.

> [!TIP]
> Más información acerca del Monitor de Azure con hello siguientes vínculos:
> - [Introducción a Azure Monitor](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Métricas de Azure](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Métricas compatibles con Azure Monitor](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Paneles de Azure](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>Paso 2: Configuración de alertas
**Alertas** puede ser configurado tootrigger en condiciones específicas para la aplicación.

En [paso 1: visualice las métricas](#metrics), hemos visto que la aplicación hello tenía un gran número de errores.

Permite configurar una alerta tooautomatically recibir notificaciones cuando se producen errores. En este caso, se desea toosend alerta hello y enviar por correo electrónico cada vez que número Hola de errores HTTP 50 X supera un umbral determinado.

toocreate una alerta, vaya demasiado**supervisión** > **alertas** y haga clic en **[+] Agregar alerta**.

![Alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Proporcione valores de configuración de alertas de hello:
- **Recurso:** Hola toomonitor de sitio con la alerta de Hola.
- **Nombre:** nombre de la alerta, en este caso: *High HTTP 50X*.
- **Descripción:** texto sin formato que explica lo que observa esta alerta.
- **Alerta activada:** las alertas pueden mirar métricas o eventos, en este ejemplo, examinamos las métricas.
- **Métrica:** qué toomonitor métrica, en este caso: *errores del servidor HTTP*.
- **Condición:** cuando tooalert, en este caso, seleccione hello *mayor* opción.
- **Umbral:** ¿qué es toolook de valor, en este caso: *400*.
- **Período:** alertas funcionan sobre valor medio de Hola de una métrica. Los períodos de tiempo menores suspenden las alertas más sensibles. En este caso examinamos *5 minutos*.
- **Propietarios y colaboradores de correo electrónico:** en este caso: *Habilitado*.

Ahora que hello alerta se crea un correo electrónico se envía cada vez hello aplicación pasa por encima del umbral de hello configurado. También se pueden revisar las alertas activas Hola portal de Azure.

![Alertas desencadenadas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Más información acerca de las alertas de Azure con hello siguientes vínculos:
> - [¿Qué son las alertas en Microsoft Azure?](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Realización de acciones en las métricas](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Creación de alertas de métrica](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a> Paso 3: App Service Companion
**Complementario de servicio de aplicaciones** ofrece una manera cómoda de toomonitor la aplicación con una experiencia nativa en su dispositivo móvil (iOS o Android).

Use Azure App Service Companion para:
- Revisar las métricas de aplicación
- Revisar y realizar acciones sobre alertas y recomendaciones de aplicación
- Realizar la solución de problemas básicos (Examinar, iniciar, detener, reiniciar aplicación de hello)
- Obtener notificaciones push de eventos críticos.

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![App Service Companion en App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion en Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

Puede instalar complementario de servicio de aplicaciones de hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) o [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a> Paso 4: Diagnóstico y solución de problemas
**Diagnosticar y resolver problemas** le ayudará a diferenciar los problemas de la aplicación de los de la plataforma. También puede sugerir a posibles mitigaciones tooget su toohealthy atrás de la aplicación Web.

![Diagnosticar y resolver problemas](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Continuar con los pasos anteriores del formulario de ejemplo Hola, podemos ver que aplicación hello ha sido problemas de disponibilidad. En cambio, la disponibilidad de la plataforma de hello no ha movido de 100%.

Cuando aplicación hello tiene el problema y hello plataforma esté activo, es una indicación clara de que estamos trabajando con un problema de aplicación.

## <a name="logging"></a> Paso 5: Registro
Ahora que nos hemos reduce un problema de aplicación Hola errores tooan, podemos observar tooget de registros de servidor y la aplicación hello obtener más información.

El registro permite toocollect ambos **Application Diagnostics** y **diagnósticos de servidor Web** registros de la aplicación Web.

### <a name="application-diagnostics"></a>Diagnósticos de aplicaciones
Diagnósticos de la aplicación permite toocapture seguimientos generados por la aplicación hello en tiempo de ejecución.

Agregar seguimiento tooyour aplicación mejora en gran medida su capacidad toodebug y problemas de punto de anclaje.

En ASP.NET, puede registrar los seguimientos de aplicación mediante [clase System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate eventos capturados por la infraestructura de registro de hello. También puede especificar la gravedad de Hola de seguimiento de Hola para filtrar más fácil.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
registro de aplicaciones de tooenable vaya demasiado**supervisión** > **registros de diagnóstico** y habilitar registro de aplicaciones con hello alterna.

![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Registros de la aplicación pueden ser el sistema de archivos de la aplicación Web almacenado tooyour o insertan tooblob almacenamiento. Los escenarios de producción, es el almacenamiento de blobs toouse recomendada.

> [!IMPORTANT]
> La habilitación del registro tiene un impacto sobre el rendimiento de su aplicación y la utilización de recursos. En escenarios de producción, se recomiendan habilitar los registros de errores. Habilite únicamente un registro más detallado al investigar problemas.

 ### <a name="web-server-diagnostics"></a>Diagnósticos del servidor web
Los registros del servidor web se generan aunque la aplicación no se haya instrumentado. App Service puede recopilar tres tipos diferentes de registros de servidor:

- **Registro del servidor web**.
    - Obtener información sobre las transacciones HTTP mediante hello [formato de archivo de registro extendido W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Resulta útil al determinar las métricas generales de sitio como número de Hola de las solicitudes administradas o cuántas solicitudes provienen de una dirección IP específica.
- **Registro de error detallado**
    - Información de error detallada de los códigos de estado HTTP que indican un error (código de estado 400 o superior).
    - [Más información sobre el registro de errores detallado](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Seguimiento de solicitudes erróneas**.
    - Información detallada acerca de solicitudes con error, incluidos un seguimiento de los componentes de IIS de hello usa tooprocess Hola hello y solicitud de tiempo que se tarda en cada componente.
    - Registros de solicitudes con error son útiles al tratar de tooisolate cuál es la causa un error HTTP específico.
    - [Más información acerca del seguimiento de solicitudes con error](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

registro del servidor tooenable:
- vaya demasiado**supervisión** > **registros de diagnóstico**.
- Habilitar a tipos diferentes de hello de diagnósticos de servidor Web mediante Hola alterna.

![Supervisión de la aplicación](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> La habilitación del registro tiene un impacto sobre el rendimiento de su aplicación y la utilización de recursos. En escenarios de producción, se recomienda habilitar los registros de errores. Habilite únicamente un registro más detallado al investigar problemas.

### <a name="accessing-logs"></a>Acceso a los registros
El acceso a los registros almacenados en Blob Storage se realiza mediante el Explorador de Azure Storage. Se obtiene acceso a registros almacenados en el sistema de archivos de la aplicación hello Web a través de FTP en hello siguiendo las rutas de acceso:

- **Registros de la aplicación** - `%HOME%/LogFiles/Application/`.
    - Esta carpeta contiene uno o varios archivos de texto con información generada por el registro de aplicaciones.
- **Seguimiento de solicitudes con error** - `%HOME%/LogFiles/W3SVC#########/`.
    - Esta carpeta contiene un archivo XSL y uno o varios archivos XML.
- **Registros de errores detallados** - `%HOME%/LogFiles/DetailedErrors/`.
    - Esta carpeta contiene uno o varios archivos .htm con información extensa sobre los errores HTTP generados por la aplicación.
- **Registros del servidor web** - `%HOME%/LogFiles/http/RawLogs`.
    - Esta carpeta contiene uno o varios archivos de texto con formato con formato de archivo de registro extendido W3C de Hola.

## <a name="streaming"></a>Paso 6: Registros de streaming
Los registros de streaming resultan prácticos al depurar una aplicación desde que ahorra tiempo en comparación con demasiado[acceso a registros de hello](#Accessing-Logs) a través de FTP.

App Service puede transmitir **registros de la aplicación** y **registros del servidor web** a medida que se generan.

> [!TIP]
> Antes de intentar toostream registros, asegúrese de que ha habilitado la recopilación de registros como se describe en hello [registro](#logging) sección.

registros de toostream, vaya demasiado**supervisión**> **flujo de registro**. Seleccione **Registros de aplicación** o **Registros del servidor web** según la información que busque. Desde aquí, también puede pausar, reiniciar y borrar el búfer de Hola.

![Registros de transmisión](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Registros solo se generan cuando hay tráfico en la aplicación hello, también puede aumentar el nivel de detalle de Hola de registros tooget más eventos o información.

## <a name="remote"></a>Paso 7: Depuración remota
Una vez que tenga el origen de Hola que señala el pin de problemas de aplicaciones de hello, use **depuración remota** toowalk a través del código de hello.

Permite la depuración remota se adjunta una aplicación Web de depurador tooyour ejecutando en la nube de Hola. Puede establecer puntos de interrupción, manipula la memoria directamente, recorrer el código e incluso cambiar la ruta de acceso de código de hello tal como lo hace para aplicaciones que se ejecutan localmente.

tooattach Hola depurador tooyour aplicación que se ejecuta en la nube de hello:

- Con Visual Studio 2017, solución de hello abierto para la aplicación hello desea toodebug
- Establezca algunos puntos de interrupción, igual que haría con el desarrollo local.
- Abra **Cloud Explorer** (Ctr + /, Ctrl + x).
- Inicie sesión con sus credenciales de Azure según sea necesario.
- Aplicación hello de búsqueda que desee toodebug
- Seleccione **adjuntar depurador** Hola formulario **acciones** panel.

![Depuración remota](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio configura su aplicación para la depuración remota y abre una ventana del explorador que navega tooyour aplicación. Examine los puntos de interrupción de tootrigger de aplicación y recorrer el código de hello.

> [!WARNING]
> No se recomienda ejecutar el modo de depuración en producción. Si la aplicación de producción no se escala toomultiple instancias de servidor, depuración impedir que servidor de web de Hola desde responde las solicitudes de tooother. Para solucionar problemas de producción, el mejor recurso es demasiado[configurar el registro de](#logging) y [Application Insights](#insights).



## <a name="explorer"></a> Paso 8: Explorador de procesos
Cuando la aplicación se escalado toomore más de una instancia, **Explorador de procesos** puede ayudarle a identificar problemas específicos de instancia.

Use el **Explorador de procesos** para:

- Enumerar todos los procesos de hello en instancias diferentes de su plan de servicio de aplicaciones.
- Explorar en profundidad y ver identificadores de Hola y módulos asociados a cada proceso.
- Recuento de CPU de la vista, el espacio de trabajo y el subproceso en hello procesar nivel toohelp identificar procesos descontrolados
- Encontrar identificadores de archivos abiertos e incluso eliminar una instancia de proceso específica.

El explorador de procesos puede estar en **Supervisión** > **Explorador de procesos**.

![Explorador de procesos](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a> Paso 9: Application Insights
**Application Insights** proporciona funcionalidades avanzadas de supervisión y generación de perfiles de aplicaciones para su aplicación.

Use Application Insights toodetect y diagnosticar los problemas de rendimiento de la aplicación Web y las excepciones.

Puede habilitar Application Insights para su aplicación web en **Supervisión** > **Application Insights**

> [!NOTE]
> Visión de la aplicación podría solicitar tooinstall Hola Application Insights sitio extensión toostart recopilación de datos. Instalando la extensión de sitio de Hola provoca el reinicio de la aplicación.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Visión de la aplicación tiene una característica enriquecida establecido, toolearn más, seguir los vínculos de hello incluido en hello [pasos](#next) sección.

## <a name="next"></a> Pasos siguientes

 - [¿Qué es Application Insights?](..\application-insights\app-insights-overview.md)
 - [Supervisión del rendimiento de aplicaciones web de Azure con Application Insights](..\application-insights\app-insights-azure-web-apps.md)
 - [Supervisión de la disponibilidad y la capacidad de respuesta de cualquier sito web con Application Insights](..\application-insights\app-insights-monitor-web-app-availability.md)
