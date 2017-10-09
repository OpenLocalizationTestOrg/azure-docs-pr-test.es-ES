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
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: métricas de rendimiento de Linux en Application Insights


estadísticas de rendimiento de sistema de Linux de tooexplore de [Application Insights](app-insights-overview.md), instalar [collectd](http://collectd.org/), junto con su complemento de Application Insights. Esta solución de código abierto recopila diversas estadísticas de red y del sistema.

Normalmente, usará collectd si ya ha [instrumentado el servicio web de Java con Application Insights][java]. Le ofrece más toohelp datos tooenhance el rendimiento de la aplicación o diagnosticar los problemas. 

![Gráficos de ejemplo](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>Obtención de la clave de instrumentación
Hola [portal de Microsoft Azure](https://portal.azure.com), abra hello [Application Insights](app-insights-overview.md) recurso donde desea hello tooappear de datos. (o bien, [cree un nuevo recurso](app-insights-create-new-resource.md)).

Realizar una copia de la clave de instrumentación de hello, que identifica el recurso de Hola.

![Examinar todo, abra el recurso y, a continuación, en hello Essentials de lista desplegable, seleccione y copie Hola clave de instrumentación](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Instalar el complemento de hello y collectd
En los equipos de servidor Linux:

1. Instale la versión de [collectd](http://collectd.org/) 5.4.0 o posterior.
2. Descargar hello [Application Insights collectd escritor complemento](https://aka.ms/aijavasdk). Tenga en cuenta el número de versión de Hola.
3. Copiar Hola complemento JAR en `/usr/share/collectd/java`.
4. Edite `/etc/collectd/collectd.conf`:
   * Asegúrese de que [Hola complemento Java](https://collectd.org/wiki/index.php/Plugin:Java) está habilitado.
   * Actualizar hello JVMArg para Hola java.class.path tooinclude Hola después JAR. Actualizar Hola Hola del toomatch número de versión que descargó:
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * Agregue este fragmento de código, utilizando Hola clave de instrumentación desde el recurso:

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

A continuación se muestra un archivo de configuración de ejemplo:

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

Configure otros [complementos de collectd](https://collectd.org/wiki/index.php/Table_of_Plugins)que pueden recopilar diversos datos de orígenes diferentes.

Reinicie collectd según tooits [manual](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Ver los datos de hello en Application Insights
En el recurso de Application Insights, abra [Explorer métricas y agregue gráficos][metrics], seleccionando las métricas de Hola que desea toosee de categoría de saludo personalizado.

![](./media/app-insights-java-collectd/result.png)

De forma predeterminada, se agregan las métricas de hello en todos los equipos host desde el que se recopilan las métricas de Hola. las métricas de hello tooview por host, en la hoja de detalles del gráfico de hello, activar la agrupación y, a continuación, elija toogroup CollectD host.

## <a name="tooexclude-upload-of-specific-statistics"></a>carga de tooexclude de las estadísticas específicas
De forma predeterminada, complemento de Application Insights Hola envía todos los datos de hello recopilados por todos los collectd Hola habilitado 'read' complementos. 

tooexclude datos procedentes de orígenes de datos o complementos específicos:

* Editar el archivo de configuración de Hola. 
* En `<Plugin ApplicationInsightsWriter>`, agregue líneas de directiva de esta manera:

| Directiva | Efecto |
| --- | --- |
| `Exclude disk` |Excluir todos los datos recopilados por hello `disk` complemento |
| `Exclude disk:read,write` |Excluir orígenes de hello denominados `read` y `write` de hello `disk` complemento. |

Separar directivas con una nueva línea.

## <a name="problems"></a>¿Tiene problemas?
*No se ve datos en el portal de Hola*

* Abra [búsqueda] [ diagnostic] toosee si han llegado eventos sin procesar de Hola. En ocasiones necesita más tooappear en el Explorador de métricas.
* Es posible que tenga demasiado[establecer excepciones de firewall para los datos salientes](app-insights-ip-addresses.md)
* Habilitar el seguimiento en el complemento de Application Insights Hola. Agregue esta línea en `<Plugin ApplicationInsightsWriter>`:
  * `SDKLogger true`
* Abra un terminal e iniciar collectd en modo detallado, toosee cualquier problema que está informando:
  * `sudo collectd -f`

## <a name="known-issue"></a>Problema conocido

complemento de escritura de información de aplicación Hello es compatible con ciertos complementos de lectura. Algunos complementos envían a veces "NaN" cuando el complemento de Application Insights Hola espera un número de punto flotante.

Síntoma: registro de hello collectd muestra errores que incluyen "AI:... SyntaxError: token inesperado N".

Solución alternativa: Excluir datos recopilados por los complementos de escritura de problema de Hola. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


