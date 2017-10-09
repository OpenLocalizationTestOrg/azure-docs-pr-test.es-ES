---
title: "datos de aaaTransform con actividad de Pig de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo puede utilizar Hola actividad de Pig en un scripts de Pig de toorun de factoría de datos de Azure en un clúster de HDInsight en-petición/su propio."
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
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="da9c0-103">Transformación de datos mediante la actividad de Pig en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="da9c0-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="da9c0-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="da9c0-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="da9c0-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="da9c0-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="da9c0-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="da9c0-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="da9c0-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="da9c0-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="da9c0-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="da9c0-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="da9c0-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="da9c0-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="da9c0-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="da9c0-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="da9c0-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="da9c0-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="da9c0-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="da9c0-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="da9c0-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="da9c0-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="da9c0-114">Hola actividad de HDInsight Pig en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta consultas de Pig en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) clúster de HDInsight basados en Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="da9c0-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="da9c0-115">En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="da9c0-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="da9c0-116">Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="da9c0-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="da9c0-117">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="da9c0-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="da9c0-118">Detalles de la sintaxis</span><span class="sxs-lookup"><span data-stu-id="da9c0-118">Syntax details</span></span>
| <span data-ttu-id="da9c0-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="da9c0-119">Property</span></span> | <span data-ttu-id="da9c0-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="da9c0-120">Description</span></span> | <span data-ttu-id="da9c0-121">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da9c0-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da9c0-122">name</span><span class="sxs-lookup"><span data-stu-id="da9c0-122">name</span></span> |<span data-ttu-id="da9c0-123">Nombre de actividad de Hola</span><span class="sxs-lookup"><span data-stu-id="da9c0-123">Name of hello activity</span></span> |<span data-ttu-id="da9c0-124">Sí</span><span class="sxs-lookup"><span data-stu-id="da9c0-124">Yes</span></span> |
| <span data-ttu-id="da9c0-125">description</span><span class="sxs-lookup"><span data-stu-id="da9c0-125">description</span></span> |<span data-ttu-id="da9c0-126">Texto que describe qué actividad Hola se usa para</span><span class="sxs-lookup"><span data-stu-id="da9c0-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="da9c0-127">No</span><span class="sxs-lookup"><span data-stu-id="da9c0-127">No</span></span> |
| <span data-ttu-id="da9c0-128">type</span><span class="sxs-lookup"><span data-stu-id="da9c0-128">type</span></span> |<span data-ttu-id="da9c0-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="da9c0-129">HDinsightPig</span></span> |<span data-ttu-id="da9c0-130">Sí</span><span class="sxs-lookup"><span data-stu-id="da9c0-130">Yes</span></span> |
| <span data-ttu-id="da9c0-131">inputs</span><span class="sxs-lookup"><span data-stu-id="da9c0-131">inputs</span></span> |<span data-ttu-id="da9c0-132">Una o más entradas consumen Hola actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="da9c0-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="da9c0-133">No</span><span class="sxs-lookup"><span data-stu-id="da9c0-133">No</span></span> |
| <span data-ttu-id="da9c0-134">outputs</span><span class="sxs-lookup"><span data-stu-id="da9c0-134">outputs</span></span> |<span data-ttu-id="da9c0-135">Una o más salidas producidos por hello actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="da9c0-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="da9c0-136">Sí</span><span class="sxs-lookup"><span data-stu-id="da9c0-136">Yes</span></span> |
| <span data-ttu-id="da9c0-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="da9c0-137">linkedServiceName</span></span> |<span data-ttu-id="da9c0-138">Clúster de HDInsight de referencia toohello registrado como un servicio vinculado de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="da9c0-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="da9c0-139">Sí</span><span class="sxs-lookup"><span data-stu-id="da9c0-139">Yes</span></span> |
| <span data-ttu-id="da9c0-140">script</span><span class="sxs-lookup"><span data-stu-id="da9c0-140">script</span></span> |<span data-ttu-id="da9c0-141">Especifique el script de Pig de hello en línea</span><span class="sxs-lookup"><span data-stu-id="da9c0-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="da9c0-142">No</span><span class="sxs-lookup"><span data-stu-id="da9c0-142">No</span></span> |
| <span data-ttu-id="da9c0-143">ruta de acceso de script</span><span class="sxs-lookup"><span data-stu-id="da9c0-143">script path</span></span> |<span data-ttu-id="da9c0-144">Almacenar el script de Pig hello en el almacenamiento de blobs de Azure y proporcionar Hola ruta toohello al archivo.</span><span class="sxs-lookup"><span data-stu-id="da9c0-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="da9c0-145">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="da9c0-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="da9c0-146">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="da9c0-146">Both cannot be used together.</span></span> <span data-ttu-id="da9c0-147">nombre de archivo de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="da9c0-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="da9c0-148">No</span><span class="sxs-lookup"><span data-stu-id="da9c0-148">No</span></span> |
| <span data-ttu-id="da9c0-149">define los campos</span><span class="sxs-lookup"><span data-stu-id="da9c0-149">defines</span></span> |<span data-ttu-id="da9c0-150">Especificar parámetros como pares clave/valor para hacer referencia a dentro de hello script de Pig</span><span class="sxs-lookup"><span data-stu-id="da9c0-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="da9c0-151">No</span><span class="sxs-lookup"><span data-stu-id="da9c0-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="da9c0-152">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="da9c0-152">Example</span></span>
<span data-ttu-id="da9c0-153">Veamos un ejemplo de juego registra análisis donde desea tooidentify Hola tiempo reproductores jugar iniciadas por su empresa.</span><span class="sxs-lookup"><span data-stu-id="da9c0-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="da9c0-154">Hola siguiente muestra de registro de juego es un archivo de separados por comas (,).</span><span class="sxs-lookup"><span data-stu-id="da9c0-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="da9c0-155">Contiene Hola siguientes campos: identificador de perfil, SessionStart, duración, SrcIPAddress y GameType.</span><span class="sxs-lookup"><span data-stu-id="da9c0-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="da9c0-156">Hola **script de Pig** tooprocess estos datos:</span><span class="sxs-lookup"><span data-stu-id="da9c0-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="da9c0-157">Hola tooexecute este Pig script en una canalización de factoría de datos, siga los pasos:</span><span class="sxs-lookup"><span data-stu-id="da9c0-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="da9c0-158">Crear un servicio vinculado tooregister [su propio HDInsight clústerde](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurar [clúster de cálculo de HDInsight a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="da9c0-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="da9c0-159">Llamaremos a este servicio vinculado **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="da9c0-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="da9c0-160">Crear un [servicio vinculado](data-factory-azure-blob-connector.md) almacenamiento de blobs de tooAzure en conexión de tooconfigure Hola hospeda los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="da9c0-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="da9c0-161">Llamaremos a este servicio vinculado **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="da9c0-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="da9c0-162">Crear [conjuntos de datos](data-factory-create-datasets.md) que apunta hello y toohello entrada los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="da9c0-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="da9c0-163">Vamos a llamar a conjunto de datos de entrada de hello **PigSampleIn** y conjunto de datos de salida de hello **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="da9c0-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="da9c0-164">Copiar consulta de Pig de hello en un almacenamiento de blobs de Azure configurado en el paso 2 de # Hola de archivo.</span><span class="sxs-lookup"><span data-stu-id="da9c0-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="da9c0-165">Si almacenamiento de Azure que hospeda datos Hola Hola es diferente de hello uno que hospeda el archivo de consulta de hello, crear un servicio vinculado de almacenamiento de Azure independiente.</span><span class="sxs-lookup"><span data-stu-id="da9c0-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="da9c0-166">Consulte servicio toohello vinculado en la configuración de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="da9c0-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="da9c0-167">Use ** scriptPath ** archivo de script de toospecify Hola ruta de acceso toopig y **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="da9c0-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="da9c0-168">También puede proporcionar Hola Pig script en línea en la definición de actividad de hello mediante hello **script** propiedad.</span><span class="sxs-lookup"><span data-stu-id="da9c0-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="da9c0-169">Sin embargo, no se recomienda este enfoque como todos los caracteres especiales en el script de Hola necesita toobe caracteres de escape y puede provocar problemas de depuración.</span><span class="sxs-lookup"><span data-stu-id="da9c0-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="da9c0-170">práctica recomendada de Hello es toofollow paso #4.</span><span class="sxs-lookup"><span data-stu-id="da9c0-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="da9c0-171">Crear canalización Hola con hello HDInsightPig actividad.</span><span class="sxs-lookup"><span data-stu-id="da9c0-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="da9c0-172">Esta actividad procesa los datos de entrada de hello mediante la ejecución de script de Pig en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="da9c0-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="da9c0-173">Implementar la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="da9c0-173">Deploy hello pipeline.</span></span> <span data-ttu-id="da9c0-174">Consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="da9c0-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="da9c0-175">Supervisar la canalización de hello mediante la supervisión de la factoría de datos de Hola y vistas de administración.</span><span class="sxs-lookup"><span data-stu-id="da9c0-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="da9c0-176">Consulte el artículo [Supervisión y administración de las canalizaciones de Factoría de datos](data-factory-monitor-manage-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="da9c0-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="da9c0-177">Especificación de parámetros para un script de Pig</span><span class="sxs-lookup"><span data-stu-id="da9c0-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="da9c0-178">Considere el siguiente ejemplo de Hola: registros de juegos se ingestión diariamente en el almacenamiento de blobs de Azure y se almacenan en una carpeta fecha según con particiones y la hora.</span><span class="sxs-lookup"><span data-stu-id="da9c0-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="da9c0-179">Desea que el script de Pig hello tooparameterize y pasa la ubicación de la carpeta de entrada de hello dinámicamente en tiempo de ejecución y también generar salida de hello particionado con la fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="da9c0-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="da9c0-180">toouse parámetros de script de Pig, realice Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="da9c0-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="da9c0-181">Definir los parámetros de hello en **define**.</span><span class="sxs-lookup"><span data-stu-id="da9c0-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="da9c0-182">En el Script de Pig hello, consulte parámetros toohello mediante '**$parameterName**' como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="da9c0-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="da9c0-183">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="da9c0-183">See Also</span></span>
* [<span data-ttu-id="da9c0-184">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="da9c0-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="da9c0-185">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="da9c0-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="da9c0-186">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="da9c0-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="da9c0-187">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="da9c0-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="da9c0-188">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="da9c0-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

