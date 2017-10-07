---
title: espacio de nombres de Bus de servicio de Azure de aaaCreate y poner en cola con la plantilla del Administrador de recursos de Azure | Documentos de Microsoft
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
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="96278-103">Creación de un espacio de nombres de Bus de servicio mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96278-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="96278-104">Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure crea un espacio de nombres de Bus de servicio y una cola dentro de ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="96278-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="96278-105">Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="96278-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="96278-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="96278-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="96278-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="96278-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="96278-108">Para la plantilla completa de hello, vea hello [plantilla de espacio de nombres y de cola de Bus de servicio] [ Service Bus namespace and queue template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="96278-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="96278-109">Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="96278-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="96278-110">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="96278-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="96278-111">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="96278-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="96278-112">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="96278-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * <span data-ttu-id="96278-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md) (Creación de un espacio de nombres de Service Bus con tema, suscripción y regla)</span><span class="sxs-lookup"><span data-stu-id="96278-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md)</span></span>
> 
> <span data-ttu-id="96278-114">toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque "Bus de servicio".</span><span class="sxs-lookup"><span data-stu-id="96278-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="96278-115">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="96278-115">What will you deploy?</span></span>

<span data-ttu-id="96278-116">Con esta plantilla, implementará un espacio de nombres de Bus de servicio con una cola.</span><span class="sxs-lookup"><span data-stu-id="96278-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="96278-117">[Colas de Service Bus](service-bus-queues-topics-subscriptions.md#queues) ofrecen primero en ENTRAR, primero en salir (FIFO) mensaje entrega tooone o varios consumidores en competencia.</span><span class="sxs-lookup"><span data-stu-id="96278-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="96278-118">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="96278-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="96278-119">[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="96278-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="96278-120">parameters</span><span class="sxs-lookup"><span data-stu-id="96278-120">Parameters</span></span>

<span data-ttu-id="96278-121">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="96278-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="96278-122">plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="96278-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="96278-123">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="96278-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="96278-124">No se define parámetros para valores que siempre permanecerá Hola igual.</span><span class="sxs-lookup"><span data-stu-id="96278-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="96278-125">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="96278-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="96278-126">plantilla de Hello define Hola parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="96278-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="96278-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="96278-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="96278-128">nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="96278-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="96278-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="96278-129">serviceBusQueueName</span></span>
<span data-ttu-id="96278-130">nombre de Hola de cola de hello creada en el espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="96278-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="96278-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="96278-131">serviceBusApiVersion</span></span>
<span data-ttu-id="96278-132">versión de API de Service Bus de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="96278-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="96278-133">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="96278-133">Resources toodeploy</span></span>
<span data-ttu-id="96278-134">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**con una cola.</span><span class="sxs-lookup"><span data-stu-id="96278-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="96278-135">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="96278-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="96278-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96278-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="96278-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="96278-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="96278-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96278-138">Next steps</span></span>
<span data-ttu-id="96278-139">Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos mediante la visualización de estos artículos:</span><span class="sxs-lookup"><span data-stu-id="96278-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="96278-140">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="96278-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="96278-141">Administrar recursos de Service Bus con hello Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="96278-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
