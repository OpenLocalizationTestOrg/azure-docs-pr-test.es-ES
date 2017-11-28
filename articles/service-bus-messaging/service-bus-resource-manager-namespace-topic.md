---
title: "suscripción de tema de espacio de nombres aaaCreate Service Bus de Azure mediante la plantilla del Administrador de recursos de Azure | Documentos de Microsoft"
description: "Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción mediante una plantilla de Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="36e37-103">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36e37-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="36e37-104">Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure crea un espacio de nombres de Bus de servicio y un tema y suscripción dentro de ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="36e37-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="36e37-105">Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="36e37-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="36e37-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet los requisitos</span><span class="sxs-lookup"><span data-stu-id="36e37-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="36e37-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="36e37-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="36e37-108">Para la plantilla completa de hello, vea hello [espacio de nombres de Bus de servicio con el tema y suscripción] [ Service Bus namespace with topic and subscription] plantilla.</span><span class="sxs-lookup"><span data-stu-id="36e37-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="36e37-109">Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="36e37-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="36e37-110">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="36e37-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="36e37-111">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="36e37-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="36e37-112">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="36e37-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * <span data-ttu-id="36e37-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md) (Creación de un espacio de nombres de Service Bus con tema, suscripción y regla)</span><span class="sxs-lookup"><span data-stu-id="36e37-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md)</span></span>
> 
> <span data-ttu-id="36e37-114">toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque "Bus de servicio".</span><span class="sxs-lookup"><span data-stu-id="36e37-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="36e37-115">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="36e37-115">What will you deploy?</span></span>

<span data-ttu-id="36e37-116">Con esta plantilla, implementará un espacio de nombres de Bus de servicio con un tema y una suscripción.</span><span class="sxs-lookup"><span data-stu-id="36e37-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="36e37-117">Los [temas y suscripciones de Service Bus](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) proporcionan una o varias formas de comunicación en un patrón *publicación/suscripción*.</span><span class="sxs-lookup"><span data-stu-id="36e37-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="36e37-118">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="36e37-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="36e37-119">[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="36e37-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="36e37-120">parameters</span><span class="sxs-lookup"><span data-stu-id="36e37-120">Parameters</span></span>

<span data-ttu-id="36e37-121">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="36e37-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="36e37-122">plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="36e37-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="36e37-123">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="36e37-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="36e37-124">No se define parámetros para valores que siempre permanecerá Hola igual.</span><span class="sxs-lookup"><span data-stu-id="36e37-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="36e37-125">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="36e37-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="36e37-126">plantilla de Hello define Hola parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="36e37-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="36e37-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="36e37-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="36e37-128">nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="36e37-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="36e37-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="36e37-129">serviceBusTopicName</span></span>
<span data-ttu-id="36e37-130">nombre de Hola de tema de hello creado en el espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="36e37-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="36e37-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="36e37-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="36e37-132">nombre de Hola de suscripción de hello creado en el espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="36e37-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="36e37-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="36e37-133">serviceBusApiVersion</span></span>
<span data-ttu-id="36e37-134">versión de API de Service Bus de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="36e37-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="36e37-135">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="36e37-135">Resources toodeploy</span></span>
<span data-ttu-id="36e37-136">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**con tema y suscripción.</span><span class="sxs-lookup"><span data-stu-id="36e37-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="36e37-137">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="36e37-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="36e37-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36e37-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="36e37-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="36e37-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="36e37-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="36e37-140">Next steps</span></span>
<span data-ttu-id="36e37-141">Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos mediante la visualización de estos artículos:</span><span class="sxs-lookup"><span data-stu-id="36e37-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="36e37-142">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="36e37-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="36e37-143">Administrar recursos de Service Bus con hello Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="36e37-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
