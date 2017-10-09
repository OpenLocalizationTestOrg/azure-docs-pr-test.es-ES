---
title: "aaaScheduling y la ejecución con factoría de datos | Documentos de Microsoft"
description: "Obtenga información sobre los aspectos de programación y ejecución del modelo de aplicación de Factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="a9df0-103">Programación y ejecución de Data Factory</span><span class="sxs-lookup"><span data-stu-id="a9df0-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="a9df0-104">En este artículo se explica los aspectos de programación y la ejecución de Hola Hola Data Factory de Azure del modelo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9df0-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="a9df0-105">En este artículo se presupone que comprende los conceptos básicos del modelo de aplicación de Data Factory, como la actividad, las canalizaciones, los servicios vinculados y los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="a9df0-106">Para los conceptos básicos de la factoría de datos de Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="a9df0-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="a9df0-107">Introducción tooData generador</span><span class="sxs-lookup"><span data-stu-id="a9df0-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="a9df0-108">Procesos</span><span class="sxs-lookup"><span data-stu-id="a9df0-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="a9df0-109">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="a9df0-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="a9df0-110">Horas de inicio y finalización de la canalización</span><span class="sxs-lookup"><span data-stu-id="a9df0-110">Start and end times of pipeline</span></span>
<span data-ttu-id="a9df0-111">Una canalización solo está activa entre su hora de **inicio** y de **finalización**.</span><span class="sxs-lookup"><span data-stu-id="a9df0-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="a9df0-112">No se ejecuta antes de la hora de inicio de Hola o después de la hora de finalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="a9df0-113">Si se pausa la canalización de hello, no se ejecuta independientemente de su hora de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="a9df0-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="a9df0-114">Para una toorun de canalización, se debe no se produce la pausa.</span><span class="sxs-lookup"><span data-stu-id="a9df0-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="a9df0-115">Encontrar estos valores (inicio, fin, en pausa) en la definición de la canalización de hello:</span><span class="sxs-lookup"><span data-stu-id="a9df0-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="a9df0-116">Para más información sobre estas propiedades, vea el artículo sobre la [creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a9df0-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="a9df0-117">Definición de la programación de una actividad</span><span class="sxs-lookup"><span data-stu-id="a9df0-117">Specify schedule for an activity</span></span>
<span data-ttu-id="a9df0-118">No es canalización Hola que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="a9df0-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="a9df0-119">Es actividades de Hola de canalización de Hola que se ejecutan en hello contexto general de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="a9df0-120">Puede especificar una programación periódica para una actividad mediante hello **programador** sección de JSON de la actividad.</span><span class="sxs-lookup"><span data-stu-id="a9df0-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="a9df0-121">Por ejemplo, puede programar una actividad toorun cada hora como sigue:</span><span class="sxs-lookup"><span data-stu-id="a9df0-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="a9df0-122">Como se muestra en hello siguiente diagrama, especificar que una programación para una actividad crea una serie de ventanas de saltos de tamaño constante con Hola de canalización de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="a9df0-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="a9df0-123">Las ventanas de saltos de tamaño constante son series de intervalos de tiempo de tamaño fijo, no superpuestos y contiguos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="a9df0-124">Estas ventanas de saltos lógicas de tamaño constante para la actividad se denominan **ventanas de actividad**.</span><span class="sxs-lookup"><span data-stu-id="a9df0-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Ejemplo de programador de actividades](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="a9df0-126">Hola **programador** propiedad para una actividad es opcional.</span><span class="sxs-lookup"><span data-stu-id="a9df0-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="a9df0-127">Si se especifica esta propiedad, debe coincidir con el ritmo de hello especificado en la definición de hello del conjunto de datos de salida para la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="a9df0-128">Actualmente, el conjunto de datos de salida es qué unidades Hola programación.</span><span class="sxs-lookup"><span data-stu-id="a9df0-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="a9df0-129">Por lo tanto, debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="a9df0-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="a9df0-130">Definición de la programación de un conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="a9df0-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="a9df0-131">Una actividad de una canalización de Data Factory puede tomar diversos **conjuntos de datos** de entrada, o ninguno, y generar uno o varios conjuntos de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="a9df0-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="a9df0-132">Para una actividad, puede especificar el ritmo de hello en qué Hola datos de entrada están disponibles o se generan los datos de salida de hello mediante hello **disponibilidad** sección en definiciones de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="a9df0-133">**Frecuencia** en hello **disponibilidad** sección especifica la unidad de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="a9df0-134">Hola valores permitidos para la frecuencia son: minuto, hora, día, semana y mes.</span><span class="sxs-lookup"><span data-stu-id="a9df0-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="a9df0-135">Hola **intervalo** propiedad en la sección de disponibilidad de hello especifica un multiplicador para la frecuencia.</span><span class="sxs-lookup"><span data-stu-id="a9df0-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="a9df0-136">Por ejemplo: si establece frecuencia de hello tooDay e intervalo se establece too1 para un conjunto de datos de salida, los datos de salida de hello se generan cada día.</span><span class="sxs-lookup"><span data-stu-id="a9df0-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="a9df0-137">Si especifica Hola frecuencia como minuto, se recomienda que establezca Hola intervalo toono inferior a 15.</span><span class="sxs-lookup"><span data-stu-id="a9df0-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="a9df0-138">En el siguiente ejemplo de Hola, datos de entrada de hello están disponibles por hora y los datos de salida de hello se producen cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="a9df0-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="a9df0-139">**Conjunto de datos de entrada:**</span><span class="sxs-lookup"><span data-stu-id="a9df0-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="a9df0-140">**Conjunto de datos de salida**</span><span class="sxs-lookup"><span data-stu-id="a9df0-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="a9df0-141">Actualmente, **programación de Hola de unidades de conjunto de datos de salida**.</span><span class="sxs-lookup"><span data-stu-id="a9df0-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="a9df0-142">En otras palabras, programación de hello especificada para el conjunto de datos de salida de hello es toorun usa una actividad en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a9df0-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="a9df0-143">Por lo tanto, debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="a9df0-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="a9df0-144">Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada.</span><span class="sxs-lookup"><span data-stu-id="a9df0-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="a9df0-145">En los siguientes Hola canalización definición, hello **programador** propiedad es programación toospecify usado para la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="a9df0-146">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="a9df0-146">This property is optional.</span></span> <span data-ttu-id="a9df0-147">Actualmente, programación de hello para la actividad de hello debe coincidir con programación de hello especificada para el conjunto de datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a9df0-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="a9df0-148">En este ejemplo, cada hora se ejecuta de actividad de hello entre Hola hora inicial y final de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="a9df0-149">datos de salida de saludo se produce cada hora para windows de tres horas (8 A.M. - 9 AM, 9 a 10 AM y a 10 11 AM).</span><span class="sxs-lookup"><span data-stu-id="a9df0-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="a9df0-150">Cada unidad de datos consumida o producida por la ejecución de una actividad se denomina **segmento de datos**.</span><span class="sxs-lookup"><span data-stu-id="a9df0-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="a9df0-151">Hola siguiente diagrama muestra un ejemplo de una actividad con un conjunto de datos de entrada y un conjunto de datos de salida:</span><span class="sxs-lookup"><span data-stu-id="a9df0-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Programador de disponibilidad](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="a9df0-153">diagrama de Hello muestra cada hora Hola segmentos de datos de Hola de entrada y salida de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="a9df0-154">diagrama de Hello muestra tres segmentos de entrada que están listos para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="a9df0-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="a9df0-155">actividad de 10-11 AM Hello está en curso, que produce el segmento de salida de hello 10-11 AM.</span><span class="sxs-lookup"><span data-stu-id="a9df0-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="a9df0-156">Puede tener acceso a intervalo de tiempo de hello asociado con el intervalo actual de Hola Hola de conjunto de datos JSON mediante variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) y [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="a9df0-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="a9df0-157">De forma similar, puede tener acceso a intervalo de tiempo de hello asociado con una ventana de actividad utilizando hello WindowStart y WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="a9df0-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="a9df0-158">programación Hola de una actividad debe coincidir con la programación de hello del conjunto de datos de salida de hello para la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="a9df0-159">Por lo tanto, Hola SliceStart y SliceEnd valores son Hola mismo como valores WindowStart y WindowEnd respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a9df0-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="a9df0-160">Para más información sobre estas variables, vea el artículo [Funciones y variables del sistema](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="a9df0-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="a9df0-161">Puede usar estas variables para distintos fines en el JSON de actividad.</span><span class="sxs-lookup"><span data-stu-id="a9df0-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="a9df0-162">Por ejemplo, puede utilizarlas tooselect datos de entrada y salida conjuntos de datos que representa datos de serie temporal (por ejemplo: ESTOY too9 de 8 A.M.).</span><span class="sxs-lookup"><span data-stu-id="a9df0-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="a9df0-163">Este ejemplo también utiliza **WindowStart** y **WindowEnd** tooselect datos relevantes para una actividad ejecutar y cópielo tooa blob con hello adecuado **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="a9df0-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="a9df0-164">Hola **folderPath** es toohave con parámetros en una carpeta independiente para cada hora.</span><span class="sxs-lookup"><span data-stu-id="a9df0-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="a9df0-165">En el anterior ejemplo de Hola, programación de hello especificada para los conjuntos de datos de entrada y salida se Hola igual (cada hora).</span><span class="sxs-lookup"><span data-stu-id="a9df0-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="a9df0-166">Si Hola entrada conjunto de datos de actividad hello está disponible en una frecuencia distinta, digamos cada 15 minutos, actividad de hello generadas por este conjunto de datos de salida sigue ejecutándose una vez cada hora como conjunto de datos de salida de hello es qué unidades Hola programación de actividades.</span><span class="sxs-lookup"><span data-stu-id="a9df0-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="a9df0-167">Para más información, vea [Modelado de conjuntos de datos con distintas frecuencias](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="a9df0-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="a9df0-168">Directivas y disponibilidad del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="a9df0-168">Dataset availability and policies</span></span>
<span data-ttu-id="a9df0-169">Se muestra el uso de Hola de frecuencia y el intervalo de propiedades en la sección de disponibilidad de Hola de definición de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="a9df0-170">Hay algunas propiedades que afectan a la programación de Hola y la ejecución de una actividad.</span><span class="sxs-lookup"><span data-stu-id="a9df0-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="a9df0-171">Conjunto de datos availability</span><span class="sxs-lookup"><span data-stu-id="a9df0-171">Dataset availability</span></span> 
<span data-ttu-id="a9df0-172">Hello tabla siguiente describen propiedades que puede utilizar en hello **disponibilidad** sección:</span><span class="sxs-lookup"><span data-stu-id="a9df0-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="a9df0-173">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a9df0-173">Property</span></span> | <span data-ttu-id="a9df0-174">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9df0-174">Description</span></span> | <span data-ttu-id="a9df0-175">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a9df0-175">Required</span></span> | <span data-ttu-id="a9df0-176">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="a9df0-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9df0-177">frequency</span><span class="sxs-lookup"><span data-stu-id="a9df0-177">frequency</span></span> |<span data-ttu-id="a9df0-178">Especifica la unidad de tiempo de hello para la producción de segmento del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="a9df0-179"><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="a9df0-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="a9df0-180">Sí</span><span class="sxs-lookup"><span data-stu-id="a9df0-180">Yes</span></span> |<span data-ttu-id="a9df0-181">N/D</span><span class="sxs-lookup"><span data-stu-id="a9df0-181">NA</span></span> |
| <span data-ttu-id="a9df0-182">interval</span><span class="sxs-lookup"><span data-stu-id="a9df0-182">interval</span></span> |<span data-ttu-id="a9df0-183">Especifica un multiplicador para frecuencia</span><span class="sxs-lookup"><span data-stu-id="a9df0-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="a9df0-184">"Intervalo de frecuencia x" determina con qué frecuencia hello segmento se genera.</span><span class="sxs-lookup"><span data-stu-id="a9df0-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="a9df0-185">Si necesita hello toobe de conjunto de datos se crean sectores de cada hora, establecer <b>frecuencia</b> demasiado<b>hora</b>, y <b>intervalo</b> demasiado<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="a9df0-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="a9df0-186"><b>Tenga en cuenta</b>: si especifica frecuencia como minuto, se recomienda que establezca Hola intervalo toono inferior a 15</span><span class="sxs-lookup"><span data-stu-id="a9df0-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="a9df0-187">Sí</span><span class="sxs-lookup"><span data-stu-id="a9df0-187">Yes</span></span> |<span data-ttu-id="a9df0-188">N/D</span><span class="sxs-lookup"><span data-stu-id="a9df0-188">NA</span></span> |
| <span data-ttu-id="a9df0-189">style</span><span class="sxs-lookup"><span data-stu-id="a9df0-189">style</span></span> |<span data-ttu-id="a9df0-190">Especifica si se debe generar segmento hello en hello inicio/final del intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="a9df0-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="a9df0-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="a9df0-191">StartOfInterval</span></span></li><li><span data-ttu-id="a9df0-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="a9df0-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="a9df0-193">Si se establece la frecuencia de tooMonth y se establece el estilo tooEndOfInterval, Hola segmento se genera Hola último día del mes.</span><span class="sxs-lookup"><span data-stu-id="a9df0-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="a9df0-194">Si se establece tooStartOfInterval en estilo de hello, Hola segmento se genera en hello primer día del mes.</span><span class="sxs-lookup"><span data-stu-id="a9df0-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="a9df0-195">Si se establece la frecuencia de tooDay y se establece el estilo tooEndOfInterval, segmento de Hola se genera en la última hora del día de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="a9df0-196">Si se establece la frecuencia de tooHour y se establece el estilo tooEndOfInterval, segmento de Hola se genera al final de Hola de hora de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="a9df0-197">Por ejemplo, para un intervalo durante el período de 1 P.M. – 2 P.M., segmento de Hola se genera a las 2 P.M..</span><span class="sxs-lookup"><span data-stu-id="a9df0-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="a9df0-198">No</span><span class="sxs-lookup"><span data-stu-id="a9df0-198">No</span></span> |<span data-ttu-id="a9df0-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="a9df0-199">EndOfInterval</span></span> |
| <span data-ttu-id="a9df0-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="a9df0-200">anchorDateTime</span></span> |<span data-ttu-id="a9df0-201">Define la posición absoluta de hello en el tiempo utilizado por los límites del sector de programador toocompute conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="a9df0-202"><b>Tenga en cuenta</b>: si hello AnchorDateTime tiene Dateparts más granulares que la frecuencia de hello, hello partes más pormenorizadas se omiten.</span><span class="sxs-lookup"><span data-stu-id="a9df0-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="a9df0-203">Por ejemplo, si hello <b>intervalo</b> es <b>cada hora</b> (frecuencia: hora e intervalo: 1) hello y <b>AnchorDateTime</b> contiene <b>minutos y segundos</b>, a continuación, Hola <b>minutos y segundos</b> partes de hello AnchorDateTime se omiten.</span><span class="sxs-lookup"><span data-stu-id="a9df0-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="a9df0-204">No</span><span class="sxs-lookup"><span data-stu-id="a9df0-204">No</span></span> |<span data-ttu-id="a9df0-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="a9df0-205">01/01/0001</span></span> |
| <span data-ttu-id="a9df0-206">Offset</span><span class="sxs-lookup"><span data-stu-id="a9df0-206">offset</span></span> |<span data-ttu-id="a9df0-207">Intervalo de tiempo por qué Hola se desplazan inicial y final de todos los sectores de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="a9df0-208"><b>Tenga en cuenta</b>: si se especifican anchorDateTime y offset, resultado de hello es Hola combinan MAYÚS.</span><span class="sxs-lookup"><span data-stu-id="a9df0-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="a9df0-209">No</span><span class="sxs-lookup"><span data-stu-id="a9df0-209">No</span></span> |<span data-ttu-id="a9df0-210">N/D</span><span class="sxs-lookup"><span data-stu-id="a9df0-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="a9df0-211">Ejemplo de offset</span><span class="sxs-lookup"><span data-stu-id="a9df0-211">offset example</span></span>
<span data-ttu-id="a9df0-212">De forma predeterminada, cada día (`"frequency": "Day", "interval": 1`) se inician los segmentos a las 24:00 UTC (medianoche).</span><span class="sxs-lookup"><span data-stu-id="a9df0-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="a9df0-213">Si desea Hola inicio toobe 6: 00 UTC hora en su lugar, establezca Hola offset tal como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="a9df0-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="a9df0-214">Ejemplo de anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="a9df0-214">anchorDateTime example</span></span>
<span data-ttu-id="a9df0-215">En el siguiente ejemplo de Hola Hola conjunto de datos se produce una vez cada 23 horas.</span><span class="sxs-lookup"><span data-stu-id="a9df0-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="a9df0-216">Hello primer sector comienza en tiempo de hello especificado por anchorDateTime hello, que se establece demasiado`2017-04-19T08:00:00` (hora UTC).</span><span class="sxs-lookup"><span data-stu-id="a9df0-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="a9df0-217">Ejemplo de desplazamiento y estilo</span><span class="sxs-lookup"><span data-stu-id="a9df0-217">offset/style Example</span></span>
<span data-ttu-id="a9df0-218">es un conjunto de datos mensual Hello siguiente conjunto de datos y se genera en 3rd de cada mes a las 8:00 A.M. (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="a9df0-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="a9df0-219">Directiva del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="a9df0-219">Dataset policy</span></span>
<span data-ttu-id="a9df0-220">Un conjunto de datos puede tener una directiva de validación definida que especifica cómo se pueden validar los datos de hello generados por la ejecución de un segmento antes de que está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="a9df0-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="a9df0-221">En tales casos, después de que ha terminado de ejecutarse, segmento de Hola Hola salida segmento se cambia el estado demasiado**espera** con un subestado de **validación**.</span><span class="sxs-lookup"><span data-stu-id="a9df0-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="a9df0-222">Después de validan intervalos de hello, estado del sector Hola cambia demasiado**listo**.</span><span class="sxs-lookup"><span data-stu-id="a9df0-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="a9df0-223">Si se ha generado un segmento de datos, pero no superó la validación de hello, no se procesan las ejecuciones de actividad de intervalos de nivel inferiores que dependen de este segmento.</span><span class="sxs-lookup"><span data-stu-id="a9df0-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="a9df0-224">[Supervisar y administrar las canalizaciones](data-factory-monitor-manage-pipelines.md) portadas Hola diversos estados de segmentos de datos en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="a9df0-225">Hola **directiva** sección de definición de conjunto de datos define los criterios de Hola o debe cumplir la condición de Hola que Hola segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="a9df0-226">Hello tabla siguiente describen propiedades que puede utilizar en hello **directiva** sección:</span><span class="sxs-lookup"><span data-stu-id="a9df0-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="a9df0-227">Nombre de la directiva</span><span class="sxs-lookup"><span data-stu-id="a9df0-227">Policy Name</span></span> | <span data-ttu-id="a9df0-228">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9df0-228">Description</span></span> | <span data-ttu-id="a9df0-229">Aplica demasiado</span><span class="sxs-lookup"><span data-stu-id="a9df0-229">Applied too</span></span>| <span data-ttu-id="a9df0-230">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a9df0-230">Required</span></span> | <span data-ttu-id="a9df0-231">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="a9df0-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a9df0-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="a9df0-232">minimumSizeMB</span></span> | <span data-ttu-id="a9df0-233">Valida datos hello en un **blobs de Azure** Hola de cumple los requisitos mínimos de tamaño (en megabytes).</span><span class="sxs-lookup"><span data-stu-id="a9df0-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="a9df0-234">Blob de Azure</span><span class="sxs-lookup"><span data-stu-id="a9df0-234">Azure Blob</span></span> |<span data-ttu-id="a9df0-235">No</span><span class="sxs-lookup"><span data-stu-id="a9df0-235">No</span></span> |<span data-ttu-id="a9df0-236">N/D</span><span class="sxs-lookup"><span data-stu-id="a9df0-236">NA</span></span> |
| <span data-ttu-id="a9df0-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="a9df0-237">minimumRows</span></span> | <span data-ttu-id="a9df0-238">Valida datos hello en un **base de datos SQL de Azure** o un **tabla de Azure** contiene Hola número mínimo de filas.</span><span class="sxs-lookup"><span data-stu-id="a9df0-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="a9df0-239">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a9df0-239">Azure SQL Database</span></span></li><li><span data-ttu-id="a9df0-240">tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="a9df0-240">Azure Table</span></span></li></ul> |<span data-ttu-id="a9df0-241">No</span><span class="sxs-lookup"><span data-stu-id="a9df0-241">No</span></span> |<span data-ttu-id="a9df0-242">N/D</span><span class="sxs-lookup"><span data-stu-id="a9df0-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="a9df0-243">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a9df0-243">Examples</span></span>
<span data-ttu-id="a9df0-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="a9df0-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="a9df0-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="a9df0-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="a9df0-246">Para consultar ejemplos y más información sobre estas propiedades, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="a9df0-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="a9df0-247">Directivas de la actividad</span><span class="sxs-lookup"><span data-stu-id="a9df0-247">Activity policies</span></span>
<span data-ttu-id="a9df0-248">Las directivas afectan al comportamiento de tiempo de ejecución de Hola de una actividad, específicamente cuando se procesa el sector de Hola de una tabla.</span><span class="sxs-lookup"><span data-stu-id="a9df0-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="a9df0-249">Hello en la tabla siguiente proporciona detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="a9df0-250">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a9df0-250">Property</span></span> | <span data-ttu-id="a9df0-251">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="a9df0-251">Permitted values</span></span> | <span data-ttu-id="a9df0-252">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="a9df0-252">Default Value</span></span> | <span data-ttu-id="a9df0-253">Description</span><span class="sxs-lookup"><span data-stu-id="a9df0-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9df0-254">simultaneidad</span><span class="sxs-lookup"><span data-stu-id="a9df0-254">concurrency</span></span> |<span data-ttu-id="a9df0-255">Entero </span><span class="sxs-lookup"><span data-stu-id="a9df0-255">Integer</span></span> <br/><br/><span data-ttu-id="a9df0-256">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="a9df0-256">Max value: 10</span></span> |<span data-ttu-id="a9df0-257">1</span><span class="sxs-lookup"><span data-stu-id="a9df0-257">1</span></span> |<span data-ttu-id="a9df0-258">Número de ejecuciones simultáneas de actividad hello.</span><span class="sxs-lookup"><span data-stu-id="a9df0-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="a9df0-259">Determina el número de Hola de ejecuciones paralelas que pueden ocurrir en distintos sectores.</span><span class="sxs-lookup"><span data-stu-id="a9df0-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="a9df0-260">Por ejemplo, si una actividad tiene toogo a través de un conjunto grande de datos disponibles, que tienen un valor mayor de simultaneidad acelera el procesamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="a9df0-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="a9df0-261">executionPriorityOrder</span></span> |<span data-ttu-id="a9df0-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="a9df0-262">NewestFirst</span></span><br/><br/><span data-ttu-id="a9df0-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="a9df0-263">OldestFirst</span></span> |<span data-ttu-id="a9df0-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="a9df0-264">OldestFirst</span></span> |<span data-ttu-id="a9df0-265">Determina Hola orden de los segmentos de datos que se están procesando.</span><span class="sxs-lookup"><span data-stu-id="a9df0-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="a9df0-266">Por ejemplo, si tiene 2 segmentos (que tienen lugar uno a las 4 p.m. y el otro a las 5 p.m.) y ambos están pendientes de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a9df0-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="a9df0-267">Si establece hello executionPriorityOrder toobe NewestFirst, segmento de Hola a las 5 P.M. se procesa en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="a9df0-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="a9df0-268">De forma similar si establece hello executionPriorityORder toobe OldestFIrst, segmento de Hola a las 4 P.M. se procesa.</span><span class="sxs-lookup"><span data-stu-id="a9df0-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="a9df0-269">retry</span><span class="sxs-lookup"><span data-stu-id="a9df0-269">retry</span></span> |<span data-ttu-id="a9df0-270">Entero </span><span class="sxs-lookup"><span data-stu-id="a9df0-270">Integer</span></span><br/><br/><span data-ttu-id="a9df0-271">El valor máximo permitido es 10</span><span class="sxs-lookup"><span data-stu-id="a9df0-271">Max value can be 10</span></span> |<span data-ttu-id="a9df0-272">0</span><span class="sxs-lookup"><span data-stu-id="a9df0-272">0</span></span> |<span data-ttu-id="a9df0-273">Número de reintentos antes del procesamiento de datos de hello para el segmento de Hola se marca como completada con errores.</span><span class="sxs-lookup"><span data-stu-id="a9df0-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="a9df0-274">Ejecución de actividad para un segmento de datos se vuelve a intentar la toohello especificada número de reintentos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="a9df0-275">Hola reintento se realiza tan pronto como sea posible después de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="a9df0-276">timeout</span><span class="sxs-lookup"><span data-stu-id="a9df0-276">timeout</span></span> |<span data-ttu-id="a9df0-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a9df0-277">TimeSpan</span></span> |<span data-ttu-id="a9df0-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="a9df0-278">00:00:00</span></span> |<span data-ttu-id="a9df0-279">Tiempo de espera para la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-279">Timeout for hello activity.</span></span> <span data-ttu-id="a9df0-280">Ejemplo: 00:10:00 (implica un tiempo de espera de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="a9df0-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="a9df0-281">Si un valor no se especifica o es 0, el tiempo de espera de hello es infinito.</span><span class="sxs-lookup"><span data-stu-id="a9df0-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="a9df0-282">Si el tiempo de procesamiento de datos de hello en un sector supera el valor de tiempo de espera de hello, que se cancele y sistema de hello trata el procesamiento de hello tooretry.</span><span class="sxs-lookup"><span data-stu-id="a9df0-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="a9df0-283">número de Hola de reintentos depende de la propiedad de reintento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="a9df0-284">Cuando se produce el tiempo de espera, el estado de Hola se establece tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="a9df0-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="a9df0-285">delay</span><span class="sxs-lookup"><span data-stu-id="a9df0-285">delay</span></span> |<span data-ttu-id="a9df0-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a9df0-286">TimeSpan</span></span> |<span data-ttu-id="a9df0-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="a9df0-287">00:00:00</span></span> |<span data-ttu-id="a9df0-288">Especificar el retraso de hello antes del procesamiento de datos de segmento Hola se inicia.</span><span class="sxs-lookup"><span data-stu-id="a9df0-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="a9df0-289">se inicia la ejecución de Hola de actividad para un segmento de datos una vez Hola retraso pasado Hola espera el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a9df0-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="a9df0-290">Ejemplo: 00:10:00 (implica un retraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="a9df0-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="a9df0-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="a9df0-291">longRetry</span></span> |<span data-ttu-id="a9df0-292">Entero </span><span class="sxs-lookup"><span data-stu-id="a9df0-292">Integer</span></span><br/><br/><span data-ttu-id="a9df0-293">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="a9df0-293">Max value: 10</span></span> |<span data-ttu-id="a9df0-294">1</span><span class="sxs-lookup"><span data-stu-id="a9df0-294">1</span></span> |<span data-ttu-id="a9df0-295">número de Hola de reintentos largos intentos antes de que se error al ejecutar el segmento Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="a9df0-296">Los intentos de longRetry se espacian de acuerdo a longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="a9df0-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="a9df0-297">Por lo que si necesita toospecify un tiempo entre los reintentos, utilice longRetry.</span><span class="sxs-lookup"><span data-stu-id="a9df0-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="a9df0-298">Si se especifican Retry y longRetry, cada intento de longRetry incluye los intentos de reintento y número máximo de Hola de intentos es reintento * longRetry.</span><span class="sxs-lookup"><span data-stu-id="a9df0-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="a9df0-299">Por ejemplo, si tenemos Hola después de la configuración de directiva de actividad de hello:</span><span class="sxs-lookup"><span data-stu-id="a9df0-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="a9df0-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="a9df0-300">Retry: 3</span></span><br/><span data-ttu-id="a9df0-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="a9df0-301">longRetry: 2</span></span><br/><span data-ttu-id="a9df0-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="a9df0-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="a9df0-303">Suponemos que hay solo un tooexecute de segmento (estado de espera) y ejecución de la actividad de Hola se produce un error cada vez.</span><span class="sxs-lookup"><span data-stu-id="a9df0-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="a9df0-304">Inicialmente habría tres intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a9df0-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="a9df0-305">Después de cada intento, estado del sector Hola sería Retry.</span><span class="sxs-lookup"><span data-stu-id="a9df0-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="a9df0-306">Después de 3 primeros intentos superan el tiempo de espera, estado del sector Hola sería LongRetry.</span><span class="sxs-lookup"><span data-stu-id="a9df0-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="a9df0-307">Después de una hora (es decir, el valor de longRetryInteval), se produciría otro conjunto de 3 intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a9df0-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="a9df0-308">Después de eso, el estado del sector de hello podría ser Failed y no podría realizarse ningún reintento más.</span><span class="sxs-lookup"><span data-stu-id="a9df0-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="a9df0-309">Por tanto, en total se realizaron 6 intentos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="a9df0-310">Si cualquier ejecución se realiza correctamente, el estado del sector de hello sería Ready y no se realiza ningún reintento más.</span><span class="sxs-lookup"><span data-stu-id="a9df0-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="a9df0-311">longRetry puede utilizarse en situaciones donde llegan datos dependientes en momentos no determinista o hello entorno general es inestable en el procesamiento de datos que se produce.</span><span class="sxs-lookup"><span data-stu-id="a9df0-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="a9df0-312">En tales casos, no es útil realizar reintentos uno tras otro y hacerlo después de un intervalo de tiempo provoca Hola deseado de salida.</span><span class="sxs-lookup"><span data-stu-id="a9df0-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="a9df0-313">Advertencia: No establezca valores altos para longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="a9df0-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="a9df0-314">Normalmente, los valores más altos implican otros problemas sistémicos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="a9df0-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="a9df0-315">longRetryInterval</span></span> |<span data-ttu-id="a9df0-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a9df0-316">TimeSpan</span></span> |<span data-ttu-id="a9df0-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="a9df0-317">00:00:00</span></span> |<span data-ttu-id="a9df0-318">retraso de Hello entre reintentos largos</span><span class="sxs-lookup"><span data-stu-id="a9df0-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="a9df0-319">Para más información, vea el artículo [Canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a9df0-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="a9df0-320">Procesamiento en paralelo de segmentos de datos</span><span class="sxs-lookup"><span data-stu-id="a9df0-320">Parallel processing of data slices</span></span>
<span data-ttu-id="a9df0-321">Puede establecer fecha de inicio de hello para la canalización de Hola Hola anteriores.</span><span class="sxs-lookup"><span data-stu-id="a9df0-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="a9df0-322">Al hacerlo, factoría de datos automáticamente calcula (rellenos atrás) todos los segmentos de datos en los último hello y empieza a procesarlos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="a9df0-323">Por ejemplo: si se crea una canalización con fecha de inicio de 2017-04-01 y Hola fecha actual es de 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="a9df0-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="a9df0-324">Si cadencia de Hola de hello salida de conjunto de datos es diariamente, a continuación, inicia el generador de datos procesar todos los sectores de Hola de 2017-04-01 too2017-04-09 inmediatamente porque Hola fecha de inicio se encuentra Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="a9df0-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="a9df0-325">Hola segmento de 2017-04-10 no se procesó todavía porque Hola valor de propiedad de estilo en la sección de disponibilidad de hello EndOfInterval de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a9df0-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="a9df0-326">Hello más antigua se procesa en primer lugar como valor predeterminado de hello valo executionPriorityOrder es OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="a9df0-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="a9df0-327">Para obtener una descripción de la propiedad de estilo de hello, consulte [disponibilidad del conjunto de datos](#dataset-availability) sección.</span><span class="sxs-lookup"><span data-stu-id="a9df0-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="a9df0-328">Para obtener una descripción de la sección de executionPriorityOrder hello, vea hello [las directivas de actividad](#activity-policies) sección.</span><span class="sxs-lookup"><span data-stu-id="a9df0-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="a9df0-329">Puede configurar toobe de sectores de datos se llene de back procesada en paralelo por establecer Hola **simultaneidad** propiedad Hola **directiva** sección de JSON de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="a9df0-330">Esta propiedad determina el número de Hola de ejecuciones paralelas que pueden ocurrir en distintos sectores.</span><span class="sxs-lookup"><span data-stu-id="a9df0-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="a9df0-331">valor predeterminado de Hello para la propiedad de simultaneidad de hello es 1.</span><span class="sxs-lookup"><span data-stu-id="a9df0-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="a9df0-332">Por tanto, se procesa un segmento a la vez de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a9df0-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="a9df0-333">valor máximo de Hello es 10.</span><span class="sxs-lookup"><span data-stu-id="a9df0-333">hello maximum value is 10.</span></span> <span data-ttu-id="a9df0-334">Cuando una canalización debe toogo a través de un conjunto grande de datos disponibles, que tienen un valor mayor de simultaneidad acelera el procesamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="a9df0-335">Volver a ejecutar un segmento de datos con errores</span><span class="sxs-lookup"><span data-stu-id="a9df0-335">Rerun a failed data slice</span></span>
<span data-ttu-id="a9df0-336">Cuando se produce un error durante el procesamiento de un segmento de datos, puede averiguar por qué no se pudo procesamiento Hola de un segmento mediante hojas de portal de Azure o supervisar y administrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a9df0-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="a9df0-337">Consulte [Supervisión y administración de canalizaciones mediante hojas de Azure Portal](data-factory-monitor-manage-pipelines.md) o [Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="a9df0-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="a9df0-338">Considere la posibilidad de hello siguiente ejemplo, que se muestra en dos actividades.</span><span class="sxs-lookup"><span data-stu-id="a9df0-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="a9df0-339">Activity1 y Activity2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="a9df0-340">Activity1 consume un segmento de Dataset1 y genera un segmento del conjunto de datos 2, que consume como entrada Activity2 tooproduce un segmento de hello Final del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Segmento con errores](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="a9df0-342">Hola diagrama muestra fuera de tres segmentos recientes, que se produjo un segmento de error productor Hola 9 y 10 AM para Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="a9df0-343">Factoría de datos realiza automáticamente un seguimiento de dependencia para el conjunto de datos de series de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="a9df0-344">Como resultado, no se inicia de sector de hello 9 y 10 AM siguen en la cadena de ejecución de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="a9df0-345">Herramientas de administración y supervisión del generador de datos permiten toodrill en registros de diagnóstico de Hola para hello segmento erróneo tooeasily buscar Hola raíz causa de problema de Hola y de corregirlo.</span><span class="sxs-lookup"><span data-stu-id="a9df0-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="a9df0-346">Una vez solucionado el problema de hello, puede iniciar fácilmente actividad hello ejecutar tooproduce Hola error segmento.</span><span class="sxs-lookup"><span data-stu-id="a9df0-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="a9df0-347">Para obtener más información acerca de cómo toorerun y comprender las transiciones de estado para segmentos de datos, vea [supervisión y administración de canalizaciones mediante módulos de portal de Azure](data-factory-monitor-manage-pipelines.md) o [aplicación de supervisión y administración](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9df0-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="a9df0-348">Después de volver a ejecutar Hola 9 y 10 AM segmentar de **Dataset2**, factoría de datos inicia Hola ejecute para el segmento de hello 9 y 10 AM dependientes en hello conjunto de datos final.</span><span class="sxs-lookup"><span data-stu-id="a9df0-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Repetición de ejecución de un segmento con errores](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="a9df0-350">Varias actividades en una canalización</span><span class="sxs-lookup"><span data-stu-id="a9df0-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="a9df0-351">pero se pueden tener más de una actividad en una canalización.</span><span class="sxs-lookup"><span data-stu-id="a9df0-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="a9df0-352">Si tiene varias actividades en una canalización y salida de hello de una actividad no es una entrada de otra actividad, las actividades de hello pueden ejecutar en paralelo si los segmentos de datos de entrada para las actividades de hello están listos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="a9df0-353">Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="a9df0-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="a9df0-354">Hola actividades pueden ser Hola misma canalización o en las canalizaciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="a9df0-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="a9df0-355">segunda actividad de Hola se ejecuta sólo cuando hello primero uno finaliza correctamente.</span><span class="sxs-lookup"><span data-stu-id="a9df0-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="a9df0-356">Por ejemplo, considere la posibilidad de hello siguiente caso donde una canalización tiene dos actividades:</span><span class="sxs-lookup"><span data-stu-id="a9df0-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="a9df0-357">La actividad A1 que requiere el conjunto de datos de entrada externo D1 y genera el conjunto de datos de salida D2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="a9df0-358">La actividad A2 que requiere una entrada del conjunto de datos D2 y genera el conjunto de datos de salida D3.</span><span class="sxs-lookup"><span data-stu-id="a9df0-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="a9df0-359">En este escenario, las actividades de A1 y A2 se Hola misma canalización.</span><span class="sxs-lookup"><span data-stu-id="a9df0-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="a9df0-360">actividad de Hello que a1 se ejecuta cuando los datos externos de hello están disponibles y se alcanza la frecuencia de disponibilidad de hello programado.</span><span class="sxs-lookup"><span data-stu-id="a9df0-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="a9df0-361">Hello actividad A2 se ejecuta cuando hello intervalos programados desde D2 estén disponibles y hello frecuencia disponibilidad programada se alcanza.</span><span class="sxs-lookup"><span data-stu-id="a9df0-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="a9df0-362">Si se produce un error en uno de los sectores de hello en el conjunto de datos D2, A2 no se ejecuta para dicho sector hasta que esté disponible.</span><span class="sxs-lookup"><span data-stu-id="a9df0-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="a9df0-363">Hola vista de diagrama con ambas actividades Hola misma canalización sería Hola siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="a9df0-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![El encadenamiento de actividades en hello misma canalización](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="a9df0-365">Tal y como se mencionó anteriormente, las actividades de hello pueden estar en diferentes canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="a9df0-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="a9df0-366">En este escenario, vista de diagrama de hello sería Hola siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="a9df0-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![Encadenamiento de las actividades de dos canalizaciones](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="a9df0-368">Vea hello [copiar secuencialmente](#copy-sequentially) sección en el apéndice de hello para obtener un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9df0-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="a9df0-369">Modelado de conjuntos de datos con distintas frecuencias</span><span class="sxs-lookup"><span data-stu-id="a9df0-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="a9df0-370">En los ejemplos de hello, las frecuencias de Hola de entrada y salida hello y conjuntos de datos de actividad ventana de programación se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="a9df0-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="a9df0-371">Algunos escenarios requieren la salida de hello capacidad tooproduce a una frecuencia diferente a las frecuencias de Hola de una o más entradas.</span><span class="sxs-lookup"><span data-stu-id="a9df0-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="a9df0-372">Data Factory admite el modelado de estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="a9df0-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="a9df0-373">Ejemplo 1: Generación de un informe de salida diario para los datos de entrada que esté disponibles cada hora</span><span class="sxs-lookup"><span data-stu-id="a9df0-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="a9df0-374">Considere un escenario en el que tiene datos de medida de entrada de sensores disponibles cada hora en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a9df0-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="a9df0-375">Desea tooproduce un informe diario agregado con estadísticas como Media, máximo y mínimo por día Hola con [actividad de hive de factoría de datos](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="a9df0-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="a9df0-376">A continuación, se muestra cómo puede modelar este escenario con Data Factory:</span><span class="sxs-lookup"><span data-stu-id="a9df0-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="a9df0-377">**Conjunto de datos de entrada**</span><span class="sxs-lookup"><span data-stu-id="a9df0-377">**Input dataset**</span></span>

<span data-ttu-id="a9df0-378">Hola cada hora de entrada de archivos se colocan en la carpeta Hola Hola dado día.</span><span class="sxs-lookup"><span data-stu-id="a9df0-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="a9df0-379">La disponibilidad para la entrada se establece en **Hour** (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="a9df0-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="a9df0-380">**Conjunto de datos de salida**</span><span class="sxs-lookup"><span data-stu-id="a9df0-380">**Output dataset**</span></span>

<span data-ttu-id="a9df0-381">Se crea cada día en un archivo de salida en la carpeta del día de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="a9df0-382">La disponibilidad de la salida se establece en **Day** (frecuencia: día e intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="a9df0-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a9df0-383">**Actividad: actividad de Hive en una canalización**</span><span class="sxs-lookup"><span data-stu-id="a9df0-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="a9df0-384">script de hive Hola recibe Hola adecuado *DateTime* información como parámetros que utilizan hello **WindowStart** variable tal y como se muestra en el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="a9df0-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="a9df0-385">script de hive Hola emplea estos datos de hello tooload variable desde la carpeta correcta de Hola durante el día de Hola y la salida de hello agregación toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="a9df0-386">Hello siguiente diagrama muestra el escenario de Hola desde un punto de vista de dependencia de los datos.</span><span class="sxs-lookup"><span data-stu-id="a9df0-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Dependencia de los datos](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="a9df0-388">segmento de la salida de Hello para cada día depende de 24 sectores por hora de un conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9df0-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="a9df0-389">Calcula de la factoría de datos estas dependencias automáticamente averiguando Hola segmentos de datos de entrada que se encuentran en hello mismo período de tiempo como Hola toobe de segmento de salida generado.</span><span class="sxs-lookup"><span data-stu-id="a9df0-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="a9df0-390">Si cualquiera de los segmentos de entrada de hello 24 no está disponible, factoría de datos espera Hola segmento entrada toobe listo antes de iniciar la ejecución de actividad diaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="a9df0-391">Ejemplo 2: Especificación de la dependencia con expresiones y funciones de Data Factory</span><span class="sxs-lookup"><span data-stu-id="a9df0-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="a9df0-392">Consideremos otro escenario.</span><span class="sxs-lookup"><span data-stu-id="a9df0-392">Let’s consider another scenario.</span></span> <span data-ttu-id="a9df0-393">Suponga que tiene una actividad de Hive que procesa dos conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9df0-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="a9df0-394">Uno de ellos tiene nuevos datos diariamente, pero otro obtiene datos nuevos cada semana.</span><span class="sxs-lookup"><span data-stu-id="a9df0-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="a9df0-395">Suponga que desea toodo una combinación entre dos entradas de Hola y generar una salida de cada día.</span><span class="sxs-lookup"><span data-stu-id="a9df0-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="a9df0-396">método sencillo de Hello en el que factoría de datos automáticamente determina la entrada derecha Hola segmentos tooprocess alineando salida toohello tiempo del segmento de datos no funciona período.</span><span class="sxs-lookup"><span data-stu-id="a9df0-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="a9df0-397">Debe especificar que para cada ejecución de actividad, Hola factoría de datos debe utilizar el segmento de datos de la semana pasada para hello conjunto de datos de entrada semanal.</span><span class="sxs-lookup"><span data-stu-id="a9df0-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="a9df0-398">Usar funciones de factoría de datos de Azure como se muestra en hello siguiente fragmento de código tooimplement este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="a9df0-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="a9df0-399">**Input1: blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="a9df0-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="a9df0-400">Hola primera entrada de hello blobs de Azure se actualiza diariamente.</span><span class="sxs-lookup"><span data-stu-id="a9df0-400">hello first input is hello Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a9df0-401">**Input2: blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="a9df0-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="a9df0-402">Entrada2 es hello Azure blob que se actualiza semanalmente.</span><span class="sxs-lookup"><span data-stu-id="a9df0-402">Input2 is hello Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="a9df0-403">**Salida: blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="a9df0-403">**Output: Azure blob**</span></span>

<span data-ttu-id="a9df0-404">Un archivo de salida se crea cada día en la carpeta de Hola para día Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="a9df0-405">Disponibilidad de salida se establece demasiado**día** (frecuencia: día, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="a9df0-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a9df0-406">**Actividad: actividad de Hive en una canalización**</span><span class="sxs-lookup"><span data-stu-id="a9df0-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="a9df0-407">actividad de hive Hello toma dos entradas de Hola y genera un segmento de salida todos los días.</span><span class="sxs-lookup"><span data-stu-id="a9df0-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="a9df0-408">Puede especificar toodepend de segmento de salida de cada día en Hola segmento de entrada de la semana anterior para la entrada semanal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="a9df0-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="a9df0-409">Para conocer la lista de funciones y variables del sistema que admite Data Factory, consulte el artículo [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="a9df0-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="a9df0-410">Anexo</span><span class="sxs-lookup"><span data-stu-id="a9df0-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="a9df0-411">Ejemplo: copia secuencial</span><span class="sxs-lookup"><span data-stu-id="a9df0-411">Example: copy sequentially</span></span>
<span data-ttu-id="a9df0-412">Es posible toorun varias operaciones de copia uno tras otro de forma secuencial/ordenados.</span><span class="sxs-lookup"><span data-stu-id="a9df0-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="a9df0-413">Por ejemplo, podría tener conjuntos de datos de salida de datos dos actividades de una canalización (CopyActivity1 y CopyActivity2) con hello después de entrada de copia:</span><span class="sxs-lookup"><span data-stu-id="a9df0-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="a9df0-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="a9df0-414">CopyActivity1</span></span>

<span data-ttu-id="a9df0-415">Entrada: Dataset.</span><span class="sxs-lookup"><span data-stu-id="a9df0-415">Input: Dataset.</span></span> <span data-ttu-id="a9df0-416">Salida: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-416">Output: Dataset2.</span></span>

<span data-ttu-id="a9df0-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="a9df0-417">CopyActivity2</span></span>

<span data-ttu-id="a9df0-418">Entrada: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-418">Input: Dataset2.</span></span>  <span data-ttu-id="a9df0-419">Salida: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="a9df0-419">Output: Dataset3.</span></span>

<span data-ttu-id="a9df0-420">CopyActivity2 llevarían a cabo únicamente si se ha ejecutado correctamente hello CopyActivity1 y Dataset2 está disponible.</span><span class="sxs-lookup"><span data-stu-id="a9df0-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="a9df0-421">Aquí es JSON de la canalización de ejemplo Hola:</span><span class="sxs-lookup"><span data-stu-id="a9df0-421">Here is hello sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="a9df0-422">Observe que en el ejemplo de Hola, conjunto de datos de salida de hello de hello primera actividad de copia (Dataset2) se especifica como entrada para la segunda actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="a9df0-423">Por lo tanto, Hola segunda actividad se ejecuta sólo cuando el conjunto de datos de salida de hello desde la primera actividad de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="a9df0-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="a9df0-424">En el ejemplo de Hola, CopyActivity2 puede tener una entrada diferente, como Dataset3, pero se especifica Dataset2 como una entrada tooCopyActivity2, por lo que la actividad hello no se ejecuta hasta que finalice la CopyActivity1.</span><span class="sxs-lookup"><span data-stu-id="a9df0-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="a9df0-425">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a9df0-425">For example:</span></span>

<span data-ttu-id="a9df0-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="a9df0-426">CopyActivity1</span></span>

<span data-ttu-id="a9df0-427">Entrada: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="a9df0-427">Input: Dataset1.</span></span> <span data-ttu-id="a9df0-428">Salida: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-428">Output: Dataset2.</span></span>

<span data-ttu-id="a9df0-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="a9df0-429">CopyActivity2</span></span>

<span data-ttu-id="a9df0-430">Entradas: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="a9df0-431">Salida: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="a9df0-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="a9df0-432">Tenga en cuenta que en el ejemplo de Hola, se especifican dos conjuntos de datos de entrada para la segunda actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9df0-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="a9df0-433">Cuando se especifican varias entradas, solo Hola primera entrada conjunto de datos se utiliza para copiar datos, pero otros conjuntos de datos se utilizan como dependencias.</span><span class="sxs-lookup"><span data-stu-id="a9df0-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="a9df0-434">CopyActivity2 iniciaría solo después de hello condiciones siguientes se cumplen:</span><span class="sxs-lookup"><span data-stu-id="a9df0-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="a9df0-435">ActividadCopia1 se ha completado correctamente y ConjuntoDatos2 está disponible.</span><span class="sxs-lookup"><span data-stu-id="a9df0-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="a9df0-436">Este conjunto de datos no se utiliza cuando se copian datos tooDataset4.</span><span class="sxs-lookup"><span data-stu-id="a9df0-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="a9df0-437">Solo actúa como una dependencia de programación de ActividadCopia2.</span><span class="sxs-lookup"><span data-stu-id="a9df0-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="a9df0-438">ConjuntoDatos3 está disponible.</span><span class="sxs-lookup"><span data-stu-id="a9df0-438">Dataset3 is available.</span></span> <span data-ttu-id="a9df0-439">Este conjunto de datos representa los datos de Hola que constituye el destino de toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="a9df0-439">This dataset represents hello data that is copied toohello destination.</span></span> 
