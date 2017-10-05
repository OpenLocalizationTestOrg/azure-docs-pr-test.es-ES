---
title: "Solución de problemas de Application Insights en un proyecto web de Java"
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
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="4c600-103">Solución de problemas y preguntas y respuestas sobre Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="4c600-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="4c600-104">Preguntas o problemas relacionados con [Azure Application Insights en Java][java].</span><span class="sxs-lookup"><span data-stu-id="4c600-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="4c600-105">a continuación se incluyen algunas sugerencias.</span><span class="sxs-lookup"><span data-stu-id="4c600-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="4c600-106">Errores de compilación</span><span class="sxs-lookup"><span data-stu-id="4c600-106">Build errors</span></span>
<span data-ttu-id="4c600-107">**En Eclipse, al agregar el SDK de Application Insights a través de Maven o Gradle, obtengo errores de compilación o de validación de la suma de comprobación.**</span><span class="sxs-lookup"><span data-stu-id="4c600-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="4c600-108">Si el elemento de dependencia <version> usa un patrón con caracteres comodín (por ejemplo, (Maven) `<version>[1.0,)</version>` o (Gradle) `version:'1.0.+'`), pruebe a especificar una versión concreta en lugar de `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="4c600-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="4c600-109">Consulte la [notas de la versión](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) para la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="4c600-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="4c600-110">No aparecen datos</span><span class="sxs-lookup"><span data-stu-id="4c600-110">No data</span></span>
<span data-ttu-id="4c600-111">**He agregado Application Insights correctamente y he ejecutado mi aplicación, pero no aparecen datos en el portal.**</span><span class="sxs-lookup"><span data-stu-id="4c600-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="4c600-112">Espere un minuto y haga clic en Actualizar,</span><span class="sxs-lookup"><span data-stu-id="4c600-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="4c600-113">Los gráficos se actualizan automáticamente de forma periódica, pero puede actualizarlos manualmente.</span><span class="sxs-lookup"><span data-stu-id="4c600-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="4c600-114">El intervalo de actualización depende del intervalo de tiempo del gráfico.</span><span class="sxs-lookup"><span data-stu-id="4c600-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="4c600-115">Compruebe que tiene una clave de instrumentación definida en el archivo ApplicationInsights.xml (en la carpeta de recursos del proyecto).</span><span class="sxs-lookup"><span data-stu-id="4c600-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="4c600-116">Compruebe que no haya ningún nodo `<DisableTelemetry>true</DisableTelemetry>` en el archivo xml.</span><span class="sxs-lookup"><span data-stu-id="4c600-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="4c600-117">En el firewall, es posible que tenga que abrir los puertos TCP 80 y 443 para el tráfico saliente en dc.services.visualstudio.com. Consulte la [lista completa de excepciones del firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="4c600-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="4c600-118">En el panel de inicio de Microsoft Azure, observe el mapa de estado del servicio.</span><span class="sxs-lookup"><span data-stu-id="4c600-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="4c600-119">Si hay algunas indicaciones de alerta, espere hasta que hayan vuelto a su estado correcto y después cierre y vuelva a abrir el cuadro de la aplicación de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4c600-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="4c600-120">Active el inicio de sesión en la ventana de la consola del IDE. Para ello, agregue un elemento `<SDKLogger />` bajo el nodo raíz en el archivo ApplicationInsights.xml (en la carpeta de recursos del proyecto) y compruebe si hay entradas precedidas por la indicación [Error].</span><span class="sxs-lookup"><span data-stu-id="4c600-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="4c600-121">Asegúrese de que se ha cargado correctamente el archivo ApplicationInsights.xml apropiado por parte del SDK de Java, examinando para ello los mensajes de salida de la consola para ver si hay una instrucción que haga referencia a que "el archivo de configuración se ha encontrado correctamente".</span><span class="sxs-lookup"><span data-stu-id="4c600-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="4c600-122">Si no se encuentra el archivo de configuración, compruebe los mensajes de salida para ver dónde se busca el archivo de configuración, y asegúrese de que ApplicationInsights.xml se encuentra en una de las ubicaciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4c600-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="4c600-123">Como regla general, puede colocar el archivo de configuración cerca de los JAR de SDK de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4c600-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="4c600-124">Por ejemplo: en Tomcat, esto significaría la carpeta WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="4c600-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="4c600-125">Solía ver datos, pero ya no sucede esto.</span><span class="sxs-lookup"><span data-stu-id="4c600-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="4c600-126">Compruebe el [blog de estado](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="4c600-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="4c600-127">¿Ha alcanzado su cuota mensual de puntos de datos?</span><span class="sxs-lookup"><span data-stu-id="4c600-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="4c600-128">Abra Configuración/Cuotas y Precios para averiguarlo. Si es así, puede actualizar el plan o pagar para obtener capacidad adicional.</span><span class="sxs-lookup"><span data-stu-id="4c600-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="4c600-129">Consulte el [esquema de precios](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="4c600-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="4c600-130">No veo todos los datos que esperaba</span><span class="sxs-lookup"><span data-stu-id="4c600-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="4c600-131">Abra la hoja Quotas and Pricing (Cuotas y precios) y compruebe si el [muestreo](app-insights-sampling.md) está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="4c600-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="4c600-132">(La transmisión al 100 % significa que el muestreo no está en funcionamiento). El servicio Application Insights se puede configurar para que acepte únicamente una fracción de la telemetría procedente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c600-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="4c600-133">Esto le ayuda a mantenerse en su cuota mensual de telemetría.</span><span class="sxs-lookup"><span data-stu-id="4c600-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="4c600-134">No aparecen datos de uso</span><span class="sxs-lookup"><span data-stu-id="4c600-134">No usage data</span></span>
<span data-ttu-id="4c600-135">**Veo datos sobre solicitudes y tiempos de respuesta, pero no de vista de página, del explorador o de datos de usuarios.**</span><span class="sxs-lookup"><span data-stu-id="4c600-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="4c600-136">La aplicación se ha configurado correctamente para enviar datos de telemetría desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="4c600-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="4c600-137">El paso siguiente consiste en [configurar las páginas web para enviar datos de telemetría desde el explorador web][usage].</span><span class="sxs-lookup"><span data-stu-id="4c600-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="4c600-138">Como alternativa, si el cliente es una aplicación de [teléfono o de cualquier otro dispositivo][platforms], puede enviar datos de telemetría desde este.</span><span class="sxs-lookup"><span data-stu-id="4c600-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="4c600-139">Use la misma clave de instrumentación para configurar la telemetría tanto de cliente como de servidor.</span><span class="sxs-lookup"><span data-stu-id="4c600-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="4c600-140">Los datos aparecerán en el mismo recurso de Application Insights y podrá correlacionar eventos de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="4c600-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="4c600-141">Deshabilitación de la telemetría</span><span class="sxs-lookup"><span data-stu-id="4c600-141">Disabling telemetry</span></span>
<span data-ttu-id="4c600-142">**¿Cómo puedo deshabilitar la recopilación de telemetría?**</span><span class="sxs-lookup"><span data-stu-id="4c600-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="4c600-143">En el código:</span><span class="sxs-lookup"><span data-stu-id="4c600-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="4c600-144">**O**</span><span class="sxs-lookup"><span data-stu-id="4c600-144">**Or**</span></span> 

<span data-ttu-id="4c600-145">Actualice ApplicationInsights.xml (en la carpeta de recursos del proyecto).</span><span class="sxs-lookup"><span data-stu-id="4c600-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="4c600-146">Agregue lo siguiente bajo el nodo raíz:</span><span class="sxs-lookup"><span data-stu-id="4c600-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="4c600-147">Si usa el método XML, debe reiniciar la aplicación al cambiar el valor.</span><span class="sxs-lookup"><span data-stu-id="4c600-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="4c600-148">Cambio de destino</span><span class="sxs-lookup"><span data-stu-id="4c600-148">Changing the target</span></span>
<span data-ttu-id="4c600-149">**¿Cómo puedo cambiar el recurso de Azure al que mi proyecto envía datos?**</span><span class="sxs-lookup"><span data-stu-id="4c600-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="4c600-150">[Obtenga la clave de instrumentación del nuevo recurso.][java]</span><span class="sxs-lookup"><span data-stu-id="4c600-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="4c600-151">Si ha agregado Application Insights al proyecto mediante el kit de herramientas de Azure para Eclipse, haga clic con el botón derecho en el proyecto web, seleccione **Azure**, **Configurar Application Insights** y cambie la clave.</span><span class="sxs-lookup"><span data-stu-id="4c600-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="4c600-152">De lo contrario, actualice la clave en ApplicationInsights.xml en la carpeta de recursos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="4c600-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="4c600-153">Depuración de datos del SDK</span><span class="sxs-lookup"><span data-stu-id="4c600-153">Debug data from the SDK</span></span>

<span data-ttu-id="4c600-154">**¿Cómo puedo averiguar lo que está haciendo el SDK?**</span><span class="sxs-lookup"><span data-stu-id="4c600-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="4c600-155">Para más información sobre lo que sucede en la API, agregue `<SDKLogger/>` bajo el nodo raíz del archivo de configuración ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="4c600-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="4c600-156">También puede indicar al registrador que lo envíe a un archivo:</span><span class="sxs-lookup"><span data-stu-id="4c600-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="4c600-157">Los archivos se pueden encontrar en `%temp%\javasdklogs` o `java.io.tmpdir` en el caso del servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="4c600-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="4c600-158">Pantalla de inicio de Azure</span><span class="sxs-lookup"><span data-stu-id="4c600-158">The Azure start screen</span></span>
<span data-ttu-id="4c600-159">**Estoy mirando el [portal de Azure](https://portal.azure.com). ¿El mapa indica algo sobre mi aplicación?**</span><span class="sxs-lookup"><span data-stu-id="4c600-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="4c600-160">No, este muestra el estado de los servidores de Azure en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="4c600-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="4c600-161">*¿Cómo puedo encontrar datos sobre mi aplicación desde el panel de inicio de Azure (pantalla principal)?*</span><span class="sxs-lookup"><span data-stu-id="4c600-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="4c600-162">Suponiendo que haya [configurado la aplicación para Application Insights][java], haga clic en Examinar, seleccione Application Insights y, después, elija el recurso de aplicación que haya creado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c600-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="4c600-163">Para mayor brevedad en un futuro, puede anclar la aplicación al panel de inicio.</span><span class="sxs-lookup"><span data-stu-id="4c600-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="4c600-164">Servidores de intranet</span><span class="sxs-lookup"><span data-stu-id="4c600-164">Intranet servers</span></span>
<span data-ttu-id="4c600-165">**¿Puedo supervisar un servidor de mi intranet?**</span><span class="sxs-lookup"><span data-stu-id="4c600-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="4c600-166">Sí, siempre que dicho servidor pueda enviar datos de telemetría al portal de Application Insights a través de una conexión pública a Internet.</span><span class="sxs-lookup"><span data-stu-id="4c600-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="4c600-167">En el firewall, tendrá que abrir los puertos TCP 80 y 443 para el tráfico saliente en dc.services.visualstudio.com y f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="4c600-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="4c600-168">Retención de datos</span><span class="sxs-lookup"><span data-stu-id="4c600-168">Data retention</span></span>
<span data-ttu-id="4c600-169">**¿Cuánto tiempo se retienen los datos en el portal? ¿Es seguro?**</span><span class="sxs-lookup"><span data-stu-id="4c600-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="4c600-170">Consulte [Privacidad y retención de los datos][data].</span><span class="sxs-lookup"><span data-stu-id="4c600-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c600-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c600-171">Next steps</span></span>
<span data-ttu-id="4c600-172">**He configurado Application Insights para mi aplicación de servidor Java. ¿Qué más puedo hacer?**</span><span class="sxs-lookup"><span data-stu-id="4c600-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="4c600-173">[Supervisar la disponibilidad de sus páginas web][availability]</span><span class="sxs-lookup"><span data-stu-id="4c600-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="4c600-174">[Supervisar el uso de páginas web][usage]</span><span class="sxs-lookup"><span data-stu-id="4c600-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="4c600-175">[Realizar el seguimiento del uso y diagnosticar los problemas en las aplicaciones de su dispositivo][platforms]</span><span class="sxs-lookup"><span data-stu-id="4c600-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="4c600-176">[Escribir código para realizar un seguimiento del uso de la aplicación][track]</span><span class="sxs-lookup"><span data-stu-id="4c600-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="4c600-177">[Captura de registros de diagnóstico][javalogs]</span><span class="sxs-lookup"><span data-stu-id="4c600-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="4c600-178">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="4c600-178">Get help</span></span>
* [<span data-ttu-id="4c600-179">Desbordamiento de la pila</span><span class="sxs-lookup"><span data-stu-id="4c600-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

