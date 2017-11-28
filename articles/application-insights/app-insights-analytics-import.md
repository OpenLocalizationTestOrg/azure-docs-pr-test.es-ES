---
title: "Importación de datos a Analytics en Azure Application Insights | Microsoft Docs"
description: "Importe datos estadísticos para asociarlos con la telemetría de la aplicación, o bien importe un flujo de datos independiente para consultar con Analytics."
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
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="b5e1a-104">Importación de datos a Analytics</span><span class="sxs-lookup"><span data-stu-id="b5e1a-104">Import data into Analytics</span></span>

<span data-ttu-id="b5e1a-105">Importe los datos tabulares en [Analytics](app-insights-analytics.md), ya sea para combinarlos con la telemetría de [Application Insights](app-insights-overview.md) de la aplicación, o bien para poder analizarlos como un flujo independiente.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="b5e1a-106">Analytics es un sólido lenguaje de consulta adecuado para analizar flujos de telemetría con marcas de tiempo de alto volumen.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="b5e1a-107">Puede importar datos en Analytics mediante un esquema propio.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="b5e1a-108">No tiene que utilizar los esquemas de Application Insights estándar como solicitud o seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="b5e1a-109">Puede importar archivos JSON o DSV (valores separados por delimitadores, como pueden ser comas, puntos y coma o tabulaciones).</span><span class="sxs-lookup"><span data-stu-id="b5e1a-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="b5e1a-110">Existen tres situaciones donde es útil importar a Analytics:</span><span class="sxs-lookup"><span data-stu-id="b5e1a-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="b5e1a-111">**Combinar con la telemetría de la aplicación.**</span><span class="sxs-lookup"><span data-stu-id="b5e1a-111">**Join with app telemetry.**</span></span> <span data-ttu-id="b5e1a-112">Por ejemplo, puede importar una tabla que asigna las direcciones URL de un sitio web a los títulos de página más legibles.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="b5e1a-113">En Analytics, puede crear un informe gráfico de panel que muestra las diez páginas más populares del sitio web.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="b5e1a-114">Ahora puede mostrar los títulos de página en lugar de las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="b5e1a-115">**Correlacionar la telemetría de la aplicación** con otros orígenes, como tráfico de red, datos de servidor o archivos de registro de red CDN.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="b5e1a-116">**Aplicar Analytics a un flujo de datos independiente.**</span><span class="sxs-lookup"><span data-stu-id="b5e1a-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="b5e1a-117">Application Insights de Analytics es una herramienta eficaz, que funciona bien con flujos dispersos con marca de tiempo; en muchos casos, de manera mucho mejor que SQL.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="b5e1a-118">Si tiene un flujo de este tipo de algún otro origen, puede analizarlo con Analytics.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="b5e1a-119">Enviar datos al origen de datos es fácil.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="b5e1a-120">(Una vez) Defina el esquema de los datos en un "origen de datos".</span><span class="sxs-lookup"><span data-stu-id="b5e1a-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="b5e1a-121">(Periódicamente) Cargue datos en Azure Storage y llame a la API de REST para avisar de que está esperando la ingesta de nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="b5e1a-122">En unos pocos minutos, los datos están disponibles para consultarlos en Analytics.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="b5e1a-123">El usuario define la frecuencia de carga y la rapidez con que desea que los datos estén disponibles para consultarlos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="b5e1a-124">Es más eficaz cargar datos en fragmentos más grandes, pero que no superen 1 GB.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="b5e1a-125">*¿Tiene muchos orígenes de datos para analizar?*</span><span class="sxs-lookup"><span data-stu-id="b5e1a-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="b5e1a-126">*Considere el uso de* logstash *para enviar los datos a Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="b5e1a-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="b5e1a-127">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="b5e1a-127">Before you start</span></span>

<span data-ttu-id="b5e1a-128">Necesita:</span><span class="sxs-lookup"><span data-stu-id="b5e1a-128">You need:</span></span>

1. <span data-ttu-id="b5e1a-129">Un recurso de Application Insights en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="b5e1a-130">Si desea analizar los datos por separado de los otro datos de telemetría, [cree un nuevo recurso de Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b5e1a-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="b5e1a-131">Si va a combinar o comparar los datos con la telemetría de una aplicación que ya está configurada con Application Insights, puede usar el recurso para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="b5e1a-132">Propietario o colaborador de acceso a ese recurso.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="b5e1a-133">Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-133">Azure storage.</span></span> <span data-ttu-id="b5e1a-134">Cargue datos en Azure Storage, y Analytics obtiene los datos de ahí.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="b5e1a-135">Se recomienda crear una cuenta de almacenamiento dedicado para los blobs.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="b5e1a-136">Si los blobs se comparten con otros procesos, los procesos tardan más tiempo en leer los blobs.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="b5e1a-137">Definición del esquema</span><span class="sxs-lookup"><span data-stu-id="b5e1a-137">Define your schema</span></span>

<span data-ttu-id="b5e1a-138">Para poder importar datos, debe definir un *origen de datos,* que especifica el esquema de los datos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="b5e1a-139">Puede tener hasta 50 orígenes de datos en un único recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="b5e1a-140">Inicie el Asistente para orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-140">Start the data source wizard.</span></span> <span data-ttu-id="b5e1a-141">Use el botón "Agregar nuevo origen de datos".</span><span class="sxs-lookup"><span data-stu-id="b5e1a-141">Use "Add new data source" button.</span></span> <span data-ttu-id="b5e1a-142">También puede hacer clic en el botón de configuración en la esquina superior derecha y elegir "Orígenes de datos" en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Agregar nuevo origen de datos](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="b5e1a-144">Proporcione un nombre para el nuevo origen de datos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="b5e1a-145">Defina el formato de los archivos que va a cargar.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="b5e1a-146">Puede definir manualmente el formato o cargar un archivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="b5e1a-147">Si los datos tienen el formato CSV, la primera fila del ejemplo puede corresponderse con encabezados de columna.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="b5e1a-148">Puede cambiar los nombres de campo en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="b5e1a-149">El ejemplo debe incluir al menos 10 filas o registros de datos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="b5e1a-150">Los nombres de campo o columna deben ser alfanuméricos (sin espacios ni signos de puntuación).</span><span class="sxs-lookup"><span data-stu-id="b5e1a-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Carga de un archivo de ejemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="b5e1a-152">Revise el esquema que ha obtenido el asistente.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="b5e1a-153">Si infirió los tipos de un ejemplo, probablemente tenga que ajustar los tipos inferidos de las columnas.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![Revisión del esquema inferido](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="b5e1a-155">(Opcional). Cargue una definición de esquema.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="b5e1a-156">Consulte el formato siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-156">See the format below.</span></span>

 * <span data-ttu-id="b5e1a-157">Seleccione una marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-157">Select a Timestamp.</span></span> <span data-ttu-id="b5e1a-158">Todos los datos de Analytics deben tener un campo de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="b5e1a-159">Debe tener el tipo `datetime`, pero no es necesario asignarle el nombre "marca de tiempo".</span><span class="sxs-lookup"><span data-stu-id="b5e1a-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="b5e1a-160">Si los datos tienen una columna que contiene una fecha y hora en formato ISO, elija esta opción como la columna de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="b5e1a-161">En caso contrario, elija "as data arrived" (cuando llegan los datos), y el proceso de importación agregará un campo de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="b5e1a-162">Cree el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="b5e1a-163">Formato del archivo de definición de esquema</span><span class="sxs-lookup"><span data-stu-id="b5e1a-163">Schema definition file format</span></span>

<span data-ttu-id="b5e1a-164">En lugar de editar el esquema en la IU, puede cargar la definición de esquema de un archivo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="b5e1a-165">El formato de definición de esquema es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b5e1a-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="b5e1a-166">Formato delimitado</span><span class="sxs-lookup"><span data-stu-id="b5e1a-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="b5e1a-167">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="b5e1a-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="b5e1a-168">Cada columna se identifica por la ubicación, el nombre y el tipo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="b5e1a-169">Ubicación: Para formato de archivo delimitado es la posición del valor asignado.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="b5e1a-170">Para el formato JSON, es el jpath de la clave asignada.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="b5e1a-171">Nombre: Nombre que se muestra de la columna.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="b5e1a-172">Tipo: Tipo de datos de esa columna.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="b5e1a-173">En caso de que se usen datos de ejemplo y el formato de archivo esté delimitado, la definición de esquema debe asignar todas las columnas y agregar nuevas columnas al final.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="b5e1a-174">JSON permite una asignación parcial de los datos, por lo que la definición de esquema de formato JSON no tiene que asignar cada clave que se encuentra en los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="b5e1a-175">También pueden asignar las columnas que no forman parte de los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="b5e1a-176">Importar datos</span><span class="sxs-lookup"><span data-stu-id="b5e1a-176">Import data</span></span>

<span data-ttu-id="b5e1a-177">Para importar datos, cárguelos en Azure Storage, cree una clave de acceso para ellos y después realice una llamada a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![Agregar nuevo origen de datos](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="b5e1a-179">Puede llevar a cabo el siguiente proceso manualmente o configurar un sistema automatizado para hacerlo a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="b5e1a-180">Debe seguir estos pasos para cada bloque de datos que desea importar.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="b5e1a-181">Cargue los datos en [Azure Blob Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="b5e1a-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="b5e1a-182">Los blobs pueden tener un tamaño de hasta 1 GB sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="b5e1a-183">Los blobs grandes de cientos de MB son ideales desde la perspectiva del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="b5e1a-184">Es posible comprimir con Gzip para mejorar el tiempo de carga y la latencia de los datos, a fin de que estén disponibles para consultarlos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="b5e1a-185">Use la extensión de nombre de archivo `.gz`.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="b5e1a-186">Se recomienda usar una cuenta de almacenamiento independiente para este fin, con el fin de evitar que se realicen llamadas de distintos servicios, lo que empeora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="b5e1a-187">Al enviar datos de alta frecuencia, cada pocos segundos, se recomienda utilizar más de una cuenta de almacenamiento, por motivos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="b5e1a-188">[Cree una clave de firma de acceso compartido para el blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="b5e1a-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="b5e1a-189">La clave debe tener un período de caducidad de un día y proporcionar acceso de lectura.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="b5e1a-190">Realice una llamada de REST para notificar a Application Insights que hay datos en espera.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="b5e1a-191">Punto de conexión: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="b5e1a-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="b5e1a-192">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="b5e1a-192">HTTP method: POST</span></span>
 * <span data-ttu-id="b5e1a-193">Carga útil:</span><span class="sxs-lookup"><span data-stu-id="b5e1a-193">Payload:</span></span>

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

<span data-ttu-id="b5e1a-194">Los marcadores de posición son:</span><span class="sxs-lookup"><span data-stu-id="b5e1a-194">The placeholders are:</span></span>

* <span data-ttu-id="b5e1a-195">`Blob URI with Shared Access Key`: puede obtener esta información con el procedimiento para crear una clave.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="b5e1a-196">Es específico para el blob.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-196">It is specific to the blob.</span></span>
* <span data-ttu-id="b5e1a-197">`Schema ID`: el identificador de esquema generado para el esquema definido.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="b5e1a-198">Los datos de este blob deben cumplir el esquema.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="b5e1a-199">`DateTime`: la hora a la que se envía la solicitud, UTC.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="b5e1a-200">Se aceptan estos formatos: ISO8601 (como "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="b5e1a-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="b5e1a-201">`Instrumentation key` del recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="b5e1a-202">Los datos se encuentran disponibles en Analytics después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="b5e1a-203">Respuestas de errores</span><span class="sxs-lookup"><span data-stu-id="b5e1a-203">Error responses</span></span>

* <span data-ttu-id="b5e1a-204">**400 - Solicitud incorrecta**: indica que la carga útil de solicitud no es válida.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="b5e1a-205">Comprobar:</span><span class="sxs-lookup"><span data-stu-id="b5e1a-205">Check:</span></span>
 * <span data-ttu-id="b5e1a-206">Clave de instrumentación correcta.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="b5e1a-207">Valor de hora válido.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-207">Valid time value.</span></span> <span data-ttu-id="b5e1a-208">La hora debe reflejarse ahora en UTC.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="b5e1a-209">El JSON del evento se ajusta al esquema.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="b5e1a-210">**403 Prohibido**: no se puede acceder al blob enviado.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="b5e1a-211">Asegúrese de que la clave de acceso compartido es válida y no ha expirado.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="b5e1a-212">**404 No encontrado**:</span><span class="sxs-lookup"><span data-stu-id="b5e1a-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="b5e1a-213">El blob no existe.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="b5e1a-214">El identificador de origen es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-214">The sourceId is wrong.</span></span>

<span data-ttu-id="b5e1a-215">Se puede encontrar información más detallada en el mensaje de error de respuesta.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="b5e1a-216">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b5e1a-216">Sample code</span></span>

<span data-ttu-id="b5e1a-217">Este código usa el paquete NuGet [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1).</span><span class="sxs-lookup"><span data-stu-id="b5e1a-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="b5e1a-218">Clases</span><span class="sxs-lookup"><span data-stu-id="b5e1a-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="b5e1a-219">Introducir datos</span><span class="sxs-lookup"><span data-stu-id="b5e1a-219">Ingest data</span></span>

<span data-ttu-id="b5e1a-220">Use este código para cada blob.</span><span class="sxs-lookup"><span data-stu-id="b5e1a-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="b5e1a-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5e1a-221">Next steps</span></span>

* [<span data-ttu-id="b5e1a-222">Paseo por el lenguaje de consulta de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b5e1a-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="b5e1a-223">Use *Logstash* para enviar datos a Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5e1a-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
