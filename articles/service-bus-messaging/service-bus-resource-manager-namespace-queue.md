---
title: "Creación de un espacio de nombres y una cola de Azure Service Bus mediante una plantilla de Azure Resource Manager | Microsoft Docs"
description: "Creación de un espacio de nombres de Bus de servicio y una cola mediante una plantilla de Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 4358130a2c8e897a0fdd1f9560f766d6e22db4d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="c8bd6-103">Creación de un espacio de nombres de Bus de servicio mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c8bd6-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="c8bd6-104">En este artículo se muestra cómo utilizar una plantilla de Azure Resource Manager que crea una cola y un espacio de nombres de Service Bus dentro de un espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="c8bd6-105">Aprenderá a definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="c8bd6-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="c8bd6-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c8bd6-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="c8bd6-108">Para verla completa, consulte la [plantilla de cola y espacio de nombres de Service Bus][Service Bus namespace and queue template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-108">For the complete template, see the [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="c8bd6-109">Las siguientes plantillas de Azure Resource Manager están disponibles para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="c8bd6-110">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="c8bd6-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="c8bd6-111">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="c8bd6-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="c8bd6-112">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="c8bd6-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="c8bd6-113">Creación de un espacio de nombres de Service Bus con un tema, una suscripción y una regla</span><span class="sxs-lookup"><span data-stu-id="c8bd6-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="c8bd6-114">Para buscar las últimas plantillas, visite la galería [Plantillas de inicio rápido de Azure][Azure Quickstart Templates] y busque "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="c8bd6-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="c8bd6-115">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="c8bd6-115">What will you deploy?</span></span>

<span data-ttu-id="c8bd6-116">Con esta plantilla, implementará un espacio de nombres de Bus de servicio con una cola.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="c8bd6-117">Las [colas de Service Bus](service-bus-queues-topics-subscriptions.md#queues) ofrecen una entrega de mensajes según el modelo “primero en entrar, primero en salir” (FIFO) a uno o más consumidores de la competencia.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery to one or more competing consumers.</span></span>

<span data-ttu-id="c8bd6-118">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8bd6-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="c8bd6-119">[![Implementación en Azure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="c8bd6-119">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="c8bd6-120">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c8bd6-120">Parameters</span></span>

<span data-ttu-id="c8bd6-121">Con el Administrador de recursos de Azure, se definen los parámetros de los valores que desea especificar al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="c8bd6-122">La plantilla incluye una sección denominada `Parameters` que contiene todos los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="c8bd6-123">Debe definir un parámetro para los valores que variarán según el proyecto que vaya a implementar o según el entorno en el que vaya a realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="c8bd6-124">No defina parámetros para valores que vayan a permanecer igual.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="c8bd6-125">Cada valor de parámetro se usa en la plantilla para definir los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="c8bd6-126">La plantilla define los parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="c8bd6-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="c8bd6-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="c8bd6-128">El nombre del espacio de nombres de Bus de servicio que crear.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="c8bd6-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="c8bd6-129">serviceBusQueueName</span></span>
<span data-ttu-id="c8bd6-130">El nombre de la cola creada en el espacio de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-130">The name of the queue created in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="c8bd6-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="c8bd6-131">serviceBusApiVersion</span></span>
<span data-ttu-id="c8bd6-132">La versión de la API de Bus de servicio de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-132">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="c8bd6-133">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="c8bd6-133">Resources to deploy</span></span>
<span data-ttu-id="c8bd6-134">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**con una cola.</span><span class="sxs-lookup"><span data-stu-id="c8bd6-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="c8bd6-135">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="c8bd6-135">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="c8bd6-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8bd6-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="c8bd6-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c8bd6-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="c8bd6-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c8bd6-138">Next steps</span></span>
<span data-ttu-id="c8bd6-139">Ahora que ha creado e implementado recursos con Azure Resource Manager, estos artículos le enseñarán como administrarlos:</span><span class="sxs-lookup"><span data-stu-id="c8bd6-139">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="c8bd6-140">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8bd6-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="c8bd6-141">Administración de recursos de Bus de servicio con el Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="c8bd6-141">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
