---
title: "Supervisión de aplicaciones de Docker en Azure Application Insights | Microsoft Docs"
description: "En Application Insights, se pueden mostrar los contadores de rendimiento, los eventos y las excepciones de Docker, además de la telemetría de las aplicaciones en contenedor."
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
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="b8a1d-103">Supervisar aplicaciones Docker en Application Insights</span><span class="sxs-lookup"><span data-stu-id="b8a1d-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="b8a1d-104">Los eventos de ciclo de vida y los contadores de rendimiento de los contenedores [Docker](https://www.docker.com/) pueden mostrarse en gráficos en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="b8a1d-105">Instale la imagen de [Application Insights](app-insights-overview.md) en un contenedor del host y se mostrarán los contadores de rendimiento del host, así como de las demás imágenes.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="b8a1d-106">Con Docker, distribuye sus aplicaciones en contenedores ligeros junto con todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="b8a1d-107">Estos contenedores se ejecutan en cualquier equipo host que ejecute un motor Docker.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="b8a1d-108">Al ejecutar la [imagen de Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) en el host Docker, obtendrá estas ventajas:</span><span class="sxs-lookup"><span data-stu-id="b8a1d-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="b8a1d-109">Telemetría del ciclo de vida sobre todos los contenedores que se ejecutan en el host: start, stop, etc.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="b8a1d-110">Contadores de rendimiento de todos los contenedores.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-110">Performance counters for all the containers.</span></span> <span data-ttu-id="b8a1d-111">CPU, memoria, uso de red y mucho más.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="b8a1d-112">Si [instaló el SDK de Application Insights](app-insights-java-live.md) en las aplicaciones que se ejecutan en los contenedores, toda la telemetría de dichas aplicaciones tendrán propiedades adicionales que identifiquen el contenedor y el equipo host.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="b8a1d-113">De esta forma, si tiene, por ejemplo, instancias de una aplicación que se ejecuta en más de un host, podrá filtrar fácilmente los datos de telemetría de la aplicación en función del host.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![ejemplo](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="b8a1d-115">Configurar el recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="b8a1d-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="b8a1d-116">Inicie sesión en [Microsoft Azure Portal](https://azure.com) y abra el recurso de Application Insights de la aplicación; o [cree uno nuevo](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b8a1d-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="b8a1d-117">*¿Qué recurso debería usar?*</span><span class="sxs-lookup"><span data-stu-id="b8a1d-117">*Which resource should I use?*</span></span> <span data-ttu-id="b8a1d-118">Si las aplicaciones que se ejecutan en el host las desarrolló otra persona, deberá [crear un nuevo recurso de Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b8a1d-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="b8a1d-119">Es el sitio donde verá y analizará los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="b8a1d-120">Seleccione General para el tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="b8a1d-121">Pero si usted es el desarrollador de las aplicaciones, esperamos que [haya agregado el SDK de Application Insights](app-insights-java-live.md) a cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="b8a1d-122">Si todos son realmente componentes de una aplicación empresarial única, puede configurarlas todas para que envíen telemetría a un recurso y usará ese mismo recurso para mostrar los datos de rendimiento y de ciclo de vida de Docker.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="b8a1d-123">Un tercer escenario es que haya desarrollado la mayoría de las aplicaciones, pero use recursos independientes para mostrar sus datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="b8a1d-124">En ese caso, probablemente también querrá crear un recurso independiente para los datos de Docker.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="b8a1d-125">Agregue el icono de Docker; para ello, elija **Agregar icono**, arrastre el icono de Docker desde la galería y luego haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![ejemplo](./media/app-insights-docker/03.png)
3. <span data-ttu-id="b8a1d-127">Haga clic en la lista desplegable **Essentials** y copie la clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="b8a1d-128">Se usará para indicar al SDK dónde puede enviar sus datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![ejemplo](./media/app-insights-docker/02-props.png)

<span data-ttu-id="b8a1d-130">Tenga a mano la ventana del explorador, volverá a ella pronto para examinar los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="b8a1d-131">Ejecutar la supervisión de Application Insights en el host</span><span class="sxs-lookup"><span data-stu-id="b8a1d-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="b8a1d-132">Ahora que tiene un lugar donde mostrar los datos de telemetría, puede configurar la aplicación del contenedor que los recopilará y enviará.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="b8a1d-133">Conéctese al host Docker.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="b8a1d-134">Edite la clave de instrumentación de este comando y después ejecútelo:</span><span class="sxs-lookup"><span data-stu-id="b8a1d-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="b8a1d-135">Solo es necesaria una imagen de Application Insights por cada host de Docker.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="b8a1d-136">Si la aplicación se implementa en varios hosts de Docker, repita el comando en todos los hosts.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="b8a1d-137">Actualización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b8a1d-137">Update your app</span></span>
<span data-ttu-id="b8a1d-138">Si la aplicación se instrumenta con el [SDK de Application Insights para Java`<TelemetryInitializers>`, agregue la siguiente línea en el archivo ApplicationInsights.xml del proyecto, en el elemento ](app-insights-java-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="b8a1d-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="b8a1d-139">Esto agrega información de Docker como el contenedor y el identificador de host a cada uno de los elementos de telemetría que se envían desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="b8a1d-140">Visualización de la telemetría</span><span class="sxs-lookup"><span data-stu-id="b8a1d-140">View your telemetry</span></span>
<span data-ttu-id="b8a1d-141">Vuelva al recurso de Application Insights en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="b8a1d-142">Haga clic en el icono de Docker.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-142">Click through the Docker tile.</span></span>

<span data-ttu-id="b8a1d-143">Pronto verá que llegan datos desde la aplicación de Docker, especialmente si tiene otros contenedores que se ejecutan en el motor de Docker.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="b8a1d-144">Estas son algunas de las vistas que puede obtener.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="b8a1d-145">Contadores de rendimiento por host, actividad por imagen</span><span class="sxs-lookup"><span data-stu-id="b8a1d-145">Perf counters by host, activity by image</span></span>
![ejemplo](./media/app-insights-docker/10.png)

![ejemplo](./media/app-insights-docker/11.png)

<span data-ttu-id="b8a1d-148">Haga clic en cualquier host o imagen para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="b8a1d-149">Para personalizar la vista, haga clic en cualquiera de los gráficos o en el encabezado de cuadrícula, o bien use Agregar gráfico.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="b8a1d-150">[Más información sobre el explorador de métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="b8a1d-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="b8a1d-151">Eventos de contenedor Docker</span><span class="sxs-lookup"><span data-stu-id="b8a1d-151">Docker container events</span></span>
![ejemplo](./media/app-insights-docker/13.png)

<span data-ttu-id="b8a1d-153">Para investigar eventos individuales, haga clic en [Buscar](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b8a1d-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="b8a1d-154">Busque y filtre para encontrar los eventos deseados.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="b8a1d-155">Haga clic en cualquier evento para más detalles.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="b8a1d-156">Excepciones por el nombre del contenedor</span><span class="sxs-lookup"><span data-stu-id="b8a1d-156">Exceptions by container name</span></span>
![ejemplo](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="b8a1d-158">Contexto de Docker agregado a los datos de telemetría de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b8a1d-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="b8a1d-159">Solicite datos de telemetría enviados desde la aplicación instrumentada con el SDK de AI, enriquecidos con el contexto de Docker:</span><span class="sxs-lookup"><span data-stu-id="b8a1d-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![ejemplo](./media/app-insights-docker/16.png)

<span data-ttu-id="b8a1d-161">Contadores de rendimiento de tiempo de procesador y memoria disponible, enriquecidos y agrupados según el nombre del contenedor de Docker:</span><span class="sxs-lookup"><span data-stu-id="b8a1d-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![ejemplo](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="b8a1d-163">Preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="b8a1d-163">Q & A</span></span>
<span data-ttu-id="b8a1d-164">*¿Qué me da Application Insights que no me dé Docker?*</span><span class="sxs-lookup"><span data-stu-id="b8a1d-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="b8a1d-165">Desglose detallado de los contadores de rendimiento por contenedor e imagen.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="b8a1d-166">Integración de datos de contenedores y aplicaciones en un panel.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="b8a1d-167">[Exportación de la telemetría](app-insights-export-telemetry.md) , para su análisis posterior en una base de datos, Power BI u otro panel.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="b8a1d-168">*¿Cómo se obtienen datos de telemetría de la propia aplicación?*</span><span class="sxs-lookup"><span data-stu-id="b8a1d-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="b8a1d-169">Instale el SDK de Application Insights en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8a1d-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="b8a1d-170">Más información sobre: [aplicaciones web de Java](app-insights-java-get-started.md) y [aplicaciones web de Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="b8a1d-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="b8a1d-171">Vídeo</span><span class="sxs-lookup"><span data-stu-id="b8a1d-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="b8a1d-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8a1d-172">Next steps</span></span>

* [<span data-ttu-id="b8a1d-173">Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="b8a1d-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="b8a1d-174">Application Insights para Node.js</span><span class="sxs-lookup"><span data-stu-id="b8a1d-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="b8a1d-175">Application Insights para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b8a1d-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
