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
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="9fa3f-103">Exploración de los registros de seguimiento de Java en Application Insights</span><span class="sxs-lookup"><span data-stu-id="9fa3f-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="9fa3f-104">Si usa Logback o Log4J (v1.2 o v2.0) para el seguimiento, puede que los registros de seguimiento que se envía automáticamente información que le permite explorar y buscar en ellos tooApplication.</span><span class="sxs-lookup"><span data-stu-id="9fa3f-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="9fa3f-105">Instalar Hola SDK de Java</span><span class="sxs-lookup"><span data-stu-id="9fa3f-105">Install hello Java SDK</span></span>

<span data-ttu-id="9fa3f-106">Instale el [SDK de Application Insights para Java][java], si no ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="9fa3f-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="9fa3f-107">(Si no desea que las solicitudes de tootrack HTTP, puede omitir la mayor parte del archivo de configuración .xml hello, pero debe incluir al menos hello `InstrumentationKey` elemento.</span><span class="sxs-lookup"><span data-stu-id="9fa3f-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="9fa3f-108">También debe llamar a `new TelemetryClient()` tooinitialize Hola SDK.)</span><span class="sxs-lookup"><span data-stu-id="9fa3f-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="9fa3f-109">Agregar proyecto de tooyour de bibliotecas de registro</span><span class="sxs-lookup"><span data-stu-id="9fa3f-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="9fa3f-110">*Elija la forma adecuada de hello para el proyecto.*</span><span class="sxs-lookup"><span data-stu-id="9fa3f-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="9fa3f-111">Si está usando Maven...</span><span class="sxs-lookup"><span data-stu-id="9fa3f-111">If you're using Maven...</span></span>
<span data-ttu-id="9fa3f-112">Si el proyecto ya está configurado toouse Maven de compilación, la mezcla uno Hola siguientes fragmentos de código en el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="9fa3f-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="9fa3f-113">A continuación, actualice las dependencias del proyecto de hello, archivos binarios de hello tooget descargados.</span><span class="sxs-lookup"><span data-stu-id="9fa3f-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="9fa3f-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="9fa3f-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="9fa3f-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="9fa3f-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="9fa3f-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="9fa3f-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="9fa3f-117">Si está usando Gradle...</span><span class="sxs-lookup"><span data-stu-id="9fa3f-117">If you're using Gradle...</span></span>
<span data-ttu-id="9fa3f-118">Si el proyecto ya está configurado toouse Gradle de compilación, agregue uno de hello después líneas toohello `dependencies` grupo en el archivo build.gradle:</span><span class="sxs-lookup"><span data-stu-id="9fa3f-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="9fa3f-119">A continuación, actualice las dependencias del proyecto de hello, archivos binarios de hello tooget descargados.</span><span class="sxs-lookup"><span data-stu-id="9fa3f-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="9fa3f-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="9fa3f-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="9fa3f-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="9fa3f-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="9fa3f-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="9fa3f-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="9fa3f-123">De lo contrario...</span><span class="sxs-lookup"><span data-stu-id="9fa3f-123">Otherwise ...</span></span>
<span data-ttu-id="9fa3f-124">Descargar y extraer appender adecuado de hello, a continuación, agregar Hola biblioteca adecuada tooyour proyecto:</span><span class="sxs-lookup"><span data-stu-id="9fa3f-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="9fa3f-125">Registrador</span><span class="sxs-lookup"><span data-stu-id="9fa3f-125">Logger</span></span> | <span data-ttu-id="9fa3f-126">Descargar</span><span class="sxs-lookup"><span data-stu-id="9fa3f-126">Download</span></span> | <span data-ttu-id="9fa3f-127">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="9fa3f-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9fa3f-128">Logback</span><span class="sxs-lookup"><span data-stu-id="9fa3f-128">Logback</span></span> |[<span data-ttu-id="9fa3f-129">SDK con el appender de Logback</span><span class="sxs-lookup"><span data-stu-id="9fa3f-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="9fa3f-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="9fa3f-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="9fa3f-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="9fa3f-131">Log4J v2.0</span></span> |[<span data-ttu-id="9fa3f-132">SDK con el appender de Log4J v2</span><span class="sxs-lookup"><span data-stu-id="9fa3f-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="9fa3f-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="9fa3f-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="9fa3f-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="9fa3f-134">Log4j v1.2</span></span> |[<span data-ttu-id="9fa3f-135">SDK con el appender de Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="9fa3f-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="9fa3f-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="9fa3f-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="9fa3f-137">Agregar el marco de trabajo de hello registro de tooyour appender</span><span class="sxs-lookup"><span data-stu-id="9fa3f-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="9fa3f-138">toostart obtener seguimientos, mezcla Hola relevante fragmento de código de código toohello Log4J o un archivo de configuración de Logback:</span><span class="sxs-lookup"><span data-stu-id="9fa3f-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="9fa3f-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="9fa3f-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="9fa3f-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="9fa3f-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="9fa3f-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="9fa3f-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="9fa3f-142">appenders de Application Insights Hola pueden hacer referencia a cualquier registrador configurado y no necesariamente registrador de hello raíz (como se muestra en los ejemplos de código de hello anteriores).</span><span class="sxs-lookup"><span data-stu-id="9fa3f-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="9fa3f-143">Explorar los seguimientos en el portal de Application Insights Hola</span><span class="sxs-lookup"><span data-stu-id="9fa3f-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="9fa3f-144">Ahora que ha configurado visión tooApplication realiza un seguimiento de su toosend de proyecto, puede ver y buscar estos seguimientos en el portal de Application Insights hello, Hola [búsqueda] [ diagnostic] hoja.</span><span class="sxs-lookup"><span data-stu-id="9fa3f-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![En el portal de Application Insights hello, abra búsqueda](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="9fa3f-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fa3f-146">Next steps</span></span>
<span data-ttu-id="9fa3f-147">[Búsqueda de diagnóstico][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="9fa3f-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


