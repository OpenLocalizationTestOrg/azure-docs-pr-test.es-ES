---
title: "puntos de conexión de aprendizaje automático de Azure de aaaUse en análisis de transmisiones | Documentos de Microsoft"
description: "Funciones definidas por el usuario de Aprendizaje automático de Azure en Análisis de transmisiones"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="ba5b7-103">Integración de Aprendizaje automático en Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="ba5b7-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="ba5b7-104">Análisis de transmisiones admite funciones definidas por el usuario que informan sobre los puntos de conexión de aprendizaje automático de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="ba5b7-105">Compatibilidad con la API de REST para esta característica se detalla en hello [biblioteca de API de REST de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba5b7-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="ba5b7-106">Este artículo proporciona información adicional necesaria para una implementación correcta de esta capacidad en Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="ba5b7-107">También se ha publicado un tutorial, que está disponible [aquí](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ba5b7-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="ba5b7-108">Información general: terminología de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="ba5b7-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="ba5b7-109">Aprendizaje automático de Microsoft Azure proporciona una herramienta de colaboración, arrastrar y colocar que puede usar toobuild, probar e implementar soluciones de análisis predictivo en los datos.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="ba5b7-110">Esta herramienta se denomina hello *estudio de aprendizaje automático de Azure*.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="ba5b7-111">studio Hello toointeract usado con hello recursos de aprendizaje automático y compilar fácilmente, probar y repita el diseño.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="ba5b7-112">A continuación, se proporcionan estos recursos y sus definiciones.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="ba5b7-113">**Área de trabajo**: Hola *área de trabajo* es un contenedor que contiene todos los demás recursos de aprendizaje automático en un contenedor para la administración y control.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="ba5b7-114">**Experimento**: *experimentos* se crean los conjuntos de datos de datos científicos tooutilize y entrenar un modelo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="ba5b7-115">**Punto de conexión**: *extremos* son Hola aprendizaje características tootake de objeto que se usa como entrada, aplicar un modelo de aprendizaje automático especificado y devuelve un resultado con puntuación.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="ba5b7-116">**Servicio web de puntuación**: un *servicio web de puntuación* es una colección de puntos de conexión, como se mencionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="ba5b7-117">Cada punto de conexión tiene varias API para la ejecución de lotes y la ejecución sincrónica.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="ba5b7-118">Análisis de transmisiones usa la ejecución sincrónica.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="ba5b7-119">se denomina servicio específico de Hello un [servicio de solicitud/respuesta](../machine-learning/machine-learning-consume-web-services.md) en studio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="ba5b7-120">Recursos de Machine Learning necesarios para trabajos de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ba5b7-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="ba5b7-121">Para los fines de Hola de análisis de transmisiones de trabajo de procesamiento, un punto de conexión de solicitud/respuesta, un [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), y una definición de swagger son necesarias para la ejecución correcta.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="ba5b7-122">Análisis de transmisiones tiene un punto de conexión adicional que construye la dirección url de hello para el extremo de swagger, busca la interfaz de Hola y devuelve un usuario de toohello de definición de UDF de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="ba5b7-123">Configuración de un Análisis de transmisiones y funciones definidas por el usuario de Aprendizaje automático mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="ba5b7-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="ba5b7-124">Mediante el uso de las API de REST puede configurar las funciones de idioma de la máquina de Azure de toocall de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="ba5b7-125">pasos de Hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ba5b7-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="ba5b7-126">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="ba5b7-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="ba5b7-127">Definición de una entrada</span><span class="sxs-lookup"><span data-stu-id="ba5b7-127">Define an input</span></span>
3. <span data-ttu-id="ba5b7-128">Definición de una salida</span><span class="sxs-lookup"><span data-stu-id="ba5b7-128">Define an output</span></span>
4. <span data-ttu-id="ba5b7-129">Creación de una función definida por el usuario</span><span class="sxs-lookup"><span data-stu-id="ba5b7-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="ba5b7-130">Escribe una transformación de análisis de transmisiones que llamadas Hola UDF</span><span class="sxs-lookup"><span data-stu-id="ba5b7-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="ba5b7-131">Iniciar el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="ba5b7-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="ba5b7-132">Creación de una función definida por el usuario con las propiedades básicas</span><span class="sxs-lookup"><span data-stu-id="ba5b7-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="ba5b7-133">Por ejemplo, hello siguiente código de ejemplo crea una UDF escalar denominada *newudf* que enlaza el punto de conexión de tooan aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="ba5b7-134">Tenga en cuenta que hello *extremo* (URI del servicio) puede encontrarse en la página de Ayuda de hello API de hello elegido hello y servicio *apiKey* puede encontrarse en la página principal de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="ba5b7-135">Ejemplo del cuerpo de solicitud:</span><span class="sxs-lookup"><span data-stu-id="ba5b7-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="ba5b7-136">Llamada al punto de conexión RetrieveDefaultDefinition para la función definida por el usuario predeterminada</span><span class="sxs-lookup"><span data-stu-id="ba5b7-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="ba5b7-137">Una vez Hola esqueleto que UDF se crea la definición completa de Hola de hello que UDF es necesario.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="ba5b7-138">el punto de conexión de Hello RetreiveDefaultDefinition le ayuda a obtener la definición de hello predeterminada para una función escalar que es el punto de conexión de tooan enlazado aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="ba5b7-139">carga de Hello siguiente requiere definición de UDF de tooget Hola default para una función escalar que es el punto de conexión de tooan enlazado aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="ba5b7-140">No especifica extremo real Hola tal y como ya se ha proporcionado durante la solicitud PUT.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="ba5b7-141">Análisis de transmisiones llama extremo Hola proporcionado en la solicitud de hello si se proporciona explícitamente.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="ba5b7-142">En caso contrario, utiliza Hola uno originalmente al que hace referencia.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="ba5b7-143">Hola aquí toma UDF una sola cadena de parámetro (una frase) y devuelve una única salida de tipo string que indica la etiqueta de "opiniones" hello para esa frase.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="ba5b7-144">Ejemplo del cuerpo de solicitud:</span><span class="sxs-lookup"><span data-stu-id="ba5b7-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="ba5b7-145">Un ejemplo de salida tendría el aspecto siguiente.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="ba5b7-146">UDF de revisión con respuesta Hola</span><span class="sxs-lookup"><span data-stu-id="ba5b7-146">Patch UDF with hello response</span></span>
<span data-ttu-id="ba5b7-147">Ahora hello UDF debe modificarse con la respuesta anterior de hello, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="ba5b7-148">Cuerpo de la solicitud (salida de RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="ba5b7-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="ba5b7-149">Implementar el análisis de transmisiones transformación toocall Hola UDF</span><span class="sxs-lookup"><span data-stu-id="ba5b7-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="ba5b7-150">Ahora realizar consultas Hola UDF (aquí denominado scoreTweet) para cada evento de entrada y escribir una respuesta para que los resultados del evento tooan.</span><span class="sxs-lookup"><span data-stu-id="ba5b7-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="ba5b7-151">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="ba5b7-151">Get help</span></span>
<span data-ttu-id="ba5b7-152">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="ba5b7-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba5b7-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba5b7-153">Next steps</span></span>
* [<span data-ttu-id="ba5b7-154">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="ba5b7-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ba5b7-155">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ba5b7-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ba5b7-156">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="ba5b7-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ba5b7-157">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="ba5b7-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ba5b7-158">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ba5b7-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
