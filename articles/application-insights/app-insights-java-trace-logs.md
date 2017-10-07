---
title: registros de aaaExplore seguimiento de Java en Azure Application Insights | Documentos de Microsoft
description: "Búsqueda de seguimiento Log4J o Logback en Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a>Exploración de los registros de seguimiento de Java en Application Insights
Si usa Logback o Log4J (v1.2 o v2.0) para el seguimiento, puede que los registros de seguimiento que se envía automáticamente información que le permite explorar y buscar en ellos tooApplication.

## <a name="install-hello-java-sdk"></a>Instalar Hola SDK de Java

Instale el [SDK de Application Insights para Java][java], si no ha hecho ya.

(Si no desea que las solicitudes de tootrack HTTP, puede omitir la mayor parte del archivo de configuración .xml hello, pero debe incluir al menos hello `InstrumentationKey` elemento. También debe llamar a `new TelemetryClient()` tooinitialize Hola SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Agregar proyecto de tooyour de bibliotecas de registro
*Elija la forma adecuada de hello para el proyecto.*

#### <a name="if-youre-using-maven"></a>Si está usando Maven...
Si el proyecto ya está configurado toouse Maven de compilación, la mezcla uno Hola siguientes fragmentos de código en el archivo pom.xml.

A continuación, actualice las dependencias del proyecto de hello, archivos binarios de hello tooget descargados.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Si está usando Gradle...
Si el proyecto ya está configurado toouse Gradle de compilación, agregue uno de hello después líneas toohello `dependencies` grupo en el archivo build.gradle:

A continuación, actualice las dependencias del proyecto de hello, archivos binarios de hello tooget descargados.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J v1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>De lo contrario...
Descargar y extraer appender adecuado de hello, a continuación, agregar Hola biblioteca adecuada tooyour proyecto:

| Registrador | Descargar | Biblioteca |
| --- | --- | --- |
| Logback |[SDK con el appender de Logback](https://aka.ms/xt62a4) |applicationinsights-logging-logback |
| Log4J v2.0 |[SDK con el appender de Log4J v2](https://aka.ms/qypznq) |applicationinsights-logging-log4j2 |
| Log4J v1.2 |[SDK con el appender de Log4J v1.2](https://aka.ms/ky9cbo) |applicationinsights-logging-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Agregar el marco de trabajo de hello registro de tooyour appender
toostart obtener seguimientos, mezcla Hola relevante fragmento de código de código toohello Log4J o un archivo de configuración de Logback: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

*Log4J v1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

appenders de Application Insights Hola pueden hacer referencia a cualquier registrador configurado y no necesariamente registrador de hello raíz (como se muestra en los ejemplos de código de hello anteriores).

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Explorar los seguimientos en el portal de Application Insights Hola
Ahora que ha configurado visión tooApplication realiza un seguimiento de su toosend de proyecto, puede ver y buscar estos seguimientos en el portal de Application Insights hello, Hola [búsqueda] [ diagnostic] hoja.

![En el portal de Application Insights hello, abra búsqueda](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Pasos siguientes
[Búsqueda de diagnóstico][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


