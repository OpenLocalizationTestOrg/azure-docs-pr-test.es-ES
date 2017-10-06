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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Usar plantillas toocreate Data Factory de Azure entidades
## <a name="overview"></a>Información general
Durante el uso de Data Factory de Azure para sus necesidades de integración de datos, es probable que se encuentre reutilizar Hola mismo patrón en distintos entornos o implementar Hola igual de tareas repetidamente dentro de hello misma solución. Las plantillas le permiten implementar y administrar estos escenarios de una forma sencilla. Las plantillas de Azure Data Factory son ideales para los escenarios que implican la reutilización y la repetición.

Considere la posibilidad de situación Hola donde una organización tiene 10 plantas de fabricación a través de Hola a todos. registros de Hola desde cada planta se almacenan en una base de datos de SQL Server local independiente. empresa Hola quiere toobuild un único almacén en la nube de Hola para análisis ad hoc. También quiere toohave Hola misma lógica pero diferentes configuraciones para los entornos de desarrollo, prueba y producción.

En este caso, una tarea debe toobe repite dentro Hola mismo entorno, pero con valores diferentes a través de Hola 10 factorías de datos para cada planta de fabricación. En efecto, la **repetición** está presente. Creación de plantillas permite abstracción Hola de este flujo genérico (es decir, canalizaciones tener Hola mismas actividades en cada factoría de datos), pero usa un archivo de parámetros independiente para cada planta de fabricación.

Además, como Hola organización quiere toodeploy estos generadores de 10 datos varias veces en distintos entornos, las plantillas pueden usar esto **reusabilidad** mediante el uso de archivos de parámetro independiente para el desarrollo, prueba, y entornos de producción.

## <a name="templating-with-azure-resource-manager"></a>Creación de plantillas con Azure Resource Manager
[Plantillas de administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md#template-deployment) son una creación de plantillas de tooachieve excelente manera de factoría de datos de Azure. Las plantillas de administrador de recursos definen infraestructura hello y la configuración de la solución de Azure a través de un archivo JSON. Dado que las plantillas de Azure Resource Manager funcionan con la mayoría o todos los servicios de Azure, se puede usar ampliamente tooeasily administrar todos los recursos de sus activos de Azure. Vea [plantillas del Administrador de recursos de Azure de creación](../azure-resource-manager/resource-group-authoring-templates.md) toolearn más información sobre Hola plantillas del Administrador de recursos en general.

## <a name="tutorials"></a>Tutoriales
Vea Hola siguientes tutoriales para entidades de instrucciones paso a paso toocreate factoría de datos mediante plantillas de administrador de recursos:

* [Tutorial: Crear una canalización de datos de toocopy mediante el uso de la plantilla del Administrador de recursos de Azure](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Tutorial: Crear una canalización de datos de tooprocess mediante el uso de la plantilla del Administrador de recursos de Azure](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Plantillas de Data Factory en GitHub
Extraer del repositorio Hola siguiendo las plantillas de inicio rápido de Azure en GitHub:

* [Crear datos generador toocopy los datos de almacenamiento de blobs de Azure tooAzure base de datos SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Creación de una instancia de Data Factory con actividad de Hive en un clúster de Azure HDInsight)
* [Crear datos generador toocopy los datos de Salesforce tooAzure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Crear un generador de datos que se vincula las actividades: copia datos de un servidor FTP tooAzure Blobs, invoca un script de hive en un datos a petición HDInsight clúster tootransform hello y copia el resultado en la base de datos de SQL Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

Cree tooshare libre sus plantillas de Data Factory de Azure en [inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/). Consulte toohello [Guía de colaboración](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) durante el desarrollo de plantillas que se pueden compartir a través de este repositorio.

Hola las secciones siguientes proporciona detalles acerca de cómo definir recursos de la factoría de datos en una plantilla de administrador de recursos.

## <a name="defining-data-factory-resources-in-templates"></a>Definición de recursos de Data Factory en plantillas
plantilla de nivel superior de Hola para definir una factoría de datos es:

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

### <a name="define-data-factory"></a>Definición de factoría de datos
Defina una factoría de datos en la plantilla de administrador de recursos de hello tal y como se muestra en el siguiente ejemplo de Hola:

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
Hola dataFactoryName se define en "variables" como:

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Definición de servicios vinculados

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

Vea [servicio vinculado de almacenamiento](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [servicios vinculados de proceso](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obtener más información acerca de las propiedades JSON de Hola para servicio vinculado específico de hello desea toodeploy. parámetro de "dependsOn" Hello especifica el nombre de la factoría de datos correspondiente de Hola. Se muestra un ejemplo de definición de un servicio vinculado para el almacenamiento de Azure en hello después de la definición de JSON:

### <a name="define-datasets"></a>Definición de conjuntos de datos

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
Consulte demasiado[admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para obtener más información acerca de las propiedades JSON de hello para el tipo de conjunto de datos específico de hello desea toodeploy. Tenga en cuenta Hola "dependsOn" parámetro especifica el nombre de los datos correspondientes de Hola generador y el almacenamiento de servicio vinculan. Se muestra un ejemplo de definición de tipo de conjunto de datos de almacenamiento de blobs de Azure en hello después de la definición de JSON:

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

### <a name="define-pipelines"></a>Definición de canalizaciones

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

Consulte demasiado[definir canalizaciones](data-factory-create-pipelines.md#pipeline-json) para detalles acerca de las propiedades JSON de Hola para definir Hola canalización específica y las actividades que se va toodeploy. Nota Hola "dependsOn" parámetro especifica el nombre de la factoría de datos de hello y los correspondientes servicios vinculados o conjuntos de datos. Se muestra un ejemplo de una canalización que copia datos de almacenamiento de blobs de Azure tooAzure base de datos SQL en hello siguiente fragmento de JSON:

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
## <a name="parameterizing-data-factory-template"></a>Parametrización de la plantilla de Data Factory
Para obtener los procedimientos recomendados sobre parametrización, consulte el artículo [Procedimientos recomendados para crear plantillas de Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters). Por lo general, se debe minimizar el uso de parámetros, especialmente si se pueden utilizar variables en su lugar. Solo se proporcionan parámetros Hola los escenarios siguientes:

* La configuración varía según el entorno (por ejemplo: desarrollo, prueba y producción)
* Secretos (por ejemplo, las contraseñas)

Si necesita toopull secretos de [el almacén de claves de Azure](../key-vault/key-vault-get-started.md) al implementar las entidades de la factoría de datos de Azure mediante plantillas, especifique hello **el almacén de claves** y **nombre secreto** tal y como se muestra en Hola al ejemplo siguiente:

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
> Al exportar plantillas para los generadores de datos existente actualmente todavía no es compatible, es en hello funciona.
>
>
