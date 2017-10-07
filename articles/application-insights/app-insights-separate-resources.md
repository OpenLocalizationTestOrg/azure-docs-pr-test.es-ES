---
title: "telemetría aaaSeparating desde el desarrollo, prueba y suelte en Azure Application Insights | Documentos de Microsoft"
description: "Recursos de toodifferent de telemetría directa para que las marcas de desarrollo, prueba y producción."
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
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="e8ff5-103">Separación de la telemetría de desarrollo, prueba y producción</span><span class="sxs-lookup"><span data-stu-id="e8ff5-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="e8ff5-104">Cuando está desarrollando la próxima versión de Hola de una aplicación web, no desea toomix seguridad hello [Application Insights](app-insights-overview.md) telemetría de la nueva versión de hello y la versión de Hola ya publicado.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="e8ff5-105">tooavoid confusión, envío Hola telemetría de desarrollo diferentes fases tooseparate recursos de Application Insights, con claves de instrumentación independiente (ikeys).</span><span class="sxs-lookup"><span data-stu-id="e8ff5-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="e8ff5-106">toomake sea más fácil toochange Hola Instrumental clave como una versión se mueve de una fase tooanother, puede ser útil tooset Hola ikey en el código en lugar de en el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="e8ff5-107">(Si el sistema es un servicio en la nube de Azure, hay [otra forma de configurar claves separadas](app-insights-cloudservices.md)).</span><span class="sxs-lookup"><span data-stu-id="e8ff5-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="e8ff5-108">Acerca de los recursos y las claves de instrumentación</span><span class="sxs-lookup"><span data-stu-id="e8ff5-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="e8ff5-109">Al configurar la supervisión de Application Insights para su aplicación web, se crea un *recurso* de Application Insights en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="e8ff5-110">Abrir este recurso en el portal de Azure en orden toosee hello y analizar la telemetría de hello recopilada desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="e8ff5-111">recursos de Hola se identifican mediante un *clave de instrumentación* (ikey).</span><span class="sxs-lookup"><span data-stu-id="e8ff5-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="e8ff5-112">Cuando se instala Hola Application Insights empaquetarla toomonitor, configurarlo con clave de instrumentación de hello, para que sepa dónde toosend Hola telemetría.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="e8ff5-113">Normalmente elija recursos independientes toouse o un único recurso compartido en escenarios diferentes:</span><span class="sxs-lookup"><span data-stu-id="e8ff5-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="e8ff5-114">Aplicaciones independientes y diferentes: use un recurso y una clave iKey independientes para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="e8ff5-115">Usar varios componentes o funciones de una sola aplicación comercial - un [único recurso compartido](app-insights-monitor-multi-role-apps.md) para todas las aplicaciones de componente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="e8ff5-116">Puede filtrar o segmentada por propiedad de hello cloud_RoleName telemetría.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="e8ff5-117">Desarrollo y prueba, versión, usan un recurso independiente y ikey de versiones del sistema de hello en 'marca' o una fase de producción.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="e8ff5-118">Pruebas A/B: use un único recurso.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="e8ff5-119">Cree una tooadd TelemetryInitializer una telemetría de toohello de propiedad que identifica las variantes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="e8ff5-120"><a name="dynamic-ikey"></a> Copia de la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="e8ff5-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="e8ff5-121">toomake, facilitando la toochange Hola ikey como código de hello se mueve entre fases de producción, establézcala en el código en lugar de en el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="e8ff5-122">Establezca la clave de hello en un método de inicialización, como global.aspx.cs en un servicio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="e8ff5-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="e8ff5-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="e8ff5-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="e8ff5-124">En este ejemplo, hello ikeys para los distintos recursos de Hola se colocan en las diferentes versiones del archivo de configuración web de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="e8ff5-125">Archivo de configuración de web de hello intercambiando - lo que puede hacer como parte del script de la versión de Hola - intercambiará recurso de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="e8ff5-126">Páginas web</span><span class="sxs-lookup"><span data-stu-id="e8ff5-126">Web pages</span></span>
<span data-ttu-id="e8ff5-127">Hola iKey también se utiliza en páginas web de la aplicación, en hello [secuencia de comandos que obtuvo en la hoja de inicio rápido de hello](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="e8ff5-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="e8ff5-128">En lugar de codificar, literalmente en el script de Hola, generar desde el estado del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="e8ff5-129">Por ejemplo, en una aplicación ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="e8ff5-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="e8ff5-130">*JavaScript en Razor*</span><span class="sxs-lookup"><span data-stu-id="e8ff5-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="e8ff5-131">Creación de recurso de Application Insights adicionales</span><span class="sxs-lookup"><span data-stu-id="e8ff5-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="e8ff5-132">tooseparate telemetría para los componentes de aplicación diferente o para marcas de tiempo diferentes (desarrollo/prueba/producción) de hello mismo componente, entonces tendrá toocreate un nuevo recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="e8ff5-133">Hola [portal.azure.com](https://portal.azure.com), agregar un recurso de información de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="e8ff5-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Haga clic en Nuevo, Application Insights.](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="e8ff5-135">**Tipo de aplicación** afecta a lo que ve en la hoja de información general de Hola y Hola propiedades [explorer métrica](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="e8ff5-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="e8ff5-136">Si no ve el tipo de aplicación, elija uno de los tipos de hello web para las páginas web.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="e8ff5-137">**grupo de recursos** resulta práctico para administrar propiedades como el  como el [control de acceso](app-insights-resources-roles-access-control.md)de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="e8ff5-138">Puede usar grupos de recursos independientes para desarrollo, prueba y producción.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="e8ff5-139">**suscripción** es su cuenta de pago de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="e8ff5-140">**ubicación** es donde se guardan los datos.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="e8ff5-141">Actualmente no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="e8ff5-142">**Agregar toodashboard** coloca un icono de acceso rápido para el recurso en la página principal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="e8ff5-143">Crear recursos de hello tarda unos segundos.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="e8ff5-144">Verá una alerta cuando esté listo.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="e8ff5-145">(Puede escribir una [script de PowerShell](app-insights-powershell-script-create-resource.md) toocreate un recurso automáticamente.)</span><span class="sxs-lookup"><span data-stu-id="e8ff5-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="e8ff5-146">Obtener clave de instrumentación de Hola</span><span class="sxs-lookup"><span data-stu-id="e8ff5-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="e8ff5-147">clave de instrumentación de Hello identifica recursos de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![Haga clic en Essentials, haga clic en hello clave de instrumentación, CTRL + c.](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="e8ff5-149">Se necesitan las claves de instrumentación de Hola de todos los toowhich de recursos de Hola la aplicación enviará los datos.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="e8ff5-150">Filtrado por número de compilación</span><span class="sxs-lookup"><span data-stu-id="e8ff5-150">Filter on build number</span></span>
<span data-ttu-id="e8ff5-151">Cuando se publica una nueva versión de la aplicación, le interesará telemetría de hello tooseparate capaz de toobe desde diferentes compilaciones.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="e8ff5-152">Puede establecer la propiedad de versión de la aplicación hello para que pueda filtrar [búsqueda](app-insights-diagnostic-search.md) y [explorer métrica](app-insights-metrics-explorer.md) resultados.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtrado según una propiedad](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="e8ff5-154">Existen varios métodos diferentes de establecer la propiedad de versión de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="e8ff5-155">Establezca directamente:</span><span class="sxs-lookup"><span data-stu-id="e8ff5-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="e8ff5-156">Ajustar esa línea en un [inicializador de telemetría](app-insights-api-custom-events-metrics.md#defaults) tooensure que todas las instancias de TelemetryClient se establecen de forma coherente.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="e8ff5-157">[ASP.NET] Establecer versión de hello en `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="e8ff5-158">módulo de Hello web recogerá versión Hola de nodo de BuildLabel Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="e8ff5-159">Incluir este archivo en el proyecto y recordar tooset Hola copiar siempre propiedad el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

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
* <span data-ttu-id="e8ff5-160">[ASP.NET] Genere BuildInfo.config automáticamente en MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="e8ff5-161">toodo, agregar algunas de las líneas de tooyour `.csproj` archivo:</span><span class="sxs-lookup"><span data-stu-id="e8ff5-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="e8ff5-162">Esto genera un archivo denominado *NombreDelProyecto*. Hola BuildInfo.config. proceso de publicación cambia su nombre tooBuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="e8ff5-163">etiqueta de compilación de Hello contiene un marcador de posición (AutoGen_...) al compilar con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="e8ff5-164">Pero cuando se compila con MSBuild, se rellena con el número de versión correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="e8ff5-165">números de versión de MSBuild toogenerate tooallow, versión del juego de hello como `1.0.*` en AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="e8ff5-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="e8ff5-166">Versión y seguimiento de versiones</span><span class="sxs-lookup"><span data-stu-id="e8ff5-166">Version and release tracking</span></span>
<span data-ttu-id="e8ff5-167">versión de la aplicación hello tootrack, asegúrese de que `buildinfo.config` generado por el proceso de Microsoft Build Engine.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="e8ff5-168">En su archivo .csproj, agregue:</span><span class="sxs-lookup"><span data-stu-id="e8ff5-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="e8ff5-169">Cuando tiene información de compilación de hello, agrega automáticamente el módulo de web Application Insights hello **versión de la aplicación** como un elemento de propiedad tooevery de telemetría.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="e8ff5-170">Que permite toofilter versión al realizar [búsquedas diagnóstico](app-insights-diagnostic-search.md), o cuando se [explorar métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="e8ff5-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="e8ff5-171">Sin embargo, observe que el número de versión de compilación de Hola se genera solo por hello Microsoft Build Engine, no por el desarrollador de Hola se crean en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="e8ff5-172">Anotaciones de la versión</span><span class="sxs-lookup"><span data-stu-id="e8ff5-172">Release annotations</span></span>
<span data-ttu-id="e8ff5-173">Si usa Visual Studio Team Services, puede [obtener un marcador de anotación](app-insights-annotations.md) agregan gráficos tooyour cada vez que publica una versión nueva.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="e8ff5-174">Hola siguiente imagen muestra la apariencia de este marcador.</span><span class="sxs-lookup"><span data-stu-id="e8ff5-174">hello following image shows how this marker appears.</span></span>

![Captura de pantalla de la anotación de la versión de ejemplo en un gráfico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="e8ff5-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e8ff5-176">Next steps</span></span>

* [<span data-ttu-id="e8ff5-177">Recursos compartidos para varios roles</span><span class="sxs-lookup"><span data-stu-id="e8ff5-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="e8ff5-178">Crear un toodistinguish de inicializador de telemetría A | Variantes de B</span><span class="sxs-lookup"><span data-stu-id="e8ff5-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
