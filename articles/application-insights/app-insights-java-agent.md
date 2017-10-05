---
title: "Supervisión de rendimiento de aplicaciones web de Java en Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="ca3ed-103">Supervisión de dependencias, excepciones y tiempos de ejecución en aplicaciones web de Java</span><span class="sxs-lookup"><span data-stu-id="ca3ed-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="ca3ed-104">Si ha [instrumentado la aplicación web de Java con Application Insights][java], puede usar el agente de Java para obtener información más clara, sin tener que realizar cambios de código:</span><span class="sxs-lookup"><span data-stu-id="ca3ed-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="ca3ed-105">**Dependencias:** datos sobre las llamadas realizadas por la aplicación a otros componentes, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ca3ed-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="ca3ed-106">**Llamadas REST** realizadas a través de HttpClient, OkHttp y RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="ca3ed-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="ca3ed-107">**Redis** llamadas realizadas a través del cliente de Jedis.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="ca3ed-108">Si la llamada tarda más de 10 s, el agente captura también los argumentos de la llamada.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="ca3ed-109">**[Llamadas JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**: MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB o DB Derby de Apache.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="ca3ed-110">Se admiten llamadas "executeBatch".</span><span class="sxs-lookup"><span data-stu-id="ca3ed-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="ca3ed-111">En el caso de MySQL y PostgreSQL, si la llamada tarda más de 10 s, el agente notifica el plan de consulta.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="ca3ed-112">**Excepciones detectadas:** datos sobre las excepciones que controla el código.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="ca3ed-113">**Tiempo de ejecución del método:** datos sobre el tiempo necesario para ejecutar métodos específicos.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="ca3ed-114">Para usar el agente de Java, debe instalarlo en el servidor.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="ca3ed-115">Las aplicaciones web deben instrumentarse con el [SDK de Application Insights para Java][java].</span><span class="sxs-lookup"><span data-stu-id="ca3ed-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="ca3ed-116">Instalación del agente de Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="ca3ed-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="ca3ed-117">[Descargue el agente](https://aka.ms/aijavasdk)en la máquina que ejecuta el servidor de Java.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="ca3ed-118">Edite el script de inicio del servidor de aplicaciones y agregue la siguiente JVM:</span><span class="sxs-lookup"><span data-stu-id="ca3ed-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="ca3ed-119">`javaagent:`*ruta de acceso completa al archivo JAR del agente*</span><span class="sxs-lookup"><span data-stu-id="ca3ed-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="ca3ed-120">Por ejemplo, en Tomcat en un equipo Linux:</span><span class="sxs-lookup"><span data-stu-id="ca3ed-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="ca3ed-121">Reinicie el servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="ca3ed-122">Configuración del agente</span><span class="sxs-lookup"><span data-stu-id="ca3ed-122">Configure the agent</span></span>
<span data-ttu-id="ca3ed-123">Cree un archivo denominado `AI-Agent.xml` y colóquelo en la misma carpeta que el archivo JAR del agente.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="ca3ed-124">Establezca el contenido del archivo XML.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-124">Set the content of the xml file.</span></span> <span data-ttu-id="ca3ed-125">Edite el ejemplo siguiente para incluir u omitir las características que desee.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="ca3ed-126">Debe habilitar la excepción de los informes y los intervalos de método para métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="ca3ed-127">De forma predeterminada, `reportExecutionTime` es true y `reportCaughtExceptions` es false.</span><span class="sxs-lookup"><span data-stu-id="ca3ed-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="ca3ed-128">Visualización de los datos</span><span class="sxs-lookup"><span data-stu-id="ca3ed-128">View the data</span></span>
<span data-ttu-id="ca3ed-129">En el recurso de Application Insights, aparecen tiempos de ejecución agregados de métodos y dependencias remotos [en el icono Rendimiento][metrics].</span><span class="sxs-lookup"><span data-stu-id="ca3ed-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="ca3ed-130">Para buscar instancias individuales de informes de dependencia, excepción y método, abra [Buscar][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="ca3ed-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="ca3ed-131">[Más información sobre diagnósticos de problemas de dependencia](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="ca3ed-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="ca3ed-132">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="ca3ed-132">Questions?</span></span> <span data-ttu-id="ca3ed-133">¿Tiene problemas?</span><span class="sxs-lookup"><span data-stu-id="ca3ed-133">Problems?</span></span>
* <span data-ttu-id="ca3ed-134">¿No hay datos?</span><span class="sxs-lookup"><span data-stu-id="ca3ed-134">No data?</span></span> [<span data-ttu-id="ca3ed-135">Establezca excepciones del firewall</span><span class="sxs-lookup"><span data-stu-id="ca3ed-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="ca3ed-136">Solución de problemas de Java</span><span class="sxs-lookup"><span data-stu-id="ca3ed-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
