---
title: "Creación de un espacio de nombres de Azure Service Bus con un tema, una suscripción y una regla mediante una plantilla de Azure Resource Manager | Microsoft Docs"
description: "Creación de un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla mediante una plantilla de Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="c1423-103">Creación de un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1423-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="c1423-104">En este artículo se muestra cómo utilizar una plantilla de Azure Resource Manager que crea un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla (filtro).</span><span class="sxs-lookup"><span data-stu-id="c1423-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="c1423-105">Aprenderá a definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="c1423-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="c1423-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="c1423-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="c1423-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c1423-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="c1423-108">Para más información sobre prácticas y patrones de convenciones de nomenclatura de recursos de Azure, consulte [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources](Convenciones de nomenclatura recomendadas para los recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="c1423-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="c1423-109">Para verla completa, consulte la plantilla de [espacio de nombres de Service Bus con tema, suscripción y regla][Service Bus namespace with topic, subscription, and rule].</span><span class="sxs-lookup"><span data-stu-id="c1423-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="c1423-110">Las siguientes plantillas de Azure Resource Manager están disponibles para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="c1423-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="c1423-111">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="c1423-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="c1423-112">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="c1423-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="c1423-113">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="c1423-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="c1423-114">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="c1423-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="c1423-115">Para buscar las últimas plantillas, visite la galería [Plantillas de inicio rápido de Azure][Azure Quickstart Templates] y busque "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="c1423-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="c1423-116">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="c1423-116">What will you deploy?</span></span>

<span data-ttu-id="c1423-117">Con esta plantilla, implementará un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla (filtro).</span><span class="sxs-lookup"><span data-stu-id="c1423-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="c1423-118">Los [temas y suscripciones de Service Bus](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) proporcionan una o varias formas de comunicación en un patrón *publicación/suscripción*.</span><span class="sxs-lookup"><span data-stu-id="c1423-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="c1423-119">Al usar temas y suscripciones, los componentes de una aplicación distribuida no se comunican directamente entre ellos, sino que intercambian mensajes a través de un tema que actúa como un intermediario. Una suscripción a un tema es similar a una cola virtual que recibe copias de mensajes que se enviaron al tema.</span><span class="sxs-lookup"><span data-stu-id="c1423-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="c1423-120">Un filtro de una suscripción permite especificar qué mensajes enviados a un tema deben aparecer dentro de una suscripción a un tema determinado.</span><span class="sxs-lookup"><span data-stu-id="c1423-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="c1423-121">¿Cuáles son las reglas (filtros)?</span><span class="sxs-lookup"><span data-stu-id="c1423-121">What are rules (filters)?</span></span>

<span data-ttu-id="c1423-122">En muchos escenarios, los mensajes que tienen características específicas deben procesarse de maneras diferentes.</span><span class="sxs-lookup"><span data-stu-id="c1423-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="c1423-123">Para permitirlo, puede configurar suscripciones para buscar los mensajes que tengan propiedades específicas y, después, realizar modificaciones en dichas propiedades.</span><span class="sxs-lookup"><span data-stu-id="c1423-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="c1423-124">Aunque las suscripciones de Service Bus ven todos los mensajes enviados al tema, solo se puede copiar un subconjunto de dichos mensajes en la cola de suscripción virtual.</span><span class="sxs-lookup"><span data-stu-id="c1423-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="c1423-125">Esto se consigue mediante los filtros de suscripción.</span><span class="sxs-lookup"><span data-stu-id="c1423-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="c1423-126">Para más información sobre las reglas (filtros), vea [Reglas y acciones](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="c1423-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="c1423-127">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1423-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="c1423-128">[![Implementación en Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="c1423-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="c1423-129">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c1423-129">Parameters</span></span>

<span data-ttu-id="c1423-130">Con Azure Resource Manager, se definen los parámetros de los valores que desea especificar al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="c1423-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="c1423-131">La plantilla incluye una sección denominada `Parameters` que contiene todos los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="c1423-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="c1423-132">Debe definir un parámetro para esos valores que variarán según el proyecto que vaya a implementar o según el entorno en el que vaya a realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="c1423-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="c1423-133">No defina parámetros para valores que siempre permanezcan igual.</span><span class="sxs-lookup"><span data-stu-id="c1423-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="c1423-134">Cada valor de parámetro se usa en la plantilla para definir los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="c1423-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="c1423-135">La plantilla define los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="c1423-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="c1423-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="c1423-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="c1423-137">El nombre del espacio de nombres de Bus de servicio que crear.</span><span class="sxs-lookup"><span data-stu-id="c1423-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="c1423-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="c1423-138">serviceBusTopicName</span></span>
<span data-ttu-id="c1423-139">El nombre del tema creado en el espacio de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="c1423-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="c1423-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="c1423-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="c1423-141">El nombre de la suscripción creada en el espacio de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="c1423-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="c1423-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="c1423-142">serviceBusRuleName</span></span>
<span data-ttu-id="c1423-143">El nombre de la regla (filtro) creada en el espacio de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="c1423-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="c1423-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="c1423-144">serviceBusApiVersion</span></span>
<span data-ttu-id="c1423-145">La versión de la API de Bus de servicio de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="c1423-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="c1423-146">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="c1423-146">Resources to deploy</span></span>
<span data-ttu-id="c1423-147">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**con tema, suscripción y reglas.</span><span class="sxs-lookup"><span data-stu-id="c1423-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="c1423-148">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="c1423-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="c1423-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1423-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="c1423-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c1423-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="c1423-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1423-151">Next steps</span></span>
<span data-ttu-id="c1423-152">Ahora que ha creado e implementado recursos con Azure Resource Manager, estos artículos le enseñarán como administrarlos:</span><span class="sxs-lookup"><span data-stu-id="c1423-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="c1423-153">Administración de Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="c1423-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="c1423-154">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1423-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="c1423-155">Administración de recursos de Bus de servicio con el Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="c1423-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

