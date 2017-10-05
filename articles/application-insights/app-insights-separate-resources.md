---
title: "Separación de la telemetría de desarrollo, prueba y publicación en Azure Application Insights | Microsoft Docs"
description: "Este artículo trata sobre el envío directo de la telemetría a los diferentes recursos para los sellos de desarrollo, prueba y producción."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: f51fa4639aaa60686cc349683713c6e5f9732bb9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="9938b-103">Separación de la telemetría de desarrollo, prueba y producción</span><span class="sxs-lookup"><span data-stu-id="9938b-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="9938b-104">Cuando esté desarrollando la próxima versión de una aplicación web, no querrá mezclar la telemetría de [Application Insights](app-insights-overview.md) de la nueva versión con la que ya se ha publicado.</span><span class="sxs-lookup"><span data-stu-id="9938b-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="9938b-105">Para evitar confusiones, envíe la telemetría de las distintas fases de desarrollo para separar los recursos de Application Insights con claves de instrumentación independientes (iKey).</span><span class="sxs-lookup"><span data-stu-id="9938b-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="9938b-106">Para que sea más fácil cambiar la clave de instrumentación cuando pase una versión de una fase a otro, puede ser útil establecer la clave iKey en el código en lugar de en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="9938b-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="9938b-107">(Si el sistema es un servicio en la nube de Azure, hay [otra forma de configurar claves separadas](app-insights-cloudservices.md)).</span><span class="sxs-lookup"><span data-stu-id="9938b-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="9938b-108">Acerca de los recursos y las claves de instrumentación</span><span class="sxs-lookup"><span data-stu-id="9938b-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="9938b-109">Al configurar la supervisión de Application Insights para su aplicación web, se crea un *recurso* de Application Insights en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9938b-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="9938b-110">Abra este recurso en Azure Portal con el fin de ver y analizar la telemetría recopilada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9938b-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="9938b-111">Cada recurso se identifica con una *clave de instrumentación* (iKey).</span><span class="sxs-lookup"><span data-stu-id="9938b-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="9938b-112">Cuando se instala el paquete de Application Insights para supervisar la aplicación, configúrelo con la clave de instrumentación para que sepa dónde enviar la telemetría.</span><span class="sxs-lookup"><span data-stu-id="9938b-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="9938b-113">Normalmente, decidirá usar recursos independientes o un recurso compartido único en escenarios diferentes:</span><span class="sxs-lookup"><span data-stu-id="9938b-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="9938b-114">Aplicaciones independientes y diferentes: use un recurso y una clave iKey independientes para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="9938b-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="9938b-115">Varios componentes o roles de una sola aplicación empresarial: use un [único recurso compartido](app-insights-monitor-multi-role-apps.md) para todas las aplicaciones de componentes.</span><span class="sxs-lookup"><span data-stu-id="9938b-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="9938b-116">La telemetría puede filtrarse o segmentarse por la propiedad cloud_RoleName.</span><span class="sxs-lookup"><span data-stu-id="9938b-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="9938b-117">Desarrollo, prueba y publicación: use un recurso y una clave iKey independientes para las versiones del sistema en "sellos" o fase de producción.</span><span class="sxs-lookup"><span data-stu-id="9938b-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="9938b-118">Pruebas A/B: use un único recurso.</span><span class="sxs-lookup"><span data-stu-id="9938b-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="9938b-119">Cree un elemento TelemetryInitializer para agregar una propiedad a la telemetría que identifica las variantes.</span><span class="sxs-lookup"><span data-stu-id="9938b-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <span data-ttu-id="9938b-120"><a name="dynamic-ikey"></a> Copia de la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="9938b-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="9938b-121">Para que sea más fácil cambiar la clave iKey cuando el código se mueva entre las fases de producción, establézcala en el código en lugar de en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="9938b-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="9938b-122">Establezca la clave en un método de inicialización, como global.aspx.cs en un servicio de ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="9938b-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="9938b-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="9938b-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="9938b-124">En este ejemplo, las ikeys para los distintos recursos se colocan en diferentes versiones del archivo de configuración web.</span><span class="sxs-lookup"><span data-stu-id="9938b-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="9938b-125">Si cambia el archivo de configuración web (algo que se puede hacer como parte del script de lanzamiento), se intercambiará el recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="9938b-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="9938b-126">Páginas web</span><span class="sxs-lookup"><span data-stu-id="9938b-126">Web pages</span></span>
<span data-ttu-id="9938b-127">La iKey también se usa en las páginas web de su aplicación, en el [script que obtuvo desde la hoja Inicio rápido](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="9938b-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="9938b-128">En vez de codificarla literalmente en el script, genérela desde el estado del servidor.</span><span class="sxs-lookup"><span data-stu-id="9938b-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="9938b-129">Por ejemplo, en una aplicación ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="9938b-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="9938b-130">*JavaScript en Razor*</span><span class="sxs-lookup"><span data-stu-id="9938b-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="9938b-131">Creación de recurso de Application Insights adicionales</span><span class="sxs-lookup"><span data-stu-id="9938b-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="9938b-132">Con el fin de separar la telemetría para los diferentes componentes de la aplicación, o para diferentes sellos (desarrollo, prueba y producción) del mismo componente, tendrá que crear un recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9938b-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="9938b-133">En el [portal.azure.com](https://portal.azure.com), agregue un recurso de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="9938b-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Haga clic en Nuevo, Application Insights.](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="9938b-135">**tipo de aplicación** afecta a lo que ve en la hoja de información general y las propiedades disponibles en el [explorador de métricas](app-insights-metrics-explorer.md)de Azure.</span><span class="sxs-lookup"><span data-stu-id="9938b-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="9938b-136">Si no ve el tipo de aplicación, elija uno de los tipos web para páginas web.</span><span class="sxs-lookup"><span data-stu-id="9938b-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="9938b-137">**grupo de recursos** resulta práctico para administrar propiedades como el  como el [control de acceso](app-insights-resources-roles-access-control.md)de Azure.</span><span class="sxs-lookup"><span data-stu-id="9938b-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="9938b-138">Puede usar grupos de recursos independientes para desarrollo, prueba y producción.</span><span class="sxs-lookup"><span data-stu-id="9938b-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="9938b-139">**suscripción** es su cuenta de pago de Azure.</span><span class="sxs-lookup"><span data-stu-id="9938b-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="9938b-140">**ubicación** es donde se guardan los datos.</span><span class="sxs-lookup"><span data-stu-id="9938b-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="9938b-141">Actualmente no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="9938b-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="9938b-142">**Agregar al panel** coloca un icono de acceso rápido al recurso en la página principal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9938b-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="9938b-143">El recurso tarda unos segundos en crearse.</span><span class="sxs-lookup"><span data-stu-id="9938b-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="9938b-144">Verá una alerta cuando esté listo.</span><span class="sxs-lookup"><span data-stu-id="9938b-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="9938b-145">(Puede escribir un [script de PowerShell](app-insights-powershell-script-create-resource.md) para crear un recurso  automáticamente.)</span><span class="sxs-lookup"><span data-stu-id="9938b-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="9938b-146">Obtención de la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="9938b-146">Getting the instrumentation key</span></span>
<span data-ttu-id="9938b-147">La clave de instrumentación identifica al recurso que ha creado.</span><span class="sxs-lookup"><span data-stu-id="9938b-147">The instrumentation key identifies the resource that you created.</span></span> 

![Haga clic en Essentials y elija la clave de instrumentación, CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="9938b-149">Necesita las claves de instrumentación de todos los recursos a los que la aplicación enviará datos.</span><span class="sxs-lookup"><span data-stu-id="9938b-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="9938b-150">Filtrado por número de compilación</span><span class="sxs-lookup"><span data-stu-id="9938b-150">Filter on build number</span></span>
<span data-ttu-id="9938b-151">Cuando se publica una nueva versión de la aplicación, querrá poder separar la telemetría en las diferentes versiones.</span><span class="sxs-lookup"><span data-stu-id="9938b-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="9938b-152">Puede establecer la propiedad de versión de la aplicación para filtrar los resultados de la [búsqueda](app-insights-diagnostic-search.md) y del [explorador de métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9938b-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtrado según una propiedad](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="9938b-154">Hay diferentes métodos de establecer la propiedad de versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9938b-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="9938b-155">Establezca directamente:</span><span class="sxs-lookup"><span data-stu-id="9938b-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="9938b-156">Ajuste esa línea en un [inicializador de telemetría](app-insights-api-custom-events-metrics.md#defaults) para asegurarse de que todas las instancias de TelemetryClient se establecen de forma coherente.</span><span class="sxs-lookup"><span data-stu-id="9938b-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="9938b-157">[ASP.NET] Establezca la versión en `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="9938b-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="9938b-158">El módulo web recogerá la versión del nodo BuildLabel.</span><span class="sxs-lookup"><span data-stu-id="9938b-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="9938b-159">Incluya este archivo en el proyecto y recuerde que establecer la propiedad Copiar siempre en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="9938b-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="9938b-160">[ASP.NET] Genere BuildInfo.config automáticamente en MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9938b-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="9938b-161">Para ello, agregue unas líneas a su archivo `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="9938b-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="9938b-162">Esto genera un archivo denominado *suNombreProyecto*.BuildInfo.config. El proceso de publicación cambia su nombre a BuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="9938b-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="9938b-163">La etiqueta de compilación contiene un marcador de posición (AutoGen_...) al compilar con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9938b-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="9938b-164">Pero cuando se crea con MSBuild, se rellena con el número de versión correcto.</span><span class="sxs-lookup"><span data-stu-id="9938b-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="9938b-165">Para permitir que MSBuild genere números de versión, establezca la versión como `1.0.*` en AssemblyReference.cs.</span><span class="sxs-lookup"><span data-stu-id="9938b-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="9938b-166">Versión y seguimiento de versiones</span><span class="sxs-lookup"><span data-stu-id="9938b-166">Version and release tracking</span></span>
<span data-ttu-id="9938b-167">Para realizar el seguimiento de la versión de la aplicación, asegúrese de que `buildinfo.config` lo genera el proceso de Microsoft Build Engine.</span><span class="sxs-lookup"><span data-stu-id="9938b-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="9938b-168">En su archivo .csproj, agregue:</span><span class="sxs-lookup"><span data-stu-id="9938b-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="9938b-169">Cuando tenga la información de la compilación, el módulo web de Application Insights agregará automáticamente la **versión de la aplicación** como una propiedad a cada elemento de telemetría.</span><span class="sxs-lookup"><span data-stu-id="9938b-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="9938b-170">Esto le permite filtrar por versión al realizar [búsquedas de diagnósticos](app-insights-diagnostic-search.md) o al [explorar métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9938b-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="9938b-171">Sin embargo, tenga en cuenta que el número de versión de la compilación solo lo genera Microsoft Build Engine, no la compilación de desarrollador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9938b-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="9938b-172">Anotaciones de la versión</span><span class="sxs-lookup"><span data-stu-id="9938b-172">Release annotations</span></span>
<span data-ttu-id="9938b-173">Si usa Visual Studio Team Services, puede [obtener un marcador de anotación](app-insights-annotations.md) agregado a los gráficos, siempre que publique una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="9938b-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="9938b-174">La siguiente imagen muestra cómo aparece este marcador.</span><span class="sxs-lookup"><span data-stu-id="9938b-174">The following image shows how this marker appears.</span></span>

![Captura de pantalla de la anotación de la versión de ejemplo en un gráfico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="9938b-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9938b-176">Next steps</span></span>

* [<span data-ttu-id="9938b-177">Recursos compartidos para varios roles</span><span class="sxs-lookup"><span data-stu-id="9938b-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="9938b-178">Creación de un inicializador de telemetría para distinguir variantes A/B</span><span class="sxs-lookup"><span data-stu-id="9938b-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
