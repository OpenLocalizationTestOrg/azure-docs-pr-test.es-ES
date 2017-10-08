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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Supervisión de servicios y aplicaciones de Node.js con Application Insights

[Azure Application Insights](app-insights-overview.md) supervisa los servicios back-end y componentes después de implementarlos toohelp se [detectar y diagnosticar rápidamente problemas de rendimiento y otros](app-insights-detect-triage-diagnose.md). Puede utilizarlo para servicios de Node.js hospedados en cualquier lugar: su centro de datos, máquinas virtuales de Azure y aplicaciones web, e incluso otras nubes públicas.

tooreceive, almacenar y explorar los datos de supervisión, siga Hola siguiendo las instrucciones tooinclude un agente en el código y configurar un recurso de Application Insights correspondiente en Azure. agente de Hello envía toothat recurso de datos para su posterior análisis y la exploración.

automáticamente puede supervisar el agente de Node.js de Hola entrantes y salientes HTTP solicitudes, varias métricas del sistema y excepciones. A partir de la versión v0.20, también puede supervisar algunos paquetes comunes de terceros como `mongodb`, `mysql` y `redis`. Todos los eventos relacionados con la solicitud HTTP de entrada tooan se ponen en correlación para solucionar el problema con mayor rapidez.

Puede supervisar varios aspectos de la aplicación y sistema mediante la instrumentación de ellos manualmente mediante la API del agente de Hola se describe más adelante.

![Gráficos de supervisión de rendimiento de ejemplo](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Introducción

Vamos a configurar la supervisión para una aplicación o servicio.

### <a name="resource"></a> Configuración de un recurso de App Insights

**Antes de empezar**, asegúrese de que tiene una suscripción de Azure o bien [obtenga una nueva de forma gratuita][azure-free-offer]. Si su organización ya tiene una suscripción de Azure, un administrador puede seguir [estas instrucciones] [ add-aad-user] tooadd se tooit.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Ahora iniciar sesión en toohello [portal de Azure] [ portal] y crear un recurso de Application Insights tal y como se muestra en la siguiente hello: haga clic en "Nuevo" > "Developer tools" > "Application Insights". recursos de Hello incluyen un punto de conexión para recibir los datos de telemetría, almacenamiento de estos datos, guarda los informes y paneles, reglas y configuración de alertas y mucho más.

![Creación de recursos en Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

En la página de creación del recurso de hello, elija "Aplicación Node.js" en desplegable de tipo de aplicación Hola. tipo de aplicación Hola determina conjunto predeterminado de Hola de paneles e informes creados por usted. No se preocupe, cualquier recurso de Application Insights puede recopilar datos de cualquier lenguaje o plataforma.

![Formulario de nuevo recurso de Application Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Configurar el agente de hello Node.js

Ahora es agente de hello tooinclude de tiempo de la aplicación por lo que pueden recopilar datos.
Iniciar mediante la copia de la clave de instrumentación de los recursos (en adelante denominado tooas su `ikey`) desde el portal de hello, tal como se muestra a continuación. Hola visión de la aplicación sistema usa este tooyour de datos de clave toomap recursos de Azure, por lo que necesita toospecify en una variable de entorno o el código de hello agente toouse.  

![Copia de la clave de instrumentación](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

A continuación, agregue las dependencias de la aplicación de hello Node.js agente biblioteca tooyour a través de package.json. En la carpeta raíz de saludo de la aplicación, ejecute:

```bash
npm install applicationinsights --save
```

Ahora tiene una biblioteca de tooexplicitly carga hello en el código. Dado que el agente de hello inserta Instrumental en muchas otras bibliotecas, debe cargarlo tan pronto como sea posible, incluso antes que otras `require` instrucciones. tooget iniciado, en parte superior de hello del primer archivo .js agregue:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Hola `setup` método configura clave de instrumentación de hello (y, por tanto, los recursos de Azure) toobe utilizado de forma predeterminada para todos los elementos. Llame a `start` después de que la configuración es toobegin termine de recopilar y enviar los datos de telemetría.

También puede proporcionar un ikey a través de la variable de entorno de hello APPINSIGHTS\_INSTRUMENTATIONKEY en lugar de pasar manualmente demasiado `setup()` o `getClient()`. Esta práctica permite conservar ikeys fuera del código fuente confirmada y toospecify ikeys distintos para diferentes entornos.

A continuación se documentan opciones de configuración adicionales.

Puede intentar a agente Hola sin enviar telemetría mediante el establecimiento de la cadena no vacía de hello Instrumental tooany clave.

### <a name="monitor"></a> Supervisión de la aplicación

agente de Hello automáticamente recopila telemetría sobre el tiempo de ejecución de hello Node.js y algunos módulos de terceros comunes. Use su toogenerate de aplicación ahora algunos de estos datos.

A continuación, en hello [portal de Azure] [ portal] Explorar recurso de Application Insights toohello que creó anteriormente y busque el primer algunos puntos de datos en hello información general sobre la escala de tiempo, como en hello después de la imagen. Desplazarse por los gráficos de Hola para obtener más detalles.

![Primeros puntos de datos](./media/app-insights-nodejs/12-first-perf.png)

Haga clic en hello mapa botón tooview Hola topología de la aplicación detectado para la aplicación, como en hello después de la imagen. Desplazarse por los componentes en el mapa de Hola para obtener más detalles.

![Mapa de aplicación simple](./media/app-insights-nodejs/06-appinsights_appmap.png)

Obtener más información sobre la aplicación y solucionar problemas de uso Hola otras vistas disponibles en la sección "Investigar" Hola.

![Sección Investigar](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>¿No hay datos?

Porque los datos para el envío de lotes de agente de hello puede haber un retraso antes de que los elementos se muestran en el portal de Hola. Si no ve los datos en el recurso pruebe algunas de hello siguientes correcciones:

* Use la aplicación hello algo más; tomar más toogenerate acciones telemetría más.
* Haga clic en **actualizar** Hola portal en vista de recursos. Gráficos de actualización automáticamente a sí mismos periódicamente pero actualizar fuerza este toohappen inmediatamente.
* Compruebe que los [puertos de salida necesarios](app-insights-ip-addresses.md) estén abiertos.
* Abra hello [búsqueda](app-insights-diagnostic-search.md) icono y buscar los eventos individuales.
* Comprobar hello [preguntas más frecuentes sobre][].


## <a name="agent-configuration"></a>Configuración de agente

Siguientes son métodos de configuración del agente de Hola y sus valores predeterminados.

toofully correlacionar eventos en un servicio, ser seguro tooset `.setAutoDependencyCorrelation(true)`. Esto permite a agente de hello tootrack contexto a través de las devoluciones de llamada asincrónicas en Node.js.

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

## <a name="agent-api"></a>API del agente

<!-- TODO: Fully document agent API. -->

Hola .NET API del agente se describe con detalle [aquí](app-insights-api-custom-events-metrics.md).

Puede realizar un seguimiento de cualquier solicitud, el evento, la métrica o la excepción mediante el cliente de aplicación visión Node.js de Hola. Hello en el ejemplo siguiente se muestra algunas de hello las API disponibles.

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

### <a name="track-your-dependencies"></a>Seguimiento de las dependencias

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

### <a name="add-a-custom-property-tooall-events"></a>Agregar un eventos tooall de propiedad personalizada

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>Seguimiento de solicitudes HTTP GET

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Seguimiento de la hora de inicio del servidor

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Más recursos

* [Supervise la telemetría en el portal de Hola](app-insights-dashboards.md)
* [Escritura de consultas de Analytics sobre los datos de telemetría](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[preguntas más frecuentes sobre]: app-insights-troubleshoot-faq.md
