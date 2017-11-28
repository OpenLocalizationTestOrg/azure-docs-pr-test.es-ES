---
title: "Transformación de datos mediante Hadoop Streaming Activity - Azure | Microsoft Docs"
description: "Aprenda cómo puede usar Hadoop Streaming Activity en Azure Data Factory para transformar datos mediante la ejecución de programas de Hadoop Streaming en un clúster de HDInsight propio o a petición."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="6ef49-103">Transformación de datos mediante Hadoop Streaming Activity en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6ef49-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="6ef49-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="6ef49-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="6ef49-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="6ef49-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="6ef49-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="6ef49-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="6ef49-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="6ef49-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="6ef49-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="6ef49-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="6ef49-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6ef49-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="6ef49-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6ef49-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="6ef49-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="6ef49-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="6ef49-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6ef49-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="6ef49-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="6ef49-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="6ef49-114">Puede usar la actividad HDInsightStreamingActivity para invocar un trabajo de streaming de Hadoop desde una canalización de Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ef49-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="6ef49-115">El siguiente fragmento de código JSON muestra la sintaxis para usar HDInsightStreamingActivity en un archivo JSON de canalización.</span><span class="sxs-lookup"><span data-stu-id="6ef49-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="6ef49-116">La actividad de streaming de HDInsight en una [canalización](data-factory-create-pipelines.md) de Data Factory ejecuta programas de streaming de Hadoop en un clúster de HDInsight basado en Windows/Linux [propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o en uno [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="6ef49-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6ef49-117">Este artículo se basa en el artículo sobre [actividades de transformación de datos](data-factory-data-transformation-activities.md) , que presenta información general de la transformación de datos y las actividades de transformación admitidas.</span><span class="sxs-lookup"><span data-stu-id="6ef49-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="6ef49-118">Si no está familiarizado con Azure Data Factory, lea [Introducción a Azure Data Factory](data-factory-introduction.md) y realice el tutorial de [compilación de la primera canalización de datos](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="6ef49-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="6ef49-119">Ejemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="6ef49-119">JSON sample</span></span>
<span data-ttu-id="6ef49-120">El clúster de HDInsight se rellena automáticamente con los programas de ejemplo (wc.exe y cat.exe) y los datos (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="6ef49-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="6ef49-121">De forma predeterminada, el nombre del contenedor usado por el clúster de HDInsight es el nombre del propio clúster.</span><span class="sxs-lookup"><span data-stu-id="6ef49-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="6ef49-122">Por ejemplo, si el nombre del clúster es myhdicluster, el nombre del contenedor de blobs asociado sería myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="6ef49-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

<span data-ttu-id="6ef49-123">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="6ef49-123">Note the following points:</span></span>

1. <span data-ttu-id="6ef49-124">Establezca **linkedServiceName** en el nombre del servicio vinculado que apunta al clúster de HDInsight en el que se va a ejecutar el trabajo de MapReduce de streaming.</span><span class="sxs-lookup"><span data-stu-id="6ef49-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="6ef49-125">Establezca el tipo de la actividad en **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="6ef49-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="6ef49-126">Para la propiedad **mapper** , especifique el nombre del ejecutable del asignador.</span><span class="sxs-lookup"><span data-stu-id="6ef49-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="6ef49-127">En el ejemplo, cat.exe es el ejecutable del asignador.</span><span class="sxs-lookup"><span data-stu-id="6ef49-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="6ef49-128">Para la propiedad **reducer** , especifique el nombre del ejecutable del reductor.</span><span class="sxs-lookup"><span data-stu-id="6ef49-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="6ef49-129">En el ejemplo, wc.exe es el ejecutable del reductor.</span><span class="sxs-lookup"><span data-stu-id="6ef49-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="6ef49-130">Para la propiedad **input** type, especifique el archivo de entrada (incluida la ubicación) para el asignador.</span><span class="sxs-lookup"><span data-stu-id="6ef49-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="6ef49-131">En el ejemplo: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample es el contenedor de blobs, example/data/Gutenberg es la carpeta y davinci.txt es el blob.</span><span class="sxs-lookup"><span data-stu-id="6ef49-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="6ef49-132">Para la propiedad **output** type, especifique el archivo de salida (incluida la ubicación) para el reductor.</span><span class="sxs-lookup"><span data-stu-id="6ef49-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="6ef49-133">La salida del trabajo de streaming de Hadoop se escribirá en la ubicación especificada para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="6ef49-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="6ef49-134">En la sección **filePaths** , especifique las rutas de acceso para los archivos ejecutables del asignador y del reductor.</span><span class="sxs-lookup"><span data-stu-id="6ef49-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="6ef49-135">En el ejemplo: "adfsample/example/apps/wc.exe", adfsample es el contenedor de blobs, example/apps es la carpeta y wc.exe es el ejecutable.</span><span class="sxs-lookup"><span data-stu-id="6ef49-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="6ef49-136">Para la propiedad **fileLinkedService** , especifique el servicio vinculado de Almacenamiento de vinculados que representa el almacenamiento de Azure que contiene los archivos especificados en la sección filePaths.</span><span class="sxs-lookup"><span data-stu-id="6ef49-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="6ef49-137">Para la propiedad **arguments** , especifique los argumentos para el trabajo de streaming.</span><span class="sxs-lookup"><span data-stu-id="6ef49-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="6ef49-138">La propiedad **getDebugInfo** es un elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="6ef49-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="6ef49-139">Cuando se establece en Failure, los registros solo se descargan en caso de error.</span><span class="sxs-lookup"><span data-stu-id="6ef49-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="6ef49-140">Cuando se establece en Always, los registros se descargan siempre, sea cual sea el estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6ef49-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="6ef49-141">Como se muestra en el ejemplo, deberá especificar un conjunto de datos de salida para la actividad de streaming de Hadoop en la propiedad **outputs** .</span><span class="sxs-lookup"><span data-stu-id="6ef49-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="6ef49-142">Este conjunto de datos es simplemente un conjunto de datos ficticio que es necesario para la programación de la canalización.</span><span class="sxs-lookup"><span data-stu-id="6ef49-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="6ef49-143">No es necesario especificar ningún conjunto de datos de entrada para la actividad de la propiedad **inputs** .</span><span class="sxs-lookup"><span data-stu-id="6ef49-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="6ef49-144">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6ef49-144">Example</span></span>
<span data-ttu-id="6ef49-145">La canalización de este tutorial ejecuta el programa de asignación/reducción de transmisión por secuencias del recuento de palabras en el clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ef49-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="6ef49-146">Servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="6ef49-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="6ef49-147">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="6ef49-147">Azure Storage linked service</span></span>
<span data-ttu-id="6ef49-148">En primer lugar, cree un servicio vinculado para vincular el almacenamiento de Azure usado por el clúster de HDInsight de Azure con la Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ef49-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="6ef49-149">Si copia/pega el código siguiente, no olvide reemplazar el nombre y la clave de la cuenta por el nombre y la clave de su Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ef49-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="6ef49-150">Servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="6ef49-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="6ef49-151">A continuación, cree un servicio vinculado para vincular el clúster de HDInsight de Azure con la Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ef49-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="6ef49-152">Si copia/pegar el código siguiente, reemplace el nombre del clúster de HDInsight por el nombre de su clúster de HDInsight y cambie los valores de nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="6ef49-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="6ef49-153">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="6ef49-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="6ef49-154">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="6ef49-154">Output dataset</span></span>
<span data-ttu-id="6ef49-155">La canalización de este ejemplo no toma ninguna entrada.</span><span class="sxs-lookup"><span data-stu-id="6ef49-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="6ef49-156">Deberá especificar un conjunto de datos de salida para la actividad de streaming de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ef49-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="6ef49-157">Este conjunto de datos es simplemente un conjunto de datos ficticio que es necesario para la programación de la canalización.</span><span class="sxs-lookup"><span data-stu-id="6ef49-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="6ef49-158">Canalización</span><span class="sxs-lookup"><span data-stu-id="6ef49-158">Pipeline</span></span>
<span data-ttu-id="6ef49-159">La canalización de este ejemplo tiene solo una actividad de tipo: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="6ef49-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="6ef49-160">El clúster de HDInsight se rellena automáticamente con los programas de ejemplo (wc.exe y cat.exe) y los datos (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="6ef49-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="6ef49-161">De forma predeterminada, el nombre del contenedor usado por el clúster de HDInsight es el nombre del propio clúster.</span><span class="sxs-lookup"><span data-stu-id="6ef49-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="6ef49-162">Por ejemplo, si el nombre del clúster es myhdicluster, el nombre del contenedor de blobs asociado sería myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="6ef49-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a><span data-ttu-id="6ef49-163">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6ef49-163">See Also</span></span>
* [<span data-ttu-id="6ef49-164">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="6ef49-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="6ef49-165">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="6ef49-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="6ef49-166">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="6ef49-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="6ef49-167">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="6ef49-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="6ef49-168">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="6ef49-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

