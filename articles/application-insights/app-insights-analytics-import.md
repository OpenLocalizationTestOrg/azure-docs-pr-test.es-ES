---
title: aaaImport su tooAnalytics de datos en Azure Application Insights | Documentos de Microsoft
description: "Importar datos estáticos toojoin con la telemetría de aplicación, o importar un tooquery de flujo de datos independiente con el análisis."
services: application-insights
keywords: "esquema abierto, importación de datos"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="1ee6c-104">Importación de datos a Analytics</span><span class="sxs-lookup"><span data-stu-id="1ee6c-104">Import data into Analytics</span></span>

<span data-ttu-id="1ee6c-105">Importar los datos tabulares en [análisis](app-insights-analytics.md), ya sea toojoin con [Application Insights](app-insights-overview.md) telemetría de la aplicación, o para que se puede analizar como una secuencia independiente.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="1ee6c-106">El análisis es una secuencias de consulta eficaz lenguaje tooanalyzing adecuada con marca de tiempo de gran volumen de telemetría.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="1ee6c-107">Puede importar datos en Analytics mediante un esquema propio.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="1ee6c-108">No tiene esquemas toouse Hola de Application Insights estándar como solicitud o un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="1ee6c-109">Puede importar archivos JSON o DSV (valores separados por delimitadores, como pueden ser comas, puntos y coma o tabulaciones).</span><span class="sxs-lookup"><span data-stu-id="1ee6c-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="1ee6c-110">Existen tres situaciones donde es útil importar tooAnalytics:</span><span class="sxs-lookup"><span data-stu-id="1ee6c-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="1ee6c-111">**Combinar con la telemetría de la aplicación.**</span><span class="sxs-lookup"><span data-stu-id="1ee6c-111">**Join with app telemetry.**</span></span> <span data-ttu-id="1ee6c-112">Por ejemplo, puede importar una tabla que asigna las direcciones URL de los títulos de página legible toomore de sitio Web.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="1ee6c-113">En el análisis, puede crear un informe de gráfico de panel que muestra los diez páginas más populares de hello en el sitio Web.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="1ee6c-114">Ahora puede mostrar títulos de página en lugar de direcciones URL de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="1ee6c-115">**Correlacionar la telemetría de la aplicación** con otros orígenes, como tráfico de red, datos de servidor o archivos de registro de red CDN.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="1ee6c-116">**Aplicar el flujo de datos independiente de análisis tooa.**</span><span class="sxs-lookup"><span data-stu-id="1ee6c-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="1ee6c-117">Application Insights de Analytics es una herramienta eficaz, que funciona bien con flujos dispersos con marca de tiempo; en muchos casos, de manera mucho mejor que SQL.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="1ee6c-118">Si tiene un flujo de este tipo de algún otro origen, puede analizarlo con Analytics.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="1ee6c-119">Origen de datos de envío datos tooyour es fácil.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="1ee6c-120">(Una vez) Definir el esquema de Hola de los datos en un origen de datos' '.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="1ee6c-121">(Periódicamente) Cargar el almacenamiento de datos tooAzure y toonotify de la API de REST de hello nos llame que está esperando la ingesta de nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="1ee6c-122">Dentro de unos minutos, están disponibles para consultas de análisis de datos Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="1ee6c-123">frecuencia de carga de Hola Hola se define una por parte del usuario y rapidez quiere que su toobe de datos disponible para las consultas.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="1ee6c-124">Es más eficiente de los datos de tooupload en fragmentos mayores, pero no mayor que 1GB.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee6c-125">*¿Tiene una gran cantidad de tooanalyze de orígenes de datos?*</span><span class="sxs-lookup"><span data-stu-id="1ee6c-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="1ee6c-126">*Considere el uso de* logstash *tooship los datos en información de la aplicación.*</span><span class="sxs-lookup"><span data-stu-id="1ee6c-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="1ee6c-127">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="1ee6c-127">Before you start</span></span>

<span data-ttu-id="1ee6c-128">Necesita:</span><span class="sxs-lookup"><span data-stu-id="1ee6c-128">You need:</span></span>

1. <span data-ttu-id="1ee6c-129">Un recurso de Application Insights en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="1ee6c-130">Si desea que tooanalyze los datos por separado de los otro telemetría, [crear un nuevo recurso de Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1ee6c-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="1ee6c-131">Si va a combinar o comparar los datos con la telemetría desde una aplicación que ya está configurada con Application Insights, puede usar recursos de Hola para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="1ee6c-132">Recursos de toothat de acceso de propietario o colaborador.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="1ee6c-133">Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-133">Azure storage.</span></span> <span data-ttu-id="1ee6c-134">Cargar tooAzure almacenamiento y análisis obtiene los datos a partir de ahí.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="1ee6c-135">Se recomienda crear una cuenta de almacenamiento dedicado para los blobs.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="1ee6c-136">Si los blobs se comparten con otros procesos, se tarda más tiempo para nuestro tooread procesos los blobs.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="1ee6c-137">Definición del esquema</span><span class="sxs-lookup"><span data-stu-id="1ee6c-137">Define your schema</span></span>

<span data-ttu-id="1ee6c-138">Para poder importar datos, debe definir un *origen de datos,* que especifica el esquema de Hola de los datos.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="1ee6c-139">Puede tener hasta too50 orígenes de datos en un único recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="1ee6c-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="1ee6c-140">Inicie el Asistente para orígenes de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-140">Start hello data source wizard.</span></span> <span data-ttu-id="1ee6c-141">Use el botón "Agregar nuevo origen de datos".</span><span class="sxs-lookup"><span data-stu-id="1ee6c-141">Use "Add new data source" button.</span></span> <span data-ttu-id="1ee6c-142">También puede hacer clic en el botón de configuración en la esquina superior derecha y elegir "Orígenes de datos" en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Agregar nuevo origen de datos](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="1ee6c-144">Proporcione un nombre para el nuevo origen de datos.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="1ee6c-145">Definir el formato de los archivos de Hola que va a cargar.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="1ee6c-146">Puede definir manualmente el formato de Hola o cargar un archivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="1ee6c-147">Si los datos de hello están en formato CSV, Hola primera fila de ejemplo Hola puede ser encabezados de columna.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="1ee6c-148">Puede cambiar los nombres de campo de hello en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="1ee6c-149">ejemplo de Hola debe incluir al menos 10 filas o registros de datos.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="1ee6c-150">Los nombres de campo o columna deben ser alfanuméricos (sin espacios ni signos de puntuación).</span><span class="sxs-lookup"><span data-stu-id="1ee6c-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Carga de un archivo de ejemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="1ee6c-152">Esquema de Hola de revisión que Hola asistente tiene una capacidad.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="1ee6c-153">Si deduce tipos Hola de un ejemplo, tendrá que los tipos de hello inferir tooadjust de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Esquema de hello inferida de revisión](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="1ee6c-155">(Opcional). Cargue una definición de esquema.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="1ee6c-156">Consulte formato de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-156">See hello format below.</span></span>

 * <span data-ttu-id="1ee6c-157">Seleccione una marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-157">Select a Timestamp.</span></span> <span data-ttu-id="1ee6c-158">Todos los datos de Analytics deben tener un campo de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="1ee6c-159">Debe tener el tipo `datetime`, pero no es necesario toobe denominado 'timestamp'.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="1ee6c-160">Si los datos tienen una columna que contiene una fecha y hora en formato ISO, elija esta opción como columna de marca de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="1ee6c-161">En caso contrario, elija "como datos llegó" y proceso de importación de Hola agregará un campo de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="1ee6c-162">Crear origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="1ee6c-163">Formato del archivo de definición de esquema</span><span class="sxs-lookup"><span data-stu-id="1ee6c-163">Schema definition file format</span></span>

<span data-ttu-id="1ee6c-164">En lugar de modificar el esquema de hello en la interfaz de usuario, puede cargar la definición de esquema de Hola desde un archivo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="1ee6c-165">formato de definición de esquemas de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="1ee6c-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="1ee6c-166">Formato delimitado</span><span class="sxs-lookup"><span data-stu-id="1ee6c-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="1ee6c-167">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="1ee6c-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="1ee6c-168">Cada columna se identifica por tipo, nombre y ubicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="1ee6c-169">Ubicación: de archivo delimitado formatearlo es posición Hola del valor de hello asignado.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="1ee6c-170">Para el formato JSON, resulta jpath Hola de clave de hello asignado.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="1ee6c-171">Nombre: Hola muestra el nombre de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="1ee6c-172">Tipo: tipo de datos de Hola de esa columna.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="1ee6c-173">En caso de que se usan datos de muestra y está delimitada por el formato de archivo, definición de esquemas de hello debe asignar todas las columnas y agregar nuevas columnas al final de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="1ee6c-174">JSON permite una asignación parcial de los datos de hello, por lo tanto, hello definición de esquemas de formato JSON no tiene toomap todas las claves que se encuentra en datos de muestra.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="1ee6c-175">También pueden asignar las columnas que no forman parte de los datos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="1ee6c-176">Importar datos</span><span class="sxs-lookup"><span data-stu-id="1ee6c-176">Import data</span></span>

<span data-ttu-id="1ee6c-177">datos de tooimport, cargarlo tooAzure almacenamiento, crear una clave de acceso para él y, a continuación, realizar una llamada de API de REST.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Agregar nuevo origen de datos](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="1ee6c-179">Puede realizar Hola siguiendo el proceso manualmente o configurar un sistema automatizado toodo él a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="1ee6c-180">Necesita toofollow estos pasos para cada bloque de datos que desee tooimport.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="1ee6c-181">Cargar datos de hello demasiado[almacenamiento de blobs de Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="1ee6c-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="1ee6c-182">Blobs pueden tener cualquier tamaño la too1GB sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="1ee6c-183">Los blobs grandes de cientos de MB son ideales desde la perspectiva del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="1ee6c-184">Es posible comprimir con tiempo de carga tooimprove Gzip y latencia de hello datos toobe disponible para su consulta.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="1ee6c-185">Hola de uso `.gz` extensión de nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="1ee6c-186">Es mejor toouse una cuenta de almacenamiento independiente para este propósito, tooavoid llamadas de distintos servicios disminuyendo el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="1ee6c-187">Al enviar datos de alta frecuencia, cada pocos segundos, se recomienda toouse más de una cuenta de almacenamiento, por motivos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="1ee6c-188">[Crear una clave de firma de acceso compartido para el blob de hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="1ee6c-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="1ee6c-189">clave de Hello debe disponer de un período de expiración de un día y proporcionar acceso de lectura.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="1ee6c-190">Realizar una toonotify de llamada REST Application Insights que está esperando los datos.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="1ee6c-191">Punto de conexión: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="1ee6c-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="1ee6c-192">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="1ee6c-192">HTTP method: POST</span></span>
 * <span data-ttu-id="1ee6c-193">Carga útil:</span><span class="sxs-lookup"><span data-stu-id="1ee6c-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="1ee6c-194">marcadores de posición de Hello son:</span><span class="sxs-lookup"><span data-stu-id="1ee6c-194">hello placeholders are:</span></span>

* <span data-ttu-id="1ee6c-195">`Blob URI with Shared Access Key`: Puede obtener del procedimiento de Hola para crear una clave.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="1ee6c-196">Es blob toohello específico.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="1ee6c-197">`Schema ID`: Hola Id. del esquema generado para el esquema definido.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="1ee6c-198">datos de Hello en este blob deben cumplir toohello esquema.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="1ee6c-199">`DateTime`: hora de hello en qué Hola se envía la solicitud, UTC.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="1ee6c-200">Se aceptan estos formatos: ISO8601 (como "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="1ee6c-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="1ee6c-201">`Instrumentation key` del recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="1ee6c-202">datos de Hello están disponibles en el análisis después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="1ee6c-203">Respuestas de errores</span><span class="sxs-lookup"><span data-stu-id="1ee6c-203">Error responses</span></span>

* <span data-ttu-id="1ee6c-204">**400 Solicitud incorrecta**: indica que esa carga de la solicitud de hello es válido.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="1ee6c-205">Comprobar:</span><span class="sxs-lookup"><span data-stu-id="1ee6c-205">Check:</span></span>
 * <span data-ttu-id="1ee6c-206">Clave de instrumentación correcta.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="1ee6c-207">Valor de hora válido.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-207">Valid time value.</span></span> <span data-ttu-id="1ee6c-208">Debe ser tiempo Hola ahora en UTC.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="1ee6c-209">JSON de evento Hola cumple toohello esquema.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="1ee6c-210">**403 Prohibido**: blob Hola que ha enviado no es accesible.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="1ee6c-211">Asegúrese de que esa clave de acceso compartido hello es válida y no ha expirado.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="1ee6c-212">**404 No encontrado**:</span><span class="sxs-lookup"><span data-stu-id="1ee6c-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="1ee6c-213">no existe el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="1ee6c-214">Hola sourceId es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="1ee6c-215">Información más detallada está disponible en el mensaje de error de respuesta de saludo.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="1ee6c-216">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1ee6c-216">Sample code</span></span>

<span data-ttu-id="1ee6c-217">Este código usa hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="1ee6c-218">Clases</span><span class="sxs-lookup"><span data-stu-id="1ee6c-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="1ee6c-219">Introducir datos</span><span class="sxs-lookup"><span data-stu-id="1ee6c-219">Ingest data</span></span>

<span data-ttu-id="1ee6c-220">Use este código para cada blob.</span><span class="sxs-lookup"><span data-stu-id="1ee6c-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="1ee6c-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ee6c-221">Next steps</span></span>

* [<span data-ttu-id="1ee6c-222">Paseo de hello lenguaje de consultas de análisis de registros</span><span class="sxs-lookup"><span data-stu-id="1ee6c-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="1ee6c-223">Use *Logstash* toosend datos tooApplication visión</span><span class="sxs-lookup"><span data-stu-id="1ee6c-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
