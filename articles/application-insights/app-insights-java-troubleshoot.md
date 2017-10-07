---
title: aaaTroubleshoot Application Insights en un proyecto web de Java
description: "Guía de solución de problemas: supervisión de aplicaciones activas Java con Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="4641b-103">Solución de problemas y preguntas y respuestas sobre Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="4641b-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="4641b-104">Preguntas o problemas relacionados con [Azure Application Insights en Java][java].</span><span class="sxs-lookup"><span data-stu-id="4641b-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="4641b-105">a continuación se incluyen algunas sugerencias.</span><span class="sxs-lookup"><span data-stu-id="4641b-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="4641b-106">Errores de compilación</span><span class="sxs-lookup"><span data-stu-id="4641b-106">Build errors</span></span>
<span data-ttu-id="4641b-107">**En Eclipse, cuando Agregar Hola Application Insights SDK a través de Maven o Gradle, puede obtener errores de validación de suma de comprobación o de compilación.**</span><span class="sxs-lookup"><span data-stu-id="4641b-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="4641b-108">Si Hola dependencia <version> elemento está usando un patrón con caracteres comodín (por ejemplo, (Maven) `<version>[1.0,)</version>` o (Gradle) `version:'1.0.+'`), pruebe a especificar una versión específica en su lugar como `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="4641b-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="4641b-109">Vea hello [notas de la versión](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) para la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4641b-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="4641b-110">No aparecen datos</span><span class="sxs-lookup"><span data-stu-id="4641b-110">No data</span></span>
<span data-ttu-id="4641b-111">**He agregado Application Insights correctamente y se ejecutó la aplicación, pero nunca he visto datos en el portal de Hola.**</span><span class="sxs-lookup"><span data-stu-id="4641b-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="4641b-112">Espere un minuto y haga clic en Actualizar,</span><span class="sxs-lookup"><span data-stu-id="4641b-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="4641b-113">gráficos de Hello actualización por sí mismas periódicamente, pero también puede actualizar manualmente.</span><span class="sxs-lookup"><span data-stu-id="4641b-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="4641b-114">intervalo de actualización de Hello depende del intervalo de tiempo de hello del gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="4641b-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="4641b-115">Compruebe que tiene una clave de instrumentación definida en hello ApplicationInsights.xml archivo (en la carpeta de recursos de hello en el proyecto)</span><span class="sxs-lookup"><span data-stu-id="4641b-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="4641b-116">Compruebe que no hay ningún `<DisableTelemetry>true</DisableTelemetry>` nodo en el archivo xml de hello.</span><span class="sxs-lookup"><span data-stu-id="4641b-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="4641b-117">En el firewall, es posible que tenga tooopen los puertos TCP 80 y 443 para toodc.services.visualstudio.com de tráfico saliente. Vea hello [lista completa de las excepciones del firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="4641b-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="4641b-118">En Microsoft Azure Hola iniciar panel, examine mapa de estado del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4641b-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="4641b-119">Si hay alguna alerta indicaciones, espere hasta que hayan devuelto tooOK y, a continuación, cierre y vuelva a abrir la hoja de la aplicación Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4641b-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="4641b-120">Activar el registro toohello la ventana de consola del IDE, mediante la adición de un `<SDKLogger />` elemento bajo el nodo de raíz de hello en el archivo de hello ApplicationInsights.xml (en la carpeta de recursos de hello en el proyecto) y busque las entradas que se prologa con [Error].</span><span class="sxs-lookup"><span data-stu-id="4641b-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="4641b-121">Asegúrese de que ese Hola correcto ApplicationInsights.xml archivo se ha cargado correctamente por hello SDK de Java, examinando los mensajes de salida de la consola de Hola para una instrucción "archivo de configuración se encontró correctamente".</span><span class="sxs-lookup"><span data-stu-id="4641b-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="4641b-122">Si no se encuentra el archivo de configuración de hello, compruebe toosee de mensajes de salida de hello donde se busca el archivo de configuración de Hola y asegúrese de que ese hello que applicationinsights.XML se encuentra en una de esas ubicaciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4641b-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="4641b-123">Como regla general, puede colocar el archivo de configuración de hello cerca Hola aplicación visión SDK JAR.</span><span class="sxs-lookup"><span data-stu-id="4641b-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="4641b-124">Por ejemplo: en Tomcat, esto significaría Hola carpeta WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="4641b-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="4641b-125">He usado toosee datos, pero se ha detenido</span><span class="sxs-lookup"><span data-stu-id="4641b-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="4641b-126">Comprobar hello [estado blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="4641b-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="4641b-127">¿Ha alcanzado su cuota mensual de puntos de datos?</span><span class="sxs-lookup"><span data-stu-id="4641b-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="4641b-128">Abra Configuración/cuotas y precios toofind out. Si es así, puede actualizar el plan o pagar para obtener capacidad adicional.</span><span class="sxs-lookup"><span data-stu-id="4641b-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="4641b-129">Vea hello [precios esquema](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="4641b-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="4641b-130">No veo todos los datos de hello que estoy esperando</span><span class="sxs-lookup"><span data-stu-id="4641b-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="4641b-131">Abra hello las cuotas y precios hoja y compruebe si [muestreo](app-insights-sampling.md) está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="4641b-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="4641b-132">(transmisión de 100% significa que muestreo no está en funcionamiento). Hola servicio Application Insights puede ser conjunto tooaccept sólo una fracción de telemetría de Hola que llega desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4641b-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="4641b-133">Esto le ayuda a mantenerse en su cuota mensual de telemetría.</span><span class="sxs-lookup"><span data-stu-id="4641b-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="4641b-134">No aparecen datos de uso</span><span class="sxs-lookup"><span data-stu-id="4641b-134">No usage data</span></span>
<span data-ttu-id="4641b-135">**Veo datos sobre solicitudes y tiempos de respuesta, pero no de vista de página, del explorador o de datos de usuarios.**</span><span class="sxs-lookup"><span data-stu-id="4641b-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="4641b-136">Ha configurado correctamente la la telemetría de toosend de aplicación desde el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4641b-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="4641b-137">Ahora el siguiente paso es demasiado[configurar la telemetría de toosend de páginas web desde el Explorador de web de hello][usage].</span><span class="sxs-lookup"><span data-stu-id="4641b-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="4641b-138">Como alternativa, si el cliente es una aplicación de [teléfono o de cualquier otro dispositivo][platforms], puede enviar datos de telemetría desde este.</span><span class="sxs-lookup"><span data-stu-id="4641b-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="4641b-139">Use Hola mismo tooset clave de instrumentación la telemetría de su cliente y el servidor.</span><span class="sxs-lookup"><span data-stu-id="4641b-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="4641b-140">datos de Hello aparecerán en Hola mismo recurso de Application Insights y podrá toocorrelate capaz de eventos de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="4641b-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="4641b-141">Deshabilitación de la telemetría</span><span class="sxs-lookup"><span data-stu-id="4641b-141">Disabling telemetry</span></span>
<span data-ttu-id="4641b-142">**¿Cómo puedo deshabilitar la recopilación de telemetría?**</span><span class="sxs-lookup"><span data-stu-id="4641b-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="4641b-143">En el código:</span><span class="sxs-lookup"><span data-stu-id="4641b-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="4641b-144">**O**</span><span class="sxs-lookup"><span data-stu-id="4641b-144">**Or**</span></span> 

<span data-ttu-id="4641b-145">Actualizar ApplicationInsights.xml (en la carpeta de recursos de hello en el proyecto).</span><span class="sxs-lookup"><span data-stu-id="4641b-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="4641b-146">Agregue los siguiente hello en el nodo raíz de hello:</span><span class="sxs-lookup"><span data-stu-id="4641b-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="4641b-147">Mediante el método XML de hello, tendrá que aplicación de hello toorestart cuando se cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4641b-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="4641b-148">Cambiar el destino de Hola</span><span class="sxs-lookup"><span data-stu-id="4641b-148">Changing hello target</span></span>
<span data-ttu-id="4641b-149">**¿Cómo puedo cambiar el recurso de Azure al que mi proyecto envía datos?**</span><span class="sxs-lookup"><span data-stu-id="4641b-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="4641b-150">[Obtener clave de instrumentación de Hola de nuevo recurso de Hola.][java]</span><span class="sxs-lookup"><span data-stu-id="4641b-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="4641b-151">Si agrega el proyecto de tooyour de Application Insights mediante hello Azure Toolkit for Eclipse, haga clic con el proyecto web, seleccione **Azure**, **configurar Application Insights**y cambiar la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="4641b-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="4641b-152">En caso contrario, actualizar la clave de Hola de ApplicationInsights.xml en la carpeta de recursos de hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4641b-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="4641b-153">Depurar datos de hello SDK</span><span class="sxs-lookup"><span data-stu-id="4641b-153">Debug data from hello SDK</span></span>

<span data-ttu-id="4641b-154">**¿Cómo puedo averiguar qué Hola SDK está haciendo?**</span><span class="sxs-lookup"><span data-stu-id="4641b-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="4641b-155">Para obtener más información acerca de lo que ocurre en hello API, agregar a tooget `<SDKLogger/>` en el nodo raíz de Hola Hola ApplicationInsights.xml del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="4641b-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="4641b-156">También puede indicar al archivo de hello registrador toooutput tooa:</span><span class="sxs-lookup"><span data-stu-id="4641b-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="4641b-157">Hola archivos pueden encontrarse en `%temp%\javasdklogs` o `java.io.tmpdir` en el caso de servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="4641b-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="4641b-158">pantalla de inicio de Azure de bienvenida</span><span class="sxs-lookup"><span data-stu-id="4641b-158">hello Azure start screen</span></span>
<span data-ttu-id="4641b-159">**Estoy observando [Hola portal de Azure](https://portal.azure.com). ¿Mapa Hola decirme algo acerca de mi aplicación?**</span><span class="sxs-lookup"><span data-stu-id="4641b-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="4641b-160">No, muestra el estado de Hola de servidores Azure alrededor de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="4641b-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="4641b-161">*En panel de inicio de Azure de hello (pantalla principal), ¿cómo busco datos acerca de mi aplicación?*</span><span class="sxs-lookup"><span data-stu-id="4641b-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="4641b-162">Suponiendo que [configurar su aplicación para Application Insights][java], haga clic en Examinar, seleccione Application Insights y seleccionar recurso de aplicación Hola que creó para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4641b-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="4641b-163">tooget existe con mayor rapidez en el futuro, puede anclar el panel de inicio de toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4641b-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="4641b-164">Servidores de intranet</span><span class="sxs-lookup"><span data-stu-id="4641b-164">Intranet servers</span></span>
<span data-ttu-id="4641b-165">**¿Puedo supervisar un servidor de mi intranet?**</span><span class="sxs-lookup"><span data-stu-id="4641b-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="4641b-166">Sí, siempre que el servidor puede enviar el portal de Application Insights toohello de telemetría a través de Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="4641b-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="4641b-167">En el firewall, es posible que tenga tooopen los puertos TCP 80 y 443 para toodc.services.visualstudio.com de tráfico saliente y f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="4641b-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="4641b-168">Retención de datos</span><span class="sxs-lookup"><span data-stu-id="4641b-168">Data retention</span></span>
<span data-ttu-id="4641b-169">**¿Cuánto tiempo se retienen los datos en el portal de hello? ¿Es seguro?**</span><span class="sxs-lookup"><span data-stu-id="4641b-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="4641b-170">Consulte [Privacidad y retención de los datos][data].</span><span class="sxs-lookup"><span data-stu-id="4641b-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4641b-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4641b-171">Next steps</span></span>
<span data-ttu-id="4641b-172">**He configurado Application Insights para mi aplicación de servidor Java. ¿Qué más puedo hacer?**</span><span class="sxs-lookup"><span data-stu-id="4641b-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="4641b-173">[Supervisar la disponibilidad de sus páginas web][availability]</span><span class="sxs-lookup"><span data-stu-id="4641b-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="4641b-174">[Supervisar el uso de páginas web][usage]</span><span class="sxs-lookup"><span data-stu-id="4641b-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="4641b-175">[Realizar el seguimiento del uso y diagnosticar los problemas en las aplicaciones de su dispositivo][platforms]</span><span class="sxs-lookup"><span data-stu-id="4641b-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="4641b-176">[Escribir un uso tootrack de código de la aplicación][track]</span><span class="sxs-lookup"><span data-stu-id="4641b-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="4641b-177">[Captura de registros de diagnóstico][javalogs]</span><span class="sxs-lookup"><span data-stu-id="4641b-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="4641b-178">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="4641b-178">Get help</span></span>
* [<span data-ttu-id="4641b-179">Desbordamiento de la pila</span><span class="sxs-lookup"><span data-stu-id="4641b-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

