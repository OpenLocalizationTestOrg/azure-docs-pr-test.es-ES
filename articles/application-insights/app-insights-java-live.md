---
title: "Application Insights para aplicaciones web de Java que ya están activas"
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="7c951-103">Application Insights para aplicaciones web de Java que ya están activas</span><span class="sxs-lookup"><span data-stu-id="7c951-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="7c951-104">Si tiene una aplicación web que se está ejecutando en el servidor de J2EE, puede iniciar la supervisión con [Application Insights](app-insights-overview.md) sin necesidad de realizar cambios de código ni volver a compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7c951-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="7c951-105">Con esta opción, obtendrá información acerca de las solicitudes HTTP enviadas al servidor, las excepciones no controladas y contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7c951-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="7c951-106">Necesitará una suscripción a [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c951-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="7c951-107">El procedimiento en esta página agrega el SDK a la aplicación web en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="7c951-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="7c951-108">Esta instrumentación en tiempo de ejecución es útil si no desea actualizar o volver a generar el código fuente.</span><span class="sxs-lookup"><span data-stu-id="7c951-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="7c951-109">Pero si es posible, se recomienda [agregar el SDK al código fuente](app-insights-java-get-started.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7c951-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="7c951-110">Que proporciona más opciones, como la escritura de código para realizar el seguimiento de actividad del usuario.</span><span class="sxs-lookup"><span data-stu-id="7c951-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="7c951-111">1. Obtención de una clave de instrumentación de Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c951-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="7c951-112">Inicie sesión en el [Portal de Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7c951-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="7c951-113">Cree un nuevo recurso de Application Insights y establezca el tipo de aplicación en aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="7c951-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Rellene un nombre, elija la aplicación web de Java y haga clic en Crear.](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="7c951-115">El recurso se crea en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="7c951-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="7c951-116">Abra el nuevo recurso y obtenga su clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="7c951-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="7c951-117">Pronto tendrá que pegarla en el proyecto de código.</span><span class="sxs-lookup"><span data-stu-id="7c951-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![En la información general de nuevos recursos, haga clic en Propiedades y copie la clave de instrumentación.](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="7c951-119">2. Descarga del SDK</span><span class="sxs-lookup"><span data-stu-id="7c951-119">2. Download the SDK</span></span>
1. <span data-ttu-id="7c951-120">Descargue el [SDK de Application Insights para Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="7c951-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="7c951-121">En el servidor, extraiga el contenido del SDK en el directorio desde el que se cargan los archivos binarios de proyecto.</span><span class="sxs-lookup"><span data-stu-id="7c951-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="7c951-122">Si usa Tomcat, este directorio se encontrará normalmente en `webapps/<your_app_name>/WEB-INF/lib`.</span><span class="sxs-lookup"><span data-stu-id="7c951-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="7c951-123">Tenga en cuenta que necesitará repetir este procedimiento en cada instancia de servidor y en cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c951-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="7c951-124">3. Adición de un archivo xml de Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c951-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="7c951-125">Cree ApplicationInsights.xml en la carpeta en la que se ha agregado el SDK.</span><span class="sxs-lookup"><span data-stu-id="7c951-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="7c951-126">Ponga el archivo en el siguiente XML.</span><span class="sxs-lookup"><span data-stu-id="7c951-126">Put into it the following XML.</span></span>

<span data-ttu-id="7c951-127">Sustituya la clave de instrumentación que obtuvo en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c951-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="7c951-128">La clave de instrumentación se envía junto con todos los elementos de telemetría e indica a Application Insights que se muestre en el recurso.</span><span class="sxs-lookup"><span data-stu-id="7c951-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="7c951-129">El componente de la solicitud HTTP es opcional.</span><span class="sxs-lookup"><span data-stu-id="7c951-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="7c951-130">Envía automáticamente telemetría sobre las solicitudes y tiempos de respuesta en el portal.</span><span class="sxs-lookup"><span data-stu-id="7c951-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="7c951-131">La correlación de eventos es un complemento del componente de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="7c951-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="7c951-132">Asigna un identificador a cada solicitud recibida por el servidor y agrega este identificador como propiedad a todos los elementos de telemetría como la propiedad 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="7c951-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="7c951-133">Le permite correlacionar la telemetría asociada a cada solicitud estableciendo un filtro en la [búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="7c951-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="7c951-134">4. Adición de un filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="7c951-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="7c951-135">Busque y abra el archivo web.xml en el proyecto y combine el siguiente fragmento de código bajo el nodo web-app, donde se han configurado los filtros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c951-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="7c951-136">Para obtener los resultados más precisos, el filtro debe asignarse antes de todos los demás filtros.</span><span class="sxs-lookup"><span data-stu-id="7c951-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="7c951-137">5. Comprobación de las excepciones del firewall</span><span class="sxs-lookup"><span data-stu-id="7c951-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="7c951-138">Es posible que deba [establecer excepciones para enviar los datos salientes](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="7c951-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="7c951-139">6. Reinicio de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="7c951-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="7c951-140">7. Visualización de la telemetría en Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c951-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="7c951-141">Vuelva al recurso de Application Insights en el [Portal de Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c951-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7c951-142">Se mostrará telemetría sobre las solicitudes HTTP en la hoja de información general.</span><span class="sxs-lookup"><span data-stu-id="7c951-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="7c951-143">(Si todavía no está ahí, espere unos segundos y, a continuación, haga clic en Actualizar).</span><span class="sxs-lookup"><span data-stu-id="7c951-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![datos de ejemplo](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="7c951-145">Haga clic en cualquier gráfico para ver métricas más detalladas.</span><span class="sxs-lookup"><span data-stu-id="7c951-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="7c951-146">Y cuando vea las propiedades de una solicitud, podrá ver los eventos de telemetría asociados, como solicitudes y excepciones.</span><span class="sxs-lookup"><span data-stu-id="7c951-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="7c951-147">Más información acerca de las métricas.</span><span class="sxs-lookup"><span data-stu-id="7c951-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="7c951-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c951-148">Next steps</span></span>
* <span data-ttu-id="7c951-149">[Agregue telemetría a las páginas web](app-insights-javascript.md) para supervisar las vistas de páginas y las métricas de usuario.</span><span class="sxs-lookup"><span data-stu-id="7c951-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="7c951-150">[Configure las pruebas web](app-insights-monitor-web-app-availability.md) para comprobar que la aplicación efectivamente está activa y responde adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="7c951-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="7c951-151">Captura de seguimiento de registros</span><span class="sxs-lookup"><span data-stu-id="7c951-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="7c951-152">[Busque eventos y registros](app-insights-diagnostic-search.md) para ayudar a diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="7c951-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

