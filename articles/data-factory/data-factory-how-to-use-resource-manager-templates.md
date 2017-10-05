---
title: Uso de plantillas de Resource Manager en Data Factory | Microsoft Docs
description: Aprenda a crear y usar plantillas de Azure Resource Manager para crear entidades de Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="f8ec1-103">Uso de plantillas para crear entidades de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f8ec1-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="f8ec1-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f8ec1-104">Overview</span></span>
<span data-ttu-id="f8ec1-105">Cuando utiliza Azure Data Factory para sus necesidades de integración de datos, es posible que tenga que reutilizar el mismo patrón en distintos entornos o implementar la misma tarea repetidamente dentro de la misma solución.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="f8ec1-106">Las plantillas le permiten implementar y administrar estos escenarios de una forma sencilla.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="f8ec1-107">Las plantillas de Azure Data Factory son ideales para los escenarios que implican la reutilización y la repetición.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="f8ec1-108">Imagine una situación en la que una organización tiene 10 plantas de fabricación distribuidas por todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="f8ec1-109">Los registros de cada planta se almacenan en una base de datos de SQL Server local independiente.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="f8ec1-110">La empresa desea crear un único almacén de datos en la nube para análisis ad hoc.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="f8ec1-111">También quiere tener la misma lógica pero diferentes configuraciones para los entornos de desarrollo, prueba y producción.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="f8ec1-112">En este caso, se deberá repetir una tarea dentro del mismo entorno pero con valores diferentes en 10 factorías de datos para cada planta de fabricación.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="f8ec1-113">En efecto, la **repetición** está presente.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="f8ec1-114">La creación de plantillas permite la abstracción de este flujo genérico (es decir, de las canalizaciones que tengan las mismas actividades en cada factoría de datos), pero usa un archivo de parámetros distinto para cada planta de fabricación.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="f8ec1-115">Además, como la organización desea implementar estas 10 factorías de datos varias veces en distintos entornos, las plantillas pueden utilizar esta característica de **reusabilidad** mediante los archivos de parámetros independientes para entornos de desarrollo, prueba y producción.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="f8ec1-116">Creación de plantillas con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8ec1-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="f8ec1-117">Las [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) son una excelente manera de lograr la creación de plantillas en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="f8ec1-118">Las plantillas de Resource Manager definen la infraestructura y la configuración de la solución de Azure mediante un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="f8ec1-119">Como las plantillas de Azure Resource Manager funcionan con todos los servicios de Azure (o la mayoría de ellos), se pueden usar ampliamente para administrar fácilmente todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="f8ec1-120">Consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) para conocer más información acerca de estas plantillas en general.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="f8ec1-121">Tutoriales</span><span class="sxs-lookup"><span data-stu-id="f8ec1-121">Tutorials</span></span>
<span data-ttu-id="f8ec1-122">Consulte los siguientes tutoriales para obtener instrucciones detalladas para crear entidades de Data Factory mediante plantillas de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* <span data-ttu-id="f8ec1-123">[Tutorial: Create a pipeline to copy data by using Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Tutorial: Creación de una canalización para copiar datos mediante el uso de plantillas de Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-123">[Tutorial: Create a pipeline to copy data by using Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)</span></span>
* <span data-ttu-id="f8ec1-124">[Tutorial: Create a pipeline to copy data by using Azure Resource Manager template](data-factory-build-your-first-pipeline.md) (Tutorial: Creación de una canalización para procesar datos mediante el uso de plantillas de Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-124">[Tutorial: Create a pipeline to process data by using Azure Resource Manager template](data-factory-build-your-first-pipeline.md)</span></span>

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="f8ec1-125">Plantillas de Data Factory en GitHub</span><span class="sxs-lookup"><span data-stu-id="f8ec1-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="f8ec1-126">Consulte las siguientes plantillas de inicio rápido de Azure en GitHub:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-126">Check out the following Azure quick start templates on GitHub:</span></span>

* <span data-ttu-id="f8ec1-127">[Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) (Creación de una instancia de Data Factory para copiar datos desde Azure Blob Storage en Azure SQL Database)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-127">[Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)</span></span>
* <span data-ttu-id="f8ec1-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Creación de una instancia de Data Factory con actividad de Hive en un clúster de Azure HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)</span></span>
* <span data-ttu-id="f8ec1-129">[Create a Data factory to copy data from Salesforce to Azure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) (Creación de una instancia de Data Factory para copiar datos desde Salesforce en Azure Blobs)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-129">[Create a Data factory to copy data from Salesforce to Azure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)</span></span>
* <span data-ttu-id="f8ec1-130">[Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob) (Creación de Data Factory que encadena actividades: copia de datos desde un servidor FTP en blobs de Azure, invocación de un script de hive en un clúster de HDInsight a petición para transformar los datos y copia del resultado en Azure SQL Database)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-130">[Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)</span></span>

<span data-ttu-id="f8ec1-131">No dude en compartir sus plantillas de Azure Data Factory en [Inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="f8ec1-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="f8ec1-132">Consulte la [Guía de contribución](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) cuando desarrolle plantillas que se puedan compartir a través de este repositorio.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="f8ec1-133">Las secciones siguientes proporcionan detalles acerca de cómo definir los recursos de Data Factory en una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="f8ec1-134">Definición de recursos de Data Factory en plantillas</span><span class="sxs-lookup"><span data-stu-id="f8ec1-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="f8ec1-135">La plantilla de nivel superior para definir una factoría de datos es:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-135">The top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="f8ec1-136">Definición de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="f8ec1-136">Define data factory</span></span>
<span data-ttu-id="f8ec1-137">Puede definir una factoría de datos en la plantilla de Resource Manager como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="f8ec1-138">El dataFactoryName se define en "variables" como:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="f8ec1-139">Definición de servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="f8ec1-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="f8ec1-140">Consulte [Servicio vinculado de almacenamiento](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [Servicios vinculados de procesos](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para más información acerca de las propiedades JSON para el servicio vinculado específico que desea implementar.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="f8ec1-141">El parámetro "dependsOn" especifica el nombre de la factoría de datos correspondiente.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="f8ec1-142">En la siguiente definición de JSON, se muestra un ejemplo de definición de un servicio vinculado para Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="f8ec1-143">Definición de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="f8ec1-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="f8ec1-144">Consulte [Almacenes de datos que se admiten](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para más información acerca de las propiedades JSON para el tipo de conjunto de datos específico que desea implementar.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="f8ec1-145">Observe que el parámetro "dependsOn" especifica el nombre de la factoría de datos correspondiente y el servicio vinculado de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="f8ec1-146">En la siguiente definición de JSON, se muestra un ejemplo de definición de un tipo de Azure Blob Storage:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="f8ec1-147">Definición de canalizaciones</span><span class="sxs-lookup"><span data-stu-id="f8ec1-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="f8ec1-148">Consulte [Definición de canalizaciones](data-factory-create-pipelines.md#pipeline-json) para más información acerca de las propiedades JSON para definir la canalización específica y las actividades que desea implementar.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="f8ec1-149">Tenga en cuenta que el parámetro "dependsOn" especifica el nombre de la factoría de datos y todos los servicios vinculados o conjuntos de datos correspondientes.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="f8ec1-150">En el siguiente fragmento de código JSON se muestra un ejemplo de una canalización que copia datos de Azure Blob Storage en Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

```JSON
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
        "description": "Copy data frm Azure blob to Azure SQL",
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="f8ec1-151">Parametrización de la plantilla de Data Factory</span><span class="sxs-lookup"><span data-stu-id="f8ec1-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="f8ec1-152">Para obtener los procedimientos recomendados sobre parametrización, consulte el artículo [Procedimientos recomendados para crear plantillas de Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="f8ec1-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="f8ec1-153">Por lo general, se debe minimizar el uso de parámetros, especialmente si se pueden utilizar variables en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="f8ec1-154">Solo proporcione parámetros en los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="f8ec1-155">La configuración varía según el entorno (por ejemplo: desarrollo, prueba y producción)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="f8ec1-156">Secretos (por ejemplo, las contraseñas)</span><span class="sxs-lookup"><span data-stu-id="f8ec1-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="f8ec1-157">Si necesita extraer los secretos de [Azure Key Vault](../key-vault/key-vault-get-started.md) al implementar las entidades de Azure Data Factory mediante plantillas, especifique el **almacén de claves** y el **nombre secreto** tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8ec1-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="f8ec1-158">Aunque todavía no se admite la exportación de plantillas para factorías de datos ya existentes, esto está en proyecto.</span><span class="sxs-lookup"><span data-stu-id="f8ec1-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
