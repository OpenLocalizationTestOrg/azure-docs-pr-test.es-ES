---
title: aaaExport tooPower BI de Application Insights | Documentos de Microsoft
description: Las consultas de Analytics se pueden mostrar en Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="2c1d4-103">Alimentación de Power BI desde Application Insights</span><span class="sxs-lookup"><span data-stu-id="2c1d4-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="2c1d4-104">[Power BI](http://www.powerbi.com/) es un conjunto de herramientas de análisis de negocios que pueden ayudar a analizar datos y compartir conocimientos.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="2c1d4-105">Cada dispositivo cuenta con paneles que incluyen gran cantidad de datos.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="2c1d4-106">Puede combinar datos de varios orígenes, incluidas las consultas de Analytics en [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c1d4-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="2c1d4-107">Hay tres métodos recomendados para exportar datos de Application Insights tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="2c1d4-108">Se pueden utilizar por separado o conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-108">You can use them separately or together.</span></span>

* <span data-ttu-id="2c1d4-109">[**Adaptador de Power BI**](#power-pi-adapter): configure un panel completo de telemetría desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="2c1d4-110">depende del conjunto de Hola de gráficos, pero puede agregar sus propias consultas de cualquier otro origen.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="2c1d4-111">[**Exportar las consultas de análisis** ](#export-analytics-queries) -escribir ni una sola consulta que desee usar análisis y exportarlo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="2c1d4-112">Puede colocar esta consulta en un panel junto con otros datos.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="2c1d4-113">[**Exportación continua y análisis de transmisiones** ](app-insights-export-stream-analytics.md) -esto implica tooset de trabajo más seguridad.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="2c1d4-114">Resulta útil si desea que tookeep los datos durante largos períodos.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="2c1d4-115">En caso contrario, hello otros métodos son recomendables.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="2c1d4-116">Adaptador de Power BI</span><span class="sxs-lookup"><span data-stu-id="2c1d4-116">Power BI adapter</span></span>
<span data-ttu-id="2c1d4-117">Este método crea un panel completo de telemetría.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="2c1d4-118">depende del conjunto de datos inicial de Hello, pero puede agregar más tooit de datos.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="2c1d4-119">Obtiene el adaptador de Hola</span><span class="sxs-lookup"><span data-stu-id="2c1d4-119">Get hello adapter</span></span>
1. <span data-ttu-id="2c1d4-120">Inicie sesión en demasiado[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="2c1d4-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="2c1d4-121">Abra **Obtener datos**, **Servicios**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="2c1d4-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Obtención de un origen de datos de Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="2c1d4-123">Proporcione detalles de Hola de su recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Obtención de un origen de datos de Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="2c1d4-125">Espere un minuto o dos para hello toobe de datos importado.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Adaptador de Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="2c1d4-127">Se puede modificar el panel de hello, combinar gráficos de Application Insights Hola con los de otros orígenes y con las consultas de análisis.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="2c1d4-128">Tiene a su disposición una galería de visualización en la que puede obtener más gráficos; y cada gráfico tiene a su vez parámetros que puede configurar.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="2c1d4-129">Después de la importación inicial de hello, panel de Hola y los informes de hello continuar tooupdate diariamente.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="2c1d4-130">Puede controlar la programación de actualización de hello en el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="2c1d4-131">Exportación de consultas de Analytics</span><span class="sxs-lookup"><span data-stu-id="2c1d4-131">Export Analytics queries</span></span>
<span data-ttu-id="2c1d4-132">Esta ruta permite toowrite cualquier análisis desea consultar y, a continuación, exportar ese panel de Power BI tooa.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="2c1d4-133">(Puede agregar panel toohello creada por el adaptador de hello).</span><span class="sxs-lookup"><span data-stu-id="2c1d4-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="2c1d4-134">Una vez: instalar Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="2c1d4-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="2c1d4-135">tooimport su consulta Application Insights, utilice la versión de escritorio de Hola de Power BI.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="2c1d4-136">Pero, a continuación, puede publicar web toohello o tooyour el área de trabajo de Power BI en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="2c1d4-137">Instale [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="2c1d4-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="2c1d4-138">Exportación de una consulta de Analytics</span><span class="sxs-lookup"><span data-stu-id="2c1d4-138">Export an Analytics query</span></span>
1. <span data-ttu-id="2c1d4-139">[Abra Analytics y escriba la consulta](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="2c1d4-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="2c1d4-140">Probar y refinar la consulta de hello hasta que esté satisfecho con los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="2c1d4-141">**Asegúrese de que esa consulta Hola se ejecuta correctamente en el análisis antes de exportarla.**</span><span class="sxs-lookup"><span data-stu-id="2c1d4-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="2c1d4-142">En hello **exportar** menú, elija **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="2c1d4-143">Guarde el archivo de texto hello.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-143">Save hello text file.</span></span>
   
    ![Exportación de la consulta de Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="2c1d4-145">En Power BI Desktop, seleccione **obtener datos, realice una consulta en blanco** y, a continuación, en hello editor de consultas, en **vista** seleccione **Editor de consultas avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="2c1d4-146">Script de lenguaje M pegar Hola exportado en Hola Editor de consultas avanzadas.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Editor de consultas avanzadas](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="2c1d4-148">Es posible que tenga tooprovide credenciales tooallow Power BI tooaccess Azure.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="2c1d4-149">Use 'cuenta profesional' toosign con su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Proporcione las credenciales de Azure tooenable Power BI toorun la consulta de Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="2c1d4-151">(Si necesita tooverify Hola credenciales, utilice comando de menú de configuración del origen de datos de Hola Hola Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="2c1d4-152">Tenga cuidado las credenciales de hello toospecify que use para Azure, que podría ser diferente de las credenciales de Power BI.)</span><span class="sxs-lookup"><span data-stu-id="2c1d4-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="2c1d4-153">Elija una visualización de la consulta y seleccione campos de hello para el eje x, eje y y segmentación de dimensión.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Seleccionar la visualización](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="2c1d4-155">Publicar el área de trabajo de informes tooyour Power BI en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="2c1d4-156">Desde allí, puede incluir una versión sincronizada en otras páginas web.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Seleccionar la visualización](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="2c1d4-158">Actualizar informes de hello manualmente a intervalos o configurar una actualización programada en la página de opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2c1d4-159">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="2c1d4-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="2c1d4-160">401 o 403 No autorizado</span><span class="sxs-lookup"><span data-stu-id="2c1d4-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="2c1d4-161">Esto puede ocurrir si no se ha actualizado su token de actualización.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="2c1d4-162">Pruebe estas tooensure pasos que todavía tiene acceso.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="2c1d4-163">Si tiene acceso y las credenciales de hello refershing no funciona, abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="2c1d4-164">Inicie sesión en el Portal de Azure de Hola y asegúrese de que puede tener acceso a recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="2c1d4-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="2c1d4-165">Ensaye con credenciales de hello toorefresh para hello panel</span><span class="sxs-lookup"><span data-stu-id="2c1d4-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="2c1d4-166">Puerta de enlace incorrecta 502</span><span class="sxs-lookup"><span data-stu-id="2c1d4-166">502 Bad Gateway</span></span>
<span data-ttu-id="2c1d4-167">Esto se debe normalmente a una consulta de Analytics que devuelve demasiados datos.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="2c1d4-168">También debe intentar usar un intervalo de tiempo más reducido o mediante el uso de hello [hace](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) o [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) solo funciones [proyecto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Hola campos necesarios.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="2c1d4-169">Si reduce el conjunto de datos de hello procedentes de la consulta de análisis de hello no cumple sus requisitos debe considerar el uso de hello [API](https://dev.applicationinsights.io/documentation/overview) toopull un conjunto de datos mayor.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="2c1d4-170">Aquí indicamos cómo tooconvert Hola consulta M exportar toouse Hola API.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="2c1d4-171">Cree una [clave de API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).</span><span class="sxs-lookup"><span data-stu-id="2c1d4-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="2c1d4-172">Hola actualización secuencias de comandos de Power BI M que haya exportado desde análisis reemplazando hello ARM URL con la API de AI (vea el ejemplo siguiente)</span><span class="sxs-lookup"><span data-stu-id="2c1d4-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="2c1d4-173">Reemplace **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="2c1d4-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="2c1d4-174">por **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="2c1d4-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="2c1d4-175">Por último, actualizar credenciales toobasic y usar su clave de API</span><span class="sxs-lookup"><span data-stu-id="2c1d4-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="2c1d4-176">**Script existente**</span><span class="sxs-lookup"><span data-stu-id="2c1d4-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="2c1d4-177">**Script actualizado**</span><span class="sxs-lookup"><span data-stu-id="2c1d4-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="2c1d4-178">Acerca del muestreo</span><span class="sxs-lookup"><span data-stu-id="2c1d4-178">About sampling</span></span>
<span data-ttu-id="2c1d4-179">Si la aplicación envía una gran cantidad de datos, característica de muestreo adaptativo de hello puede operar y enviar solamente un porcentaje de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="2c1d4-180">Hola que mismo es verdadero si ha configurado manualmente de muestreo en hello SDK o en la recopilación.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="2c1d4-181">Aprenda más sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="2c1d4-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="2c1d4-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c1d4-182">Next steps</span></span>
* [<span data-ttu-id="2c1d4-183">Power BI: más información</span><span class="sxs-lookup"><span data-stu-id="2c1d4-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="2c1d4-184">Tutorial de Analytics</span><span class="sxs-lookup"><span data-stu-id="2c1d4-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

