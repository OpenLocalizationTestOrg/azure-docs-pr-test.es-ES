---
title: "plantillas de administrador de recursos de aaaUse de factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y use el Administrador de recursos de Azure plantillas toocreate factoría de datos entidades."
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
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="bc95b-103">Usar plantillas toocreate Data Factory de Azure entidades</span><span class="sxs-lookup"><span data-stu-id="bc95b-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="bc95b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="bc95b-104">Overview</span></span>
<span data-ttu-id="bc95b-105">Durante el uso de Data Factory de Azure para sus necesidades de integración de datos, es probable que se encuentre reutilizar Hola mismo patrón en distintos entornos o implementar Hola igual de tareas repetidamente dentro de hello misma solución.</span><span class="sxs-lookup"><span data-stu-id="bc95b-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="bc95b-106">Las plantillas le permiten implementar y administrar estos escenarios de una forma sencilla.</span><span class="sxs-lookup"><span data-stu-id="bc95b-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="bc95b-107">Las plantillas de Azure Data Factory son ideales para los escenarios que implican la reutilización y la repetición.</span><span class="sxs-lookup"><span data-stu-id="bc95b-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="bc95b-108">Considere la posibilidad de situación Hola donde una organización tiene 10 plantas de fabricación a través de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="bc95b-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="bc95b-109">registros de Hola desde cada planta se almacenan en una base de datos de SQL Server local independiente.</span><span class="sxs-lookup"><span data-stu-id="bc95b-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="bc95b-110">empresa Hola quiere toobuild un único almacén en la nube de Hola para análisis ad hoc.</span><span class="sxs-lookup"><span data-stu-id="bc95b-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="bc95b-111">También quiere toohave Hola misma lógica pero diferentes configuraciones para los entornos de desarrollo, prueba y producción.</span><span class="sxs-lookup"><span data-stu-id="bc95b-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="bc95b-112">En este caso, una tarea debe toobe repite dentro Hola mismo entorno, pero con valores diferentes a través de Hola 10 factorías de datos para cada planta de fabricación.</span><span class="sxs-lookup"><span data-stu-id="bc95b-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="bc95b-113">En efecto, la **repetición** está presente.</span><span class="sxs-lookup"><span data-stu-id="bc95b-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="bc95b-114">Creación de plantillas permite abstracción Hola de este flujo genérico (es decir, canalizaciones tener Hola mismas actividades en cada factoría de datos), pero usa un archivo de parámetros independiente para cada planta de fabricación.</span><span class="sxs-lookup"><span data-stu-id="bc95b-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="bc95b-115">Además, como Hola organización quiere toodeploy estos generadores de 10 datos varias veces en distintos entornos, las plantillas pueden usar esto **reusabilidad** mediante el uso de archivos de parámetro independiente para el desarrollo, prueba, y entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="bc95b-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="bc95b-116">Creación de plantillas con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc95b-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="bc95b-117">[Plantillas de administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md#template-deployment) son una creación de plantillas de tooachieve excelente manera de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc95b-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="bc95b-118">Las plantillas de administrador de recursos definen infraestructura hello y la configuración de la solución de Azure a través de un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="bc95b-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="bc95b-119">Dado que las plantillas de Azure Resource Manager funcionan con la mayoría o todos los servicios de Azure, se puede usar ampliamente tooeasily administrar todos los recursos de sus activos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc95b-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="bc95b-120">Vea [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md) toolearn más información sobre Hola plantillas del Administrador de recursos en general.</span><span class="sxs-lookup"><span data-stu-id="bc95b-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="bc95b-121">Tutoriales</span><span class="sxs-lookup"><span data-stu-id="bc95b-121">Tutorials</span></span>
<span data-ttu-id="bc95b-122">Vea Hola siguientes tutoriales para entidades de instrucciones paso a paso toocreate factoría de datos mediante plantillas de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="bc95b-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="bc95b-123">Tutorial: Crear una canalización de datos de toocopy mediante el uso de la plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="bc95b-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="bc95b-124">Tutorial: Crear una canalización de datos de tooprocess mediante el uso de la plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="bc95b-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="bc95b-125">Plantillas de Data Factory en GitHub</span><span class="sxs-lookup"><span data-stu-id="bc95b-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="bc95b-126">Extraer del repositorio Hola siguiendo las plantillas de inicio rápido de Azure en GitHub:</span><span class="sxs-lookup"><span data-stu-id="bc95b-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="bc95b-127">Crear datos generador toocopy los datos de almacenamiento de blobs de Azure tooAzure base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="bc95b-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* <span data-ttu-id="bc95b-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Creación de una instancia de Data Factory con actividad de Hive en un clúster de Azure HDInsight)</span><span class="sxs-lookup"><span data-stu-id="bc95b-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)</span></span>
* [<span data-ttu-id="bc95b-129">Crear datos generador toocopy los datos de Salesforce tooAzure Blobs</span><span class="sxs-lookup"><span data-stu-id="bc95b-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="bc95b-130">Crear un generador de datos que se vincula las actividades: copia datos de un servidor FTP tooAzure Blobs, invoca un script de hive en un datos a petición HDInsight clúster tootransform hello y copia el resultado en la base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bc95b-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="bc95b-131">Cree tooshare libre sus plantillas de Data Factory de Azure en [inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="bc95b-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="bc95b-132">Consulte toohello [Guía de colaboración](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) durante el desarrollo de plantillas que se pueden compartir a través de este repositorio.</span><span class="sxs-lookup"><span data-stu-id="bc95b-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="bc95b-133">Hola las secciones siguientes proporciona detalles acerca de cómo definir recursos de la factoría de datos en una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="bc95b-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="bc95b-134">Definición de recursos de Data Factory en plantillas</span><span class="sxs-lookup"><span data-stu-id="bc95b-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="bc95b-135">plantilla de nivel superior de Hola para definir una factoría de datos es:</span><span class="sxs-lookup"><span data-stu-id="bc95b-135">hello top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="bc95b-136">Definición de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="bc95b-136">Define data factory</span></span>
<span data-ttu-id="bc95b-137">Defina una factoría de datos en la plantilla de administrador de recursos de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bc95b-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="bc95b-138">Hola dataFactoryName se define en "variables" como:</span><span class="sxs-lookup"><span data-stu-id="bc95b-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="bc95b-139">Definición de servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="bc95b-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="bc95b-140">Vea [servicio vinculado de almacenamiento](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [servicios vinculados de proceso](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obtener más información acerca de las propiedades JSON de Hola para servicio vinculado específico de hello desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bc95b-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="bc95b-141">parámetro de "dependsOn" Hello especifica el nombre de la factoría de datos correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc95b-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="bc95b-142">Se muestra un ejemplo de definición de un servicio vinculado para el almacenamiento de Azure en hello después de la definición de JSON:</span><span class="sxs-lookup"><span data-stu-id="bc95b-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="bc95b-143">Definición de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="bc95b-143">Define datasets</span></span>

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
<span data-ttu-id="bc95b-144">Consulte demasiado[admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para obtener más información acerca de las propiedades JSON de hello para el tipo de conjunto de datos específico de hello desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bc95b-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="bc95b-145">Tenga en cuenta Hola "dependsOn" parámetro especifica el nombre de los datos correspondientes de Hola generador y el almacenamiento de servicio vinculan.</span><span class="sxs-lookup"><span data-stu-id="bc95b-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="bc95b-146">Se muestra un ejemplo de definición de tipo de conjunto de datos de almacenamiento de blobs de Azure en hello después de la definición de JSON:</span><span class="sxs-lookup"><span data-stu-id="bc95b-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="bc95b-147">Definición de canalizaciones</span><span class="sxs-lookup"><span data-stu-id="bc95b-147">Define pipelines</span></span>

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

<span data-ttu-id="bc95b-148">Consulte demasiado[definir canalizaciones](data-factory-create-pipelines.md#pipeline-json) para detalles acerca de las propiedades JSON de Hola para definir Hola canalización específica y las actividades que se va toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bc95b-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="bc95b-149">Nota Hola "dependsOn" parámetro especifica el nombre de la factoría de datos de hello y los correspondientes servicios vinculados o conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="bc95b-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="bc95b-150">Se muestra un ejemplo de una canalización que copia datos de almacenamiento de blobs de Azure tooAzure base de datos SQL en hello siguiente fragmento de JSON:</span><span class="sxs-lookup"><span data-stu-id="bc95b-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="bc95b-151">Parametrización de la plantilla de Data Factory</span><span class="sxs-lookup"><span data-stu-id="bc95b-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="bc95b-152">Para obtener los procedimientos recomendados sobre parametrización, consulte el artículo [Procedimientos recomendados para crear plantillas de Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="bc95b-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="bc95b-153">Por lo general, se debe minimizar el uso de parámetros, especialmente si se pueden utilizar variables en su lugar.</span><span class="sxs-lookup"><span data-stu-id="bc95b-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="bc95b-154">Solo se proporcionan parámetros Hola los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="bc95b-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="bc95b-155">La configuración varía según el entorno (por ejemplo: desarrollo, prueba y producción)</span><span class="sxs-lookup"><span data-stu-id="bc95b-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="bc95b-156">Secretos (por ejemplo, las contraseñas)</span><span class="sxs-lookup"><span data-stu-id="bc95b-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="bc95b-157">Si necesita toopull secretos de [el almacén de claves de Azure](../key-vault/key-vault-get-started.md) al implementar las entidades de la factoría de datos de Azure mediante plantillas, especifique hello **el almacén de claves** y **nombre secreto** tal y como se muestra en Hola al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc95b-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

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
> <span data-ttu-id="bc95b-158">Al exportar plantillas para los generadores de datos existente actualmente todavía no es compatible, es en hello funciona.</span><span class="sxs-lookup"><span data-stu-id="bc95b-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
