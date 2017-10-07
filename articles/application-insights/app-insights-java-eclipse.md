---
title: "aaaGet a trabajar con información de la aplicación de Azure con Java en Eclipse | Documentos de Microsoft"
description: Usar Hola rendimiento tooadd complemento de Eclipse y uso de supervisar el sitio Web de Java de tooyour con Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="2db86-103">Introducción a Application Insights con Java en Eclipse</span><span class="sxs-lookup"><span data-stu-id="2db86-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="2db86-104">Hola Application Insights SDK envía telemetría desde la aplicación web de Java para que se pueden analizar el uso y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2db86-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="2db86-105">Hola Eclipse complemento para Application Insights automáticamente instala Hola SDK en el proyecto para sacar partido de telemetría de cuadro de hello, además de una API que puede usar la telemetría personalizada toowrite.</span><span class="sxs-lookup"><span data-stu-id="2db86-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="2db86-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2db86-106">Prerequisites</span></span>
<span data-ttu-id="2db86-107">Hola complemento funciona actualmente para los proyectos de Maven y proyectos Web dinámicos en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2db86-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="2db86-108">([Tipos de tooother agregar Application Insights de proyecto de Java][java].)</span><span class="sxs-lookup"><span data-stu-id="2db86-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="2db86-109">Necesitará:</span><span class="sxs-lookup"><span data-stu-id="2db86-109">You'll need:</span></span>

* <span data-ttu-id="2db86-110">Oracle JRE 1.6 o posterior</span><span class="sxs-lookup"><span data-stu-id="2db86-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="2db86-111">Una suscripción demasiado[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2db86-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="2db86-112">[Eclipse IDE para Java EE Developers](http://www.eclipse.org/downloads/), Indigo o superior.</span><span class="sxs-lookup"><span data-stu-id="2db86-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="2db86-113">Windows 7 o posterior, o Windows Server 2008 o posterior</span><span class="sxs-lookup"><span data-stu-id="2db86-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="2db86-114">Instalar SDK de hello en Eclipse (una vez)</span><span class="sxs-lookup"><span data-stu-id="2db86-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="2db86-115">Solo tiene toodo una vez por equipo.</span><span class="sxs-lookup"><span data-stu-id="2db86-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="2db86-116">Este paso instala un Kit de herramientas que, a continuación, se puede agregar el SDK de hello tooeach Dynamic Web Project.</span><span class="sxs-lookup"><span data-stu-id="2db86-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="2db86-117">En Eclipse, haga clic en Ayuda, Instalar nuevo software.</span><span class="sxs-lookup"><span data-stu-id="2db86-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Ayuda, Instalar nuevo software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="2db86-119">Hola SDK se encuentra en http://dl.microsoft.com/eclipse, en el Kit de herramientas de Azure.</span><span class="sxs-lookup"><span data-stu-id="2db86-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="2db86-120">Desactive **Ponerse en contacto con todos los sitios de actualización...**</span><span class="sxs-lookup"><span data-stu-id="2db86-120">Uncheck **Contact all update sites...**</span></span>

    ![Para el SDK de Application Insights, desactive Ponerse en contacto con todos los sitios de actualización](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="2db86-122">Siga Hola restantes pasos para cada proyecto de Java.</span><span class="sxs-lookup"><span data-stu-id="2db86-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="2db86-123">Creación de un recurso de Application Insights en Azure</span><span class="sxs-lookup"><span data-stu-id="2db86-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="2db86-124">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2db86-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2db86-125">Cree un recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2db86-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="2db86-126">Establezca tooJava de tipo hello aplicación aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="2db86-126">Set hello application type tooJava web application.</span></span>  

    ![Haga clic en + y elija Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="2db86-128">Buscar la clave de instrumentación de Hola de nuevo recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="2db86-129">Necesitará toopaste en el proyecto de código en breve.</span><span class="sxs-lookup"><span data-stu-id="2db86-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="2db86-131">Agregar proyecto de tooyour Application Insights</span><span class="sxs-lookup"><span data-stu-id="2db86-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="2db86-132">Agregar Application Insights en menú contextual de Hola de su proyecto web de Java.</span><span class="sxs-lookup"><span data-stu-id="2db86-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="2db86-134">Pegue la clave de instrumentación de Hola que obtuvo en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2db86-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![En hello nueva información general de recursos, haga clic en propiedades y copiar Hola clave de instrumentación](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="2db86-136">clave de Hola se envía junto con todos los elementos de telemetría e indica toodisplay Application Insights en el recurso.</span><span class="sxs-lookup"><span data-stu-id="2db86-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="2db86-137">Ejecutar la aplicación hello y ver las métricas</span><span class="sxs-lookup"><span data-stu-id="2db86-137">Run hello application and see metrics</span></span>
<span data-ttu-id="2db86-138">Ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2db86-138">Run your application.</span></span>

<span data-ttu-id="2db86-139">Devolver el recurso de Application Insights de tooyour en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2db86-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="2db86-140">Datos de las solicitudes HTTP aparecerá en la hoja de información general de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="2db86-141">(Si todavía no está ahí, espere unos segundos y, a continuación, haga clic en Actualizar).</span><span class="sxs-lookup"><span data-stu-id="2db86-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="2db86-142">Respuesta del servidor, recuentos de solicitudes y errores</span><span class="sxs-lookup"><span data-stu-id="2db86-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="2db86-143">Haga clic en a través de cualquier toosee gráfico métricas más detalladas.</span><span class="sxs-lookup"><span data-stu-id="2db86-143">Click through any chart toosee more detailed metrics.</span></span>

![Recuentos de solicitudes por nombre](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="2db86-145">[Más información acerca de las métricas.][metrics]</span><span class="sxs-lookup"><span data-stu-id="2db86-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="2db86-146">Y, al ver las propiedades de Hola de una solicitud, puede ver eventos de telemetría de hello asociados con él, como las solicitudes y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="2db86-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Todos los seguimientos para esta solicitud](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="2db86-148">Telemetría de cliente</span><span class="sxs-lookup"><span data-stu-id="2db86-148">Client-side telemetry</span></span>
<span data-ttu-id="2db86-149">Desde la hoja de inicio rápido de hello, haga clic en Get código toomonitor páginas web:</span><span class="sxs-lookup"><span data-stu-id="2db86-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![En la hoja de información general sobre la aplicación, elija Inicio rápido, obtener código toomonitor las páginas web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="2db86-152">Insertar fragmento de código de hello en el encabezado de Hola de los archivos HTML.</span><span class="sxs-lookup"><span data-stu-id="2db86-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="2db86-153">Visualización de datos del lado cliente</span><span class="sxs-lookup"><span data-stu-id="2db86-153">View client-side data</span></span>
<span data-ttu-id="2db86-154">Abra las páginas web actualizadas y úselas.</span><span class="sxs-lookup"><span data-stu-id="2db86-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="2db86-155">Espere un minuto o dos, a continuación, devolver tooApplication visión y hoja de uso de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="2db86-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="2db86-156">(Desde la hoja de información general de hello, desplácese hacia abajo y haga clic en uso).</span><span class="sxs-lookup"><span data-stu-id="2db86-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="2db86-157">Métricas de sesión, usuarios y vista de página aparecerán en la hoja de Hola de uso:</span><span class="sxs-lookup"><span data-stu-id="2db86-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Sesiones, usuarios y vistas de página](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="2db86-159">[Más información sobre la configuración de la telemetría de cliente.][usage]</span><span class="sxs-lookup"><span data-stu-id="2db86-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="2db86-160">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2db86-160">Publish your application</span></span>
<span data-ttu-id="2db86-161">Publicar ahora el servidor de toohello de aplicación, permitir a los usuarios usar e inspeccionar telemetría Hola aparezca en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="2db86-162">Asegúrese de que el firewall permite la aplicación toosend puertos toothese de telemetría:</span><span class="sxs-lookup"><span data-stu-id="2db86-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="2db86-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="2db86-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="2db86-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="2db86-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="2db86-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="2db86-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="2db86-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="2db86-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="2db86-167">En los servidores de Windows, instale:</span><span class="sxs-lookup"><span data-stu-id="2db86-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="2db86-168">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="2db86-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="2db86-169">(Esto habilita los contadores de rendimiento.)</span><span class="sxs-lookup"><span data-stu-id="2db86-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="2db86-170">Excepciones y errores de solicitud</span><span class="sxs-lookup"><span data-stu-id="2db86-170">Exceptions and request failures</span></span>
<span data-ttu-id="2db86-171">Las excepciones no controladas se recopilan automáticamente:</span><span class="sxs-lookup"><span data-stu-id="2db86-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="2db86-172">toocollect datos en otras excepciones, tienes dos opciones:</span><span class="sxs-lookup"><span data-stu-id="2db86-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="2db86-173">[Insertar llamadas tooTrackException en su código](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="2db86-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="2db86-174">[Instalar agente Java hello en el servidor](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="2db86-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="2db86-175">Especificar métodos de Hola que desee toowatch.</span><span class="sxs-lookup"><span data-stu-id="2db86-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="2db86-176">Supervisión de llamadas a métodos y dependencias externas</span><span class="sxs-lookup"><span data-stu-id="2db86-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="2db86-177">[Instalar agente Java hello](app-insights-java-agent.md) toolog especifica métodos internos y las llamadas realizadas a través de JDBC, con datos de tiempo.</span><span class="sxs-lookup"><span data-stu-id="2db86-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="2db86-178">Contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="2db86-178">Performance counters</span></span>
<span data-ttu-id="2db86-179">En la hoja de información general, desplácese hacia abajo y haga clic en hello **servidores** icono.</span><span class="sxs-lookup"><span data-stu-id="2db86-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="2db86-180">Verá diferentes contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2db86-180">You'll see a range of performance counters.</span></span>

![Desplácese hacia abajo del icono de servidores de hello tooclick](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="2db86-182">Personalizar la recopilación de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="2db86-182">Customize performance counter collection</span></span>
<span data-ttu-id="2db86-183">colección de toodisable del conjunto estándar de Hola de contadores de rendimiento, agregar Hola siguiente código en el nodo raíz de Hola de archivo de hello ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="2db86-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="2db86-184">Recopilar contadores de rendimiento adicionales</span><span class="sxs-lookup"><span data-stu-id="2db86-184">Collect additional performance counters</span></span>
<span data-ttu-id="2db86-185">Puede especificar toobe de contadores de rendimiento adicionales recopilados.</span><span class="sxs-lookup"><span data-stu-id="2db86-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="2db86-186">Contadores JMX (expuestos por máquina Virtual Java de hello)</span><span class="sxs-lookup"><span data-stu-id="2db86-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="2db86-187">`displayName`: nombre de hello mostrado en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="2db86-188">`objectName`: nombre de objeto JMX Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="2db86-189">`attribute`: atributo Hola de hello JMX objeto nombre toofetch</span><span class="sxs-lookup"><span data-stu-id="2db86-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="2db86-190">`type`(opcional): Hola tipo de atributo del objeto JMX:</span><span class="sxs-lookup"><span data-stu-id="2db86-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="2db86-191">Valor predeterminado: un tipo simple como int o long.</span><span class="sxs-lookup"><span data-stu-id="2db86-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="2db86-192">`composite`: datos de contador de rendimiento de hello están en formato de Hola de 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="2db86-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="2db86-193">`tabular`: datos de contador de rendimiento de hello están en formato de Hola de una fila de tabla</span><span class="sxs-lookup"><span data-stu-id="2db86-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="2db86-194">Contadores de rendimiento de Windows</span><span class="sxs-lookup"><span data-stu-id="2db86-194">Windows performance counters</span></span>
<span data-ttu-id="2db86-195">Cada [contador de rendimiento de Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) es un miembro de una categoría (Hola igual que un campo es un miembro de una clase).</span><span class="sxs-lookup"><span data-stu-id="2db86-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="2db86-196">Las categorías puede ser globales, o pueden tener instancias con nombre o numeradas.</span><span class="sxs-lookup"><span data-stu-id="2db86-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="2db86-197">displayName: nombre de hello mostrado en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="2db86-198">categoryName: Hola categoría contador de rendimiento (objeto de rendimiento) al que está asociado este contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2db86-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="2db86-199">counterName: nombre de Hola Hola del contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2db86-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="2db86-200">instanceName: Hola nombre de instancia de categoría de contador de rendimiento de Hola o una cadena vacía (""), si la categoría de hello contiene una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="2db86-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="2db86-201">Si Hola categoryName es el proceso y le gustaría toocollect del contador de rendimiento hello es proceso JVM actual de hello en que se ejecuta la aplicación, especifique `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="2db86-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="2db86-202">Los contadores de rendimiento están visibles como métricas personalizadas en el [Explorador de métricas][metrics].</span><span class="sxs-lookup"><span data-stu-id="2db86-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="2db86-203">Contadores de rendimiento de Unix</span><span class="sxs-lookup"><span data-stu-id="2db86-203">Unix performance counters</span></span>
* <span data-ttu-id="2db86-204">[Instalar collectd con el complemento de Application Insights hello](app-insights-java-collectd.md) tooget una amplia variedad de datos del sistema y de red.</span><span class="sxs-lookup"><span data-stu-id="2db86-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="2db86-205">Pruebas web de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="2db86-205">Availability web tests</span></span>
<span data-ttu-id="2db86-206">Application Insights pueden probar su sitio Web en intervalos regulares toocheck que está en funcionamiento y responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="2db86-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="2db86-207">[tooset una][availability], desplácese hacia abajo tooclick disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="2db86-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Desplácese hacia abajo, haga clic en Disponibilidad y, a continuación, en Agregar prueba web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="2db86-209">Obtendrá gráficos de tiempos de respuesta, junto con notificaciones por correo electrónico si su sitio deja de funcionar.</span><span class="sxs-lookup"><span data-stu-id="2db86-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Ejemplo de prueba web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="2db86-211">[Más información acerca de las pruebas web de disponibilidad.][availability]</span><span class="sxs-lookup"><span data-stu-id="2db86-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="2db86-212">Registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="2db86-212">Diagnostic logs</span></span>
<span data-ttu-id="2db86-213">Si usa Logback o Log4J (v1.2 o v2.0) para el seguimiento, puede que los registros de seguimiento que se envía automáticamente información que le permite explorar y buscar en ellos tooApplication.</span><span class="sxs-lookup"><span data-stu-id="2db86-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="2db86-214">[Más información sobre los registros de diagnóstico][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2db86-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="2db86-215">Telemetría personalizada</span><span class="sxs-lookup"><span data-stu-id="2db86-215">Custom telemetry</span></span>
<span data-ttu-id="2db86-216">Insertar unas pocas líneas de código en su toofind de aplicación web de Java a lo que hacen los usuarios con él o toohelp diagnosticar los problemas.</span><span class="sxs-lookup"><span data-stu-id="2db86-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="2db86-217">Puede insertar código en la página web JavaScript y en hello servidor Java.</span><span class="sxs-lookup"><span data-stu-id="2db86-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="2db86-218">[Obtenga información sobre la telemetría personalizad][track]</span><span class="sxs-lookup"><span data-stu-id="2db86-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="2db86-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2db86-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="2db86-220">Detección y diagnóstico de problemas</span><span class="sxs-lookup"><span data-stu-id="2db86-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="2db86-221">[Agregar telemetría de cliente web] [ usage] tooget telemetría de rendimiento de cliente web de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="2db86-222">[Configurar las pruebas web] [ availability] toomake seguro de la aplicación permanece en vivo y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="2db86-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="2db86-223">[Buscar eventos y registros] [ diagnostic] toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="2db86-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="2db86-224">[Captura de los seguimientos Log4J o Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2db86-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="2db86-225">Seguir el uso</span><span class="sxs-lookup"><span data-stu-id="2db86-225">Track usage</span></span>
* <span data-ttu-id="2db86-226">[Agregar telemetría de cliente web] [ usage] toomonitor página vistas y las métricas de usuario básica.</span><span class="sxs-lookup"><span data-stu-id="2db86-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="2db86-227">[Realizar un seguimiento de eventos personalizados y las métricas](app-insights-web-track-usage.md) toolearn acerca de cómo se utiliza la aplicación, tanto en el cliente de Hola y el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db86-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
