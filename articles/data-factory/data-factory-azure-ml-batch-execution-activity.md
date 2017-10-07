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
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Creación de canalizaciones predictivas con Azure Machine Learning y Azure Data Factory

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

## <a name="introduction"></a>Introducción

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
[Aprendizaje automático de Azure](https://azure.microsoft.com/documentation/services/machine-learning/) permite toobuild, probar e implementar soluciones de análisis predictivo. Desde una perspectiva general, esto se realiza en tres pasos:

1. **Crear un experimento de entrenamiento**. Realice este paso mediante el uso de hello estudio de aprendizaje automático. estudio de aprendizaje automático de Hello es un entorno de desarrollo visual de colaboración que use tootrain y probar un modelo de análisis predictivos utilizando los datos de entrenamiento.
2. **Convertir experimento predictivo tooa**. Una vez que el modelo se ha entrenado con datos existentes y está listo toouse se tooscore nuevos datos, preparar y simplificar el experimento de puntuación.
3. **Implementarlo como un servicio web**. Puede publicar el experimento de puntuación como un servicio web de Azure. Puede enviar tooyour modelo de datos a través de este extremo de servicio web y recibir predicciones de resultado para el modelo de Hola.  

### <a name="azure-data-factory"></a>Azure Data Factory
Factoría de datos es un servicio de integración de datos en la nube que organiza y automatiza hello **movimiento** y **transformación** de datos. Puede crear soluciones de integración de datos mediante Data Factory de Azure que pueden recopilar datos de varios almacenes de datos, transformar y procesar los datos de Hola y publicación de almacenes de datos de toohello de datos de resultado de hello.

Servicio de factoría de datos permite toocreate las canalizaciones de datos que moverán y transforman datos y, a continuación, ejecuta canalizaciones de hello según una programación especificada (cada hora, diariamente, semanalmente, etcetera). También proporciona las dependencias entre sus canalizaciones de datos y el linaje de Hola de visualizaciones enriquecidas toodisplay y supervisar todos sus canalizaciones de datos desde una única vista unificada tooeasily identificar con exactitud los problemas y las alertas de supervisión de la instalación.

Vea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y [crear su primera canalización](data-factory-build-your-first-pipeline.md) tooquickly artículos empezar a trabajar con hello servicio Data Factory de Azure.

### <a name="data-factory-and-machine-learning-together"></a>Data Factory y Machine Learning juntos
Azure habilita la factoría de datos se tooeasily crear canalizaciones que usan un informe publicado [aprendizaje automático de Azure] [ azure-machine-learning] web service para realizar análisis predictivos. Con hello **actividad de ejecución de lotes** en una canalización del generador de datos de Azure, puede invocar un predicciones de toomake de servicio de web de aprendizaje automático de Azure en los datos de hello en lote. Vea [invocar un aprendizaje automático de Azure servicio web usando Hola actividad de ejecución de lotes](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sección para obtener más información.

Con el tiempo, los modelos de predicción de hello en experimentos de puntuación de aprendizaje automático de Azure de hello necesitan toobe volver a entrenar con los nuevos conjuntos de datos de entrada. Puede volver a entrenar un modelo de aprendizaje automático de Azure desde una canalización de factoría de datos realizando Hola pasos:

1. Publicar el experimento de entrenamiento de hello (experimento no predicción) como un servicio web. Realice este paso en estudio de aprendizaje automático de hello como lo hizo tooexpose predictivo experimento como un servicio web en el escenario anterior Hola.
2. Usar Hola el servicio web de actividad de ejecución de lotes de aprendizaje automático de Azure tooinvoke Hola para experimento de entrenamiento de Hola. Básicamente, puede usar tooinvoke de actividad de ejecución de lotes de aprendizaje automático de Azure Hola el servicio web de entrenamiento y la puntuación del servicio web.

Cuando termine con reciclaje, actualizar Hola la puntuación del servicio web (se expone como un servicio web predictivo experimento) con hello recién entrenado usando hello **actualizar recursos actividad de aprendizaje automático de Azure**. Para obtener más información, consulte el artículo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Actualización de modelos mediante la actividad de recursos de actualización).

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Invocación de un servicio web mediante la actividad de ejecución de lotes
Usar procesamiento y movimiento de datos de Data Factory de Azure tooorchestrate y, a continuación, realizar la ejecución por lotes mediante el aprendizaje automático de Azure. Estos son los pasos de nivel superior de hello:

1. Cree un servicio vinculado de Aprendizaje automático de Azure. Necesita Hola siguientes valores:

   1. **URI de solicitud** para hello API de ejecución por lotes. Puede encontrar Hola URI de solicitud, haga clic en hello **ejecución por lotes** vínculo en la página de servicios web de Hola.
   2. **Clave de API** para hello publica el servicio web de aprendizaje automático de Azure. Puede encontrar la clave de API de hello haciendo clic en el servicio web de Hola que haya publicado.
   3. Hola de uso **AzureMLBatchExecution** actividad.

      ![Panel de aprendizaje automático](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI del lote](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Escenario: Experimentos con Web service entradas/salidas que hacen referencia toodata en almacenamiento de blobs de Azure
En este escenario, Hola servicio Web de aprendizaje de máquina de Azure lleva a cabo predicciones mediante datos de un archivo en el almacenamiento de blobs de Azure y almacena los resultados de predicción de hello en el almacenamiento de blobs de Hola. Hello JSON siguiente define una canalización de factoría de datos con una actividad AzureMLBatchExecution. actividad Hello tiene el conjunto de datos de hello **DecisionTreeInputBlob** como entrada y **DecisionTreeResultBlob** como salida de hello. Hola **DecisionTreeInputBlob** se pasa como un servicio web de entrada toohello por mediante hello **webServiceInput** propiedad JSON. Hola **DecisionTreeResultBlob** se pasa como un servicio de Web de salida toohello por mediante hello **webServiceOutputs** propiedad JSON.  

> [!IMPORTANT]
> Si el servicio web de hello toma varias entradas, usar hello **webServiceInputs** propiedad en lugar de usar **webServiceInput**. Vea hello [servicio Web requiere varias entradas](#web-service-requires-multiple-inputs) sección para obtener un ejemplo del uso de hello webServiceInputs propiedad.
>
> Conjuntos de datos que se hace referencia mediante hello **webServiceInput**/**webServiceInputs** y **webServiceOutputs** propiedades (en  **typeProperties**) también deben incluirse en hello actividad **entradas** y **genera**.
>
> En el experimento de Azure ML, la entrada del servicio web y los puertos de salida y parámetros globales tienen nombres predeterminados (input1 e input2) que se pueden personalizar. nombres de Hola que utilizar para webServiceInputs, webServiceOutputs y la configuración de globalParameters deben coincidir exactamente con nombres de hello en experimentos de Hola. Puede ver carga de solicitud de ejemplo de Hola en la página de Ayuda de ejecución de lotes de Hola para su asignación de aprendizaje automático de Azure extremo tooverify Hola esperado.
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
> Solo entradas y salidas de hello AzureMLBatchExecution actividad pueden pasarse como parámetros toohello servicio Web. Por ejemplo, en hello por encima del fragmento de JSON, DecisionTreeInputBlob es una entrada toohello AzureMLBatchExecution actividad, que se pasa como un servicio Web de entrada toohello a través del parámetro webServiceInput.   
>
>

### <a name="example"></a>Ejemplo
Esta toohold de almacenamiento de Azure de ejemplo utiliza ambas Hola datos de entrada y salida.

Se recomienda que atraviesan hello [crear su primera canalización con factoría de datos] [ adf-build-1st-pipeline] tutorial antes de pasar a través de este ejemplo. En este ejemplo, use artefactos de factoría de datos de toocreate de hello Editor de generador de datos (servicios vinculados, conjuntos de datos, canalización).   

1. Cree un **servicio vinculado** para su instancia de **Azure Storage**. Si hello archivos de entrada y salida están en diferentes cuentas de almacenamiento, necesita dos servicios vinculados. Este es un ejemplo de JSON:

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
2. Crear hello **entrada** Data Factory de Azure **conjunto de datos**. A diferencia de otros conjuntos de datos de Data Factory, estos deben contener tanto los valores de **folderPath** como de **fileName**. Puede usar particiones toocause cada tooprocess de ejecución (cada segmento de datos) de proceso por lotes o generar entrada único y archivos de salida. Puede que necesite tooinclude algunos hello tootransform de actividad de nivel superior de entrada en formato de archivo CSV de Hola y lo coloca en la cuenta de almacenamiento de Hola para cada sector. En ese caso, no incluiría hello **externo** y **externalData** configuración se muestra en hello después de ejemplo y su DecisionTreeInputBlob sería el conjunto de datos de salida de hello de una actividad diferente.

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

    El archivo de entrada csv debe tener una fila de encabezado de columna de Hola. Si usas hello **actividad de copia** toocreate o mover Hola csv en almacenamiento de blobs de hello, debe establecer propiedad de receptor de hello **blobWriterAddHeader** demasiado**true**. Por ejemplo:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Si el archivo csv de hello no tiene fila de encabezado de hello, puede ver Hola siguiente error: **produjo Error en actividad: Error al leer la cadena. Token inesperado: StartObject. Path '', line 1, position 1**.
3. Crear hello **salida** Data Factory de Azure **conjunto de datos**. Este ejemplo utiliza particiones toocreate una ruta de acceso de salida único para cada ejecución del segmento. Sin particiones hello, actividad hello reemplazaría archivo hello.

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
4. Crear un **servicio vinculado** de tipo: **AzureMLLinkedService**, que proporciona la clave de API de Hola y URL de ejecución por lotes del modelo.

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
5. Por último, cree una canalización que contenga una actividad **AzureMLBatchExecution** . En tiempo de ejecución, canalización lleva a cabo Hola pasos:

   1. Obtiene la ubicación de Hola Hola del archivo de entrada de los conjuntos de datos de entrada.
   2. Invoca la ejecución por lotes de aprendizaje automático de Azure Hola API
   3. Copias Hola blob de toohello de salida por lotes ejecución determinado del conjunto de datos de salida.

      > [!NOTE]
      > La actividad AzureMLBatchExecution puede tener cero o más entradas y una o más salidas.
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

      Las fechas y horas de inicio (**start**) y de finalización (**end**) deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2014-10-14T16:32:41Z. Hola **final** tiempo es opcional. Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas.**" canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad. Para obtener más información sobre las propiedades JSON, vea [Referencia de scripting JSON](https://msdn.microsoft.com/library/dn835050.aspx) .

      > [!NOTE]
      > Especificar la entrada para la actividad de hello AzureMLBatchExecution es opcional.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Escenario: Experimentos con módulos de lector/escritor toorefer toodata en varios almacenamientos
Otro escenario común al crear experimentos de aprendizaje automático de Azure es toouse módulos de lectura y escritura. módulo de lector de Hello es datos tooload usado en un experimento y módulo de escritor de hello es toosave datos de experimentos. Para obtener información sobre los módulos lector y escritor, consulte los temas [Lector](https://msdn.microsoft.com/library/azure/dn905997.aspx) y [Escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) en MSDN Library.     

Al utilizar los módulos de lector y escritor de hello, es recomendable toouse un parámetro del servicio Web para cada propiedad de estos módulos de lectura/escritura. Estos parámetros web le permiten valores de hello tooconfigure en tiempo de ejecución. Por ejemplo, podría crear un experimento con un módulo lector que usa una base de datos SQL de Azure: XXX.database.windows.net. Una vez implementado el servicio web de hello, desea que los consumidores de hello tooenable de hello web servicio toospecify otro servidor de SQL Azure denominada YYY.database.windows.net. Puede usar un tooallow de parámetro del servicio Web este toobe valor configurado.

> [!NOTE]
> Las entradas y salidas de servicio web son diferentes de los parámetros de servicio web. En el primer escenario hello, ha visto cómo se pueden especificar una entrada y salida para un servicio Web de aprendizaje automático de Azure. En este escenario, pasar parámetros para un servicio Web que se corresponden tooproperties de módulos de lectura/escritura.
>
>

Echemos un vistazo a un escenario de uso de parámetros de servicio web. Tiene un servicio web de aprendizaje automático de Azure implementado que usa un tooread datos del módulo de lector de uno de los orígenes de datos de hello admitidos por el aprendizaje automático de Azure (por ejemplo: base de datos de SQL Azure). Una vez realizada la ejecución por lotes hello, se escriben los resultados de hello mediante un módulo de escritor (base de datos de SQL Azure).  No tiene entradas de servicio web y las salidas se definen en los experimentos de Hola. En este caso, se recomienda que configurar parámetros del servicio web relevantes para los módulos de lector y escritor de Hola. Esta configuración permite a Hola lector/escritor toobe módulos configurada cuando se usa la actividad de hello AzureMLBatchExecution. Especificar parámetros de servicio Web en hello **globalParameters** sección actividad hello JSON como se indica a continuación.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

También puede usar [funciones de factoría de datos](data-factory-functions-variables.md) para pasar valores de hello parámetros del servicio Web como se muestra en el siguiente ejemplo de Hola:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parámetros de servicio Web de Hello distinguen mayúsculas de minúsculas, por lo que garantizar que los nombres de Hola que especifique en la actividad de Hola JSON coinciden con hello las expuestas por hello servicio Web.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>Utiliza una tooread de módulo de lector datos de varios archivos en blobs de Azure
La canalización de macrodatos con actividades como Pig y Hive puede generar uno o varios archivos de salida sin extensiones. Por ejemplo, cuando se especifica una tabla de Hive externa, datos de hello para la tabla de Hive externo Hola pueden almacenarse en el almacenamiento de blobs de Azure con hello después 000000_0 de nombre. También puede usar varios archivos de módulo de lector de hello en un experimento tooread y usarlos para las predicciones.

Cuando se usa el módulo de lector de hello en un experimento de aprendizaje automático de Azure, puede especificar el Blob de Azure como entrada. archivos de Hola Hola almacenamiento de blobs de Azure pueden ser archivos de salida de hello (ejemplo: 000000_0) que se hayan producido por un script de Pig y Hive con HDInsight. Hello módulo de lector permite tooread archivos (con ninguna extensión) mediante la configuración de hello **toocontainer de ruta de acceso, directorio o blob**. Hola **toocontainer de ruta de acceso** puntos toohello contenedor y **directorio/blob** señala toofolder que contiene archivos de hello como se muestra en hello después de la imagen. Hola asterisco es decir, \*) **especifica que todos los archivos en la carpeta de contenedor de Hola Hola (es decir, datos/aggregateddata/año = mes/2014-6 /\*)** se lee como parte del experimento de Hola.

![Propiedades de Blob de Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Ejemplo
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Canalización con la actividad AzureMLBatchExecution con parámetros de servicio web

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

Hola ejemplo JSON anterior:

* Hola implementado Azure Machine Learning servicio Web utiliza un lector y un sistema de escritura módulo tooread/escribir datos de / tooan base de datos de SQL Azure. Este servicio Web expone Hola cuatro parámetros siguientes: nombre del servidor, nombre de base de datos, nombre de cuenta de usuario de servidor y contraseña de cuenta de usuario de servidor de base de datos.  
* Las fechas y horas de inicio (**start**) y de finalización (**end**) deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2014-10-14T16:32:41Z. Hola **final** tiempo es opcional. Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas.**" canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad. Para obtener más información sobre las propiedades JSON, vea [Referencia de scripting JSON](https://msdn.microsoft.com/library/dn835050.aspx) .

### <a name="other-scenarios"></a>Otros escenarios
#### <a name="web-service-requires-multiple-inputs"></a>El servicio web requiere varias entradas
Si el servicio web de hello toma varias entradas, usar hello **webServiceInputs** propiedad en lugar de usar **webServiceInput**. Conjuntos de datos que se hace referencia mediante hello **webServiceInputs** también debe incluirse en hello actividad **entradas**.

En el experimento de Azure ML, la entrada del servicio web y los puertos de salida y parámetros globales tienen nombres predeterminados (input1 e input2) que se pueden personalizar. nombres de Hola que utilizar para webServiceInputs, webServiceOutputs y la configuración de globalParameters deben coincidir exactamente con nombres de hello en experimentos de Hola. Puede ver carga de solicitud de ejemplo de Hola en la página de Ayuda de ejecución de lotes de Hola para su asignación de aprendizaje automático de Azure extremo tooverify Hola esperado.

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

#### <a name="web-service-does-not-require-an-input"></a>Servicio web no requiere una entrada
Servicios de Azure ML lote ejecución web puede ser toorun usado en los flujos de trabajo, por ejemplo, R o scripts de Python, que no requieran ninguna entrada. O bien, experimento Hola puede configurarse con un módulo de lector que no expone ningún GlobalParameters. En ese caso, hello AzureMLBatchExecution actividad se puede configurar como se indica a continuación:

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

#### <a name="web-service-does-not-require-an-inputoutput"></a>Servicio web no requiere entrada/salida
servicio web de aprendizaje automático de Azure batch ejecución Hola podría no tener ningún resultado del servicio Web configurado. En este ejemplo, no hay ninguna entrada o salida de servicio web ni tampoco hay configurado ningún GlobalParameters. Sigue siendo una salida configurada en la propia actividad de hello, pero no se proporciona como un webServiceOutput.

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Ejecuciones de actividad de hello solo cuando otras actividades han sido correctos y escritores y lectores de usos de servicio Web
Hello Azure ML web lector y escritor de módulos de servicio podrían ser toorun configurado con o sin ningún GlobalParameters. Sin embargo, puede que desee tooembed servicio llama en una canalización que utiliza el servicio de Hola de tooinvoke de dependencias de conjunto de datos solo cuando se ha completado un procesamiento de nivel superior. También puede desencadenar otra acción una vez completada la ejecución por lotes Hola con este enfoque. En ese caso, puede expresar las dependencias de hello mediante actividad entradas y salidas, sin asignar un nombre cualquiera de ellos como servicio Web entradas ni salidas.

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

Hola **impresiones** son:

* Si el punto de conexión de experimento usa un webServiceInput: se representa mediante un conjunto de datos de blob y se incluye en entradas de actividad de Hola y propiedad de webServiceInput Hola. En caso contrario, se omite la propiedad de webServiceInput Hola.
* Si el punto de conexión de experimento usa webServiceOutput(s): se incluyen en salidas de la actividad de Hola y en la propiedad webServiceOutputs de Hola y se representan mediante conjuntos de datos de blob. actividad Hello genera e webServiceOutputs se asignan por nombre de Hola de cada salida en el experimento de Hola. En caso contrario, se omite la propiedad webServiceOutputs de Hola.
* Si el punto de conexión de experimento expone globalParameter(s), se facilita en la propiedad globalParameters de hello actividad como pares de clave, valor. En caso contrario, se omite la propiedad globalParameters de Hola. las claves de Hello distinguen mayúsculas de minúsculas. [Las funciones de factoría de datos Azure](data-factory-functions-variables.md) se puede utilizar en valores de hello.
* Conjuntos de datos adicionales pueden incluirse en las propiedades de entradas y salidas de actividad de hello, sin que se hace referencia en hello actividad typeProperties. Estos conjuntos de datos controlan la ejecución con las dependencias de segmento pero en caso contrario, se omiten por hello AzureMLBatchExecution actividad.


## <a name="updating-models-using-update-resource-activity"></a>Actualización de modelos mediante la actividad de recursos de actualización
Cuando termine con reciclaje, actualizar Hola la puntuación del servicio web (se expone como un servicio web predictivo experimento) con hello recién entrenado usando hello **actualizar recursos actividad de aprendizaje automático de Azure**. Para obtener más información, consulte el artículo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Actualización de modelos mediante la actividad de recursos de actualización).

### <a name="reader-and-writer-modules"></a>Módulos Lector y Escritor
Un escenario común para utilizar parámetros de servicio Web es usar Hola de Azure SQL lectores y escritores. módulo de lector de Hello es datos tooload usado en un experimento desde los servicios de administración de datos fuera de estudio de aprendizaje automático de Azure. módulo de escritor de Hello es toosave datos de experimentos en servicios de administración de datos fuera de estudio de aprendizaje automático de Azure.  

Para obtener información acerca del lector o escritor de SQL/blob de Azure, consulte los temas [Lector ](https://msdn.microsoft.com/library/azure/dn905997.aspx)y [Escritor](https://msdn.microsoft.com/library/azure/dn905984.aspx) en MSDN Library. ejemplo de Hola en la sección anterior de hello usa hello Azure Blob lector y el escritor de Blob de Azure. En esta sección se trata el uso del lector SQL Azure y el escritor SQL Azure.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
**P:** Tengo varios archivos generados por medio de mis canalizaciones de macrodatos. ¿Puedo usar hello AzureMLBatchExecution actividad toowork en todos los archivos de hello?

**R:** Sí. Vea hello **utiliza una tooread de módulo de lector datos de varios archivos en blobs de Azure** sección para obtener más información.

## <a name="azure-ml-batch-scoring-activity"></a>Actividad de puntuación de lotes de Aprendizaje automático de Azure
Si usas hello **AzureMLBatchScoring** toointegrate de actividad con aprendizaje automático de Azure, se recomienda que realice hello más reciente **AzureMLBatchExecution** actividad.

Hola AzureMLBatchExecution actividad se introdujo en hello lanzamiento de agosto de 2015 de SDK de Azure y Azure PowerShell.

Si desea que toocontinue mediante la actividad de AzureMLBatchScoring hello, seguir leyendo a través de esta sección.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Actividad de puntuación de lotes de Aprendizaje automático de Azure con Almacenamiento de Azure para entrada/salida

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

### <a name="web-service-parameters"></a>Parámetros de servicio web
toospecify valores para los parámetros de servicio Web, agregue un **typeProperties** sección toohello **AzureMLBatchScoringActivty** sección en JSON como se muestra en el siguiente ejemplo de Hola de la canalización de hello:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
También puede usar [funciones de factoría de datos](data-factory-functions-variables.md) para pasar valores de hello parámetros del servicio Web como se muestra en el siguiente ejemplo de Hola:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parámetros de servicio Web de Hello distinguen mayúsculas de minúsculas, por lo que garantizar que los nombres de Hola que especifique en la actividad de Hola JSON coinciden con hello las expuestas por hello servicio Web.
>
>

## <a name="see-also"></a>Otras referencias
* [Entrada de blog de Azure: Introducción a la factoría de datos de Azure y al Aprendizaje automático de Azure](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
