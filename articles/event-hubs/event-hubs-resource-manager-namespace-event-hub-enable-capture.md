---
title: un espacio de nombres de los centros de eventos de Azure y habilite capturan con una plantilla de aaaCreate | Documentos de Microsoft
description: "Creación de un espacio de nombres de Azure Event Hubs con un centro de eventos y habilitación de la funcionalidad de captura mediante una plantilla de Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Creación de un espacio de nombres de Event Hubs con un centro de eventos y habilitación de Capture mediante una plantilla de Azure Resource Manager

Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure que crea un espacio de nombres de los centros de eventos, instancia de base de datos central de un evento, y también permite hello [característica de captura](event-hubs-capture-overview.md) en concentrador de eventos de Hola. Hola artículo se describe cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola. Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.

En este artículo también se muestra cómo toospecify que los eventos se capturan en Blobs de almacenamiento de Azure o un almacén de Azure Data Lake, en función de hello destino que elija.

Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).

Para más información sobre patrones y prácticas de convenciones de nomenclatura de recursos de Azure, consulte [Convenciones de nomenclatura de recursos de Azure][Azure Resources naming conventions].

Para las plantillas de hello completa, haga clic en hello siguientes vínculos de GitHub:

- [Plantilla de tooStorage de captura de concentrador y habilitar eventos][Event Hub and enable Capture tooStorage template] 
- [Concentrador y habilitar captura tooAzure almacén de Data Lake plantilla de evento][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque los centros de eventos.
> 
> 

## <a name="what-will-you-deploy"></a>¿Qué va a implementar?

Con esta plantilla, implementará un espacio de nombres de Event Hubs con un centro de eventos y habilitará la [captura de Event Hubs](event-hubs-capture-overview.md).

[Los concentradores de eventos](event-hubs-what-is-event-hubs.md) es un evento de procesamiento tooprovide de servicio que se utiliza a eventos y telemetría de la tooAzure de entrada con el a escala masiva, con baja latencia y alta fiabilidad. Evento concentradores capturar permite tooautomatically entregar Hola transmisión por secuencias de datos en el almacenamiento de blobs de los centros de eventos tooAzure o almacén de Azure Data Lake, dentro de un tiempo especificado o un intervalo de tamaño de su elección.

Haga clic en hello después tooenable botón capturar de concentradores de eventos en el almacenamiento de Azure:

[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Haga clic en hello después tooenable botón capturar de concentradores de eventos en el almacén de Azure Data Lake:

[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>parameters

Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla. plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola. Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola. No se define parámetros para valores que permanezcan siempre Hola igual. Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.

plantilla de Hello define Hola parámetros siguientes.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

nombre de Hola de hello [espacio de nombres de los centros de eventos](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

nombre de Hello del concentrador de eventos de hello creado en hello [espacio de nombres de los centros de eventos](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

número de Hola de mensajes de saludo de tooretain días en el concentrador de eventos de Hola. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

número de Hola de toocreate de particiones en el centro de eventos de Hola.

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

Habilitar la captura en el concentrador de eventos de Hola.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

especificar datos de eventos de hello tooserialize el formato de codificación de Hola.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

intervalo de tiempo de Hello en el que captura de los centros de eventos se inicia la captura de datos de Hola.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
intervalo de tamaño de saludo donde captura inicia la captura de datos de Hola.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

formato de nombre de Hello utilizado por los archivos de captura de los centros de eventos toowrite hello Avro. Tenga en cuenta que un formato de nombre de Capture debe contener los campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` y `{Second}`. Estos se pueden organizar en cualquier orden, con o sin delimitadores.
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

versión de API de Hola de plantilla de Hola.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Usar hello parámetros siguientes si elige como destino de almacenamiento de Azure.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Captura de requiere un tooenable de Id. de recurso de almacenamiento de Azure cuenta capturar tooyour deseado cuenta de almacenamiento.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

Hola contenedor de blobs en qué toocapture los datos del evento.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Usar hello parámetros siguientes si elige como destino de almacén de Azure Data Lake. Debe establecer permisos en la ruta de acceso del almacén de Data Lake, en el que desea eventos de hello tooCapture. permisos de tooset, consulte [este artículo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

Identificador de suscripción para el espacio de nombres de los centros de eventos de Hola y almacén de Azure Data Lake. Ambos estos recursos deben estar en hello mismo identificador de suscripción.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

nombre de almacén de Azure Data Lake de Hola para hello los eventos capturados.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

ruta de carpeta de destino de Hola de hello los eventos capturados.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Toodeploy de recursos para el almacenamiento de Azure como eventos de toocaptured de destino

Crea un espacio de nombres del tipo **EventHubs**, centro de un evento, y también permite capturar tooAzure almacenamiento de blobs.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Toodeploy de recursos para el almacén de Data Lake de Azure como destino

Crea un espacio de nombres del tipo **EventHubs**, centro de un evento, y también habilita el almacén de captura tooAzure Data Lake.

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Implementación de toorun de comandos

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Implemente su tooenable plantilla capturar de concentradores de eventos en el almacenamiento de Azure:
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Implemente su tooenable plantilla capturar de concentradores de eventos en el almacén de Azure Data Lake:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>CLI de Azure

Elección de Azure Blob Storage como destino:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Elección de Azure Data Lake Store como destino:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Pasos siguientes

También puede configurar la captura de los centros de eventos a través de hello [portal de Azure](https://portal.azure.com). Para obtener más información, consulte [habilitar la captura de concentradores de eventos utilizando Hola portal de Azure](event-hubs-capture-enable-through-portal.md).

Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
