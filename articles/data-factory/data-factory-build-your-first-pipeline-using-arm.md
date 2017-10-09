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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="3619f-103">Tutorial: Compilación de la primera Data Factory de Azure con la plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3619f-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3619f-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3619f-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="3619f-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3619f-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="3619f-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3619f-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="3619f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3619f-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="3619f-108">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3619f-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="3619f-109">API DE REST</span><span class="sxs-lookup"><span data-stu-id="3619f-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="3619f-110">En este artículo, use un toocreate de plantilla de Azure Resource Manager su primera factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="3619f-111">tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="3619f-112">canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="3619f-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="3619f-113">Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce.</span><span class="sxs-lookup"><span data-stu-id="3619f-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="3619f-114">canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="3619f-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="3619f-115">canalización de datos de Hello en este tutorial transforma los datos de salida de tooproduce de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="3619f-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="3619f-116">Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3619f-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="3619f-117">canalización de Hello en este tutorial tiene sólo una actividad de tipo: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="3619f-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="3619f-118">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="3619f-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="3619f-119">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="3619f-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="3619f-120">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="3619f-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3619f-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3619f-121">Prerequisites</span></span>
* <span data-ttu-id="3619f-122">Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="3619f-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="3619f-123">Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall versión más reciente de PowerShell de Azure en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3619f-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="3619f-124">Vea [creación de plantillas de administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn acerca de las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3619f-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="3619f-125">Apartados de este tutorial</span><span class="sxs-lookup"><span data-stu-id="3619f-125">In this tutorial</span></span>
| <span data-ttu-id="3619f-126">Entidad</span><span class="sxs-lookup"><span data-stu-id="3619f-126">Entity</span></span> | <span data-ttu-id="3619f-127">Description</span><span class="sxs-lookup"><span data-stu-id="3619f-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3619f-128">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3619f-128">Azure Storage linked service</span></span> |<span data-ttu-id="3619f-129">Vincula la factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="3619f-130">Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="3619f-131">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3619f-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="3619f-132">Vincula un generador de datos a petición toohello de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3619f-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="3619f-133">clúster de Hola se crea automáticamente para usted tooprocess datos y se elimina después de que se realiza un procesamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="3619f-134">Conjunto de datos de entrada de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="3619f-134">Azure Blob input dataset</span></span> |<span data-ttu-id="3619f-135">Hace una referencia de servicio de almacenamiento de Azure vinculada toohello.</span><span class="sxs-lookup"><span data-stu-id="3619f-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="3619f-136">Hello servicio vinculado hace referencia tooan cuenta de almacenamiento de Azure y conjunto de datos de Blob de Azure Hola especifica Hola contenedor, carpeta y nombre de archivo en el almacenamiento de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="3619f-137">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="3619f-137">Azure Blob output dataset</span></span> |<span data-ttu-id="3619f-138">Hace una referencia de servicio de almacenamiento de Azure vinculada toohello.</span><span class="sxs-lookup"><span data-stu-id="3619f-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="3619f-139">Hello servicio vinculado hace referencia tooan cuenta de almacenamiento de Azure y conjunto de datos de Blob de Azure de hello especifica Hola contenedor, carpeta y nombre de archivo en el almacenamiento de Hola que contiene datos de salida de saludo.</span><span class="sxs-lookup"><span data-stu-id="3619f-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="3619f-140">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="3619f-140">Data pipeline</span></span> |<span data-ttu-id="3619f-141">canalización de Hello tiene una actividad de tipo HDInsightHive, que consume el conjunto de datos de entrada de Hola y genera el conjunto de datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="3619f-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="3619f-142">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="3619f-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="3619f-143">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="3619f-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="3619f-144">Hay dos tipos de actividades: [actividades de movimiento de datos](data-factory-data-movement-activities.md) y [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3619f-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="3619f-145">En este tutorial se crea una canalización con una actividad (actividad de Hive).</span><span class="sxs-lookup"><span data-stu-id="3619f-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="3619f-146">Hello siguiente sección proporciona Hola completa el Administrador de recursos plantilla para definir las entidades de la factoría de datos para que pueda ejecutar rápidamente a través de la plantilla de Hola Hola tutorial y prueba.</span><span class="sxs-lookup"><span data-stu-id="3619f-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="3619f-147">toounderstand cómo se define cada entidad de la factoría de datos, vea [las entidades de la factoría de datos de plantilla de hello](#data-factory-entities-in-the-template) sección.</span><span class="sxs-lookup"><span data-stu-id="3619f-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="3619f-148">Plantilla JSON de Data Factory</span><span class="sxs-lookup"><span data-stu-id="3619f-148">Data Factory JSON template</span></span>
<span data-ttu-id="3619f-149">Hola de plantilla de administrador de recursos nivel superior para definir una factoría de datos es:</span><span class="sxs-lookup"><span data-stu-id="3619f-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="3619f-150">Cree un archivo JSON denominado **ADFTutorialARM.json** en **C:\ADFGetStarted** carpeta con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="3619f-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

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
> <span data-ttu-id="3619f-151">Puede encontrar otro ejemplo de plantilla de Resource Manager para crear una factoría de datos de Azure en [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Tutorial: Creación de una canalización con la actividad de copia mediante una plantilla de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3619f-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="3619f-152">Parámetros JSON</span><span class="sxs-lookup"><span data-stu-id="3619f-152">Parameters JSON</span></span>
<span data-ttu-id="3619f-153">Cree un archivo JSON denominado **ADFTutorialARM Parameters.json** que contiene parámetros de plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3619f-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3619f-154">Especificar nombre de Hola y la clave de la cuenta de almacenamiento de Azure para hello **storageAccountName** y **storageAccountKey** parámetros en este archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="3619f-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="3619f-155">Puede tener archivos JSON de parámetro independiente para el desarrollo, pruebas y entornos de producción que puede usar con Hola misma plantilla JSON de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="3619f-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="3619f-156">Al usar un script de PowerShell, puede automatizar la implementación de las entidades de Data Factory en estos entornos.</span><span class="sxs-lookup"><span data-stu-id="3619f-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="3619f-157">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="3619f-157">Create data factory</span></span>
1. <span data-ttu-id="3619f-158">Iniciar **Azure PowerShell** y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3619f-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="3619f-159">Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="3619f-160">Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="3619f-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="3619f-161">Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.</span><span class="sxs-lookup"><span data-stu-id="3619f-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="3619f-162">Esta suscripción debe ser Hola igual que la que usó en el portal de Azure Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="3619f-163">Ejecute hello después de entidades de factoría de datos de toodeploy de comando mediante la plantilla de administrador de recursos de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="3619f-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="3619f-164">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="3619f-164">Monitor pipeline</span></span>
1. <span data-ttu-id="3619f-165">Después de iniciar sesión toohello [portal de Azure](https://portal.azure.com/), haga clic en **examinar** y seleccione **factorías de datos**.</span><span class="sxs-lookup"><span data-stu-id="3619f-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="3619f-166">![Examinar-&gt;Factorías de datos](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="3619f-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="3619f-167">Hola **factorías de datos** hoja, haga clic en la factoría de datos de hello (**TutorialFactoryARM**) que ha creado.</span><span class="sxs-lookup"><span data-stu-id="3619f-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="3619f-168">Hola **factoría de datos** hoja de la factoría de datos, haga clic en **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="3619f-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Icono Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="3619f-170">Hola **vista de diagrama**, verá información general de las canalizaciones de Hola y conjuntos de datos utilizan en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3619f-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Vista de diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="3619f-172">Hola vista de diagrama, haga doble clic en el conjunto de datos de hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="3619f-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="3619f-173">Vea dicho sector Hola que se está procesando actualmente.</span><span class="sxs-lookup"><span data-stu-id="3619f-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="3619f-175">Cuando se realiza el procesamiento, verá que el segmento de hello en **listo** estado.</span><span class="sxs-lookup"><span data-stu-id="3619f-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="3619f-176">La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="3619f-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="3619f-177">Por consiguiente, esperan Hola canalización tootake **aproximadamente 30 minutos** tooprocess Hola segmento.</span><span class="sxs-lookup"><span data-stu-id="3619f-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="3619f-179">Cuando se encuentra el segmento de hello en **listo** de estado, compruebe hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="3619f-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="3619f-180">Vea [supervisar conjuntos de datos y canalización](data-factory-monitor-manage-pipelines.md) para obtener instrucciones sobre cómo canalización de toouse hello Azure hojas portal toomonitor hello y conjuntos de datos ha creado en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3619f-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="3619f-181">También puede utilizar toomonitor de supervisar y administrar aplicaciones sus canalizaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="3619f-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="3619f-182">Vea [supervisar y administrar las canalizaciones de factoría de datos de Azure mediante la aplicación de supervisión](data-factory-monitor-manage-app.md) para obtener más información sobre el uso de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3619f-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3619f-183">archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente.</span><span class="sxs-lookup"><span data-stu-id="3619f-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="3619f-184">Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="3619f-185">Entidades de generador de datos en la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="3619f-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="3619f-186">Definición de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="3619f-186">Define data factory</span></span>
<span data-ttu-id="3619f-187">Defina una factoría de datos en la plantilla de administrador de recursos de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="3619f-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="3619f-188">Hola dataFactoryName se define como:</span><span class="sxs-lookup"><span data-stu-id="3619f-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="3619f-189">Es una cadena única en función de identificador de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="3619f-190">Definición de las entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="3619f-190">Defining Data Factory entities</span></span>
<span data-ttu-id="3619f-191">Hello siguientes entidades de la factoría de datos definidas en hello JSON plantilla:</span><span class="sxs-lookup"><span data-stu-id="3619f-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="3619f-192">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="3619f-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="3619f-193">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3619f-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="3619f-194">Conjunto de datos de entrada de blob de Azure:</span><span class="sxs-lookup"><span data-stu-id="3619f-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="3619f-195">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="3619f-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="3619f-196">Canalización de datos con una actividad de copia</span><span class="sxs-lookup"><span data-stu-id="3619f-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="3619f-197">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3619f-197">Azure Storage linked service</span></span>
<span data-ttu-id="3619f-198">Especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure en esta sección.</span><span class="sxs-lookup"><span data-stu-id="3619f-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="3619f-199">Vea [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="3619f-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="3619f-200">Hola **connectionString** usa Hola parámetros storageAccountName y storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="3619f-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="3619f-201">valores de Hello para estos parámetros pasados mediante el uso de un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="3619f-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="3619f-202">definición de Hello también usa las variables: azureStroageLinkedService y dataFactoryName se definen en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="3619f-203">Servicio vinculado a petición de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3619f-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="3619f-204">Vea [servicios vinculados de proceso](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) un servicio vinculado de HDInsight a petición del artículo para obtener más información acerca de toodefine de propiedades que se usan JSON.</span><span class="sxs-lookup"><span data-stu-id="3619f-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="3619f-205">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="3619f-205">Note hello following points:</span></span> 

* <span data-ttu-id="3619f-206">Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello por encima de JSON.</span><span class="sxs-lookup"><span data-stu-id="3619f-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="3619f-207">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="3619f-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="3619f-208">Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="3619f-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="3619f-209">Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="3619f-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="3619f-210">clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="3619f-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="3619f-211">HDInsight no elimine este contenedor cuando se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="3619f-212">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="3619f-212">This behavior is by design.</span></span> <span data-ttu-id="3619f-213">Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que un segmento necesario toobe procesado a menos que haya un clúster existente en vivo (**timeToLive**) y se elimina cuando se realiza un procesamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="3619f-214">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="3619f-215">Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="3619f-216">nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="3619f-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="3619f-217">Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="3619f-218">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="3619f-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="3619f-219">Conjunto de datos de entrada de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="3619f-219">Azure blob input dataset</span></span>
<span data-ttu-id="3619f-220">Especificar nombres de Hola de contenedor de blobs, carpeta y archivo que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3619f-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="3619f-221">Vea [propiedades de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="3619f-222">Esta definición usa Hola parámetros definidos en la plantilla de parámetro siguientes: blobContainer, inputBlobFolder y inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="3619f-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="3619f-223">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="3619f-223">Azure Blob output dataset</span></span>
<span data-ttu-id="3619f-224">Especificar nombres de Hola de contenedor de blob y la carpeta que contiene los datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="3619f-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="3619f-225">Vea [propiedades de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="3619f-226">Esta definición usa Hola parámetros definidos en la plantilla del parámetro hello siguientes: blobContainer y outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="3619f-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="3619f-227">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="3619f-227">Data pipeline</span></span>
<span data-ttu-id="3619f-228">Defina una canalización que transforme los datos mediante la ejecución de un script de Hive en un clúster a petición de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3619f-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="3619f-229">Vea [JSON de canalización](data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos que se usan de JSON toodefine una canalización en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3619f-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="3619f-230">Plantilla de reutilización Hola</span><span class="sxs-lookup"><span data-stu-id="3619f-230">Reuse hello template</span></span>
<span data-ttu-id="3619f-231">En el tutorial de hello, ha creado una plantilla para definir las entidades de la factoría de datos y una plantilla para pasar valores de parámetros.</span><span class="sxs-lookup"><span data-stu-id="3619f-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="3619f-232">toouse Hola mismos entornos plantilla toodeploy factoría de datos entidades toodifferent, cree un archivo de parámetros para cada entorno y utilizarlo al implementar el entorno de toothat.</span><span class="sxs-lookup"><span data-stu-id="3619f-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="3619f-233">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3619f-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="3619f-234">Observe que Hola el primer parámetro de comando usa de archivos para el entorno de desarrollo de hello, otra para el entorno de prueba de Hola y Hola una tercera para entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="3619f-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="3619f-235">También puede volver a usar Hola plantilla tooperform tareas que se repiten.</span><span class="sxs-lookup"><span data-stu-id="3619f-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="3619f-236">Por ejemplo, necesita toocreate muchos generadores de datos con uno o más de las canalizaciones que implementan Hola misma lógica, pero cada almacenamiento de Azure diferentes datos generador utiliza y las cuentas de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="3619f-237">En este escenario, utilice Hola misma plantilla Hola mismo entorno (desarrollo, prueba o producción) con parámetros diferentes archivos toocreate factorías de datos.</span><span class="sxs-lookup"><span data-stu-id="3619f-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="3619f-238">Plantilla de Resource Manager para crear una puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="3619f-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="3619f-239">Aquí es una plantilla de administrador de recursos de ejemplo para crear una puerta de enlace lógico Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3619f-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="3619f-240">Instala una puerta de enlace en el equipo local o la máquina virtual de IaaS de Azure y registrar la puerta de enlace de hello con servicio de factoría de datos mediante una clave.</span><span class="sxs-lookup"><span data-stu-id="3619f-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="3619f-241">Para más información, consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="3619f-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="3619f-242">Esta plantilla crea una factoría de datos denominada GatewayUsingArmDF con una puerta de enlace llamada GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="3619f-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="3619f-243">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3619f-243">See Also</span></span>
| <span data-ttu-id="3619f-244">Tema.</span><span class="sxs-lookup"><span data-stu-id="3619f-244">Topic</span></span> | <span data-ttu-id="3619f-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="3619f-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="3619f-246">Procesos</span><span class="sxs-lookup"><span data-stu-id="3619f-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="3619f-247">En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa.</span><span class="sxs-lookup"><span data-stu-id="3619f-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="3619f-248">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="3619f-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="3619f-249">Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="3619f-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="3619f-250">Programación y ejecución con Data Factory</span><span class="sxs-lookup"><span data-stu-id="3619f-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="3619f-251">En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3619f-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="3619f-252">Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="3619f-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="3619f-253">Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3619f-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

