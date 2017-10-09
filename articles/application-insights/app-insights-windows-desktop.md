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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="79cb1-103">Supervisión del uso y el rendimiento en las aplicaciones de escritorio de Windows</span><span class="sxs-lookup"><span data-stu-id="79cb1-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="79cb1-104">[Azure Application Insights](app-insights-overview.md) y [HockeyApp](https://hockeyapp.net) permiten supervisar el uso y rendimiento de la aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="79cb1-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79cb1-105">Se recomienda [HockeyApp](https://hockeyapp.net) toodistribute y monitor de aplicaciones de escritorio y dispositivos.</span><span class="sxs-lookup"><span data-stu-id="79cb1-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="79cb1-106">Con HockeyApp, se puede administrar la distribución, las pruebas en directo y los comentarios de los usuarios, así como supervisar los informes de uso y bloqueo.</span><span class="sxs-lookup"><span data-stu-id="79cb1-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="79cb1-107">También puede [exportar y consultar la telemetría con Analytics](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="79cb1-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="79cb1-108">Aunque puede enviar telemetría visión tooApplication desde una aplicación de escritorio, esto es principalmente útil con fines de depuración y experimental.</span><span class="sxs-lookup"><span data-stu-id="79cb1-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="79cb1-109">toosend telemetría tooApplication visión desde una aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="79cb1-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="79cb1-110">Hola [portal de Azure](https://portal.azure.com), [crear un recurso de Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="79cb1-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="79cb1-111">Para el tipo de aplicación, elija la aplicación ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="79cb1-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="79cb1-112">Realizar una copia de hello clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="79cb1-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="79cb1-113">Busque la clave de Hola Hola desplegable Essentials de nuevo recurso de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="79cb1-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="79cb1-114">En Visual Studio, edite los paquetes de NuGet Hola de su proyecto de aplicación y agregue Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="79cb1-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="79cb1-115">(O presione a Microsoft.ApplicationInsights si solo desea Hola API reconstrucción, sin los módulos de recopilación de telemetría estándar hello).</span><span class="sxs-lookup"><span data-stu-id="79cb1-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="79cb1-116">Establecer la clave de instrumentación de hello en el código:</span><span class="sxs-lookup"><span data-stu-id="79cb1-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="79cb1-117">`TelemetryConfiguration.Active.InstrumentationKey = "`*su clave*`";`</span><span class="sxs-lookup"><span data-stu-id="79cb1-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="79cb1-118">o en ApplicationInsights.config (si instaló uno de los paquetes de saludo telemetría estándar):</span><span class="sxs-lookup"><span data-stu-id="79cb1-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="79cb1-119">`<InstrumentationKey>`*su clave*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="79cb1-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="79cb1-120">Si usa ApplicationInsights.config, asegúrese de que sus propiedades en el Explorador de soluciones se establecen demasiado**acción de compilación = el contenido, copia tooOutput Directory = copia**.</span><span class="sxs-lookup"><span data-stu-id="79cb1-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="79cb1-121">[Usar la API de hello](app-insights-api-custom-events-metrics.md) toosend telemetría.</span><span class="sxs-lookup"><span data-stu-id="79cb1-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="79cb1-122">Ejecutar la aplicación y vea telemetría hello en recursos de Hola que creó en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="79cb1-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="79cb1-123"><a name="telemetry"></a>Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="79cb1-123"><a name="telemetry"></a>Example code</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="79cb1-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79cb1-124">Next steps</span></span>
* [<span data-ttu-id="79cb1-125">Creación de un panel</span><span class="sxs-lookup"><span data-stu-id="79cb1-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="79cb1-126">Búsqueda de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="79cb1-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="79cb1-127">Exploración de métricas</span><span class="sxs-lookup"><span data-stu-id="79cb1-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="79cb1-128">Escribir consultas de Analytics</span><span class="sxs-lookup"><span data-stu-id="79cb1-128">Write Analytics queries</span></span>](app-insights-analytics.md)

