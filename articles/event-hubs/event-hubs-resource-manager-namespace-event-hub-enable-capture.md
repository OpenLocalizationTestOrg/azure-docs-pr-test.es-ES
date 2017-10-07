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
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="52f00-103">Creación de un espacio de nombres de Event Hubs con un centro de eventos y habilitación de Capture mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="52f00-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="52f00-104">Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure que crea un espacio de nombres de los centros de eventos, instancia de base de datos central de un evento, y también permite hello [característica de captura](event-hubs-capture-overview.md) en concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="52f00-105">Hola artículo se describe cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="52f00-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="52f00-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="52f00-107">En este artículo también se muestra cómo toospecify que los eventos se capturan en Blobs de almacenamiento de Azure o un almacén de Azure Data Lake, en función de hello destino que elija.</span><span class="sxs-lookup"><span data-stu-id="52f00-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="52f00-108">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="52f00-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="52f00-109">Para más información sobre patrones y prácticas de convenciones de nomenclatura de recursos de Azure, consulte [Convenciones de nomenclatura de recursos de Azure][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="52f00-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="52f00-110">Para las plantillas de hello completa, haga clic en hello siguientes vínculos de GitHub:</span><span class="sxs-lookup"><span data-stu-id="52f00-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="52f00-111">[Plantilla de tooStorage de captura de concentrador y habilitar eventos][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="52f00-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="52f00-112">[Concentrador y habilitar captura tooAzure almacén de Data Lake plantilla de evento][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="52f00-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="52f00-113">toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="52f00-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="52f00-114">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="52f00-114">What will you deploy?</span></span>

<span data-ttu-id="52f00-115">Con esta plantilla, implementará un espacio de nombres de Event Hubs con un centro de eventos y habilitará la [captura de Event Hubs](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52f00-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="52f00-116">[Los concentradores de eventos](event-hubs-what-is-event-hubs.md) es un evento de procesamiento tooprovide de servicio que se utiliza a eventos y telemetría de la tooAzure de entrada con el a escala masiva, con baja latencia y alta fiabilidad.</span><span class="sxs-lookup"><span data-stu-id="52f00-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="52f00-117">Evento concentradores capturar permite tooautomatically entregar Hola transmisión por secuencias de datos en el almacenamiento de blobs de los centros de eventos tooAzure o almacén de Azure Data Lake, dentro de un tiempo especificado o un intervalo de tamaño de su elección.</span><span class="sxs-lookup"><span data-stu-id="52f00-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="52f00-118">Haga clic en hello después tooenable botón capturar de concentradores de eventos en el almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="52f00-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="52f00-119">[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="52f00-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="52f00-120">Haga clic en hello después tooenable botón capturar de concentradores de eventos en el almacén de Azure Data Lake:</span><span class="sxs-lookup"><span data-stu-id="52f00-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="52f00-121">[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="52f00-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="52f00-122">parameters</span><span class="sxs-lookup"><span data-stu-id="52f00-122">Parameters</span></span>

<span data-ttu-id="52f00-123">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="52f00-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="52f00-124">plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="52f00-125">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="52f00-126">No se define parámetros para valores que permanezcan siempre Hola igual.</span><span class="sxs-lookup"><span data-stu-id="52f00-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="52f00-127">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="52f00-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="52f00-128">plantilla de Hello define Hola parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="52f00-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="52f00-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="52f00-129">eventHubNamespaceName</span></span>

<span data-ttu-id="52f00-130">nombre de Hola de hello [espacio de nombres de los centros de eventos](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="52f00-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="52f00-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="52f00-131">eventHubName</span></span>

<span data-ttu-id="52f00-132">nombre de Hello del concentrador de eventos de hello creado en hello [espacio de nombres de los centros de eventos](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="52f00-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="52f00-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="52f00-133">messageRetentionInDays</span></span>

<span data-ttu-id="52f00-134">número de Hola de mensajes de saludo de tooretain días en el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

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

### <a name="partitioncount"></a><span data-ttu-id="52f00-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="52f00-135">partitionCount</span></span>

<span data-ttu-id="52f00-136">número de Hola de toocreate de particiones en el centro de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-136">hello number of partitions toocreate in hello event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="52f00-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="52f00-137">captureEnabled</span></span>

<span data-ttu-id="52f00-138">Habilitar la captura en el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-138">Enable Capture on hello event hub.</span></span>

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
### <a name="captureencodingformat"></a><span data-ttu-id="52f00-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="52f00-139">captureEncodingFormat</span></span>

<span data-ttu-id="52f00-140">especificar datos de eventos de hello tooserialize el formato de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-140">hello encoding format you specify tooserialize hello event data.</span></span>

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

### <a name="capturetime"></a><span data-ttu-id="52f00-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="52f00-141">captureTime</span></span>

<span data-ttu-id="52f00-142">intervalo de tiempo de Hello en el que captura de los centros de eventos se inicia la captura de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

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

### <a name="capturesize"></a><span data-ttu-id="52f00-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="52f00-143">captureSize</span></span>
<span data-ttu-id="52f00-144">intervalo de tamaño de saludo donde captura inicia la captura de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-144">hello size interval at which Capture starts capturing hello data.</span></span>

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

###<a name="capturenameformat"></a><span data-ttu-id="52f00-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="52f00-145">captureNameFormat</span></span>

<span data-ttu-id="52f00-146">formato de nombre de Hello utilizado por los archivos de captura de los centros de eventos toowrite hello Avro.</span><span class="sxs-lookup"><span data-stu-id="52f00-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="52f00-147">Tenga en cuenta que un formato de nombre de Capture debe contener los campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` y `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="52f00-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="52f00-148">Estos se pueden organizar en cualquier orden, con o sin delimitadores.</span><span class="sxs-lookup"><span data-stu-id="52f00-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="52f00-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="52f00-149">apiVersion</span></span>

<span data-ttu-id="52f00-150">versión de API de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f00-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="52f00-151">Usar hello parámetros siguientes si elige como destino de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="52f00-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="52f00-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="52f00-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="52f00-153">Captura de requiere un tooenable de Id. de recurso de almacenamiento de Azure cuenta capturar tooyour deseado cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="52f00-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="52f00-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="52f00-154">blobContainerName</span></span>

<span data-ttu-id="52f00-155">Hola contenedor de blobs en qué toocapture los datos del evento.</span><span class="sxs-lookup"><span data-stu-id="52f00-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="52f00-156">Usar hello parámetros siguientes si elige como destino de almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="52f00-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="52f00-157">Debe establecer permisos en la ruta de acceso del almacén de Data Lake, en el que desea eventos de hello tooCapture.</span><span class="sxs-lookup"><span data-stu-id="52f00-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="52f00-158">permisos de tooset, consulte [este artículo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="52f00-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="52f00-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="52f00-159">subscriptionId</span></span>

<span data-ttu-id="52f00-160">Identificador de suscripción para el espacio de nombres de los centros de eventos de Hola y almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="52f00-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="52f00-161">Ambos estos recursos deben estar en hello mismo identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="52f00-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="52f00-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="52f00-162">dataLakeAccountName</span></span>

<span data-ttu-id="52f00-163">nombre de almacén de Azure Data Lake de Hola para hello los eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="52f00-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="52f00-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="52f00-164">dataLakeFolderPath</span></span>

<span data-ttu-id="52f00-165">ruta de carpeta de destino de Hola de hello los eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="52f00-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="52f00-166">Toodeploy de recursos para el almacenamiento de Azure como eventos de toocaptured de destino</span><span class="sxs-lookup"><span data-stu-id="52f00-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="52f00-167">Crea un espacio de nombres del tipo **EventHubs**, centro de un evento, y también permite capturar tooAzure almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="52f00-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

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

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="52f00-168">Toodeploy de recursos para el almacén de Data Lake de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="52f00-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="52f00-169">Crea un espacio de nombres del tipo **EventHubs**, centro de un evento, y también habilita el almacén de captura tooAzure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="52f00-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="52f00-170">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="52f00-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="52f00-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52f00-171">PowerShell</span></span>

<span data-ttu-id="52f00-172">Implemente su tooenable plantilla capturar de concentradores de eventos en el almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="52f00-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="52f00-173">Implemente su tooenable plantilla capturar de concentradores de eventos en el almacén de Azure Data Lake:</span><span class="sxs-lookup"><span data-stu-id="52f00-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="52f00-174">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="52f00-174">Azure CLI</span></span>

<span data-ttu-id="52f00-175">Elección de Azure Blob Storage como destino:</span><span class="sxs-lookup"><span data-stu-id="52f00-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="52f00-176">Elección de Azure Data Lake Store como destino:</span><span class="sxs-lookup"><span data-stu-id="52f00-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="52f00-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52f00-177">Next steps</span></span>

<span data-ttu-id="52f00-178">También puede configurar la captura de los centros de eventos a través de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="52f00-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="52f00-179">Para obtener más información, consulte [habilitar la captura de concentradores de eventos utilizando Hola portal de Azure](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="52f00-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="52f00-180">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="52f00-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="52f00-181">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="52f00-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="52f00-182">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="52f00-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="52f00-183">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="52f00-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
