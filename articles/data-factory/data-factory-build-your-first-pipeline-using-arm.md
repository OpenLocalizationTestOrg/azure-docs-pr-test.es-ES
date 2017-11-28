---
title: "Creación de la primera factoría de datos (plantilla de Resource Manager) | Microsoft Azure"
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
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="2a775-103">Tutorial: Compilación de la primera Data Factory de Azure con la plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2a775-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a775-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a775-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="2a775-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="2a775-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a775-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="2a775-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a775-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="2a775-108">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2a775-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="2a775-109">API DE REST</span><span class="sxs-lookup"><span data-stu-id="2a775-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="2a775-110">En este artículo, usará una plantilla de Azure Resource Manager para crear su primera instancia de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2a775-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="2a775-111">Para realizar el tutorial con otros SDK/herramientas, seleccione una de las opciones de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="2a775-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="2a775-112">La canalización de este tutorial tiene una actividad: **actividad de HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="2a775-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="2a775-113">Esta actividad ejecuta un script de Hive en un clúster de Azure HDInsight que transforma los datos de entrada para generar datos de salida.</span><span class="sxs-lookup"><span data-stu-id="2a775-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="2a775-114">La canalización está programada para ejecutarse una vez al mes entre las horas de inicio y finalización especificadas.</span><span class="sxs-lookup"><span data-stu-id="2a775-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="2a775-115">En este tutorial, la canalización de datos transforma los datos de entrada para generar datos de salida.</span><span class="sxs-lookup"><span data-stu-id="2a775-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="2a775-116">Para ver un tutorial acerca de cómo copiar datos mediante Azure Data Factory, consulte [Copia de datos de Blob Storage en SQL Database mediante Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2a775-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="2a775-117">La canalización de este tutorial tiene solo una actividad de tipo: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="2a775-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="2a775-118">pero se puede tener más de una actividad en una canalización.</span><span class="sxs-lookup"><span data-stu-id="2a775-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="2a775-119">También puede encadenar dos actividades (ejecutar una después de otra) haciendo que el conjunto de datos de salida de una actividad sea el conjunto de datos de entrada de la otra actividad.</span><span class="sxs-lookup"><span data-stu-id="2a775-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="2a775-120">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="2a775-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2a775-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a775-121">Prerequisites</span></span>
* <span data-ttu-id="2a775-122">Lea el artículo [Tutorial: Compilación de la primera canalización para procesar datos mediante el clúster de Hadoop](data-factory-build-your-first-pipeline.md) y complete los pasos de los **requisitos previos** .</span><span class="sxs-lookup"><span data-stu-id="2a775-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="2a775-123">Siga las instrucciones del artículo [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para instalar la última versión de Azure PowerShell en su equipo.</span><span class="sxs-lookup"><span data-stu-id="2a775-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="2a775-124">Para más información sobre las plantillas de Azure Resource Manager (ARM), consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="2a775-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="2a775-125">Apartados de este tutorial</span><span class="sxs-lookup"><span data-stu-id="2a775-125">In this tutorial</span></span>
| <span data-ttu-id="2a775-126">Entidad</span><span class="sxs-lookup"><span data-stu-id="2a775-126">Entity</span></span> | <span data-ttu-id="2a775-127">Description</span><span class="sxs-lookup"><span data-stu-id="2a775-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a775-128">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-128">Azure Storage linked service</span></span> |<span data-ttu-id="2a775-129">Vincula la cuenta de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2a775-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="2a775-130">La cuenta de Almacenamiento de Azure contiene los datos de entrada y salida de la canalización de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2a775-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="2a775-131">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a775-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="2a775-132">Vincula un clúster de HDInsight a petición a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2a775-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="2a775-133">El clúster se crea automáticamente para procesar los datos y se elimina después de que termina el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="2a775-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="2a775-134">Conjunto de datos de entrada de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-134">Azure Blob input dataset</span></span> |<span data-ttu-id="2a775-135">Hace referencia al servicio vinculado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2a775-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="2a775-136">El servicio vinculado hace referencia a una cuenta de Azure Storage y los conjuntos de datos del blob de Azure especifican el contenedor, la carpeta y el nombre de archivo del almacenamiento que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2a775-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="2a775-137">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-137">Azure Blob output dataset</span></span> |<span data-ttu-id="2a775-138">Hace referencia al servicio vinculado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2a775-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="2a775-139">El servicio vinculado hace referencia a una cuenta de Azure Storage y el conjunto de datos de Azure Blob especifica el contenedor, la carpeta y el nombre de archivo del almacenamiento que contiene los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="2a775-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="2a775-140">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="2a775-140">Data pipeline</span></span> |<span data-ttu-id="2a775-141">La canalización tiene una actividad de tipo HDInsightHive, que consume el conjunto de datos de entrada y genera el conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="2a775-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="2a775-142">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="2a775-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="2a775-143">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="2a775-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="2a775-144">Hay dos tipos de actividades: [actividades de movimiento de datos](data-factory-data-movement-activities.md) y [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2a775-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="2a775-145">En este tutorial se crea una canalización con una actividad (actividad de Hive).</span><span class="sxs-lookup"><span data-stu-id="2a775-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="2a775-146">En la siguiente sección se proporciona la plantilla completa de Resource Manager para definir las entidades de Data Factory para que pueda ejecutar el tutorial rápidamente y probar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="2a775-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="2a775-147">Para entender cómo se define cada entidad de Data Factory, consulte la sección [Entidades de Data Factory en la plantilla](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="2a775-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="2a775-148">Plantilla JSON de Data Factory</span><span class="sxs-lookup"><span data-stu-id="2a775-148">Data Factory JSON template</span></span>
<span data-ttu-id="2a775-149">La plantilla de Resource Manager de nivel superior para definir una factoría de datos es:</span><span class="sxs-lookup"><span data-stu-id="2a775-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="2a775-150">Cree un archivo JSON llamado **ADFTutorialARM.json** en la carpeta **C:\ADFGetStarted** con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="2a775-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
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
> <span data-ttu-id="2a775-151">Puede encontrar otro ejemplo de plantilla de Resource Manager para crear una factoría de datos de Azure en [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Tutorial: Creación de una canalización con la actividad de copia mediante una plantilla de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="2a775-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="2a775-152">Parámetros JSON</span><span class="sxs-lookup"><span data-stu-id="2a775-152">Parameters JSON</span></span>
<span data-ttu-id="2a775-153">Cree un archivo JSON denominado **ADFTutorialARM Parameters.json** que contenga parámetros para la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2a775-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="2a775-154">Especifique el nombre y la clave de la cuenta de Azure Storage para los parámetros **storageAccountName** y **storageAccountKey** en este archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="2a775-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="2a775-155">Puede tener archivos JSON de parámetros independientes para los entornos de desarrollo, pruebas y producción, que puede usar con la misma plantilla JSON de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2a775-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="2a775-156">Al usar un script de PowerShell, puede automatizar la implementación de las entidades de Data Factory en estos entornos.</span><span class="sxs-lookup"><span data-stu-id="2a775-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="2a775-157">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="2a775-157">Create data factory</span></span>
1. <span data-ttu-id="2a775-158">Inicie **Azure PowerShell** y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2a775-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="2a775-159">Ejecute el siguiente comando y escriba el nombre de usuario y la contraseña que utiliza para iniciar sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a775-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="2a775-160">Ejecute el siguiente comando para ver todas las suscripciones para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="2a775-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="2a775-161">Ejecute el comando siguiente para seleccionar la suscripción con la que desea trabajar.</span><span class="sxs-lookup"><span data-stu-id="2a775-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="2a775-162">Esta suscripción debe ser la misma que la que usó en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a775-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="2a775-163">Ejecute el siguiente comando para implementar las entidades de Data Factory mediante la plantilla de Resource Manager que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="2a775-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="2a775-164">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="2a775-164">Monitor pipeline</span></span>
1. <span data-ttu-id="2a775-165">Después de iniciar sesión en [Azure Portal](https://portal.azure.com/), haga clic en **Examinar** y seleccione **Factorías de datos**.</span><span class="sxs-lookup"><span data-stu-id="2a775-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="2a775-166">![Examinar->Factorías de datos](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="2a775-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="2a775-167">En la hoja **Factorías de datos**, haga clic en la factoría de datos (**TutorialFactoryARM**) que creó.</span><span class="sxs-lookup"><span data-stu-id="2a775-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="2a775-168">En la hoja **Factoría de datos** de su factoría de datos, haga clic en **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="2a775-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Icono Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="2a775-170">En la **Vista de diagrama**, se ve información general de las canalizaciones y los conjuntos de datos empleados en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a775-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Vista de diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="2a775-172">En la Vista de diagrama, haga doble clic en el conjunto de datos **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="2a775-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="2a775-173">Se ve que el segmento se está procesando.</span><span class="sxs-lookup"><span data-stu-id="2a775-173">You see that the slice that is currently being processed.</span></span>
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="2a775-175">Cuando finalice el procesamiento, el segmento aparece con el estado **Listo** .</span><span class="sxs-lookup"><span data-stu-id="2a775-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="2a775-176">La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="2a775-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="2a775-177">Por tanto, cabe esperar que la canalización tarde **aproximadamente 30 minutos** en procesar el segmento.</span><span class="sxs-lookup"><span data-stu-id="2a775-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="2a775-179">Cuando el segmento tenga el estado **Listo**, busque los datos de salida en la carpeta **partitioneddata** del contenedor **adfgetstarted** del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="2a775-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="2a775-180">Para obtener instrucciones sobre cómo usar las hojas del Portal de Azure para supervisar la canalización y los conjuntos de datos creados en este tutorial, consulte [Supervisión de conjuntos de datos y canalizaciones](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="2a775-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="2a775-181">También puede supervisar y administrar la aplicación para supervisar las canalizaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="2a775-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="2a775-182">Para más información acerca del uso de la aplicación, consulte [Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) .</span><span class="sxs-lookup"><span data-stu-id="2a775-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2a775-183">El archivo de entrada se elimina cuando el segmento se procesa correctamente.</span><span class="sxs-lookup"><span data-stu-id="2a775-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="2a775-184">Por lo tanto, si desea volver a ejecutar el segmento o volver a realizar el tutorial, cargue el archivo de entrada (input.log) en la carpeta inputdata del contenedor adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="2a775-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="2a775-185">Entidades de Data Factory en la plantilla</span><span class="sxs-lookup"><span data-stu-id="2a775-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="2a775-186">Definición de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="2a775-186">Define data factory</span></span>
<span data-ttu-id="2a775-187">Puede definir una factoría de datos en la plantilla de Resource Manager como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a775-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="2a775-188">El valor de dataFactoryName se define como:</span><span class="sxs-lookup"><span data-stu-id="2a775-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="2a775-189">Es una cadena única basada en el identificador del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2a775-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="2a775-190">Definición de las entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="2a775-190">Defining Data Factory entities</span></span>
<span data-ttu-id="2a775-191">Las siguientes entidades de Data Factory se definen en la plantilla JSON:</span><span class="sxs-lookup"><span data-stu-id="2a775-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="2a775-192">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="2a775-193">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a775-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="2a775-194">Conjunto de datos de entrada de blob de Azure:</span><span class="sxs-lookup"><span data-stu-id="2a775-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="2a775-195">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="2a775-196">Canalización de datos con una actividad de copia</span><span class="sxs-lookup"><span data-stu-id="2a775-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="2a775-197">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-197">Azure Storage linked service</span></span>
<span data-ttu-id="2a775-198">Especifique el nombre y la clave de la cuenta de almacenamiento de Azure en esta sección.</span><span class="sxs-lookup"><span data-stu-id="2a775-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="2a775-199">Consulte [Servicio vinculado de Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service) para más información sobre las propiedades JSON usadas para definir un servicio vinculado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2a775-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="2a775-200">**connectionString** usa los parámetros storageAccountName y storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="2a775-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="2a775-201">Los valores de estos parámetros se pasan mediante el uso de un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2a775-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="2a775-202">La definición también usa las variables azureStroageLinkedService y dataFactoryName definidas en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="2a775-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="2a775-203">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a775-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="2a775-204">Consulte el artículo [Servicios vinculados de proceso](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para más información sobre las propiedades JSON que se usan para definir un servicio vinculado a petición de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a775-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="2a775-205">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="2a775-205">Note the following points:</span></span> 

* <span data-ttu-id="2a775-206">Data Factory crea un clúster de HDInsight **basado en Linux** con el código JSON anterior.</span><span class="sxs-lookup"><span data-stu-id="2a775-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="2a775-207">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="2a775-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="2a775-208">Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="2a775-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="2a775-209">Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="2a775-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="2a775-210">El clúster de HDInsight crea un **contenedor predeterminado** en el almacenamiento de blobs que especificó en JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="2a775-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="2a775-211">HDInsight no elimina este contenedor cuando se elimina el clúster.</span><span class="sxs-lookup"><span data-stu-id="2a775-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="2a775-212">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="2a775-212">This behavior is by design.</span></span> <span data-ttu-id="2a775-213">Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez tenga que procesarse un segmento, a menos que haya un clúster existente activo (**timeToLive**), que se elimina cuando finaliza el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="2a775-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="2a775-214">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a775-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="2a775-215">Si no los necesita para solucionar problemas de trabajos, puede eliminarlos para reducir el costo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2a775-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="2a775-216">Los nombres de estos contenedores siguen este patrón: "adf**nombredefactoría dedatos**-**nombredelserviciovinculado**-marcadefechayhora".</span><span class="sxs-lookup"><span data-stu-id="2a775-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="2a775-217">Use herramientas como el [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) para eliminar contenedores de Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a775-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="2a775-218">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="2a775-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="2a775-219">Conjunto de datos de entrada de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-219">Azure blob input dataset</span></span>
<span data-ttu-id="2a775-220">Especifique los nombres del contenedor de blobs, la carpeta y el archivo que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2a775-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="2a775-221">Consulte las [propiedades del conjunto de datos de Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) para más información sobre las propiedades JSON usadas para definir un conjunto de datos de Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="2a775-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="2a775-222">Esta definición usa los siguientes parámetros definidos en la plantilla de parámetros: blobContainer, inputBlobFolder y inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="2a775-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="2a775-223">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="2a775-223">Azure Blob output dataset</span></span>
<span data-ttu-id="2a775-224">Especifique los nombres del contenedor de blobs y la carpeta que contiene los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="2a775-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="2a775-225">Consulte las [propiedades del conjunto de datos de Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) para más información sobre las propiedades JSON usadas para definir un conjunto de datos de Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="2a775-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="2a775-226">Esta definición usa los siguientes parámetros definidos en la plantilla de parámetros: blobContainer y outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="2a775-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="2a775-227">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="2a775-227">Data pipeline</span></span>
<span data-ttu-id="2a775-228">Defina una canalización que transforme los datos mediante la ejecución de un script de Hive en un clúster a petición de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a775-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="2a775-229">Consulte [JSON de canalización](data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos JSON que se usan para definir una canalización en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2a775-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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

## <a name="reuse-the-template"></a><span data-ttu-id="2a775-230">Reutilización de la plantilla</span><span class="sxs-lookup"><span data-stu-id="2a775-230">Reuse the template</span></span>
<span data-ttu-id="2a775-231">En el tutorial, ha creado una plantilla para definir las entidades de Data Factory y una plantilla para pasar valores de parámetros.</span><span class="sxs-lookup"><span data-stu-id="2a775-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="2a775-232">Para usar la misma plantilla para implementar las entidades de Data Factory en distintos entornos, cree un archivo de parámetros para cada entorno y utilícelo al implementarla en ese entorno.</span><span class="sxs-lookup"><span data-stu-id="2a775-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="2a775-233">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2a775-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="2a775-234">Tenga en cuenta que el primer comando usa el archivo de parámetros para el entorno de desarrollo, el segundo para el entorno de prueba y el tercero para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2a775-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="2a775-235">También puede volver a usar la plantilla para llevar a cabo tareas repetidas.</span><span class="sxs-lookup"><span data-stu-id="2a775-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="2a775-236">Por ejemplo, necesita crear muchas factorías de datos con una o varias canalizaciones que implementen la misma lógica, pero cada factoría de datos usa cuentas de Azure Storage y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2a775-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="2a775-237">En este escenario, usa la misma plantilla en el mismo entorno (desarrollo, prueba o producción) con distintos archivos de parámetros para crear factorías de datos.</span><span class="sxs-lookup"><span data-stu-id="2a775-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="2a775-238">Plantilla de Resource Manager para crear una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="2a775-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="2a775-239">Aquí aparece una plantilla de Resource Manager de ejemplo para crear una puerta de enlace lógica en la parte posterior.</span><span class="sxs-lookup"><span data-stu-id="2a775-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="2a775-240">Instale una puerta de enlace en el equipo local o en la máquina virtual de IaaS de Azure y registrar la puerta de enlace con el servicio Data Factory mediante una clave.</span><span class="sxs-lookup"><span data-stu-id="2a775-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="2a775-241">Para más información, consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2a775-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="2a775-242">Esta plantilla crea una factoría de datos denominada GatewayUsingArmDF con una puerta de enlace llamada GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="2a775-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="2a775-243">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2a775-243">See Also</span></span>
| <span data-ttu-id="2a775-244">Tema.</span><span class="sxs-lookup"><span data-stu-id="2a775-244">Topic</span></span> | <span data-ttu-id="2a775-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="2a775-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="2a775-246">Procesos</span><span class="sxs-lookup"><span data-stu-id="2a775-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="2a775-247">Este artículo ayuda a conocer las canalizaciones y actividades de Data Factory de Azure y cómo aprovecharlas para construir flujos de trabajo controlados por datos de un extremo a otro para su escenario o negocio.</span><span class="sxs-lookup"><span data-stu-id="2a775-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="2a775-248">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="2a775-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="2a775-249">Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a775-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="2a775-250">Programación y ejecución con Data Factory</span><span class="sxs-lookup"><span data-stu-id="2a775-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="2a775-251">En este artículo se explican los aspectos de programación y ejecución del modelo de aplicación de Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a775-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="2a775-252">Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="2a775-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="2a775-253">En este artículo se describe cómo supervisar, administrar y depurar las canalizaciones mediante la aplicación de supervisión y administración.</span><span class="sxs-lookup"><span data-stu-id="2a775-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

