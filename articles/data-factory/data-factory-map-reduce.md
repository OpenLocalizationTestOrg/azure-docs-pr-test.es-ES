---
title: "aaaInvoke programa de MapReduce desde la factoría de datos de Azure"
description: "Obtenga información acerca de cómo agrupar tooprocess datos mediante la ejecución de programas de MapReduce en un HDInsight de Azure de un generador de datos de Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="843c9-103">Invocar programas MapReduce desde la factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="843c9-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="843c9-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="843c9-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="843c9-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="843c9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="843c9-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="843c9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="843c9-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="843c9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="843c9-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="843c9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="843c9-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="843c9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="843c9-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="843c9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="843c9-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="843c9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="843c9-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="843c9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="843c9-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="843c9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="843c9-114">Hola actividad de HDInsight MapReduce en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta programas MapReduce en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) clúster de HDInsight basados en Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="843c9-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="843c9-115">En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="843c9-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="843c9-116">Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="843c9-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="843c9-117">Introducción</span><span class="sxs-lookup"><span data-stu-id="843c9-117">Introduction</span></span>
<span data-ttu-id="843c9-118">Una canalización en una factoría de datos de Azure procesa los datos de los servicios de almacenamiento vinculados mediante el uso de servicios de proceso vinculados.</span><span class="sxs-lookup"><span data-stu-id="843c9-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="843c9-119">Contiene una secuencia de actividades donde cada actividad realiza una operación de procesamiento específica.</span><span class="sxs-lookup"><span data-stu-id="843c9-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="843c9-120">En este artículo se describe el uso de hello HDInsight MapReduce actividad.</span><span class="sxs-lookup"><span data-stu-id="843c9-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="843c9-121">Consulte [Pig](data-factory-pig-activity.md) y [Hive](data-factory-hive-activity.md) para obtener detalles sobre la ejecución de scripts de Pig/Hive en un clúster de HDInsight basado en Windows/Linux desde una canalización mediante actividades de Pig y Hive para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="843c9-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="843c9-122">JSON para la actividad MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="843c9-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="843c9-123">Hola definición de JSON para hello actividad de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="843c9-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="843c9-124">Conjunto hello **tipo** de hello **actividad** demasiado**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="843c9-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="843c9-125">Especificar nombre de Hola de clase de Hola para **className** propiedad.</span><span class="sxs-lookup"><span data-stu-id="843c9-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="843c9-126">Especificar Hola ruta de acceso toohello JAR archivo, incluido el nombre de archivo de Hola de **jarFilePath** propiedad.</span><span class="sxs-lookup"><span data-stu-id="843c9-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="843c9-127">Especifique el servicio de hello vinculado que hace referencia toohello almacenamiento de blobs de Azure que contiene el archivo JAR de hello para **jarLinkedService** propiedad.</span><span class="sxs-lookup"><span data-stu-id="843c9-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="843c9-128">Especifique los argumentos de programa de MapReduce Hola Hola **argumentos** sección.</span><span class="sxs-lookup"><span data-stu-id="843c9-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="843c9-129">En tiempo de ejecución, verá que algunos argumentos adicionales (por ejemplo: mapreduce.job.tags) de marco de trabajo de MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="843c9-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="843c9-130">toodifferentiate los argumentos con argumentos de MapReduce hello, considere el uso de opción y valor como argumentos tal como se muestra en el siguiente ejemplo de Hola (- s,--entrada,--salida etc., son opciones seguidos inmediatamente por sus valores).</span><span class="sxs-lookup"><span data-stu-id="843c9-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="843c9-131">Puede usar Hola actividad de HDInsight MapReduce toorun cualquier archivo jar de MapReduce en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="843c9-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="843c9-132">Hola siguiente definición de JSON de ejemplo de una canalización, Hola actividad de HDInsight está configurado toorun un archivo JAR Mahout.</span><span class="sxs-lookup"><span data-stu-id="843c9-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="843c9-133">Ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="843c9-133">Sample on GitHub</span></span>
<span data-ttu-id="843c9-134">Puede descargar un ejemplo para el uso de la actividad de HDInsight MapReduce Hola desde: [ejemplos de generador de datos en GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="843c9-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="843c9-135">Ejecutar programa de hello contar palabras</span><span class="sxs-lookup"><span data-stu-id="843c9-135">Running hello Word Count program</span></span>
<span data-ttu-id="843c9-136">canalización de Hello en este ejemplo ejecuta Hola programa de asignación y reducción del número de palabras en el clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="843c9-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="843c9-137">Servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="843c9-137">Linked Services</span></span>
<span data-ttu-id="843c9-138">En primer lugar, cree un Hola de toolink almacenamiento de Azure que se usa por factoría de datos de Azure de toohello de clúster de HDInsight de Azure de Hola de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="843c9-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="843c9-139">Si copiar y pegar los Hola siguiente código, no olvide tooreplace **nombre-cuenta** y **clave de cuenta** con nombre hello y la clave de su almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="843c9-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="843c9-140">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="843c9-140">Azure Storage linked service</span></span>

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="843c9-141">Servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="843c9-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="843c9-142">A continuación, cree un servicio vinculado toolink su factoría de datos de Azure de toohello de clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="843c9-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="843c9-143">Si copiar y pegar los Hola después de código, reemplace **el nombre del clúster de HDInsight** con nombre hello del clúster de HDInsight y cambiar valores de nombre y la contraseña de usuario.</span><span class="sxs-lookup"><span data-stu-id="843c9-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="843c9-144">CONJUNTOS DE DATOS</span><span class="sxs-lookup"><span data-stu-id="843c9-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="843c9-145">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="843c9-145">Output dataset</span></span>
<span data-ttu-id="843c9-146">canalización de Hello en este ejemplo no tiene ninguna entrada.</span><span class="sxs-lookup"><span data-stu-id="843c9-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="843c9-147">Especifique un conjunto de datos de salida para la actividad de HDInsight MapReduce Hola.</span><span class="sxs-lookup"><span data-stu-id="843c9-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="843c9-148">Este conjunto de datos es simplemente un dataset ficticio que es necesario toodrive Hola canalización programación.</span><span class="sxs-lookup"><span data-stu-id="843c9-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="843c9-149">Canalización</span><span class="sxs-lookup"><span data-stu-id="843c9-149">Pipeline</span></span>
<span data-ttu-id="843c9-150">canalización de Hello en este ejemplo tiene sólo una actividad que es de tipo: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="843c9-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="843c9-151">Algunas propiedades importantes de Hola Hola JSON son:</span><span class="sxs-lookup"><span data-stu-id="843c9-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="843c9-152">Propiedad</span><span class="sxs-lookup"><span data-stu-id="843c9-152">Property</span></span> | <span data-ttu-id="843c9-153">Notas</span><span class="sxs-lookup"><span data-stu-id="843c9-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="843c9-154">type</span><span class="sxs-lookup"><span data-stu-id="843c9-154">type</span></span> |<span data-ttu-id="843c9-155">se debe establecer el tipo de Hello demasiado**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="843c9-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="843c9-156">className</span><span class="sxs-lookup"><span data-stu-id="843c9-156">className</span></span> |<span data-ttu-id="843c9-157">Nombre de clase hello es: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="843c9-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="843c9-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="843c9-158">jarFilePath</span></span> |<span data-ttu-id="843c9-159">Archivo de ruta de acceso toohello jar que contiene la clase hello.</span><span class="sxs-lookup"><span data-stu-id="843c9-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="843c9-160">Si copiar y pegar los Hola siguiente código, no olvide toochange Hola nombre de hello clúster.</span><span class="sxs-lookup"><span data-stu-id="843c9-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="843c9-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="843c9-161">jarLinkedService</span></span> |<span data-ttu-id="843c9-162">Servicio vinculado de almacenamiento Azure que contiene el archivo jar de Hola.</span><span class="sxs-lookup"><span data-stu-id="843c9-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="843c9-163">Este servicio vinculado hace referencia a un almacenamiento toohello que está asociado con el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="843c9-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="843c9-164">argumentos</span><span class="sxs-lookup"><span data-stu-id="843c9-164">arguments</span></span> |<span data-ttu-id="843c9-165">programa de wordcount Hola toma dos argumentos, una entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="843c9-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="843c9-166">Hola entrada archivo es hello davinci.txt.</span><span class="sxs-lookup"><span data-stu-id="843c9-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="843c9-167">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="843c9-167">frequency/interval</span></span> |<span data-ttu-id="843c9-168">valores de Hello para estas propiedades coincidan con conjunto de datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="843c9-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="843c9-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="843c9-169">linkedServiceName</span></span> |<span data-ttu-id="843c9-170">hace una referencia de servicio vinculado de HDInsight de toohello había creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="843c9-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="843c9-171">Ejecutar programas Spark</span><span class="sxs-lookup"><span data-stu-id="843c9-171">Run Spark programs</span></span>
<span data-ttu-id="843c9-172">Puede usar programas de MapReduce actividad toorun Spark en el clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="843c9-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="843c9-173">Consulte [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) (Invocar programas Spark desde Data Factory de Azure) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="843c9-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="843c9-174">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="843c9-174">See Also</span></span>
* [<span data-ttu-id="843c9-175">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="843c9-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="843c9-176">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="843c9-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="843c9-177">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="843c9-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="843c9-178">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="843c9-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="843c9-179">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="843c9-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

