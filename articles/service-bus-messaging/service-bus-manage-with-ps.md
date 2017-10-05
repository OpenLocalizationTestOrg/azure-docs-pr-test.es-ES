---
title: Uso de PowerShell para administrar recursos de Azure Service Bus | Microsoft Docs
description: "Use el módulo de PowerShell para crear y administrar recursos de Service Bus"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 1205f9fcabf5788c970fbce257aa5ad04f32cddc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="65a8b-103">Use PowerShell para administrar recursos de Service Bus</span><span class="sxs-lookup"><span data-stu-id="65a8b-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="65a8b-104">Microsoft Azure PowerShell es un entorno de scripting que puede usar para controlar y automatizar la implementación y la administración de sus servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="65a8b-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="65a8b-105">En este artículo se describe cómo utilizar el [módulo de PowerShell de Resource Manager de Service Bus](/powershell/module/azurerm.servicebus) para aprovisionar y administrar entidades de Service Bus (espacios de nombres, colas, temas y suscripciones) mediante una consola o un script de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65a8b-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="65a8b-106">Las entidades de Service Bus también se pueden administrar mediante plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65a8b-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="65a8b-107">Para más información, consulte el artículo [Cómo crear recursos de Service Bus mediante plantillas de Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65a8b-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65a8b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="65a8b-108">Prerequisites</span></span>

<span data-ttu-id="65a8b-109">Antes de comenzar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="65a8b-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="65a8b-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="65a8b-110">An Azure subscription.</span></span> <span data-ttu-id="65a8b-111">Para obtener más información sobre cómo obtener una suscripción, consulte [Opciones de compra][purchase options], [ofertas para miembros][member offers] o [cuenta gratuita][free account].</span><span class="sxs-lookup"><span data-stu-id="65a8b-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="65a8b-112">Un equipo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65a8b-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="65a8b-113">Para obtener instrucciones, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="65a8b-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="65a8b-114">Conocimientos generales sobre los scripts de PowerShell, paquetes de NuGet y .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="65a8b-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="65a8b-115">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="65a8b-115">Get started</span></span>

<span data-ttu-id="65a8b-116">El primer paso es usar PowerShell para iniciar sesión en su cuenta de Azure y su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="65a8b-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="65a8b-117">Siga las instrucciones descritas en [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps) para iniciar sesión en su cuenta de Azure y recuperar y tener acceso a los recursos de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="65a8b-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="65a8b-118">Aprovisionar un espacio de nombres de Service Bus</span><span class="sxs-lookup"><span data-stu-id="65a8b-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="65a8b-119">Al trabajar con espacios de nombres de Service Bus, puede usar los cmdlets [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace) y [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace).</span><span class="sxs-lookup"><span data-stu-id="65a8b-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="65a8b-120">En este ejemplo se crean algunas variables locales en el script: `$Namespace` y `$Location`.</span><span class="sxs-lookup"><span data-stu-id="65a8b-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="65a8b-121">`$Namespace` es el nombre del espacio de nombres de Service Bus con el que queremos trabajar.</span><span class="sxs-lookup"><span data-stu-id="65a8b-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="65a8b-122">`$Location` identifica el centro de datos en el que aprovisionaremos el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="65a8b-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="65a8b-123">`$CurrentNamespace` almacena el espacio de nombres de referencia que vamos a recuperar (o crear).</span><span class="sxs-lookup"><span data-stu-id="65a8b-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="65a8b-124">En un script real, `$Namespace` y `$Location` se pueden pasar como parámetros.</span><span class="sxs-lookup"><span data-stu-id="65a8b-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="65a8b-125">Esta parte del script hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="65a8b-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="65a8b-126">Intenta recuperar un espacio de nombres de Service Bus con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="65a8b-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="65a8b-127">Si se encuentra el espacio de nombres, informa de lo que ha encontrado.</span><span class="sxs-lookup"><span data-stu-id="65a8b-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="65a8b-128">Si no se encuentra el espacio de nombres, lo crea y luego recupera el espacio de nombres recién creado.</span><span class="sxs-lookup"><span data-stu-id="65a8b-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="65a8b-129">Creación de una regla de autorización de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="65a8b-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="65a8b-130">En el ejemplo siguiente se muestra cómo administrar las reglas de autorización de espacios de nombres mediante los cmdlets [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get- AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule) y [Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="65a8b-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="65a8b-131">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="65a8b-131">Create a queue</span></span>

<span data-ttu-id="65a8b-132">Para crear una cola o un tema, realice una comprobación de espacio de nombres mediante el script de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="65a8b-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="65a8b-133">Después, cree la cola:</span><span class="sxs-lookup"><span data-stu-id="65a8b-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="65a8b-134">Modificación de las propiedades de una cola</span><span class="sxs-lookup"><span data-stu-id="65a8b-134">Modify queue properties</span></span>

<span data-ttu-id="65a8b-135">Después de ejecutar el script de las sección anterior, puede usar el cmdlet [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) para actualizar las propiedades de una cola, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="65a8b-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="65a8b-136">Aprovisionamiento de otras entidades de Service Bus</span><span class="sxs-lookup"><span data-stu-id="65a8b-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="65a8b-137">Puede usar el [módulo de PowerShell de Service Bus](/powershell/module/azurerm.servicebus) para aprovisionar otras entidades, como temas y suscripciones.</span><span class="sxs-lookup"><span data-stu-id="65a8b-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="65a8b-138">Estos cmdlets son sintácticamente similares a los de creación de colas que se han mostrado en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="65a8b-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65a8b-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65a8b-139">Next steps</span></span>

- <span data-ttu-id="65a8b-140">Consulte la documentación completa del módulo de PowerShell de Resource Manager de Event Hubs [aquí](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="65a8b-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="65a8b-141">Esta página enumera todos los cmdlets disponibles.</span><span class="sxs-lookup"><span data-stu-id="65a8b-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="65a8b-142">Para obtener información acerca del uso de las plantillas de Azure Resource Manager, consulte el artículo [Cómo crear recursos de Service Bus mediante plantillas de Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65a8b-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="65a8b-143">Información sobre las [bibliotecas de administración de .NET de Service Bus](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="65a8b-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="65a8b-144">Hay varias formas alternativas de administrar entidades de Service Bus, tal como se describe en estas entradas de blog:</span><span class="sxs-lookup"><span data-stu-id="65a8b-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="65a8b-145">Cómo crear colas, temas y suscripciones de Service Bus con un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="65a8b-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="65a8b-146">Cómo crear un espacio de nombres de Service Bus y un centro de eventos mediante un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="65a8b-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="65a8b-147">Scripts de PowerShell de Service Bus</span><span class="sxs-lookup"><span data-stu-id="65a8b-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
