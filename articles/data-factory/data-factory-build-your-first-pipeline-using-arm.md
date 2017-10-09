---
title: "aaaBuild su primera factoría de datos (plantilla de administrador de recursos) | Documentos de Microsoft"
description: "En este tutorial, creará una canalización de Azure Data Factory de ejemplo con la plantilla de Azure Resource Manager."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Tutorial: Compilación de la primera Data Factory de Azure con la plantilla de Azure Resource Manager
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-build-your-first-pipeline.md)
> * [Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Plantilla de Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API DE REST](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

En este artículo, use un toocreate de plantilla de Azure Resource Manager su primera factoría de datos de Azure. tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola.

canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**. Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce. canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización. 

> [!NOTE]
> canalización de datos de Hello en este tutorial transforma los datos de salida de tooproduce de datos de entrada. Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> canalización de Hello en este tutorial tiene sólo una actividad de tipo: HDInsightHive. pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Requisitos previos
* Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.
* Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall versión más reciente de PowerShell de Azure en el equipo.
* Vea [creación de plantillas de administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn acerca de las plantillas de Azure Resource Manager. 

## <a name="in-this-tutorial"></a>Apartados de este tutorial
| Entidad | Description |
| --- | --- |
| Servicio vinculado de Azure Storage |Vincula la factoría de datos de toohello de cuenta de almacenamiento de Azure. Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola. |
| Servicio vinculado a petición de HDInsight |Vincula un generador de datos a petición toohello de clúster de HDInsight. clúster de Hola se crea automáticamente para usted tooprocess datos y se elimina después de que se realiza un procesamiento Hola. |
| Conjunto de datos de entrada de blob de Azure |Hace una referencia de servicio de almacenamiento de Azure vinculada toohello. Hello servicio vinculado hace referencia tooan cuenta de almacenamiento de Azure y conjunto de datos de Blob de Azure Hola especifica Hola contenedor, carpeta y nombre de archivo en el almacenamiento de Hola que contiene los datos de entrada de Hola. |
| Conjunto de datos de salida de blob de Azure |Hace una referencia de servicio de almacenamiento de Azure vinculada toohello. Hello servicio vinculado hace referencia tooan cuenta de almacenamiento de Azure y conjunto de datos de Blob de Azure de hello especifica Hola contenedor, carpeta y nombre de archivo en el almacenamiento de Hola que contiene datos de salida de saludo. |
| Canalización de datos |canalización de Hello tiene una actividad de tipo HDInsightHive, que consume el conjunto de datos de entrada de Hola y genera el conjunto de datos de salida de hello. |

Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Hay dos tipos de actividades: [actividades de movimiento de datos](data-factory-data-movement-activities.md) y [actividades de transformación de datos](data-factory-data-transformation-activities.md). En este tutorial se crea una canalización con una actividad (actividad de Hive).

Hello siguiente sección proporciona Hola completa el Administrador de recursos plantilla para definir las entidades de la factoría de datos para que pueda ejecutar rápidamente a través de la plantilla de Hola Hola tutorial y prueba. toounderstand cómo se define cada entidad de la factoría de datos, vea [las entidades de la factoría de datos de plantilla de hello](#data-factory-entities-in-the-template) sección.

## <a name="data-factory-json-template"></a>Plantilla JSON de Data Factory
Hola de plantilla de administrador de recursos nivel superior para definir una factoría de datos es: 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
Cree un archivo JSON denominado **ADFTutorialARM.json** en **C:\ADFGetStarted** carpeta con hello siguen contenido:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> Puede encontrar otro ejemplo de plantilla de Resource Manager para crear una factoría de datos de Azure en [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Tutorial: Creación de una canalización con la actividad de copia mediante una plantilla de Azure Resource Manager).  
> 
> 

## <a name="parameters-json"></a>Parámetros JSON
Cree un archivo JSON denominado **ADFTutorialARM Parameters.json** que contiene parámetros de plantilla de hello Azure Resource Manager.  

> [!IMPORTANT]
> Especificar nombre de Hola y la clave de la cuenta de almacenamiento de Azure para hello **storageAccountName** y **storageAccountKey** parámetros en este archivo de parámetros. 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> Puede tener archivos JSON de parámetro independiente para el desarrollo, pruebas y entornos de producción que puede usar con Hola misma plantilla JSON de factoría de datos. Al usar un script de PowerShell, puede automatizar la implementación de las entidades de Data Factory en estos entornos. 
> 
> 

## <a name="create-data-factory"></a>Creación de Data Factory
1. Iniciar **Azure PowerShell** y ejecución Hola siguiente comando: 
   * Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con. Esta suscripción debe ser Hola igual que la que usó en el portal de Azure Hola Hola.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Ejecute hello después de entidades de factoría de datos de toodeploy de comando mediante la plantilla de administrador de recursos de Hola que creó en el paso 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Supervisión de la canalización
1. Después de iniciar sesión toohello [portal de Azure](https://portal.azure.com/), haga clic en **examinar** y seleccione **factorías de datos**.
     ![Examinar-&gt;Factorías de datos](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. Hola **factorías de datos** hoja, haga clic en la factoría de datos de hello (**TutorialFactoryARM**) que ha creado.    
3. Hola **factoría de datos** hoja de la factoría de datos, haga clic en **diagrama**.

     ![Icono Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. Hola **vista de diagrama**, verá información general de las canalizaciones de Hola y conjuntos de datos utilizan en este tutorial.
   
   ![Vista de diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Hola vista de diagrama, haga doble clic en el conjunto de datos de hello **AzureBlobOutput**. Vea dicho sector Hola que se está procesando actualmente.
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Cuando se realiza el procesamiento, verá que el segmento de hello en **listo** estado. La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente). Por consiguiente, esperan Hola canalización tootake **aproximadamente 30 minutos** tooprocess Hola segmento.
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Cuando se encuentra el segmento de hello en **listo** de estado, compruebe hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.  

Vea [supervisar conjuntos de datos y canalización](data-factory-monitor-manage-pipelines.md) para obtener instrucciones sobre cómo canalización de toouse hello Azure hojas portal toomonitor hello y conjuntos de datos ha creado en este tutorial.

También puede utilizar toomonitor de supervisar y administrar aplicaciones sus canalizaciones de datos. Vea [supervisar y administrar las canalizaciones de factoría de datos de Azure mediante la aplicación de supervisión](data-factory-monitor-manage-app.md) para obtener más información sobre el uso de la aplicación hello. 

> [!IMPORTANT]
> archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente. Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Entidades de generador de datos en la plantilla de Hola
### <a name="define-data-factory"></a>Definición de factoría de datos
Defina una factoría de datos en la plantilla de administrador de recursos de hello tal y como se muestra en el siguiente ejemplo de Hola:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
Hola dataFactoryName se define como: 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Es una cadena única en función de identificador de grupo de recursos de Hola.  

### <a name="defining-data-factory-entities"></a>Definición de las entidades de Data Factory
Hello siguientes entidades de la factoría de datos definidas en hello JSON plantilla: 

* [Servicio vinculado de Almacenamiento de Azure](#azure-storage-linked-service)
* [Servicio vinculado a petición de HDInsight](#hdinsight-on-demand-linked-service)
* [Conjunto de datos de entrada de blob de Azure:](#azure-blob-input-dataset)
* [Conjunto de datos de salida de blob de Azure](#azure-blob-output-dataset)
* [Canalización de datos con una actividad de copia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Servicio vinculado de Azure Storage
Especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure en esta sección. Vea [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado. 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Hola **connectionString** usa Hola parámetros storageAccountName y storageAccountKey. valores de Hello para estos parámetros pasados mediante el uso de un archivo de configuración. definición de Hello también usa las variables: azureStroageLinkedService y dataFactoryName se definen en la plantilla de Hola. 

#### <a name="hdinsight-on-demand-linked-service"></a>Servicio vinculado a petición de HDInsight
Vea [servicios vinculados de proceso](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) un servicio vinculado de HDInsight a petición del artículo para obtener más información acerca de toodefine de propiedades que se usan JSON.  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
Tenga en cuenta Hola siguientes puntos: 

* Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello por encima de JSON. Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) . 
* Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición. Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento necesario toobe procesado a menos que haya un clúster existente en vivo (**timeToLive**) y se elimina cuando se realiza un procesamiento Hola.
  
    A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.

Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

#### <a name="azure-blob-input-dataset"></a>Conjunto de datos de entrada de blob de Azure
Especificar nombres de Hola de contenedor de blobs, carpeta y archivo que contiene los datos de entrada de Hola. Vea [propiedades de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure. 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
Esta definición usa Hola parámetros definidos en la plantilla de parámetro siguientes: blobContainer, inputBlobFolder y inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Conjunto de datos de salida de blob de Azure
Especificar nombres de Hola de contenedor de blob y la carpeta que contiene los datos de salida de hello. Vea [propiedades de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

Esta definición usa Hola parámetros definidos en la plantilla del parámetro hello siguientes: blobContainer y outputBlobFolder. 

#### <a name="data-pipeline"></a>Canalización de datos
Defina una canalización que transforme los datos mediante la ejecución de un script de Hive en un clúster a petición de Azure HDInsight. Vea [JSON de canalización](data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos que se usan de JSON toodefine una canalización en este ejemplo. 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a>Plantilla de reutilización Hola
En el tutorial de hello, ha creado una plantilla para definir las entidades de la factoría de datos y una plantilla para pasar valores de parámetros. toouse Hola mismos entornos plantilla toodeploy factoría de datos entidades toodifferent, cree un archivo de parámetros para cada entorno y utilizarlo al implementar el entorno de toothat.     

Ejemplo:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Observe que Hola el primer parámetro de comando usa de archivos para el entorno de desarrollo de hello, otra para el entorno de prueba de Hola y Hola una tercera para entorno de producción de hello.  

También puede volver a usar Hola plantilla tooperform tareas que se repiten. Por ejemplo, necesita toocreate muchos generadores de datos con uno o más de las canalizaciones que implementan Hola misma lógica, pero cada almacenamiento de Azure diferentes datos generador utiliza y las cuentas de base de datos de SQL Azure. En este escenario, utilice Hola misma plantilla Hola mismo entorno (desarrollo, prueba o producción) con parámetros diferentes archivos toocreate factorías de datos. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Plantilla de Resource Manager para crear una puerta de enlace
Aquí es una plantilla de administrador de recursos de ejemplo para crear una puerta de enlace lógico Hola de nuevo. Instala una puerta de enlace en el equipo local o la máquina virtual de IaaS de Azure y registrar la puerta de enlace de hello con servicio de factoría de datos mediante una clave. Para más información, consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) .

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
Esta plantilla crea una factoría de datos denominada GatewayUsingArmDF con una puerta de enlace llamada GatewayUsingARM. 

## <a name="see-also"></a>Otras referencias
| Tema. | Descripción |
|:--- |:--- |
| [Procesos](data-factory-create-pipelines.md) |En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa. |
| [Conjuntos de datos](data-factory-create-datasets.md) |Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure. |
| [Programación y ejecución con Data Factory](data-factory-scheduling-and-execution.md) |En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación. |
| [Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) |Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones. |

