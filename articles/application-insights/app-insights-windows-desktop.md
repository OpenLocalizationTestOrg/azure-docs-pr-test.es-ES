---
title: uso de aaaMonitoring y rendimiento para aplicaciones de escritorio de Windows
description: "Analice el uso y el rendimiento de la aplicación de escritorio de Windows con HockeyApp y Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Supervisión del uso y el rendimiento en las aplicaciones de escritorio de Windows


[Azure Application Insights](app-insights-overview.md) y [HockeyApp](https://hockeyapp.net) permiten supervisar el uso y rendimiento de la aplicación implementada.

> [!IMPORTANT]
> Se recomienda [HockeyApp](https://hockeyapp.net) toodistribute y monitor de aplicaciones de escritorio y dispositivos. Con HockeyApp, se puede administrar la distribución, las pruebas en directo y los comentarios de los usuarios, así como supervisar los informes de uso y bloqueo. También puede [exportar y consultar la telemetría con Analytics](app-insights-hockeyapp-bridge-app.md).
> 
> Aunque puede enviar telemetría visión tooApplication desde una aplicación de escritorio, esto es principalmente útil con fines de depuración y experimental.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>toosend telemetría tooApplication visión desde una aplicación de Windows
1. Hola [portal de Azure](https://portal.azure.com), [crear un recurso de Application Insights](app-insights-create-new-resource.md). Para el tipo de aplicación, elija la aplicación ASP.NET.
2. Realizar una copia de hello clave de instrumentación. Busque la clave de Hola Hola desplegable Essentials de nuevo recurso de Hola que acaba de crear. 
3. En Visual Studio, edite los paquetes de NuGet Hola de su proyecto de aplicación y agregue Microsoft.ApplicationInsights.WindowsServer. (O presione a Microsoft.ApplicationInsights si solo desea Hola API reconstrucción, sin los módulos de recopilación de telemetría estándar hello).
4. Establecer la clave de instrumentación de hello en el código:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "`*su clave*`";` 
   
    o en ApplicationInsights.config (si instaló uno de los paquetes de saludo telemetría estándar):
   
    `<InstrumentationKey>`*su clave*`</InstrumentationKey>` 
   
    Si usa ApplicationInsights.config, asegúrese de que sus propiedades en el Explorador de soluciones se establecen demasiado**acción de compilación = el contenido, copia tooOutput Directory = copia**.
5. [Usar la API de hello](app-insights-api-custom-events-metrics.md) toosend telemetría.
6. Ejecutar la aplicación y vea telemetría hello en recursos de Hola que creó en hello Portal de Azure.

## <a name="telemetry"></a>Ejemplo de código
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a>Pasos siguientes
* [Creación de un panel](app-insights-dashboards.md)
* [Búsqueda de diagnóstico](app-insights-diagnostic-search.md)
* [Exploración de métricas](app-insights-metrics-explorer.md)
* [Escribir consultas de Analytics](app-insights-analytics.md)

