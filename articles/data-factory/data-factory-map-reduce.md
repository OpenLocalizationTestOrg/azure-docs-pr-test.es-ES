---
title: "Invocar programa MapReduce desde la factoría de datos de Azure"
description: "Obtenga información sobre cómo procesar datos mediante la ejecución de programas MapReduce en un clúster de HDInsight de Azure desde una factoría de datos de Azure."
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
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="7e473-103">Invocar programas MapReduce desde la factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="7e473-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="7e473-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="7e473-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="7e473-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="7e473-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="7e473-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="7e473-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="7e473-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e473-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="7e473-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="7e473-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="7e473-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7e473-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="7e473-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7e473-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="7e473-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="7e473-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="7e473-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7e473-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="7e473-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="7e473-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="7e473-114">La actividad de MapReduce para HDInsight en una [canalización](data-factory-create-pipelines.md) de Data Factory ejecuta programas de MapReduce en un clúster de HDInsight basado en Windows/Linux [propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o en uno [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="7e473-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7e473-115">Este artículo se basa en el artículo sobre [actividades de transformación de datos](data-factory-data-transformation-activities.md) , que presenta información general de la transformación de datos y las actividades de transformación admitidas.</span><span class="sxs-lookup"><span data-stu-id="7e473-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="7e473-116">Si no está familiarizado con Azure Data Factory, lea [Introducción a Azure Data Factory](data-factory-introduction.md) y realice el tutorial de [compilación de la primera canalización de datos](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="7e473-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="7e473-117">Introducción</span><span class="sxs-lookup"><span data-stu-id="7e473-117">Introduction</span></span>
<span data-ttu-id="7e473-118">Una canalización en una factoría de datos de Azure procesa los datos de los servicios de almacenamiento vinculados mediante el uso de servicios de proceso vinculados.</span><span class="sxs-lookup"><span data-stu-id="7e473-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="7e473-119">Contiene una secuencia de actividades donde cada actividad realiza una operación de procesamiento específica.</span><span class="sxs-lookup"><span data-stu-id="7e473-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="7e473-120">En este artículo se describe el uso de la actividad MapReduce de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e473-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="7e473-121">Consulte [Pig](data-factory-pig-activity.md) y [Hive](data-factory-hive-activity.md) para obtener detalles sobre la ejecución de scripts de Pig/Hive en un clúster de HDInsight basado en Windows/Linux desde una canalización mediante actividades de Pig y Hive para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e473-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="7e473-122">JSON para la actividad MapReduce de HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e473-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="7e473-123">En la definición de JSON para la actividad de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7e473-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="7e473-124">Establezca el **tipo** de la **actividad** en **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7e473-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="7e473-125">Especifique el nombre de la clase para la propiedad **className** .</span><span class="sxs-lookup"><span data-stu-id="7e473-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="7e473-126">Especifique la ruta de acceso al archivo JAR incluyendo el nombre de archivo de la propiedad **jarFilePath** .</span><span class="sxs-lookup"><span data-stu-id="7e473-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="7e473-127">Especifique el servicio vinculado que hace referencia al almacenamiento de blobs de Azure que contiene el archivo JAR de la propiedad **jarLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="7e473-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="7e473-128">Especifique los argumentos para el programa de MapReduce en la sección **argumentos** .</span><span class="sxs-lookup"><span data-stu-id="7e473-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="7e473-129">En tiempo de ejecución, verá unos argumentos adicionales (por ejemplo, mapreduce.job.tags) desde el marco de trabajo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e473-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="7e473-130">Para diferenciar sus argumentos con los argumentos de MapReduce, considere el uso tanto de opción como valor como argumentos tal como se muestra en el siguiente ejemplo (-s, --input, --output etc., son opciones seguidas inmediatamente por sus valores).</span><span class="sxs-lookup"><span data-stu-id="7e473-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
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
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="7e473-131">Puede usar la actividad MapReduce de HDInsight para ejecutar cualquier archivo jar de MapReduce en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e473-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="7e473-132">En la siguiente definición de JSON de ejemplo de una canalización, la actividad de HDInsight se configura para ejecutar un archivo JAR de Mahout.</span><span class="sxs-lookup"><span data-stu-id="7e473-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="7e473-133">Ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="7e473-133">Sample on GitHub</span></span>
<span data-ttu-id="7e473-134">Puede descargar un ejemplo para usar la actividad MapReduce de HDInsight desde: [Ejemplos de factoría de datos en GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="7e473-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="7e473-135">Ejecutar el programa de recuento de palabras</span><span class="sxs-lookup"><span data-stu-id="7e473-135">Running the Word Count program</span></span>
<span data-ttu-id="7e473-136">La canalización de este ejemplo ejecuta el programa de asignación/reducción del recuento de palabras en el clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e473-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="7e473-137">Servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="7e473-137">Linked Services</span></span>
<span data-ttu-id="7e473-138">En primer lugar, cree un servicio vinculado para vincular el almacenamiento de Azure usado por el clúster de HDInsight de Azure con la Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e473-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="7e473-139">Si copia/pega el código siguiente, no olvide reemplazar el **nombre de la cuenta** y la **clave de la cuenta** por el nombre y la clave de su instancia de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7e473-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="7e473-140">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7e473-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="7e473-141">Servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="7e473-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="7e473-142">A continuación, cree un servicio vinculado para vincular el clúster de HDInsight de Azure con la Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e473-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="7e473-143">Si copia/pegar el código siguiente, reemplace el **nombre del clúster de HDInsight** por el nombre de su clúster de HDInsight y cambie los valores de nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="7e473-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="7e473-144">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="7e473-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="7e473-145">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="7e473-145">Output dataset</span></span>
<span data-ttu-id="7e473-146">La canalización de este ejemplo no toma ninguna entrada.</span><span class="sxs-lookup"><span data-stu-id="7e473-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="7e473-147">Deberá especificar un conjunto de datos de salida para la actividad MapReduce de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e473-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="7e473-148">Este conjunto de datos es simplemente un conjunto de datos ficticio que es necesario para la programación de la canalización.</span><span class="sxs-lookup"><span data-stu-id="7e473-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="7e473-149">Canalización</span><span class="sxs-lookup"><span data-stu-id="7e473-149">Pipeline</span></span>
<span data-ttu-id="7e473-150">La canalización de este ejemplo tiene solo una actividad de tipo: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e473-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="7e473-151">Algunas de las propiedades importantes en JSON son:</span><span class="sxs-lookup"><span data-stu-id="7e473-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="7e473-152">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7e473-152">Property</span></span> | <span data-ttu-id="7e473-153">Notas</span><span class="sxs-lookup"><span data-stu-id="7e473-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="7e473-154">type</span><span class="sxs-lookup"><span data-stu-id="7e473-154">type</span></span> |<span data-ttu-id="7e473-155">El tipo debe establecerse en **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="7e473-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="7e473-156">className</span><span class="sxs-lookup"><span data-stu-id="7e473-156">className</span></span> |<span data-ttu-id="7e473-157">El nombre de la clase es: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="7e473-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="7e473-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="7e473-158">jarFilePath</span></span> |<span data-ttu-id="7e473-159">Ruta de acceso al archivo .jar que contiene la clase anterior.</span><span class="sxs-lookup"><span data-stu-id="7e473-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="7e473-160">Si copia/pega el código siguiente, no olvide cambiar el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="7e473-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="7e473-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="7e473-161">jarLinkedService</span></span> |<span data-ttu-id="7e473-162">Servicio vinculado al Almacenamiento de Azure que contiene el archivo jar.</span><span class="sxs-lookup"><span data-stu-id="7e473-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="7e473-163">Este servicio vinculado hace referencia al almacenamiento asociado al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e473-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="7e473-164">argumentos</span><span class="sxs-lookup"><span data-stu-id="7e473-164">arguments</span></span> |<span data-ttu-id="7e473-165">El programa de recuento de palabras toma dos argumentos, una entrada y una salida.</span><span class="sxs-lookup"><span data-stu-id="7e473-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="7e473-166">El archivo de entrada es el archivo davinci.txt.</span><span class="sxs-lookup"><span data-stu-id="7e473-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="7e473-167">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="7e473-167">frequency/interval</span></span> |<span data-ttu-id="7e473-168">Los valores de estas propiedades coinciden con el conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="7e473-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="7e473-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7e473-169">linkedServiceName</span></span> |<span data-ttu-id="7e473-170">hace referencia al servicio vinculado a HDInsight creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7e473-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="7e473-171">Ejecutar programas Spark</span><span class="sxs-lookup"><span data-stu-id="7e473-171">Run Spark programs</span></span>
<span data-ttu-id="7e473-172">Puede usar la actividad MapReduce para ejecutar programas Spark en su clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7e473-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="7e473-173">Consulte [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) (Invocar programas Spark desde Data Factory de Azure) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="7e473-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="7e473-174">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7e473-174">See Also</span></span>
* [<span data-ttu-id="7e473-175">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="7e473-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="7e473-176">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="7e473-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="7e473-177">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e473-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="7e473-178">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="7e473-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="7e473-179">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="7e473-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

