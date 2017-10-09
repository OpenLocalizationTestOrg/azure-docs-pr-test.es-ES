---
title: un grupo de espacio de nombres y el consumidor de centros de eventos de Azure mediante una plantilla de aaaCreate | Documentos de Microsoft
description: "Creación de un espacio de nombres de Event Hubs con un centro de eventos y un grupo de consumidores mediante plantillas de Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="e1ccc-103">Creación de un espacio de nombres de Event Hubs con un centro de eventos y un grupo de consumidores mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e1ccc-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="e1ccc-104">Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure crea un espacio de nombres de tipo de los centros de eventos con el concentrador de un evento y un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="e1ccc-105">Hola artículo se muestra cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="e1ccc-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet los requisitos</span><span class="sxs-lookup"><span data-stu-id="e1ccc-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="e1ccc-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="e1ccc-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="e1ccc-108">Para la plantilla completa de hello, vea hello [plantilla de grupo de concentrador y consumidor de eventos] [ Event Hub and consumer group template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ccc-109">toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="e1ccc-110">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="e1ccc-110">What will you deploy?</span></span>
<span data-ttu-id="e1ccc-111">Con esta plantilla, implementará un espacio de nombres de Event Hubs con un grupo de consumidores y un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="e1ccc-112">[Los concentradores de eventos](event-hubs-what-is-event-hubs.md) es un evento de procesamiento tooprovide de servicio que se utiliza a eventos y telemetría de la tooAzure de entrada con el a escala masiva, con baja latencia y alta fiabilidad.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="e1ccc-113">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="e1ccc-114">[![Implementar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e1ccc-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="e1ccc-115">parameters</span><span class="sxs-lookup"><span data-stu-id="e1ccc-115">Parameters</span></span>
<span data-ttu-id="e1ccc-116">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="e1ccc-117">plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="e1ccc-118">Debe definir un parámetro para aquellos valores que puede variar, basada en la que va a implementar el proyecto de Hola o en hello entorno toowhich que va a implementar.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="e1ccc-119">No se define parámetros para valores que permanezcan siempre Hola igual.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="e1ccc-120">Cada valor de parámetro de plantilla de hello define recursos de Hola que se implementan.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="e1ccc-121">plantilla de Hello define Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="e1ccc-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="e1ccc-122">eventHubNamespaceName</span></span>
<span data-ttu-id="e1ccc-123">nombre de Hola de toocreate de espacio de nombres de los centros de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="e1ccc-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="e1ccc-124">eventHubName</span></span>
<span data-ttu-id="e1ccc-125">nombre de Hello del concentrador de eventos de hello creado en el espacio de nombres de hello centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="e1ccc-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="e1ccc-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="e1ccc-127">nombre de Hello del grupo de consumidores de hello creado para el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="e1ccc-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e1ccc-128">apiVersion</span></span>
<span data-ttu-id="e1ccc-129">versión de API de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="e1ccc-130">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="e1ccc-130">Resources toodeploy</span></span>
<span data-ttu-id="e1ccc-131">Crea un espacio de nombres de tipo **Event Hubs** con un centro de eventos y un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="e1ccc-132">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="e1ccc-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="e1ccc-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1ccc-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="e1ccc-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e1ccc-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="e1ccc-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1ccc-135">Next steps</span></span>
<span data-ttu-id="e1ccc-136">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="e1ccc-137">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e1ccc-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e1ccc-138">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="e1ccc-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="e1ccc-139">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e1ccc-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
