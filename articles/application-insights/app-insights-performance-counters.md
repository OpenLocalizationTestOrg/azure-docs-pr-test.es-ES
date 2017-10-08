---
title: contadores de aaaPerformance en Application Insights | Documentos de Microsoft
description: Supervise los contadores de rendimiento de .NET, tanto del sistema como personalizados, en Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Contadores de rendimiento de sistema en Application Insights
Windows proporciona una amplia variedad de [contadores de rendimiento](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), como la ocupación de la CPU, memoria, disco y uso de la red. También puede definir sus propios contadores. [Application Insights](app-insights-overview.md) puede mostrar estos contadores de rendimiento si la aplicación que ejecuta en IIS en un toowhich de host o máquina virtual local tengan acceso administrativo. gráficos de Hello indican Hola recursos disponibles tooyour vivo de las aplicaciones y pueden ayudar a tooidentify carga desequilibrada entre instancias de servidor.

Contadores de rendimiento aparecen en la hoja de servidores de hello, que incluye una tabla que segmenta por instancia de servidor.

![Contadores de rendimiento notificados en Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

(Los contadores de rendimiento no están disponibles para Azure Web Apps. Pero puede [enviar información de diagnóstico de Azure tooApplication](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Visualización de contadores
hoja de servidores de Hello muestra un conjunto predeterminado de contadores de rendimiento. 

toosee otros contadores, edite los gráficos de hello en la hoja de servidores de Hola o abra una nueva [Explorer métricas](app-insights-metrics-explorer.md) hoja y agregar nuevos gráficos. 

se enumeran los contadores disponibles de Hello métricas cuando se edita un gráfico.

![Contadores de rendimiento notificados en Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

toosee todos los gráficos más útiles en un solo lugar, cree un [panel](app-insights-dashboards.md) y anclarlos tooit.

## <a name="add-counters"></a>Adición de contadores
Si desea que el contador de rendimiento de hello no se muestre en lista de Hola de métricas, eso es porque Hola Application Insights SDK no está recopilando en el servidor web. Se puede configurar toodo así.

1. Averiguar qué contadores están disponibles en el servidor mediante el uso de este comando de PowerShell en el servidor de hello:
   
    `Get-Counter -ListSet *`
   
    (Consulte [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx)).
2. Abra ApplicationInsights.config.
   
   * Si agrega Application Insights tooyour aplicación durante el desarrollo, editar ApplicationInsights.config en el proyecto y, a continuación, volver a implementarlo tooyour servidores.
   * Si utiliza el Monitor de estado tooinstrument una aplicación web en tiempo de ejecución, buscar ApplicationInsights.config en el directorio raíz de saludo de la aplicación hello en IIS. Actualícelo allí en cada instancia del servidor.
3. Editar directiva de recopilador de rendimiento de hello:
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

Puede capturar tanto los contadores estándar como los que ha implementado usted mismo. `\Objects\Processes` es un ejemplo de contador estándar, disponible en todos los sistemas Windows. `\Sales(photo)\# Items Sold` es un ejemplo de contador personalizado que podría implementarse en un servicio web. 

formato de Hello es `\Category(instance)\Counter"`, o en categorías que no tienen instancias, simplemente `\Category\Counter`.

`ReportAs`es necesario para los nombres de contadores que no coinciden `[a-zA-Z()/-_ \.]+` : es decir, que contienen caracteres que no están en hello siguientes conjuntos de: letras de ida y vuelta entre corchetes, barra diagonal, guión, subrayado, espacio, punto.

Si especifica una instancia, se recopilará como una dimensión "CounterInstanceName" de hello indica métrica.

### <a name="collecting-performance-counters-in-code"></a>Recopilación de contadores de rendimiento en el código
los contadores de rendimiento del sistema toocollect y enviarlos tooApplication visión, puede adaptar el siguiente fragmento de hello:


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

O bien puede hacerlo Hola lo mismo con métricas personalizadas que creó:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Contadores de rendimiento en Analytics
Puede buscar y mostrar informes de contador de rendimiento en [Analytics](app-insights-analytics.md).

Hola **performanceCounters** esquema expone hello `category`, `counter` nombre, y `instance` nombre de cada contador de rendimiento.  En la telemetría de Hola para cada aplicación, verá solo los contadores de Hola para esa aplicación. Por ejemplo, toosee qué contadores están disponibles: 

![Contadores de rendimiento en Application Insights Analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

(Aquí 'Instance' hace referencia la instancia de contador de rendimiento de toohello, no Hola instancia de máquina del servidor o rol. nombre de instancia de contador de rendimiento de Hello segmenta normalmente contadores como el tiempo de procesador por nombre de hello del proceso de Hola o la aplicación.)

tooget un gráfico de memoria disponible a través de hello período de tiempo reciente: 

![Gráfico de tiempo de la memoria in Application Insights Analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

Al igual que otros telemetría **performanceCounters** también tiene una columna `cloud_RoleInstance` que indica la identidad de Hola de instancia del servidor de host de hello en el que se ejecuta la aplicación. Por ejemplo, toocompare Hola rendimiento de la aplicación en equipos diferentes de hello: 

![Rendimiento segmentado por instancia de rol en Application Insights Analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>Recuentos de ASP.NET y Application Insights
*¿Cuál es la diferencia de hello entre la tasa de excepción de Hola y métricas de excepciones?*

* *tasa de excepciones* es un contador de rendimiento del sistema. Hola CLR cuenta todos los Hola controlan y las excepciones no controladas que se producen y total de Hola se divide en un intervalo de muestreo por longitud de Hola de intervalo de saludo. Hola Application Insights SDK recopila este resultado y lo envía toohello portal.
* *Excepciones* es un recuento de hello informes TrackException recibidos por el portal de hello en el intervalo de muestreo de saludo del gráfico de Hola. Incluye solo Hola excepciones controladas en donde haya terminado de escribir TrackException llama en el código y no incluye todos los [las excepciones no controladas](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Alertas
Al igual que otras métricas, puede [establecer una alerta](app-insights-alerts.md) toowarn si un contador de rendimiento queda fuera de un límite especifique. Abra la hoja de alertas de Hola y haga clic en Agregar alerta.

## <a name="next"></a>Pasos siguientes
* [Seguimiento de dependencias](app-insights-asp-net-dependencies.md)
* [Seguimiento de excepciones](app-insights-asp-net-exceptions.md)

