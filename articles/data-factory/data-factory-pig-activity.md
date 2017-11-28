---
title: "Transformación de datos mediante la actividad de Pig en Azure Data Factory | Microsoft Docs"
description: "Aprenda cómo puede usar la actividad de Pig en Factoría de datos de Azure para ejecutar scripts de Pig en un clúster de HDInsight suyo propio o a petición."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="32f9f-103">Transformación de datos mediante la actividad de Pig en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="32f9f-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="32f9f-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="32f9f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="32f9f-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="32f9f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="32f9f-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="32f9f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="32f9f-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="32f9f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="32f9f-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="32f9f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="32f9f-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32f9f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="32f9f-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32f9f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="32f9f-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="32f9f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="32f9f-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="32f9f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="32f9f-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="32f9f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="32f9f-114">La actividad de Pig para HDInsight en una [canalización](data-factory-create-pipelines.md) de Data Factory ejecuta consultas de Pig en un clúster de HDInsight basado en Windows/Linux [propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o en uno [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="32f9f-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="32f9f-115">Este artículo se basa en el artículo sobre [actividades de transformación de datos](data-factory-data-transformation-activities.md) , que presenta información general de la transformación de datos y las actividades de transformación admitidas.</span><span class="sxs-lookup"><span data-stu-id="32f9f-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="32f9f-116">Si no está familiarizado con Azure Data Factory, lea [Introducción a Azure Data Factory](data-factory-introduction.md) y realice el tutorial de [compilación de la primera canalización de datos](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="32f9f-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="32f9f-117">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="32f9f-117">Syntax</span></span>

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a><span data-ttu-id="32f9f-118">Detalles de la sintaxis</span><span class="sxs-lookup"><span data-stu-id="32f9f-118">Syntax details</span></span>
| <span data-ttu-id="32f9f-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="32f9f-119">Property</span></span> | <span data-ttu-id="32f9f-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="32f9f-120">Description</span></span> | <span data-ttu-id="32f9f-121">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="32f9f-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32f9f-122">name</span><span class="sxs-lookup"><span data-stu-id="32f9f-122">name</span></span> |<span data-ttu-id="32f9f-123">Nombre de la actividad</span><span class="sxs-lookup"><span data-stu-id="32f9f-123">Name of the activity</span></span> |<span data-ttu-id="32f9f-124">Sí</span><span class="sxs-lookup"><span data-stu-id="32f9f-124">Yes</span></span> |
| <span data-ttu-id="32f9f-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="32f9f-125">description</span></span> |<span data-ttu-id="32f9f-126">Texto que describe para qué se usa la actividad.</span><span class="sxs-lookup"><span data-stu-id="32f9f-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="32f9f-127">No</span><span class="sxs-lookup"><span data-stu-id="32f9f-127">No</span></span> |
| <span data-ttu-id="32f9f-128">type</span><span class="sxs-lookup"><span data-stu-id="32f9f-128">type</span></span> |<span data-ttu-id="32f9f-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="32f9f-129">HDinsightPig</span></span> |<span data-ttu-id="32f9f-130">Sí</span><span class="sxs-lookup"><span data-stu-id="32f9f-130">Yes</span></span> |
| <span data-ttu-id="32f9f-131">inputs</span><span class="sxs-lookup"><span data-stu-id="32f9f-131">inputs</span></span> |<span data-ttu-id="32f9f-132">Una o varias entradas consumidas por la actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="32f9f-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="32f9f-133">No</span><span class="sxs-lookup"><span data-stu-id="32f9f-133">No</span></span> |
| <span data-ttu-id="32f9f-134">outputs</span><span class="sxs-lookup"><span data-stu-id="32f9f-134">outputs</span></span> |<span data-ttu-id="32f9f-135">Una o varias salidas producidas por la actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="32f9f-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="32f9f-136">Sí</span><span class="sxs-lookup"><span data-stu-id="32f9f-136">Yes</span></span> |
| <span data-ttu-id="32f9f-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="32f9f-137">linkedServiceName</span></span> |<span data-ttu-id="32f9f-138">Referencia al clúster de HDInsight registrado como un servicio vinculado en la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="32f9f-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="32f9f-139">Sí</span><span class="sxs-lookup"><span data-stu-id="32f9f-139">Yes</span></span> |
| <span data-ttu-id="32f9f-140">script</span><span class="sxs-lookup"><span data-stu-id="32f9f-140">script</span></span> |<span data-ttu-id="32f9f-141">Especifica el script de Pig en línea</span><span class="sxs-lookup"><span data-stu-id="32f9f-141">Specify the Pig script inline</span></span> |<span data-ttu-id="32f9f-142">No</span><span class="sxs-lookup"><span data-stu-id="32f9f-142">No</span></span> |
| <span data-ttu-id="32f9f-143">ruta de acceso de script</span><span class="sxs-lookup"><span data-stu-id="32f9f-143">script path</span></span> |<span data-ttu-id="32f9f-144">Almacena el script de Pig en un almacenamiento de blobs de Azure y proporciona la ruta de acceso al archivo.</span><span class="sxs-lookup"><span data-stu-id="32f9f-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="32f9f-145">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="32f9f-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="32f9f-146">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="32f9f-146">Both cannot be used together.</span></span> <span data-ttu-id="32f9f-147">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="32f9f-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="32f9f-148">No</span><span class="sxs-lookup"><span data-stu-id="32f9f-148">No</span></span> |
| <span data-ttu-id="32f9f-149">define los campos</span><span class="sxs-lookup"><span data-stu-id="32f9f-149">defines</span></span> |<span data-ttu-id="32f9f-150">Especifique parámetros como pares de clave y valor para referencia en el script de Pig</span><span class="sxs-lookup"><span data-stu-id="32f9f-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="32f9f-151">No</span><span class="sxs-lookup"><span data-stu-id="32f9f-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="32f9f-152">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="32f9f-152">Example</span></span>
<span data-ttu-id="32f9f-153">Veamos un ejemplo de análisis de registros de juegos en el que desea identificar el tiempo dedicado por los usuarios a los juegos de su compañía.</span><span class="sxs-lookup"><span data-stu-id="32f9f-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="32f9f-154">El registro de juegos de ejemplo siguiente es un archivo separado por comas (,),</span><span class="sxs-lookup"><span data-stu-id="32f9f-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="32f9f-155">que contiene los siguientes campos: ProfileID, SessionStart, Duration, SrcIPAddress y GameType.</span><span class="sxs-lookup"><span data-stu-id="32f9f-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="32f9f-156">El **script de Pig** para procesar estos datos tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="32f9f-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="32f9f-157">Para ejecutar este script de Pig en una canalización de Data Factory, tiene que hacer los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="32f9f-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="32f9f-158">Crear un servicio vinculado para registrar [su propio clúster de proceso de HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurar un [clúster de proceso de HDInsight a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="32f9f-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="32f9f-159">Llamaremos a este servicio vinculado **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="32f9f-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="32f9f-160">Crear un [servicio vinculado](data-factory-azure-blob-connector.md) para configurar la conexión al almacenamiento de blobs de Azure que hospeda los datos.</span><span class="sxs-lookup"><span data-stu-id="32f9f-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="32f9f-161">Llamaremos a este servicio vinculado **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="32f9f-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="32f9f-162">Crear [conjuntos de datos](data-factory-create-datasets.md) que apuntan a los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="32f9f-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="32f9f-163">Llamaremos al conjunto de datos de entrada **PigSampleIn** y al conjunto de datos de salida **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="32f9f-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="32f9f-164">Copie la consulta de Pig en un archivo de almacenamiento de blobs de Azure configurado en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="32f9f-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="32f9f-165">Si el almacenamiento de Azure que hospeda los datos es diferente del que hospeda el archivo de consulta, cree un servicio vinculado de almacenamiento de Azure independiente.</span><span class="sxs-lookup"><span data-stu-id="32f9f-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="32f9f-166">Consulte el servicio vinculado en la configuración de la actividad.</span><span class="sxs-lookup"><span data-stu-id="32f9f-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="32f9f-167">Use **scriptPath** para especificar la ruta de acceso al archivo de script de Pig y **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="32f9f-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="32f9f-168">También puede proporcionar el script de Pig en línea en la definición de actividad mediante la propiedad **script** .</span><span class="sxs-lookup"><span data-stu-id="32f9f-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="32f9f-169">Sin embargo, no se recomienda este enfoque cuando todos los caracteres especiales del script tienen que ser caracteres de escape y pueden provocar problemas de depuración.</span><span class="sxs-lookup"><span data-stu-id="32f9f-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="32f9f-170">La práctica recomendada es seguir el paso 4.</span><span class="sxs-lookup"><span data-stu-id="32f9f-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="32f9f-171">Cree la canalización con la actividad HDInsightPig.</span><span class="sxs-lookup"><span data-stu-id="32f9f-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="32f9f-172">Esta actividad procesa los datos de entrada mediante la ejecución de script de Pig en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="32f9f-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. <span data-ttu-id="32f9f-173">Implemente la canalización.</span><span class="sxs-lookup"><span data-stu-id="32f9f-173">Deploy the pipeline.</span></span> <span data-ttu-id="32f9f-174">Consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="32f9f-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="32f9f-175">Supervise la canalización mediante las vistas de supervisión y administración de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="32f9f-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="32f9f-176">Consulte el artículo [Supervisión y administración de las canalizaciones de Factoría de datos](data-factory-monitor-manage-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="32f9f-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="32f9f-177">Especificación de parámetros para un script de Pig</span><span class="sxs-lookup"><span data-stu-id="32f9f-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="32f9f-178">Tenga en cuenta el siguiente ejemplo en el que los registros de juegos se introducen diariamente en el almacenamiento de blobs de Azure y se almacenan en una carpeta en función de la fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="32f9f-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="32f9f-179">Desea parametrizar el script de Pig y pasar la ubicación de la carpeta de entrada dinámicamente en tiempo de ejecución y también generar la salida dividida con fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="32f9f-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="32f9f-180">Para usar un script de Pig parametrizado, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="32f9f-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="32f9f-181">Defina los parámetros en **defines**.</span><span class="sxs-lookup"><span data-stu-id="32f9f-181">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* <span data-ttu-id="32f9f-182">En el script de Pig, consulte los parámetros utilizando '**$parameterName**' como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="32f9f-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="32f9f-183">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="32f9f-183">See Also</span></span>
* [<span data-ttu-id="32f9f-184">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="32f9f-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="32f9f-185">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="32f9f-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="32f9f-186">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="32f9f-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="32f9f-187">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="32f9f-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="32f9f-188">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="32f9f-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

