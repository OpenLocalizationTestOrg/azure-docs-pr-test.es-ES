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
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Application Insights para aplicaciones web de Java que ya están activas


Si tiene una aplicación web que ya se está ejecutando en el servidor J2EE, puede iniciar la supervisión con [Application Insights](app-insights-overview.md) sin Hola necesita toomake cambios en el código o volver a compilar el proyecto. Con esta opción, obtendrá información sobre las solicitudes HTTP enviadas tooyour server, las excepciones no controladas y contadores de rendimiento.

Necesitará una suscripción demasiado[Microsoft Azure](https://azure.com).

> [!NOTE]
> procedimiento de Hello en esta página agrega la aplicación web de hello SDK tooyour en tiempo de ejecución. Este tiempo de ejecución instrumentación es útil si no desea tooupdate o volver a generar el código fuente. Pero si es posible, le recomendamos que [agregar código fuente de hello SDK toohello](app-insights-java-get-started.md) en su lugar. Que proporciona más opciones, como la escritura de actividad de usuario de tootrack de código.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Obtención de una clave de instrumentación de Application Insights
1. Inicie sesión en toohello [portal de Microsoft Azure](https://portal.azure.com)
2. Crear un nuevo recurso de Application Insights y establecer la aplicación web de hello aplicación tipo tooJava.
   
    ![Rellene un nombre, elija la aplicación web de Java y haga clic en Crear.](./media/app-insights-java-live/02-create.png)

    se crea el recurso de Hello en unos segundos.

4. Abra el nuevo recurso de Hola y obtener su clave de instrumentación. Necesitará toopaste esta clave en el proyecto de código en breve.
   
    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Descargar Hola SDK
1. Descargar hello [Application Insights SDK para Java](https://aka.ms/aijavasdk). 
2. En el servidor, extraiga el directorio de toohello del contenido SDK de Hola desde el que se cargan los archivos binarios de proyecto. Si usa Tomcat, este directorio se encontrará normalmente en `webapps/<your_app_name>/WEB-INF/lib`.

Tenga en cuenta que necesita toorepeat esto en cada instancia del servidor y para cada aplicación.

## <a name="3-add-an-application-insights-xml-file"></a>3. Adición de un archivo xml de Application Insights
Crear ApplicationInsights.xml en carpeta de hello en el que se agrega Hola SDK. Coloque en él Hola después de XML.

Sustituya la clave de instrumentación de Hola que obtuvo en hello portal de Azure.

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

* clave de instrumentación de Hola se envía junto con todos los elementos de telemetría e indica toodisplay Application Insights en el recurso.
* Hola componente de la solicitud HTTP es opcional. Envía automáticamente telemetría sobre las solicitudes y portal de toohello de tiempos de respuesta.
* Correlación de eventos es un componente de solicitud de incorporación toohello HTTP. Asigna una identificador tooeach las solicitudes recibidas por server hello y agrega este identificador como un elemento de propiedad tooevery de telemetría como propiedad de hello 'Operation.Id'. Le permite la telemetría de hello toocorrelate asociado con cada solicitud estableciendo un filtro [búsqueda diagnóstico](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. Adición de un filtro HTTP
Busque y abra el archivo web.xml de hello en el proyecto y Hola de mezcla después de fragmento de código bajo el nodo de la aplicación web de hello, donde se configuran los filtros de aplicación.

resultados más precisos tooget hello, filtro de hello deben asignarse antes de todos los demás filtros.

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

## <a name="5-check-firewall-exceptions"></a>5. Comprobación de las excepciones del firewall
Es posible que tenga demasiado[establecer excepciones datos salientes toosend](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Reinicio de la aplicación web
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Visualización de la telemetría en Application Insights
Devolver recurso de Application Insights tooyour en [portal de Microsoft Azure](https://portal.azure.com).

Telemetría sobre solicitudes HTTP que aparece en la hoja de información general de Hola. (Si todavía no está ahí, espere unos segundos y, a continuación, haga clic en Actualizar).

![datos de ejemplo](./media/app-insights-java-live/5-results.png)

Haga clic en a través de cualquier toosee gráfico métricas más detalladas. 

![](./media/app-insights-java-live/6-barchart.png)

Y, al ver las propiedades de Hola de una solicitud, puede ver eventos de telemetría de hello asociados con él, como las solicitudes y las excepciones.

![](./media/app-insights-java-live/7-instance.png)

[Más información acerca de las métricas.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Pasos siguientes
* [Agregar páginas web de telemetría tooyour](app-insights-javascript.md) toomonitor página vistas y las métricas de usuario.
* [Configurar las pruebas web](app-insights-monitor-web-app-availability.md) toomake seguro de la aplicación permanece en vivo y capacidad de respuesta.
* [Captura de seguimiento de registros](app-insights-java-trace-logs.md)
* [Buscar eventos y registros](app-insights-diagnostic-search.md) toohelp diagnosticar problemas.

