---
title: "Creación de recursos de Azure Service Bus con las plantillas de Azure Resource Manager | Microsoft Docs"
description: "Uso de las plantillas de Azure Resource Manager para automatizar la creación de recursos de Bus de servicio"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="74959-103">Creación de recursos de Bus de servicio con las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74959-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="74959-104">Este artículo describe cómo crear e implementar recursos de Service Bus y Event Hubs con plantillas de Azure Resource Manager, PowerShell y el proveedor de recursos de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="74959-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="74959-105">Las plantillas de Azure Resource Manager ayudan a definir los recursos que se implementarán en una solución, y a especificar parámetros y variables que permitan introducir valores de entrada para distintos entornos.</span><span class="sxs-lookup"><span data-stu-id="74959-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="74959-106">La plantilla consta de JSON y expresiones que puede usar para generar valores para su implementación.</span><span class="sxs-lookup"><span data-stu-id="74959-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="74959-107">Para obtener información detallada sobre cómo escribir plantillas de Azure Resource Manager y una explicación del formato de plantilla, vea [Nociones sobre la estructura y la sintaxis de las plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="74959-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="74959-108">Los ejemplos de este artículo muestran cómo utilizar Azure Resource Manager para crear una entidad de mensajería (cola) y un espacio de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="74959-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="74959-109">Para obtener otros ejemplos de plantillas, visite la [Galería de plantillas de inicio rápido de Azure][Azure Quickstart Templates gallery] y busque "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="74959-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="74959-110">Plantillas de Resource Manager para Service Bus</span><span class="sxs-lookup"><span data-stu-id="74959-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="74959-111">Estas plantillas de Service Bus y Azure Resource Manager están disponibles para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="74959-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="74959-112">Haga clic en los siguientes vínculos para obtener más información sobre cada uno, con vínculos a las plantillas de GitHub:</span><span class="sxs-lookup"><span data-stu-id="74959-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="74959-113">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="74959-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="74959-114">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="74959-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="74959-115">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="74959-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="74959-116">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="74959-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="74959-117">Creación de un espacio de nombres de Service Bus con un tema, una suscripción y una regla</span><span class="sxs-lookup"><span data-stu-id="74959-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="74959-118">Implementación con PowerShell</span><span class="sxs-lookup"><span data-stu-id="74959-118">Deploy with PowerShell</span></span>

<span data-ttu-id="74959-119">El siguiente procedimiento describe cómo usar PowerShell para implementar una plantilla de Azure Resource Manager que crea un espacio de nombres de Service Bus de nivel **Estándar** y una cola dentro de ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="74959-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="74959-120">Este ejemplo se basa en la plantilla de [Creación de un espacio de nombres de Service Bus con cola](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue).</span><span class="sxs-lookup"><span data-stu-id="74959-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="74959-121">El flujo de trabajo aproximado es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="74959-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="74959-122">Instale PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74959-122">Install PowerShell.</span></span>
2. <span data-ttu-id="74959-123">Cree la plantilla y (opcionalmente) un archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="74959-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="74959-124">En PowerShell, inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="74959-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="74959-125">Si no existe, cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74959-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="74959-126">Pruebe la implementación.</span><span class="sxs-lookup"><span data-stu-id="74959-126">Test the deployment.</span></span>
6. <span data-ttu-id="74959-127">Si lo desea, establezca el modo de implementación.</span><span class="sxs-lookup"><span data-stu-id="74959-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="74959-128">Implemente la plantilla.</span><span class="sxs-lookup"><span data-stu-id="74959-128">Deploy the template.</span></span>

<span data-ttu-id="74959-129">Para obtener información completa sobre la implementación de plantillas de Azure Resource Manager, vea [Implementación de recursos con las plantillas de Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="74959-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="74959-130">Instale PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74959-130">Install PowerShell</span></span>

<span data-ttu-id="74959-131">Instale Azure PowerShell siguiendo las instrucciones de [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps) (Introducción a Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="74959-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="74959-132">Creación de una plantilla</span><span class="sxs-lookup"><span data-stu-id="74959-132">Create a template</span></span>

<span data-ttu-id="74959-133">Clone o copie la plantilla [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) de GitHub:</span><span class="sxs-lookup"><span data-stu-id="74959-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="74959-134">Creación de un archivo de parámetros (opcional)</span><span class="sxs-lookup"><span data-stu-id="74959-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="74959-135">Para utilizar un archivo de parámetros opcional, copie el archivo [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="74959-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="74959-136">Reemplace el valor de `serviceBusNamespaceName` por el nombre del espacio de nombres de Bus de servicio que desee crear en esta implementación y sustituya el valor de `serviceBusQueueName` por el nombre de la cola que desee crear.</span><span class="sxs-lookup"><span data-stu-id="74959-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="74959-137">Para más información, consulte el tema [Parámetros](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span><span class="sxs-lookup"><span data-stu-id="74959-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="74959-138">Inicio de sesión en Azure y establecimiento de la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="74959-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="74959-139">En una secuencia de comandos de PowerShell, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="74959-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="74959-140">Se le solicitará que inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="74959-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="74959-141">Después de iniciar sesión, ejecute el siguiente comando para ver sus suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="74959-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="74959-142">Este comando devuelve una lista de suscripciones de Azure disponibles.</span><span class="sxs-lookup"><span data-stu-id="74959-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="74959-143">Seleccione una suscripción para la sesión actual mediante la ejecución del siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="74959-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="74959-144">Reemplace `<YourSubscriptionId>` por el GUID de la suscripción de Azure que desea usar.</span><span class="sxs-lookup"><span data-stu-id="74959-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="74959-145">Configuración del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="74959-145">Set the resource group</span></span>

<span data-ttu-id="74959-146">Si no tiene un grupo de recursos existente, cree uno con el comando **New-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="74959-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="74959-147">Proporcione el nombre del grupo de recursos y la ubicación que desee utilizar.</span><span class="sxs-lookup"><span data-stu-id="74959-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="74959-148">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="74959-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="74959-149">Si es correcto, se muestra un resumen del nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74959-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="74959-150">Prueba de la implementación</span><span class="sxs-lookup"><span data-stu-id="74959-150">Test the deployment</span></span>

<span data-ttu-id="74959-151">Valide la implementación mediante la ejecución del cmdlet `Test-AzureRmResourceGroupDeployment`.</span><span class="sxs-lookup"><span data-stu-id="74959-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="74959-152">Al probar la implementación, proporcione los parámetros exactamente como lo haría al ejecutar la implementación.</span><span class="sxs-lookup"><span data-stu-id="74959-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="74959-153">Creación de la implementación</span><span class="sxs-lookup"><span data-stu-id="74959-153">Create the deployment</span></span>

<span data-ttu-id="74959-154">Para crear la nueva implementación, ejecute el cmdlet `New-AzureRmResourceGroupDeployment` y proporcione los parámetros necesarios cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="74959-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="74959-155">Los parámetros incluyen un nombre para la implementación, el nombre del grupo de recursos y la ruta de acceso o la dirección URL al archivo de plantilla.</span><span class="sxs-lookup"><span data-stu-id="74959-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="74959-156">Si no se especifica el parámetro **Modo**, se usa el valor predeterminado **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="74959-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="74959-157">Para más información, vea [Implementaciones incrementales y completas](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="74959-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="74959-158">El siguiente comando le solicita los tres parámetros en la ventana de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="74959-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="74959-159">Para especificar un archivo de parámetros en su lugar, use el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="74959-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="74959-160">También puede utilizar parámetros en línea cuando ejecute el cmdlet de implementación.</span><span class="sxs-lookup"><span data-stu-id="74959-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="74959-161">El comando es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="74959-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="74959-162">Para ejecutar una implementación [completa](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments), establezca el parámetro **Modo** en **Completo**:</span><span class="sxs-lookup"><span data-stu-id="74959-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="74959-163">Comprobar la implementación</span><span class="sxs-lookup"><span data-stu-id="74959-163">Verify the deployment</span></span>
<span data-ttu-id="74959-164">Si los recursos se implementan correctamente, aparecerá un resumen de la implementación en la ventana de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="74959-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="74959-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74959-165">Next steps</span></span>
<span data-ttu-id="74959-166">Ahora ha visto los comandos y el flujo de trabajo básico para la implementación de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74959-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="74959-167">Para obtener información más detallada, viste los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="74959-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="74959-168">[Información general sobre Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="74959-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="74959-169">[Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="74959-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="74959-170">Creación de plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="74959-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
