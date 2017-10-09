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
# <a name="machine-learning-integration-in-stream-analytics"></a>Integración de Aprendizaje automático en Análisis de transmisiones
Análisis de transmisiones admite funciones definidas por el usuario que informan sobre los puntos de conexión de aprendizaje automático de tooAzure. Compatibilidad con la API de REST para esta característica se detalla en hello [biblioteca de API de REST de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn835031.aspx). Este artículo proporciona información adicional necesaria para una implementación correcta de esta capacidad en Análisis de transmisiones. También se ha publicado un tutorial, que está disponible [aquí](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Información general: terminología de Aprendizaje automático de Azure
Aprendizaje automático de Microsoft Azure proporciona una herramienta de colaboración, arrastrar y colocar que puede usar toobuild, probar e implementar soluciones de análisis predictivo en los datos. Esta herramienta se denomina hello *estudio de aprendizaje automático de Azure*. studio Hello toointeract usado con hello recursos de aprendizaje automático y compilar fácilmente, probar y repita el diseño. A continuación, se proporcionan estos recursos y sus definiciones.

* **Área de trabajo**: Hola *área de trabajo* es un contenedor que contiene todos los demás recursos de aprendizaje automático en un contenedor para la administración y control.
* **Experimento**: *experimentos* se crean los conjuntos de datos de datos científicos tooutilize y entrenar un modelo de aprendizaje automático.
* **Punto de conexión**: *extremos* son Hola aprendizaje características tootake de objeto que se usa como entrada, aplicar un modelo de aprendizaje automático especificado y devuelve un resultado con puntuación.
* **Servicio web de puntuación**: un *servicio web de puntuación* es una colección de puntos de conexión, como se mencionó anteriormente.

Cada punto de conexión tiene varias API para la ejecución de lotes y la ejecución sincrónica. Análisis de transmisiones usa la ejecución sincrónica. se denomina servicio específico de Hello un [servicio de solicitud/respuesta](../machine-learning/machine-learning-consume-web-services.md) en studio de aprendizaje automático de Azure.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Recursos de Machine Learning necesarios para trabajos de Stream Analytics
Para los fines de Hola de análisis de transmisiones de trabajo de procesamiento, un punto de conexión de solicitud/respuesta, un [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), y una definición de swagger son necesarias para la ejecución correcta. Análisis de transmisiones tiene un punto de conexión adicional que construye la dirección url de hello para el extremo de swagger, busca la interfaz de Hola y devuelve un usuario de toohello de definición de UDF de forma predeterminada.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Configuración de un Análisis de transmisiones y funciones definidas por el usuario de Aprendizaje automático mediante la API de REST
Mediante el uso de las API de REST puede configurar las funciones de idioma de la máquina de Azure de toocall de trabajo. pasos de Hello son los siguientes:

1. Creación de un trabajo de Análisis de transmisiones
2. Definición de una entrada
3. Definición de una salida
4. Creación de una función definida por el usuario
5. Escribe una transformación de análisis de transmisiones que llamadas Hola UDF
6. Iniciar el trabajo de Hola

## <a name="creating-a-udf-with-basic-properties"></a>Creación de una función definida por el usuario con las propiedades básicas
Por ejemplo, hello siguiente código de ejemplo crea una UDF escalar denominada *newudf* que enlaza el punto de conexión de tooan aprendizaje automático de Azure. Tenga en cuenta que hello *extremo* (URI del servicio) puede encontrarse en la página de Ayuda de hello API de hello elegido hello y servicio *apiKey* puede encontrarse en la página principal de servicios de Hola.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Ejemplo del cuerpo de solicitud:  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>Llamada al punto de conexión RetrieveDefaultDefinition para la función definida por el usuario predeterminada
Una vez Hola esqueleto que UDF se crea la definición completa de Hola de hello que UDF es necesario. el punto de conexión de Hello RetreiveDefaultDefinition le ayuda a obtener la definición de hello predeterminada para una función escalar que es el punto de conexión de tooan enlazado aprendizaje automático de Azure. carga de Hello siguiente requiere definición de UDF de tooget Hola default para una función escalar que es el punto de conexión de tooan enlazado aprendizaje automático de Azure. No especifica extremo real Hola tal y como ya se ha proporcionado durante la solicitud PUT. Análisis de transmisiones llama extremo Hola proporcionado en la solicitud de hello si se proporciona explícitamente. En caso contrario, utiliza Hola uno originalmente al que hace referencia. Hola aquí toma UDF una sola cadena de parámetro (una frase) y devuelve una única salida de tipo string que indica la etiqueta de "opiniones" hello para esa frase.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Ejemplo del cuerpo de solicitud:  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Un ejemplo de salida tendría el aspecto siguiente.  

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

## <a name="patch-udf-with-hello-response"></a>UDF de revisión con respuesta Hola
Ahora hello UDF debe modificarse con la respuesta anterior de hello, tal y como se muestra a continuación.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

Cuerpo de la solicitud (salida de RetrieveDefaultDefinition):

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Implementar el análisis de transmisiones transformación toocall Hola UDF
Ahora realizar consultas Hola UDF (aquí denominado scoreTweet) para cada evento de entrada y escribir una respuesta para que los resultados del evento tooan.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
