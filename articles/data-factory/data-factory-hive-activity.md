---
title: "Transformación de datos mediante la actividad de Hive - Azure | Microsoft Docs"
description: "Aprenda cómo puede usar la actividad de Hive en Factoría de datos de Azure para ejecutar consultas de Hive en un clúster de HDInsight suyo propio o a petición."
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
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="adebd-103">Transformación de datos mediante la actividad de Hive en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="adebd-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="adebd-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="adebd-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="adebd-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="adebd-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="adebd-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="adebd-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="adebd-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="adebd-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="adebd-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="adebd-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="adebd-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="adebd-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="adebd-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="adebd-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="adebd-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="adebd-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="adebd-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="adebd-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="adebd-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="adebd-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="adebd-114">La actividad de Hive de HDInsight en una [canalización](data-factory-create-pipelines.md) de Data Factory ejecuta consultas de Hive en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) clúster de HDInsight o en uno [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) basado en Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="adebd-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="adebd-115">Este artículo se basa en el artículo sobre [actividades de transformación de datos](data-factory-data-transformation-activities.md) , que presenta información general de la transformación de datos y las actividades de transformación admitidas.</span><span class="sxs-lookup"><span data-stu-id="adebd-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="adebd-116">Si no está familiarizado con Azure Data Factory, lea [Introducción a Azure Data Factory](data-factory-introduction.md) y realice el tutorial de [compilación de la primera canalización de datos](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="adebd-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="adebd-117">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="adebd-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="adebd-118">Detalles de la sintaxis</span><span class="sxs-lookup"><span data-stu-id="adebd-118">Syntax details</span></span>
| <span data-ttu-id="adebd-119">Propiedad</span><span class="sxs-lookup"><span data-stu-id="adebd-119">Property</span></span> | <span data-ttu-id="adebd-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="adebd-120">Description</span></span> | <span data-ttu-id="adebd-121">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="adebd-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="adebd-122">name</span><span class="sxs-lookup"><span data-stu-id="adebd-122">name</span></span> |<span data-ttu-id="adebd-123">Nombre de la actividad</span><span class="sxs-lookup"><span data-stu-id="adebd-123">Name of the activity</span></span> |<span data-ttu-id="adebd-124">Sí</span><span class="sxs-lookup"><span data-stu-id="adebd-124">Yes</span></span> |
| <span data-ttu-id="adebd-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="adebd-125">description</span></span> |<span data-ttu-id="adebd-126">Texto que describe para qué se usa la actividad.</span><span class="sxs-lookup"><span data-stu-id="adebd-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="adebd-127">No</span><span class="sxs-lookup"><span data-stu-id="adebd-127">No</span></span> |
| <span data-ttu-id="adebd-128">type</span><span class="sxs-lookup"><span data-stu-id="adebd-128">type</span></span> |<span data-ttu-id="adebd-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="adebd-129">HDinsightHive</span></span> |<span data-ttu-id="adebd-130">Sí</span><span class="sxs-lookup"><span data-stu-id="adebd-130">Yes</span></span> |
| <span data-ttu-id="adebd-131">inputs</span><span class="sxs-lookup"><span data-stu-id="adebd-131">inputs</span></span> |<span data-ttu-id="adebd-132">Entradas consumidas por la actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="adebd-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="adebd-133">No</span><span class="sxs-lookup"><span data-stu-id="adebd-133">No</span></span> |
| <span data-ttu-id="adebd-134">outputs</span><span class="sxs-lookup"><span data-stu-id="adebd-134">outputs</span></span> |<span data-ttu-id="adebd-135">Salidas producidas por la actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="adebd-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="adebd-136">Sí</span><span class="sxs-lookup"><span data-stu-id="adebd-136">Yes</span></span> |
| <span data-ttu-id="adebd-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="adebd-137">linkedServiceName</span></span> |<span data-ttu-id="adebd-138">Referencia al clúster de HDInsight registrado como un servicio vinculado en la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="adebd-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="adebd-139">Sí</span><span class="sxs-lookup"><span data-stu-id="adebd-139">Yes</span></span> |
| <span data-ttu-id="adebd-140">script</span><span class="sxs-lookup"><span data-stu-id="adebd-140">script</span></span> |<span data-ttu-id="adebd-141">Especifica el script de Hive en línea</span><span class="sxs-lookup"><span data-stu-id="adebd-141">Specify the Hive script inline</span></span> |<span data-ttu-id="adebd-142">No</span><span class="sxs-lookup"><span data-stu-id="adebd-142">No</span></span> |
| <span data-ttu-id="adebd-143">script path</span><span class="sxs-lookup"><span data-stu-id="adebd-143">script path</span></span> |<span data-ttu-id="adebd-144">Almacena el script de Hive en un almacenamiento de blobs de Azure y proporciona la ruta de acceso al archivo.</span><span class="sxs-lookup"><span data-stu-id="adebd-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="adebd-145">Use la propiedad 'script' o 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="adebd-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="adebd-146">No se pueden usar las dos juntas.</span><span class="sxs-lookup"><span data-stu-id="adebd-146">Both cannot be used together.</span></span> <span data-ttu-id="adebd-147">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="adebd-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="adebd-148">No</span><span class="sxs-lookup"><span data-stu-id="adebd-148">No</span></span> |
| <span data-ttu-id="adebd-149">define los campos</span><span class="sxs-lookup"><span data-stu-id="adebd-149">defines</span></span> |<span data-ttu-id="adebd-150">Especifique parámetros como pares de clave y valor para referencia en el script de Hive con 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="adebd-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="adebd-151">No</span><span class="sxs-lookup"><span data-stu-id="adebd-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="adebd-152">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="adebd-152">Example</span></span>
<span data-ttu-id="adebd-153">Veamos un ejemplo de análisis de registros de juegos en el que desea identificar el tiempo dedicado por los usuarios a los juegos de su empresa.</span><span class="sxs-lookup"><span data-stu-id="adebd-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="adebd-154">El siguiente registro muestra un registro de juego de ejemplo, que está separado por comas (`,`) y que contiene los siguientes campos: ProfileID, SessionStart, Duration, SrcIPAddress y GameType.</span><span class="sxs-lookup"><span data-stu-id="adebd-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="adebd-155">El **script de Hive** para procesar estos datos tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="adebd-155">The **Hive script** to process this data:</span></span>

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

<span data-ttu-id="adebd-156">Para ejecutar este script de Hive en una canalización de Data Factory, necesita hacer lo siguiente</span><span class="sxs-lookup"><span data-stu-id="adebd-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="adebd-157">Crear un servicio vinculado para registrar [su propio clúster de proceso de HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurar un [clúster de proceso de HDInsight a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="adebd-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="adebd-158">Llamaremos a este servicio vinculado "HDInsightLinkedService".</span><span class="sxs-lookup"><span data-stu-id="adebd-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="adebd-159">Crear un [servicio vinculado](data-factory-azure-blob-connector.md) para configurar la conexión al almacenamiento de blobs de Azure que hospeda los datos.</span><span class="sxs-lookup"><span data-stu-id="adebd-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="adebd-160">Llamaremos a este servicio vinculado "StorageLinkedService"</span><span class="sxs-lookup"><span data-stu-id="adebd-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="adebd-161">Crear [conjuntos de datos](data-factory-create-datasets.md) que apuntan a los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="adebd-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="adebd-162">Llamaremos al conjunto de datos de entrada "HiveSampleIn" y al conjunto de datos de salida "HiveSampleOut"</span><span class="sxs-lookup"><span data-stu-id="adebd-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="adebd-163">Copiar la consulta de Hive como un archivo en Azure Blob Storage configurado en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="adebd-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="adebd-164">Si el almacenamiento para hospedar los datos es diferente al que hospeda este archivo de consulta, crear un servicio vinculado de Azure Storage independiente y hacer referencia a él en la actividad.</span><span class="sxs-lookup"><span data-stu-id="adebd-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="adebd-165">Use **scriptPath** para especificar la ruta de acceso al archivo de consulta de Hive y **scriptLinkedService** para especificar el almacenamiento de Azure que contiene el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="adebd-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="adebd-166">También puede proporcionar el script de Hive en línea en la definición de actividad mediante la propiedad **script** .</span><span class="sxs-lookup"><span data-stu-id="adebd-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="adebd-167">No se recomienda este enfoque si todos los caracteres especiales del script del documento JSON tienen que ser caracteres de escape y pueden provocar problemas de depuración.</span><span class="sxs-lookup"><span data-stu-id="adebd-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="adebd-168">La práctica recomendada es seguir el paso 4.</span><span class="sxs-lookup"><span data-stu-id="adebd-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="adebd-169">Cree una canalización con la actividad HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="adebd-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="adebd-170">La actividad de procesa y transforma los datos.</span><span class="sxs-lookup"><span data-stu-id="adebd-170">The activity processes/transforms the data.</span></span>

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
6. <span data-ttu-id="adebd-171">Implemente la canalización.</span><span class="sxs-lookup"><span data-stu-id="adebd-171">Deploy the pipeline.</span></span> <span data-ttu-id="adebd-172">Consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="adebd-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="adebd-173">Supervise la canalización mediante las vistas de supervisión y administración de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="adebd-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="adebd-174">Consulte el artículo [Supervisión y administración de las canalizaciones de Factoría de datos](data-factory-monitor-manage-pipelines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="adebd-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="adebd-175">Especificación de parámetros para un script de Hive</span><span class="sxs-lookup"><span data-stu-id="adebd-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="adebd-176">En este ejemplo, los registros de juegos se introducen diariamente en Azure Blob Storage y se almacenan en una carpeta dividida con fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="adebd-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="adebd-177">Desea parametrizar el script de Hive y pasar la ubicación de la carpeta de entrada dinámicamente en tiempo de ejecución y también generar la salida dividida con fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="adebd-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="adebd-178">Para usar scripts de Hive parametrizados, haga lo siguiente</span><span class="sxs-lookup"><span data-stu-id="adebd-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="adebd-179">Defina los parámetros en **defines**.</span><span class="sxs-lookup"><span data-stu-id="adebd-179">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="adebd-180">En el Script de Hive, consulte el parámetro mediante **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="adebd-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="adebd-181">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="adebd-181">See Also</span></span>
* [<span data-ttu-id="adebd-182">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="adebd-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="adebd-183">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="adebd-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="adebd-184">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="adebd-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="adebd-185">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="adebd-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="adebd-186">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="adebd-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

