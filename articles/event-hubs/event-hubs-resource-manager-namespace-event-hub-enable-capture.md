---
title: "Creación de un espacio de nombres de Azure Event Hubs y habilitación de la funcionalidad de captura mediante una plantilla | Microsoft Docs"
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
ms.openlocfilehash: 19bbb51868e767aa1d15f4574628b7fd36607207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="48af4-103">Creación de un espacio de nombres de Event Hubs con un centro de eventos y habilitación de Capture mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48af4-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="48af4-104">En este artículo se muestra cómo usar una plantilla de Azure Resource Manager que crea un espacio de nombres de Event Hubs, con una instancia de centro de eventos, y también habilita la [característica Capture](event-hubs-capture-overview.md) en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="48af4-104">This article shows how to use an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub.</span></span> <span data-ttu-id="48af4-105">En este artículo se describe cómo definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="48af4-105">The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="48af4-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="48af4-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="48af4-107">En este artículo también se muestra cómo especificar los eventos que se capturan en instancias de Azure Storage Blob o de Azure Data Lake Store, basándose en el destino que elija.</span><span class="sxs-lookup"><span data-stu-id="48af4-107">This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.</span></span>

<span data-ttu-id="48af4-108">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="48af4-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="48af4-109">Para más información sobre patrones y prácticas de convenciones de nomenclatura de recursos de Azure, consulte [Convenciones de nomenclatura de recursos de Azure][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="48af4-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="48af4-110">Para ver las plantillas completas, haga clic en los siguientes vínculos de GitHub:</span><span class="sxs-lookup"><span data-stu-id="48af4-110">For the complete templates, click the following GitHub links:</span></span>

- <span data-ttu-id="48af4-111">[Centro de eventos y habilitación de Capture en una plantilla de Storage][Event Hub and enable Capture to Storage template]</span><span class="sxs-lookup"><span data-stu-id="48af4-111">[Event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]</span></span> 
- <span data-ttu-id="48af4-112">[Centro de eventos y habilitación de Capture en una plantilla de Azure Data Lake Store][Event Hub and enable Capture to Azure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="48af4-112">[Event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="48af4-113">Para buscar las plantillas más recientes, visite la galería de [Plantillas de inicio rápido de Azure][Azure Quickstart Templates] y busque Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="48af4-113">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="48af4-114">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="48af4-114">What will you deploy?</span></span>

<span data-ttu-id="48af4-115">Con esta plantilla, implementará un espacio de nombres de Event Hubs con un centro de eventos y habilitará la [captura de Event Hubs](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48af4-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="48af4-116">[Centros de eventos](event-hubs-what-is-event-hubs.md) es un servicio de procesamiento de eventos que se usa para ofrecer la entrada de telemetría y eventos en Azure a escala masiva, con una latencia baja y una alta confiabilidad.</span><span class="sxs-lookup"><span data-stu-id="48af4-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="48af4-117">Event Hubs Capture le permite entregar automáticamente los datos de streaming de sus instancias de Event Hubs a una instancia de Azure Blob Storage o Azure Data Lake Store, en el tiempo especificado o el intervalo de tamaño que prefiera.</span><span class="sxs-lookup"><span data-stu-id="48af4-117">Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="48af4-118">Haga clic en el botón siguiente para habilitar Event Hubs Capture en Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="48af4-118">Click the following button to enable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="48af4-119">[![Implementación en Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="48af4-119">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="48af4-120">Haga clic en el botón siguiente para habilitar Event Hubs Capture en Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="48af4-120">Click the following button to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="48af4-121">[![Implementación en Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="48af4-121">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="48af4-122">Parámetros</span><span class="sxs-lookup"><span data-stu-id="48af4-122">Parameters</span></span>

<span data-ttu-id="48af4-123">Con el Administrador de recursos de Azure, se definen los parámetros de los valores que desea especificar al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="48af4-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="48af4-124">La plantilla incluye una sección denominada `Parameters` que contiene todos los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="48af4-124">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="48af4-125">Debe definir un parámetro para esos valores que variarán según el proyecto que vaya a implementar o según el entorno en el que vaya a realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="48af4-125">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="48af4-126">No defina parámetros para valores que siempre permanezcan igual.</span><span class="sxs-lookup"><span data-stu-id="48af4-126">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="48af4-127">Cada valor de parámetro se usa en la plantilla para definir los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="48af4-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="48af4-128">La plantilla define los parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="48af4-128">The template defines the following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="48af4-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="48af4-129">eventHubNamespaceName</span></span>

<span data-ttu-id="48af4-130">El nombre del [espacio de nombres de Event Hubs](event-hubs-create.md) que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="48af4-130">The name of the [Event Hubs namespace](event-hubs-create.md) to create.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of the EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="48af4-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="48af4-131">eventHubName</span></span>

<span data-ttu-id="48af4-132">El nombre del centro de eventos creado en el [espacio de nombres de Event Hubs](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="48af4-132">The name of the event hub created in the [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of the event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="48af4-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="48af4-133">messageRetentionInDays</span></span>

<span data-ttu-id="48af4-134">El número de días que se deben conservar los mensajes en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="48af4-134">The number of days to retain the messages in the event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long to retain the data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="48af4-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="48af4-135">partitionCount</span></span>

<span data-ttu-id="48af4-136">El número de particiones que se van a crear en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="48af4-136">The number of partitions to create in the event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="48af4-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="48af4-137">captureEnabled</span></span>

<span data-ttu-id="48af4-138">Habilita la funcionalidad de captura en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="48af4-138">Enable Capture on the event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable the Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="48af4-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="48af4-139">captureEncodingFormat</span></span>

<span data-ttu-id="48af4-140">El formato de codificación que especifica para serializar los datos de eventos.</span><span class="sxs-lookup"><span data-stu-id="48af4-140">The encoding format you specify to serialize the event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"The encoding format in which Capture serializes the EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="48af4-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="48af4-141">captureTime</span></span>

<span data-ttu-id="48af4-142">El intervalo de tiempo en el que Event Hubs Capture comienza a capturar los datos.</span><span class="sxs-lookup"><span data-stu-id="48af4-142">The time interval in which Event Hubs Capture starts capturing the data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"the time window in seconds for the capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="48af4-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="48af4-143">captureSize</span></span>
<span data-ttu-id="48af4-144">El intervalo de tamaño en el que Capture comienza a capturar los datos.</span><span class="sxs-lookup"><span data-stu-id="48af4-144">The size interval at which Capture starts capturing the data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"The size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="48af4-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="48af4-145">captureNameFormat</span></span>

<span data-ttu-id="48af4-146">El formato de nombre que usa Event Hubs Capture para escribir archivos Avro.</span><span class="sxs-lookup"><span data-stu-id="48af4-146">The name format used by Event Hubs Capture to write the Avro files.</span></span> <span data-ttu-id="48af4-147">Tenga en cuenta que un formato de nombre de Capture debe contener los campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` y `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="48af4-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="48af4-148">Estos se pueden organizar en cualquier orden, con o sin delimitadores.</span><span class="sxs-lookup"><span data-stu-id="48af4-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="48af4-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="48af4-149">apiVersion</span></span>

<span data-ttu-id="48af4-150">La versión de API de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="48af4-150">The API version of the template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by the template"
    }
 }
```

<span data-ttu-id="48af4-151">Si elige como destino Azure Storage, use los parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="48af4-151">Use the following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="48af4-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="48af4-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="48af4-153">La funcionalidad de captura requiere un identificador de recurso de una cuenta de Azure Storage para habilitar esta funcionalidad en la cuenta deseada de Storage.</span><span class="sxs-lookup"><span data-stu-id="48af4-153">Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want the blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="48af4-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="48af4-154">blobContainerName</span></span>

<span data-ttu-id="48af4-155">El contenedor de blobs en el que se van a capturar los datos del evento.</span><span class="sxs-lookup"><span data-stu-id="48af4-155">The blob container in which to capture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want the blobs captured"
    }
}
```

<span data-ttu-id="48af4-156">Si elige como destino Azure Data Lake Store, use los parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="48af4-156">Use the following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="48af4-157">Debe establecer permisos en la ruta de acceso de Data Lake Store, en el que desea capturar el evento.</span><span class="sxs-lookup"><span data-stu-id="48af4-157">You must set permissions on your Data Lake Store path, in which you want to Capture the event.</span></span> <span data-ttu-id="48af4-158">Para establecer los permisos, consulte [este artículo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="48af4-158">To set permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="48af4-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="48af4-159">subscriptionId</span></span>

<span data-ttu-id="48af4-160">El identificador de suscripción para el espacio de nombres de Event Hubs y Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="48af4-160">Subscription ID for the Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="48af4-161">Ambos recursos deben estar en el mismo identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="48af4-161">Both these resources must be under the same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="48af4-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="48af4-162">dataLakeAccountName</span></span>

<span data-ttu-id="48af4-163">El nombre de Azure Data Lake Store para los eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="48af4-163">The Azure Data Lake Store name for the captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="48af4-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="48af4-164">dataLakeFolderPath</span></span>

<span data-ttu-id="48af4-165">La ruta de acceso de la carpeta de destino para los eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="48af4-165">The destination folder path for the captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-to-deploy-for-azure-storage-as-destination-to-captured-events"></a><span data-ttu-id="48af4-166">Recursos que deben implementarse para Azure Storage como destino para los eventos capturados</span><span class="sxs-lookup"><span data-stu-id="48af4-166">Resources to deploy for Azure Storage as destination to captured events</span></span>

<span data-ttu-id="48af4-167">Crea un espacio de nombres de tipo **EventHubs**, con un centro de eventos, y también habilita Capture en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="48af4-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Blob Storage.</span></span>

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

## <a name="resources-to-deploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="48af4-168">Recursos que deben implementarse para Azure Data Lake Store como destino</span><span class="sxs-lookup"><span data-stu-id="48af4-168">Resources to deploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="48af4-169">Crea un espacio de nombres de tipo **EventHubs**, con un centro de eventos, y también habilita Capture en Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="48af4-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Data Lake Store.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="48af4-170">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="48af4-170">Commands to run deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="48af4-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48af4-171">PowerShell</span></span>

<span data-ttu-id="48af4-172">Implemente la plantilla para habilitar Event Hubs Capture en Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="48af4-172">Deploy your template to enable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="48af4-173">Implemente la plantilla para habilitar Event Hubs Capture en Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="48af4-173">Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="48af4-174">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="48af4-174">Azure CLI</span></span>

<span data-ttu-id="48af4-175">Elección de Azure Blob Storage como destino:</span><span class="sxs-lookup"><span data-stu-id="48af4-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="48af4-176">Elección de Azure Data Lake Store como destino:</span><span class="sxs-lookup"><span data-stu-id="48af4-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="48af4-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48af4-177">Next steps</span></span>

<span data-ttu-id="48af4-178">También puede configurar la funcionalidad de captura de Events Hubs mediante [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48af4-178">You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="48af4-179">Para más información, consulte [Habilitación de la funcionalidad de captura de Event Hubs mediante Azure Portal](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48af4-179">For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="48af4-180">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="48af4-180">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="48af4-181">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="48af4-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="48af4-182">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="48af4-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="48af4-183">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="48af4-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture to Storage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture to Azure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls