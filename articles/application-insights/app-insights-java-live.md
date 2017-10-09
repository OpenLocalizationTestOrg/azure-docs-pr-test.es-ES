---
title: "aaaApplication aplicaciones que ya están en vivo de web de visión para Java"
description: "Inicio de la supervisión de una aplicación web que se ya se está ejecutando en el servidor"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="6aa63-103">Application Insights para aplicaciones web de Java que ya están activas</span><span class="sxs-lookup"><span data-stu-id="6aa63-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="6aa63-104">Si tiene una aplicación web que ya se está ejecutando en el servidor J2EE, puede iniciar la supervisión con [Application Insights](app-insights-overview.md) sin Hola necesita toomake cambios en el código o volver a compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6aa63-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="6aa63-105">Con esta opción, obtendrá información sobre las solicitudes HTTP enviadas tooyour server, las excepciones no controladas y contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="6aa63-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="6aa63-106">Necesitará una suscripción demasiado[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aa63-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="6aa63-107">procedimiento de Hello en esta página agrega la aplicación web de hello SDK tooyour en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6aa63-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="6aa63-108">Este tiempo de ejecución instrumentación es útil si no desea tooupdate o volver a generar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="6aa63-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="6aa63-109">Pero si es posible, le recomendamos que [agregar código fuente de hello SDK toohello](app-insights-java-get-started.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="6aa63-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="6aa63-110">Que proporciona más opciones, como la escritura de actividad de usuario de tootrack de código.</span><span class="sxs-lookup"><span data-stu-id="6aa63-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="6aa63-111">1. Obtención de una clave de instrumentación de Application Insights</span><span class="sxs-lookup"><span data-stu-id="6aa63-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="6aa63-112">Inicie sesión en toohello [portal de Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6aa63-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="6aa63-113">Crear un nuevo recurso de Application Insights y establecer la aplicación web de hello aplicación tipo tooJava.</span><span class="sxs-lookup"><span data-stu-id="6aa63-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Rellene un nombre, elija la aplicación web de Java y haga clic en Crear.](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="6aa63-115">se crea el recurso de Hello en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="6aa63-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="6aa63-116">Abra el nuevo recurso de Hola y obtener su clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="6aa63-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="6aa63-117">Necesitará toopaste esta clave en el proyecto de código en breve.</span><span class="sxs-lookup"><span data-stu-id="6aa63-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="6aa63-119">2. Descargar Hola SDK</span><span class="sxs-lookup"><span data-stu-id="6aa63-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="6aa63-120">Descargar hello [Application Insights SDK para Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="6aa63-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="6aa63-121">En el servidor, extraiga el directorio de toohello del contenido SDK de Hola desde el que se cargan los archivos binarios de proyecto.</span><span class="sxs-lookup"><span data-stu-id="6aa63-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="6aa63-122">Si usa Tomcat, este directorio se encontrará normalmente en `webapps/<your_app_name>/WEB-INF/lib`.</span><span class="sxs-lookup"><span data-stu-id="6aa63-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="6aa63-123">Tenga en cuenta que necesita toorepeat esto en cada instancia del servidor y para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="6aa63-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="6aa63-124">3. Adición de un archivo xml de Application Insights</span><span class="sxs-lookup"><span data-stu-id="6aa63-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="6aa63-125">Crear ApplicationInsights.xml en carpeta de hello en el que se agrega Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="6aa63-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="6aa63-126">Coloque en él Hola después de XML.</span><span class="sxs-lookup"><span data-stu-id="6aa63-126">Put into it hello following XML.</span></span>

<span data-ttu-id="6aa63-127">Sustituya la clave de instrumentación de Hola que obtuvo en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa63-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="6aa63-128">clave de instrumentación de Hola se envía junto con todos los elementos de telemetría e indica toodisplay Application Insights en el recurso.</span><span class="sxs-lookup"><span data-stu-id="6aa63-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="6aa63-129">Hola componente de la solicitud HTTP es opcional.</span><span class="sxs-lookup"><span data-stu-id="6aa63-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="6aa63-130">Envía automáticamente telemetría sobre las solicitudes y portal de toohello de tiempos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="6aa63-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="6aa63-131">Correlación de eventos es un componente de solicitud de incorporación toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="6aa63-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="6aa63-132">Asigna una identificador tooeach las solicitudes recibidas por server hello y agrega este identificador como un elemento de propiedad tooevery de telemetría como propiedad de hello 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="6aa63-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="6aa63-133">Le permite la telemetría de hello toocorrelate asociado con cada solicitud estableciendo un filtro [búsqueda diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="6aa63-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="6aa63-134">4. Adición de un filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="6aa63-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="6aa63-135">Busque y abra el archivo web.xml de hello en el proyecto y Hola de mezcla después de fragmento de código bajo el nodo de la aplicación web de hello, donde se configuran los filtros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6aa63-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="6aa63-136">resultados más precisos tooget hello, filtro de hello deben asignarse antes de todos los demás filtros.</span><span class="sxs-lookup"><span data-stu-id="6aa63-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="6aa63-137">5. Comprobación de las excepciones del firewall</span><span class="sxs-lookup"><span data-stu-id="6aa63-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="6aa63-138">Es posible que tenga demasiado[establecer excepciones datos salientes toosend](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="6aa63-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="6aa63-139">6. Reinicio de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="6aa63-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="6aa63-140">7. Visualización de la telemetría en Application Insights</span><span class="sxs-lookup"><span data-stu-id="6aa63-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="6aa63-141">Devolver recurso de Application Insights tooyour en [portal de Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aa63-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="6aa63-142">Telemetría sobre solicitudes HTTP que aparece en la hoja de información general de Hola.</span><span class="sxs-lookup"><span data-stu-id="6aa63-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="6aa63-143">(Si todavía no está ahí, espere unos segundos y, a continuación, haga clic en Actualizar).</span><span class="sxs-lookup"><span data-stu-id="6aa63-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![datos de ejemplo](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="6aa63-145">Haga clic en a través de cualquier toosee gráfico métricas más detalladas.</span><span class="sxs-lookup"><span data-stu-id="6aa63-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="6aa63-146">Y, al ver las propiedades de Hola de una solicitud, puede ver eventos de telemetría de hello asociados con él, como las solicitudes y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="6aa63-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="6aa63-147">Más información acerca de las métricas.</span><span class="sxs-lookup"><span data-stu-id="6aa63-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="6aa63-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6aa63-148">Next steps</span></span>
* <span data-ttu-id="6aa63-149">[Agregar páginas web de telemetría tooyour](app-insights-javascript.md) toomonitor página vistas y las métricas de usuario.</span><span class="sxs-lookup"><span data-stu-id="6aa63-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="6aa63-150">[Configurar las pruebas web](app-insights-monitor-web-app-availability.md) toomake seguro de la aplicación permanece en vivo y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="6aa63-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="6aa63-151">Captura de seguimiento de registros</span><span class="sxs-lookup"><span data-stu-id="6aa63-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="6aa63-152">[Buscar eventos y registros](app-insights-diagnostic-search.md) toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="6aa63-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

