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
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Actualización de los modelos de Azure Machine Learning con la actividad de actualización de recurso

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Actividad de Hive](data-factory-hive-activity.md) 
> * [Actividad de Pig](data-factory-pig-activity.md)
> * [Actividad MapReduce](data-factory-map-reduce.md)
> * [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Actividad de Spark](data-factory-spark.md)
> * [Actividad de ejecución de Batch de Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Actividad Actualizar recurso de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md)
> * [Actividad U-SQL de Data Lake Analytics](data-factory-usql-activity.md)
> * [Actividad personalizada de .NET](data-factory-use-custom-activities.md)

En este artículo complementa Hola factoría de datos principal de Azure: artículo de integración de aprendizaje automático de Azure: [crear canalizaciones predictivas con aprendizaje automático de Azure y Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md). Si aún no lo ha hecho, revise el artículo principal de hello antes de leer este artículo. 

## <a name="overview"></a>Información general
Con el tiempo, los modelos de predicción de hello en experimentos de puntuación de aprendizaje automático de Azure de hello necesitan toobe volver a entrenar con los nuevos conjuntos de datos de entrada. Cuando termine con reciclaje, desea hello tooupdate la puntuación del servicio web con hello volver a entrenar el modelo de aprendizaje automático. Hola pasos típicos tooenable reciclaje y actualizables modelos de aprendizaje automático de Azure a través de servicios web son:

1. Crear un experimento en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net).
2. Cuando esté satisfecho con el modelo de hello, utilice servicios de web toopublish de estudio de aprendizaje automático para ambos hello **experimento de entrenamiento** y puntuación /**experimento predictivo**.

Hello tabla siguiente describen los servicios de web Hola utilizados en este ejemplo.  Consulte [Volver a entrenar modelos de aprendizaje automático mediante programación](../machine-learning/machine-learning-retrain-models-programmatically.md) para obtener información detallada.

- **Servicio web de entrenamiento**: recibe datos de entrenamiento y genera modelos entrenados. salida de Hello de reciclaje de hello es un archivo de .ilearner en un almacenamiento de blobs de Azure. Hola **predeterminado extremo** se crea automáticamente para que cuando publica entrenamiento Hola experimenta como un servicio web. Puede crear varios puntos de conexión pero el ejemplo de Hola utiliza solo Hola punto de conexión predeterminado.
- **Servicio web de puntuación**: recibe ejemplos de datos sin etiqueta y realiza predicciones. salida de Hello de predicción podría tener diversas formas, como un archivo .csv o filas de una base de datos de SQL Azure, dependiendo de la configuración Hola del experimento de Hola. el punto de conexión de Hello predeterminado se crea automáticamente al publicar el experimento de predicción de Hola como un servicio web. 

Hello siguiente imagen muestra hello relación entre el entrenamiento y de los puntos de conexión de puntuación de aprendizaje automático de Azure.

![SERVICIOS WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Puede invocar hello **entrenamiento servicio web** mediante el uso de hello **actividad de ejecución de lotes de aprendizaje automático de Azure**. La invocación de un servicio web de entrenamiento es lo mismo que invocar un servicio web de Azure Machine Learning (servicio web de puntuación) para puntuar datos. Hola anterior portada de secciones de canalización en detalle cómo tooinvoke un servicio web de aprendizaje automático de Azure de una factoría de datos de Azure. 

Puede invocar hello **la puntuación del servicio web** mediante el uso de hello **actividad de recursos de actualización de aprendizaje automático de Azure** servicio de web de hello tooupdate con hello recién entrenado. Hello en los ejemplos siguientes proporciona definiciones de servicio vinculado: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>El servicio web de puntuación es un servicio web clásico
Si la puntuación del servicio web de hello es un **servicio web clásico**, crear hello en segundo lugar **no predeterminado y puede actualizar el extremo** mediante el uso de hello [portal de Azure](https://manage.windowsazure.com). Para conocer los pasos necesarios para ello, consulte el artículo [Creación de puntos de conexión](../machine-learning/machine-learning-create-endpoint.md). Después de crear extremo actualizables de hello no predeterminado, Hola pasos:

* Haga clic en **ejecución por lotes** tooget Hola URI valor hello **mlEndpoint** propiedad JSON.
* Haga clic en **recurso de actualización** vincular el valor URI de hello tooget para hello **updateResourceEndpoint** propiedad JSON. clave de API de Hello es en la propia página de punto de conexión hello (en la esquina inferior derecha de hello).

![punto de conexión actualizable](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

Hola de ejemplo siguiente proporciona una definición de JSON de ejemplo de Hola servicio vinculado de aprendizaje automático de Azure. Hola servicio vinculado utiliza hello apiKey para la autenticación.  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>El servicio web de puntuación es el servicio web Azure Resource Manager 
Si el servicio web de hello es Hola nuevo tipo de servicio web que expone un punto de conexión de administrador de recursos de Azure, no es necesario tooadd hello en segundo lugar **no predeterminado** punto de conexión. Hola **updateResourceEndpoint** Hola servicio vinculado tiene el formato de hello: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

Puede obtener valores para los marcadores de posición en la dirección URL de hello al consultar el servicio web de hello en hello [Web Services Portal de Azure Machine Learning](https://services.azureml.net/). nuevo tipo de punto de conexión de recurso de actualización de Hello requiere un token AAD (Azure Active Directory). Especifique **servicePrincipalId** y **servicePrincipalKey**en el servicio vinculado AzureML. Vea [cómo toocreate entidad de seguridad de servicio y asignar permisos toomanage recursos de Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md). Esta es la definición de un servicio vinculado AzureML de ejemplo: 

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

Hello escenario siguiente proporciona más detalles. Tiene un ejemplo para volver a entrenar y actualizar modelos de Azure Machine Learning a partir de una canalización de Azure Data Factory.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Escenario: entrenamiento y actualización de un modelo de Aprendizaje automático de Azure
Esta sección proporciona una canalización de ejemplo que usa hello **actividad de ejecución de lotes de aprendizaje automático de Azure** tooretrain un modelo. También utiliza la canalización de Hola Hola **actividad de recurso de actualización de Azure ML** tooupdate modelo de Hola Hola la puntuación del servicio web. sección de Hello también proporciona Hola de fragmentos de código JSON para todos los servicios vinculados, conjuntos de datos y canalización de ejemplo de Hola.

Esta es la vista de diagrama de Hola de canalización de ejemplo de Hola. Como puede ver, Hola actividad de ejecución de lotes de aprendizaje automático de Azure toma la entrada de entrenamiento de Hola y genera una salida de entrenamiento (archivo iLearner). Hola actividad de recursos de actualización de aprendizaje automático de Azure toma esta salida de entrenamiento y las actualizaciones de Hola modelo Hola la puntuación del extremo del servicio web. Hola actividades de actualización de recursos no genera ningún resultado. Hola placeholderBlob es simplemente un conjunto de datos de salida ficticio requerido por la canalización de hello Data Factory de Azure servicio toorun Hola.

![diagrama de canalización](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Servicio vinculado de almacenamiento de blobs de Azure:
Hola almacenamiento de Azure contiene Hola datos siguientes:

* datos de aprendizaje. datos de entrada de Hola para servicio de web de aprendizaje de hello aprendizaje automático de Azure.  
* archivo iLearner. Hola de salida de servicio de web de aprendizaje de hello aprendizaje automático de Azure. Este archivo también está Hola entrada toohello actividad de recurso de actualización.  

Aquí está la definición de JSON de ejemplo de Hola del servicio de hello vinculado:

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

### <a name="training-input-dataset"></a>Conjunto de datos de entrada de entrenamiento:
Hello siguiente conjunto de datos representa los datos de entrenamiento de entrada de Hola para servicio de web de aprendizaje de aprendizaje automático de Azure de Hola. Hola actividad de ejecución de lotes de aprendizaje automático de Azure tiene este conjunto de datos como entrada.

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

### <a name="training-output-dataset"></a>Conjunto de datos de salida de entrenamiento:
Hello siguiente conjunto de datos representa hello iLearner archivo de salida de servicio de web de aprendizaje de hello aprendizaje automático de Azure. Hola actividad de ejecución de lotes de aprendizaje automático de Azure genera este conjunto de datos. Este conjunto de datos también es Hola entrada toohello actividad de recurso de actualización de aprendizaje automático de Azure.

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Servicio vinculado para el punto de conexión de entrenamiento de Aprendizaje automático de Azure
Hola siguiente fragmento JSON define un servicio vinculado de aprendizaje de automático de Azure que señala el punto de conexión de toohello predeterminado del servicio web de aprendizaje de Hola.

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

En **estudio de aprendizaje automático**, Hola estos valores de tooget para **mlEndpoint** y **apiKey**:

1. Haga clic en **servicios WEB** en el menú de la izquierda Hola.
2. Haga clic en hello **entrenamiento servicio web** en la lista de hello de servicios web.
3. Haga clic en Copiar a continuación demasiado**clave de API** cuadro de texto. Pegue la clave de hello en el Portapapeles de hello en el editor de JSON de factoría de datos de Hola.
4. Hola **estudio de aprendizaje automático de Azure**, haga clic en **ejecución por lotes** vínculo.
5. Hola copia **URI de solicitud** de hello **solicitar** sección y péguela en el editor de JSON de factoría de datos de Hola.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Servicio vinculado para el punto de conexión de puntuación actualizable de Aprendizaje automático de Azure:
Hola siguiente fragmento JSON define un servicio vinculado de aprendizaje de automático de Azure que señala el extremo actualizables de toohello no predeterminado de hello la puntuación del servicio web.  

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

### <a name="placeholder-output-dataset"></a>Conjunto de datos de salida de marcador de posición:
Hola actividad de recurso de actualización de aprendizaje automático de Azure no genera ningún resultado. Sin embargo, Data Factory de Azure requiere una programación de Hola de toodrive de conjunto de datos de salida de una canalización. Por lo tanto, utilizamos un conjunto de datos ficticio o un marcador de posición en este ejemplo.  

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

### <a name="pipeline"></a>Canalización
canalización de Hello tiene dos actividades: **AzureMLBatchExecution** y **AzureMLUpdateResource**. Hola actividad de ejecución de lotes de aprendizaje automático de Azure toma los datos de entrenamiento de hello como entrada y genera un archivo iLearner como salida. actividad Hello invoca el servicio web de aprendizaje hello (se expone como un servicio web experimento de entrenamiento) con los datos de entrenamiento de entradas de Hola y recibe el archivo ilearner de hello de hello webservice. Hola placeholderBlob es simplemente un conjunto de datos de salida ficticio requerido por la canalización de hello Data Factory de Azure servicio toorun Hola.

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
