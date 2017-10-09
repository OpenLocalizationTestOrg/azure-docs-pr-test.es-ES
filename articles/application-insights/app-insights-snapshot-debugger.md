---
title: "aaaAzure aplicación visión instantánea depurador para las aplicaciones de .NET | Documentos de Microsoft"
description: "Depuración de las instantáneas que se recopilan automáticamente cuando se producen excepciones en aplicaciones de producción de .NET"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="96083-103">Depurar instantáneas cuando se producen excepciones en aplicaciones de .NET</span><span class="sxs-lookup"><span data-stu-id="96083-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="96083-104">Cuando se produce una excepción, puede recopilar automáticamente una instantánea de depuración desde la aplicación web activa.</span><span class="sxs-lookup"><span data-stu-id="96083-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="96083-105">instantánea de Hello muestra el estado de Hola de código fuente y variables Hola momento Hola mensaje de excepción lanzada.</span><span class="sxs-lookup"><span data-stu-id="96083-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="96083-106">Hola instantánea depurador (versión preliminar) en [Azure Application Insights](app-insights-overview.md) supervisa la telemetría de excepción de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="96083-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="96083-107">Recopila instantáneas en las parte superior: iniciar excepciones para que tenga información de Hola que necesita toodiagnose problemas en producción.</span><span class="sxs-lookup"><span data-stu-id="96083-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="96083-108">Incluir hello [paquete de NuGet del compilador instantánea](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) en la aplicación y, opcionalmente, configurar los parámetros de recopilación en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Las instantáneas aparecen en [excepciones](app-insights-asp-net-exceptions.md) en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="96083-109">Puede ver instantáneas de depuración en la pila de llamadas de Hola Hola toosee portal e inspeccionar las variables en cada marco de pila de llamadas.</span><span class="sxs-lookup"><span data-stu-id="96083-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="96083-110">una experiencia de depuración más eficaz con el código fuente, abra instantáneas con Visual Studio Enterprise de 2017 por tooget [descargar la extensión del depurador de instantánea de Hola para Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="96083-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="96083-111">La recopilación de instantáneas está disponible para:</span><span class="sxs-lookup"><span data-stu-id="96083-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="96083-112">Aplicaciones de .NET Framework y ASP.NET que ejecuten .NET Framework 4.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="96083-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="96083-113">Aplicaciones de .NET Core 2.0 y ASP.NET Core 2.0 que se ejecuten en Windows.</span><span class="sxs-lookup"><span data-stu-id="96083-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="96083-114">Configurar la recopilación de instantáneas para aplicaciones ASP.NET</span><span class="sxs-lookup"><span data-stu-id="96083-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="96083-115">[Habilite Application Insights en su aplicación web](app-insights-asp-net.md), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="96083-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="96083-116">Incluir hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) paquete de NuGet en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96083-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="96083-117">Revisar opciones predeterminadas de Hola que Hola paquete agregado demasiado[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="96083-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="96083-118">Las instantáneas se recopilan sólo en las excepciones que son notificados tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="96083-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="96083-119">En algunos casos (por ejemplo, versiones anteriores de la plataforma .NET de hello), puede que tenga demasiado[configurar la recopilación de excepción](app-insights-asp-net-exceptions.md#exceptions) toosee excepciones con las instantáneas en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="96083-120">Configurar la recopilación de instantáneas para aplicaciones ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="96083-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="96083-121">[Habilite Application Insights en su aplicación web ASP.NET Core](app-insights-asp-net-core.md), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="96083-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="96083-122">Incluir hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) paquete de NuGet en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96083-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="96083-123">Modificar hello `ConfigureServices` método de la aplicación `Startup` clase procesador de telemetría del recopilador de tooadd Hola instantánea.</span><span class="sxs-lookup"><span data-stu-id="96083-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="96083-124">debe agregar el código de Hello depende de la versión que se hace referencia de Hola de hello paquete Microsoft.ApplicationInsights.ASPNETCore NuGet.</span><span class="sxs-lookup"><span data-stu-id="96083-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="96083-125">Para Microsoft.ApplicationInsights.AspNetCore 2.1.0, agregue:</span><span class="sxs-lookup"><span data-stu-id="96083-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="96083-126">Para Microsoft.ApplicationInsights.AspNetCore 2.1.1, agregue:</span><span class="sxs-lookup"><span data-stu-id="96083-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="96083-127">Configurar la recopilación de instantáneas para otras aplicaciones .NET</span><span class="sxs-lookup"><span data-stu-id="96083-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="96083-128">Si la aplicación ya no está instrumentada con Application Insights, empezar por [habilitar Application Insights y clave de instrumentación de configuración hello](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="96083-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="96083-129">Agregar hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) paquete de NuGet en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96083-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="96083-130">Las instantáneas se recopilan sólo en las excepciones que son notificados tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="96083-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="96083-131">Puede que necesite toomodify su tooreport código ellos.</span><span class="sxs-lookup"><span data-stu-id="96083-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="96083-132">código de control de excepciones de Hello depende de la estructura de saludo de la aplicación, pero es un ejemplo a continuación:</span><span class="sxs-lookup"><span data-stu-id="96083-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="96083-133">Concesión de permisos</span><span class="sxs-lookup"><span data-stu-id="96083-133">Grant permissions</span></span>

<span data-ttu-id="96083-134">Los propietarios de hello suscripción de Azure pueden inspeccionar las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="96083-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="96083-135">Otros usuarios deben obtener permiso de un propietario.</span><span class="sxs-lookup"><span data-stu-id="96083-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="96083-136">permiso de toogrant, asignar Hola `Application Insights Snapshot Debugger` toousers de rol que inspeccionará las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="96083-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="96083-137">Esta función se puede asignar tooindividual a los usuarios o grupos por propietarios de suscripciones de recurso de información de la aplicación de destino de Hola o su grupo de recursos o suscripción.</span><span class="sxs-lookup"><span data-stu-id="96083-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="96083-138">Abra la hoja de Control de acceso (IAM) de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="96083-139">Haga clic en Hola + botón Agregar.</span><span class="sxs-lookup"><span data-stu-id="96083-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="96083-140">Seleccione a depurador de instantánea de información de aplicación de lista desplegable de hello Roles.</span><span class="sxs-lookup"><span data-stu-id="96083-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="96083-141">Buscar y escriba un nombre para hello tooadd de usuario.</span><span class="sxs-lookup"><span data-stu-id="96083-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="96083-142">Haga clic en función de hello guardar botón tooadd Hola usuario toohello.</span><span class="sxs-lookup"><span data-stu-id="96083-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="96083-143">Las instantáneas pueden contener información personal y otra información confidencial en valores de variables y parámetros.</span><span class="sxs-lookup"><span data-stu-id="96083-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="96083-144">Depurar las instantáneas en el portal de Application Insights Hola</span><span class="sxs-lookup"><span data-stu-id="96083-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="96083-145">Si una instantánea está disponible para una determinada excepción o un Id. del problema, un **Abrir instantánea depurar** botón se muestra en hello [excepción](app-insights-asp-net-exceptions.md) en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![Botón Abrir instantánea de depuración de la excepción](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="96083-147">Hola vista de instantánea de depurar, verá una pila de llamadas y un panel de variables.</span><span class="sxs-lookup"><span data-stu-id="96083-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="96083-148">Cuando se selecciona marcos de llamada de Hola se apilan en el panel de pila de llamadas de hello, puede ver las variables locales y parámetros de dicha función llame a en el panel de variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Vista de depuración instantánea en el portal de Hola](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="96083-150">Las instantáneas pueden contener información confidencial y, de forma predeterminada, no están visibles.</span><span class="sxs-lookup"><span data-stu-id="96083-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="96083-151">tooview instantáneas, debe tener hello `Application Insights Snapshot Debugger` tooyou rol asignado.</span><span class="sxs-lookup"><span data-stu-id="96083-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="96083-152">Depuración de instantáneas con Visual Studio Enterprise 2017</span><span class="sxs-lookup"><span data-stu-id="96083-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="96083-153">Haga clic en hello **descargar instantánea** toodownload botón un `.diagsession` archivo, que puede abrirse en Visual Studio Enterprise de 2017.</span><span class="sxs-lookup"><span data-stu-id="96083-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="96083-154">Hola tooopen `.diagsession` archivo, primero debe [descargar e instalar la extensión del depurador de instantánea de Hola para Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="96083-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="96083-155">Después de abrir el archivo de instantánea de hello, aparece la página de depuración de minivolcado de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="96083-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="96083-156">Haga clic en **depurar código administrado** toostart depuración instantánea Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="96083-157">instantánea de Hello abre toohello línea de código donde se inició la excepción de Hola para que se puede depurar el estado actual de hello del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Visualización de la instantánea de depuración en Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="96083-159">Hola descargado instantánea contiene los archivos de símbolos que se encontraron en el servidor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="96083-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="96083-160">Estos archivos de símbolos son datos de instantánea tooassociate necesarios con el código fuente.</span><span class="sxs-lookup"><span data-stu-id="96083-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="96083-161">Para las aplicaciones de servicio de aplicaciones, asegúrese de implementación de símbolos tooenable seguro al publicar las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="96083-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="96083-162">Funcionamiento de las instantáneas</span><span class="sxs-lookup"><span data-stu-id="96083-162">How snapshots work</span></span>

<span data-ttu-id="96083-163">Cuando se inicia la aplicación, se crea un proceso independiente de usuario de carga de instantáneas que supervisa las solicitudes de instantáneas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96083-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="96083-164">Cuando se solicita una instantánea, se realiza una instantánea de hello ejecutando el proceso en unos 10 minutos de too20.</span><span class="sxs-lookup"><span data-stu-id="96083-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="96083-165">a continuación, se analiza el proceso de instantáneas de Hello y una instantánea se crea mientras continúa el proceso principal de hello toorun sirven para toousers de tráfico.</span><span class="sxs-lookup"><span data-stu-id="96083-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="96083-166">Hello instantánea es cargado tooApplication visión junto con los archivos pertinentes símbolos (.pdb) que necesita tooview instantánea Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="96083-167">Limitaciones actuales</span><span class="sxs-lookup"><span data-stu-id="96083-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="96083-168">Publicación de símbolos</span><span class="sxs-lookup"><span data-stu-id="96083-168">Publish symbols</span></span>
<span data-ttu-id="96083-169">Hola instantánea depurador requiere archivos de símbolos en variables de toodecode de servidor de producción de hello y tooprovide una experiencia de depuración en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="96083-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="96083-170">versión de Hola 15,2 de Visual Studio de 2017 publica símbolos para versiones de lanzamiento de forma predeterminada cuando se publique tooApp servicio.</span><span class="sxs-lookup"><span data-stu-id="96083-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="96083-171">En las versiones anteriores, necesita tooadd Hola siguiente perfil de publicación de la línea tooyour `.pubxml` de archivos para que los símbolos se publican en modo de lanzamiento:</span><span class="sxs-lookup"><span data-stu-id="96083-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="96083-172">Para el cálculo de Azure y otros tipos, asegúrese de que los archivos de símbolos de Hola Hola misma carpeta del archivo .dll de aplicación principal de hello (normalmente, `wwwroot/bin`) o están disponibles en la ruta de acceso actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="96083-173">Compilaciones optimizadas</span><span class="sxs-lookup"><span data-stu-id="96083-173">Optimized builds</span></span>
<span data-ttu-id="96083-174">En algunos casos, las variables locales no pueda visualizarse en versiones de lanzamiento debido a optimizaciones que se aplican durante el proceso de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="96083-175">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="96083-175">Troubleshooting</span></span>

<span data-ttu-id="96083-176">Estas sugerencias de ayudarán para solucionar problemas con hello depurador de instantánea.</span><span class="sxs-lookup"><span data-stu-id="96083-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="96083-177">Compruebe la clave de instrumentación de Hola</span><span class="sxs-lookup"><span data-stu-id="96083-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="96083-178">Asegúrese de que está utilizando la clave de instrumentación correcta de hello en la aplicación publicada.</span><span class="sxs-lookup"><span data-stu-id="96083-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="96083-179">Por lo general, Application Insights lee clave de instrumentación de Hola Hola ApplicationInsights.config archivo.</span><span class="sxs-lookup"><span data-stu-id="96083-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="96083-180">Compruebe que el valor de hello es Hola igual como clave de instrumentación de hello para el recurso de Application Insights de Hola que aparece en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="96083-181">Compruebe los registros de cargador de Hola</span><span class="sxs-lookup"><span data-stu-id="96083-181">Check hello uploader logs</span></span>

<span data-ttu-id="96083-182">Después de crear una instantánea, se crea un archivo de minivolcado (.dmp) en el disco.</span><span class="sxs-lookup"><span data-stu-id="96083-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="96083-183">Un proceso independiente de la herramienta de envío toma ese archivo de minivolcado y lo carga, junto con los archivos PDB asociados, tooApplication almacenamiento de visión instantánea depurador.</span><span class="sxs-lookup"><span data-stu-id="96083-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="96083-184">Una vez minivolcado Hola ha cargado correctamente, se elimina del disco.</span><span class="sxs-lookup"><span data-stu-id="96083-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="96083-185">archivos de registro de Hello de cargador de minivolcado Hola se conservan en disco.</span><span class="sxs-lookup"><span data-stu-id="96083-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="96083-186">En un entorno de App Service, puede encontrar estos registros en `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="96083-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="96083-187">Sitio de administración de uso hello Kudu para el servicio de aplicaciones toofind estos archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="96083-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="96083-188">Abra la aplicación de servicio de aplicaciones en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="96083-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="96083-189">Seleccione hello **herramientas avanzadas** hoja o buscar **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="96083-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="96083-190">Haga clic en **Ir**.</span><span class="sxs-lookup"><span data-stu-id="96083-190">Click **Go**.</span></span>
4. <span data-ttu-id="96083-191">Hola **consola de depuración** cuadro de lista desplegable, seleccione **CMD**.</span><span class="sxs-lookup"><span data-stu-id="96083-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="96083-192">Haga clic en **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="96083-192">Click **LogFiles**.</span></span>

<span data-ttu-id="96083-193">Debería ver al menos un archivo con un nombre que comienza con `Uploader_` y una extensión `.log`.</span><span class="sxs-lookup"><span data-stu-id="96083-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="96083-194">Haga clic en toodownload de icono adecuado de hello los archivos de registro o abrirlos en un explorador.</span><span class="sxs-lookup"><span data-stu-id="96083-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="96083-195">nombre de archivo de Hello incluye el nombre del equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="96083-196">Si la instancia de App Service se hospeda en más de un equipo, hay archivos de registro independientes para cada equipo.</span><span class="sxs-lookup"><span data-stu-id="96083-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="96083-197">Cuando el cargador de hello detecta un nuevo archivo de minivolcado, se registra en el archivo de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="96083-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="96083-198">Este es un ejemplo de carga correcta:</span><span class="sxs-lookup"><span data-stu-id="96083-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="96083-199">En el ejemplo anterior de hello, es la clave de instrumentación de hello `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="96083-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="96083-200">Este valor debe coincidir con la clave de instrumentación de hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96083-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="96083-201">minivolcado Hola está asociado a una instantánea con el Id. de hello `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="96083-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="96083-202">Puede utilizar este identificador posterior hello toolocate asociados telemetría de excepción en el análisis de visión de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="96083-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="96083-203">cargador de Hello busca archivos PDB nuevo una vez cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="96083-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="96083-204">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="96083-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="96083-205">Para las aplicaciones que son _no_ hospedado en el servicio de aplicaciones, los registros de cargador de hello están en hello misma carpeta que minivolcados de hello: `%TEMP%\Dumps\<ikey>` (donde `<ikey>` es la clave de instrumentación).</span><span class="sxs-lookup"><span data-stu-id="96083-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="96083-206">Use Application Insights buscar excepciones toofind con instantáneas</span><span class="sxs-lookup"><span data-stu-id="96083-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="96083-207">Cuando se crea una instantánea, Hola producir la excepción se etiqueta con un identificador de instantánea.</span><span class="sxs-lookup"><span data-stu-id="96083-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="96083-208">Una vez telemetría de excepción de hello tooApplication notificado visión, ese identificador de la instantánea se incluye como una propiedad personalizada.</span><span class="sxs-lookup"><span data-stu-id="96083-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="96083-209">Hoja de búsqueda de hello en Application Insights, puede utilizar para buscar todos los telemetría con hello `ai.snapshot.id` propiedad personalizada.</span><span class="sxs-lookup"><span data-stu-id="96083-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="96083-210">Buscar recursos de Application Insights tooyour Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="96083-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="96083-211">Haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="96083-211">Click **Search**.</span></span>
3. <span data-ttu-id="96083-212">Tipo `ai.snapshot.id` en Hola cuadro de texto Buscar y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="96083-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Búsqueda de telemetría con un identificador de la instantánea en el portal de Hola](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="96083-214">Si esta búsqueda no devuelve ningún resultado, no hay instantáneas eran visión tooApplication notificado para su aplicación en el intervalo de tiempo de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="96083-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="96083-215">toosearch para un identificador de la instantánea específico de registros de cargador de hello, escriba ese identificador en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="96083-216">Si no se encuentra la telemetría para una instantánea que sabe que se cargó, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="96083-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="96083-217">Compruebe que está viendo en el recurso de Application Insights derecho Hola comprobando clave de instrumentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="96083-218">Al usar Hola marca de tiempo de registro de cargador de hello, ajustar filtro de intervalo de tiempo de Hola de hello búsqueda toocover ese intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="96083-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="96083-219">Si aún no ve una excepción con ese identificador de la instantánea, excepción de telemetría de hello no estaba incluido tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="96083-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="96083-220">Esta situación puede ocurrir si se bloqueó la aplicación después de que tomó la instantánea de hello, pero para que notifique telemetría de excepción de Hola.</span><span class="sxs-lookup"><span data-stu-id="96083-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="96083-221">En este caso, compruebe Hola inicia el servicio de aplicaciones con `Diagnose and solve problems` toosee si hubiera inesperado se reinicia o las excepciones no controladas.</span><span class="sxs-lookup"><span data-stu-id="96083-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96083-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96083-222">Next steps</span></span>

* <span data-ttu-id="96083-223">[Establecer snappoints en el código](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget instantáneas sin tener que esperar una excepción.</span><span class="sxs-lookup"><span data-stu-id="96083-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="96083-224">[Diagnosticar las excepciones en las aplicaciones web](app-insights-asp-net-exceptions.md) explica cómo toomake tooApplication visible de excepciones más información.</span><span class="sxs-lookup"><span data-stu-id="96083-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="96083-225">[Detección inteligente](app-insights-proactive-diagnostics.md) detecta automáticamente las anomalías de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="96083-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
