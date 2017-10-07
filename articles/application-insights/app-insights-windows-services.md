---
title: "roles de servidor y de trabajo de visión de aplicación para Windows aaaAzure | Documentos de Microsoft"
description: "Agregar manualmente el rendimiento, disponibilidad y uso de tooanalyze para la aplicación de ASP.NET de hello Application Insights SDK tooyour."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Configuración manual de Application Insights para aplicaciones .NET

Puede configurar [Application Insights](app-insights-overview.md) toomonitor una amplia variedad de aplicaciones o roles de aplicación, componentes o microservicios. Para servicios y aplicaciones web, Visual Studio ofrece una [configuración de un solo paso](app-insights-asp-net.md). Para otros tipos de aplicación. NET, como roles de servidor back-end o aplicaciones de escritorio, puede configurar Application Insights manualmente.

![Gráficos de supervisión de rendimiento de ejemplo](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Antes de comenzar

Necesita:

* Una suscripción demasiado[Microsoft Azure](http://azure.com). Si su equipo u organización tiene una suscripción de Azure, propietario de hello puede agregar tooit, con su [cuenta de Microsoft](http://live.com).
* Visual Studio 2013 o posterior.

## <a name="add"></a>1. Selección de un recurso en Application Insights

Hola 'recurso' es donde los datos se recopilan y se muestran en hello portal de Azure. Si necesita toodecide toocreate uno nuevo, o compartir una existente.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Parte de una aplicación de mayor tamaño: usar un recurso existente

Si la aplicación web tiene varios componentes: por ejemplo, una aplicación web front-end y uno o más servicios back-end -, debe enviar telemetría desde todos los toohello de componentes de hello mismo recurso. Esto habilitará ellos toobe que se muestra en una sola asignación de aplicación y que sea posible tootrace una solicitud de un componente tooanother.

Por lo tanto, si ya se están supervisando otros componentes de esta aplicación, a continuación, solo tienes que usar Hola mismo recurso.

Abrir el recurso de Hola Hola [portal de Azure](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Aplicación independiente: crear un recurso

Si Hola nueva aplicación es tooother relacionado con las aplicaciones, debe tener su propio recurso.

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/)y crear un nuevo recurso de Application Insights. Elija ASP.NET como tipo de aplicación Hola.

![Haga clic en Nuevo, Application Insights.](./media/app-insights-windows-services/01-new-asp.png)

elección de Hello del tipo de aplicación establece contenido predeterminado de Hola de módulos de recursos de Hola.

## <a name="2-copy-hello-instrumentation-key"></a>2. Copiar Hola clave de instrumentación
clave de Hello identifica recursos de Hola. Se va a instalar pronto en hello SDK, en orden toodirect datos toohello de recursos.

![Haga clic en Propiedades, seleccione la clave de hello y presione ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Instalar el paquete de Application Insights de hello en la aplicación
Instalar y configurar Hola Application Insights paquete varía según la plataforma de Hola que está trabajando. 

1. En Visual Studio, haga clic con el botón derecho en el proyecto y elija **Administrar paquetes NuGet**.
   
    ![Haga clic en proyecto de Hola y seleccione Administrar paquetes de Nuget](./media/app-insights-windows-services/03-nuget.png)
2. Instalar el paquete de Application Insights de Hola para las aplicaciones de Windows server, "Microsoft.ApplicationInsights.WindowsServer."
   
    ![Busque "Application Insights"](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *¿Qué versión?*

    Comprobar **incluir versión preliminar** si desea tootry nuestras características más recientes. documentos relevantes de Hola o blogs tenga en cuenta si necesita una versión preliminar.
    
    *¿Puedo usar otros paquetes?*
   
    Sí. Elija "A Microsoft.ApplicationInsights" Si sólo desea toouse Hola API toosend su propio telemetría. paquete de Windows Server de Hello incluye Hola API junto con un número de otros paquetes como recopilación del contador de rendimiento y supervisión de las dependencias. 

### <a name="tooupgrade-toofuture-package-versions"></a>versiones del paquete tooupgrade toofuture
Se lanzará una nueva versión de hello SDK de tootime de tiempo.

tooupgrade tooa [nueva versión del paquete de hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), vuelva a abrir el Administrador de paquetes de NuGet y filtrar los paquetes instalados. Seleccione **Microsoft.ApplicationInsights.WindowsServer** y elija **Actualizar**.

Si ha realizado cualquier tooApplicationInsights.config personalizaciones, guarde una copia del mismo antes de actualizar y después combinar los cambios en la nueva versión de hello.

## <a name="4-send-telemetry"></a>4. Envío de datos de telemetría
**Si instala únicamente el paquete de hello API:**

* Establezca la clave de instrumentación de hello en el código, por ejemplo en `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "`*su clave*`";` 
* [Escribir su propio telemetría mediante API de hello](app-insights-api-custom-events-metrics.md#ikey).

**Si ha instalado otros paquetes de Application Insights,** puede usar si lo prefiere, clave de instrumentación de hello .config archivo tooset hello:

* Editar ApplicationInsights.config (que se agregó de forma Hola instalar NuGet). Inserte este justo antes de la etiqueta de cierre de hello:
  
    `<InstrumentationKey>`*clave de instrumentación de hello copió*`</InstrumentationKey>`
* Asegúrese de que las propiedades de Hola de ApplicationInsights.config en el Explorador de soluciones se establecen demasiado**acción de compilación = el contenido, copia tooOutput Directory = copia**.

Resulta útil tooset clave de instrumentación de hello en el código si desea demasiado[conmutador Hola clave para diferentes configuraciones de compilación](app-insights-separate-resources.md). Si se establece la clave de hello en el código, no tiene tooset en hello `.config` archivo.

## <a name="run"></a> Ejecución del proyecto
Hola de uso **F5** toorun la aplicación y pruébela: abrir diferentes páginas toogenerate algunos telemetría.

En Visual Studio, verá un recuento de eventos de Hola que se han enviado.

![Recuento de eventos en Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Visualización de los datos de telemetría
Devolver toohello [portal de Azure](https://portal.azure.com/) y busque el recurso de Application Insights tooyour.

Buscar datos en los gráficos de información general de Hola. Al principio, solo aparecerán uno o dos puntos. Por ejemplo:

![Desplazarse por los datos de toomore](./media/app-insights-windows-services/12-first-perf.png)

Haga clic en a través de cualquier toosee gráfico métricas más detalladas. [Más información acerca de las métricas](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>¿No hay datos?
* Utilizar la aplicación de hello, abrir varias páginas para que genere algunos telemetría.
* Abra hello [búsqueda](app-insights-diagnostic-search.md) icono toosee los eventos individuales. A veces tiene eventos tooget un poco más de tiempo ya a través de la canalización de métricas de Hola.
* Espere unos segundos y haga clic en **Actualizar**. Gráficos propios actualización periódicamente, pero sí puede actualizar manualmente si está esperando para algunos datos tooshow.
* Vea [Solución de problemas](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Publicación de la aplicación
Ahora la implementación del servidor de tooyour de aplicación o se acumulan datos hello tooAzure e inspección.

![Usar la aplicación de Visual Studio toopublish](./media/app-insights-windows-services/15-publish.png)

Cuando se ejecuta en modo de depuración, se agiliza la telemetría a través de la canalización de hello, por lo que debería ver los datos que aparecen en segundos. Al implementar la aplicación en la configuración de lanzamiento, los datos se acumulan más lentamente.

### <a name="no-data-after-you-publish-tooyour-server"></a>¿Después de publicar el servidor de tooyour de ningún dato?
Abra los puertos para el tráfico de salida en el firewall del servidor. Vea [esta página](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) para lista de Hola de direcciones necesarias 

### <a name="trouble-on-your-build-server"></a>¿Tiene problemas el servidor de compilación?
Consulte [este apartado de la solución de problemas](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Si la aplicación genera una gran cantidad de telemetría, módulo de muestreo adaptativo de Hola reducirá automáticamente volumen Hola que se envía toohello portal enviando sólo una fracción representativa de eventos. Sin embargo, eventos que están relacionado toohello misma solicitud se selecciona o anula la selección como un grupo, por lo que puede desplazarse entre los eventos relacionados. 
> [Más información sobre el muestreo](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Pasos siguientes
* [Agregar más telemetría](app-insights-asp-net-more.md) tooget Hola vista de 360 grados completa de la aplicación.

