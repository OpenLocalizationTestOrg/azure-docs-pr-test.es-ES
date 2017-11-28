---
title: recursos de Service Bus de Azure de aaaCreate usando plantillas del Administrador de recursos de Azure | Documentos de Microsoft
description: "Utilizar la creación de Azure Resource Manager plantillas tooautomate Hola de recursos de Bus de servicio"
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="3de1e-103">Creación de recursos de Bus de servicio con las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3de1e-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="3de1e-104">Este artículo se describe cómo toocreate e implementar recursos de Bus de servicio mediante plantillas, PowerShell y proveedor de recursos de Bus de servicio de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3de1e-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="3de1e-105">Plantillas de administrador de recursos de Azure ayudan a definir hello toodeploy de recursos para una solución y toospecify parámetros y variables que permiten valores tooinput para diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="3de1e-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="3de1e-106">plantilla de Hello consta de JSON y expresiones que puede utilizar valores de tooconstruct para su implementación.</span><span class="sxs-lookup"><span data-stu-id="3de1e-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="3de1e-107">Para obtener información detallada sobre cómo escribir plantillas del Administrador de recursos de Azure y una explicación del formato de la plantilla de hello, consulte [estructura y la sintaxis de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3de1e-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3de1e-108">Hola ejemplos en esta presentación de artículo cómo toouse Azure Resource Manager toocreate un espacio de nombres de Bus de servicio y la mensajería de entidad (cola).</span><span class="sxs-lookup"><span data-stu-id="3de1e-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="3de1e-109">Para obtener ejemplos de la plantilla, visite hello [Galería de plantillas de inicio rápido de Azure] [ Azure Quickstart Templates gallery] y busque "Bus de servicio".</span><span class="sxs-lookup"><span data-stu-id="3de1e-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="3de1e-110">Plantillas de Resource Manager para Service Bus</span><span class="sxs-lookup"><span data-stu-id="3de1e-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="3de1e-111">Estas plantillas de Service Bus y Azure Resource Manager están disponibles para su descarga e implementación.</span><span class="sxs-lookup"><span data-stu-id="3de1e-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="3de1e-112">Haga clic en hello siguientes vínculos para obtener más información acerca de cada uno, con plantillas de toohello de vínculos en GitHub:</span><span class="sxs-lookup"><span data-stu-id="3de1e-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="3de1e-113">Creación de un espacio de nombres de bus de servicio</span><span class="sxs-lookup"><span data-stu-id="3de1e-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="3de1e-114">Creación de un espacio de nombres de Bus de servicio con cola</span><span class="sxs-lookup"><span data-stu-id="3de1e-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="3de1e-115">Creación de un espacio de nombres de Bus de servicio con un tema y una suscripción</span><span class="sxs-lookup"><span data-stu-id="3de1e-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="3de1e-116">Creación de un espacio de nombres de Bus de servicio con regla de autorización y cola</span><span class="sxs-lookup"><span data-stu-id="3de1e-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="3de1e-117">Creación de un espacio de nombres de Service Bus con un tema, una suscripción y una regla</span><span class="sxs-lookup"><span data-stu-id="3de1e-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="3de1e-118">Implementación con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de1e-118">Deploy with PowerShell</span></span>

<span data-ttu-id="3de1e-119">Hello siguiente procedimiento describe cómo toouse PowerShell toodeploy una plantilla de administrador de recursos de Azure que crea un **estándar** de nivel de espacio de nombres de Bus de servicio y una cola dentro de ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="3de1e-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="3de1e-120">En este ejemplo se basa en hello [crear un espacio de nombres de Bus de servicio con cola](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) plantilla.</span><span class="sxs-lookup"><span data-stu-id="3de1e-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="3de1e-121">flujo de trabajo aproximado de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="3de1e-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="3de1e-122">Instale PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3de1e-122">Install PowerShell.</span></span>
2. <span data-ttu-id="3de1e-123">Crear plantilla de Hola y (opcionalmente) un archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="3de1e-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="3de1e-124">En PowerShell, inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3de1e-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="3de1e-125">Si no existe, cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3de1e-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="3de1e-126">Probar la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de1e-126">Test hello deployment.</span></span>
6. <span data-ttu-id="3de1e-127">Si lo desea, establezca el modo de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de1e-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="3de1e-128">Implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de1e-128">Deploy hello template.</span></span>

<span data-ttu-id="3de1e-129">Para obtener información completa sobre la implementación de plantillas de Azure Resource Manager, vea [Implementación de recursos con las plantillas de Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="3de1e-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="3de1e-130">Instale PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3de1e-130">Install PowerShell</span></span>

<span data-ttu-id="3de1e-131">Instale Azure PowerShell siguiendo las instrucciones de hello en [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="3de1e-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="3de1e-132">Creación de una plantilla</span><span class="sxs-lookup"><span data-stu-id="3de1e-132">Create a template</span></span>

<span data-ttu-id="3de1e-133">Hola de clon o una copia [201-servicebus-Crear-cola](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) plantilla desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="3de1e-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="3de1e-134">Creación de un archivo de parámetros (opcional)</span><span class="sxs-lookup"><span data-stu-id="3de1e-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="3de1e-135">toouse un archivo de parámetros opcionales, Hola copia [201-servicebus-Crear-cola](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) archivo.</span><span class="sxs-lookup"><span data-stu-id="3de1e-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="3de1e-136">Reemplazar el valor de Hola de `serviceBusNamespaceName` con nombre hello del espacio de nombres de Bus de servicio de Hola que desee toocreate en esta implementación y reemplazar el valor de Hola de `serviceBusQueueName` con el nombre de Hola de cola de hello desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="3de1e-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="3de1e-137">Para obtener más información, vea hello [parámetros](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) tema.</span><span class="sxs-lookup"><span data-stu-id="3de1e-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="3de1e-138">Inicie sesión en tooAzure y establecer Hola suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="3de1e-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="3de1e-139">Desde un símbolo del sistema de PowerShell, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="3de1e-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3de1e-140">Son toolog solicitada en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3de1e-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="3de1e-141">Después de iniciar sesión, ejecute hello después comando tooview las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="3de1e-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="3de1e-142">Este comando devuelve una lista de suscripciones de Azure disponibles.</span><span class="sxs-lookup"><span data-stu-id="3de1e-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="3de1e-143">Elija una suscripción para hello sesión actual ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de1e-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="3de1e-144">Reemplace `<YourSubscriptionId>` con hello GUID para hello suscripción de Azure que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="3de1e-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="3de1e-145">Grupo de recursos de Hola de conjunto</span><span class="sxs-lookup"><span data-stu-id="3de1e-145">Set hello resource group</span></span>

<span data-ttu-id="3de1e-146">Si no tiene un recurso existente de grupo, cree un nuevo grupo de recursos con Hola ** New-AzureRmResourceGroup ** comando.</span><span class="sxs-lookup"><span data-stu-id="3de1e-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="3de1e-147">Proporcione el nombre de hello del grupo de recursos de Hola y la ubicación que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="3de1e-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="3de1e-148">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3de1e-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="3de1e-149">Si se realiza correctamente, se muestra un resumen del nuevo grupo de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="3de1e-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="3de1e-150">Implementación de prueba de Hola</span><span class="sxs-lookup"><span data-stu-id="3de1e-150">Test hello deployment</span></span>

<span data-ttu-id="3de1e-151">Validación de la implementación mediante la ejecución de hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3de1e-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="3de1e-152">Al probar la implementación de hello, proporcionar parámetros exactamente como lo haría al ejecutar la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de1e-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="3de1e-153">Crear implementación de Hola</span><span class="sxs-lookup"><span data-stu-id="3de1e-153">Create hello deployment</span></span>

<span data-ttu-id="3de1e-154">toocreate Hola nueva implementación, ejecute hello `New-AzureRmResourceGroupDeployment` cmdlet y proporcionar los parámetros necesarios de hello cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="3de1e-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="3de1e-155">parámetros de Hello incluyen un nombre para la implementación, el nombre de Hola de su grupo de recursos y la ruta de acceso de Hola o el archivo de plantilla de dirección URL toohello.</span><span class="sxs-lookup"><span data-stu-id="3de1e-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="3de1e-156">Si hello **modo** no se especifica el parámetro, Hola valor predeterminado de **Incremental** se utiliza.</span><span class="sxs-lookup"><span data-stu-id="3de1e-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="3de1e-157">Para más información, vea [Implementaciones incrementales y completas](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="3de1e-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="3de1e-158">Hola después de símbolo del sistema, para los parámetros de hello tres en la ventana de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="3de1e-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="3de1e-159">toospecify un archivo de parámetros en su lugar, use Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="3de1e-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="3de1e-160">También puede utilizar parámetros en línea cuando se ejecuta el cmdlet de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de1e-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="3de1e-161">comando Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="3de1e-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="3de1e-162">toorun una [completa](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) implementación, conjunto hello **modo** parámetro demasiado**completar**:</span><span class="sxs-lookup"><span data-stu-id="3de1e-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="3de1e-163">Comprobar la implementación de Hola</span><span class="sxs-lookup"><span data-stu-id="3de1e-163">Verify hello deployment</span></span>
<span data-ttu-id="3de1e-164">Si los recursos de Hola se implementan correctamente, se muestra un resumen de implementación de hello en la ventana de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="3de1e-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3de1e-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3de1e-165">Next steps</span></span>
<span data-ttu-id="3de1e-166">Ahora ha visto el flujo de trabajo básico de Hola y comandos para la implementación de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3de1e-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="3de1e-167">Para obtener más información, visite Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="3de1e-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="3de1e-168">[Información general sobre Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="3de1e-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="3de1e-169">[Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="3de1e-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="3de1e-170">Creación de plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="3de1e-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
