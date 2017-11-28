---
title: "Creación de un espacio de nombres y un grupo de consumidores de Azure Event Hubs mediante una plantilla | Microsoft Docs"
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
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="f9a63-103">Creación de un espacio de nombres de Event Hubs con un centro de eventos y un grupo de consumidores mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f9a63-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="f9a63-104">En este artículo se muestra cómo usar una plantilla de Azure Resource Manager, que crea un espacio de nombres de tipo Event Hubs, con un centro de eventos y un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="f9a63-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="f9a63-105">El artículo muestra cómo definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="f9a63-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="f9a63-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="f9a63-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="f9a63-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="f9a63-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="f9a63-108">Para ver la plantilla completa, consulte la [plantilla de grupos de consumidores y un centro de eventos][Event Hub and consumer group template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="f9a63-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="f9a63-109">Para buscar las plantillas más recientes, visite la galería de [Plantillas de inicio rápido de Azure][Azure Quickstart Templates] y busque Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f9a63-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="f9a63-110">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="f9a63-110">What will you deploy?</span></span>
<span data-ttu-id="f9a63-111">Con esta plantilla, implementará un espacio de nombres de Event Hubs con un grupo de consumidores y un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="f9a63-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="f9a63-112">[Centros de eventos](event-hubs-what-is-event-hubs.md) es un servicio de procesamiento de eventos que se usa para ofrecer la entrada de telemetría y eventos en Azure a escala masiva, con una latencia baja y una alta confiabilidad.</span><span class="sxs-lookup"><span data-stu-id="f9a63-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="f9a63-113">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9a63-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="f9a63-114">[![Implementación en Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="f9a63-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="f9a63-115">Parámetros</span><span class="sxs-lookup"><span data-stu-id="f9a63-115">Parameters</span></span>
<span data-ttu-id="f9a63-116">Con el Administrador de recursos de Azure, se definen los parámetros de los valores que desea especificar al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f9a63-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="f9a63-117">La plantilla incluye una sección denominada `Parameters` que contiene todos los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="f9a63-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="f9a63-118">Debe definir un parámetro para estos valores que variarán según el proyecto que vaya a implementar o según el entorno en el que vaya a realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="f9a63-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="f9a63-119">No defina parámetros para valores que siempre permanezcan igual.</span><span class="sxs-lookup"><span data-stu-id="f9a63-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="f9a63-120">Cada valor de parámetro de la plantilla define los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="f9a63-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="f9a63-121">La plantilla define los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9a63-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="f9a63-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="f9a63-122">eventHubNamespaceName</span></span>
<span data-ttu-id="f9a63-123">El nombre del espacio de nombres de Centros de eventos que se creará.</span><span class="sxs-lookup"><span data-stu-id="f9a63-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="f9a63-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="f9a63-124">eventHubName</span></span>
<span data-ttu-id="f9a63-125">El nombre del centro de eventos creado en el espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f9a63-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="f9a63-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="f9a63-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="f9a63-127">El nombre del grupo de consumidores creado para el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="f9a63-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="f9a63-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f9a63-128">apiVersion</span></span>
<span data-ttu-id="f9a63-129">La versión de API de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f9a63-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="f9a63-130">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="f9a63-130">Resources to deploy</span></span>
<span data-ttu-id="f9a63-131">Crea un espacio de nombres de tipo **Event Hubs** con un centro de eventos y un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="f9a63-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="f9a63-132">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="f9a63-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="f9a63-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9a63-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="f9a63-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f9a63-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="f9a63-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9a63-135">Next steps</span></span>
<span data-ttu-id="f9a63-136">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9a63-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="f9a63-137">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f9a63-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="f9a63-138">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="f9a63-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="f9a63-139">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f9a63-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
