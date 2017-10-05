---
title: "Actualización de los modelos de Machine Learning con Azure Data Factory | Microsoft Docs"
description: "Describe cómo crear canalizaciones predictivas con Factoría de datos de Azure y Aprendizaje automático de Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="4e8f0-103">Actualización de los modelos de Azure Machine Learning con la actividad de actualización de recurso</span><span class="sxs-lookup"><span data-stu-id="4e8f0-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4e8f0-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="4e8f0-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4e8f0-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="4e8f0-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4e8f0-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="4e8f0-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4e8f0-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="4e8f0-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4e8f0-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="4e8f0-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4e8f0-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4e8f0-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4e8f0-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4e8f0-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4e8f0-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="4e8f0-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4e8f0-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4e8f0-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4e8f0-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="4e8f0-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="4e8f0-114">Este artículo complementa el artículo de integración principal Azure Data Factory - Azure Machine Learning: [Creación de canalizaciones predictivas con Azure Machine Learning y Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="4e8f0-115">Si aún no lo ha hecho, revise el artículo principal antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="4e8f0-116">Información general</span><span class="sxs-lookup"><span data-stu-id="4e8f0-116">Overview</span></span>
<span data-ttu-id="4e8f0-117">Pasado algún tiempo, los modelos predictivos en los experimentos de puntuación de Aprendizaje automático de Azure tienen que volver a entrenarse con nuevos conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="4e8f0-118">Después de terminar con el nuevo entrenamiento, tendrá que actualizar el servicio web de puntuación con el modelo de Aprendizaje automático que volvió a entrenar.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="4e8f0-119">Los pasos más comunes para habilitar el nuevo entrenamiento y actualizar los modelos de Aprendizaje automático de Azure mediante los servicios web son:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="4e8f0-120">Crear un experimento en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="4e8f0-121">Cuando esté satisfecho con el modelo, use Azure Machine Learning Studio para publicar servicios web para el **experimento de entrenamiento** y el **experimento predictivo o de puntuación**.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="4e8f0-122">En la tabla siguiente se describen los servicios web empleados en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="4e8f0-123">Consulte [Volver a entrenar modelos de aprendizaje automático mediante programación](../machine-learning/machine-learning-retrain-models-programmatically.md) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="4e8f0-124">**Servicio web de entrenamiento**: recibe datos de entrenamiento y genera modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="4e8f0-125">El resultado del nuevo entrenamiento es un archivo .ilearner en Blob Storage de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="4e8f0-126">El **punto de conexión predeterminado** se crea automáticamente para cuando publique el experimento de entrenamiento como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="4e8f0-127">Se pueden crear más puntos de conexión, pero el ejemplo usa solo el predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="4e8f0-128">**Servicio web de puntuación**: recibe ejemplos de datos sin etiqueta y realiza predicciones.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="4e8f0-129">El resultado de la predicción puede presentarse en diversas formas, como un archivo .csv o como las filas de una Base de datos de SQL de Azure, dependiendo de la configuración del experimento.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="4e8f0-130">El punto de conexión predeterminado se crea automáticamente cuando se publica el experimento predictivo como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="4e8f0-131">La siguiente imagen muestra la relación entre los puntos de conexión de entrenamiento y de puntuación de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVICIOS WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="4e8f0-133">Puede invocar el **training web service** a través de **actividad de ejecución de lotes de Aprendizaje automático de Azure**.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="4e8f0-134">La invocación de un servicio web de entrenamiento es lo mismo que invocar un servicio web de Azure Machine Learning (servicio web de puntuación) para puntuar datos.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="4e8f0-135">Las secciones anteriores abarcan cómo invocar un servicio web de Azure Machine Learning a partir de una canalización de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="4e8f0-136">Puede invocar el **scoring web service** a través de **Actividad de recursos de actualización de Aprendizaje automático de Azure** para actualizar el servicio web con el modelo recién entrenado.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="4e8f0-137">Los ejemplos siguientes proporcionan definiciones de servicios vinculados:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="4e8f0-138">El servicio web de puntuación es un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="4e8f0-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="4e8f0-139">Si el servicio web de puntuación es un **servicio web clásico**, cree el segundo **punto de conexión no predeterminado y actualizable** mediante [Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="4e8f0-140">Para conocer los pasos necesarios para ello, consulte el artículo [Creación de puntos de conexión](../machine-learning/machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="4e8f0-141">Después de crear el punto de conexión actualizable no predeterminado, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="4e8f0-142">Haga clic en **EJECUCIÓN DE LOTES** para obtener el valor del URI para la propiedad JSON **mlEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="4e8f0-143">Haga clic en vínculo **ACTUALIZAR RECURSO** para obtener el valor de URI para la propiedad JSON **updateResourceEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="4e8f0-144">La clave de API está en la página de punto de conexión (en la esquina inferior derecha).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![punto de conexión actualizable](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="4e8f0-146">En el ejemplo siguiente se proporciona una definición de JSON de ejemplo para el servicio vinculado de AzureML.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="4e8f0-147">El servicio vinculado utiliza apiKey para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-147">The linked service uses the apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="4e8f0-148">El servicio web de puntuación es el servicio web Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e8f0-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="4e8f0-149">Si el servicio web es el nuevo tipo de servicio web que expone un punto de conexión de Azure Resource Manager, no es preciso agregar el segundo punto de conexión **no predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="4e8f0-150">En el servicio vinculado, **updateResourceEndpoint** tiene el formato:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="4e8f0-151">Puede obtener valores para los marcadores de posición en la dirección URL al consultar el servicio web en el [Portal de servicios web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="4e8f0-152">El nuevo tipo de punto de conexión del recurso de actualización requiere un token AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="4e8f0-153">Especifique **servicePrincipalId** y **servicePrincipalKey**en el servicio vinculado AzureML.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="4e8f0-154">Consulte [Uso del portal para crear una aplicación de Active Directory y una entidad de servicio con acceso a los recursos](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="4e8f0-155">Esta es la definición de un servicio vinculado AzureML de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="4e8f0-156">El escenario siguiente proporciona más detalles.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-156">The following scenario provides more details.</span></span> <span data-ttu-id="4e8f0-157">Tiene un ejemplo para volver a entrenar y actualizar modelos de Azure Machine Learning a partir de una canalización de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="4e8f0-158">Escenario: entrenamiento y actualización de un modelo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4e8f0-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="4e8f0-159">Esta sección proporciona una canalización de ejemplo que usa la **actividad Ejecución de lotes de Azure Machine Learning** para volver a entrenar un modelo.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="4e8f0-160">La canalización usa también la **actividad Actualizar recurso de Azure Machine Learning** para actualizar el modelo en el servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="4e8f0-161">La sección también proporciona fragmentos JSON para todos los servicios vinculados, conjuntos de datos y canalización en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="4e8f0-162">Esta es la vista de diagrama de la canalización de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="4e8f0-163">Como se puede apreciar, la actividad Ejecución de lotes de Azure Machine Learning toma la entrada de entrenamiento y genera un resultado de entrenamiento (archivo iLearner).</span><span class="sxs-lookup"><span data-stu-id="4e8f0-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="4e8f0-164">La Actividad de recursos de actualización de Aprendizaje automático de Azure toma este resultado de entrenamiento y actualiza el modelo en el punto de conexión de servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="4e8f0-165">La Actividad de recursos de actualización no produce ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="4e8f0-166">El placeholderBlob es simplemente un conjunto de datos de salida ficticio que el servicio de Factoría de datos de Azure necesita para ejecutar la canalización.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![diagrama de canalización](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="4e8f0-168">Servicio vinculado de almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="4e8f0-169">Almacenamiento de Azure contiene los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="4e8f0-170">datos de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-170">training data.</span></span> <span data-ttu-id="4e8f0-171">Los datos de entrada para el servicio web de entrenamiento de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="4e8f0-172">archivo iLearner.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-172">iLearner file.</span></span> <span data-ttu-id="4e8f0-173">La salida del servicio web de entrenamiento de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="4e8f0-174">Este archivo también es la entrada para la actividad Actualizar recurso.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="4e8f0-175">Esta es la definición de JSON de ejemplo del servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-175">Here is the sample JSON definition of the linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="4e8f0-176">Conjunto de datos de entrada de entrenamiento:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-176">Training input dataset:</span></span>
<span data-ttu-id="4e8f0-177">El siguiente conjunto de datos representa los datos de entrenamiento de entrada para el servicio web de entrenamiento de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="4e8f0-178">La Actividad de ejecución de lotes de Aprendizaje automático de Azure toma este conjunto de datos como entrada.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="4e8f0-179">Conjunto de datos de salida de entrenamiento:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-179">Training output dataset:</span></span>
<span data-ttu-id="4e8f0-180">El siguiente conjunto de datos representa el archivo iLearner de salida del servicio web de entrenamiento de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="4e8f0-181">La Actividad de ejecución de lotes de Aprendizaje automático de Azure produce este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="4e8f0-182">Este conjunto de datos es también la entrada para la Actividad de recursos de actualización de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="4e8f0-183">Servicio vinculado para el punto de conexión de entrenamiento de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4e8f0-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="4e8f0-184">El siguiente fragmento JSON define un servicio vinculado de Aprendizaje automático de Azure que apunta al punto de conexión predeterminado del servicio web de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="4e8f0-185">En **Azure ML Studio**, haga lo siguiente para obtener los valores de **mlEndpoint** y **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="4e8f0-186">Haga clic en **SERVICIOS WEB** en el menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="4e8f0-187">En la lista de servicios web, haga clic en el **servicio web de entrenamiento** .</span><span class="sxs-lookup"><span data-stu-id="4e8f0-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="4e8f0-188">Haga clic en Copiar junto al cuadro de texto **Clave de API** .</span><span class="sxs-lookup"><span data-stu-id="4e8f0-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="4e8f0-189">Pegue la clave del portapapeles en el editor de JSON de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="4e8f0-190">En **Azure ML Studio**, haga clic en el vínculo **EJECUCIÓN DE LOTES**.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="4e8f0-191">Copie el **URI de solicitud** de la sección **Solicitar** y péguelo en el editor de JSON de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="4e8f0-192">Servicio vinculado para el punto de conexión de puntuación actualizable de Aprendizaje automático de Azure:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="4e8f0-193">El siguiente fragmento JSON define un servicio vinculado de Aprendizaje automático de Azure que apunta al punto de conexión no predeterminado y actualizable del servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="4e8f0-194">Conjunto de datos de salida de marcador de posición:</span><span class="sxs-lookup"><span data-stu-id="4e8f0-194">Placeholder output dataset:</span></span>
<span data-ttu-id="4e8f0-195">La actividad Actualizar recurso de Azure Machine Learning no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="4e8f0-196">Sin embargo, Azure Data Factory requiere un conjunto de datos de salida para impulsar la programación de una canalización.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="4e8f0-197">Por lo tanto, utilizamos un conjunto de datos ficticio o un marcador de posición en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="4e8f0-198">Canalización</span><span class="sxs-lookup"><span data-stu-id="4e8f0-198">Pipeline</span></span>
<span data-ttu-id="4e8f0-199">La canalización tiene dos actividades: **AzureMLBatchExecution** y **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="4e8f0-200">La actividad Ejecución de lotes de Azure Machine Learning toma los datos de entrenamiento como entrada y genera como resultado un archivo iLearner.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="4e8f0-201">La actividad invoca el servicio web de entrenamiento (el experimento de entrenamiento expuesto como servicio web) con los datos de entrenamiento de entrada y recibe el archivo ilearner desde el servicio web.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="4e8f0-202">El placeholderBlob es simplemente un conjunto de datos de salida ficticio que el servicio de Factoría de datos de Azure necesita para ejecutar la canalización.</span><span class="sxs-lookup"><span data-stu-id="4e8f0-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![diagrama de canalización](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
