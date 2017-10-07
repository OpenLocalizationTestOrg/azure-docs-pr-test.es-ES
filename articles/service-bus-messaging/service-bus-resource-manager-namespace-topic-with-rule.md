---
title: "aaaCreate suscripción de tema de Bus de servicio de Azure y regla con la plantilla del Administrador de recursos de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="950c9-103">Creación de un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="950c9-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="950c9-104">Este artículo muestra cómo toouse una plantilla de administrador de recursos de Azure crea un espacio de nombres de Bus de servicio con un tema, la suscripción y la regla (filtro).</span><span class="sxs-lookup"><span data-stu-id="950c9-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="950c9-105">Aprenderá cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="950c9-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet los requisitos</span><span class="sxs-lookup"><span data-stu-id="950c9-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="950c9-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="950c9-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="950c9-108">Para más información sobre prácticas y patrones de convenciones de nomenclatura de recursos de Azure, consulte [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources](Convenciones de nomenclatura recomendadas para los recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="950c9-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="950c9-109">Para la plantilla completa de hello, vea hello [espacio de nombres de Bus de servicio con el tema y suscripción, regla] [ Service Bus namespace with topic, subscription, and rule] plantilla.</span><span class="sxs-lookup"><span data-stu-id="950c9-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="950c9-110">Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="950c9-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="950c9-111">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="950c9-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="950c9-112">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="950c9-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="950c9-113">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="950c9-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="950c9-114">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="950c9-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="950c9-115">toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y búsqueda de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="950c9-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="950c9-116">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="950c9-116">What will you deploy?</span></span>

<span data-ttu-id="950c9-117">Con esta plantilla, implementará un espacio de nombres de Bus de servicio con un tema, una suscripción y una regla (filtro).</span><span class="sxs-lookup"><span data-stu-id="950c9-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="950c9-118">Los [temas y suscripciones de Service Bus](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) proporcionan una o varias formas de comunicación en un patrón *publicación/suscripción*.</span><span class="sxs-lookup"><span data-stu-id="950c9-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="950c9-119">Cuando se usan temas y suscripciones, componentes de una aplicación distribuida no se comunican directamente entre sí, en su lugar que intercambian mensajes a través del tema que actúa como intermediario. Un tema de tooa de suscripción es similar a una cola virtual que recibe copias de mensajes que se enviaron toohello tema.</span><span class="sxs-lookup"><span data-stu-id="950c9-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="950c9-120">Un filtro de suscripción le permite toospecify que envían los mensajes tooa tema debe aparecer dentro de una suscripción de tema específico.</span><span class="sxs-lookup"><span data-stu-id="950c9-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="950c9-121">¿Cuáles son las reglas (filtros)?</span><span class="sxs-lookup"><span data-stu-id="950c9-121">What are rules (filters)?</span></span>

<span data-ttu-id="950c9-122">En muchos escenarios, los mensajes que tienen características específicas deben procesarse de maneras diferentes.</span><span class="sxs-lookup"><span data-stu-id="950c9-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="950c9-123">tooenable esto, puede configurar mensajes de toofind de las suscripciones que tienen propiedades concretas y, a continuación, realizan propiedades toothose de modificaciones.</span><span class="sxs-lookup"><span data-stu-id="950c9-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="950c9-124">Aunque las suscripciones de Bus de servicio ven todos los mensajes enviados toohello tema, puede copiar solo un subconjunto de esas cola de mensajes toohello suscripción virtual.</span><span class="sxs-lookup"><span data-stu-id="950c9-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="950c9-125">Esto se consigue mediante los filtros de suscripción.</span><span class="sxs-lookup"><span data-stu-id="950c9-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="950c9-126">toolearn más información acerca de las reglas (filtros), consulte [reglas y acciones](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="950c9-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="950c9-127">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="950c9-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="950c9-128">[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="950c9-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="950c9-129">parameters</span><span class="sxs-lookup"><span data-stu-id="950c9-129">Parameters</span></span>

<span data-ttu-id="950c9-130">Con el Administrador de recursos de Azure, debe definir parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="950c9-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="950c9-131">plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="950c9-132">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="950c9-133">No se define parámetros para valores que permanezcan siempre Hola igual.</span><span class="sxs-lookup"><span data-stu-id="950c9-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="950c9-134">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="950c9-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="950c9-135">plantilla de Hello define Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="950c9-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="950c9-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="950c9-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="950c9-137">nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="950c9-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="950c9-138">serviceBusTopicName</span></span>
<span data-ttu-id="950c9-139">nombre de Hola de tema de hello creado en el espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="950c9-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="950c9-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="950c9-141">nombre de Hola de suscripción de hello creado en el espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="950c9-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="950c9-142">serviceBusRuleName</span></span>
<span data-ttu-id="950c9-143">nombre de Hola de rule(filter) Hola creado en el espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="950c9-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="950c9-144">serviceBusApiVersion</span></span>
<span data-ttu-id="950c9-145">versión de API de Service Bus de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="950c9-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="950c9-146">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="950c9-146">Resources toodeploy</span></span>
<span data-ttu-id="950c9-147">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**con tema, suscripción y reglas.</span><span class="sxs-lookup"><span data-stu-id="950c9-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="950c9-148">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="950c9-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="950c9-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="950c9-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="950c9-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="950c9-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="950c9-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="950c9-151">Next steps</span></span>
<span data-ttu-id="950c9-152">Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos mediante la visualización de estos artículos:</span><span class="sxs-lookup"><span data-stu-id="950c9-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="950c9-153">Administración de Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="950c9-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="950c9-154">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="950c9-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="950c9-155">Administrar recursos de Service Bus con hello Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="950c9-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

