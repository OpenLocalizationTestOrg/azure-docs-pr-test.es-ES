---
title: espacio de nombres de Bus de servicio de aaaCreate mediante una plantilla de Azure Resource Manager | Documentos de Microsoft
description: Use el Administrador de recursos de Azure plantilla toocreate un espacio de nombres de Bus de servicio
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="b683a-103">Creación de un espacio de nombres del Bus de servicio mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b683a-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="b683a-104">Este artículo describe cómo toouse una plantilla de administrador de recursos de Azure que crea un espacio de nombres de Bus de servicio de tipo **mensajería** a una SKU Standard/Basic.</span><span class="sxs-lookup"><span data-stu-id="b683a-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="b683a-105">artículo de Hello también define los parámetros de Hola que se especifican para la ejecución de Hola de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b683a-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="b683a-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="b683a-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="b683a-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="b683a-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="b683a-108">Para la plantilla completa de hello, vea hello [plantilla de espacio de nombres de Bus de servicio] [ Service Bus namespace template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b683a-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="b683a-109">Hola siguiendo las plantillas del Administrador de recursos de Azure está disponible para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="b683a-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="b683a-110">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="b683a-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="b683a-111">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="b683a-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="b683a-112">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="b683a-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * <span data-ttu-id="b683a-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md) (Creación de un espacio de nombres de Service Bus con tema, suscripción y regla)</span><span class="sxs-lookup"><span data-stu-id="b683a-113">[Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md)</span></span>
> 
> <span data-ttu-id="b683a-114">toocheck para las plantillas de hello más recientes, visite hello [plantillas de inicio rápido de Azure] [ Azure Quickstart Templates] galería y búsqueda de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b683a-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="b683a-115">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="b683a-115">What will you deploy?</span></span>
<span data-ttu-id="b683a-116">Con esta plantilla, implementará un espacio de nombres de Service Bus con una SKU de nivel [básico, estándar o premium](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="b683a-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="b683a-117">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="b683a-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="b683a-118">[![Implementar tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b683a-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b683a-119">parameters</span><span class="sxs-lookup"><span data-stu-id="b683a-119">Parameters</span></span>
<span data-ttu-id="b683a-120">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="b683a-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="b683a-121">plantilla de Hello incluye una sección denominada `Parameters` que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="b683a-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="b683a-122">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="b683a-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="b683a-123">No se define parámetros para valores que siempre permanecerá Hola igual.</span><span class="sxs-lookup"><span data-stu-id="b683a-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="b683a-124">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="b683a-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="b683a-125">Esta plantilla define Hola parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="b683a-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="b683a-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="b683a-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="b683a-127">nombre de Hola de toocreate de espacio de nombres de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b683a-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="b683a-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="b683a-128">serviceBusSKU</span></span>
<span data-ttu-id="b683a-129">nombre de Hola de hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="b683a-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="b683a-130">plantilla de Hello define los valores de hello permitidas para este parámetro (Basic, Standard o Premium) y asigna un valor predeterminado (estándar) si no se especifica ningún valor.</span><span class="sxs-lookup"><span data-stu-id="b683a-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="b683a-131">Para más información sobre los precios de Service Bus, consulte [Precios y facturación de Service Bus][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="b683a-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="b683a-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="b683a-132">serviceBusApiVersion</span></span>
<span data-ttu-id="b683a-133">versión de API de Service Bus de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b683a-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="b683a-134">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="b683a-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="b683a-135">Espacio de nombres de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b683a-135">Service Bus namespace</span></span>
<span data-ttu-id="b683a-136">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**.</span><span class="sxs-lookup"><span data-stu-id="b683a-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="b683a-137">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="b683a-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b683a-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b683a-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="b683a-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b683a-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="b683a-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b683a-140">Next steps</span></span>
<span data-ttu-id="b683a-141">Ahora que ha creado e implementado recursos con el Administrador de recursos de Azure, obtenga información acerca de cómo toomanage estos recursos, lea los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b683a-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="b683a-142">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b683a-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="b683a-143">Administrar recursos de Service Bus con hello Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b683a-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
