---
title: "Tutorial: Creación de una canalización mediante el uso de plantillas de Azure Resource Manager | Documentos de Microsoft"
description: "En este tutorial, creará una canalización de Azure Data Factory mediante una plantilla de Azure Resource Manager. Esta canalización copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Tutorial: Utilizar el Administrador de recursos de Azure plantilla toocreate una toocopy de datos de canalización de factoría de datos 
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Asistente para copia](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Plantilla de Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API DE REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Este tutorial muestra cómo toouse una toocreate de plantilla de Azure Resource Manager un generador de datos de Azure. canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. No transforma datos de salida de tooproduce de datos de entrada. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).

En este tutorial, creará una canalización con una actividad en ella: la actividad de copia. actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos. Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).

pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Requisitos previos
* Vaya a través de [Tutorial de introducción y los requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hello completa y **prerequisite** pasos.
* Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall versión más reciente de PowerShell de Azure en el equipo. En este tutorial, usará entidades de factoría de datos de toodeploy de PowerShell. 
* (opcional) Vea [creación de plantillas de administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn acerca de las plantillas de Azure Resource Manager.

## <a name="in-this-tutorial"></a>Apartados de este tutorial
En este tutorial, creará una factoría de datos con hello siguiendo las entidades de la factoría de datos:

| Entidad | Description |
| --- | --- |
| Servicio vinculado de Azure Storage |Vincula la factoría de datos de toohello de cuenta de almacenamiento de Azure. Almacenamiento de Azure es el almacén de datos de origen de Hola y base de datos de SQL Azure es el almacén de datos de receptor de hello para la actividad de copia de hello en tutorial Hola. Especifica la cuenta de almacenamiento de Hola que contiene los datos de entrada de hello para la actividad de copia de Hola. |
| Servicio vinculado a Azure SQL Database |Vincula la factoría de datos de toohello de base de datos de SQL Azure. Especifica la base de datos de SQL Azure de Hola que contiene los datos de salida de hello para la actividad de copia de Hola. |
| Conjunto de datos de entrada de blob de Azure |Hace una referencia de servicio de almacenamiento de Azure vinculada toohello. Hello servicio vinculado hace referencia tooan cuenta de almacenamiento de Azure y conjunto de datos de Blob de Azure Hola especifica Hola contenedor, carpeta y nombre de archivo en el almacenamiento de Hola que contiene los datos de entrada de Hola. |
| Conjunto de datos de salida SQL de Azure |Hace una referencia de servicio de SQL Azure vinculado toohello. servicio vinculado de SQL Azure de Hola hace referencia tooan servidor SQL de Azure y conjunto de datos de SQL Azure Hola especifica el nombre de Hola de tabla de Hola que contiene los datos de salida de hello. |
| Canalización de datos |canalización de Hello tiene una actividad de escriba Copy que toma el conjunto de datos de blob de Azure de hello como entrada y Hola conjunto de datos de SQL Azure como una salida. actividad de copia de Hello copia datos de una tabla de tooa de blobs de Azure en la base de datos de SQL Azure Hola. |

Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Hay dos tipos de actividades: [actividades de movimiento de datos](data-factory-data-movement-activities.md) y [actividades de transformación de datos](data-factory-data-transformation-activities.md). En este tutorial, va a crear una canalización con una actividad (actividad de copia).

![Copiar blobs de Azure tooAzure base de datos SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

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
Cree un archivo JSON denominado **ADFCopyTutorialARM.json** en **C:\ADFGetStarted** carpeta con hello siguen contenido:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob tooAzure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a>Parámetros JSON
Cree un archivo JSON denominado **ADFCopyTutorialARM Parameters.json** que contiene parámetros de plantilla de hello Azure Resource Manager. 

> [!IMPORTANT]
> Especifique el nombre y la clave de la cuenta de Azure Storage para los parámetros storageAccountName y storageAccountKey.  
> 
> Especifique el servidor de Azure SQL, la base de datos, el usuario y la contraseña de los parámetros sqlServerName, databaseName, sqlServerUserName y sqlServerPassword.  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
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
   * Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. Ejecute hello después de entidades de factoría de datos de toodeploy de comando mediante la plantilla de administrador de recursos de Hola que creó en el paso 1.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Supervisión de la canalización

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con su cuenta de Azure.
2. Haga clic en **factorías de datos** Hola izquierdo menú (o) haga clic en **más servicios** y haga clic en **factorías de datos** en **INTELLIGENCE + análisis** categoría.
   
    ![Menú Factorías de datos](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. Hola **factorías de datos** página, buscar y encontrar su factoría de datos (AzureBlobToAzureSQLDatabaseDF). 
   
    ![Búsqueda de la factoría de datos](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Haga clic en su factoría de datos de Azure. Ver página principal de Hola de factoría de datos de Hola.
   
    ![Página principal de la factoría de datos](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Siga las instrucciones de [supervisar conjuntos de datos y canalización](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor canalización de Hola y conjuntos de datos ha creado en este tutorial. Actualmente, Visual Studio no permite supervisar canalizaciones de Data Factory.
7. Cuando se encuentra un segmento en hello **listo** estado, compruebe que los datos de hello están toohello copiado **emp** tabla de base de datos de SQL Azure Hola.


Para obtener más información sobre cómo canalización toomonitor de toouse hojas de portal de Azure y conjuntos de datos ha creado en este tutorial, vea [supervisar conjuntos de datos y canalización](data-factory-monitor-manage-pipelines.md) .

Para obtener más información sobre cómo toouse toomonitor de hello Monitor & Administrar aplicación los datos canalizaciones, consulte [supervisar y administrar las canalizaciones de factoría de datos de Azure mediante la aplicación de supervisión](data-factory-monitor-manage-app.md).

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
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

Es una cadena única en función de identificador de grupo de recursos de Hola.  

### <a name="defining-data-factory-entities"></a>Definición de las entidades de Data Factory
Hello siguientes entidades de la factoría de datos definidas en hello JSON plantilla: 

1. [Servicio vinculado de Almacenamiento de Azure](#azure-storage-linked-service)
2. [Servicio vinculado de Azure SQL](#azure-sql-database-linked-service)
3. [Conjunto de datos del blob de Azure](#azure-blob-dataset)
4. [Conjunto de datos de Azure SQL](#azure-sql-dataset)
5. [Canalización de datos con una actividad de copia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Servicio vinculado de Azure Storage
Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Crea un contenedor y cargar la cuenta de almacenamiento de datos toothis como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure en esta sección. Vea [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado. 

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

Hola connectionString utiliza los parámetros de storageAccountName y storageAccountKey de Hola. valores de Hello para estos parámetros pasados mediante el uso de un archivo de configuración. definición de Hello también usa las variables: azureStroageLinkedService y dataFactoryName se definen en la plantilla de Hola. 

#### <a name="azure-sql-database-linked-service"></a>Servicio vinculado a Azure SQL Database
AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Especifique el nombre del servidor SQL Azure hello, nombre de base de datos, nombre de usuario y contraseña de usuario en esta sección. Vea [servicio vinculado de SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obtener más información acerca de toodefine de propiedades que se usan JSON SQL Azure servicio vinculado.  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

Hola connectionString usa sqlServerName, databaseName, sqlServerUserName y parámetros de sqlServerPassword cuyos valores se pasan mediante un archivo de configuración. Hello definición también utiliza Hola siguientes variables de plantilla de hello: azureSqlLinkedServiceName, dataFactoryName.

#### <a name="azure-blob-dataset"></a>Conjunto de datos del blob de Azure
servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. En la definición de conjunto de datos de blob de Azure, especifique los nombres de contenedor de blobs, carpeta y archivo que contiene los datos de entrada de Hola. Vea [propiedades de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure. 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a>Conjunto de datos de Azure SQL
Especificar nombre de Hola de tabla de hello en la base de datos de SQL Azure de Hola que contiene los datos de hello copiado desde Hola almacenamiento de blobs de Azure. Vea [propiedades de conjunto de datos de SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de SQL Azure. 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a>Canalización de datos
Definir una canalización que copia datos de conjunto de datos de hello Azure blob dataset toohello SQL Azure. Vea [JSON de canalización](data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos que se usan de JSON toodefine una canalización en este ejemplo. 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob tooAzure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-hello-template"></a>Plantilla de reutilización Hola
En el tutorial de hello, ha creado una plantilla para definir las entidades de la factoría de datos y una plantilla para pasar valores de parámetros. canalización de Hello copia datos de una cuenta de almacenamiento de Azure tooan de SQL Azure de base de datos especificado a través de parámetros. toouse Hola mismos entornos plantilla toodeploy factoría de datos entidades toodifferent, cree un archivo de parámetros para cada entorno y utilizarlo al implementar el entorno de toothat.     

Ejemplo:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

Observe que Hola el primer parámetro de comando usa de archivos para el entorno de desarrollo de hello, otra para el entorno de prueba de Hola y Hola una tercera para entorno de producción de hello.  

También puede volver a usar Hola plantilla tooperform tareas que se repiten. Por ejemplo, necesita toocreate muchos generadores de datos con una o más de las canalizaciones que implementan Hola mismo lógica, pero cada factoría de datos utiliza diferentes cuentas de almacenamiento y base de datos SQL. En este escenario, utilice Hola misma plantilla Hola mismo entorno (desarrollo, prueba o producción) con parámetros diferentes archivos toocreate factorías de datos.   

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.
