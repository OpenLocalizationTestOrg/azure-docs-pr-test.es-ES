---
title: "Creación de canalizaciones de datos predictivas con Azure Data Factory | Microsoft Docs"
description: "Describe cómo crear canalizaciones predictivas con Factoría de datos de Azure y Aprendizaje automático de Azure"
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
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="c80e0-103">Creación de canalizaciones predictivas con Azure Machine Learning y Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c80e0-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="c80e0-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="c80e0-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="c80e0-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="c80e0-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="c80e0-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="c80e0-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="c80e0-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="c80e0-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="c80e0-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="c80e0-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="c80e0-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c80e0-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="c80e0-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c80e0-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="c80e0-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="c80e0-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="c80e0-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c80e0-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="c80e0-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="c80e0-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="c80e0-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="c80e0-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="c80e0-115">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="c80e0-115">Azure Machine Learning</span></span>
<span data-ttu-id="c80e0-116">[Aprendizaje automático de Azure](https://azure.microsoft.com/documentation/services/machine-learning/) permite compilar, probar e implementar soluciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="c80e0-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="c80e0-117">Desde una perspectiva general, esto se realiza en tres pasos:</span><span class="sxs-lookup"><span data-stu-id="c80e0-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="c80e0-118">**Crear un experimento de entrenamiento**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-118">**Create a training experiment**.</span></span> <span data-ttu-id="c80e0-119">Este paso se lleva a cabo mediante Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c80e0-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="c80e0-120">ML Studio es un entorno de desarrollo visual de colaboración que se emplea para entrenar y probar un modelo de análisis predictivo con datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="c80e0-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="c80e0-121">**Convertirlo en un experimento predictivo**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="c80e0-122">Una vez que el modelo se ha entrenado con datos existentes y está listo para usarlo para puntuar nuevos datos, debe preparar y simplificar el experimento para la puntuación.</span><span class="sxs-lookup"><span data-stu-id="c80e0-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="c80e0-123">**Implementarlo como un servicio web**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="c80e0-124">Puede publicar el experimento de puntuación como un servicio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="c80e0-125">Los usuarios pueden enviar datos al modelo a través de este punto de conexión de servicio web y recibir las predicciones de resultado para el modelo.</span><span class="sxs-lookup"><span data-stu-id="c80e0-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="c80e0-126">Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="c80e0-126">Azure Data Factory</span></span>
<span data-ttu-id="c80e0-127">Data Factory es un servicio de integración de datos basado en la nube que organiza y automatiza el **movimiento** y la **transformación** de los datos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="c80e0-128">Con Azure Data Factory se pueden crear soluciones de integración de datos que pueden ingerir datos de distintos almacenes de datos, transformarlos y procesarlos, y publicar los datos resultantes en los almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="c80e0-129">El servicio Data Factory permite crear canalizaciones de datos que mueven y transforman datos y, después, ejecutar los procesos según una programación especificada (cada hora, diariamente, semanalmente, etc.).</span><span class="sxs-lookup"><span data-stu-id="c80e0-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="c80e0-130">También proporciona excelentes visualizaciones para mostrar el linaje y las dependencias entre las canalizaciones de datos y para poder supervisar todas las canalizaciones de datos desde una única vista unificada, con el fin de facilitar la identificación de los problemas y la configuración de alertas de supervisión.</span><span class="sxs-lookup"><span data-stu-id="c80e0-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="c80e0-131">Consulte los artículos [Introducción a Azure Data Factory](data-factory-introduction.md) y [Creación de la primera canalización de datos](data-factory-build-your-first-pipeline.md) para empezar a trabajar rápidamente con el servicio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c80e0-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="c80e0-132">Data Factory y Machine Learning juntos</span><span class="sxs-lookup"><span data-stu-id="c80e0-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="c80e0-133">Azure Data Factory permite crear fácilmente canalizaciones que utilizan un servicio web de [Azure Machine Learning][azure-machine-learning] publicado para realizar análisis predictivos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="c80e0-134">Mediante la **actividad de ejecución de lotes** en una canalización de Factoría de datos de Azure, puede invocar un servicio web de Aprendizaje automático de Azure para realizar predicciones sobre los datos en el lote.</span><span class="sxs-lookup"><span data-stu-id="c80e0-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="c80e0-135">Consulte la sección [Invocación de un servicio web de Aprendizaje automático de Azure mediante la actividad de ejecución de lotes](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="c80e0-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="c80e0-136">Pasado algún tiempo, los modelos predictivos en los experimentos de puntuación de Aprendizaje automático de Azure tienen que volver a entrenarse con nuevos conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c80e0-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="c80e0-137">Puede volver a entrenar un modelo de Aprendizaje automático de Azure de una canalización de Factoría de datos realizando los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c80e0-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="c80e0-138">Publicar el experimento de entrenamiento (experimento no predictivo) como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="c80e0-139">Tiene que llevar a cabo este paso en Azure Machine Learning Studio, tal como hizo para exponer el experimento predictivo como un servicio web en el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="c80e0-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="c80e0-140">Usar la actividad de ejecución de lotes de Aprendizaje automático de Azure para invocar el servicio web para el experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="c80e0-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="c80e0-141">Básicamente, puede emplear la actividad de ejecución de lotes de Aprendizaje automático de Azure para invocar el servicio web de aprendizaje y el servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="c80e0-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="c80e0-142">Cuando haya terminado el reciclaje, actualice el servicio web de puntuación (experimento predictivo expuesto como servicio web) con el modelo recién entrenado mediante la **actividad de recursos de actualización de Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="c80e0-143">Para obtener más información, consulte el artículo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Actualización de modelos mediante la actividad de recursos de actualización).</span><span class="sxs-lookup"><span data-stu-id="c80e0-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="c80e0-144">Invocación de un servicio web mediante la actividad de ejecución de lotes</span><span class="sxs-lookup"><span data-stu-id="c80e0-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="c80e0-145">Factoría de datos de Azure se usa para coordinar el procesamiento y el movimiento de datos y, posteriormente, realizar la ejecución por lotes mediante Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="c80e0-146">Estos son los pasos de nivel superior:</span><span class="sxs-lookup"><span data-stu-id="c80e0-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="c80e0-147">Cree un servicio vinculado de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="c80e0-148">Necesita los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c80e0-148">You need the following values:</span></span>

   1. <span data-ttu-id="c80e0-149">**URI de solicitud** para la API Ejecución de lotes.</span><span class="sxs-lookup"><span data-stu-id="c80e0-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="c80e0-150">Para encontrar el URI de solicitud, haga clic en el vínculo **EJECUCIÓN DE LOTES** en la página de servicios web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="c80e0-151">**Clave de API** para el servicio web de Aprendizaje automático de Azure publicado.</span><span class="sxs-lookup"><span data-stu-id="c80e0-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="c80e0-152">Para encontrar la clave de API, haga clic en el servicio web que ha publicado.</span><span class="sxs-lookup"><span data-stu-id="c80e0-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="c80e0-153">Use la actividad **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="c80e0-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Panel de aprendizaje automático](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI del lote](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="c80e0-156">Escenario: Experimentos mediante entradas y salidas de servicios web que hacen referencia a datos de Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="c80e0-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="c80e0-157">En este escenario, el servicio web de Aprendizaje automático de Azure realiza predicciones mediante datos de un archivo de un almacenamiento de blobs de Azure y almacena los resultados de predicción en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c80e0-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="c80e0-158">El siguiente JSON define una canalización de Data Factory con una actividad AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="c80e0-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="c80e0-159">La actividad tiene el conjunto de datos **DecisionTreeInputBlob** como entrada y **DecisionTreeResultBlob** como salida.</span><span class="sxs-lookup"><span data-stu-id="c80e0-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="c80e0-160">**DecisionTreeInputBlob** se pasa como entrada al servicio web mediante la propiedad JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="c80e0-161">**DecisionTreeResultBlob** se pasa como salida al servicio web mediante la propiedad JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c80e0-162">Si el servicio web toma varias entradas, use la propiedad **webServiceInputs** en lugar de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="c80e0-163">Consulte la sección [El servicio web requiere varias entradas](#web-service-requires-multiple-inputs) para ver un ejemplo de cómo usar la propiedad webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="c80e0-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="c80e0-164">Los conjuntos de datos a los que hacen referencia las propiedades **webServiceInput**/**webServiceInputs** y **webServiceOutputs** (en **typeProperties**) también se deben incluir en las **entradas** y las **salidas** de la actividad.</span><span class="sxs-lookup"><span data-stu-id="c80e0-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="c80e0-165">En el experimento de Azure ML, la entrada del servicio web y los puertos de salida y parámetros globales tienen nombres predeterminados (input1 e input2) que se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="c80e0-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="c80e0-166">Los nombres que se utilizan para la configuración de globalParameters, webServiceOutputs y webServiceInputs deben coincidir exactamente con los de los experimentos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="c80e0-167">Puede ver la carga útil de la solicitud de ejemplo en la página de ayuda de ejecución de lotes del punto de conexión de Azure ML para comprobar la asignación esperada.</span><span class="sxs-lookup"><span data-stu-id="c80e0-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
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
> <span data-ttu-id="c80e0-168">Solo las entradas y salidas de la actividad AzureMLBatchExecution pueden pasarse como parámetros al servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="c80e0-169">Por ejemplo, en el fragmento JSON anterior, DecisionTreeInputBlob es una entrada a la actividad AzureMLBatchExecution, que se pasa como entrada al servicio web mediante el parámetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="c80e0-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="c80e0-170">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c80e0-170">Example</span></span>
<span data-ttu-id="c80e0-171">Este ejemplo utiliza Almacenamiento de Azure para almacenar los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="c80e0-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="c80e0-172">Se recomienda que siga el tutorial [Compilación de la primera canalización con Data Factory][adf-build-1st-pipeline] antes de llevar a cabo este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c80e0-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="c80e0-173">Utilice el editor de Data Factory para crear artefactos de Data Factory (servicios vinculados, conjuntos de datos, canalización) en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c80e0-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="c80e0-174">Cree un **servicio vinculado** para su instancia de **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="c80e0-175">Si los archivos de entrada y salida están en diferentes cuentas de almacenamiento, necesita dos servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="c80e0-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="c80e0-176">Este es un ejemplo de JSON:</span><span class="sxs-lookup"><span data-stu-id="c80e0-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="c80e0-177">Cree el **conjunto de datos** de **entrada** de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c80e0-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="c80e0-178">A diferencia de otros conjuntos de datos de Data Factory, estos deben contener tanto los valores de **folderPath** como de **fileName**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="c80e0-179">Puede utilizar la creación de particiones para hacer que cada ejecución de lotes (cada segmento de datos) se procese o produzca archivos de entrada y salida únicos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="c80e0-180">Probablemente necesitará incluir alguna actividad ascendente para transformar la entrada en el formato de archivo CSV y colocarlo en la cuenta de almacenamiento para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="c80e0-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="c80e0-181">En ese caso, no incluiría la configuración de **external** y **externalData** que se muestra en el ejemplo siguiente, y su valor de DecisionTreeInputBlob sería el conjunto de datos de salida de una actividad diferente.</span><span class="sxs-lookup"><span data-stu-id="c80e0-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="c80e0-182">Su archivo CSV de entrada debe tener la fila de encabezado de columna.</span><span class="sxs-lookup"><span data-stu-id="c80e0-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="c80e0-183">Si está usando la **actividad de copia** para crear o mover el archivo CSV a Blob Storage, debe establecer la propiedad **blobWriterAddHeader** del receptor en **true**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="c80e0-184">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c80e0-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="c80e0-185">Si el archivo CSV no tiene la fila de encabezado, es posible que vea el siguiente error: **Error en actividad: error de lectura de la cadena. Token inesperado: StartObject. Path '', line 1, position 1**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="c80e0-186">Cree el **conjunto de datos** de **salida** de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c80e0-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="c80e0-187">En este ejemplo se usa la creación de particiones para crear una ruta de acceso de salida única para cada ejecución de segmento.</span><span class="sxs-lookup"><span data-stu-id="c80e0-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="c80e0-188">Sin la creación de particiones, la actividad sobrescribiría el archivo.</span><span class="sxs-lookup"><span data-stu-id="c80e0-188">Without the partitioning, the activity would overwrite the file.</span></span>

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
4. <span data-ttu-id="c80e0-189">Cree un **servicio vinculado** de tipo **AzureMLLinkedService**; para ello, proporcione la clave de API y la URL de ejecución de lotes.</span><span class="sxs-lookup"><span data-stu-id="c80e0-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="c80e0-190">Por último, cree una canalización que contenga una actividad **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="c80e0-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="c80e0-191">En tiempo de ejecución, la canalización lleva a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c80e0-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="c80e0-192">Obtiene la ubicación del archivo de entrada de los conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c80e0-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="c80e0-193">Invoca a la API de ejecución de lotes de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c80e0-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="c80e0-194">Copia el resultado de la ejecución por lotes en el blob proporcionado en el conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="c80e0-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c80e0-195">La actividad AzureMLBatchExecution puede tener cero o más entradas y una o más salidas.</span><span class="sxs-lookup"><span data-stu-id="c80e0-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="c80e0-196">Las fechas y horas de inicio (**start**) y de finalización (**end**) deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c80e0-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c80e0-197">Por ejemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c80e0-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="c80e0-198">La hora de la propiedad **end** es opcional.</span><span class="sxs-lookup"><span data-stu-id="c80e0-198">The **end** time is optional.</span></span> <span data-ttu-id="c80e0-199">Si no especifica ningún valor para la propiedad **end**, se calcula como "**start + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="c80e0-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="c80e0-200">Para ejecutar la canalización indefinidamente, especifique **9999-09-09** como valor de propiedad **end**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="c80e0-201">Para obtener más información sobre las propiedades JSON, vea [Referencia de scripting JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c80e0-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c80e0-202">La especificación de la entrada para la actividad AzureMLBatchExecution es opcional.</span><span class="sxs-lookup"><span data-stu-id="c80e0-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="c80e0-203">Escenario: Experimentos mediante módulos Lector y Escritor para hacer referencia a datos de varios almacenamientos</span><span class="sxs-lookup"><span data-stu-id="c80e0-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="c80e0-204">Otro escenario común al crear experimentos de Aprendizaje automático de Azure es usar módulos Lector y Escritor.</span><span class="sxs-lookup"><span data-stu-id="c80e0-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="c80e0-205">El módulo lector se usa para cargar datos en un experimento y el módulo escritor para guardar los datos de los experimentos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="c80e0-206">Para obtener información sobre los módulos lector y escritor, consulte los temas [Lector](https://msdn.microsoft.com/library/azure/dn905997.aspx) y [Escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) en MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="c80e0-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="c80e0-207">Al usar los módulos lector y escritor, es recomendable emplear un parámetro de servicio web para cada propiedad de estos módulos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="c80e0-208">Estos parámetros web permiten configurar los valores en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c80e0-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="c80e0-209">Por ejemplo, podría crear un experimento con un módulo lector que usa una base de datos SQL de Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c80e0-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="c80e0-210">Una vez implementado el servicio web, quiere habilitar los consumidores del servicio web con el fin de especificar otro servidor Azure SQL Server denominado YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c80e0-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="c80e0-211">Puede usar un parámetro de servicio web para permitir que se configure este valor.</span><span class="sxs-lookup"><span data-stu-id="c80e0-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="c80e0-212">Las entradas y salidas de servicio web son diferentes de los parámetros de servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="c80e0-213">En el primer escenario, ha visto cómo pueden especificarse una entrada y una salida para un servicio web de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="c80e0-214">En este escenario, se pasan parámetros para un servicio web que corresponden a las propiedades de los módulos lector y escritor.</span><span class="sxs-lookup"><span data-stu-id="c80e0-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="c80e0-215">Echemos un vistazo a un escenario de uso de parámetros de servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="c80e0-216">Tiene un servicio web implementado de Azure Machine Learning que usa un módulo lector para leer datos de uno de los orígenes de datos admitidos por Azure Machine Learning (por ejemplo: Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="c80e0-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="c80e0-217">Después de realizar la ejecución de lotes, los resultados se escriben con un módulo escritor (Base de datos SQL de Azure).</span><span class="sxs-lookup"><span data-stu-id="c80e0-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="c80e0-218">No hay entradas ni salidas de servicio web definidas en los experimentos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="c80e0-219">En este caso, se recomienda que configure los parámetros de servicio web pertinentes para los módulos lector y escritor.</span><span class="sxs-lookup"><span data-stu-id="c80e0-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="c80e0-220">De esta forma, se podrán configurar los módulos lector y escritor cuando se use la actividad AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="c80e0-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="c80e0-221">Los parámetros de servicio web se especifican en la sección **globalParameters** de la actividad JSON como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="c80e0-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="c80e0-222">También puede usar [Funciones de Factoría de datos](data-factory-functions-variables.md) para pasar valores para los parámetros de servicio web como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c80e0-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="c80e0-223">Los parámetros de servicio web distinguen entre mayúsculas y minúsculas para garantizar que los nombres que especifica en JSON de actividad coinciden con los que muestra el servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="c80e0-224">Uso de un módulo lector para leer datos de varios archivos de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="c80e0-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="c80e0-225">La canalización de macrodatos con actividades como Pig y Hive puede generar uno o varios archivos de salida sin extensiones.</span><span class="sxs-lookup"><span data-stu-id="c80e0-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="c80e0-226">Por ejemplo, cuando se especifica una tabla externa de Hive, los datos de dicha tabla se pueden almacenar en el almacenamiento de blobs de Azure con el siguiente nombre 000000_0.</span><span class="sxs-lookup"><span data-stu-id="c80e0-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="c80e0-227">Puede usar el módulo lector en un experimento para leer varios archivos y usarlos para realizar predicciones.</span><span class="sxs-lookup"><span data-stu-id="c80e0-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="c80e0-228">Al usar el módulo lector en un experimento de Aprendizaje automático de Azure, puede especificar Blob de Azure como entrada.</span><span class="sxs-lookup"><span data-stu-id="c80e0-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="c80e0-229">Los archivos en Blob Storage de Azure pueden ser los archivos de salida (por ejemplo, 000000_0) que se generan mediante un script de Pig y Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c80e0-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="c80e0-230">El módulo de lector permite leer archivos (sin extensiones) mediante la configuración de la propiedad **Path to container, directory/blob**(Ruta de acceso al contenedor, directorio o blob).</span><span class="sxs-lookup"><span data-stu-id="c80e0-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="c80e0-231">La **ruta de acceso al contenedor** apunta al contenedor y el **directorio o blob** apunta a la carpeta que contiene los archivos, tal y como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="c80e0-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="c80e0-232">Tenga en cuenta que el asterisco (\*) **especifica que todos los archivos de la carpeta o contenedor (es decir, data/aggregateddata/year=2014/month-6/\*)** se leen como parte del experimento.</span><span class="sxs-lookup"><span data-stu-id="c80e0-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Propiedades de Blob de Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="c80e0-234">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c80e0-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="c80e0-235">Canalización con la actividad AzureMLBatchExecution con parámetros de servicio web</span><span class="sxs-lookup"><span data-stu-id="c80e0-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="c80e0-236">En el ejemplo JSON anterior:</span><span class="sxs-lookup"><span data-stu-id="c80e0-236">In the above JSON example:</span></span>

* <span data-ttu-id="c80e0-237">El servicio web implementado de Aprendizaje automático de Azure usa un módulo lector y otro escritor para leer y escribir datos desde y hacia una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="c80e0-238">Este servicio web expone los cuatro parámetros siguientes: nombre de servidor de base de datos, nombre de base de datos, nombre de cuenta de usuario de servidor y contraseña de cuenta de usuario de servidor.</span><span class="sxs-lookup"><span data-stu-id="c80e0-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="c80e0-239">Las fechas y horas de inicio (**start**) y de finalización (**end**) deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c80e0-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c80e0-240">Por ejemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c80e0-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="c80e0-241">La hora de la propiedad **end** es opcional.</span><span class="sxs-lookup"><span data-stu-id="c80e0-241">The **end** time is optional.</span></span> <span data-ttu-id="c80e0-242">Si no especifica ningún valor para la propiedad **end**, se calcula como "**start + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="c80e0-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="c80e0-243">Para ejecutar la canalización indefinidamente, especifique **9999-09-09** como valor de propiedad **end**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="c80e0-244">Para obtener más información sobre las propiedades JSON, vea [Referencia de scripting JSON](https://msdn.microsoft.com/library/dn835050.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c80e0-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="c80e0-245">Otros escenarios</span><span class="sxs-lookup"><span data-stu-id="c80e0-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="c80e0-246">El servicio web requiere varias entradas</span><span class="sxs-lookup"><span data-stu-id="c80e0-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="c80e0-247">Si el servicio web toma varias entradas, use la propiedad **webServiceInputs** en lugar de usar **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="c80e0-248">Los conjuntos de datos a los que hace referencia **webServiceInputs** también deben incluirse en las **entradas** de la actividad.</span><span class="sxs-lookup"><span data-stu-id="c80e0-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="c80e0-249">En el experimento de Azure ML, la entrada del servicio web y los puertos de salida y parámetros globales tienen nombres predeterminados (input1 e input2) que se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="c80e0-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="c80e0-250">Los nombres que se utilizan para la configuración de globalParameters, webServiceOutputs y webServiceInputs deben coincidir exactamente con los de los experimentos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="c80e0-251">Puede ver la carga útil de la solicitud de ejemplo en la página de ayuda de ejecución de lotes del punto de conexión de Azure ML para comprobar la asignación esperada.</span><span class="sxs-lookup"><span data-stu-id="c80e0-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="c80e0-252">Servicio web no requiere una entrada</span><span class="sxs-lookup"><span data-stu-id="c80e0-252">Web Service does not require an input</span></span>
<span data-ttu-id="c80e0-253">Los servicios web de ejecución de lotes de Aprendizaje automático de Azure se pueden usar para ejecutar cualquier flujo de trabajo, por ejemplo, scripts R o Python, que puedan no requerir entradas.</span><span class="sxs-lookup"><span data-stu-id="c80e0-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="c80e0-254">O bien, el experimento se podría configurar con un módulo Lector que no expone ningún GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="c80e0-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="c80e0-255">En ese caso, la actividad AzureMLBatchExecution se configuraría de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c80e0-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="c80e0-256">Servicio web no requiere entrada/salida</span><span class="sxs-lookup"><span data-stu-id="c80e0-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="c80e0-257">El servicio web de ejecución de lotes de Aprendizaje automático de Azure podría no tener configurada ninguna salida de servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="c80e0-258">En este ejemplo, no hay ninguna entrada o salida de servicio web ni tampoco hay configurado ningún GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="c80e0-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="c80e0-259">Todavía hay una salida configurada en la propia actividad, pero que no se presenta como webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="c80e0-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="c80e0-260">Servicio web usa lectores y escritores y la actividad solo se ejecuta cuando otras actividades se realizaron correctamente</span><span class="sxs-lookup"><span data-stu-id="c80e0-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="c80e0-261">Los módulos lector y escritor del servicio web de Aprendizaje automático de Azure se podrían configurar para ejecutarse con o sin GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="c80e0-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="c80e0-262">Sin embargo, quizá quiera insertar llamadas de servicio en una canalización que use dependencias del conjunto de datos para invocar al servicio solo cuando se haya completado un procesamiento ascendente.</span><span class="sxs-lookup"><span data-stu-id="c80e0-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="c80e0-263">También puede desencadenar otra acción una vez completada la ejecución por lotes con este enfoque.</span><span class="sxs-lookup"><span data-stu-id="c80e0-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="c80e0-264">En ese caso, puede expresar las dependencias mediante entradas y salidas de la actividad, sin denominar a ninguna de ellas como entradas o salidas del servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="c80e0-265">Las principales **ideas** obtenidas son:</span><span class="sxs-lookup"><span data-stu-id="c80e0-265">The **takeaways** are:</span></span>

* <span data-ttu-id="c80e0-266">Si el punto de conexión del experimento usa una propiedad webServiceInput: se representa con un conjunto de datos de blobs y se incluye en las entradas de la actividad y en la propiedad webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="c80e0-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="c80e0-267">De lo contrario, se omite la propiedad webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="c80e0-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="c80e0-268">Si el punto de conexión del experimento utiliza webServiceOutput(s): se representan con conjuntos de datos de blobs y se incluyen en la salidas de la actividad y en la propiedad webServiceOutputs.</span><span class="sxs-lookup"><span data-stu-id="c80e0-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="c80e0-269">Las salidas de la actividad y webServiceOutputs se asignan por el nombre de cada salida en el experimento.</span><span class="sxs-lookup"><span data-stu-id="c80e0-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="c80e0-270">De lo contrario, se omite la propiedad webServiceOutputs.</span><span class="sxs-lookup"><span data-stu-id="c80e0-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="c80e0-271">Si el punto de conexión del experimento expone una o más propiedades globalParameters, se proporcionan en la propiedad globalParameters como pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="c80e0-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="c80e0-272">De lo contrario, se omite la propiedad globalParameters.</span><span class="sxs-lookup"><span data-stu-id="c80e0-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="c80e0-273">Las claves distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c80e0-273">The keys are case-sensitive.</span></span> <span data-ttu-id="c80e0-274">[Las funciones de Factoría de datos de Azure](data-factory-functions-variables.md) se pueden usar en los valores.</span><span class="sxs-lookup"><span data-stu-id="c80e0-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="c80e0-275">Es posible incluir conjuntos de datos adicionales en las propiedades de entradas y salidas de la actividad, sin que typeProperties de la actividad haga referencia a ellos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="c80e0-276">Estos conjunto de datos rigen la ejecución mediante el uso de las dependencias de segmento; de no ser así, la actividad AzureMLBatchExecution los omitirá.</span><span class="sxs-lookup"><span data-stu-id="c80e0-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="c80e0-277">Actualización de modelos mediante la actividad de recursos de actualización</span><span class="sxs-lookup"><span data-stu-id="c80e0-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="c80e0-278">Cuando haya terminado el reciclaje, actualice el servicio web de puntuación (experimento predictivo expuesto como servicio web) con el modelo recién entrenado mediante la **actividad de recursos de actualización de Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="c80e0-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="c80e0-279">Para obtener más información, consulte el artículo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Actualización de modelos mediante la actividad de recursos de actualización).</span><span class="sxs-lookup"><span data-stu-id="c80e0-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="c80e0-280">Módulos Lector y Escritor</span><span class="sxs-lookup"><span data-stu-id="c80e0-280">Reader and Writer Modules</span></span>
<span data-ttu-id="c80e0-281">Un escenario común para el uso de parámetros de servicio web es el uso de Lectores y escritores SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="c80e0-282">El módulo Lector se usa para cargar datos en un experimento desde los servicios de administración de datos fuera de Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c80e0-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="c80e0-283">El módulo Escritor sirve para guardar datos desde los experimentos en servicios de administración de datos fuera de Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c80e0-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="c80e0-284">Para obtener información acerca del lector o escritor de SQL/blob de Azure, consulte los temas [Lector ](https://msdn.microsoft.com/library/azure/dn905997.aspx)y [Escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) en MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="c80e0-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="c80e0-285">El ejemplo de la sección anterior utilizó el lector de Blob de Azure y el lector de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="c80e0-286">En esta sección se trata el uso del lector SQL Azure y el escritor SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c80e0-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="c80e0-287">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="c80e0-287">Frequently asked questions</span></span>
<span data-ttu-id="c80e0-288">**P:** Tengo varios archivos generados por medio de mis canalizaciones de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="c80e0-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="c80e0-289">¿Puedo usar la actividad AzureMLBatchExecution para trabajar en todos los archivos?</span><span class="sxs-lookup"><span data-stu-id="c80e0-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="c80e0-290">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="c80e0-290">**A:** Yes.</span></span> <span data-ttu-id="c80e0-291">Consulte **Uso de un módulo lector para leer datos de varios archivos de blob de Azure** para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c80e0-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="c80e0-292">Actividad de puntuación de lotes de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="c80e0-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="c80e0-293">Si va a usar la actividad **AzureMLBatchScoring** para la integración con Azure Machine Learning, se recomienda usar la actividad **AzureMLBatchExecution** más reciente.</span><span class="sxs-lookup"><span data-stu-id="c80e0-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="c80e0-294">La actividad AzureMLBatchExecution se introdujo en la versión de agosto de 2015 del SDK de Azure y Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c80e0-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="c80e0-295">Si desea continuar utilizando la actividad AzureMLBatchScoring, siga leyendo esta sección.</span><span class="sxs-lookup"><span data-stu-id="c80e0-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="c80e0-296">Actividad de puntuación de lotes de Aprendizaje automático de Azure con Almacenamiento de Azure para entrada/salida</span><span class="sxs-lookup"><span data-stu-id="c80e0-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="c80e0-297">Parámetros de servicio web</span><span class="sxs-lookup"><span data-stu-id="c80e0-297">Web Service Parameters</span></span>
<span data-ttu-id="c80e0-298">Para especificar los valores de los parámetros de un servicio web, agregue una sección **typeProperties** a la sección **AzureMLBatchScoringActivty** en el JSON de canalización, tal y como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c80e0-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="c80e0-299">También puede usar [Funciones de Factoría de datos](data-factory-functions-variables.md) para pasar valores para los parámetros de servicio web como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c80e0-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="c80e0-300">Los parámetros de servicio web distinguen entre mayúsculas y minúsculas para garantizar que los nombres que especifica en JSON de actividad coinciden con los que muestra el servicio web.</span><span class="sxs-lookup"><span data-stu-id="c80e0-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="c80e0-301">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c80e0-301">See Also</span></span>
* [<span data-ttu-id="c80e0-302">Entrada de blog de Azure: Introducción a la factoría de datos de Azure y al Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="c80e0-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
