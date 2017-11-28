---
title: aaaMonitor Node.js servicios con Azure Application Insights | Documentos de Microsoft
description: Supervise el rendimiento y diagnostique problemas en servicios de Node.js con Application Insights.
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="c690b-103">Supervisión de servicios y aplicaciones de Node.js con Application Insights</span><span class="sxs-lookup"><span data-stu-id="c690b-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="c690b-104">[Azure Application Insights](app-insights-overview.md) supervisa los servicios back-end y componentes después de implementarlos toohelp se [detectar y diagnosticar rápidamente problemas de rendimiento y otros](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="c690b-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="c690b-105">Puede utilizarlo para servicios de Node.js hospedados en cualquier lugar: su centro de datos, máquinas virtuales de Azure y aplicaciones web, e incluso otras nubes públicas.</span><span class="sxs-lookup"><span data-stu-id="c690b-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="c690b-106">tooreceive, almacenar y explorar los datos de supervisión, siga Hola siguiendo las instrucciones tooinclude un agente en el código y configurar un recurso de Application Insights correspondiente en Azure.</span><span class="sxs-lookup"><span data-stu-id="c690b-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="c690b-107">agente de Hello envía toothat recurso de datos para su posterior análisis y la exploración.</span><span class="sxs-lookup"><span data-stu-id="c690b-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="c690b-108">automáticamente puede supervisar el agente de Node.js de Hola entrantes y salientes HTTP solicitudes, varias métricas del sistema y excepciones.</span><span class="sxs-lookup"><span data-stu-id="c690b-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="c690b-109">A partir de la versión v0.20, también puede supervisar algunos paquetes comunes de terceros como `mongodb`, `mysql` y `redis`.</span><span class="sxs-lookup"><span data-stu-id="c690b-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="c690b-110">Todos los eventos relacionados con la solicitud HTTP de entrada tooan se ponen en correlación para solucionar el problema con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="c690b-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="c690b-111">Puede supervisar varios aspectos de la aplicación y sistema mediante la instrumentación de ellos manualmente mediante la API del agente de Hola se describe más adelante.</span><span class="sxs-lookup"><span data-stu-id="c690b-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Gráficos de supervisión de rendimiento de ejemplo](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="c690b-113">Introducción</span><span class="sxs-lookup"><span data-stu-id="c690b-113">Getting Started</span></span>

<span data-ttu-id="c690b-114">Vamos a configurar la supervisión para una aplicación o servicio.</span><span class="sxs-lookup"><span data-stu-id="c690b-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="c690b-115"><a name="resource"></a> Configuración de un recurso de App Insights</span><span class="sxs-lookup"><span data-stu-id="c690b-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="c690b-116">**Antes de empezar**, asegúrese de que tiene una suscripción de Azure o bien [obtenga una nueva de forma gratuita][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="c690b-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="c690b-117">Si su organización ya tiene una suscripción de Azure, un administrador puede seguir [estas instrucciones] [ add-aad-user] tooadd se tooit.</span><span class="sxs-lookup"><span data-stu-id="c690b-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="c690b-118">Ahora iniciar sesión en toohello [portal de Azure] [ portal] y crear un recurso de Application Insights tal y como se muestra en la siguiente hello: haga clic en "Nuevo" > "Developer tools" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="c690b-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="c690b-119">recursos de Hello incluyen un punto de conexión para recibir los datos de telemetría, almacenamiento de estos datos, guarda los informes y paneles, reglas y configuración de alertas y mucho más.</span><span class="sxs-lookup"><span data-stu-id="c690b-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Creación de recursos en Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="c690b-121">En la página de creación del recurso de hello, elija "Aplicación Node.js" en desplegable de tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c690b-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="c690b-122">tipo de aplicación Hola determina conjunto predeterminado de Hola de paneles e informes creados por usted.</span><span class="sxs-lookup"><span data-stu-id="c690b-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="c690b-123">No se preocupe, cualquier recurso de Application Insights puede recopilar datos de cualquier lenguaje o plataforma.</span><span class="sxs-lookup"><span data-stu-id="c690b-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Formulario de nuevo recurso de Application Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="c690b-125"><a name="agent"></a>Configurar el agente de hello Node.js</span><span class="sxs-lookup"><span data-stu-id="c690b-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="c690b-126">Ahora es agente de hello tooinclude de tiempo de la aplicación por lo que pueden recopilar datos.</span><span class="sxs-lookup"><span data-stu-id="c690b-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="c690b-127">Iniciar mediante la copia de la clave de instrumentación de los recursos (en adelante denominado tooas su `ikey`) desde el portal de hello, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="c690b-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="c690b-128">Hola visión de la aplicación sistema usa este tooyour de datos de clave toomap recursos de Azure, por lo que necesita toospecify en una variable de entorno o el código de hello agente toouse.</span><span class="sxs-lookup"><span data-stu-id="c690b-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Copia de la clave de instrumentación](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="c690b-130">A continuación, agregue las dependencias de la aplicación de hello Node.js agente biblioteca tooyour a través de package.json.</span><span class="sxs-lookup"><span data-stu-id="c690b-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="c690b-131">En la carpeta raíz de saludo de la aplicación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="c690b-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="c690b-132">Ahora tiene una biblioteca de tooexplicitly carga hello en el código.</span><span class="sxs-lookup"><span data-stu-id="c690b-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="c690b-133">Dado que el agente de hello inserta Instrumental en muchas otras bibliotecas, debe cargarlo tan pronto como sea posible, incluso antes que otras `require` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="c690b-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="c690b-134">tooget iniciado, en parte superior de hello del primer archivo .js agregue:</span><span class="sxs-lookup"><span data-stu-id="c690b-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="c690b-135">Hola `setup` método configura clave de instrumentación de hello (y, por tanto, los recursos de Azure) toobe utilizado de forma predeterminada para todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="c690b-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="c690b-136">Llame a `start` después de que la configuración es toobegin termine de recopilar y enviar los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="c690b-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="c690b-137">También puede proporcionar un ikey a través de la variable de entorno de hello APPINSIGHTS\_INSTRUMENTATIONKEY en lugar de pasar manualmente demasiado `setup()` o `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="c690b-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="c690b-138">Esta práctica permite conservar ikeys fuera del código fuente confirmada y toospecify ikeys distintos para diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="c690b-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="c690b-139">A continuación se documentan opciones de configuración adicionales.</span><span class="sxs-lookup"><span data-stu-id="c690b-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="c690b-140">Puede intentar a agente Hola sin enviar telemetría mediante el establecimiento de la cadena no vacía de hello Instrumental tooany clave.</span><span class="sxs-lookup"><span data-stu-id="c690b-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="c690b-141"><a name="monitor"></a> Supervisión de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c690b-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="c690b-142">agente de Hello automáticamente recopila telemetría sobre el tiempo de ejecución de hello Node.js y algunos módulos de terceros comunes.</span><span class="sxs-lookup"><span data-stu-id="c690b-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="c690b-143">Use su toogenerate de aplicación ahora algunos de estos datos.</span><span class="sxs-lookup"><span data-stu-id="c690b-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="c690b-144">A continuación, en hello [portal de Azure] [ portal] Explorar recurso de Application Insights toohello que creó anteriormente y busque el primer algunos puntos de datos en hello información general sobre la escala de tiempo, como en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="c690b-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="c690b-145">Desplazarse por los gráficos de Hola para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="c690b-145">Click through hello charts for more details.</span></span>

![Primeros puntos de datos](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="c690b-147">Haga clic en hello mapa botón tooview Hola topología de la aplicación detectado para la aplicación, como en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="c690b-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="c690b-148">Desplazarse por los componentes en el mapa de Hola para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="c690b-148">Click through components in hello map for more details.</span></span>

![Mapa de aplicación simple](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="c690b-150">Obtener más información sobre la aplicación y solucionar problemas de uso Hola otras vistas disponibles en la sección "Investigar" Hola.</span><span class="sxs-lookup"><span data-stu-id="c690b-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Sección Investigar](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="c690b-152">¿No hay datos?</span><span class="sxs-lookup"><span data-stu-id="c690b-152">No data?</span></span>

<span data-ttu-id="c690b-153">Porque los datos para el envío de lotes de agente de hello puede haber un retraso antes de que los elementos se muestran en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c690b-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="c690b-154">Si no ve los datos en el recurso pruebe algunas de hello siguientes correcciones:</span><span class="sxs-lookup"><span data-stu-id="c690b-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="c690b-155">Use la aplicación hello algo más; tomar más toogenerate acciones telemetría más.</span><span class="sxs-lookup"><span data-stu-id="c690b-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="c690b-156">Haga clic en **actualizar** Hola portal en vista de recursos.</span><span class="sxs-lookup"><span data-stu-id="c690b-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="c690b-157">Gráficos de actualización automáticamente a sí mismos periódicamente pero actualizar fuerza este toohappen inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="c690b-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="c690b-158">Compruebe que los [puertos de salida necesarios](app-insights-ip-addresses.md) estén abiertos.</span><span class="sxs-lookup"><span data-stu-id="c690b-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="c690b-159">Abra hello [búsqueda](app-insights-diagnostic-search.md) icono y buscar los eventos individuales.</span><span class="sxs-lookup"><span data-stu-id="c690b-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="c690b-160">Comprobar hello [preguntas más frecuentes sobre][].</span><span class="sxs-lookup"><span data-stu-id="c690b-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="c690b-161">Configuración de agente</span><span class="sxs-lookup"><span data-stu-id="c690b-161">Agent Configuration</span></span>

<span data-ttu-id="c690b-162">Siguientes son métodos de configuración del agente de Hola y sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="c690b-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="c690b-163">toofully correlacionar eventos en un servicio, ser seguro tooset `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="c690b-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="c690b-164">Esto permite a agente de hello tootrack contexto a través de las devoluciones de llamada asincrónicas en Node.js.</span><span class="sxs-lookup"><span data-stu-id="c690b-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="c690b-165">API del agente</span><span class="sxs-lookup"><span data-stu-id="c690b-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="c690b-166">Hola .NET API del agente se describe con detalle [aquí](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c690b-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="c690b-167">Puede realizar un seguimiento de cualquier solicitud, el evento, la métrica o la excepción mediante el cliente de aplicación visión Node.js de Hola.</span><span class="sxs-lookup"><span data-stu-id="c690b-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="c690b-168">Hello en el ejemplo siguiente se muestra algunas de hello las API disponibles.</span><span class="sxs-lookup"><span data-stu-id="c690b-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="c690b-169">Seguimiento de las dependencias</span><span class="sxs-lookup"><span data-stu-id="c690b-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="c690b-170">Agregar un eventos tooall de propiedad personalizada</span><span class="sxs-lookup"><span data-stu-id="c690b-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="c690b-171">Seguimiento de solicitudes HTTP GET</span><span class="sxs-lookup"><span data-stu-id="c690b-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="c690b-172">Seguimiento de la hora de inicio del servidor</span><span class="sxs-lookup"><span data-stu-id="c690b-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="c690b-173">Más recursos</span><span class="sxs-lookup"><span data-stu-id="c690b-173">More resources</span></span>

* [<span data-ttu-id="c690b-174">Supervise la telemetría en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="c690b-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="c690b-175">Escritura de consultas de Analytics sobre los datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="c690b-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[preguntas más frecuentes sobre]: app-insights-troubleshoot-faq.md
