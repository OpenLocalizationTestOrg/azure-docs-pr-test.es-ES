---
title: "aaaPerformance de supervisión para las aplicaciones web de Java en Azure Application Insights | Documentos de Microsoft"
description: "Supervisión extendida del rendimiento y el uso de su sitio web de Java con Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="6b74c-103">Supervisión de dependencias, excepciones y tiempos de ejecución en aplicaciones web de Java</span><span class="sxs-lookup"><span data-stu-id="6b74c-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="6b74c-104">Si tiene [instrumentar la aplicación web de Java con Application Insights][java], puede usar Hola agente Java tooget información más detallada, sin realizar ningún cambio en el código:</span><span class="sxs-lookup"><span data-stu-id="6b74c-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="6b74c-105">**Dependencias:** datos sobre las llamadas que la aplicación realiza tooother componentes, incluido:</span><span class="sxs-lookup"><span data-stu-id="6b74c-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="6b74c-106">**Llamadas REST** realizadas a través de HttpClient, OkHttp y RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="6b74c-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="6b74c-107">**Redis** llamadas realizadas a través hello Jedis cliente.</span><span class="sxs-lookup"><span data-stu-id="6b74c-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="6b74c-108">Si llamada Hola tarda más 10s, agente de hello también captura los argumentos de llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b74c-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="6b74c-109">**[Llamadas JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**: MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB o DB Derby de Apache.</span><span class="sxs-lookup"><span data-stu-id="6b74c-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="6b74c-110">Se admiten llamadas "executeBatch".</span><span class="sxs-lookup"><span data-stu-id="6b74c-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="6b74c-111">Para MySQL y PostgreSQL, si la llamada de hello tarda más tiempo que 10s, agente de hello informa plan de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b74c-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="6b74c-112">**Excepciones detectadas:** datos sobre las excepciones que controla el código.</span><span class="sxs-lookup"><span data-stu-id="6b74c-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="6b74c-113">**Tiempo de ejecución del método:** datos sobre Hola de tiempo que tarda tooexecute determinados métodos.</span><span class="sxs-lookup"><span data-stu-id="6b74c-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="6b74c-114">agente de Java de toouse hello, instalarlo en el servidor.</span><span class="sxs-lookup"><span data-stu-id="6b74c-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="6b74c-115">Las aplicaciones web deben ser instrumentadas con hello [Application Insights Java SDK][java].</span><span class="sxs-lookup"><span data-stu-id="6b74c-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="6b74c-116">Instalar a agente de Application Insights de Hola para Java</span><span class="sxs-lookup"><span data-stu-id="6b74c-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="6b74c-117">En la máquina de hello ejecutando el servidor de Java, [descargar agente hello](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="6b74c-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="6b74c-118">Editar script de inicio de servidor de aplicación hello y agregue Hola después de JVM:</span><span class="sxs-lookup"><span data-stu-id="6b74c-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="6b74c-119">`javaagent:`*archivo JAR de ruta de acceso completa toohello agente*</span><span class="sxs-lookup"><span data-stu-id="6b74c-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="6b74c-120">Por ejemplo, en Tomcat en un equipo Linux:</span><span class="sxs-lookup"><span data-stu-id="6b74c-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="6b74c-121">Reinicie el servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6b74c-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="6b74c-122">Configurar el agente de Hola</span><span class="sxs-lookup"><span data-stu-id="6b74c-122">Configure hello agent</span></span>
<span data-ttu-id="6b74c-123">Cree un archivo denominado `AI-Agent.xml` y lo coloca en hello misma carpeta que el archivo JAR de hello agente.</span><span class="sxs-lookup"><span data-stu-id="6b74c-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="6b74c-124">Establecer Hola de contenido del archivo xml de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b74c-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="6b74c-125">Editar siguiendo tooinclude de ejemplo de Hola u omita las características de Hola que desea.</span><span class="sxs-lookup"><span data-stu-id="6b74c-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="6b74c-126">Tener tooenable informes excepción y temporización de método para los métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="6b74c-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="6b74c-127">De forma predeterminada, `reportExecutionTime` es true y `reportCaughtExceptions` es false.</span><span class="sxs-lookup"><span data-stu-id="6b74c-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="6b74c-128">Ver datos de Hola</span><span class="sxs-lookup"><span data-stu-id="6b74c-128">View hello data</span></span>
<span data-ttu-id="6b74c-129">Hola recursos de Application Insights, aparece agregados tiempos de ejecución remotos dependencia y el método [en hello rendimiento icono][metrics].</span><span class="sxs-lookup"><span data-stu-id="6b74c-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="6b74c-130">Abra toosearch para las instancias individuales de informes de dependencia, la excepción y el método, [búsqueda][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="6b74c-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="6b74c-131">[Más información sobre diagnósticos de problemas de dependencia](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="6b74c-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="6b74c-132">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="6b74c-132">Questions?</span></span> <span data-ttu-id="6b74c-133">¿Tiene problemas?</span><span class="sxs-lookup"><span data-stu-id="6b74c-133">Problems?</span></span>
* <span data-ttu-id="6b74c-134">¿No hay datos?</span><span class="sxs-lookup"><span data-stu-id="6b74c-134">No data?</span></span> [<span data-ttu-id="6b74c-135">Establezca excepciones del firewall</span><span class="sxs-lookup"><span data-stu-id="6b74c-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="6b74c-136">Solución de problemas de Java</span><span class="sxs-lookup"><span data-stu-id="6b74c-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
