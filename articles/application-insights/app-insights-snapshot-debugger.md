---
title: "Depurador de instantáneas de Azure Application Insights para aplicaciones de .NET | Microsoft Docs"
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="d0dff-103">Depurar instantáneas cuando se producen excepciones en aplicaciones de .NET</span><span class="sxs-lookup"><span data-stu-id="d0dff-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="d0dff-104">Cuando se produce una excepción, puede recopilar automáticamente una instantánea de depuración desde la aplicación web activa.</span><span class="sxs-lookup"><span data-stu-id="d0dff-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="d0dff-105">La instantánea muestra el estado del código fuente y las variables en el momento en que se produjo la excepción.</span><span class="sxs-lookup"><span data-stu-id="d0dff-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="d0dff-106">El depurador de instantáneas (versión preliminar) de [Azure Application Insights](app-insights-overview.md) supervisa la telemetría de excepciones de su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d0dff-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="d0dff-107">Recopila instantáneas de las excepciones más importantes con el fin de que tenga la información necesaria para diagnosticar problemas en producción.</span><span class="sxs-lookup"><span data-stu-id="d0dff-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="d0dff-108">Incluya el [paquete NuGet del recopilador de instantáneas](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) en la aplicación y, opcionalmente, configure los parámetros de recopilación en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Las instantáneas aparecen en [excepciones](app-insights-asp-net-exceptions.md) en el portal de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d0dff-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="d0dff-109">Puede ver las instantáneas de depuración en el portal para examinar la pila de llamadas e inspeccionar las variables en cada marco de pila de llamadas.</span><span class="sxs-lookup"><span data-stu-id="d0dff-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="d0dff-110">Para obtener una experiencia de depuración más eficaz con el código fuente, abra las instantáneas con Visual Studio Enterprise de 2017 [descargando la extensión del depurador de instantáneas para Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="d0dff-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="d0dff-111">La recopilación de instantáneas está disponible para:</span><span class="sxs-lookup"><span data-stu-id="d0dff-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="d0dff-112">Aplicaciones de .NET Framework y ASP.NET que ejecuten .NET Framework 4.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d0dff-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="d0dff-113">Aplicaciones de .NET Core 2.0 y ASP.NET Core 2.0 que se ejecuten en Windows.</span><span class="sxs-lookup"><span data-stu-id="d0dff-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="d0dff-114">Configurar la recopilación de instantáneas para aplicaciones ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d0dff-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="d0dff-115">[Habilite Application Insights en su aplicación web](app-insights-asp-net.md), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="d0dff-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="d0dff-116">Incluya el paquete NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0dff-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="d0dff-117">Revise las opciones predeterminadas que el paquete ha agregado a [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="d0dff-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="d0dff-118">Las instantáneas solo se recopilan en las excepciones de las que se informa a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d0dff-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="d0dff-119">En algunos casos (por ejemplo, en versiones anteriores de la plataforma. NET), es posible que tenga que [configurar la recopilación de excepciones](app-insights-asp-net-exceptions.md#exceptions) para ver las excepciones con las instantáneas en el portal.</span><span class="sxs-lookup"><span data-stu-id="d0dff-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="d0dff-120">Configurar la recopilación de instantáneas para aplicaciones ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="d0dff-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="d0dff-121">[Habilite Application Insights en su aplicación web ASP.NET Core](app-insights-asp-net-core.md), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="d0dff-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="d0dff-122">Incluya el paquete NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0dff-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="d0dff-123">Modifique el método `ConfigureServices` de la clase `Startup` de la aplicación para agregar el procesador de telemetría del recopilador de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="d0dff-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="d0dff-124">El código que debe agregar depende de la versión del paquete NuGet Microsoft.ApplicationInsights.ASPNETCore a la que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="d0dff-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="d0dff-125">Para Microsoft.ApplicationInsights.AspNetCore 2.1.0, agregue:</span><span class="sxs-lookup"><span data-stu-id="d0dff-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="d0dff-126">Para Microsoft.ApplicationInsights.AspNetCore 2.1.1, agregue:</span><span class="sxs-lookup"><span data-stu-id="d0dff-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="d0dff-127">Configurar la recopilación de instantáneas para otras aplicaciones .NET</span><span class="sxs-lookup"><span data-stu-id="d0dff-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="d0dff-128">Si la aplicación aún no tiene Application Insights, debe empezar por [habilitar Application Insights y establecer la clave de instrumentación](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="d0dff-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="d0dff-129">Agregue el paquete NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0dff-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="d0dff-130">Las instantáneas solo se recopilan en las excepciones de las que se informa a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d0dff-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="d0dff-131">Es posible que tenga que modificar el código para informar de las excepciones.</span><span class="sxs-lookup"><span data-stu-id="d0dff-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="d0dff-132">El código de control de excepciones depende de la estructura de la aplicación, pero a continuación se muestra un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0dff-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="d0dff-133">Concesión de permisos</span><span class="sxs-lookup"><span data-stu-id="d0dff-133">Grant permissions</span></span>

<span data-ttu-id="d0dff-134">Los propietarios de la suscripción de Azure pueden inspeccionar instantáneas.</span><span class="sxs-lookup"><span data-stu-id="d0dff-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="d0dff-135">Otros usuarios deben obtener permiso de un propietario.</span><span class="sxs-lookup"><span data-stu-id="d0dff-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="d0dff-136">Para conceder permiso, asigne el rol `Application Insights Snapshot Debugger` a los usuarios que inspeccionarán instantáneas.</span><span class="sxs-lookup"><span data-stu-id="d0dff-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="d0dff-137">Los propietarios de suscripción pueden asignar este rol a usuarios individuales o grupos en el recurso de Application Insights de destino o en su grupo de recursos o suscripción.</span><span class="sxs-lookup"><span data-stu-id="d0dff-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="d0dff-138">Abra la hoja Access Control (IAM).</span><span class="sxs-lookup"><span data-stu-id="d0dff-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="d0dff-139">Haga clic en el botón +Agregar.</span><span class="sxs-lookup"><span data-stu-id="d0dff-139">Click the +Add button.</span></span>
1. <span data-ttu-id="d0dff-140">Seleccione Depurador de instantáneas de Application Insights en la lista desplegable Roles.</span><span class="sxs-lookup"><span data-stu-id="d0dff-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="d0dff-141">Busque el usuario que quiere agregar y escriba un nombre.</span><span class="sxs-lookup"><span data-stu-id="d0dff-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="d0dff-142">Haga clic en el botón Guardar para agregar el usuario al rol.</span><span class="sxs-lookup"><span data-stu-id="d0dff-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="d0dff-143">Las instantáneas pueden contener información personal y otra información confidencial en valores de variables y parámetros.</span><span class="sxs-lookup"><span data-stu-id="d0dff-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="d0dff-144">Depuración de instantáneas en el portal de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d0dff-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="d0dff-145">Si una instantánea está disponible para una excepción o un identificador de problema determinados, se mostrará un botón **Abrir instantánea de depuración** en la [excepción](app-insights-asp-net-exceptions.md) del portal de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d0dff-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![Botón Abrir instantánea de depuración de la excepción](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="d0dff-147">En la vista de depuración instantánea, verá una pila de llamadas y un panel de variables.</span><span class="sxs-lookup"><span data-stu-id="d0dff-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="d0dff-148">Al seleccionar marcos de la pila de llamadas en el panel de la pila de llamadas, podrá ver las variables locales y los parámetros para esa llamada de función en el panel de variables.</span><span class="sxs-lookup"><span data-stu-id="d0dff-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![Visualización de la instantánea de depuración en el portal](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="d0dff-150">Las instantáneas pueden contener información confidencial y, de forma predeterminada, no están visibles.</span><span class="sxs-lookup"><span data-stu-id="d0dff-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="d0dff-151">Para ver las instantáneas, debe tener asignado el rol `Application Insights Snapshot Debugger`.</span><span class="sxs-lookup"><span data-stu-id="d0dff-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="d0dff-152">Depuración de instantáneas con Visual Studio Enterprise 2017</span><span class="sxs-lookup"><span data-stu-id="d0dff-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="d0dff-153">Haga clic en el botón **Descargar instantánea** para descargar un archivo `.diagsession`, que puede abrirse en Visual Studio Enterprise 2017.</span><span class="sxs-lookup"><span data-stu-id="d0dff-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="d0dff-154">Para abrir el archivo `.diagsession`, debe primero [descargar e instalar la extensión del Depurador de instantáneas para Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="d0dff-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="d0dff-155">Después de abrir el archivo de instantánea, aparece la página de depuración de minivolcado de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0dff-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="d0dff-156">Haga clic en **Depurar código administrado** para empezar a depurar la instantánea.</span><span class="sxs-lookup"><span data-stu-id="d0dff-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="d0dff-157">La instantánea se abre en la línea de código donde se produjo la excepción para que pueda depurar el estado actual del proceso.</span><span class="sxs-lookup"><span data-stu-id="d0dff-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![Visualización de la instantánea de depuración en Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="d0dff-159">La instantánea descargada contiene los archivos de símbolos que se encontraron en el servidor de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="d0dff-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="d0dff-160">Estos archivos de símbolos son necesarios para asociar los datos de instantáneas con el código fuente.</span><span class="sxs-lookup"><span data-stu-id="d0dff-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="d0dff-161">Para las aplicaciones de App Service, asegúrese de habilitar la implementación de símbolos cuando publique las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="d0dff-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="d0dff-162">Funcionamiento de las instantáneas</span><span class="sxs-lookup"><span data-stu-id="d0dff-162">How snapshots work</span></span>

<span data-ttu-id="d0dff-163">Cuando se inicia la aplicación, se crea un proceso independiente de usuario de carga de instantáneas que supervisa las solicitudes de instantáneas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0dff-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="d0dff-164">Cuando se solicita una instantánea, se realiza una instantánea de los procesos en ejecución en unos 10-20 minutos.</span><span class="sxs-lookup"><span data-stu-id="d0dff-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="d0dff-165">El proceso de instantánea se analiza y se crea una instantánea mientras el proceso principal sigue ejecutándose y entregando el tráfico a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d0dff-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="d0dff-166">Luego, la instantánea se carga en Application Insights junto con los correspondientes archivos de símbolos (.pdb) que sean necesarios para ver la instantánea.</span><span class="sxs-lookup"><span data-stu-id="d0dff-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="d0dff-167">Limitaciones actuales</span><span class="sxs-lookup"><span data-stu-id="d0dff-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="d0dff-168">Publicación de símbolos</span><span class="sxs-lookup"><span data-stu-id="d0dff-168">Publish symbols</span></span>
<span data-ttu-id="d0dff-169">El Depurador de instantáneas requiere que los archivos de símbolos estén presentes en el servidor de producción para descodificar variables y proporcionar una experiencia de depuración en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0dff-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="d0dff-170">La versión 15.2 de Visual Studio 2017 publica símbolos de compilaciones de versión de forma predeterminada al publicar en App Service.</span><span class="sxs-lookup"><span data-stu-id="d0dff-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="d0dff-171">En las versiones anteriores, tiene que agregar la siguiente línea al archivo `.pubxml` de su perfil de publicación para que los símbolos se publiquen en modo de versión:</span><span class="sxs-lookup"><span data-stu-id="d0dff-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="d0dff-172">Para Azure Compute y otros tipos, asegúrese de que los archivos de símbolos están en la misma carpeta del archivo .dll principal de la aplicación (normalmente, `wwwroot/bin`), o que están disponibles en la ruta de acceso actual.</span><span class="sxs-lookup"><span data-stu-id="d0dff-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="d0dff-173">Compilaciones optimizadas</span><span class="sxs-lookup"><span data-stu-id="d0dff-173">Optimized builds</span></span>
<span data-ttu-id="d0dff-174">En algunos casos, las variables locales no se pueden ver en las compilaciones de versión debido a las optimizaciones que se aplican durante el proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="d0dff-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d0dff-175">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="d0dff-175">Troubleshooting</span></span>

<span data-ttu-id="d0dff-176">Estas sugerencias le ayudarán a solucionar problemas con el depurador de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="d0dff-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="d0dff-177">Comprobar la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="d0dff-177">Verify the instrumentation key</span></span>

<span data-ttu-id="d0dff-178">Asegúrese de que está usando la clave de instrumentación correcta en la aplicación publicada.</span><span class="sxs-lookup"><span data-stu-id="d0dff-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="d0dff-179">Por lo general, Application Insights lee la clave de instrumentación desde el archivo ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="d0dff-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="d0dff-180">Compruebe que el valor es igual que la clave de instrumentación para el recurso de Application Insights que ve en el portal.</span><span class="sxs-lookup"><span data-stu-id="d0dff-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="d0dff-181">Comprobar los registros de usuario de carga</span><span class="sxs-lookup"><span data-stu-id="d0dff-181">Check the uploader logs</span></span>

<span data-ttu-id="d0dff-182">Después de crear una instantánea, se crea un archivo de minivolcado (.dmp) en el disco.</span><span class="sxs-lookup"><span data-stu-id="d0dff-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="d0dff-183">Un proceso de usuario de carga independiente toma ese archivo de minivolcado y lo carga, junto con los archivos PDB asociados, al almacenamiento del depurador de instantáneas de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d0dff-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="d0dff-184">Después de cargar correctamente el minivolcado, se elimina del disco.</span><span class="sxs-lookup"><span data-stu-id="d0dff-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="d0dff-185">Los archivos de registro para el usuario de carga del minivolcado se conservan en disco.</span><span class="sxs-lookup"><span data-stu-id="d0dff-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="d0dff-186">En un entorno de App Service, puede encontrar estos registros en `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="d0dff-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="d0dff-187">Use el sitio de administración de Kudu para App Service para buscar estos archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="d0dff-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="d0dff-188">Abra la aplicación App Service en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d0dff-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="d0dff-189">Seleccione la hoja **Herramientas avanzadas** o busque **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="d0dff-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="d0dff-190">Haga clic en **Ir**.</span><span class="sxs-lookup"><span data-stu-id="d0dff-190">Click **Go**.</span></span>
4. <span data-ttu-id="d0dff-191">En el cuadro de lista desplegable **Consola de depuración**, seleccione **CMD**.</span><span class="sxs-lookup"><span data-stu-id="d0dff-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="d0dff-192">Haga clic en **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="d0dff-192">Click **LogFiles**.</span></span>

<span data-ttu-id="d0dff-193">Debería ver al menos un archivo con un nombre que comienza con `Uploader_` y una extensión `.log`.</span><span class="sxs-lookup"><span data-stu-id="d0dff-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="d0dff-194">Haga clic en el icono adecuado para descargar los archivos de registro o abrirlos en un explorador.</span><span class="sxs-lookup"><span data-stu-id="d0dff-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="d0dff-195">El nombre de archivo incluye el nombre del equipo.</span><span class="sxs-lookup"><span data-stu-id="d0dff-195">The file name includes the machine name.</span></span> <span data-ttu-id="d0dff-196">Si la instancia de App Service se hospeda en más de un equipo, hay archivos de registro independientes para cada equipo.</span><span class="sxs-lookup"><span data-stu-id="d0dff-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="d0dff-197">Cuando el usuario de carga detecta un nuevo archivo de minivolcado, se registra en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="d0dff-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="d0dff-198">Este es un ejemplo de carga correcta:</span><span class="sxs-lookup"><span data-stu-id="d0dff-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="d0dff-199">En el ejemplo anterior, la clave de instrumentación es `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="d0dff-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="d0dff-200">Este valor debe coincidir con la clave de instrumentación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0dff-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="d0dff-201">El minivolcado está asociado a una instantánea con el identificador `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="d0dff-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="d0dff-202">Puede usar este identificador más adelante para buscar la telemetría de excepciones asociada en Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="d0dff-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="d0dff-203">El usuario de carga busca nuevos archivos PDB una vez cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="d0dff-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="d0dff-204">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0dff-204">Here's an example:</span></span>

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

<span data-ttu-id="d0dff-205">Para las aplicaciones que _no_ están hospedadas en App Service, los registros de usuario de carga están en la misma carpeta que los minivolcados: `%TEMP%\Dumps\<ikey>` (donde `<ikey>` es la clave de instrumentación).</span><span class="sxs-lookup"><span data-stu-id="d0dff-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="d0dff-206">Usar la búsqueda de Application Insights para buscar excepciones con instantáneas</span><span class="sxs-lookup"><span data-stu-id="d0dff-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="d0dff-207">Cuando se crea una instantánea, la excepción iniciada se etiqueta con un identificador de instantánea.</span><span class="sxs-lookup"><span data-stu-id="d0dff-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="d0dff-208">Cuando se notifica la telemetría de excepciones a Application Insights, ese identificador de instantánea se incluye como una propiedad personalizada.</span><span class="sxs-lookup"><span data-stu-id="d0dff-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="d0dff-209">Mediante la hoja de búsqueda de Application Insights, puede buscar toda la telemetría con la propiedad personalizada `ai.snapshot.id`.</span><span class="sxs-lookup"><span data-stu-id="d0dff-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="d0dff-210">Vaya al recurso de Application Insights en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d0dff-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="d0dff-211">Haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="d0dff-211">Click **Search**.</span></span>
3. <span data-ttu-id="d0dff-212">En el cuadro de texto Buscar, escriba `ai.snapshot.id` y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="d0dff-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![Buscar telemetría con un identificador de instantánea en el portal](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="d0dff-214">Si esta búsqueda no devuelve ningún resultado, no se ha informado de ninguna instantánea a Application Insights para la aplicación en el intervalo de tiempo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d0dff-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="d0dff-215">Para buscar un identificador de instantánea específico en los registros de usuario de carga, escriba ese identificador en el cuadro Buscar.</span><span class="sxs-lookup"><span data-stu-id="d0dff-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="d0dff-216">Si no se encuentra la telemetría para una instantánea que sabe que se cargó, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d0dff-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="d0dff-217">Compruebe que está viendo el recurso de Application Insights correcto comprobando la clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="d0dff-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="d0dff-218">Mediante la marca de tiempo del registro del usuario de carga, ajuste el filtro de intervalo de tiempo de la búsqueda para cubrir ese intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="d0dff-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="d0dff-219">Si sigue sin ver una excepción con ese identificador de instantánea, significa que la excepción de telemetría no se ha notificado a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d0dff-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="d0dff-220">Esta situación puede ocurrir si se bloqueó la aplicación después de que tomó la instantánea, pero antes de notificar la telemetría de excepción.</span><span class="sxs-lookup"><span data-stu-id="d0dff-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="d0dff-221">En este caso, compruebe los registros de App Service en `Diagnose and solve problems` para ver si hay reinicios inesperados o excepciones no controladas.</span><span class="sxs-lookup"><span data-stu-id="d0dff-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0dff-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0dff-222">Next steps</span></span>

* <span data-ttu-id="d0dff-223">[Establezca puntos de ajuste en el código](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) para obtener instantáneas sin tener que esperar una excepción.</span><span class="sxs-lookup"><span data-stu-id="d0dff-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="d0dff-224">En el artículo sobre cómo [diagnosticar excepciones en aplicaciones web](app-insights-asp-net-exceptions.md) se explica cómo hacer más visibles las excepciones en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d0dff-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="d0dff-225">[Detección inteligente](app-insights-proactive-diagnostics.md) detecta automáticamente las anomalías de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d0dff-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
