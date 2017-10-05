---
title: "Creación de reglas de autorización de Service Bus con plantillas de Azure Resource Manager | Microsoft Docs"
description: "Creación de una regla de autorización de Bus de servicio para un espacio de nombres y una cola mediante una plantilla de Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fbd2372829a1aefa2c080c0a8a72b9ff4375b16f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="b84c1-103">Creación de una regla de autorización de Bus de servicio para un espacio de nombres y una cola mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b84c1-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="b84c1-104">En este artículo se muestra cómo utilizar una plantilla de Azure Resource Manager que crea una [regla de autorización](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) para una cola y un espacio de nombres de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b84c1-104">This article shows how to use an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="b84c1-105">Aprenderá a definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="b84c1-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="b84c1-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="b84c1-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="b84c1-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="b84c1-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="b84c1-108">Para ver la plantilla completa, consulte la [plantilla de regla de autorización de Service Bus][Service Bus auth rule template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b84c1-108">For the complete template, see the [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="b84c1-109">Las siguientes plantillas de Azure Resource Manager están disponibles para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="b84c1-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="b84c1-110">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b84c1-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="b84c1-111">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="b84c1-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="b84c1-112">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="b84c1-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="b84c1-113">Creación de un espacio de nombres de Service Bus con un tema, una suscripción y una regla</span><span class="sxs-lookup"><span data-stu-id="b84c1-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="b84c1-114">Para buscar las últimas plantillas, visite la galería [Plantillas de inicio rápido de Azure][Azure Quickstart Templates] y busque "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="b84c1-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="b84c1-115">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="b84c1-115">What will you deploy?</span></span>
<span data-ttu-id="b84c1-116">Con esta plantilla, implementará una regla de autorización de Bus de servicio para una entidad de mensajería y espacio de nombres (una cola en este caso).</span><span class="sxs-lookup"><span data-stu-id="b84c1-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="b84c1-117">Esta plantilla usa la [firma de acceso compartido (SAS)](service-bus-sas.md) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="b84c1-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="b84c1-118">SAS permite a las aplicaciones autenticarse en el Bus de servicio mediante una clave de acceso configurada en el espacio de nombres o en la entidad de mensajería (cola o tema) al que se asocian derechos específicos.</span><span class="sxs-lookup"><span data-stu-id="b84c1-118">SAS enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="b84c1-119">A continuación, puede usar esta clave para generar un token SAS que a su vez, los clientes pueden usar para autenticarse en el Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b84c1-119">You can then use this key to generate a SAS token that clients can in turn use to authenticate to Service Bus.</span></span>

<span data-ttu-id="b84c1-120">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="b84c1-120">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="b84c1-121">[![Implementación en Azure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b84c1-121">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b84c1-122">Parámetros</span><span class="sxs-lookup"><span data-stu-id="b84c1-122">Parameters</span></span>

<span data-ttu-id="b84c1-123">Con el Administrador de recursos de Azure, se definen los parámetros de los valores que desea especificar al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="b84c1-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="b84c1-124">La plantilla incluye una sección denominada `Parameters` que contiene todos los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="b84c1-124">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="b84c1-125">Debe definir un parámetro para los valores que variarán según el proyecto que vaya a implementar o según el entorno en el que vaya a realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="b84c1-125">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="b84c1-126">No defina parámetros para valores que vayan a permanecer igual.</span><span class="sxs-lookup"><span data-stu-id="b84c1-126">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="b84c1-127">Cada valor de parámetro se usa en la plantilla para definir los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="b84c1-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="b84c1-128">La plantilla define los parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="b84c1-128">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="b84c1-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="b84c1-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="b84c1-130">El nombre del espacio de nombres de Bus de servicio que crear.</span><span class="sxs-lookup"><span data-stu-id="b84c1-130">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="b84c1-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="b84c1-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="b84c1-132">El nombre de la regla de autorización para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b84c1-132">The name of the authorization rule for the namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="b84c1-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="b84c1-133">serviceBusQueueName</span></span>
<span data-ttu-id="b84c1-134">El nombre de la cola en el espacio de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b84c1-134">The name of the queue in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="b84c1-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="b84c1-135">serviceBusApiVersion</span></span>
<span data-ttu-id="b84c1-136">La versión de la API de Bus de servicio de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="b84c1-136">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="b84c1-137">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="b84c1-137">Resources to deploy</span></span>
<span data-ttu-id="b84c1-138">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**y una regla de autorización de Bus de servicio para el espacio de nombres y la entidad.</span><span class="sxs-lookup"><span data-stu-id="b84c1-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="b84c1-139">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="b84c1-139">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b84c1-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b84c1-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="b84c1-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b84c1-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="b84c1-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b84c1-142">Next steps</span></span>
<span data-ttu-id="b84c1-143">Ahora que ha creado e implementado recursos con Azure Resource Manager, estos artículos le enseñarán como administrarlos:</span><span class="sxs-lookup"><span data-stu-id="b84c1-143">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="b84c1-144">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b84c1-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="b84c1-145">Administración de recursos de Bus de servicio con el Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b84c1-145">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="b84c1-146">Autenticación y autorización de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b84c1-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
