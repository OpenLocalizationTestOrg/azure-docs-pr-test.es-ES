---
title: "regla de autorización de Bus de servicio aaaCreate con plantilla del Administrador de recursos de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="d4f19-103">Creación de una regla de autorización de Bus de servicio para un espacio de nombres y una cola mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d4f19-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="d4f19-104">Este artículo se muestra cómo toouse una plantilla de administrador de recursos de Azure que crea un [regla de autorización](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) para un espacio de nombres de Bus de servicio y una cola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="d4f19-105">Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="d4f19-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="d4f19-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="d4f19-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="d4f19-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="d4f19-108">Para la plantilla completa de hello, vea hello [plantilla de regla de autorización de Bus de servicio] [ Service Bus auth rule template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d4f19-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="d4f19-109">Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="d4f19-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="d4f19-110">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="d4f19-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="d4f19-111">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="d4f19-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="d4f19-112">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="d4f19-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * <span data-ttu-id="d4f19-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md) (Creación de un espacio de nombres de Service Bus con tema, suscripción y regla)</span><span class="sxs-lookup"><span data-stu-id="d4f19-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md)</span></span>
> 
> <span data-ttu-id="d4f19-114">toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y busque "Bus de servicio".</span><span class="sxs-lookup"><span data-stu-id="d4f19-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="d4f19-115">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="d4f19-115">What will you deploy?</span></span>
<span data-ttu-id="d4f19-116">Con esta plantilla, implementará una regla de autorización de Bus de servicio para una entidad de mensajería y espacio de nombres (una cola en este caso).</span><span class="sxs-lookup"><span data-stu-id="d4f19-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="d4f19-117">Esta plantilla usa la [firma de acceso compartido (SAS)](service-bus-sas.md) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d4f19-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="d4f19-118">SAS permite que las aplicaciones tooauthenticate tooService Bus mediante una clave de acceso configurada en el espacio de nombres de Hola o en hello entidad (cola o tema) de mensajería con qué derechos específicos que están asociados.</span><span class="sxs-lookup"><span data-stu-id="d4f19-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="d4f19-119">A continuación, puede usar esta clave toogenerate un token SAS que los clientes pueden usar a su vez tooauthenticate tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="d4f19-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="d4f19-120">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="d4f19-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="d4f19-121">[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d4f19-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="d4f19-122">parameters</span><span class="sxs-lookup"><span data-stu-id="d4f19-122">Parameters</span></span>

<span data-ttu-id="d4f19-123">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="d4f19-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="d4f19-124">plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="d4f19-125">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="d4f19-126">No se define parámetros para valores que siempre permanecerá Hola igual.</span><span class="sxs-lookup"><span data-stu-id="d4f19-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="d4f19-127">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="d4f19-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="d4f19-128">plantilla de Hello define Hola parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="d4f19-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="d4f19-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="d4f19-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="d4f19-130">nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="d4f19-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="d4f19-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="d4f19-132">nombre de Hola de regla de autorización de hello para el espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="d4f19-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="d4f19-133">serviceBusQueueName</span></span>
<span data-ttu-id="d4f19-134">nombre de Hola de cola de hello en el espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="d4f19-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="d4f19-135">serviceBusApiVersion</span></span>
<span data-ttu-id="d4f19-136">versión de API de Service Bus de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f19-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="d4f19-137">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="d4f19-137">Resources toodeploy</span></span>
<span data-ttu-id="d4f19-138">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**y una regla de autorización de Bus de servicio para el espacio de nombres y la entidad.</span><span class="sxs-lookup"><span data-stu-id="d4f19-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="d4f19-139">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="d4f19-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d4f19-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4f19-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="d4f19-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d4f19-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="d4f19-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4f19-142">Next steps</span></span>
<span data-ttu-id="d4f19-143">Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos mediante la visualización de estos artículos:</span><span class="sxs-lookup"><span data-stu-id="d4f19-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="d4f19-144">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4f19-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="d4f19-145">Administrar recursos de Service Bus con hello Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="d4f19-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="d4f19-146">Autenticación y autorización de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="d4f19-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
