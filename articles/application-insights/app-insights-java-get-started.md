---
title: "análisis de las aplicaciones web aaaJava con Azure Application Insights | Documentos de Microsoft"
description: "Supervisión del rendimiento de aplicaciones web de Java con Application Insights. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="49e58-103">Introducción a Application Insights en un proyecto web de Java</span><span class="sxs-lookup"><span data-stu-id="49e58-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="49e58-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) es un servicio de análisis extensible para los desarrolladores web que le ayuda a comprensión el rendimiento de Hola y el uso de la aplicación en vivo.</span><span class="sxs-lookup"><span data-stu-id="49e58-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="49e58-105">Usarlo demasiado[detectar y diagnosticar problemas de rendimiento y excepciones](app-insights-detect-triage-diagnose.md), y [escribir código] [ api] tootrack qué hacer un usuario con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="49e58-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![datos de ejemplo](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="49e58-107">Application Insights es compatible con aplicaciones Java que se ejecutan en Linux, Unix o Windows.</span><span class="sxs-lookup"><span data-stu-id="49e58-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="49e58-108">Necesita:</span><span class="sxs-lookup"><span data-stu-id="49e58-108">You need:</span></span>

* <span data-ttu-id="49e58-109">Oracle JRE 1.6 o posterior, o Zulu JRE 1.6 o posterior</span><span class="sxs-lookup"><span data-stu-id="49e58-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="49e58-110">Una suscripción demasiado[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="49e58-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="49e58-111">*Si tiene una aplicación web que ya está en funcionamiento, pueden ir procedimiento alternativo Hola demasiado[agregar Hola SDK en tiempo de ejecución en el servidor web de hello](app-insights-java-live.md). Esa alternativa evita volver a generar código de hello, pero no obtiene la actividad de usuario de hello opción toowrite código tootrack.*</span><span class="sxs-lookup"><span data-stu-id="49e58-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="49e58-112">1. Obtención de una clave de instrumentación de Application Insights</span><span class="sxs-lookup"><span data-stu-id="49e58-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="49e58-113">Inicie sesión en toohello [portal de Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49e58-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="49e58-114">Cree un recurso en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="49e58-114">Create an Application Insights resource.</span></span> <span data-ttu-id="49e58-115">Establezca tooJava de tipo hello aplicación aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="49e58-115">Set hello application type tooJava web application.</span></span>

    ![Rellene un nombre, elija la aplicación web de Java y haga clic en Crear.](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="49e58-117">Buscar la clave de instrumentación de Hola de nuevo recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e58-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="49e58-118">Necesitará toopaste esta clave en el proyecto de código en breve.</span><span class="sxs-lookup"><span data-stu-id="49e58-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="49e58-120">2. Agregar hello Application Insights SDK para el proyecto de Java tooyour</span><span class="sxs-lookup"><span data-stu-id="49e58-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="49e58-121">*Elija la forma adecuada de hello para el proyecto.*</span><span class="sxs-lookup"><span data-stu-id="49e58-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="49e58-122">Si está usando Eclipse toocreate un proyecto Web dinámico o Maven...</span><span class="sxs-lookup"><span data-stu-id="49e58-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="49e58-123">Hola de uso [Application Insights SDK para Java complemento][eclipse].</span><span class="sxs-lookup"><span data-stu-id="49e58-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="49e58-124">Si está usando Maven...</span><span class="sxs-lookup"><span data-stu-id="49e58-124">If you're using Maven...</span></span>
<span data-ttu-id="49e58-125">Si el proyecto ya está configurado toouse Maven de compilación, combine Hola siguiente archivo de código tooyour pom.xml.</span><span class="sxs-lookup"><span data-stu-id="49e58-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="49e58-126">A continuación, descargan tooget Hola binarios de actualización Hola proyecto dependencias.</span><span class="sxs-lookup"><span data-stu-id="49e58-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="49e58-127">*¿Errores de validación en la suma de comprobación o la compilación?*</span><span class="sxs-lookup"><span data-stu-id="49e58-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="49e58-128">Pruebe en su lugar una versión específica, como:`<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="49e58-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="49e58-129">Encontrará la versión más reciente de Hola Hola [notas de la versión de SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) o en nuestros [artefactos de Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="49e58-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="49e58-130">*¿Necesita tooupdate tooa nuevo SDK?*</span><span class="sxs-lookup"><span data-stu-id="49e58-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="49e58-131">Actualice las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="49e58-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="49e58-132">Si está usando Gradle...</span><span class="sxs-lookup"><span data-stu-id="49e58-132">If you're using Gradle...</span></span>
<span data-ttu-id="49e58-133">Si el proyecto ya está configurado toouse Gradle de compilación, la mezcla Hola siguiente archivo de código tooyour build.gradle.</span><span class="sxs-lookup"><span data-stu-id="49e58-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="49e58-134">Luego se descargarán tooget Hola binarios de actualización Hola proyecto dependencias.</span><span class="sxs-lookup"><span data-stu-id="49e58-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="49e58-135">*¿Errores de validación de suma de comprobación o de compilación? Utilice en su lugar una versión específica, como:* `version:'1.0.n'`</span><span class="sxs-lookup"><span data-stu-id="49e58-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="49e58-136">*Encontrará la versión más reciente de Hola Hola [notas de la versión de SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="49e58-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="49e58-137">*tooupdate tooa nuevo SDK*</span><span class="sxs-lookup"><span data-stu-id="49e58-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="49e58-138">Actualice las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="49e58-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="49e58-139">De lo contrario...</span><span class="sxs-lookup"><span data-stu-id="49e58-139">Otherwise ...</span></span>
<span data-ttu-id="49e58-140">Agregar manualmente Hola SDK:</span><span class="sxs-lookup"><span data-stu-id="49e58-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="49e58-141">Descargar hello [Application Insights SDK para Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="49e58-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="49e58-142">Extraer los archivos binarios de Hola de archivo zip de Hola y agréguelos tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="49e58-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="49e58-143">Preguntas...</span><span class="sxs-lookup"><span data-stu-id="49e58-143">Questions...</span></span>
* <span data-ttu-id="49e58-144">*¿Cuál es la relación de hello entre hello `-core` y `-web` componentes en zip Hola?*</span><span class="sxs-lookup"><span data-stu-id="49e58-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="49e58-145">`applicationinsights-core`Encontrará Hola reconstrucción API.</span><span class="sxs-lookup"><span data-stu-id="49e58-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="49e58-146">Este componente se necesita siempre.</span><span class="sxs-lookup"><span data-stu-id="49e58-146">You always need this component.</span></span>
  * <span data-ttu-id="49e58-147">`applicationinsights-web` proporciona métricas que realizan el seguimiento de recuentos de solicitud HTTP y tiempos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="49e58-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="49e58-148">Este componente se puede omitir si no se desea que se recopilen automáticamente los datos de esta telemetría.</span><span class="sxs-lookup"><span data-stu-id="49e58-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="49e58-149">Por ejemplo, si desea que toowrite sus propios.</span><span class="sxs-lookup"><span data-stu-id="49e58-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="49e58-150">*Hola tooupdate SDK cuando se publican los cambios*</span><span class="sxs-lookup"><span data-stu-id="49e58-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="49e58-151">Descargar más reciente hello [Application Insights SDK para Java](https://aka.ms/qqkaq6) y reemplazar Hola los antiguos.</span><span class="sxs-lookup"><span data-stu-id="49e58-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="49e58-152">Se describen los cambios en hello [notas de la versión de SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="49e58-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="49e58-153">3. Adición de un archivo .xml de Application Insights</span><span class="sxs-lookup"><span data-stu-id="49e58-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="49e58-154">Agregar carpeta de recursos de ApplicationInsights.xml toohello en el proyecto, o asegúrese de que se agrega la ruta de clase de implementación del proyecto tooyour.</span><span class="sxs-lookup"><span data-stu-id="49e58-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="49e58-155">Copie Hola continuación de XML en ella.</span><span class="sxs-lookup"><span data-stu-id="49e58-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="49e58-156">Sustituya la clave de instrumentación de Hola que obtuvo en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="49e58-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

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


* <span data-ttu-id="49e58-157">clave de instrumentación de Hola se envía junto con todos los elementos de telemetría e indica toodisplay Application Insights en el recurso.</span><span class="sxs-lookup"><span data-stu-id="49e58-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="49e58-158">Hola componente de la solicitud HTTP es opcional.</span><span class="sxs-lookup"><span data-stu-id="49e58-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="49e58-159">Envía automáticamente telemetría sobre las solicitudes y portal de toohello de tiempos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="49e58-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="49e58-160">Correlación de eventos es un componente de solicitud de incorporación toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="49e58-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="49e58-161">Asigna una identificador tooeach las solicitudes recibidas por server hello y agrega este identificador como un elemento de propiedad tooevery de telemetría como propiedad de hello 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="49e58-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="49e58-162">Le permite la telemetría de hello toocorrelate asociado con cada solicitud estableciendo un filtro [búsqueda diagnóstico][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="49e58-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="49e58-163">clave de Application Insights Hola puede pasarse dinámicamente desde Hola portal de Azure como una propiedad del sistema (-DAPPLICATION_INSIGHTS_IKEY = your_ikey).</span><span class="sxs-lookup"><span data-stu-id="49e58-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="49e58-164">Si no hay ninguna propiedad definida, busca la variable de entorno (APPLICATION_INSIGHTS_IKEY) en la configuración de las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="49e58-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="49e58-165">Si ambas propiedades hello no están definidos, se usa Hola predeterminado InstrumentationKey desde ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="49e58-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="49e58-166">Esta secuencia ayuda a toomanage InstrumentationKeys distintos para diferentes entornos dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="49e58-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="49e58-167">Clave de instrumentación de formas alternativas tooset Hola</span><span class="sxs-lookup"><span data-stu-id="49e58-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="49e58-168">Application Insights SDK busca clave hello en este orden:</span><span class="sxs-lookup"><span data-stu-id="49e58-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="49e58-169">Propiedad del sistema:-DAPPLICATION_INSIGHTS_IKEY = your_ikey</span><span class="sxs-lookup"><span data-stu-id="49e58-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="49e58-170">Variable de entorno: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="49e58-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="49e58-171">Archivo de configuración: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="49e58-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="49e58-172">También se puede [configurar en el código](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="49e58-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="49e58-173">4. Adición de un filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="49e58-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="49e58-174">último paso de configuración Hola permite Hola HTTP solicitud componente toolog cada solicitud web.</span><span class="sxs-lookup"><span data-stu-id="49e58-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="49e58-175">(No es necesario si desea simplemente API reconstrucción Hola.)</span><span class="sxs-lookup"><span data-stu-id="49e58-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="49e58-176">Busque y abra el archivo web.xml de hello en el proyecto y Hola de combinación siguiente código bajo el nodo de la aplicación web de hello, donde se configuran los filtros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="49e58-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="49e58-177">resultados más precisos tooget hello, filtro de hello deben asignarse antes de todos los demás filtros.</span><span class="sxs-lookup"><span data-stu-id="49e58-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="49e58-178">Si utiliza Spring Web MVC 3.1, o cualquier versión posterior</span><span class="sxs-lookup"><span data-stu-id="49e58-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="49e58-179">Editar estos elementos en *-paquete de Application Insights de servlet.xml tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="49e58-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="49e58-180">Si está usando Struts 2</span><span class="sxs-lookup"><span data-stu-id="49e58-180">If you're using Struts 2</span></span>
<span data-ttu-id="49e58-181">Agregue este archivo de configuración de elemento toohello Struts (generalmente denominado struts.xml o struts default.xml):</span><span class="sxs-lookup"><span data-stu-id="49e58-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="49e58-182">(Si tiene interceptores definidos en una pila de manera predeterminada, el interceptor de hello puede simplemente agregarán toothat pila).</span><span class="sxs-lookup"><span data-stu-id="49e58-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="49e58-183">5. Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="49e58-183">5. Run your application</span></span>
<span data-ttu-id="49e58-184">Ejecutar en modo de depuración en el equipo de desarrollo, o publicar tooyour server.</span><span class="sxs-lookup"><span data-stu-id="49e58-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="49e58-185">6. Visualización de la telemetría en Application Insights</span><span class="sxs-lookup"><span data-stu-id="49e58-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="49e58-186">Devolver recurso de Application Insights tooyour en [portal de Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49e58-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="49e58-187">Datos de las solicitudes HTTP aparecen en la hoja de información general de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e58-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="49e58-188">(Si todavía no está ahí, espere unos segundos y, a continuación, haga clic en Actualizar).</span><span class="sxs-lookup"><span data-stu-id="49e58-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![datos de ejemplo](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="49e58-190">[Más información acerca de las métricas.][metrics]</span><span class="sxs-lookup"><span data-stu-id="49e58-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="49e58-191">Click-through cualquier toosee gráfico más detallada agrega métricas.</span><span class="sxs-lookup"><span data-stu-id="49e58-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="49e58-192">Visión de la aplicación, se da por supuesto formato Hola de solicitudes HTTP que las aplicaciones MVC es: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="49e58-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="49e58-193">Por ejemplo, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` y `GET Home/Product/sdf96vws` se agrupan en `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="49e58-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="49e58-194">Esta agrupación permite agregaciones significativas de solicitudes, como el número de solicitudes y el tiempo medio de ejecución de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="49e58-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="49e58-195">Datos de instancia</span><span class="sxs-lookup"><span data-stu-id="49e58-195">Instance data</span></span>
<span data-ttu-id="49e58-196">Click-through de una solicitud específica escriba toosee las instancias individuales.</span><span class="sxs-lookup"><span data-stu-id="49e58-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="49e58-197">Se muestran dos tipos de datos en Application Insights: datos agregados, almacenados y mostrados como promedios, recuentos y sumas; y datos de instancia, como informes individuales de las solicitudes HTTP, excepciones, vistas de página o eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="49e58-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="49e58-198">Al ver las propiedades de Hola de una solicitud, puede ver eventos de telemetría de hello asociados con él, como las solicitudes y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="49e58-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="49e58-199">Analytics: Lenguaje de consulta eficaz</span><span class="sxs-lookup"><span data-stu-id="49e58-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="49e58-200">Dado que acumulan más datos, puede ejecutar consultas en ambas instancias de tooaggregate toofind y de datos individuales.</span><span class="sxs-lookup"><span data-stu-id="49e58-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="49e58-201">[Analytics](app-insights-analytics.md) es una eficaz herramienta tanto para conocer el rendimiento y el uso, como para el diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="49e58-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Ejemplo de Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="49e58-203">7. Instale la aplicación en el servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="49e58-203">7. Install your app on hello server</span></span>
<span data-ttu-id="49e58-204">Publicar ahora el servidor de toohello de aplicación, permitir a los usuarios usar e inspeccionar telemetría Hola aparezca en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e58-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="49e58-205">Asegúrese de que el firewall permite la aplicación toosend puertos toothese de telemetría:</span><span class="sxs-lookup"><span data-stu-id="49e58-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="49e58-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="49e58-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="49e58-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="49e58-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="49e58-208">Si el tráfico saliente debe enrutarse a través de un firewall, defina las propiedades de sistema `http.proxyHost` y `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="49e58-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="49e58-209">En los servidores de Windows, instale:</span><span class="sxs-lookup"><span data-stu-id="49e58-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="49e58-210">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="49e58-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="49e58-211">(Este componente habilita los contadores de rendimiento.)</span><span class="sxs-lookup"><span data-stu-id="49e58-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="49e58-212">Excepciones y errores de solicitud</span><span class="sxs-lookup"><span data-stu-id="49e58-212">Exceptions and request failures</span></span>
<span data-ttu-id="49e58-213">Las excepciones no controladas se recopilan automáticamente:</span><span class="sxs-lookup"><span data-stu-id="49e58-213">Unhandled exceptions are automatically collected:</span></span>

![Abra Configuración, Errores](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="49e58-215">toocollect datos en otras excepciones, tienes dos opciones:</span><span class="sxs-lookup"><span data-stu-id="49e58-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="49e58-216">[Insertar llamadas tootrackException() en su código][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="49e58-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="49e58-217">[Instalar agente Java hello en el servidor](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="49e58-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="49e58-218">Especificar métodos de Hola que desee toowatch.</span><span class="sxs-lookup"><span data-stu-id="49e58-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="49e58-219">Supervisión de llamadas a métodos y dependencias externas</span><span class="sxs-lookup"><span data-stu-id="49e58-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="49e58-220">[Instalar agente Java hello](app-insights-java-agent.md) toolog especifica métodos internos y las llamadas realizadas a través de JDBC, con datos de tiempo.</span><span class="sxs-lookup"><span data-stu-id="49e58-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="49e58-221">Contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="49e58-221">Performance counters</span></span>
<span data-ttu-id="49e58-222">Abra **configuración**, **servidores**, toosee un intervalo de los contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="49e58-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="49e58-223">Personalizar la recopilación de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="49e58-223">Customize performance counter collection</span></span>
<span data-ttu-id="49e58-224">colección de toodisable del conjunto estándar de Hola de contadores de rendimiento, agregar Hola siguiente código en el nodo raíz de Hola de archivo de hello ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="49e58-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="49e58-225">Recopilar contadores de rendimiento adicionales</span><span class="sxs-lookup"><span data-stu-id="49e58-225">Collect additional performance counters</span></span>
<span data-ttu-id="49e58-226">Puede especificar toobe de contadores de rendimiento adicionales recopilados.</span><span class="sxs-lookup"><span data-stu-id="49e58-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="49e58-227">Contadores JMX (expuestos por máquina Virtual Java de hello)</span><span class="sxs-lookup"><span data-stu-id="49e58-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="49e58-228">`displayName`: nombre de hello mostrado en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="49e58-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="49e58-229">`objectName`: nombre de objeto JMX Hola.</span><span class="sxs-lookup"><span data-stu-id="49e58-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="49e58-230">`attribute`: atributo Hola de hello JMX objeto nombre toofetch</span><span class="sxs-lookup"><span data-stu-id="49e58-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="49e58-231">`type`(opcional): Hola tipo de atributo del objeto JMX:</span><span class="sxs-lookup"><span data-stu-id="49e58-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="49e58-232">Valor predeterminado: un tipo simple como int o long.</span><span class="sxs-lookup"><span data-stu-id="49e58-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="49e58-233">`composite`: datos de contador de rendimiento de hello están en formato de Hola de 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="49e58-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="49e58-234">`tabular`: datos de contador de rendimiento de hello están en formato de Hola de una fila de tabla</span><span class="sxs-lookup"><span data-stu-id="49e58-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="49e58-235">Contadores de rendimiento de Windows</span><span class="sxs-lookup"><span data-stu-id="49e58-235">Windows performance counters</span></span>
<span data-ttu-id="49e58-236">Cada [contador de rendimiento de Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) es un miembro de una categoría (Hola igual que un campo es un miembro de una clase).</span><span class="sxs-lookup"><span data-stu-id="49e58-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="49e58-237">Las categorías puede ser globales, o pueden tener instancias con nombre o numeradas.</span><span class="sxs-lookup"><span data-stu-id="49e58-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="49e58-238">displayName: nombre de hello mostrado en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="49e58-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="49e58-239">categoryName: Hola categoría contador de rendimiento (objeto de rendimiento) al que está asociado este contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="49e58-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="49e58-240">counterName: nombre de Hola Hola del contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="49e58-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="49e58-241">instanceName: Hola nombre de instancia de categoría de contador de rendimiento de Hola o una cadena vacía (""), si la categoría de hello contiene una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="49e58-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="49e58-242">Si Hola categoryName es el proceso y le gustaría toocollect del contador de rendimiento hello es proceso JVM actual de hello en que se ejecuta la aplicación, especifique `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="49e58-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="49e58-243">Los contadores de rendimiento están visibles como métricas personalizadas en el [Explorador de métricas][metrics].</span><span class="sxs-lookup"><span data-stu-id="49e58-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="49e58-244">Contadores de rendimiento de Unix</span><span class="sxs-lookup"><span data-stu-id="49e58-244">Unix performance counters</span></span>
* <span data-ttu-id="49e58-245">[Instalar collectd con el complemento de Application Insights hello](app-insights-java-collectd.md) tooget una amplia variedad de datos del sistema y de red.</span><span class="sxs-lookup"><span data-stu-id="49e58-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="49e58-246">Obtención de datos de usuario y sesión</span><span class="sxs-lookup"><span data-stu-id="49e58-246">Get user and session data</span></span>
<span data-ttu-id="49e58-247">Bien, va a enviar telemetría desde el servidor web.</span><span class="sxs-lookup"><span data-stu-id="49e58-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="49e58-248">Ahora tooget Hola vista de 360 grados completa de la aplicación, puede agregar más supervisión:</span><span class="sxs-lookup"><span data-stu-id="49e58-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="49e58-249">[Agregar páginas web de telemetría tooyour] [ usage] toomonitor página vistas y las métricas de usuario.</span><span class="sxs-lookup"><span data-stu-id="49e58-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="49e58-250">[Configurar las pruebas web] [ availability] toomake seguro de la aplicación permanece en vivo y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="49e58-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="49e58-251">Captura de seguimiento de registros</span><span class="sxs-lookup"><span data-stu-id="49e58-251">Capture log traces</span></span>
<span data-ttu-id="49e58-252">Puede usar Application Insights tooslice y reorganizar los registros de Log4J, Logback u otros marcos de registro.</span><span class="sxs-lookup"><span data-stu-id="49e58-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="49e58-253">Puede correlacionar los registros de hello con las solicitudes HTTP y otro telemetría.</span><span class="sxs-lookup"><span data-stu-id="49e58-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="49e58-254">[Vea cómo][javalogs].</span><span class="sxs-lookup"><span data-stu-id="49e58-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="49e58-255">Envío de su propia telemetría</span><span class="sxs-lookup"><span data-stu-id="49e58-255">Send your own telemetry</span></span>
<span data-ttu-id="49e58-256">Ahora que ha instalado Hola SDK, puede usar Hola API toosend su propio telemetría.</span><span class="sxs-lookup"><span data-stu-id="49e58-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="49e58-257">[Realizar un seguimiento de eventos personalizados y las métricas] [ api] toolearn hacen lo que los usuarios con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="49e58-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="49e58-258">[Buscar eventos y registros] [ diagnostic] toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="49e58-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="49e58-259">Pruebas web de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="49e58-259">Availability web tests</span></span>
<span data-ttu-id="49e58-260">Application Insights pueden probar su sitio Web en intervalos regulares toocheck que está en funcionamiento y responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="49e58-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="49e58-261">[tooset una][availability], haga clic en las pruebas Web.</span><span class="sxs-lookup"><span data-stu-id="49e58-261">[tooset up][availability], click Web tests.</span></span>

![Haga clic en Pruebas web y luego en Agregar prueba web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="49e58-263">Obtendrá gráficos de tiempos de respuesta, junto con notificaciones por correo electrónico si su sitio deja de funcionar.</span><span class="sxs-lookup"><span data-stu-id="49e58-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Ejemplo de prueba web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="49e58-265">[Más información acerca de las pruebas web de disponibilidad.][availability]</span><span class="sxs-lookup"><span data-stu-id="49e58-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="49e58-266">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="49e58-266">Questions?</span></span> <span data-ttu-id="49e58-267">¿Tiene problemas?</span><span class="sxs-lookup"><span data-stu-id="49e58-267">Problems?</span></span>
[<span data-ttu-id="49e58-268">Solución de problemas de Java</span><span class="sxs-lookup"><span data-stu-id="49e58-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="49e58-269">Vídeo</span><span class="sxs-lookup"><span data-stu-id="49e58-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="49e58-270">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49e58-270">Next steps</span></span>
* [<span data-ttu-id="49e58-271">Supervisión de llamadas a dependencias</span><span class="sxs-lookup"><span data-stu-id="49e58-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="49e58-272">Supervisión de contadores de rendimiento de Unix</span><span class="sxs-lookup"><span data-stu-id="49e58-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="49e58-273">Agregar [tooyour las páginas web de supervisión](app-insights-javascript.md) tiempo de carga de la página de toomonitor, llamadas de AJAX, excepciones de explorador.</span><span class="sxs-lookup"><span data-stu-id="49e58-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="49e58-274">Escribir [telemetría personalizada](app-insights-api-custom-events-metrics.md) tootrack uso en el Explorador de Hola o en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="49e58-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="49e58-275">Crear [paneles](app-insights-dashboards.md) gráficos de clave toobring Hola juntos para supervisar el sistema.</span><span class="sxs-lookup"><span data-stu-id="49e58-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="49e58-276">Uso de [Analytics](app-insights-analytics.md) para realizar consultas eficaces sobre los datos de telemetría de la aplicación</span><span class="sxs-lookup"><span data-stu-id="49e58-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="49e58-277">Para más información, visite [Azure para desarrolladores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="49e58-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
