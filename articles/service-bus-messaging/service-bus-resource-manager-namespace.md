---
title: "Creación de un espacio de nombres de Service Bus con una plantilla de Azure Resource Manager | Microsoft Docs"
description: Utilice la plantilla de Azure Resource Manager para crear un espacio de nombres de Bus de servicio
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
ms.openlocfilehash: 8fff390919a1807995646dab322b4cbe56dd0268
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="3e72d-103">Creación de un espacio de nombres del Bus de servicio mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3e72d-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="3e72d-104">En este artículo se describe cómo utilizar una plantilla de Azure Resource Manager que crea un espacio de nombres de Service Bus del tipo **Mensajería** con una SKU de nivel básico o estándar.</span><span class="sxs-lookup"><span data-stu-id="3e72d-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="3e72d-105">El artículo también define los parámetros que se especifican para la ejecución de la implementación.</span><span class="sxs-lookup"><span data-stu-id="3e72d-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="3e72d-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="3e72d-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="3e72d-107">Para más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates] (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3e72d-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="3e72d-108">Para ver la plantilla completa, consulte la [plantilla de espacio de nombres de Service Bus][Service Bus namespace template] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e72d-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="3e72d-109">Las siguientes plantillas de Azure Resource Manager están disponibles para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="3e72d-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="3e72d-110">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="3e72d-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="3e72d-111">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="3e72d-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="3e72d-112">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="3e72d-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="3e72d-113">Creación de un espacio de nombres de Service Bus con un tema, una suscripción y una regla</span><span class="sxs-lookup"><span data-stu-id="3e72d-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="3e72d-114">Para buscar las últimas plantillas, visite la galería [Plantillas de inicio rápido de Azure][Azure Quickstart Templates] y busque "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="3e72d-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="3e72d-115">¿Qué va a implementar?</span><span class="sxs-lookup"><span data-stu-id="3e72d-115">What will you deploy?</span></span>
<span data-ttu-id="3e72d-116">Con esta plantilla, implementará un espacio de nombres de Service Bus con una SKU de nivel [básico, estándar o premium](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3e72d-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="3e72d-117">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e72d-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="3e72d-118">[![Implementación en Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3e72d-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3e72d-119">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3e72d-119">Parameters</span></span>
<span data-ttu-id="3e72d-120">Con el Administrador de recursos de Azure, se definen los parámetros de los valores que desea especificar al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="3e72d-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="3e72d-121">La plantilla incluye una sección denominada `Parameters` que contiene todos los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="3e72d-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="3e72d-122">Debe definir un parámetro para los valores que variarán según el proyecto que vaya a implementar o según el entorno en el que vaya a realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="3e72d-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="3e72d-123">No defina parámetros para valores que vayan a permanecer igual.</span><span class="sxs-lookup"><span data-stu-id="3e72d-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="3e72d-124">Cada valor de parámetro se usa en la plantilla para definir los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="3e72d-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="3e72d-125">Esta plantilla define los parámetros siguientes.</span><span class="sxs-lookup"><span data-stu-id="3e72d-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="3e72d-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="3e72d-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="3e72d-127">El nombre del espacio de nombres de Bus de servicio que crear.</span><span class="sxs-lookup"><span data-stu-id="3e72d-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="3e72d-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="3e72d-128">serviceBusSKU</span></span>
<span data-ttu-id="3e72d-129">El nombre de la [SKU](https://azure.microsoft.com/pricing/details/service-bus/) de Bus de servicio que crear.</span><span class="sxs-lookup"><span data-stu-id="3e72d-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

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
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="3e72d-130">La plantilla define los valores permitidos para este parámetro (Básico, Estándar o Premium) y asigna un valor predeterminado (Estándar) si no se especifica ningún valor.</span><span class="sxs-lookup"><span data-stu-id="3e72d-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="3e72d-131">Para más información sobre los precios de Service Bus, consulte [Precios y facturación de Service Bus][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="3e72d-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="3e72d-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="3e72d-132">serviceBusApiVersion</span></span>
<span data-ttu-id="3e72d-133">La versión de la API de Bus de servicio de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="3e72d-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="3e72d-134">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="3e72d-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="3e72d-135">Espacio de nombres de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="3e72d-135">Service Bus namespace</span></span>
<span data-ttu-id="3e72d-136">Crea un espacio de nombres de Bus de servicio estándar de tipo **Mensajería**.</span><span class="sxs-lookup"><span data-stu-id="3e72d-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="3e72d-137">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="3e72d-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="3e72d-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e72d-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="3e72d-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3e72d-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="3e72d-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e72d-140">Next steps</span></span>
<span data-ttu-id="3e72d-141">Ahora que ha creado e implementado recursos con Azure Resource Manager, lea los artículos siguientes para obtener información sobre cómo administrar dichos recursos:</span><span class="sxs-lookup"><span data-stu-id="3e72d-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="3e72d-142">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e72d-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="3e72d-143">Administración de recursos de Bus de servicio con el Explorador de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="3e72d-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
