---
title: datos de aaaTransform con Hadoop Streaming Activity - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede utilizar hello Hadoop Streaming Activity en un datos tootransform de factoría de datos de Azure mediante la ejecución de programas de Streaming de Hadoop en un clúster de HDInsight en-petición/su propio."
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
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="7e8b2-103">Transformación de datos mediante Hadoop Streaming Activity en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7e8b2-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="7e8b2-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="7e8b2-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="7e8b2-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="7e8b2-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="7e8b2-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="7e8b2-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="7e8b2-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e8b2-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="7e8b2-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="7e8b2-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="7e8b2-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7e8b2-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="7e8b2-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7e8b2-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="7e8b2-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="7e8b2-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="7e8b2-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7e8b2-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="7e8b2-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="7e8b2-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="7e8b2-114">Puede usar hello HDInsightStreamingActivity actividad invocar un trabajo de Streaming de Hadoop desde una canalización de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="7e8b2-115">Hello siguiente fragmento JSON muestra sintaxis de Hola para usar hello HDInsightStreamingActivity en un archivo de canalización JSON.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="7e8b2-116">Hola actividad de transmisión por secuencias de HDInsight en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta programas de Streaming de Hadoop en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight basados en Windows/Linux clúster.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7e8b2-117">En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="7e8b2-118">Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="7e8b2-119">Ejemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="7e8b2-119">JSON sample</span></span>
<span data-ttu-id="7e8b2-120">clúster de HDInsight de Hola se rellena automáticamente con los programas de ejemplo (wc.exe y cat.exe) y los datos (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="7e8b2-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="7e8b2-121">De forma predeterminada, nombre de contenedor de Hola que se usa por clúster de HDInsight de Hola es nombre de hello del propio clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="7e8b2-122">Por ejemplo, si el nombre de clúster es myhdicluster, nombre del contenedor de blob de hello asociado sería myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="7e8b2-123">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="7e8b2-123">Note hello following points:</span></span>

1. <span data-ttu-id="7e8b2-124">Conjunto hello **linkedServiceName** toohello nombre del saludo servicio vinculado que apunta el clúster de HDInsight tooyour en qué Hola streaming mapreduce se ejecuta el trabajo.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="7e8b2-125">Establecer tipo de Hola de actividad hello demasiado**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="7e8b2-126">Para hello **asignador** propiedad, especifique Hola nombre del ejecutable del asignador de.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="7e8b2-127">En el ejemplo de Hola, cat.exe es el asignador de hello ejecutable.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="7e8b2-128">Para hello **reductor** propiedad, especifique Hola nombre del ejecutable del reductor.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="7e8b2-129">En el ejemplo de Hola, wc.exe es reductor Hola ejecutable.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="7e8b2-130">Para hello **entrada** type (propiedad), especifique el archivo de entrada de hello (incluida la ubicación de hello) para el asignador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="7e8b2-131">En el ejemplo de Hola: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample es el contenedor de blob de hello, ejemplo/data/Gutenberg es la carpeta de Hola y davinci.txt es blob Hola.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="7e8b2-132">Para hello **salida** type (propiedad), especifique el archivo de salida de hello (incluida la ubicación de hello) para reductor Hola.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="7e8b2-133">salida de Hello de trabajo de Streaming de Hadoop de Hola se escribe ubicación toohello especificado para esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="7e8b2-134">Hola **filePaths** sección, especifique las rutas de acceso de Hola para los ejecutables de asignador y reductor Hola.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="7e8b2-135">En el ejemplo de Hola: "adfsample/example/apps/wc.exe", adfsample es el contenedor de blob de hello, example/apps es la carpeta de Hola y wc.exe es ejecutable hello.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="7e8b2-136">Para hello **fileLinkedService** propiedad, especifique Hola Hola de servicio vinculado que representa el almacenamiento de Azure que contiene archivos de hello especificados en la sección de hello filePaths el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="7e8b2-137">Para hello **argumentos** propiedad, especifique los argumentos de Hola para hello trabajo de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="7e8b2-138">Hola **getDebugInfo** propiedad es un elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="7e8b2-139">Cuando se establece tooFailure, registros de Hola se descargan solo en caso de error.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="7e8b2-140">Cuando se establece tooAlways, registros siempre se descargan independientemente del estado de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="7e8b2-141">Como se muestra en el ejemplo de Hola, especificar un conjunto de datos de salida de hello Hadoop Streaming Activity para hello **genera** propiedad.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="7e8b2-142">Este conjunto de datos es simplemente un dataset ficticio que es necesario toodrive Hola canalización programación.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="7e8b2-143">No es necesario ningún conjunto de datos de entrada de toospecify de actividad de Hola de hello **entradas** propiedad.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="7e8b2-144">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="7e8b2-144">Example</span></span>
<span data-ttu-id="7e8b2-145">canalización de Hello en este tutorial ejecuta el programa de asignación y reducción de transmisión por secuencias de hello contar palabras en el clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="7e8b2-146">Servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="7e8b2-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="7e8b2-147">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7e8b2-147">Azure Storage linked service</span></span>
<span data-ttu-id="7e8b2-148">En primer lugar, cree un Hola de toolink almacenamiento de Azure que se usa por factoría de datos de Azure de toohello de clúster de HDInsight de Azure de Hola de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="7e8b2-149">Si copiar y pegar los Hola siguiente código, no olvide tooreplace cuenta nombre y clave de cuenta con el nombre de Hola y la clave de su almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="7e8b2-150">Servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="7e8b2-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="7e8b2-151">A continuación, cree un servicio vinculado toolink su factoría de datos de Azure de toohello de clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="7e8b2-152">Si copiar y pegar los Hola después de código, reemplace el nombre del clúster de HDInsight por nombre de Hola de su clúster de HDInsight y cambiar los valores de nombre y la contraseña de usuario.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="7e8b2-153">CONJUNTOS DE DATOS</span><span class="sxs-lookup"><span data-stu-id="7e8b2-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="7e8b2-154">Conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="7e8b2-154">Output dataset</span></span>
<span data-ttu-id="7e8b2-155">canalización de Hello en este ejemplo no tiene ninguna entrada.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="7e8b2-156">Especifique un conjunto de datos de salida de hello actividad de transmisión por secuencias de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="7e8b2-157">Este conjunto de datos es simplemente un dataset ficticio que es necesario toodrive Hola canalización programación.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="7e8b2-158">Canalización</span><span class="sxs-lookup"><span data-stu-id="7e8b2-158">Pipeline</span></span>
<span data-ttu-id="7e8b2-159">canalización de Hello en este ejemplo tiene sólo una actividad que es de tipo: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="7e8b2-160">clúster de HDInsight de Hola se rellena automáticamente con los programas de ejemplo (wc.exe y cat.exe) y los datos (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="7e8b2-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="7e8b2-161">De forma predeterminada, nombre de contenedor de Hola que se usa por clúster de HDInsight de Hola es nombre de hello del propio clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="7e8b2-162">Por ejemplo, si el nombre de clúster es myhdicluster, nombre del contenedor de blob de hello asociado sería myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="7e8b2-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="7e8b2-163">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7e8b2-163">See Also</span></span>
* [<span data-ttu-id="7e8b2-164">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="7e8b2-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="7e8b2-165">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="7e8b2-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="7e8b2-166">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="7e8b2-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="7e8b2-167">Invocar programas Spark</span><span class="sxs-lookup"><span data-stu-id="7e8b2-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="7e8b2-168">Invocar scripts de R</span><span class="sxs-lookup"><span data-stu-id="7e8b2-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

