---
title: aaaMonitor un live ASP.NET web app con Azure Application Insights | Documentos de Microsoft
description: "Supervise el rendimiento de un sitio web sin volver a implementarlo. Funciona con las aplicaciones web de ASP.NET hospedadas en local, en las máquinas virtuales o en Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Instrumentar aplicaciones web en tiempo de ejecución con Application Insights


Puede instrumentar una aplicación web en directo con Azure Application Insights, sin necesidad de toomodify o volver a implementar el código. Si las aplicaciones se hospedan en un servidor IIS local, instale el Monitor de estado. Aplicaciones web de Azure o ejecutar en una máquina virtual de Azure, puede activar la supervisión de Application Insights hello Azure del panel de control. (También hay varios artículos sobre cómo configurar [aplicaciones web en directo de J2EE](app-insights-java-live.md) y [Azure Cloud Services](app-insights-cloudservices.md)). Necesita una suscripción a [Microsoft Azure](http://azure.com) .

![gráficos de ejemplo](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

Tiene la opción de tres rutas tooapply Application Insights tooyour .NET las aplicaciones web:

* **Tiempo de compilación:** [Hola agregar Application Insights SDK] [ greenbrown] tooyour código de la aplicación de web.
* **Tiempo de ejecución:** instrumentar la aplicación web en el servidor de hello, tal y como se describe a continuación, sin volver a generar e implementar código de hello.
* **Both:** compilar Hola SDK en el código de aplicación web y también se aplican las extensiones de tiempo de ejecución de Hola. Obtener Hola lo mejor de ambas opciones.

A continuación hay un resumen de lo que se obtiene por cada vía:

|  | Tiempo de compilación | Tiempo de ejecución |
| --- | --- | --- |
| Solicitudes y excepciones |Sí |Sí |
| [Excepciones más detalladas](app-insights-asp-net-exceptions.md) | |Sí |
| [Diagnósticos de dependencia](app-insights-asp-net-dependencies.md) |En .NET 4.6 +, pero con menos detalle |Sí, detalles completos: códigos de resultado, texto de comandos SQL, verbo HTTP|
| [Contadores de rendimiento del sistema](app-insights-performance-counters.md) |Sí |Sí |
| [API para la telemetría personalizada][api] |Sí |No |
| [Integración del registro de seguimiento](app-insights-asp-net-trace-logs.md) |Sí |No |
| [Datos de usuario y página](app-insights-javascript.md) |Sí |No |
| Necesita un código toorebuild |Sí | No |


## <a name="monitor-a-live-azure-web-app"></a>Supervisión de una aplicación web de Azure activa

Si la aplicación se ejecuta como un servicio web de Azure, aquí de cómo tooswitch acerca de cómo supervisar:

* Seleccionar Application Insights en panel de control de la aplicación hello en Azure.

    ![Configuración de Application Insights para una aplicación web de Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Cuando se abre la página de resumen de Application Insights de hello, haga clic en vínculo hello en hello inferior tooopen Hola completa Application Insights a recursos.

    ![Haga clic en a través de tooApplication visión](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Supervisión de aplicaciones de nube y VM](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Habilitar la supervisión de cliente en Azure

Si ha habilitado Application Insights en Azure, puede agregar la vista de página y la telemetría de usuario.

1. Seleccione Configuración > Configuración de la aplicación.
2.  En Configuración de la aplicación, agregue un nuevo par clave-valor: 
   
    Clave: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valor: `true`
3. **Guardar** Hola configuración y **reiniciar** la aplicación.

Hola Application Insights JavaScript SDK ahora se aplica en cada página web.

## <a name="monitor-a-live-iis-web-app"></a>Supervisión de una aplicación web de IIS activa

Si la aplicación se hospeda en un servidor IIS, habilite Application Insights con el Monitor de estado.

1. En el servidor web IIS, inicie sesión con las credenciales de administrador.
2. Si ya no está instalado el Monitor de estado de aplicación visión, descargue y ejecute hello [instalador del Monitor de estado](http://go.microsoft.com/fwlink/?LinkId=506648) (o ejecute [instalador de plataforma Web](https://www.microsoft.com/web/downloads/platform.aspx) y busque en el mismo estado de visión de la aplicación Monitor).
3. En el Monitor de estado, seleccione aplicación web de hello instalado o el sitio Web que desea toomonitor. Inicie sesión con sus credenciales de Azure.

    Configurar recursos de Hola donde desea toosee resultados de hello en el portal de Application Insights Hola. (Normalmente, es mejor toocreate un nuevo recurso. Seleccione un recurso existente si ya tiene [pruebas web][availability] o la [supervisión de cliente][client] para esta aplicación). 

    ![Elija una aplicación y un recurso.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Reinicie IIS.

    ![Elija reiniciar en parte superior de saludo del cuadro de diálogo de Hola.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    El servicio web se interrumpe durante un breve período.

## <a name="customize-monitoring-options"></a>Personalización de las opciones de supervisión

La habilitación de Application Insights agrega archivos DLL y ApplicationInsights.config tooyour web app. También puede [editar el archivo .config de hello](app-insights-configuration-with-applicationinsights-config.md) toochange algunas de las opciones de Hola.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Al volver a publicar la aplicación, vuelva a habilitar Application Insights

Antes de volver a publicar la aplicación, considere la posibilidad de [agregar código de toohello de Application Insights en Visual Studio][greenbrown]. Obtendrá más detallada telemetría y telemetría personalizada de hello capacidad toowrite.

Si desea que toore-publicar sin agregar Application Insights toohello código, tenga en cuenta que el proceso de implementación de hello puede eliminar archivos DLL de Hola y ApplicationInsights.config de hello Publicar sitio web. Por lo tanto:

1. Si edita el archivo ApplicationInsights.config, realice una copia del mismo antes de volver a publicar la aplicación.
2. Vuelva a publicar la aplicación.
3. Vuelva a habilitar la supervisión de Application Insights. (Use el método adecuado de hello: panel de control de aplicación web de Azure de Hola u Hola Monitor de estado en un host IIS.)
4. Volver a aplicar las modificaciones realizadas en el archivo .config de Hola.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Solución de problemas de configuración en tiempo de ejecución de Application Insights

### <a name="cant-connect-no-telemetry"></a>¿No se puede conectar? ¿No hay telemetría?

* Abra [Hola puertos salientes necesarios](app-insights-ip-addresses.md#outgoing-ports) en toowork de Monitor de estado de su servidor firewall tooallow.

* Abrir el Monitor de estado y seleccione la aplicación en el panel izquierdo. Compruebe si hay algún mensaje de diagnóstico para esta aplicación en la sección "Notificaciones de configuración" hello:

  ![Abra la solicitud de toosee de hoja de rendimiento de hello, tiempo de respuesta, dependencias y otros datos](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* En el servidor de hello, si ve un mensaje de "permisos insuficientes", pruebe siguiente hello:
  * En el Administrador de IIS, seleccione el grupo de aplicaciones, abra **configuración avanzada**y en **modelo de proceso** tenga en cuenta Hola identidad.
  * En el panel de control de administración de equipo, agregue este grupo de usuarios del Monitor de rendimiento de toohello de identidad.
* Si tiene instalado MMA/SCOM (Systems Center Operation Manager) en el servidor, algunas versiones pueden entrar en conflicto. Desinstalar SCOM y Monitor de estado y volver a instalar versiones más recientes de Hola.
* Consulte [Solución de problemas][qna].

## <a name="system-requirements"></a>Requisitos del sistema
Compatibilidad de sistema operativo para el Monitor de estado de Application Insights en servidor:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

con el último Service Pack y .NET Framework 4.5

En el lado del cliente de hello: Windows 7, 8, 8.1 y 10, con .NET Framework 4.5

La compatibilidad de IIS es: IIS 7, 7.5, 8 y 8.5 (se requiere IIS)

## <a name="automation-with-powershell"></a>Automatización con PowerShell
Puede iniciar y detener la supervisión mediante PowerShell en el servidor IIS.

Importar módulo de Application Insights de hello en primer lugar:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Encuentre las aplicaciones en supervisión:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`Nombre de hello (opcional) de una aplicación web.
* Muestra Hola estado de supervisión de Application Insights para cada aplicación web (u Hola con el nombre de aplicación) en este servidor IIS.
* Devuelve `ApplicationInsightsApplication` para cada aplicación:

  * `SdkState==EnabledAfterDeployment`: La aplicación se está supervisando y se ha instrumentado en tiempo de ejecución mediante la herramienta Monitor de estado de hello, o por `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: no se ha instrumentado aplicación hello para Application Insights. Nunca se ha instrumentado o se deshabilitó la supervisión de tiempo de ejecución con la herramienta Monitor de estado de Hola o con `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: se ha instrumentado aplicación hello mediante la adición de código fuente de hello SDK toohello. El SDK no se puede actualizar ni detener.
  * `SdkVersion`Muestra la versión de Hola en uso para la supervisión de esta aplicación.
  * `LatestAvailableSdkVersion`Muestra la versión de Hola actualmente disponible en la Galería de NuGet Hola. versión de toothis aplicación tooupgrade hello, use `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`nombre de saludo de la aplicación hello en IIS
* `-InstrumentationKey`Hola ikey de hello donde desea hello toobe de resultados muestra el recurso de Application Insights.
* Este cmdlet solo afecta a las aplicaciones que no se han instrumentado, es decir, aquellas cuyo SdkState == NotInstrumented.

    Hola cmdlet no afecta a una aplicación que ya se ha instrumentado. No importa si se ha instrumentado aplicación hello en tiempo de compilación mediante la adición de código de hello SDK toohello o en tiempo de ejecución por un uso anterior de este cmdlet.

    Hola SDK versión utilizada tooinstrument Hola aplicación es server toothis de descarga de la versión de Hola último.

    versión más reciente de toodownload hello, use Update-ApplicationInsightsVersion.
* Si se descarga correctamente, devuelve `ApplicationInsightsApplication` . Si se produce un error, registra un toostderr de seguimiento.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`nombre de Hola de una aplicación en IIS
* `-All` Detiene la supervisión de todas las aplicaciones en este servidor IIS con `SdkState==EnabledAfterDeployment`
* Detiene la supervisión de hello aplicaciones especificadas y quita la instrumentación. Solo funciona para las aplicaciones que se han instrumentado en tiempo de ejecución mediante Hola herramienta de supervisión de estado o ApplicationInsightsApplication de inicio. (`SdkState==EnabledAfterDeployment`)
* Devuelve ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: nombre de Hola de una aplicación web en IIS.
* `-InstrumentationKey` (Opcional). Use que este toochange Hola recursos toowhich Hola telemetría de la aplicación se envía.
* Este cmdlet:
  * Hola de actualizaciones con el nombre de versión de toohello la aplicación de hello SDK descargada más recientemente toothis máquina. (Solo funciona si `SdkState==EnabledAfterDeployment`)
  * Si proporciona una clave de instrumentación, Hola con el nombre de aplicación es toosend ha vuelto a configurar telemetría toohello recursos con esa clave. (Funciona si `SdkState != Disabled`)

`Update-ApplicationInsightsVersion`

* Descarga el servidor de toohello de Application Insights SDK más reciente de Hola.

## <a name="questions"></a>Preguntas acerca del Monitor de estado

### <a name="what-is-status-monitor"></a>¿Qué es el Monitor de estado?

Una aplicación de escritorio que se instala en el servidor web de IIS. Le ayuda a instrumentar y configurar aplicaciones web. 

### <a name="when-do-i-use-status-monitor"></a>¿Cuándo puedo usar el Monitor de estado?

* tooinstrument cualquier aplicación que se ejecuta en el servidor IIS - de web incluso si ya se está ejecutando.
* tooenable telemetría adicionales para las aplicaciones web que se han [compiladas con hello Application Insights SDK](app-insights-asp-net.md) en tiempo de compilación. 

### <a name="can-i-close-it-after-it-runs"></a>¿Puedo cerrarlo después de ejecutarlo?

Sí. Una vez se ha instrumentado sitios Web de Hola que seleccione, puede cerrarlo.

No recopila telemetría por sí mismo. Simplemente configura las aplicaciones web hello y establece algunos permisos.

### <a name="what-does-status-monitor-do"></a>¿Qué hace el Monitor de estado?

Al seleccionar una aplicación web para tooinstrument de Monitor de estado:

* Descarga y coloca ensamblados de Application Insights de Hola y el archivo .config en carpeta de archivos binarios de la aplicación hello web.
* Modifica `web.config` módulo de seguimiento de información de aplicaciones HTTP tooadd Hola.
* Permite llamadas de dependencia toocollect de generación de perfiles de CLR.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>¿Es necesario toorun Monitor de estado cada vez que actualice la aplicación hello?

No si reimplementa de forma incremental. 

Si seleccionó la opción de 'eliminar los archivos existentes' de Hola Hola proceso de publicación, necesitaría toore y ejecutar el Monitor de estado tooconfigure Application Insights.

### <a name="what-telemetry-is-collected"></a>¿Qué telemetría se recopila?

En el caso de las aplicaciones que instrumenta solo en tiempo de ejecución mediante el Monitor de estado:

* Solicitudes HTTP
* Llamadas toodependencies
* Excepciones
* Contadores de rendimiento

En el caso de las aplicaciones ya instrumentadas en el momento de la compilación:

 * Contadores de proceso.
 * Llamadas de dependencia (.NET 4.5); valores devueltos en las llamadas de dependencia (.NET 4.6).
 * Valores de seguimiento de la pila de excepción.

[Más información](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Pasos siguientes

Vea la telemetría:

* [Explorar las métricas](app-insights-metrics-explorer.md) toomonitor rendimiento y uso
* [Buscar eventos y registros] [ diagnostic] toodiagnose problemas
* [Análisis](app-insights-analytics.md) para más consultas avanzadas
* [Creación de paneles](app-insights-dashboards.md)

Agregue más telemetría:

* [Crear pruebas web] [ availability] toomake seguro el sitio permanece activo.
* [Agregar telemetría de cliente web] [ usage] toosee excepciones de código de la página web y toolet insertar seguimiento de llamadas.
* [Agregar código de aplicación visión SDK tooyour] [ greenbrown] para que pueda insertar seguimiento y registrar las llamadas

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
