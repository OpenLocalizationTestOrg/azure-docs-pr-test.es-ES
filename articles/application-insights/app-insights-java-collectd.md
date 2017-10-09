---
title: "rendimiento de aplicación web de Java en Linux - Azure aaaMonitor | Documentos de Microsoft"
description: "Extender la aplicación supervisión del rendimiento de su sitio Web de Java con hello CollectD complemento de Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="2290b-103">collectd: métricas de rendimiento de Linux en Application Insights</span><span class="sxs-lookup"><span data-stu-id="2290b-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="2290b-104">estadísticas de rendimiento de sistema de Linux de tooexplore de [Application Insights](app-insights-overview.md), instalar [collectd](http://collectd.org/), junto con su complemento de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2290b-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="2290b-105">Esta solución de código abierto recopila diversas estadísticas de red y del sistema.</span><span class="sxs-lookup"><span data-stu-id="2290b-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="2290b-106">Normalmente, usará collectd si ya ha [instrumentado el servicio web de Java con Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="2290b-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="2290b-107">Le ofrece más toohelp datos tooenhance el rendimiento de la aplicación o diagnosticar los problemas.</span><span class="sxs-lookup"><span data-stu-id="2290b-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![Gráficos de ejemplo](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="2290b-109">Obtención de la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="2290b-109">Get your instrumentation key</span></span>
<span data-ttu-id="2290b-110">Hola [portal de Microsoft Azure](https://portal.azure.com), abra hello [Application Insights](app-insights-overview.md) recurso donde desea hello tooappear de datos.</span><span class="sxs-lookup"><span data-stu-id="2290b-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="2290b-111">(o bien, [cree un nuevo recurso](app-insights-create-new-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="2290b-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="2290b-112">Realizar una copia de la clave de instrumentación de hello, que identifica el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2290b-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Examinar todo, abra el recurso y, a continuación, en hello Essentials de lista desplegable, seleccione y copie Hola clave de instrumentación](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="2290b-114">Instalar el complemento de hello y collectd</span><span class="sxs-lookup"><span data-stu-id="2290b-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="2290b-115">En los equipos de servidor Linux:</span><span class="sxs-lookup"><span data-stu-id="2290b-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="2290b-116">Instale la versión de [collectd](http://collectd.org/) 5.4.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2290b-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="2290b-117">Descargar hello [Application Insights collectd escritor complemento](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="2290b-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="2290b-118">Tenga en cuenta el número de versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2290b-118">Note hello version number.</span></span>
3. <span data-ttu-id="2290b-119">Copiar Hola complemento JAR en `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="2290b-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="2290b-120">Edite `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="2290b-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="2290b-121">Asegúrese de que [Hola complemento Java](https://collectd.org/wiki/index.php/Plugin:Java) está habilitado.</span><span class="sxs-lookup"><span data-stu-id="2290b-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="2290b-122">Actualizar hello JVMArg para Hola java.class.path tooinclude Hola después JAR.</span><span class="sxs-lookup"><span data-stu-id="2290b-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="2290b-123">Actualizar Hola Hola del toomatch número de versión que descargó:</span><span class="sxs-lookup"><span data-stu-id="2290b-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="2290b-124">Agregue este fragmento de código, utilizando Hola clave de instrumentación desde el recurso:</span><span class="sxs-lookup"><span data-stu-id="2290b-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="2290b-125">A continuación se muestra un archivo de configuración de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2290b-125">Here's part of a sample configuration file:</span></span>

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

<span data-ttu-id="2290b-126">Configure otros [complementos de collectd](https://collectd.org/wiki/index.php/Table_of_Plugins)que pueden recopilar diversos datos de orígenes diferentes.</span><span class="sxs-lookup"><span data-stu-id="2290b-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="2290b-127">Reinicie collectd según tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="2290b-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="2290b-128">Ver los datos de hello en Application Insights</span><span class="sxs-lookup"><span data-stu-id="2290b-128">View hello data in Application Insights</span></span>
<span data-ttu-id="2290b-129">En el recurso de Application Insights, abra [Explorer métricas y agregue gráficos][metrics], seleccionando las métricas de Hola que desea toosee de categoría de saludo personalizado.</span><span class="sxs-lookup"><span data-stu-id="2290b-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="2290b-130">De forma predeterminada, se agregan las métricas de hello en todos los equipos host desde el que se recopilan las métricas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2290b-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="2290b-131">las métricas de hello tooview por host, en la hoja de detalles del gráfico de hello, activar la agrupación y, a continuación, elija toogroup CollectD host.</span><span class="sxs-lookup"><span data-stu-id="2290b-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="2290b-132">carga de tooexclude de las estadísticas específicas</span><span class="sxs-lookup"><span data-stu-id="2290b-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="2290b-133">De forma predeterminada, complemento de Application Insights Hola envía todos los datos de hello recopilados por todos los collectd Hola habilitado 'read' complementos.</span><span class="sxs-lookup"><span data-stu-id="2290b-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="2290b-134">tooexclude datos procedentes de orígenes de datos o complementos específicos:</span><span class="sxs-lookup"><span data-stu-id="2290b-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="2290b-135">Editar el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="2290b-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="2290b-136">En `<Plugin ApplicationInsightsWriter>`, agregue líneas de directiva de esta manera:</span><span class="sxs-lookup"><span data-stu-id="2290b-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="2290b-137">Directiva</span><span class="sxs-lookup"><span data-stu-id="2290b-137">Directive</span></span> | <span data-ttu-id="2290b-138">Efecto</span><span class="sxs-lookup"><span data-stu-id="2290b-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="2290b-139">Excluir todos los datos recopilados por hello `disk` complemento</span><span class="sxs-lookup"><span data-stu-id="2290b-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="2290b-140">Excluir orígenes de hello denominados `read` y `write` de hello `disk` complemento.</span><span class="sxs-lookup"><span data-stu-id="2290b-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="2290b-141">Separar directivas con una nueva línea.</span><span class="sxs-lookup"><span data-stu-id="2290b-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="2290b-142">¿Tiene problemas?</span><span class="sxs-lookup"><span data-stu-id="2290b-142">Problems?</span></span>
<span data-ttu-id="2290b-143">*No se ve datos en el portal de Hola*</span><span class="sxs-lookup"><span data-stu-id="2290b-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="2290b-144">Abra [búsqueda] [ diagnostic] toosee si han llegado eventos sin procesar de Hola.</span><span class="sxs-lookup"><span data-stu-id="2290b-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="2290b-145">En ocasiones necesita más tooappear en el Explorador de métricas.</span><span class="sxs-lookup"><span data-stu-id="2290b-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="2290b-146">Es posible que tenga demasiado[establecer excepciones de firewall para los datos salientes](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="2290b-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="2290b-147">Habilitar el seguimiento en el complemento de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="2290b-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="2290b-148">Agregue esta línea en `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="2290b-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="2290b-149">Abra un terminal e iniciar collectd en modo detallado, toosee cualquier problema que está informando:</span><span class="sxs-lookup"><span data-stu-id="2290b-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="2290b-150">Problema conocido</span><span class="sxs-lookup"><span data-stu-id="2290b-150">Known issue</span></span>

<span data-ttu-id="2290b-151">complemento de escritura de información de aplicación Hello es compatible con ciertos complementos de lectura.</span><span class="sxs-lookup"><span data-stu-id="2290b-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="2290b-152">Algunos complementos envían a veces "NaN" cuando el complemento de Application Insights Hola espera un número de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="2290b-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="2290b-153">Síntoma: registro de hello collectd muestra errores que incluyen "AI:... SyntaxError: token inesperado N".</span><span class="sxs-lookup"><span data-stu-id="2290b-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="2290b-154">Solución alternativa: Excluir datos recopilados por los complementos de escritura de problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="2290b-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


