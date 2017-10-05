---
title: "Programación y ejecución con Data Factory | Microsoft Docs"
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
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="78a62-103">Programación y ejecución de Data Factory</span><span class="sxs-lookup"><span data-stu-id="78a62-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="78a62-104">En este artículo se explican los aspectos de programación y ejecución del modelo de aplicación de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="78a62-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="78a62-105">En este artículo se presupone que comprende los conceptos básicos del modelo de aplicación de Data Factory, como la actividad, las canalizaciones, los servicios vinculados y los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="78a62-106">Para los conceptos básicos de Azure Data Factory, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78a62-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="78a62-107">Introducción al servicio Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="78a62-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="78a62-108">Procesos</span><span class="sxs-lookup"><span data-stu-id="78a62-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="78a62-109">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="78a62-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="78a62-110">Horas de inicio y finalización de la canalización</span><span class="sxs-lookup"><span data-stu-id="78a62-110">Start and end times of pipeline</span></span>
<span data-ttu-id="78a62-111">Una canalización solo está activa entre su hora de **inicio** y de **finalización**.</span><span class="sxs-lookup"><span data-stu-id="78a62-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="78a62-112">No se ejecuta antes de la hora de inicio ni después de la hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="78a62-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="78a62-113">Si la canalización está en pausa, no se ejecuta, independientemente de su hora de inicio y de finalización.</span><span class="sxs-lookup"><span data-stu-id="78a62-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="78a62-114">Para que se ejecute una canalización, no debe estar en pausa.</span><span class="sxs-lookup"><span data-stu-id="78a62-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="78a62-115">Puede encontrar esta configuración (inicio, finalización y pausa) en la definición de la canalización:</span><span class="sxs-lookup"><span data-stu-id="78a62-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="78a62-116">Para más información sobre estas propiedades, vea el artículo sobre la [creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="78a62-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="78a62-117">Definición de la programación de una actividad</span><span class="sxs-lookup"><span data-stu-id="78a62-117">Specify schedule for an activity</span></span>
<span data-ttu-id="78a62-118">La canalización en sí no se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="78a62-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="78a62-119">Son las actividades que incluye las que se ejecutan en el contexto general de la canalización.</span><span class="sxs-lookup"><span data-stu-id="78a62-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="78a62-120">Puede especificar una programación recurrente para una actividad; para ello, use la sección **scheduler** de la actividad JSON.</span><span class="sxs-lookup"><span data-stu-id="78a62-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="78a62-121">Por ejemplo, puede programar una actividad para que se ejecute cada hora de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="78a62-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="78a62-122">Como se muestra en el diagrama siguiente, al especificar una programación de una actividad se crea una ventana de saltos de tamaño constante con las horas de inicio y finalización de la canalización.</span><span class="sxs-lookup"><span data-stu-id="78a62-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="78a62-123">Las ventanas de saltos de tamaño constante son series de intervalos de tiempo de tamaño fijo, no superpuestos y contiguos.</span><span class="sxs-lookup"><span data-stu-id="78a62-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="78a62-124">Estas ventanas de saltos lógicas de tamaño constante para la actividad se denominan **ventanas de actividad**.</span><span class="sxs-lookup"><span data-stu-id="78a62-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Ejemplo de programador de actividades](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="78a62-126">La propiedad **scheduler** de una actividad es opcional.</span><span class="sxs-lookup"><span data-stu-id="78a62-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="78a62-127">Si especifica esta propiedad, debe coincidir con la cadencia que indique en la definición del conjunto de datos de salida de la actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="78a62-128">Actualmente, el conjunto de datos de salida es lo que impulsa la programación.</span><span class="sxs-lookup"><span data-stu-id="78a62-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="78a62-129">Por tanto, debe crear un conjunto de datos de salida incluso si la actividad no produce ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="78a62-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="78a62-130">Definición de la programación de un conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="78a62-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="78a62-131">Una actividad de una canalización de Data Factory puede tomar diversos **conjuntos de datos** de entrada, o ninguno, y generar uno o varios conjuntos de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="78a62-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="78a62-132">Para una actividad, puede especificar la cadencia con que se encuentran disponibles los datos de entrada o con que se producen los datos de salida en la sección **availability** de las definiciones de los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="78a62-133">La propiedad **frecuency** de la sección **availability** especifica la unidad de tiempo.</span><span class="sxs-lookup"><span data-stu-id="78a62-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="78a62-134">Los valores permitidos para frequency son: Minute, Hour, Day, Week y Month.</span><span class="sxs-lookup"><span data-stu-id="78a62-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="78a62-135">La propiedad **interval** de la sección availability especifica un multiplicador para la frecuencia.</span><span class="sxs-lookup"><span data-stu-id="78a62-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="78a62-136">Por ejemplo, si la propiedad frecuency se establece en Day y la propiedad interval, en 1 para un conjunto de datos de salida, los datos de salida se generan diariamente.</span><span class="sxs-lookup"><span data-stu-id="78a62-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="78a62-137">Si especifica frequency como Minute, se recomienda establecer interval en no menos de 15.</span><span class="sxs-lookup"><span data-stu-id="78a62-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="78a62-138">En el ejemplo siguiente, los datos de entrada están disponibles cada hora y los datos de salida se generan cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="78a62-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="78a62-139">**Conjunto de datos de entrada:**</span><span class="sxs-lookup"><span data-stu-id="78a62-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="78a62-140">**Conjunto de datos de salida**</span><span class="sxs-lookup"><span data-stu-id="78a62-140">**Output dataset**</span></span>

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

<span data-ttu-id="78a62-141">Actualmente, **el conjunto de datos de salida impulsa la programación**.</span><span class="sxs-lookup"><span data-stu-id="78a62-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="78a62-142">En otras palabras, la programación especificada para el conjunto de datos de salida se usa para ejecutar una actividad en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="78a62-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="78a62-143">Por tanto, debe crear un conjunto de datos de salida incluso si la actividad no produce ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="78a62-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="78a62-144">Si la actividad no toma ninguna entrada, puede omitir la creación del conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="78a62-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="78a62-145">En la siguiente definición de la canalización, la propiedad **scheduler** se utiliza para especificar la programación de la actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="78a62-146">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="78a62-146">This property is optional.</span></span> <span data-ttu-id="78a62-147">Actualmente, la programación de la actividad debe coincidir con la programación especificada para el conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="78a62-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
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

<span data-ttu-id="78a62-148">En este ejemplo, la actividad se ejecuta cada hora entre las horas de inicio y finalización de la canalización.</span><span class="sxs-lookup"><span data-stu-id="78a62-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="78a62-149">Los datos de salida se generan cada hora durante ventanas de tres horas (8:00 a 9:00, 9:00 a 10:00 y 10:00 a 11:00).</span><span class="sxs-lookup"><span data-stu-id="78a62-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="78a62-150">Cada unidad de datos consumida o producida por la ejecución de una actividad se denomina **segmento de datos**.</span><span class="sxs-lookup"><span data-stu-id="78a62-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="78a62-151">El diagrama siguiente muestra un ejemplo de una actividad con un conjunto de datos de entrada y uno de salida:</span><span class="sxs-lookup"><span data-stu-id="78a62-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Programador de disponibilidad](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="78a62-153">En el diagrama se muestran los segmentos de datos por hora para el conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="78a62-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="78a62-154">El diagrama muestra tres segmentos de entrada que están listos para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="78a62-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="78a62-155">La actividad 10-11 AM está en curso, produciendo el segmento de salida 10-11 AM.</span><span class="sxs-lookup"><span data-stu-id="78a62-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="78a62-156">Puede acceder al intervalo de tiempo asociado al segmento actual en el JSON del conjunto de datos con las variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) y [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="78a62-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="78a62-157">De forma similar, puede acceder al intervalo de tiempo asociado con una ventana de actividad con las variables WindowStart y WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="78a62-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="78a62-158">La programación de una actividad debe coincidir con la programación del conjunto de datos de salida de la actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="78a62-159">Por lo tanto, los valores de SliceStart y SliceEnd son los mismos que los valores de WindowStart y WindowEnd, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="78a62-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="78a62-160">Para más información sobre estas variables, vea el artículo [Funciones y variables del sistema](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="78a62-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="78a62-161">Puede usar estas variables para distintos fines en el JSON de actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="78a62-162">Por ejemplo, puede usarlas para seleccionar datos de conjuntos de datos de entrada y salida que representen datos de serie temporal (por ejemplo, de 8:00 a 9:00).</span><span class="sxs-lookup"><span data-stu-id="78a62-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="78a62-163">En el ejemplo también se usan **WindowStart** y **WindowEnd** para seleccionar datos pertinentes para la ejecución de una actividad y copiarlos en un blob con el valor de **folderPath** adecuado.</span><span class="sxs-lookup"><span data-stu-id="78a62-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="78a62-164">**folderPath** se parametriza para tener una carpeta independiente para cada hora.</span><span class="sxs-lookup"><span data-stu-id="78a62-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="78a62-165">En el ejemplo anterior, la programación especificada para los conjuntos de entrada y salida es la misma (hora).</span><span class="sxs-lookup"><span data-stu-id="78a62-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="78a62-166">Si el conjunto de datos de entrada para la actividad está disponible en una frecuencia distinta, digamos cada 15 minutos, la actividad que genera este conjunto de datos de salida sigue ejecutándose una vez cada hora, ya que el conjunto de datos de salida es el que impulsa la programación de la actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="78a62-167">Para más información, vea [Modelado de conjuntos de datos con distintas frecuencias](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="78a62-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="78a62-168">Directivas y disponibilidad del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="78a62-168">Dataset availability and policies</span></span>
<span data-ttu-id="78a62-169">Se ha analizado el uso de las propiedades frequency e interval en la sección availability de la definición del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="78a62-170">Hay otras propiedades que afectan a la programación y ejecución de una actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="78a62-171">Disponibilidad del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="78a62-171">Dataset availability</span></span> 
<span data-ttu-id="78a62-172">La tabla siguiente describe las propiedades que puede utilizar en la sección de **disponibilidad**:</span><span class="sxs-lookup"><span data-stu-id="78a62-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="78a62-173">Propiedad</span><span class="sxs-lookup"><span data-stu-id="78a62-173">Property</span></span> | <span data-ttu-id="78a62-174">Descripción</span><span class="sxs-lookup"><span data-stu-id="78a62-174">Description</span></span> | <span data-ttu-id="78a62-175">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="78a62-175">Required</span></span> | <span data-ttu-id="78a62-176">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="78a62-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="78a62-177">frequency</span><span class="sxs-lookup"><span data-stu-id="78a62-177">frequency</span></span> |<span data-ttu-id="78a62-178">Especifica la unidad de tiempo para la producción de segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="78a62-179"><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="78a62-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="78a62-180">Sí</span><span class="sxs-lookup"><span data-stu-id="78a62-180">Yes</span></span> |<span data-ttu-id="78a62-181">N/D</span><span class="sxs-lookup"><span data-stu-id="78a62-181">NA</span></span> |
| <span data-ttu-id="78a62-182">interval</span><span class="sxs-lookup"><span data-stu-id="78a62-182">interval</span></span> |<span data-ttu-id="78a62-183">Especifica un multiplicador para frecuencia</span><span class="sxs-lookup"><span data-stu-id="78a62-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="78a62-184">”Frequency x interval” determina la frecuencia con la que se produce el segmento.</span><span class="sxs-lookup"><span data-stu-id="78a62-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="78a62-185">Si necesita segmentar el conjunto de datos cada hora, establezca <b>frequency</b> en <b>hour</b> e <b>interval</b> en <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="78a62-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="78a62-186"><b>Nota:</b> Si especifica Frequency como Minute, se recomienda establecer interval en no menos de 15.</span><span class="sxs-lookup"><span data-stu-id="78a62-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="78a62-187">Sí</span><span class="sxs-lookup"><span data-stu-id="78a62-187">Yes</span></span> |<span data-ttu-id="78a62-188">N/D</span><span class="sxs-lookup"><span data-stu-id="78a62-188">NA</span></span> |
| <span data-ttu-id="78a62-189">style</span><span class="sxs-lookup"><span data-stu-id="78a62-189">style</span></span> |<span data-ttu-id="78a62-190">Especifica si el segmento debe producirse al principio o al final del intervalo.</span><span class="sxs-lookup"><span data-stu-id="78a62-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="78a62-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="78a62-191">StartOfInterval</span></span></li><li><span data-ttu-id="78a62-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="78a62-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="78a62-193">Si frequency se establece en Month y style se establece en EndOfInterval, el segmento se produce el último día del mes.</span><span class="sxs-lookup"><span data-stu-id="78a62-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="78a62-194">Si style se establece en StartOfInterval, el segmento se produce el primer día del mes.</span><span class="sxs-lookup"><span data-stu-id="78a62-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="78a62-195">Si frequency se establece en Day y style se establece en EndOfInterval, el segmento se produce la última hora del día.</span><span class="sxs-lookup"><span data-stu-id="78a62-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="78a62-196">Si frequency se establece en Hour y style se establece en EndOfInterval, el segmento se produce al final de la hora.</span><span class="sxs-lookup"><span data-stu-id="78a62-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="78a62-197">Por ejemplo, para un segmento para el período de 1 p.m. – 2 p.m., el segmento se producirá a las 2 p.m.</span><span class="sxs-lookup"><span data-stu-id="78a62-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="78a62-198">No</span><span class="sxs-lookup"><span data-stu-id="78a62-198">No</span></span> |<span data-ttu-id="78a62-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="78a62-199">EndOfInterval</span></span> |
| <span data-ttu-id="78a62-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="78a62-200">anchorDateTime</span></span> |<span data-ttu-id="78a62-201">Define la posición absoluta en el tiempo usada por el programador para calcular los límites del segmento de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="78a62-202"><b>Nota:</b> Si AnchorDateTime tiene partes de fecha más pormenorizadas que la frecuencia, estas se omitirán.</span><span class="sxs-lookup"><span data-stu-id="78a62-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="78a62-203">Por ejemplo, si el valor de <b>interval</b> es <b>hourly</b> (frequency: hour e interval: 1) y <b>AnchorDateTime</b> contiene <b>minutes and seconds</b>, las partes <b>minutes and seconds</b> de AnchorDateTime no se tienen en cuenta.</span><span class="sxs-lookup"><span data-stu-id="78a62-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="78a62-204">No</span><span class="sxs-lookup"><span data-stu-id="78a62-204">No</span></span> |<span data-ttu-id="78a62-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="78a62-205">01/01/0001</span></span> |
| <span data-ttu-id="78a62-206">Offset</span><span class="sxs-lookup"><span data-stu-id="78a62-206">offset</span></span> |<span data-ttu-id="78a62-207">Intervalo de tiempo en función del cual se desplazan el inicio y el final de todos los segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="78a62-208"><b>Nota:</b> Si se especifican anchorDateTime y offset, el resultado es el desplazamiento combinado.</span><span class="sxs-lookup"><span data-stu-id="78a62-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="78a62-209">No</span><span class="sxs-lookup"><span data-stu-id="78a62-209">No</span></span> |<span data-ttu-id="78a62-210">N/D</span><span class="sxs-lookup"><span data-stu-id="78a62-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="78a62-211">Ejemplo de offset</span><span class="sxs-lookup"><span data-stu-id="78a62-211">offset example</span></span>
<span data-ttu-id="78a62-212">De forma predeterminada, cada día (`"frequency": "Day", "interval": 1`) se inician los segmentos a las 24:00 UTC (medianoche).</span><span class="sxs-lookup"><span data-stu-id="78a62-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="78a62-213">Si desea que, en su lugar, la hora de inicio sea a las 6:00 UTC, defina el desplazamiento como se muestra en el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="78a62-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="78a62-214">Ejemplo de anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="78a62-214">anchorDateTime example</span></span>
<span data-ttu-id="78a62-215">En el ejemplo siguiente, el conjunto de datos se produce una vez cada 23 horas.</span><span class="sxs-lookup"><span data-stu-id="78a62-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="78a62-216">El primer segmento se inicia a la hora especificada en anchorDateTime, que se define en `2017-04-19T08:00:00` (hora UTC).</span><span class="sxs-lookup"><span data-stu-id="78a62-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="78a62-217">Ejemplo de desplazamiento y estilo</span><span class="sxs-lookup"><span data-stu-id="78a62-217">offset/style Example</span></span>
<span data-ttu-id="78a62-218">El siguiente conjunto de datos es un conjunto de datos mensual y se produce el tercer día de cada mes a las 8:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="78a62-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="78a62-219">Directiva del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="78a62-219">Dataset policy</span></span>
<span data-ttu-id="78a62-220">Un conjunto de datos puede tener una directiva de validación definida que especifique cómo se pueden validar los datos generados por la ejecución de un segmento antes de que esté listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="78a62-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="78a62-221">En estos casos, cuando el segmento ha terminado de ejecutarse, el estado del mismo cambia a **En espera** con un subestado de **Validación**.</span><span class="sxs-lookup"><span data-stu-id="78a62-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="78a62-222">Una vez validados los segmentos, el estado del segmento cambia a **Listo**.</span><span class="sxs-lookup"><span data-stu-id="78a62-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="78a62-223">Si se ha generado un segmento de datos, pero no ha pasado la validación, no se procesan las ejecuciones de actividad de los segmentos de nivel inferior que dependen de ese segmento.</span><span class="sxs-lookup"><span data-stu-id="78a62-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="78a62-224">[Supervisión y administración de canalizaciones](data-factory-monitor-manage-pipelines.md) se tratan los diversos estados de los segmentos de datos en Data Factory.</span><span class="sxs-lookup"><span data-stu-id="78a62-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="78a62-225">En la sección **policy** de la definición del conjunto de datos se definen los criterios o condiciones que deben cumplir los segmentos del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="78a62-226">La tabla siguiente describe las propiedades que puede utilizar en la sección **policy**:</span><span class="sxs-lookup"><span data-stu-id="78a62-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="78a62-227">Nombre de la directiva</span><span class="sxs-lookup"><span data-stu-id="78a62-227">Policy Name</span></span> | <span data-ttu-id="78a62-228">Descripción</span><span class="sxs-lookup"><span data-stu-id="78a62-228">Description</span></span> | <span data-ttu-id="78a62-229">Aplicado a</span><span class="sxs-lookup"><span data-stu-id="78a62-229">Applied To</span></span> | <span data-ttu-id="78a62-230">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="78a62-230">Required</span></span> | <span data-ttu-id="78a62-231">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="78a62-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="78a62-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="78a62-232">minimumSizeMB</span></span> | <span data-ttu-id="78a62-233">Valida que los datos de un **blob de Azure** cumplen los requisitos de tamaño mínimo (en megabytes).</span><span class="sxs-lookup"><span data-stu-id="78a62-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="78a62-234">blob de Azure</span><span class="sxs-lookup"><span data-stu-id="78a62-234">Azure Blob</span></span> |<span data-ttu-id="78a62-235">No</span><span class="sxs-lookup"><span data-stu-id="78a62-235">No</span></span> |<span data-ttu-id="78a62-236">N/D</span><span class="sxs-lookup"><span data-stu-id="78a62-236">NA</span></span> |
| <span data-ttu-id="78a62-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="78a62-237">minimumRows</span></span> | <span data-ttu-id="78a62-238">Valida que los datos de una **base de datos SQL de Azure** o una **tabla de Azure** contienen el número mínimo de filas.</span><span class="sxs-lookup"><span data-stu-id="78a62-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="78a62-239">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="78a62-239">Azure SQL Database</span></span></li><li><span data-ttu-id="78a62-240">tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="78a62-240">Azure Table</span></span></li></ul> |<span data-ttu-id="78a62-241">No</span><span class="sxs-lookup"><span data-stu-id="78a62-241">No</span></span> |<span data-ttu-id="78a62-242">N/D</span><span class="sxs-lookup"><span data-stu-id="78a62-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="78a62-243">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="78a62-243">Examples</span></span>
<span data-ttu-id="78a62-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="78a62-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="78a62-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="78a62-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="78a62-246">Para consultar ejemplos y más información sobre estas propiedades, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="78a62-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="78a62-247">Directivas de la actividad</span><span class="sxs-lookup"><span data-stu-id="78a62-247">Activity policies</span></span>
<span data-ttu-id="78a62-248">Las directivas afectan al comportamiento en tiempo de ejecución de una actividad, concretamente cuando se procesa el segmento de una tabla.</span><span class="sxs-lookup"><span data-stu-id="78a62-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="78a62-249">En la tabla siguiente se proporciona los detalles.</span><span class="sxs-lookup"><span data-stu-id="78a62-249">The following table provides the details.</span></span>

| <span data-ttu-id="78a62-250">Propiedad</span><span class="sxs-lookup"><span data-stu-id="78a62-250">Property</span></span> | <span data-ttu-id="78a62-251">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="78a62-251">Permitted values</span></span> | <span data-ttu-id="78a62-252">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="78a62-252">Default Value</span></span> | <span data-ttu-id="78a62-253">Description</span><span class="sxs-lookup"><span data-stu-id="78a62-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="78a62-254">simultaneidad</span><span class="sxs-lookup"><span data-stu-id="78a62-254">concurrency</span></span> |<span data-ttu-id="78a62-255">Entero </span><span class="sxs-lookup"><span data-stu-id="78a62-255">Integer</span></span> <br/><br/><span data-ttu-id="78a62-256">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="78a62-256">Max value: 10</span></span> |<span data-ttu-id="78a62-257">1</span><span class="sxs-lookup"><span data-stu-id="78a62-257">1</span></span> |<span data-ttu-id="78a62-258">Número de ejecuciones simultáneas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="78a62-259">Determina el número de ejecuciones paralelas de la actividad que pueden tener lugar en distintos segmentos.</span><span class="sxs-lookup"><span data-stu-id="78a62-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="78a62-260">Por ejemplo, si una actividad tiene que recorrer un gran conjunto de datos disponibles, tener un valor mayor de simultaneidad acelera el procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="78a62-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="78a62-261">executionPriorityOrder</span></span> |<span data-ttu-id="78a62-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="78a62-262">NewestFirst</span></span><br/><br/><span data-ttu-id="78a62-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="78a62-263">OldestFirst</span></span> |<span data-ttu-id="78a62-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="78a62-264">OldestFirst</span></span> |<span data-ttu-id="78a62-265">Determina el orden de los segmentos de datos que se están procesando.</span><span class="sxs-lookup"><span data-stu-id="78a62-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="78a62-266">Por ejemplo, si tiene 2 segmentos (que tienen lugar uno a las 4 p.m. y el otro a las 5 p.m.) y ambos están pendientes de ejecución.</span><span class="sxs-lookup"><span data-stu-id="78a62-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="78a62-267">Si establece que executionPriorityOrder sea NewestFirst, se procesará primero el segmento de las 5 p.m.</span><span class="sxs-lookup"><span data-stu-id="78a62-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="78a62-268">De forma similar, si establece que executionPriorityORder sea OldestFIrst, se procesará el segmento de las 4 p.m.</span><span class="sxs-lookup"><span data-stu-id="78a62-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="78a62-269">retry</span><span class="sxs-lookup"><span data-stu-id="78a62-269">retry</span></span> |<span data-ttu-id="78a62-270">Entero </span><span class="sxs-lookup"><span data-stu-id="78a62-270">Integer</span></span><br/><br/><span data-ttu-id="78a62-271">El valor máximo permitido es 10</span><span class="sxs-lookup"><span data-stu-id="78a62-271">Max value can be 10</span></span> |<span data-ttu-id="78a62-272">0</span><span class="sxs-lookup"><span data-stu-id="78a62-272">0</span></span> |<span data-ttu-id="78a62-273">Número de reintentos antes de que el procesamiento de datos del segmento se marque como error.</span><span class="sxs-lookup"><span data-stu-id="78a62-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="78a62-274">La ejecución de la actividad de un segmento de datos se vuelve a intentar hasta el número de reintentos especificado.</span><span class="sxs-lookup"><span data-stu-id="78a62-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="78a62-275">El reintento se realiza tan pronto como sea posible después del error.</span><span class="sxs-lookup"><span data-stu-id="78a62-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="78a62-276">timeout</span><span class="sxs-lookup"><span data-stu-id="78a62-276">timeout</span></span> |<span data-ttu-id="78a62-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78a62-277">TimeSpan</span></span> |<span data-ttu-id="78a62-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="78a62-278">00:00:00</span></span> |<span data-ttu-id="78a62-279">Tiempo de espera para la actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-279">Timeout for the activity.</span></span> <span data-ttu-id="78a62-280">Ejemplo: 00:10:00 (implica un tiempo de espera de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="78a62-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="78a62-281">Si un valor no se especifica o es 0, el tiempo de espera es infinito.</span><span class="sxs-lookup"><span data-stu-id="78a62-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="78a62-282">Si el tiempo de procesamiento de los datos en un segmento supera el valor de tiempo de espera, se cancela y el sistema vuelve a intentar el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="78a62-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="78a62-283">El número de reintentos depende de la propiedad retry.</span><span class="sxs-lookup"><span data-stu-id="78a62-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="78a62-284">Si se excede el tiempo de espera, el estado será TimedOut.</span><span class="sxs-lookup"><span data-stu-id="78a62-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="78a62-285">delay</span><span class="sxs-lookup"><span data-stu-id="78a62-285">delay</span></span> |<span data-ttu-id="78a62-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78a62-286">TimeSpan</span></span> |<span data-ttu-id="78a62-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="78a62-287">00:00:00</span></span> |<span data-ttu-id="78a62-288">Especifica el retraso antes de iniciar el procesamiento de los datos del segmento.</span><span class="sxs-lookup"><span data-stu-id="78a62-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="78a62-289">La ejecución de la actividad de un segmento de datos se inicia una vez que transcurra el retraso más allá del tiempo de ejecución esperado.</span><span class="sxs-lookup"><span data-stu-id="78a62-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="78a62-290">Ejemplo: 00:10:00 (implica un retraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="78a62-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="78a62-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="78a62-291">longRetry</span></span> |<span data-ttu-id="78a62-292">Entero </span><span class="sxs-lookup"><span data-stu-id="78a62-292">Integer</span></span><br/><br/><span data-ttu-id="78a62-293">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="78a62-293">Max value: 10</span></span> |<span data-ttu-id="78a62-294">1</span><span class="sxs-lookup"><span data-stu-id="78a62-294">1</span></span> |<span data-ttu-id="78a62-295">Número de reintentos largos antes de que la ejecución de los segmentos produzca error.</span><span class="sxs-lookup"><span data-stu-id="78a62-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="78a62-296">Los intentos de longRetry se espacian de acuerdo a longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="78a62-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="78a62-297">Por tanto, si necesita especificar un tiempo entre reintentos, utilice longRetry.</span><span class="sxs-lookup"><span data-stu-id="78a62-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="78a62-298">Si se especifican Retry y longRetry, cada intento de longRetry incluirá el número de intentos de Retry y el número máximo de intentos será Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="78a62-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="78a62-299">Por ejemplo, si tenemos la siguiente configuración en la directiva de la actividad:</span><span class="sxs-lookup"><span data-stu-id="78a62-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="78a62-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="78a62-300">Retry: 3</span></span><br/><span data-ttu-id="78a62-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="78a62-301">longRetry: 2</span></span><br/><span data-ttu-id="78a62-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="78a62-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="78a62-303">Se supone que existe un solo segmento para ejecutar (el estado es En espera) y la ejecución de la actividad no se puede realizar nunca.</span><span class="sxs-lookup"><span data-stu-id="78a62-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="78a62-304">Inicialmente habría tres intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="78a62-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="78a62-305">Después de cada intento, el estado del segmento sería Retry.</span><span class="sxs-lookup"><span data-stu-id="78a62-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="78a62-306">Después de los 3 primeros intentos, el estado del segmento sería LongRetry.</span><span class="sxs-lookup"><span data-stu-id="78a62-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="78a62-307">Después de una hora (es decir, el valor de longRetryInteval), se produciría otro conjunto de 3 intentos consecutivos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="78a62-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="78a62-308">Después de eso, el estado del segmento sería Failed y ya no se realizarían más intentos.</span><span class="sxs-lookup"><span data-stu-id="78a62-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="78a62-309">Por tanto, en total se realizaron 6 intentos.</span><span class="sxs-lookup"><span data-stu-id="78a62-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="78a62-310">Si una ejecución se realiza correctamente, el estado del segmento sería Ready y no se realizaría ningún otro reintento.</span><span class="sxs-lookup"><span data-stu-id="78a62-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="78a62-311">longRetry puede usarse en situaciones donde llegan datos dependientes a horas no deterministas o el entorno general en el que se produce el procesamiento de datos es poco confiable.</span><span class="sxs-lookup"><span data-stu-id="78a62-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="78a62-312">En esos casos es posible que realizar reintentos uno tras otro no ayude, mientras que hacerlo después de un intervalo de tiempo puede generar el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="78a62-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="78a62-313">Advertencia: No establezca valores altos para longRetry o longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="78a62-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="78a62-314">Normalmente, los valores más altos implican otros problemas sistémicos.</span><span class="sxs-lookup"><span data-stu-id="78a62-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="78a62-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="78a62-315">longRetryInterval</span></span> |<span data-ttu-id="78a62-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78a62-316">TimeSpan</span></span> |<span data-ttu-id="78a62-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="78a62-317">00:00:00</span></span> |<span data-ttu-id="78a62-318">El retraso entre reintentos largos</span><span class="sxs-lookup"><span data-stu-id="78a62-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="78a62-319">Para más información, vea el artículo [Canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="78a62-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="78a62-320">Procesamiento en paralelo de segmentos de datos</span><span class="sxs-lookup"><span data-stu-id="78a62-320">Parallel processing of data slices</span></span>
<span data-ttu-id="78a62-321">Puede establecer la fecha de inicio de la canalización en el pasado.</span><span class="sxs-lookup"><span data-stu-id="78a62-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="78a62-322">Al hacerlo, Data Factory calcula automáticamente (relleno de fondo) todos los segmentos de datos en el pasado y empieza a procesarlos.</span><span class="sxs-lookup"><span data-stu-id="78a62-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="78a62-323">Por ejemplo, si crea una canalización con la fecha de inicio 01-04-2017 y la fecha actual es 10-04-2017.</span><span class="sxs-lookup"><span data-stu-id="78a62-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="78a62-324">Si la cadencia del conjunto de datos de salida es diaria, Data Factory empieza a procesar todos los segmentos desde el 01-04-2017 hasta el 09-04-2017 inmediatamente, porque la fecha de inicio se ha fijado en el pasado.</span><span class="sxs-lookup"><span data-stu-id="78a62-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="78a62-325">El segmento del 10-04-2017 no se procesa todavía porque el valor de la propiedad style de la sección availability es EndOfInterval de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="78a62-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="78a62-326">El segmento más antiguo se procesa en primer lugar, ya que el valor predeterminado de executionPriorityOrder es OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="78a62-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="78a62-327">Para obtener una descripción de la propiedad style, vea la sección [Disponibilidad del conjunto de datos](#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="78a62-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="78a62-328">Para obtener una descripción de la sección executionPriorityOrder, vea la sección [Directivas de la actividad](#activity-policies).</span><span class="sxs-lookup"><span data-stu-id="78a62-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="78a62-329">Puede configurar segmentos de datos de relleno de fondo para que se procesen en paralelo estableciendo la propiedad **concurrency** en la sección **policy** de la actividad JSON.</span><span class="sxs-lookup"><span data-stu-id="78a62-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="78a62-330">Esta propiedad determina el número de ejecuciones paralelas de la actividad que pueden tener lugar en distintos segmentos.</span><span class="sxs-lookup"><span data-stu-id="78a62-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="78a62-331">El valor predeterminado de la propiedad concurrency es 1.</span><span class="sxs-lookup"><span data-stu-id="78a62-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="78a62-332">Por tanto, se procesa un segmento a la vez de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="78a62-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="78a62-333">El valor máximo es 10.</span><span class="sxs-lookup"><span data-stu-id="78a62-333">The maximum value is 10.</span></span> <span data-ttu-id="78a62-334">Si una actividad tiene que recorrer un gran conjunto de datos disponibles, tener un valor mayor de simultaneidad acelera el procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="78a62-335">Volver a ejecutar un segmento de datos con errores</span><span class="sxs-lookup"><span data-stu-id="78a62-335">Rerun a failed data slice</span></span>
<span data-ttu-id="78a62-336">Cuando se produce un error durante el procesamiento de un segmento de datos, puede averiguar la causa en las hojas de Azure Portal o con la Aplicación de supervisión y administración.</span><span class="sxs-lookup"><span data-stu-id="78a62-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="78a62-337">Consulte [Supervisión y administración de canalizaciones mediante hojas de Azure Portal](data-factory-monitor-manage-pipelines.md) o [Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="78a62-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="78a62-338">Observe el ejemplo siguiente, que muestra dos actividades.</span><span class="sxs-lookup"><span data-stu-id="78a62-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="78a62-339">Activity1 y Activity2.</span><span class="sxs-lookup"><span data-stu-id="78a62-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="78a62-340">Activity1 consume un segmento de Dataset1 y genera un segmento de Dataset2, que Activity2 consume como entrada para generar un segmento de Final Dataset.</span><span class="sxs-lookup"><span data-stu-id="78a62-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![Segmento con errores](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="78a62-342">El diagrama muestra que en tres segmentos recientes se produjo un error al generar el segmento 9-10 AM para Dataset2.</span><span class="sxs-lookup"><span data-stu-id="78a62-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="78a62-343">Data Factory realiza automáticamente el seguimiento de la dependencia para el conjunto de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="78a62-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="78a62-344">Como resultado, no se inicia la ejecución de actividad para el segmento 9-10 AM de bajada.</span><span class="sxs-lookup"><span data-stu-id="78a62-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="78a62-345">Las herramientas de administración y supervisión de Data Factory permiten profundizar en los registros de diagnóstico del segmento con error para encontrar fácilmente la causa principal del problema y solucionarlo.</span><span class="sxs-lookup"><span data-stu-id="78a62-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="78a62-346">Una vez solucionado el problema, puede iniciar fácilmente la ejecución de la actividad para generar el segmento con error.</span><span class="sxs-lookup"><span data-stu-id="78a62-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="78a62-347">Para más información sobre cómo repetir la ejecución y entender las transiciones de estado para segmentos de datos, vea [Supervisión y administración de canalizaciones en las hojas de Azure Portal](data-factory-monitor-manage-pipelines.md) o [Aplicación de supervisión y administración](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="78a62-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="78a62-348">Tras haber repetido la ejecución del segmento 9-10 AM para **Dataset2**, Data Factory inicia la ejecución del segmento dependiente de 9-10 AM en el conjunto de datos final.</span><span class="sxs-lookup"><span data-stu-id="78a62-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Repetición de ejecución de un segmento con errores](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="78a62-350">Varias actividades en una canalización</span><span class="sxs-lookup"><span data-stu-id="78a62-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="78a62-351">pero se pueden tener más de una actividad en una canalización.</span><span class="sxs-lookup"><span data-stu-id="78a62-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="78a62-352">Si tiene varias actividades en una canalización y la salida de una actividad no es la entrada de otra actividad, las actividades se pueden ejecutar en paralelo si los segmentos de datos de entrada para las actividades están listos.</span><span class="sxs-lookup"><span data-stu-id="78a62-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="78a62-353">Puede encadenar dos actividades (ejecutar una después de otra) haciendo que el conjunto de datos de salida de una actividad sea el conjunto de datos de entrada de la otra actividad.</span><span class="sxs-lookup"><span data-stu-id="78a62-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="78a62-354">Las actividades pueden estar en la misma canalización o en canalizaciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="78a62-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="78a62-355">La segunda actividad se ejecuta solo cuando la primera de ellas se completa correctamente.</span><span class="sxs-lookup"><span data-stu-id="78a62-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="78a62-356">Por ejemplo, observe el siguiente caso en el que una canalización tiene dos actividades:</span><span class="sxs-lookup"><span data-stu-id="78a62-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="78a62-357">La actividad A1 que requiere el conjunto de datos de entrada externo D1 y genera el conjunto de datos de salida D2.</span><span class="sxs-lookup"><span data-stu-id="78a62-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="78a62-358">La actividad A2 que requiere una entrada del conjunto de datos D2 y genera el conjunto de datos de salida D3.</span><span class="sxs-lookup"><span data-stu-id="78a62-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="78a62-359">En este escenario, las actividades A1 y A2 se encuentran en la misma canalización.</span><span class="sxs-lookup"><span data-stu-id="78a62-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="78a62-360">La actividad A1 se ejecuta cuando los datos externos están disponibles y se alcanza la frecuencia de disponibilidad programada.</span><span class="sxs-lookup"><span data-stu-id="78a62-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="78a62-361">La actividad A2 se ejecuta cuando están disponibles los segmentos programados de D2 y se alcanza la frecuencia de disponibilidad programada.</span><span class="sxs-lookup"><span data-stu-id="78a62-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="78a62-362">Si se produce un error en uno de los segmentos del conjunto de datos D2, A2 no se ejecuta para ese segmento hasta que está disponible.</span><span class="sxs-lookup"><span data-stu-id="78a62-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="78a62-363">La vista Diagrama con ambas actividades en la misma canalización tendría un aspecto similar al siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="78a62-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Encadenamiento de las actividades de la misma canalización](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="78a62-365">Tal y como se ha mencionado anteriormente, las actividades pueden estar en distintas canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="78a62-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="78a62-366">En tal escenario, la vista de diagrama tendría un aspecto similar al siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="78a62-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![Encadenamiento de las actividades de dos canalizaciones](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="78a62-368">Vea la sección [Copia secuencial](#copy-sequentially) del anexo para obtener un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="78a62-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="78a62-369">Modelado de conjuntos de datos con distintas frecuencias</span><span class="sxs-lookup"><span data-stu-id="78a62-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="78a62-370">En los ejemplos, las frecuencias de los conjuntos de datos de entrada y salida y de la ventana de programación de actividad eran las mismas.</span><span class="sxs-lookup"><span data-stu-id="78a62-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="78a62-371">Algunos escenarios requieren que se puedan producir resultados a una frecuencia diferente de las frecuencias de una o más entradas.</span><span class="sxs-lookup"><span data-stu-id="78a62-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="78a62-372">Data Factory admite el modelado de estos escenarios.</span><span class="sxs-lookup"><span data-stu-id="78a62-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="78a62-373">Ejemplo 1: Generación de un informe de salida diario para los datos de entrada que esté disponibles cada hora</span><span class="sxs-lookup"><span data-stu-id="78a62-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="78a62-374">Considere un escenario en el que tiene datos de medida de entrada de sensores disponibles cada hora en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="78a62-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="78a62-375">Quiere generar un informe agregado diario con estadísticas como media, máximo y mínimo para el día con la [actividad de Hive de Data Factory](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="78a62-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="78a62-376">A continuación, se muestra cómo puede modelar este escenario con Data Factory:</span><span class="sxs-lookup"><span data-stu-id="78a62-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="78a62-377">**Conjunto de datos de entrada**</span><span class="sxs-lookup"><span data-stu-id="78a62-377">**Input dataset**</span></span>

<span data-ttu-id="78a62-378">Se quitan los archivos de entrada de cada hora en la carpeta para el día especificado.</span><span class="sxs-lookup"><span data-stu-id="78a62-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="78a62-379">La disponibilidad para la entrada se establece en **Hour** (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="78a62-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="78a62-380">**Conjunto de datos de salida**</span><span class="sxs-lookup"><span data-stu-id="78a62-380">**Output dataset**</span></span>

<span data-ttu-id="78a62-381">Cada día se crea un archivo de salida en la carpeta del día.</span><span class="sxs-lookup"><span data-stu-id="78a62-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="78a62-382">La disponibilidad de la salida se establece en **Day** (frecuencia: día e intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="78a62-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="78a62-383">**Actividad: actividad de Hive en una canalización**</span><span class="sxs-lookup"><span data-stu-id="78a62-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="78a62-384">El script de Hive recibe la información adecuada de *DateTime* como parámetros que usan la variable **WindowStart** como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="78a62-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="78a62-385">El script de Hive usa esta variable para cargar los datos de la carpeta correcta para el día y ejecutar la agregación para generar la salida.</span><span class="sxs-lookup"><span data-stu-id="78a62-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="78a62-386">El diagrama siguiente muestra el escenario desde el punto de vista de la dependencia de datos.</span><span class="sxs-lookup"><span data-stu-id="78a62-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Dependencia de los datos](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="78a62-388">El segmento de salida para cada día depende de 24 segmentos por hora del conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="78a62-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="78a62-389">Data Factory calcula automáticamente estas dependencias al determinar los segmentos de datos de entrada que se encuentran en el mismo período de tiempo que el segmento de salida que se va a producir.</span><span class="sxs-lookup"><span data-stu-id="78a62-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="78a62-390">Si cualquiera de los 24 segmentos de entrada no está disponible, Data Factory espera a que el segmento de entrada esté listo antes de empezar la ejecución de la actividad diaria.</span><span class="sxs-lookup"><span data-stu-id="78a62-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="78a62-391">Ejemplo 2: Especificación de la dependencia con expresiones y funciones de Data Factory</span><span class="sxs-lookup"><span data-stu-id="78a62-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="78a62-392">Consideremos otro escenario.</span><span class="sxs-lookup"><span data-stu-id="78a62-392">Let’s consider another scenario.</span></span> <span data-ttu-id="78a62-393">Suponga que tiene una actividad de Hive que procesa dos conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="78a62-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="78a62-394">Uno de ellos tiene nuevos datos diariamente, pero otro obtiene datos nuevos cada semana.</span><span class="sxs-lookup"><span data-stu-id="78a62-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="78a62-395">Supongamos que desea combinar las dos entradas y producir una salida cada día.</span><span class="sxs-lookup"><span data-stu-id="78a62-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="78a62-396">El enfoque sencillo, en el que Data Factory determina automáticamente los segmentos de entrada correctos que se van a procesar al alinearlos con el período de los segmentos de datos de salida, no funciona.</span><span class="sxs-lookup"><span data-stu-id="78a62-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="78a62-397">Debe especificar que para cada ejecución de actividad, Data Factory debe usar el segmento de datos de la semana pasada para el conjunto de datos de entrada semanal.</span><span class="sxs-lookup"><span data-stu-id="78a62-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="78a62-398">Utilice funciones de Azure Data Factory, como se muestra en el siguiente fragmento para implementar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="78a62-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="78a62-399">**Input1: blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="78a62-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="78a62-400">La primera entrada es el blob de Azure que se actualiza diariamente.</span><span class="sxs-lookup"><span data-stu-id="78a62-400">The first input is the Azure blob being updated daily.</span></span>

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

<span data-ttu-id="78a62-401">**Input2: blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="78a62-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="78a62-402">Input2 es el blob de Azure que se actualiza semanalmente.</span><span class="sxs-lookup"><span data-stu-id="78a62-402">Input2 is the Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="78a62-403">**Salida: blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="78a62-403">**Output: Azure blob**</span></span>

<span data-ttu-id="78a62-404">Cada día se crea un archivo de salida en la carpeta del día.</span><span class="sxs-lookup"><span data-stu-id="78a62-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="78a62-405">La disponibilidad de la salida se establece en **day** (frecuencia: día, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="78a62-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="78a62-406">**Actividad: actividad de Hive en una canalización**</span><span class="sxs-lookup"><span data-stu-id="78a62-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="78a62-407">La actividad de Hive toma las dos entradas y genera un segmento de salida cada día.</span><span class="sxs-lookup"><span data-stu-id="78a62-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="78a62-408">Puede especificar de la forma siguiente el segmento de salida de cada día para que dependa de segmento de entrada de la semana pasada para la entrada semanal.</span><span class="sxs-lookup"><span data-stu-id="78a62-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="78a62-409">Para conocer la lista de funciones y variables del sistema que admite Data Factory, consulte el artículo [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="78a62-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="78a62-410">Anexo</span><span class="sxs-lookup"><span data-stu-id="78a62-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="78a62-411">Ejemplo: copia secuencial</span><span class="sxs-lookup"><span data-stu-id="78a62-411">Example: copy sequentially</span></span>
<span data-ttu-id="78a62-412">Es posible ejecutar varias operaciones de copia sucesivas de manera secuencial y ordenada.</span><span class="sxs-lookup"><span data-stu-id="78a62-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="78a62-413">Por ejemplo, podría tener dos actividades de copia en una canalización (CopyActivity1 y CopyActivity2) con los siguientes conjuntos de datos de entrada y salida:</span><span class="sxs-lookup"><span data-stu-id="78a62-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="78a62-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="78a62-414">CopyActivity1</span></span>

<span data-ttu-id="78a62-415">Entrada: Dataset.</span><span class="sxs-lookup"><span data-stu-id="78a62-415">Input: Dataset.</span></span> <span data-ttu-id="78a62-416">Salida: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="78a62-416">Output: Dataset2.</span></span>

<span data-ttu-id="78a62-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="78a62-417">CopyActivity2</span></span>

<span data-ttu-id="78a62-418">Entrada: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="78a62-418">Input: Dataset2.</span></span>  <span data-ttu-id="78a62-419">Salida: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="78a62-419">Output: Dataset3.</span></span>

<span data-ttu-id="78a62-420">ActividadCopia2 solo se ejecutaría si ActividadCopia1 se hubiera ejecutado correctamente y ConjuntoDatos2 estuviera disponible.</span><span class="sxs-lookup"><span data-stu-id="78a62-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="78a62-421">Esta es el JSON de canalización de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="78a62-421">Here is the sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="78a62-422">Observe que en el ejemplo, el conjunto de datos de salida de la primera actividad de copia (ConjuntoDatos2) se especifica como entrada para la segunda.</span><span class="sxs-lookup"><span data-stu-id="78a62-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="78a62-423">Por lo tanto, la segunda actividad solo se ejecuta cuando el conjunto de datos de salida de la primera está listo.</span><span class="sxs-lookup"><span data-stu-id="78a62-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="78a62-424">En el ejemplo, CopyActivity2 puede tener una entrada distinta, como Dataset3, pero especifica Dataset2 como una entrada de CopyActivity2 para que la actividad no se ejecute hasta que se haya completado CopyActivity1.</span><span class="sxs-lookup"><span data-stu-id="78a62-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="78a62-425">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="78a62-425">For example:</span></span>

<span data-ttu-id="78a62-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="78a62-426">CopyActivity1</span></span>

<span data-ttu-id="78a62-427">Entrada: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="78a62-427">Input: Dataset1.</span></span> <span data-ttu-id="78a62-428">Salida: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="78a62-428">Output: Dataset2.</span></span>

<span data-ttu-id="78a62-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="78a62-429">CopyActivity2</span></span>

<span data-ttu-id="78a62-430">Entradas: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="78a62-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="78a62-431">Salida: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="78a62-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="78a62-432">Observe que en el ejemplo, hay dos conjuntos de datos de entrada especificados para la segunda actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="78a62-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="78a62-433">Cuando se especifican varias entradas, solo se usa el primer conjunto de datos de entrada para copiar los datos. Sin embargo, los demás conjuntos de datos se usan como dependencias.</span><span class="sxs-lookup"><span data-stu-id="78a62-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="78a62-434">CopyActivity2 empezaría solo después de que se cumplen las condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="78a62-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="78a62-435">ActividadCopia1 se ha completado correctamente y ConjuntoDatos2 está disponible.</span><span class="sxs-lookup"><span data-stu-id="78a62-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="78a62-436">Este conjunto de datos no se usa al copiar datos en Dataset4.</span><span class="sxs-lookup"><span data-stu-id="78a62-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="78a62-437">Solo actúa como una dependencia de programación de ActividadCopia2.</span><span class="sxs-lookup"><span data-stu-id="78a62-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="78a62-438">ConjuntoDatos3 está disponible.</span><span class="sxs-lookup"><span data-stu-id="78a62-438">Dataset3 is available.</span></span> <span data-ttu-id="78a62-439">Este conjunto de datos representa los datos que se copian en el destino.</span><span class="sxs-lookup"><span data-stu-id="78a62-439">This dataset represents the data that is copied to the destination.</span></span> 