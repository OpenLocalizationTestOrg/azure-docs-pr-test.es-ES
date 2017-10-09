---
title: 'datos de aaaTransform con actividad de Hive: Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo puede utilizar Hola actividad de Hive en un consultas de Hive de toorun de factoría de datos de Azure en un clúster de HDInsight en-petición/su propio."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="9658f-103">Transformación de datos mediante la actividad de Hive en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9658f-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9658f-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="9658f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="9658f-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="9658f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9658f-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="9658f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9658f-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="9658f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9658f-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="9658f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9658f-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9658f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9658f-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9658f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9658f-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="9658f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9658f-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9658f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9658f-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="9658f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="9658f-114">Hola actividad de HDInsight Hive en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta consultas de Hive en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) clúster de HDInsight basados en Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="9658f-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9658f-115">En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="9658f-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="9658f-116">Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="9658f-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="9658f-117">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="9658f-117">Syntax</span></span>

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
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
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a><span data-ttu-id="9658f-118">Detalles de la sintaxis</span><span class="sxs-lookup"><span data-stu-id="9658f-118">Syntax details</span></span>
| <span data-ttu-id="9658f-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9658f-119">Property</span></span> | <span data-ttu-id="9658f-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="9658f-120">Description</span></span> | <span data-ttu-id="9658f-121">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9658f-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9658f-122">name</span><span class="sxs-lookup"><span data-stu-id="9658f-122">name</span></span> |<span data-ttu-id="9658f-123">Nombre de actividad de Hola</span><span class="sxs-lookup"><span data-stu-id="9658f-123">Name of hello activity</span></span> |<span data-ttu-id="9658f-124">Sí</span><span class="sxs-lookup"><span data-stu-id="9658f-124">Yes</span></span> |
| <span data-ttu-id="9658f-125">description</span><span class="sxs-lookup"><span data-stu-id="9658f-125">description</span></span> |<span data-ttu-id="9658f-126">Texto que describe qué actividad Hola se usa para</span><span class="sxs-lookup"><span data-stu-id="9658f-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="9658f-127">No</span><span class="sxs-lookup"><span data-stu-id="9658f-127">No</span></span> |
| <span data-ttu-id="9658f-128">type</span><span class="sxs-lookup"><span data-stu-id="9658f-128">type</span></span> |<span data-ttu-id="9658f-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="9658f-129">HDinsightHive</span></span> |<span data-ttu-id="9658f-130">Sí</span><span class="sxs-lookup"><span data-stu-id="9658f-130">Yes</span></span> |
| <span data-ttu-id="9658f-131">inputs</span><span class="sxs-lookup"><span data-stu-id="9658f-131">inputs</span></span> |<span data-ttu-id="9658f-132">Entradas consumidos por la actividad de Hive hello</span><span class="sxs-lookup"><span data-stu-id="9658f-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="9658f-133">No</span><span class="sxs-lookup"><span data-stu-id="9658f-133">No</span></span> |
| <span data-ttu-id="9658f-134">outputs</span><span class="sxs-lookup"><span data-stu-id="9658f-134">outputs</span></span> |<span data-ttu-id="9658f-135">Resultados generados por la actividad de Hive hello</span><span class="sxs-lookup"><span data-stu-id="9658f-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="9658f-136">Sí</span><span class="sxs-lookup"><span data-stu-id="9658f-136">Yes</span></span> |
| <span data-ttu-id="9658f-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9658f-137">linkedServiceName</span></span> |<span data-ttu-id="9658f-138">Clúster de HDInsight de referencia toohello registrado como un servicio vinculado de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="9658f-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="9658f-139">Sí</span><span class="sxs-lookup"><span data-stu-id="9658f-139">Yes</span></span> |
| <span data-ttu-id="9658f-140">script</span><span class="sxs-lookup"><span data-stu-id="9658f-140">script</span></span> |<span data-ttu-id="9658f-141">Especifique el script de Hive de hello en línea</span><span class="sxs-lookup"><span data-stu-id="9658f-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="9658f-142">No</span><span class="sxs-lookup"><span data-stu-id="9658f-142">No</span></span> |
| <span data-ttu-id="9658f-143">ruta de acceso de script</span><span class="sxs-lookup"><span data-stu-id="9658f-143">script path</span></span> |<span data-ttu-id="9658f-144">Hola de almacén en el almacenamiento de blobs de Azure de script de Hive y proporcionar Hola ruta toohello al archivo.</span><span class="sxs-lookup"><span data-stu-id="9658f-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="9658f-145">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="9658f-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="9658f-146">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="9658f-146">Both cannot be used together.</span></span> <span data-ttu-id="9658f-147">nombre de archivo de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9658f-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="9658f-148">No</span><span class="sxs-lookup"><span data-stu-id="9658f-148">No</span></span> |
| <span data-ttu-id="9658f-149">define los campos</span><span class="sxs-lookup"><span data-stu-id="9658f-149">defines</span></span> |<span data-ttu-id="9658f-150">Especificar parámetros como pares clave/valor para hacer referencia a dentro de script de Hive hello mediante 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="9658f-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="9658f-151">No</span><span class="sxs-lookup"><span data-stu-id="9658f-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="9658f-152">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9658f-152">Example</span></span>
<span data-ttu-id="9658f-153">Veamos un ejemplo de juego registra análisis donde desea tooidentify Hola tiempo los usuarios jugar iniciadas por su empresa.</span><span class="sxs-lookup"><span data-stu-id="9658f-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="9658f-154">Hello siguiente es un ejemplo juego registro, que es la coma (`,`) separados y contiene los siguientes campos: identificador de perfil, SessionStart, duración, SrcIPAddress y GameType de Hola.</span><span class="sxs-lookup"><span data-stu-id="9658f-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="9658f-155">Hola **de script de Hive** tooprocess estos datos:</span><span class="sxs-lookup"><span data-stu-id="9658f-155">hello **Hive script** tooprocess this data:</span></span>

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

<span data-ttu-id="9658f-156">tooexecute secuencia de comandos de esta sección en una canalización de factoría de datos, necesita toodo Hola siguiente</span><span class="sxs-lookup"><span data-stu-id="9658f-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="9658f-157">Crear un servicio vinculado tooregister [su propio HDInsight clústerde](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurar [clúster de cálculo de HDInsight a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="9658f-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="9658f-158">Llamaremos a este servicio vinculado "HDInsightLinkedService".</span><span class="sxs-lookup"><span data-stu-id="9658f-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="9658f-159">Crear un [servicio vinculado](data-factory-azure-blob-connector.md) almacenamiento de blobs de tooAzure en conexión de tooconfigure Hola hospeda los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9658f-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="9658f-160">Llamaremos a este servicio vinculado "StorageLinkedService"</span><span class="sxs-lookup"><span data-stu-id="9658f-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="9658f-161">Crear [conjuntos de datos](data-factory-create-datasets.md) que apunta hello y toohello entrada los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="9658f-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="9658f-162">Vamos a Hola llamada "HiveSampleIn" del conjunto de datos de entrada y Hola "HiveSampleOut" del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="9658f-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="9658f-163">Copiar consulta de Hive Hola como un almacenamiento de blobs configurados en el paso 2 de # tooAzure de archivo.</span><span class="sxs-lookup"><span data-stu-id="9658f-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="9658f-164">Si almacenamiento Hola para hospedar datos hello es diferente de hello uno aloja este archivo de consulta, cree un servicio vinculado de almacenamiento de Azure independiente y consulte tooit en actividad hello.</span><span class="sxs-lookup"><span data-stu-id="9658f-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="9658f-165">Use ** scriptPath ** toospecify Hola ruta toohive consulta archivo y **scriptLinkedService** toospecify Hola almacenamiento de Azure que contiene el archivo de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="9658f-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9658f-166">También puede proporcionar Hola Hive script en línea en la definición de actividad de hello mediante hello **script** propiedad.</span><span class="sxs-lookup"><span data-stu-id="9658f-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="9658f-167">No se recomienda este enfoque como todos los caracteres especiales en el script de Hola en documento JSON de hello necesita toobe caracteres de escape y la posible causa problemas de depuración.</span><span class="sxs-lookup"><span data-stu-id="9658f-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="9658f-168">práctica recomendada de Hello es toofollow paso #4.</span><span class="sxs-lookup"><span data-stu-id="9658f-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="9658f-169">Crear una canalización con hello HDInsightHive actividad.</span><span class="sxs-lookup"><span data-stu-id="9658f-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="9658f-170">procesos de actividad Hello/transformaciones datos Hola.</span><span class="sxs-lookup"><span data-stu-id="9658f-170">hello activity processes/transforms hello data.</span></span>

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. <span data-ttu-id="9658f-171">Implementar la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9658f-171">Deploy hello pipeline.</span></span> <span data-ttu-id="9658f-172">Consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9658f-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="9658f-173">Supervisar la canalización de hello mediante la supervisión de la factoría de datos de Hola y vistas de administración.</span><span class="sxs-lookup"><span data-stu-id="9658f-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="9658f-174">Consulte el artículo [Supervisión y administración de las canalizaciones de Factoría de datos](data-factory-monitor-manage-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9658f-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="9658f-175">Especificación de parámetros para un script de Hive</span><span class="sxs-lookup"><span data-stu-id="9658f-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="9658f-176">En este ejemplo, los registros de juegos se introducen diariamente en Azure Blob Storage y se almacenan en una carpeta dividida con fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="9658f-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="9658f-177">Desea script de Hive tooparameterize hello y pasar la ubicación de la carpeta de entrada de hello dinámicamente en tiempo de ejecución y también generar salida de hello particionado con la fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="9658f-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="9658f-178">toouse parámetros de script de Hive, realice Hola después</span><span class="sxs-lookup"><span data-stu-id="9658f-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="9658f-179">Definir los parámetros de hello en **define**.</span><span class="sxs-lookup"><span data-stu-id="9658f-179">Define hello parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* <span data-ttu-id="9658f-180">Hola Script de Hive, consulte toohello parámetro con **${hiveconf: ParameterName}**.</span><span class="sxs-lookup"><span data-stu-id="9658f-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a><span data-ttu-id="9658f-181">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9658f-181">See Also</span></span>
* [<span data-ttu-id="9658f-182">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="9658f-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="9658f-183">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="9658f-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="9658f-184">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="9658f-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="9658f-185">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="9658f-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="9658f-186">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="9658f-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

