---
title: "aaaExport mediante el análisis de transmisiones de Azure Application Insights | Documentos de Microsoft"
description: "Análisis de transmisiones de forma continua puede transformar, filtrar y enrutar datos hello que exporta de Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="46175-103">Usar análisis de transmisiones tooprocess datos exportados de Application Insights</span><span class="sxs-lookup"><span data-stu-id="46175-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="46175-104">[Análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/) es Hola herramienta ideal para procesar datos [exportada desde Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="46175-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="46175-105">Stream Analytics puede extraer datos de una variedad de orígenes.</span><span class="sxs-lookup"><span data-stu-id="46175-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="46175-106">Puede transformar y filtrar los datos de hello y, a continuación, distribuirlo tooa diversos receptores.</span><span class="sxs-lookup"><span data-stu-id="46175-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="46175-107">En este ejemplo, vamos a crear un adaptador que toma datos de Application Insights, cambia el nombre y procesa algunos de los campos de Hola y lo canaliza en Power BI.</span><span class="sxs-lookup"><span data-stu-id="46175-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="46175-108">Hay mucho mejor y más sencillo [formas recomendadas toodisplay datos de Application Insights en Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="46175-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="46175-109">ruta de acceso se ilustra a continuación Hello es simplemente una tooillustrate de ejemplo cómo tooprocess exportan datos.</span><span class="sxs-lookup"><span data-stu-id="46175-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Diagrama de bloques para la exportación a través de SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="46175-111">Creación de almacenamiento en Azure</span><span class="sxs-lookup"><span data-stu-id="46175-111">Create storage in Azure</span></span>
<span data-ttu-id="46175-112">Exportación continua siempre genera cuenta de almacenamiento de Azure de tooan de datos, por lo que necesita almacenamiento de hello toocreate en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="46175-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="46175-113">Crear una cuenta de almacenamiento "clásico" en su suscripción en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46175-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![En el portal de Azure, elija Nuevo, Datos, Almacenamiento.](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="46175-115">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="46175-115">Create a container</span></span>
   
    ![En un almacenamiento nuevo hello, seleccionar contenedores, haga clic en el icono de contenedores de hello y, a continuación, agregar](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="46175-117">Copie la clave de acceso de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="46175-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="46175-118">Necesitará pronto tooset seguridad de servicio de análisis de secuencia de entrada toohello Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![En el almacenamiento de hello, abra la configuración, claves y realizar una copia de la clave de acceso principal de Hola](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="46175-120">Iniciar exportación continua tooAzure almacenamiento</span><span class="sxs-lookup"><span data-stu-id="46175-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="46175-121">[exportación continua](app-insights-export-telemetry.md) transfiere los datos de Application Insights al almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="46175-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="46175-122">Hola portal de Azure, examinar recursos de Application Insights toohello que creó para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46175-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Elija Examinar, Application Insights, su aplicación.](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="46175-124">Cree una exportación continua.</span><span class="sxs-lookup"><span data-stu-id="46175-124">Create a continuous export.</span></span>
   
    ![Elija Configuración, Exportación continua, Agregar.](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="46175-126">Seleccione la cuenta de almacenamiento de Hola que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="46175-126">Select hello storage account you created earlier:</span></span>

    ![Establecer el destino de la exportación de Hola](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="46175-128">Establecer a tipos de evento de hello que desea toosee:</span><span class="sxs-lookup"><span data-stu-id="46175-128">Set hello event types you want toosee:</span></span>

    ![Elija los tipos de evento.](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="46175-130">Permita que se acumulen algunos datos.</span><span class="sxs-lookup"><span data-stu-id="46175-130">Let some data accumulate.</span></span> <span data-ttu-id="46175-131">Póngase cómo y deje que los usuarios usen su aplicación durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="46175-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="46175-132">Así, aparecerá la telemetría y verá gráficos estadísticos en el [explorador de métricas](app-insights-metrics-explorer.md) y eventos individuales en la [búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="46175-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="46175-133">Y además, los datos de hello exportará tooyour almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="46175-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="46175-134">Inspeccionar los datos de hello exportado.</span><span class="sxs-lookup"><span data-stu-id="46175-134">Inspect hello exported data.</span></span> <span data-ttu-id="46175-135">En Visual Studio, elija **Ver/Cloud Explorer** y abra Azure/Almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="46175-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="46175-136">(Si no tiene esta opción de menú, necesita tooinstall hello Azure SDK: abra el cuadro de diálogo de proyecto nuevo de Hola y abra Visual C# / nube / obtener Microsoft Azure SDK para. NET.)</span><span class="sxs-lookup"><span data-stu-id="46175-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="46175-137">Tome nota de la parte común de Hola de nombre de ruta de acceso de hello, que se deriva de la clave de nombre e instrumentación de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="46175-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="46175-138">eventos de Hola se escriben tooblob archivos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="46175-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="46175-139">Cada archivo puede contener uno o varios eventos.</span><span class="sxs-lookup"><span data-stu-id="46175-139">Each file may contain one or more events.</span></span> <span data-ttu-id="46175-140">Por lo que nos gustaría datos de eventos de tooread hello y filtrar campos Hola que queremos.</span><span class="sxs-lookup"><span data-stu-id="46175-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="46175-141">Hay todo tipo de cosas, que podríamos hacer con los datos de hello, pero nuestro plan hoy en día es toouse análisis de transmisiones toopipe Hola datos tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="46175-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="46175-142">Creación de una instancia de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="46175-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="46175-143">De hello [Portal de Azure clásico](https://manage.windowsazure.com/), seleccione servicio de análisis de transmisiones de Azure de Hola y crear un nuevo trabajo de análisis de transmisiones:</span><span class="sxs-lookup"><span data-stu-id="46175-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="46175-144">Cuando se crea el nuevo trabajo de hello, expandir los detalles:</span><span class="sxs-lookup"><span data-stu-id="46175-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="46175-145">Establecimiento de la ubicación del blob</span><span class="sxs-lookup"><span data-stu-id="46175-145">Set blob location</span></span>
<span data-ttu-id="46175-146">Establézcalo tootake entrada desde el blob exportar continua:</span><span class="sxs-lookup"><span data-stu-id="46175-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="46175-147">Ahora deberá Hola clave de acceso principal de la cuenta de almacenamiento, que se ha indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46175-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="46175-148">Utilizar esta configuración como Hola clave de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="46175-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="46175-149">Establecimiento del patrón del prefijo de la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="46175-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="46175-150">**Ser seguro tooset Hola formato de fecha tooYYYY-MM-DD (con guiones).**</span><span class="sxs-lookup"><span data-stu-id="46175-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="46175-151">Hola modelo de prefijo de ruta de acceso especifica que análisis de transmisiones busca archivos de entrada de hello en el almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="46175-152">Necesita tooset se toohow toocorrespond exportar continua almacena los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="46175-153">Configúrelo como este caso que se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="46175-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="46175-154">En este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="46175-154">In this example:</span></span>

* <span data-ttu-id="46175-155">`webapplication27`es Hola nombre de recurso de Application Insights hello **todas las minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="46175-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="46175-156">`1234...`es la clave de instrumentación de Hola de hello recurso de Application Insights, **omitir guiones**.</span><span class="sxs-lookup"><span data-stu-id="46175-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="46175-157">`PageViews`es el tipo de saludo de datos que desee tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="46175-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="46175-158">los tipos disponibles de Hello dependen de filtro de Hola que se establezca en Exportar continua.</span><span class="sxs-lookup"><span data-stu-id="46175-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="46175-159">Examinar Hola Hola de toosee de los datos exportados en otros tipos disponibles y ver hello [Exportar modelo de datos](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="46175-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="46175-160">`/{date}/{time}` es un patrón escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="46175-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="46175-161">Inspeccionar hello toomake de almacenamiento seguro de que obtener una ruta de acceso de hello derecho.</span><span class="sxs-lookup"><span data-stu-id="46175-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="46175-162">Finalización de la instalación inicial</span><span class="sxs-lookup"><span data-stu-id="46175-162">Finish initial setup</span></span>
<span data-ttu-id="46175-163">Confirme el formato de serialización de hello:</span><span class="sxs-lookup"><span data-stu-id="46175-163">Confirm hello serialization format:</span></span>

![Confirme y cierre el asistente.](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="46175-165">Cerrar el Asistente de Hola y espere Hola el programa de instalación toocomplete.</span><span class="sxs-lookup"><span data-stu-id="46175-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="46175-166">Utilice toodownload de comando de ejemplo de Hola algunos datos.</span><span class="sxs-lookup"><span data-stu-id="46175-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="46175-167">Guardarla como un toodebug de ejemplo de prueba de la consulta.</span><span class="sxs-lookup"><span data-stu-id="46175-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="46175-168">Salida de hello de conjunto</span><span class="sxs-lookup"><span data-stu-id="46175-168">Set hello output</span></span>
<span data-ttu-id="46175-169">Ahora seleccione el trabajo y establezca la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="46175-169">Now select your job and set hello output.</span></span>

![Seleccione nuevo canal de hello, haga clic en salidas, agregar, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="46175-171">Proporcionar la **cuenta profesional o educativa** tooauthorize tooaccess de análisis de transmisiones el recurso de Power BI.</span><span class="sxs-lookup"><span data-stu-id="46175-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="46175-172">A continuación, inventar un nombre para la salida de Hola y de tabla y el conjunto de datos de hello destino Power BI.</span><span class="sxs-lookup"><span data-stu-id="46175-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Invente tres nombres](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="46175-174">Consulta de conjunto Hola</span><span class="sxs-lookup"><span data-stu-id="46175-174">Set hello query</span></span>
<span data-ttu-id="46175-175">consulta de Hello rige la traducción de Hola de entrada toooutput.</span><span class="sxs-lookup"><span data-stu-id="46175-175">hello query governs hello translation from input toooutput.</span></span>

![Seleccione el trabajo de Hola y haga clic en la consulta.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="46175-178">Utilice Hola prueba función toocheck que se obtiene un resultado de hello derecho.</span><span class="sxs-lookup"><span data-stu-id="46175-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="46175-179">Proporciona datos de ejemplo de Hola que tardó en página de entradas de Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="46175-180">Consulta toodisplay recuentos de eventos</span><span class="sxs-lookup"><span data-stu-id="46175-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="46175-181">Pegue esta consulta:</span><span class="sxs-lookup"><span data-stu-id="46175-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="46175-182">entrada de exportación es alias Hola asignamos entrada de flujo de toohello</span><span class="sxs-lookup"><span data-stu-id="46175-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="46175-183">salida de pbi es alias de salida de hello definimos</span><span class="sxs-lookup"><span data-stu-id="46175-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="46175-184">Usamos [externa GetElements aplicar](https://msdn.microsoft.com/library/azure/dn706229.aspx) porque el nombre del evento de hello está en un arrray JSON anidado.</span><span class="sxs-lookup"><span data-stu-id="46175-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="46175-185">A continuación, selecciona seleccione Hola Hola nombre del evento, junto con un recuento del número de Hola de instancias con ese nombre en hello período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="46175-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="46175-186">Hola [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) cláusula agrupa elementos de hello en períodos de tiempo de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="46175-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="46175-187">Valores de métrica de toodisplay de consulta</span><span class="sxs-lookup"><span data-stu-id="46175-187">Query toodisplay metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="46175-188">Esta consulta obtiene los detalles de la hora del evento Hola métricas telemetría tooget Hola y el valor de métrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="46175-189">valores de métrica de Hello quedan dentro de una matriz, por lo que usamos filas de hello externa GetElements aplicar patrón tooextract Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="46175-190">"myMetric" es el nombre de Hola de métrica de hello en este caso.</span><span class="sxs-lookup"><span data-stu-id="46175-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="46175-191">Consulta tooinclude valores de propiedades de dimensión</span><span class="sxs-lookup"><span data-stu-id="46175-191">Query tooinclude values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="46175-192">Esta consulta incluye valores de propiedades de dimensión Hola sin dependiendo de una dimensión determinada está en un índice de matriz de dimensión Hola fijo.</span><span class="sxs-lookup"><span data-stu-id="46175-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="46175-193">Ejecutar trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="46175-193">Run hello job</span></span>
<span data-ttu-id="46175-194">Puede seleccionar una fecha en hello más allá de trabajo de hello toostart desde.</span><span class="sxs-lookup"><span data-stu-id="46175-194">You can select a date in hello past toostart hello job from.</span></span> 

![Seleccione el trabajo de Hola y haga clic en la consulta.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="46175-197">Espere hasta que se ejecuta el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="46175-198">Visualización de resultados en Power BI</span><span class="sxs-lookup"><span data-stu-id="46175-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="46175-199">Hay mucho mejor y más sencillo [formas recomendadas toodisplay datos de Application Insights en Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="46175-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="46175-200">ruta de acceso se ilustra a continuación Hello es simplemente una tooillustrate de ejemplo cómo tooprocess exportan datos.</span><span class="sxs-lookup"><span data-stu-id="46175-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="46175-201">Abra Power BI con su trabajo o cuenta del centro educativo y Hola seleccione conjunto de datos y tabla que ha definido como salida de hello de trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="46175-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![En Power BI, seleccione el conjunto de datos y los campos.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="46175-203">Ahora puede usar este conjunto de datos en informes y paneles de [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="46175-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![En Power BI, seleccione el conjunto de datos y los campos.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="46175-205">¿No hay datos?</span><span class="sxs-lookup"><span data-stu-id="46175-205">No data?</span></span>
* <span data-ttu-id="46175-206">Compruebe que [formato de fecha de conjunto hello](#set-path-prefix-pattern) correctamente tooYYYY-MM-DD (con guiones).</span><span class="sxs-lookup"><span data-stu-id="46175-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="46175-207">Vídeo</span><span class="sxs-lookup"><span data-stu-id="46175-207">Video</span></span>
<span data-ttu-id="46175-208">Noam Ben Zeev muestra cómo tooprocess había exportado mediante el análisis de transmisiones de datos.</span><span class="sxs-lookup"><span data-stu-id="46175-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="46175-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46175-209">Next steps</span></span>
* [<span data-ttu-id="46175-210">Exportación continua</span><span class="sxs-lookup"><span data-stu-id="46175-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="46175-211">Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.</span><span class="sxs-lookup"><span data-stu-id="46175-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="46175-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="46175-212">Application Insights</span></span>](app-insights-overview.md)

