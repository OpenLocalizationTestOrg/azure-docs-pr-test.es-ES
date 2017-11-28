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
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="d7593-104">Tutorial: Utilizar el Administrador de recursos de Azure plantilla toocreate una toocopy de datos de canalización de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="d7593-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7593-105">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d7593-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="d7593-106">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="d7593-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="d7593-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d7593-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="d7593-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d7593-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="d7593-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7593-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="d7593-110">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d7593-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="d7593-111">API DE REST</span><span class="sxs-lookup"><span data-stu-id="d7593-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="d7593-112">API de .NET</span><span class="sxs-lookup"><span data-stu-id="d7593-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="d7593-113">Este tutorial muestra cómo toouse una toocreate de plantilla de Azure Resource Manager un generador de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="d7593-114">canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="d7593-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="d7593-115">No transforma datos de salida de tooproduce de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="d7593-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="d7593-116">Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="d7593-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="d7593-117">En este tutorial, creará una canalización con una actividad en ella: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="d7593-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="d7593-118">actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos.</span><span class="sxs-lookup"><span data-stu-id="d7593-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="d7593-119">Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d7593-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="d7593-120">actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="d7593-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="d7593-121">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d7593-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="d7593-122">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="d7593-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="d7593-123">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="d7593-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="d7593-124">Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="d7593-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="d7593-125">canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="d7593-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="d7593-126">Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="d7593-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d7593-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d7593-127">Prerequisites</span></span>
* <span data-ttu-id="d7593-128">Vaya a través de [Tutorial de introducción y los requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hello completa y **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="d7593-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="d7593-129">Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall versión más reciente de PowerShell de Azure en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d7593-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="d7593-130">En este tutorial, usará entidades de factoría de datos de toodeploy de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7593-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="d7593-131">(opcional) Vea [creación de plantillas de administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn acerca de las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7593-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="d7593-132">Apartados de este tutorial</span><span class="sxs-lookup"><span data-stu-id="d7593-132">In this tutorial</span></span>
<span data-ttu-id="d7593-133">En este tutorial, creará una factoría de datos con hello siguiendo las entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="d7593-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="d7593-134">Entidad</span><span class="sxs-lookup"><span data-stu-id="d7593-134">Entity</span></span> | <span data-ttu-id="d7593-135">Description</span><span class="sxs-lookup"><span data-stu-id="d7593-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7593-136">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d7593-136">Azure Storage linked service</span></span> |<span data-ttu-id="d7593-137">Vincula la factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="d7593-138">Almacenamiento de Azure es el almacén de datos de origen de Hola y base de datos de SQL Azure es el almacén de datos de receptor de hello para la actividad de copia de hello en tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="d7593-139">Especifica la cuenta de almacenamiento de Hola que contiene los datos de entrada de hello para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="d7593-140">Servicio vinculado a Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d7593-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="d7593-141">Vincula la factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="d7593-142">Especifica la base de datos de SQL Azure de Hola que contiene los datos de salida de hello para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="d7593-143">Conjunto de datos de entrada de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="d7593-143">Azure Blob input dataset</span></span> |<span data-ttu-id="d7593-144">Hace una referencia de servicio de almacenamiento de Azure vinculada toohello.</span><span class="sxs-lookup"><span data-stu-id="d7593-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="d7593-145">Hello servicio vinculado hace referencia tooan cuenta de almacenamiento de Azure y conjunto de datos de Blob de Azure Hola especifica Hola contenedor, carpeta y nombre de archivo en el almacenamiento de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="d7593-146">Conjunto de datos de salida SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="d7593-146">Azure SQL output dataset</span></span> |<span data-ttu-id="d7593-147">Hace una referencia de servicio de SQL Azure vinculado toohello.</span><span class="sxs-lookup"><span data-stu-id="d7593-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="d7593-148">servicio vinculado de SQL Azure de Hola hace referencia tooan servidor SQL de Azure y conjunto de datos de SQL Azure Hola especifica el nombre de Hola de tabla de Hola que contiene los datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="d7593-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="d7593-149">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="d7593-149">Data pipeline</span></span> |<span data-ttu-id="d7593-150">canalización de Hello tiene una actividad de escriba Copy que toma el conjunto de datos de blob de Azure de hello como entrada y Hola conjunto de datos de SQL Azure como una salida.</span><span class="sxs-lookup"><span data-stu-id="d7593-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="d7593-151">actividad de copia de Hello copia datos de una tabla de tooa de blobs de Azure en la base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="d7593-152">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="d7593-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="d7593-153">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="d7593-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="d7593-154">Hay dos tipos de actividades: [actividades de movimiento de datos](data-factory-data-movement-activities.md) y [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d7593-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="d7593-155">En este tutorial, va a crear una canalización con una actividad (actividad de copia).</span><span class="sxs-lookup"><span data-stu-id="d7593-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copiar blobs de Azure tooAzure base de datos SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="d7593-157">Hello siguiente sección proporciona Hola completa el Administrador de recursos plantilla para definir las entidades de la factoría de datos para que pueda ejecutar rápidamente a través de la plantilla de Hola Hola tutorial y prueba.</span><span class="sxs-lookup"><span data-stu-id="d7593-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="d7593-158">toounderstand cómo se define cada entidad de la factoría de datos, vea [las entidades de la factoría de datos de plantilla de hello](#data-factory-entities-in-the-template) sección.</span><span class="sxs-lookup"><span data-stu-id="d7593-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="d7593-159">Plantilla JSON de Data Factory</span><span class="sxs-lookup"><span data-stu-id="d7593-159">Data Factory JSON template</span></span>
<span data-ttu-id="d7593-160">Hola de plantilla de administrador de recursos nivel superior para definir una factoría de datos es:</span><span class="sxs-lookup"><span data-stu-id="d7593-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="d7593-161">Cree un archivo JSON denominado **ADFCopyTutorialARM.json** en **C:\ADFGetStarted** carpeta con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="d7593-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

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

## <a name="parameters-json"></a><span data-ttu-id="d7593-162">Parámetros JSON</span><span class="sxs-lookup"><span data-stu-id="d7593-162">Parameters JSON</span></span>
<span data-ttu-id="d7593-163">Cree un archivo JSON denominado **ADFCopyTutorialARM Parameters.json** que contiene parámetros de plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7593-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d7593-164">Especifique el nombre y la clave de la cuenta de Azure Storage para los parámetros storageAccountName y storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="d7593-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="d7593-165">Especifique el servidor de Azure SQL, la base de datos, el usuario y la contraseña de los parámetros sqlServerName, databaseName, sqlServerUserName y sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="d7593-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

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
> <span data-ttu-id="d7593-166">Puede tener archivos JSON de parámetro independiente para el desarrollo, pruebas y entornos de producción que puede usar con Hola misma plantilla JSON de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="d7593-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="d7593-167">Al usar un script de PowerShell, puede automatizar la implementación de las entidades de Data Factory en estos entornos.</span><span class="sxs-lookup"><span data-stu-id="d7593-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="d7593-168">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="d7593-168">Create data factory</span></span>
1. <span data-ttu-id="d7593-169">Iniciar **Azure PowerShell** y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d7593-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="d7593-170">Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="d7593-171">Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="d7593-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="d7593-172">Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.</span><span class="sxs-lookup"><span data-stu-id="d7593-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="d7593-173">Ejecute hello después de entidades de factoría de datos de toodeploy de comando mediante la plantilla de administrador de recursos de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="d7593-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="d7593-174">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="d7593-174">Monitor pipeline</span></span>

1. <span data-ttu-id="d7593-175">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="d7593-176">Haga clic en **factorías de datos** Hola izquierdo menú (o) haga clic en **más servicios** y haga clic en **factorías de datos** en **INTELLIGENCE + análisis** categoría.</span><span class="sxs-lookup"><span data-stu-id="d7593-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Menú Factorías de datos](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="d7593-178">Hola **factorías de datos** página, buscar y encontrar su factoría de datos (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="d7593-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Búsqueda de la factoría de datos](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="d7593-180">Haga clic en su factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-180">Click your Azure data factory.</span></span> <span data-ttu-id="d7593-181">Ver página principal de Hola de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-181">You see hello home page for hello data factory.</span></span>
   
    ![Página principal de la factoría de datos](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="d7593-183">Siga las instrucciones de [supervisar conjuntos de datos y canalización](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor canalización de Hola y conjuntos de datos ha creado en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d7593-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="d7593-184">Actualmente, Visual Studio no permite supervisar canalizaciones de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d7593-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="d7593-185">Cuando se encuentra un segmento en hello **listo** estado, compruebe que los datos de hello están toohello copiado **emp** tabla de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="d7593-186">Para obtener más información sobre cómo canalización toomonitor de toouse hojas de portal de Azure y conjuntos de datos ha creado en este tutorial, vea [supervisar conjuntos de datos y canalización](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="d7593-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="d7593-187">Para obtener más información sobre cómo toouse toomonitor de hello Monitor & Administrar aplicación los datos canalizaciones, consulte [supervisar y administrar las canalizaciones de factoría de datos de Azure mediante la aplicación de supervisión](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="d7593-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="d7593-188">Entidades de generador de datos en la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="d7593-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="d7593-189">Definición de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="d7593-189">Define data factory</span></span>
<span data-ttu-id="d7593-190">Defina una factoría de datos en la plantilla de administrador de recursos de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="d7593-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="d7593-191">Hola dataFactoryName se define como:</span><span class="sxs-lookup"><span data-stu-id="d7593-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="d7593-192">Es una cadena única en función de identificador de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="d7593-193">Definición de las entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="d7593-193">Defining Data Factory entities</span></span>
<span data-ttu-id="d7593-194">Hello siguientes entidades de la factoría de datos definidas en hello JSON plantilla:</span><span class="sxs-lookup"><span data-stu-id="d7593-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="d7593-195">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="d7593-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="d7593-196">Servicio vinculado de Azure SQL</span><span class="sxs-lookup"><span data-stu-id="d7593-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="d7593-197">Conjunto de datos del blob de Azure</span><span class="sxs-lookup"><span data-stu-id="d7593-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="d7593-198">Conjunto de datos de Azure SQL</span><span class="sxs-lookup"><span data-stu-id="d7593-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="d7593-199">Canalización de datos con una actividad de copia</span><span class="sxs-lookup"><span data-stu-id="d7593-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="d7593-200">Servicio vinculado de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d7593-200">Azure Storage linked service</span></span>
<span data-ttu-id="d7593-201">Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="d7593-202">Crea un contenedor y cargar la cuenta de almacenamiento de datos toothis como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d7593-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="d7593-203">Especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure en esta sección.</span><span class="sxs-lookup"><span data-stu-id="d7593-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="d7593-204">Vea [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="d7593-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="d7593-205">Hola connectionString utiliza los parámetros de storageAccountName y storageAccountKey de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="d7593-206">valores de Hello para estos parámetros pasados mediante el uso de un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="d7593-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="d7593-207">definición de Hello también usa las variables: azureStroageLinkedService y dataFactoryName se definen en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="d7593-208">Servicio vinculado a Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d7593-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="d7593-209">AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="d7593-210">datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="d7593-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="d7593-211">Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d7593-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="d7593-212">Especifique el nombre del servidor SQL Azure hello, nombre de base de datos, nombre de usuario y contraseña de usuario en esta sección.</span><span class="sxs-lookup"><span data-stu-id="d7593-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="d7593-213">Vea [servicio vinculado de SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obtener más información acerca de toodefine de propiedades que se usan JSON SQL Azure servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="d7593-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="d7593-214">Hola connectionString usa sqlServerName, databaseName, sqlServerUserName y parámetros de sqlServerPassword cuyos valores se pasan mediante un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="d7593-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="d7593-215">Hello definición también utiliza Hola siguientes variables de plantilla de hello: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="d7593-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="d7593-216">Conjunto de datos del blob de Azure</span><span class="sxs-lookup"><span data-stu-id="d7593-216">Azure blob dataset</span></span>
<span data-ttu-id="d7593-217">servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="d7593-218">En la definición de conjunto de datos de blob de Azure, especifique los nombres de contenedor de blobs, carpeta y archivo que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="d7593-219">Vea [propiedades de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="d7593-220">Conjunto de datos de Azure SQL</span><span class="sxs-lookup"><span data-stu-id="d7593-220">Azure SQL dataset</span></span>
<span data-ttu-id="d7593-221">Especificar nombre de Hola de tabla de hello en la base de datos de SQL Azure de Hola que contiene los datos de hello copiado desde Hola almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="d7593-222">Vea [propiedades de conjunto de datos de SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) para obtener más información sobre JSON toodefine de propiedades que se usan un conjunto de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="d7593-223">Canalización de datos</span><span class="sxs-lookup"><span data-stu-id="d7593-223">Data pipeline</span></span>
<span data-ttu-id="d7593-224">Definir una canalización que copia datos de conjunto de datos de hello Azure blob dataset toohello SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d7593-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="d7593-225">Vea [JSON de canalización](data-factory-create-pipelines.md#pipeline-json) para obtener descripciones de elementos que se usan de JSON toodefine una canalización en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d7593-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="d7593-226">Plantilla de reutilización Hola</span><span class="sxs-lookup"><span data-stu-id="d7593-226">Reuse hello template</span></span>
<span data-ttu-id="d7593-227">En el tutorial de hello, ha creado una plantilla para definir las entidades de la factoría de datos y una plantilla para pasar valores de parámetros.</span><span class="sxs-lookup"><span data-stu-id="d7593-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="d7593-228">canalización de Hello copia datos de una cuenta de almacenamiento de Azure tooan de SQL Azure de base de datos especificado a través de parámetros.</span><span class="sxs-lookup"><span data-stu-id="d7593-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="d7593-229">toouse Hola mismos entornos plantilla toodeploy factoría de datos entidades toodifferent, cree un archivo de parámetros para cada entorno y utilizarlo al implementar el entorno de toothat.</span><span class="sxs-lookup"><span data-stu-id="d7593-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="d7593-230">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d7593-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="d7593-231">Observe que Hola el primer parámetro de comando usa de archivos para el entorno de desarrollo de hello, otra para el entorno de prueba de Hola y Hola una tercera para entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="d7593-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="d7593-232">También puede volver a usar Hola plantilla tooperform tareas que se repiten.</span><span class="sxs-lookup"><span data-stu-id="d7593-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="d7593-233">Por ejemplo, necesita toocreate muchos generadores de datos con una o más de las canalizaciones que implementan Hola mismo lógica, pero cada factoría de datos utiliza diferentes cuentas de almacenamiento y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d7593-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="d7593-234">En este escenario, utilice Hola misma plantilla Hola mismo entorno (desarrollo, prueba o producción) con parámetros diferentes archivos toocreate factorías de datos.</span><span class="sxs-lookup"><span data-stu-id="d7593-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="d7593-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7593-235">Next steps</span></span>
<span data-ttu-id="d7593-236">En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="d7593-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="d7593-237">Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello:</span><span class="sxs-lookup"><span data-stu-id="d7593-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="d7593-238">toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7593-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
