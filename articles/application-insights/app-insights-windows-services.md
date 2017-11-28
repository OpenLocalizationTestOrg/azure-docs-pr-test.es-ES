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
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="25c0b-103">Configuración manual de Application Insights para aplicaciones .NET</span><span class="sxs-lookup"><span data-stu-id="25c0b-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="25c0b-104">Puede configurar [Application Insights](app-insights-overview.md) toomonitor una amplia variedad de aplicaciones o roles de aplicación, componentes o microservicios.</span><span class="sxs-lookup"><span data-stu-id="25c0b-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="25c0b-105">Para servicios y aplicaciones web, Visual Studio ofrece una [configuración de un solo paso](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="25c0b-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="25c0b-106">Para otros tipos de aplicación. NET, como roles de servidor back-end o aplicaciones de escritorio, puede configurar Application Insights manualmente.</span><span class="sxs-lookup"><span data-stu-id="25c0b-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Gráficos de supervisión de rendimiento de ejemplo](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="25c0b-108">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="25c0b-108">Before you start</span></span>

<span data-ttu-id="25c0b-109">Necesita:</span><span class="sxs-lookup"><span data-stu-id="25c0b-109">You need:</span></span>

* <span data-ttu-id="25c0b-110">Una suscripción demasiado[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="25c0b-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="25c0b-111">Si su equipo u organización tiene una suscripción de Azure, propietario de hello puede agregar tooit, con su [cuenta de Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="25c0b-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="25c0b-112">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="25c0b-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="25c0b-113"><a name="add"></a>1. Selección de un recurso en Application Insights</span><span class="sxs-lookup"><span data-stu-id="25c0b-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="25c0b-114">Hola 'recurso' es donde los datos se recopilan y se muestran en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="25c0b-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="25c0b-115">Si necesita toodecide toocreate uno nuevo, o compartir una existente.</span><span class="sxs-lookup"><span data-stu-id="25c0b-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="25c0b-116">Parte de una aplicación de mayor tamaño: usar un recurso existente</span><span class="sxs-lookup"><span data-stu-id="25c0b-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="25c0b-117">Si la aplicación web tiene varios componentes: por ejemplo, una aplicación web front-end y uno o más servicios back-end -, debe enviar telemetría desde todos los toohello de componentes de hello mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="25c0b-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="25c0b-118">Esto habilitará ellos toobe que se muestra en una sola asignación de aplicación y que sea posible tootrace una solicitud de un componente tooanother.</span><span class="sxs-lookup"><span data-stu-id="25c0b-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="25c0b-119">Por lo tanto, si ya se están supervisando otros componentes de esta aplicación, a continuación, solo tienes que usar Hola mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="25c0b-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="25c0b-120">Abrir el recurso de Hola Hola [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="25c0b-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="25c0b-121">Aplicación independiente: crear un recurso</span><span class="sxs-lookup"><span data-stu-id="25c0b-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="25c0b-122">Si Hola nueva aplicación es tooother relacionado con las aplicaciones, debe tener su propio recurso.</span><span class="sxs-lookup"><span data-stu-id="25c0b-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="25c0b-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/)y crear un nuevo recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="25c0b-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="25c0b-124">Elija ASP.NET como tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="25c0b-124">Choose ASP.NET as hello application type.</span></span>

![Haga clic en Nuevo, Application Insights.](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="25c0b-126">elección de Hello del tipo de aplicación establece contenido predeterminado de Hola de módulos de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="25c0b-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="25c0b-127">2. Copiar Hola clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="25c0b-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="25c0b-128">clave de Hello identifica recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="25c0b-128">hello key identifies hello resource.</span></span> <span data-ttu-id="25c0b-129">Se va a instalar pronto en hello SDK, en orden toodirect datos toohello de recursos.</span><span class="sxs-lookup"><span data-stu-id="25c0b-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Haga clic en Propiedades, seleccione la clave de hello y presione ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="25c0b-131"><a name="sdk"></a>3. Instalar el paquete de Application Insights de hello en la aplicación</span><span class="sxs-lookup"><span data-stu-id="25c0b-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="25c0b-132">Instalar y configurar Hola Application Insights paquete varía según la plataforma de Hola que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="25c0b-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="25c0b-133">En Visual Studio, haga clic con el botón derecho en el proyecto y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="25c0b-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Haga clic en proyecto de Hola y seleccione Administrar paquetes de Nuget](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="25c0b-135">Instalar el paquete de Application Insights de Hola para las aplicaciones de Windows server, "Microsoft.ApplicationInsights.WindowsServer."</span><span class="sxs-lookup"><span data-stu-id="25c0b-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Busque "Application Insights"](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="25c0b-137">*¿Qué versión?*</span><span class="sxs-lookup"><span data-stu-id="25c0b-137">*Which version?*</span></span>

    <span data-ttu-id="25c0b-138">Comprobar **incluir versión preliminar** si desea tootry nuestras características más recientes.</span><span class="sxs-lookup"><span data-stu-id="25c0b-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="25c0b-139">documentos relevantes de Hola o blogs tenga en cuenta si necesita una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="25c0b-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="25c0b-140">*¿Puedo usar otros paquetes?*</span><span class="sxs-lookup"><span data-stu-id="25c0b-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="25c0b-141">Sí.</span><span class="sxs-lookup"><span data-stu-id="25c0b-141">Yes.</span></span> <span data-ttu-id="25c0b-142">Elija "A Microsoft.ApplicationInsights" Si sólo desea toouse Hola API toosend su propio telemetría.</span><span class="sxs-lookup"><span data-stu-id="25c0b-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="25c0b-143">paquete de Windows Server de Hello incluye Hola API junto con un número de otros paquetes como recopilación del contador de rendimiento y supervisión de las dependencias.</span><span class="sxs-lookup"><span data-stu-id="25c0b-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="25c0b-144">versiones del paquete tooupgrade toofuture</span><span class="sxs-lookup"><span data-stu-id="25c0b-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="25c0b-145">Se lanzará una nueva versión de hello SDK de tootime de tiempo.</span><span class="sxs-lookup"><span data-stu-id="25c0b-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="25c0b-146">tooupgrade tooa [nueva versión del paquete de hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), vuelva a abrir el Administrador de paquetes de NuGet y filtrar los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="25c0b-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="25c0b-147">Seleccione **Microsoft.ApplicationInsights.WindowsServer** y elija **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="25c0b-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="25c0b-148">Si ha realizado cualquier tooApplicationInsights.config personalizaciones, guarde una copia del mismo antes de actualizar y después combinar los cambios en la nueva versión de hello.</span><span class="sxs-lookup"><span data-stu-id="25c0b-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="25c0b-149">4. Envío de datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="25c0b-149">4. Send telemetry</span></span>
<span data-ttu-id="25c0b-150">**Si instala únicamente el paquete de hello API:**</span><span class="sxs-lookup"><span data-stu-id="25c0b-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="25c0b-151">Establezca la clave de instrumentación de hello en el código, por ejemplo en `main()`:</span><span class="sxs-lookup"><span data-stu-id="25c0b-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="25c0b-152">`TelemetryConfiguration.Active.InstrumentationKey = "`*su clave*`";`</span><span class="sxs-lookup"><span data-stu-id="25c0b-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="25c0b-153">[Escribir su propio telemetría mediante API de hello](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="25c0b-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="25c0b-154">**Si ha instalado otros paquetes de Application Insights,** puede usar si lo prefiere, clave de instrumentación de hello .config archivo tooset hello:</span><span class="sxs-lookup"><span data-stu-id="25c0b-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="25c0b-155">Editar ApplicationInsights.config (que se agregó de forma Hola instalar NuGet).</span><span class="sxs-lookup"><span data-stu-id="25c0b-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="25c0b-156">Inserte este justo antes de la etiqueta de cierre de hello:</span><span class="sxs-lookup"><span data-stu-id="25c0b-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="25c0b-157">`<InstrumentationKey>`*clave de instrumentación de hello copió*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="25c0b-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="25c0b-158">Asegúrese de que las propiedades de Hola de ApplicationInsights.config en el Explorador de soluciones se establecen demasiado**acción de compilación = el contenido, copia tooOutput Directory = copia**.</span><span class="sxs-lookup"><span data-stu-id="25c0b-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="25c0b-159">Resulta útil tooset clave de instrumentación de hello en el código si desea demasiado[conmutador Hola clave para diferentes configuraciones de compilación](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="25c0b-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="25c0b-160">Si se establece la clave de hello en el código, no tiene tooset en hello `.config` archivo.</span><span class="sxs-lookup"><span data-stu-id="25c0b-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="25c0b-161"><a name="run"></a> Ejecución del proyecto</span><span class="sxs-lookup"><span data-stu-id="25c0b-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="25c0b-162">Hola de uso **F5** toorun la aplicación y pruébela: abrir diferentes páginas toogenerate algunos telemetría.</span><span class="sxs-lookup"><span data-stu-id="25c0b-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="25c0b-163">En Visual Studio, verá un recuento de eventos de Hola que se han enviado.</span><span class="sxs-lookup"><span data-stu-id="25c0b-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Recuento de eventos en Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="25c0b-165"><a name="monitor"></a> Visualización de los datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="25c0b-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="25c0b-166">Devolver toohello [portal de Azure](https://portal.azure.com/) y busque el recurso de Application Insights tooyour.</span><span class="sxs-lookup"><span data-stu-id="25c0b-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="25c0b-167">Buscar datos en los gráficos de información general de Hola.</span><span class="sxs-lookup"><span data-stu-id="25c0b-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="25c0b-168">Al principio, solo aparecerán uno o dos puntos.</span><span class="sxs-lookup"><span data-stu-id="25c0b-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="25c0b-169">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="25c0b-169">For example:</span></span>

![Desplazarse por los datos de toomore](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="25c0b-171">Haga clic en a través de cualquier toosee gráfico métricas más detalladas.</span><span class="sxs-lookup"><span data-stu-id="25c0b-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="25c0b-172">Más información acerca de las métricas</span><span class="sxs-lookup"><span data-stu-id="25c0b-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="25c0b-173">¿No hay datos?</span><span class="sxs-lookup"><span data-stu-id="25c0b-173">No data?</span></span>
* <span data-ttu-id="25c0b-174">Utilizar la aplicación de hello, abrir varias páginas para que genere algunos telemetría.</span><span class="sxs-lookup"><span data-stu-id="25c0b-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="25c0b-175">Abra hello [búsqueda](app-insights-diagnostic-search.md) icono toosee los eventos individuales.</span><span class="sxs-lookup"><span data-stu-id="25c0b-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="25c0b-176">A veces tiene eventos tooget un poco más de tiempo ya a través de la canalización de métricas de Hola.</span><span class="sxs-lookup"><span data-stu-id="25c0b-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="25c0b-177">Espere unos segundos y haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="25c0b-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="25c0b-178">Gráficos propios actualización periódicamente, pero sí puede actualizar manualmente si está esperando para algunos datos tooshow.</span><span class="sxs-lookup"><span data-stu-id="25c0b-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="25c0b-179">Vea [Solución de problemas](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="25c0b-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="25c0b-180">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="25c0b-180">Publish your app</span></span>
<span data-ttu-id="25c0b-181">Ahora la implementación del servidor de tooyour de aplicación o se acumulan datos hello tooAzure e inspección.</span><span class="sxs-lookup"><span data-stu-id="25c0b-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Usar la aplicación de Visual Studio toopublish](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="25c0b-183">Cuando se ejecuta en modo de depuración, se agiliza la telemetría a través de la canalización de hello, por lo que debería ver los datos que aparecen en segundos.</span><span class="sxs-lookup"><span data-stu-id="25c0b-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="25c0b-184">Al implementar la aplicación en la configuración de lanzamiento, los datos se acumulan más lentamente.</span><span class="sxs-lookup"><span data-stu-id="25c0b-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="25c0b-185">¿Después de publicar el servidor de tooyour de ningún dato?</span><span class="sxs-lookup"><span data-stu-id="25c0b-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="25c0b-186">Abra los puertos para el tráfico de salida en el firewall del servidor.</span><span class="sxs-lookup"><span data-stu-id="25c0b-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="25c0b-187">Vea [esta página](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) para lista de Hola de direcciones necesarias</span><span class="sxs-lookup"><span data-stu-id="25c0b-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="25c0b-188">¿Tiene problemas el servidor de compilación?</span><span class="sxs-lookup"><span data-stu-id="25c0b-188">Trouble on your build server?</span></span>
<span data-ttu-id="25c0b-189">Consulte [este apartado de la solución de problemas](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="25c0b-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="25c0b-190">Si la aplicación genera una gran cantidad de telemetría, módulo de muestreo adaptativo de Hola reducirá automáticamente volumen Hola que se envía toohello portal enviando sólo una fracción representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="25c0b-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="25c0b-191">Sin embargo, eventos que están relacionado toohello misma solicitud se selecciona o anula la selección como un grupo, por lo que puede desplazarse entre los eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="25c0b-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="25c0b-192">[Más información sobre el muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="25c0b-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="25c0b-193">Vídeo</span><span class="sxs-lookup"><span data-stu-id="25c0b-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="25c0b-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25c0b-194">Next steps</span></span>
* <span data-ttu-id="25c0b-195">[Agregar más telemetría](app-insights-asp-net-more.md) tooget Hola vista de 360 grados completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="25c0b-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

