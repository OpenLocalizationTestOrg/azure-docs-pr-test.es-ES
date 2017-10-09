---
title: "las aplicaciones de Docker de aaaMonitor de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Excepciones, eventos y contadores de rendimiento de docker se pueden mostrar en la información de la aplicación, junto con la telemetría de Hola desde aplicaciones de hello en contenedores."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="d8910-103">Supervisar aplicaciones Docker en Application Insights</span><span class="sxs-lookup"><span data-stu-id="d8910-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="d8910-104">Los eventos de ciclo de vida y los contadores de rendimiento de los contenedores [Docker](https://www.docker.com/) pueden mostrarse en gráficos en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d8910-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="d8910-105">Instalar hello [Application Insights](app-insights-overview.md) imagen en un contenedor en el host y mostrará los contadores de rendimiento para el host de hello, como así como para Hola otras imágenes.</span><span class="sxs-lookup"><span data-stu-id="d8910-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="d8910-106">Con Docker, distribuye sus aplicaciones en contenedores ligeros junto con todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="d8910-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="d8910-107">Estos contenedores se ejecutan en cualquier equipo host que ejecute un motor Docker.</span><span class="sxs-lookup"><span data-stu-id="d8910-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="d8910-108">Cuando ejecute hello [imagen de Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) en el host Docker, obtener estas ventajas:</span><span class="sxs-lookup"><span data-stu-id="d8910-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="d8910-109">Ciclo de vida telemetría acerca de todos los contenedores de Hola que se ejecutan en el host de hello - iniciar, detener y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="d8910-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="d8910-110">Contadores de rendimiento para todos los contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8910-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="d8910-111">CPU, memoria, uso de red y mucho más.</span><span class="sxs-lookup"><span data-stu-id="d8910-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="d8910-112">Si se [instalado Application Insights SDK para Java](app-insights-java-live.md) en hello aplicaciones que se ejecutan en contenedores de hello, todos los telemetría Hola de esas aplicaciones tendrán propiedades adicionales que identifica el contenedor de Hola y el equipo host.</span><span class="sxs-lookup"><span data-stu-id="d8910-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="d8910-113">De esta forma, si tiene, por ejemplo, instancias de una aplicación que se ejecuta en más de un host, podrá filtrar fácilmente los datos de telemetría de la aplicación en función del host.</span><span class="sxs-lookup"><span data-stu-id="d8910-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![ejemplo](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="d8910-115">Configurar el recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d8910-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="d8910-116">Iniciar sesión en [portal de Microsoft Azure](https://azure.com) y abra el recurso de Application Insights de hello para la aplicación; o [crear una nueva](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d8910-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="d8910-117">*¿Qué recurso debería usar?*</span><span class="sxs-lookup"><span data-stu-id="d8910-117">*Which resource should I use?*</span></span> <span data-ttu-id="d8910-118">Si se desarrollaron hello las aplicaciones que se ejecutan en el host por otra persona, deberá demasiado[crear un nuevo recurso de Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d8910-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="d8910-119">Esto es donde ver y analizar la telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8910-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="d8910-120">(Seleccione "General" para el tipo de aplicación Hola).</span><span class="sxs-lookup"><span data-stu-id="d8910-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="d8910-121">Pero si es desarrollador de Hola de las aplicaciones de hello, a continuación, esperamos [agrega Application Insights SDK](app-insights-java-live.md) tooeach de ellos.</span><span class="sxs-lookup"><span data-stu-id="d8910-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="d8910-122">Si son todos los componentes realmente de una aplicación de negocio individual, a continuación, puede configurar todas ellas toosend telemetría tooone recurso y usará ese mismo recursos toodisplay hello Docker ciclo de vida de datos y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d8910-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="d8910-123">En un tercer escenario es que se ha desarrollado la mayoría de las aplicaciones de hello, pero que usa recursos separados toodisplay su telemetría.</span><span class="sxs-lookup"><span data-stu-id="d8910-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="d8910-124">En ese caso, probablemente también desee toocreate recursos independientes para hello datos de Docker.</span><span class="sxs-lookup"><span data-stu-id="d8910-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="d8910-125">Agregar icono de Docker de hello: elija **agregar icono**, arrastre el icono de Docker de Hola de galería de Hola y, a continuación, haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="d8910-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![ejemplo](./media/app-insights-docker/03.png)
3. <span data-ttu-id="d8910-127">Haga clic en hello **Essentials** desplegable y copie Hola clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="d8910-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="d8910-128">Utilice este hello tootell SDK donde toosend su telemetría.</span><span class="sxs-lookup"><span data-stu-id="d8910-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![ejemplo](./media/app-insights-docker/02-props.png)

<span data-ttu-id="d8910-130">Mantener esa ventana del explorador práctica, tal y como le vuelva tooit pronto toolook en la telemetría.</span><span class="sxs-lookup"><span data-stu-id="d8910-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="d8910-131">Ejecutar el monitor de Application Insights de hello en el host</span><span class="sxs-lookup"><span data-stu-id="d8910-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="d8910-132">Ahora que tienes en algún lugar telemetría de hello toodisplay, puede configurar aplicación en contenedores de hello que recopilará y enviará.</span><span class="sxs-lookup"><span data-stu-id="d8910-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="d8910-133">Conectar el host de Docker de tooyour.</span><span class="sxs-lookup"><span data-stu-id="d8910-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="d8910-134">Edite la clave de instrumentación de este comando y después ejecútelo:</span><span class="sxs-lookup"><span data-stu-id="d8910-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="d8910-135">Solo es necesaria una imagen de Application Insights por cada host de Docker.</span><span class="sxs-lookup"><span data-stu-id="d8910-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="d8910-136">Si la aplicación se implementa en varios hosts de Docker, a continuación, repita el comando de hello en todos los hosts.</span><span class="sxs-lookup"><span data-stu-id="d8910-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="d8910-137">Actualización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d8910-137">Update your app</span></span>
<span data-ttu-id="d8910-138">Si la aplicación se ha instrumentado con hello [Application Insights SDK para Java](app-insights-java-get-started.md), agregar Hola siguen en archivo de ApplicationInsights.xml hello en el proyecto, bajo hello `<TelemetryInitializers>` elemento:</span><span class="sxs-lookup"><span data-stu-id="d8910-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="d8910-139">Esto agrega información de Docker como contenedor y el host identificador tooevery telemetría item enviado desde su aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8910-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="d8910-140">Visualización de la telemetría</span><span class="sxs-lookup"><span data-stu-id="d8910-140">View your telemetry</span></span>
<span data-ttu-id="d8910-141">Volver atrás tooyour recursos de Application Insights en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8910-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="d8910-142">Haga clic en icono de Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="d8910-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="d8910-143">En breve, verá los datos que llegan desde la aplicación de Docker de hello, especialmente si tiene otros contenedores que se ejecutan en el motor de Docker.</span><span class="sxs-lookup"><span data-stu-id="d8910-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="d8910-144">Estas son algunas de las vistas de Hola que puedas.</span><span class="sxs-lookup"><span data-stu-id="d8910-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="d8910-145">Contadores de rendimiento por host, actividad por imagen</span><span class="sxs-lookup"><span data-stu-id="d8910-145">Perf counters by host, activity by image</span></span>
![ejemplo](./media/app-insights-docker/10.png)

![ejemplo](./media/app-insights-docker/11.png)

<span data-ttu-id="d8910-148">Haga clic en cualquier host o imagen para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="d8910-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="d8910-149">vista de hello toocustomize, haga clic en cualquier gráfico, el encabezado de cuadrícula de Hola o utilizar Agregar gráfico.</span><span class="sxs-lookup"><span data-stu-id="d8910-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="d8910-150">[Más información sobre el explorador de métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="d8910-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="d8910-151">Eventos de contenedor Docker</span><span class="sxs-lookup"><span data-stu-id="d8910-151">Docker container events</span></span>
![ejemplo](./media/app-insights-docker/13.png)

<span data-ttu-id="d8910-153">tooinvestigate eventos individuales, haga clic en [búsqueda](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="d8910-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="d8910-154">Buscar y filtrar los eventos de hello toofind que desee.</span><span class="sxs-lookup"><span data-stu-id="d8910-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="d8910-155">Haga clic en cualquier evento tooget más detalle.</span><span class="sxs-lookup"><span data-stu-id="d8910-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="d8910-156">Excepciones por el nombre del contenedor</span><span class="sxs-lookup"><span data-stu-id="d8910-156">Exceptions by container name</span></span>
![ejemplo](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="d8910-158">El contexto del docker agrega tooapp telemetría</span><span class="sxs-lookup"><span data-stu-id="d8910-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="d8910-159">Telemetría de solicitud enviado desde la aplicación hello instrumentado con SDK AI, enriquecido con contexto de Docker:</span><span class="sxs-lookup"><span data-stu-id="d8910-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![ejemplo](./media/app-insights-docker/16.png)

<span data-ttu-id="d8910-161">Contadores de rendimiento de tiempo de procesador y memoria disponible, enriquecidos y agrupados según el nombre del contenedor de Docker:</span><span class="sxs-lookup"><span data-stu-id="d8910-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![ejemplo](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="d8910-163">Preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="d8910-163">Q & A</span></span>
<span data-ttu-id="d8910-164">*¿Qué me da Application Insights que no me dé Docker?*</span><span class="sxs-lookup"><span data-stu-id="d8910-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="d8910-165">Desglose detallado de los contadores de rendimiento por contenedor e imagen.</span><span class="sxs-lookup"><span data-stu-id="d8910-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="d8910-166">Integración de datos de contenedores y aplicaciones en un panel.</span><span class="sxs-lookup"><span data-stu-id="d8910-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="d8910-167">[Exportar telemetría](app-insights-export-telemetry.md) para otra base de datos de analysis tooa, Power BI u otro panel.</span><span class="sxs-lookup"><span data-stu-id="d8910-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="d8910-168">*¿Cómo consigo telemetría de la propia aplicación Hola?*</span><span class="sxs-lookup"><span data-stu-id="d8910-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="d8910-169">Instalar Hola Application Insights SDK en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d8910-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="d8910-170">Más información sobre: [aplicaciones web de Java](app-insights-java-get-started.md) y [aplicaciones web de Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="d8910-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="d8910-171">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d8910-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="d8910-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8910-172">Next steps</span></span>

* [<span data-ttu-id="d8910-173">Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="d8910-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="d8910-174">Application Insights para Node.js</span><span class="sxs-lookup"><span data-stu-id="d8910-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="d8910-175">Application Insights para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d8910-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
