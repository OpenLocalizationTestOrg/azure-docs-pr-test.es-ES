---
title: las canalizaciones de datos predictivos aaaCreate con Data Factory de Azure | Documentos de Microsoft
description: "Describe cómo toocreate crear canalizaciones predictivas con factoría de datos de Azure y aprendizaje automático de Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="759e2-103">Creación de canalizaciones predictivas con Azure Machine Learning y Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="759e2-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="759e2-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="759e2-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="759e2-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="759e2-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="759e2-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="759e2-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="759e2-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="759e2-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="759e2-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="759e2-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="759e2-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="759e2-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="759e2-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="759e2-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="759e2-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="759e2-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="759e2-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="759e2-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="759e2-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="759e2-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="759e2-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="759e2-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="759e2-115">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="759e2-115">Azure Machine Learning</span></span>
<span data-ttu-id="759e2-116">[Aprendizaje automático de Azure](https://azure.microsoft.com/documentation/services/machine-learning/) permite toobuild, probar e implementar soluciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="759e2-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="759e2-117">Desde una perspectiva general, esto se realiza en tres pasos:</span><span class="sxs-lookup"><span data-stu-id="759e2-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="759e2-118">**Crear un experimento de entrenamiento**.</span><span class="sxs-lookup"><span data-stu-id="759e2-118">**Create a training experiment**.</span></span> <span data-ttu-id="759e2-119">Realice este paso mediante el uso de hello estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="759e2-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="759e2-120">estudio de aprendizaje automático de Hello es un entorno de desarrollo visual de colaboración que use tootrain y probar un modelo de análisis predictivos utilizando los datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="759e2-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="759e2-121">**Convertir experimento predictivo tooa**.</span><span class="sxs-lookup"><span data-stu-id="759e2-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="759e2-122">Una vez que el modelo se ha entrenado con datos existentes y está listo toouse se tooscore nuevos datos, preparar y simplificar el experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="759e2-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="759e2-123">**Implementarlo como un servicio web**.</span><span class="sxs-lookup"><span data-stu-id="759e2-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="759e2-124">Puede publicar el experimento de puntuación como un servicio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="759e2-125">Puede enviar tooyour modelo de datos a través de este extremo de servicio web y recibir predicciones de resultado para el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="759e2-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="759e2-126">Azure Data Factory</span></span>
<span data-ttu-id="759e2-127">Factoría de datos es un servicio de integración de datos en la nube que organiza y automatiza hello **movimiento** y **transformación** de datos.</span><span class="sxs-lookup"><span data-stu-id="759e2-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="759e2-128">Puede crear soluciones de integración de datos mediante Data Factory de Azure que pueden recopilar datos de varios almacenes de datos, transformar y procesar los datos de Hola y publicación de almacenes de datos de toohello de datos de resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="759e2-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="759e2-129">Servicio de factoría de datos permite toocreate las canalizaciones de datos que moverán y transforman datos y, a continuación, ejecuta canalizaciones de hello según una programación especificada (cada hora, diariamente, semanalmente, etcetera).</span><span class="sxs-lookup"><span data-stu-id="759e2-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="759e2-130">También proporciona las dependencias entre sus canalizaciones de datos y el linaje de Hola de visualizaciones enriquecidas toodisplay y supervisar todos sus canalizaciones de datos desde una única vista unificada tooeasily identificar con exactitud los problemas y las alertas de supervisión de la instalación.</span><span class="sxs-lookup"><span data-stu-id="759e2-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="759e2-131">Vea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y [crear su primera canalización](data-factory-build-your-first-pipeline.md) tooquickly artículos empezar a trabajar con hello servicio Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="759e2-132">Data Factory y Machine Learning juntos</span><span class="sxs-lookup"><span data-stu-id="759e2-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="759e2-133">Azure habilita la factoría de datos se tooeasily crear canalizaciones que usan un informe publicado [aprendizaje automático de Azure] [ azure-machine-learning] web service para realizar análisis predictivos.</span><span class="sxs-lookup"><span data-stu-id="759e2-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="759e2-134">Con hello **actividad de ejecución de lotes** en una canalización del generador de datos de Azure, puede invocar un predicciones de toomake de servicio de web de aprendizaje automático de Azure en los datos de hello en lote.</span><span class="sxs-lookup"><span data-stu-id="759e2-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="759e2-135">Vea [invocar un aprendizaje automático de Azure servicio web usando Hola actividad de ejecución de lotes](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="759e2-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="759e2-136">Con el tiempo, los modelos de predicción de hello en experimentos de puntuación de aprendizaje automático de Azure de hello necesitan toobe volver a entrenar con los nuevos conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="759e2-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="759e2-137">Puede volver a entrenar un modelo de aprendizaje automático de Azure desde una canalización de factoría de datos realizando Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="759e2-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="759e2-138">Publicar el experimento de entrenamiento de hello (experimento no predicción) como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="759e2-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="759e2-139">Realice este paso en estudio de aprendizaje automático de hello como lo hizo tooexpose predictivo experimento como un servicio web en el escenario anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="759e2-140">Usar Hola el servicio web de actividad de ejecución de lotes de aprendizaje automático de Azure tooinvoke Hola para experimento de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="759e2-141">Básicamente, puede usar tooinvoke de actividad de ejecución de lotes de aprendizaje automático de Azure Hola el servicio web de entrenamiento y la puntuación del servicio web.</span><span class="sxs-lookup"><span data-stu-id="759e2-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="759e2-142">Cuando termine con reciclaje, actualizar Hola la puntuación del servicio web (se expone como un servicio web predictivo experimento) con hello recién entrenado usando hello **actualizar recursos actividad de aprendizaje automático de Azure**.</span><span class="sxs-lookup"><span data-stu-id="759e2-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="759e2-143">Para obtener más información, consulte el artículo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Actualización de modelos mediante la actividad de recursos de actualización).</span><span class="sxs-lookup"><span data-stu-id="759e2-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="759e2-144">Invocación de un servicio web mediante la actividad de ejecución de lotes</span><span class="sxs-lookup"><span data-stu-id="759e2-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="759e2-145">Usar procesamiento y movimiento de datos de Data Factory de Azure tooorchestrate y, a continuación, realizar la ejecución por lotes mediante el aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="759e2-146">Estos son los pasos de nivel superior de hello:</span><span class="sxs-lookup"><span data-stu-id="759e2-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="759e2-147">Cree un servicio vinculado de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="759e2-148">Necesita Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="759e2-148">You need hello following values:</span></span>

   1. <span data-ttu-id="759e2-149">**URI de solicitud** para hello API de ejecución por lotes.</span><span class="sxs-lookup"><span data-stu-id="759e2-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="759e2-150">Puede encontrar Hola URI de solicitud, haga clic en hello **ejecución por lotes** vínculo en la página de servicios web de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="759e2-151">**Clave de API** para hello publica el servicio web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="759e2-152">Puede encontrar la clave de API de hello haciendo clic en el servicio web de Hola que haya publicado.</span><span class="sxs-lookup"><span data-stu-id="759e2-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="759e2-153">Hola de uso **AzureMLBatchExecution** actividad.</span><span class="sxs-lookup"><span data-stu-id="759e2-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Panel de aprendizaje automático](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI del lote](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="759e2-156">Escenario: Experimentos con Web service entradas/salidas que hacen referencia toodata en almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="759e2-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="759e2-157">En este escenario, Hola servicio Web de aprendizaje de máquina de Azure lleva a cabo predicciones mediante datos de un archivo en el almacenamiento de blobs de Azure y almacena los resultados de predicción de hello en el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="759e2-158">Hello JSON siguiente define una canalización de factoría de datos con una actividad AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="759e2-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="759e2-159">actividad Hello tiene el conjunto de datos de hello **DecisionTreeInputBlob** como entrada y **DecisionTreeResultBlob** como salida de hello.</span><span class="sxs-lookup"><span data-stu-id="759e2-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="759e2-160">Hola **DecisionTreeInputBlob** se pasa como un servicio web de entrada toohello por mediante hello **webServiceInput** propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="759e2-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="759e2-161">Hola **DecisionTreeResultBlob** se pasa como un servicio de Web de salida toohello por mediante hello **webServiceOutputs** propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="759e2-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="759e2-162">Si el servicio web de hello toma varias entradas, usar hello **webServiceInputs** propiedad en lugar de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="759e2-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="759e2-163">Vea hello [servicio Web requiere varias entradas](#web-service-requires-multiple-inputs) sección para obtener un ejemplo del uso de hello webServiceInputs propiedad.</span><span class="sxs-lookup"><span data-stu-id="759e2-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="759e2-164">Conjuntos de datos que se hace referencia mediante hello **webServiceInput**/**webServiceInputs** y **webServiceOutputs** propiedades (en  **typeProperties**) también deben incluirse en hello actividad **entradas** y **genera**.</span><span class="sxs-lookup"><span data-stu-id="759e2-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="759e2-165">En el experimento de Azure ML, la entrada del servicio web y los puertos de salida y parámetros globales tienen nombres predeterminados (input1 e input2) que se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="759e2-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="759e2-166">nombres de Hola que utilizar para webServiceInputs, webServiceOutputs y la configuración de globalParameters deben coincidir exactamente con nombres de hello en experimentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="759e2-167">Puede ver carga de solicitud de ejemplo de Hola en la página de Ayuda de ejecución de lotes de Hola para su asignación de aprendizaje automático de Azure extremo tooverify Hola esperado.</span><span class="sxs-lookup"><span data-stu-id="759e2-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="759e2-168">Solo entradas y salidas de hello AzureMLBatchExecution actividad pueden pasarse como parámetros toohello servicio Web.</span><span class="sxs-lookup"><span data-stu-id="759e2-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="759e2-169">Por ejemplo, en hello por encima del fragmento de JSON, DecisionTreeInputBlob es una entrada toohello AzureMLBatchExecution actividad, que se pasa como un servicio Web de entrada toohello a través del parámetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="759e2-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="759e2-170">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="759e2-170">Example</span></span>
<span data-ttu-id="759e2-171">Esta toohold de almacenamiento de Azure de ejemplo utiliza ambas Hola datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="759e2-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="759e2-172">Se recomienda que atraviesan hello [crear su primera canalización con factoría de datos] [ adf-build-1st-pipeline] tutorial antes de pasar a través de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="759e2-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="759e2-173">En este ejemplo, use artefactos de factoría de datos de toocreate de hello Editor de generador de datos (servicios vinculados, conjuntos de datos, canalización).</span><span class="sxs-lookup"><span data-stu-id="759e2-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="759e2-174">Cree un **servicio vinculado** para su instancia de **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="759e2-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="759e2-175">Si hello archivos de entrada y salida están en diferentes cuentas de almacenamiento, necesita dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="759e2-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="759e2-176">Este es un ejemplo de JSON:</span><span class="sxs-lookup"><span data-stu-id="759e2-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="759e2-177">Crear hello **entrada** Data Factory de Azure **conjunto de datos**.</span><span class="sxs-lookup"><span data-stu-id="759e2-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="759e2-178">A diferencia de otros conjuntos de datos de Data Factory, estos deben contener tanto los valores de **folderPath** como de **fileName**.</span><span class="sxs-lookup"><span data-stu-id="759e2-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="759e2-179">Puede usar particiones toocause cada tooprocess de ejecución (cada segmento de datos) de proceso por lotes o generar entrada único y archivos de salida.</span><span class="sxs-lookup"><span data-stu-id="759e2-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="759e2-180">Puede que necesite tooinclude algunos hello tootransform de actividad de nivel superior de entrada en formato de archivo CSV de Hola y lo coloca en la cuenta de almacenamiento de Hola para cada sector.</span><span class="sxs-lookup"><span data-stu-id="759e2-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="759e2-181">En ese caso, no incluiría hello **externo** y **externalData** configuración se muestra en hello después de ejemplo y su DecisionTreeInputBlob sería el conjunto de datos de salida de hello de una actividad diferente.</span><span class="sxs-lookup"><span data-stu-id="759e2-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    <span data-ttu-id="759e2-182">El archivo de entrada csv debe tener una fila de encabezado de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="759e2-183">Si usas hello **actividad de copia** toocreate o mover Hola csv en almacenamiento de blobs de hello, debe establecer propiedad de receptor de hello **blobWriterAddHeader** demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="759e2-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="759e2-184">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="759e2-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="759e2-185">Si el archivo csv de hello no tiene fila de encabezado de hello, puede ver Hola siguiente error: **produjo Error en actividad: Error al leer la cadena. Token inesperado: StartObject. Path '', line 1, position 1**.</span><span class="sxs-lookup"><span data-stu-id="759e2-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="759e2-186">Crear hello **salida** Data Factory de Azure **conjunto de datos**.</span><span class="sxs-lookup"><span data-stu-id="759e2-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="759e2-187">Este ejemplo utiliza particiones toocreate una ruta de acceso de salida único para cada ejecución del segmento.</span><span class="sxs-lookup"><span data-stu-id="759e2-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="759e2-188">Sin particiones hello, actividad hello reemplazaría archivo hello.</span><span class="sxs-lookup"><span data-stu-id="759e2-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="759e2-189">Crear un **servicio vinculado** de tipo: **AzureMLLinkedService**, que proporciona la clave de API de Hola y URL de ejecución por lotes del modelo.</span><span class="sxs-lookup"><span data-stu-id="759e2-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="759e2-190">Por último, cree una canalización que contenga una actividad **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="759e2-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="759e2-191">En tiempo de ejecución, canalización lleva a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="759e2-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="759e2-192">Obtiene la ubicación de Hola Hola del archivo de entrada de los conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="759e2-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="759e2-193">Invoca la ejecución por lotes de aprendizaje automático de Azure Hola API</span><span class="sxs-lookup"><span data-stu-id="759e2-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="759e2-194">Copias Hola blob de toohello de salida por lotes ejecución determinado del conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="759e2-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="759e2-195">La actividad AzureMLBatchExecution puede tener cero o más entradas y una o más salidas.</span><span class="sxs-lookup"><span data-stu-id="759e2-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="759e2-196">Las fechas y horas de inicio (**start**) y de finalización (**end**) deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="759e2-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="759e2-197">Por ejemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="759e2-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="759e2-198">Hola **final** tiempo es opcional.</span><span class="sxs-lookup"><span data-stu-id="759e2-198">hello **end** time is optional.</span></span> <span data-ttu-id="759e2-199">Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas.**"</span><span class="sxs-lookup"><span data-stu-id="759e2-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="759e2-200">canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.</span><span class="sxs-lookup"><span data-stu-id="759e2-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="759e2-201">Para obtener más información sobre las propiedades JSON, vea [Referencia de scripting JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="759e2-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="759e2-202">Especificar la entrada para la actividad de hello AzureMLBatchExecution es opcional.</span><span class="sxs-lookup"><span data-stu-id="759e2-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="759e2-203">Escenario: Experimentos con módulos de lector/escritor toorefer toodata en varios almacenamientos</span><span class="sxs-lookup"><span data-stu-id="759e2-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="759e2-204">Otro escenario común al crear experimentos de aprendizaje automático de Azure es toouse módulos de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="759e2-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="759e2-205">módulo de lector de Hello es datos tooload usado en un experimento y módulo de escritor de hello es toosave datos de experimentos.</span><span class="sxs-lookup"><span data-stu-id="759e2-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="759e2-206">Para obtener información sobre los módulos lector y escritor, consulte los temas [Lector](https://msdn.microsoft.com/library/azure/dn905997.aspx) y [Escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) en MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="759e2-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="759e2-207">Al utilizar los módulos de lector y escritor de hello, es recomendable toouse un parámetro del servicio Web para cada propiedad de estos módulos de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="759e2-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="759e2-208">Estos parámetros web le permiten valores de hello tooconfigure en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="759e2-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="759e2-209">Por ejemplo, podría crear un experimento con un módulo lector que usa una base de datos SQL de Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="759e2-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="759e2-210">Una vez implementado el servicio web de hello, desea que los consumidores de hello tooenable de hello web servicio toospecify otro servidor de SQL Azure denominada YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="759e2-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="759e2-211">Puede usar un tooallow de parámetro del servicio Web este toobe valor configurado.</span><span class="sxs-lookup"><span data-stu-id="759e2-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="759e2-212">Las entradas y salidas de servicio web son diferentes de los parámetros de servicio web.</span><span class="sxs-lookup"><span data-stu-id="759e2-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="759e2-213">En el primer escenario hello, ha visto cómo se pueden especificar una entrada y salida para un servicio Web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="759e2-214">En este escenario, pasar parámetros para un servicio Web que se corresponden tooproperties de módulos de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="759e2-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="759e2-215">Echemos un vistazo a un escenario de uso de parámetros de servicio web.</span><span class="sxs-lookup"><span data-stu-id="759e2-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="759e2-216">Tiene un servicio web de aprendizaje automático de Azure implementado que usa un tooread datos del módulo de lector de uno de los orígenes de datos de hello admitidos por el aprendizaje automático de Azure (por ejemplo: base de datos de SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="759e2-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="759e2-217">Una vez realizada la ejecución por lotes hello, se escriben los resultados de hello mediante un módulo de escritor (base de datos de SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="759e2-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="759e2-218">No tiene entradas de servicio web y las salidas se definen en los experimentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="759e2-219">En este caso, se recomienda que configurar parámetros del servicio web relevantes para los módulos de lector y escritor de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="759e2-220">Esta configuración permite a Hola lector/escritor toobe módulos configurada cuando se usa la actividad de hello AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="759e2-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="759e2-221">Especificar parámetros de servicio Web en hello **globalParameters** sección actividad hello JSON como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="759e2-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="759e2-222">También puede usar [funciones de factoría de datos](data-factory-functions-variables.md) para pasar valores de hello parámetros del servicio Web como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="759e2-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="759e2-223">parámetros de servicio Web de Hello distinguen mayúsculas de minúsculas, por lo que garantizar que los nombres de Hola que especifique en la actividad de Hola JSON coinciden con hello las expuestas por hello servicio Web.</span><span class="sxs-lookup"><span data-stu-id="759e2-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="759e2-224">Utiliza una tooread de módulo de lector datos de varios archivos en blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="759e2-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="759e2-225">La canalización de macrodatos con actividades como Pig y Hive puede generar uno o varios archivos de salida sin extensiones.</span><span class="sxs-lookup"><span data-stu-id="759e2-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="759e2-226">Por ejemplo, cuando se especifica una tabla de Hive externa, datos de hello para la tabla de Hive externo Hola pueden almacenarse en el almacenamiento de blobs de Azure con hello después 000000_0 de nombre.</span><span class="sxs-lookup"><span data-stu-id="759e2-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="759e2-227">También puede usar varios archivos de módulo de lector de hello en un experimento tooread y usarlos para las predicciones.</span><span class="sxs-lookup"><span data-stu-id="759e2-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="759e2-228">Cuando se usa el módulo de lector de hello en un experimento de aprendizaje automático de Azure, puede especificar el Blob de Azure como entrada.</span><span class="sxs-lookup"><span data-stu-id="759e2-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="759e2-229">archivos de Hola Hola almacenamiento de blobs de Azure pueden ser archivos de salida de hello (ejemplo: 000000_0) que se hayan producido por un script de Pig y Hive con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="759e2-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="759e2-230">Hello módulo de lector permite tooread archivos (con ninguna extensión) mediante la configuración de hello **toocontainer de ruta de acceso, directorio o blob**.</span><span class="sxs-lookup"><span data-stu-id="759e2-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="759e2-231">Hola **toocontainer de ruta de acceso** puntos toohello contenedor y **directorio/blob** señala toofolder que contiene archivos de hello como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="759e2-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="759e2-232">Hola asterisco es decir, \*) **especifica que todos los archivos en la carpeta de contenedor de Hola Hola (es decir, datos/aggregateddata/año = mes/2014-6 /\*)** se lee como parte del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Propiedades de Blob de Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="759e2-234">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="759e2-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="759e2-235">Canalización con la actividad AzureMLBatchExecution con parámetros de servicio web</span><span class="sxs-lookup"><span data-stu-id="759e2-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="759e2-236">Hola ejemplo JSON anterior:</span><span class="sxs-lookup"><span data-stu-id="759e2-236">In hello above JSON example:</span></span>

* <span data-ttu-id="759e2-237">Hola implementado Azure Machine Learning servicio Web utiliza un lector y un sistema de escritura módulo tooread/escribir datos de / tooan base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="759e2-238">Este servicio Web expone Hola cuatro parámetros siguientes: nombre del servidor, nombre de base de datos, nombre de cuenta de usuario de servidor y contraseña de cuenta de usuario de servidor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="759e2-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="759e2-239">Las fechas y horas de inicio (**start**) y de finalización (**end**) deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="759e2-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="759e2-240">Por ejemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="759e2-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="759e2-241">Hola **final** tiempo es opcional.</span><span class="sxs-lookup"><span data-stu-id="759e2-241">hello **end** time is optional.</span></span> <span data-ttu-id="759e2-242">Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas.**"</span><span class="sxs-lookup"><span data-stu-id="759e2-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="759e2-243">canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.</span><span class="sxs-lookup"><span data-stu-id="759e2-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="759e2-244">Para obtener más información sobre las propiedades JSON, vea [Referencia de scripting JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="759e2-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="759e2-245">Otros escenarios</span><span class="sxs-lookup"><span data-stu-id="759e2-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="759e2-246">El servicio web requiere varias entradas</span><span class="sxs-lookup"><span data-stu-id="759e2-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="759e2-247">Si el servicio web de hello toma varias entradas, usar hello **webServiceInputs** propiedad en lugar de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="759e2-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="759e2-248">Conjuntos de datos que se hace referencia mediante hello **webServiceInputs** también debe incluirse en hello actividad **entradas**.</span><span class="sxs-lookup"><span data-stu-id="759e2-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="759e2-249">En el experimento de Azure ML, la entrada del servicio web y los puertos de salida y parámetros globales tienen nombres predeterminados (input1 e input2) que se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="759e2-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="759e2-250">nombres de Hola que utilizar para webServiceInputs, webServiceOutputs y la configuración de globalParameters deben coincidir exactamente con nombres de hello en experimentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="759e2-251">Puede ver carga de solicitud de ejemplo de Hola en la página de Ayuda de ejecución de lotes de Hola para su asignación de aprendizaje automático de Azure extremo tooverify Hola esperado.</span><span class="sxs-lookup"><span data-stu-id="759e2-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="759e2-252">Servicio web no requiere una entrada</span><span class="sxs-lookup"><span data-stu-id="759e2-252">Web Service does not require an input</span></span>
<span data-ttu-id="759e2-253">Servicios de Azure ML lote ejecución web puede ser toorun usado en los flujos de trabajo, por ejemplo, R o scripts de Python, que no requieran ninguna entrada.</span><span class="sxs-lookup"><span data-stu-id="759e2-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="759e2-254">O bien, experimento Hola puede configurarse con un módulo de lector que no expone ningún GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="759e2-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="759e2-255">En ese caso, hello AzureMLBatchExecution actividad se puede configurar como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="759e2-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="759e2-256">Servicio web no requiere entrada/salida</span><span class="sxs-lookup"><span data-stu-id="759e2-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="759e2-257">servicio web de aprendizaje automático de Azure batch ejecución Hola podría no tener ningún resultado del servicio Web configurado.</span><span class="sxs-lookup"><span data-stu-id="759e2-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="759e2-258">En este ejemplo, no hay ninguna entrada o salida de servicio web ni tampoco hay configurado ningún GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="759e2-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="759e2-259">Sigue siendo una salida configurada en la propia actividad de hello, pero no se proporciona como un webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="759e2-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="759e2-260">Ejecuciones de actividad de hello solo cuando otras actividades han sido correctos y escritores y lectores de usos de servicio Web</span><span class="sxs-lookup"><span data-stu-id="759e2-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="759e2-261">Hello Azure ML web lector y escritor de módulos de servicio podrían ser toorun configurado con o sin ningún GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="759e2-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="759e2-262">Sin embargo, puede que desee tooembed servicio llama en una canalización que utiliza el servicio de Hola de tooinvoke de dependencias de conjunto de datos solo cuando se ha completado un procesamiento de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="759e2-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="759e2-263">También puede desencadenar otra acción una vez completada la ejecución por lotes Hola con este enfoque.</span><span class="sxs-lookup"><span data-stu-id="759e2-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="759e2-264">En ese caso, puede expresar las dependencias de hello mediante actividad entradas y salidas, sin asignar un nombre cualquiera de ellos como servicio Web entradas ni salidas.</span><span class="sxs-lookup"><span data-stu-id="759e2-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="759e2-265">Hola **impresiones** son:</span><span class="sxs-lookup"><span data-stu-id="759e2-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="759e2-266">Si el punto de conexión de experimento usa un webServiceInput: se representa mediante un conjunto de datos de blob y se incluye en entradas de actividad de Hola y propiedad de webServiceInput Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="759e2-267">En caso contrario, se omite la propiedad de webServiceInput Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="759e2-268">Si el punto de conexión de experimento usa webServiceOutput(s): se incluyen en salidas de la actividad de Hola y en la propiedad webServiceOutputs de Hola y se representan mediante conjuntos de datos de blob.</span><span class="sxs-lookup"><span data-stu-id="759e2-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="759e2-269">actividad Hello genera e webServiceOutputs se asignan por nombre de Hola de cada salida en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="759e2-270">En caso contrario, se omite la propiedad webServiceOutputs de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="759e2-271">Si el punto de conexión de experimento expone globalParameter(s), se facilita en la propiedad globalParameters de hello actividad como pares de clave, valor.</span><span class="sxs-lookup"><span data-stu-id="759e2-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="759e2-272">En caso contrario, se omite la propiedad globalParameters de Hola.</span><span class="sxs-lookup"><span data-stu-id="759e2-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="759e2-273">las claves de Hello distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="759e2-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="759e2-274">[Las funciones de factoría de datos Azure](data-factory-functions-variables.md) se puede utilizar en valores de hello.</span><span class="sxs-lookup"><span data-stu-id="759e2-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="759e2-275">Conjuntos de datos adicionales pueden incluirse en las propiedades de entradas y salidas de actividad de hello, sin que se hace referencia en hello actividad typeProperties.</span><span class="sxs-lookup"><span data-stu-id="759e2-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="759e2-276">Estos conjuntos de datos controlan la ejecución con las dependencias de segmento pero en caso contrario, se omiten por hello AzureMLBatchExecution actividad.</span><span class="sxs-lookup"><span data-stu-id="759e2-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="759e2-277">Actualización de modelos mediante la actividad de recursos de actualización</span><span class="sxs-lookup"><span data-stu-id="759e2-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="759e2-278">Cuando termine con reciclaje, actualizar Hola la puntuación del servicio web (se expone como un servicio web predictivo experimento) con hello recién entrenado usando hello **actualizar recursos actividad de aprendizaje automático de Azure**.</span><span class="sxs-lookup"><span data-stu-id="759e2-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="759e2-279">Para obtener más información, consulte el artículo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Actualización de modelos mediante la actividad de recursos de actualización).</span><span class="sxs-lookup"><span data-stu-id="759e2-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="759e2-280">Módulos Lector y Escritor</span><span class="sxs-lookup"><span data-stu-id="759e2-280">Reader and Writer Modules</span></span>
<span data-ttu-id="759e2-281">Un escenario común para utilizar parámetros de servicio Web es usar Hola de Azure SQL lectores y escritores.</span><span class="sxs-lookup"><span data-stu-id="759e2-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="759e2-282">módulo de lector de Hello es datos tooload usado en un experimento desde los servicios de administración de datos fuera de estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="759e2-283">módulo de escritor de Hello es toosave datos de experimentos en servicios de administración de datos fuera de estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="759e2-284">Para obtener información acerca del lector o escritor de SQL/blob de Azure, consulte los temas [Lector ](https://msdn.microsoft.com/library/azure/dn905997.aspx)y [Escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) en MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="759e2-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="759e2-285">ejemplo de Hola en la sección anterior de hello usa hello Azure Blob lector y el escritor de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="759e2-286">En esta sección se trata el uso del lector SQL Azure y el escritor SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="759e2-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="759e2-287">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="759e2-287">Frequently asked questions</span></span>
<span data-ttu-id="759e2-288">**P:** Tengo varios archivos generados por medio de mis canalizaciones de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="759e2-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="759e2-289">¿Puedo usar hello AzureMLBatchExecution actividad toowork en todos los archivos de hello?</span><span class="sxs-lookup"><span data-stu-id="759e2-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="759e2-290">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="759e2-290">**A:** Yes.</span></span> <span data-ttu-id="759e2-291">Vea hello **utiliza una tooread de módulo de lector datos de varios archivos en blobs de Azure** sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="759e2-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="759e2-292">Actividad de puntuación de lotes de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="759e2-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="759e2-293">Si usas hello **AzureMLBatchScoring** toointegrate de actividad con aprendizaje automático de Azure, se recomienda que realice hello más reciente **AzureMLBatchExecution** actividad.</span><span class="sxs-lookup"><span data-stu-id="759e2-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="759e2-294">Hola AzureMLBatchExecution actividad se introdujo en hello lanzamiento de agosto de 2015 de SDK de Azure y Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="759e2-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="759e2-295">Si desea que toocontinue mediante la actividad de AzureMLBatchScoring hello, seguir leyendo a través de esta sección.</span><span class="sxs-lookup"><span data-stu-id="759e2-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="759e2-296">Actividad de puntuación de lotes de Aprendizaje automático de Azure con Almacenamiento de Azure para entrada/salida</span><span class="sxs-lookup"><span data-stu-id="759e2-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="759e2-297">Parámetros de servicio web</span><span class="sxs-lookup"><span data-stu-id="759e2-297">Web Service Parameters</span></span>
<span data-ttu-id="759e2-298">toospecify valores para los parámetros de servicio Web, agregue un **typeProperties** sección toohello **AzureMLBatchScoringActivty** sección en JSON como se muestra en el siguiente ejemplo de Hola de la canalización de hello:</span><span class="sxs-lookup"><span data-stu-id="759e2-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="759e2-299">También puede usar [funciones de factoría de datos](data-factory-functions-variables.md) para pasar valores de hello parámetros del servicio Web como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="759e2-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="759e2-300">parámetros de servicio Web de Hello distinguen mayúsculas de minúsculas, por lo que garantizar que los nombres de Hola que especifique en la actividad de Hola JSON coinciden con hello las expuestas por hello servicio Web.</span><span class="sxs-lookup"><span data-stu-id="759e2-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="759e2-301">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="759e2-301">See Also</span></span>
* [<span data-ttu-id="759e2-302">Entrada de blog de Azure: Introducción a la factoría de datos de Azure y al Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="759e2-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
