---
title: "modelos de aprendizaje automático de aaaUpdate mediante Data Factory de Azure | Documentos de Microsoft"
description: "Describe cómo toocreate crear canalizaciones predictivas con factoría de datos de Azure y aprendizaje automático de Azure"
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
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="78b64-103">Actualización de los modelos de Azure Machine Learning con la actividad de actualización de recurso</span><span class="sxs-lookup"><span data-stu-id="78b64-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="78b64-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="78b64-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="78b64-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="78b64-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="78b64-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="78b64-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="78b64-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="78b64-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="78b64-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="78b64-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="78b64-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="78b64-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="78b64-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="78b64-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="78b64-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="78b64-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="78b64-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="78b64-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="78b64-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="78b64-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="78b64-114">En este artículo complementa Hola factoría de datos principal de Azure: artículo de integración de aprendizaje automático de Azure: [crear canalizaciones predictivas con aprendizaje automático de Azure y Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="78b64-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="78b64-115">Si aún no lo ha hecho, revise el artículo principal de hello antes de leer este artículo.</span><span class="sxs-lookup"><span data-stu-id="78b64-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="78b64-116">Información general</span><span class="sxs-lookup"><span data-stu-id="78b64-116">Overview</span></span>
<span data-ttu-id="78b64-117">Con el tiempo, los modelos de predicción de hello en experimentos de puntuación de aprendizaje automático de Azure de hello necesitan toobe volver a entrenar con los nuevos conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="78b64-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="78b64-118">Cuando termine con reciclaje, desea hello tooupdate la puntuación del servicio web con hello volver a entrenar el modelo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="78b64-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="78b64-119">Hola pasos típicos tooenable reciclaje y actualizables modelos de aprendizaje automático de Azure a través de servicios web son:</span><span class="sxs-lookup"><span data-stu-id="78b64-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="78b64-120">Crear un experimento en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="78b64-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="78b64-121">Cuando esté satisfecho con el modelo de hello, utilice servicios de web toopublish de estudio de aprendizaje automático para ambos hello **experimento de entrenamiento** y puntuación /**experimento predictivo**.</span><span class="sxs-lookup"><span data-stu-id="78b64-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="78b64-122">Hello tabla siguiente describen los servicios de web Hola utilizados en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="78b64-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="78b64-123">Consulte [Volver a entrenar modelos de aprendizaje automático mediante programación](../machine-learning/machine-learning-retrain-models-programmatically.md) para obtener información detallada.</span><span class="sxs-lookup"><span data-stu-id="78b64-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="78b64-124">**Servicio web de entrenamiento**: recibe datos de entrenamiento y genera modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="78b64-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="78b64-125">salida de Hello de reciclaje de hello es un archivo de .ilearner en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="78b64-126">Hola **predeterminado extremo** se crea automáticamente para que cuando publica entrenamiento Hola experimenta como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="78b64-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="78b64-127">Puede crear varios puntos de conexión pero el ejemplo de Hola utiliza solo Hola punto de conexión predeterminado.</span><span class="sxs-lookup"><span data-stu-id="78b64-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="78b64-128">**Servicio web de puntuación**: recibe ejemplos de datos sin etiqueta y realiza predicciones.</span><span class="sxs-lookup"><span data-stu-id="78b64-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="78b64-129">salida de Hello de predicción podría tener diversas formas, como un archivo .csv o filas de una base de datos de SQL Azure, dependiendo de la configuración Hola del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="78b64-130">el punto de conexión de Hello predeterminado se crea automáticamente al publicar el experimento de predicción de Hola como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="78b64-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="78b64-131">Hello siguiente imagen muestra hello relación entre el entrenamiento y de los puntos de conexión de puntuación de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![SERVICIOS WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="78b64-133">Puede invocar hello **entrenamiento servicio web** mediante el uso de hello **actividad de ejecución de lotes de aprendizaje automático de Azure**.</span><span class="sxs-lookup"><span data-stu-id="78b64-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="78b64-134">La invocación de un servicio web de entrenamiento es lo mismo que invocar un servicio web de Azure Machine Learning (servicio web de puntuación) para puntuar datos.</span><span class="sxs-lookup"><span data-stu-id="78b64-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="78b64-135">Hola anterior portada de secciones de canalización en detalle cómo tooinvoke un servicio web de aprendizaje automático de Azure de una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="78b64-136">Puede invocar hello **la puntuación del servicio web** mediante el uso de hello **actividad de recursos de actualización de aprendizaje automático de Azure** servicio de web de hello tooupdate con hello recién entrenado.</span><span class="sxs-lookup"><span data-stu-id="78b64-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="78b64-137">Hello en los ejemplos siguientes proporciona definiciones de servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="78b64-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="78b64-138">El servicio web de puntuación es un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="78b64-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="78b64-139">Si la puntuación del servicio web de hello es un **servicio web clásico**, crear hello en segundo lugar **no predeterminado y puede actualizar el extremo** mediante el uso de hello [portal de Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="78b64-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="78b64-140">Para conocer los pasos necesarios para ello, consulte el artículo [Creación de puntos de conexión](../machine-learning/machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="78b64-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="78b64-141">Después de crear extremo actualizables de hello no predeterminado, Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="78b64-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="78b64-142">Haga clic en **ejecución por lotes** tooget Hola URI valor hello **mlEndpoint** propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="78b64-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="78b64-143">Haga clic en **recurso de actualización** vincular el valor URI de hello tooget para hello **updateResourceEndpoint** propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="78b64-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="78b64-144">clave de API de Hello es en la propia página de punto de conexión hello (en la esquina inferior derecha de hello).</span><span class="sxs-lookup"><span data-stu-id="78b64-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![punto de conexión actualizable](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="78b64-146">Hola de ejemplo siguiente proporciona una definición de JSON de ejemplo de Hola servicio vinculado de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="78b64-147">Hola servicio vinculado utiliza hello apiKey para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="78b64-147">hello linked service uses hello apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="78b64-148">El servicio web de puntuación es el servicio web Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="78b64-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="78b64-149">Si el servicio web de hello es Hola nuevo tipo de servicio web que expone un punto de conexión de administrador de recursos de Azure, no es necesario tooadd hello en segundo lugar **no predeterminado** punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="78b64-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="78b64-150">Hola **updateResourceEndpoint** Hola servicio vinculado tiene el formato de hello:</span><span class="sxs-lookup"><span data-stu-id="78b64-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="78b64-151">Puede obtener valores para los marcadores de posición en la dirección URL de hello al consultar el servicio web de hello en hello [Web Services Portal de Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="78b64-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="78b64-152">nuevo tipo de punto de conexión de recurso de actualización de Hello requiere un token AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="78b64-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="78b64-153">Especifique **servicePrincipalId** y **servicePrincipalKey**en el servicio vinculado AzureML.</span><span class="sxs-lookup"><span data-stu-id="78b64-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="78b64-154">Vea [cómo toocreate entidad de seguridad de servicio y asignar permisos toomanage recursos de Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78b64-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="78b64-155">Esta es la definición de un servicio vinculado AzureML de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="78b64-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
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

<span data-ttu-id="78b64-156">Hello escenario siguiente proporciona más detalles.</span><span class="sxs-lookup"><span data-stu-id="78b64-156">hello following scenario provides more details.</span></span> <span data-ttu-id="78b64-157">Tiene un ejemplo para volver a entrenar y actualizar modelos de Azure Machine Learning a partir de una canalización de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="78b64-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="78b64-158">Escenario: entrenamiento y actualización de un modelo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="78b64-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="78b64-159">Esta sección proporciona una canalización de ejemplo que usa hello **actividad de ejecución de lotes de aprendizaje automático de Azure** tooretrain un modelo.</span><span class="sxs-lookup"><span data-stu-id="78b64-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="78b64-160">También utiliza la canalización de Hola Hola **actividad de recurso de actualización de Azure ML** tooupdate modelo de Hola Hola la puntuación del servicio web.</span><span class="sxs-lookup"><span data-stu-id="78b64-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="78b64-161">sección de Hello también proporciona Hola de fragmentos de código JSON para todos los servicios vinculados, conjuntos de datos y canalización de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="78b64-162">Esta es la vista de diagrama de Hola de canalización de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="78b64-163">Como puede ver, Hola actividad de ejecución de lotes de aprendizaje automático de Azure toma la entrada de entrenamiento de Hola y genera una salida de entrenamiento (archivo iLearner).</span><span class="sxs-lookup"><span data-stu-id="78b64-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="78b64-164">Hola actividad de recursos de actualización de aprendizaje automático de Azure toma esta salida de entrenamiento y las actualizaciones de Hola modelo Hola la puntuación del extremo del servicio web.</span><span class="sxs-lookup"><span data-stu-id="78b64-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="78b64-165">Hola actividades de actualización de recursos no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="78b64-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="78b64-166">Hola placeholderBlob es simplemente un conjunto de datos de salida ficticio requerido por la canalización de hello Data Factory de Azure servicio toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![diagrama de canalización](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="78b64-168">Servicio vinculado de almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="78b64-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="78b64-169">Hola almacenamiento de Azure contiene Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78b64-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="78b64-170">datos de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="78b64-170">training data.</span></span> <span data-ttu-id="78b64-171">datos de entrada de Hola para servicio de web de aprendizaje de hello aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="78b64-172">archivo iLearner.</span><span class="sxs-lookup"><span data-stu-id="78b64-172">iLearner file.</span></span> <span data-ttu-id="78b64-173">Hola de salida de servicio de web de aprendizaje de hello aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="78b64-174">Este archivo también está Hola entrada toohello actividad de recurso de actualización.</span><span class="sxs-lookup"><span data-stu-id="78b64-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="78b64-175">Aquí está la definición de JSON de ejemplo de Hola del servicio de hello vinculado:</span><span class="sxs-lookup"><span data-stu-id="78b64-175">Here is hello sample JSON definition of hello linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="78b64-176">Conjunto de datos de entrada de entrenamiento:</span><span class="sxs-lookup"><span data-stu-id="78b64-176">Training input dataset:</span></span>
<span data-ttu-id="78b64-177">Hello siguiente conjunto de datos representa los datos de entrenamiento de entrada de Hola para servicio de web de aprendizaje de aprendizaje automático de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="78b64-178">Hola actividad de ejecución de lotes de aprendizaje automático de Azure tiene este conjunto de datos como entrada.</span><span class="sxs-lookup"><span data-stu-id="78b64-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="78b64-179">Conjunto de datos de salida de entrenamiento:</span><span class="sxs-lookup"><span data-stu-id="78b64-179">Training output dataset:</span></span>
<span data-ttu-id="78b64-180">Hello siguiente conjunto de datos representa hello iLearner archivo de salida de servicio de web de aprendizaje de hello aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="78b64-181">Hola actividad de ejecución de lotes de aprendizaje automático de Azure genera este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="78b64-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="78b64-182">Este conjunto de datos también es Hola entrada toohello actividad de recurso de actualización de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="78b64-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="78b64-183">Servicio vinculado para el punto de conexión de entrenamiento de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="78b64-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="78b64-184">Hola siguiente fragmento JSON define un servicio vinculado de aprendizaje de automático de Azure que señala el punto de conexión de toohello predeterminado del servicio web de aprendizaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

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

<span data-ttu-id="78b64-185">En **estudio de aprendizaje automático**, Hola estos valores de tooget para **mlEndpoint** y **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="78b64-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="78b64-186">Haga clic en **servicios WEB** en el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="78b64-187">Haga clic en hello **entrenamiento servicio web** en la lista de hello de servicios web.</span><span class="sxs-lookup"><span data-stu-id="78b64-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="78b64-188">Haga clic en Copiar a continuación demasiado**clave de API** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="78b64-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="78b64-189">Pegue la clave de hello en el Portapapeles de hello en el editor de JSON de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="78b64-190">Hola **estudio de aprendizaje automático de Azure**, haga clic en **ejecución por lotes** vínculo.</span><span class="sxs-lookup"><span data-stu-id="78b64-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="78b64-191">Hola copia **URI de solicitud** de hello **solicitar** sección y péguela en el editor de JSON de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="78b64-192">Servicio vinculado para el punto de conexión de puntuación actualizable de Aprendizaje automático de Azure:</span><span class="sxs-lookup"><span data-stu-id="78b64-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="78b64-193">Hola siguiente fragmento JSON define un servicio vinculado de aprendizaje de automático de Azure que señala el extremo actualizables de toohello no predeterminado de hello la puntuación del servicio web.</span><span class="sxs-lookup"><span data-stu-id="78b64-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="78b64-194">Conjunto de datos de salida de marcador de posición:</span><span class="sxs-lookup"><span data-stu-id="78b64-194">Placeholder output dataset:</span></span>
<span data-ttu-id="78b64-195">Hola actividad de recurso de actualización de aprendizaje automático de Azure no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="78b64-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="78b64-196">Sin embargo, Data Factory de Azure requiere una programación de Hola de toodrive de conjunto de datos de salida de una canalización.</span><span class="sxs-lookup"><span data-stu-id="78b64-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="78b64-197">Por lo tanto, utilizamos un conjunto de datos ficticio o un marcador de posición en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="78b64-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="78b64-198">Canalización</span><span class="sxs-lookup"><span data-stu-id="78b64-198">Pipeline</span></span>
<span data-ttu-id="78b64-199">canalización de Hello tiene dos actividades: **AzureMLBatchExecution** y **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="78b64-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="78b64-200">Hola actividad de ejecución de lotes de aprendizaje automático de Azure toma los datos de entrenamiento de hello como entrada y genera un archivo iLearner como salida.</span><span class="sxs-lookup"><span data-stu-id="78b64-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="78b64-201">actividad Hello invoca el servicio web de aprendizaje hello (se expone como un servicio web experimento de entrenamiento) con los datos de entrenamiento de entradas de Hola y recibe el archivo ilearner de hello de hello webservice.</span><span class="sxs-lookup"><span data-stu-id="78b64-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="78b64-202">Hola placeholderBlob es simplemente un conjunto de datos de salida ficticio requerido por la canalización de hello Data Factory de Azure servicio toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="78b64-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

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
