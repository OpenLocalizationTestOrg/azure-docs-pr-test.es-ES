---
title: recursos de Service Bus de Azure de aaaUse PowerShell toomanage | Documentos de Microsoft
description: "Usar toocreate de módulo de PowerShell y administrar recursos de Bus de servicio"
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
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="de258-103">Usar recursos de Bus de servicio de toomanage de PowerShell</span><span class="sxs-lookup"><span data-stu-id="de258-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="de258-104">Microsoft Azure PowerShell es un entorno de scripting que puede usar toocontrol y automatizar la implementación de Hola y administración de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="de258-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="de258-105">Este artículo se describe cómo hello toouse [módulo de PowerShell del Administrador de recursos del Bus de servicio](/powershell/module/azurerm.servicebus) tooprovision y administrar las entidades de Bus de servicio (espacios de nombres, colas, temas y suscripciones) mediante una consola de PowerShell de Azure local o secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="de258-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="de258-106">Las entidades de Service Bus también se pueden administrar mediante plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="de258-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="de258-107">Para obtener más información, vea el artículo de hello [recursos de Bus de servicio crear usando plantillas del Administrador de recursos de Azure](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de258-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de258-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="de258-108">Prerequisites</span></span>

<span data-ttu-id="de258-109">Antes de empezar, necesitará siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="de258-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="de258-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="de258-110">An Azure subscription.</span></span> <span data-ttu-id="de258-111">Para obtener más información sobre cómo obtener una suscripción, consulte [Opciones de compra][purchase options], [ofertas para miembros][member offers] o [cuenta gratuita][free account].</span><span class="sxs-lookup"><span data-stu-id="de258-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="de258-112">Un equipo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de258-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="de258-113">Para obtener instrucciones, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="de258-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="de258-114">Una descripción general de scripts de PowerShell, paquetes de NuGet y Hola .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="de258-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="de258-115">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="de258-115">Get started</span></span>

<span data-ttu-id="de258-116">Hola primer paso es toouse PowerShell toolog en tooyour cuenta de Azure y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="de258-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="de258-117">Siga las instrucciones de hello en [empezar a trabajar con cmdlets de PowerShell de Azure](/powershell/azure/get-started-azureps) toolog en tooyour cuenta de Azure y recuperar y acceder a recursos de hello en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="de258-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="de258-118">Aprovisionar un espacio de nombres de Service Bus</span><span class="sxs-lookup"><span data-stu-id="de258-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="de258-119">Al trabajar con espacios de nombres de Bus de servicio, puede usar hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), y [AzureRmServiceBusNamespace conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="de258-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="de258-120">Este ejemplo crea algunas variables locales en el script de Hola; `$Namespace` y `$Location`.</span><span class="sxs-lookup"><span data-stu-id="de258-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="de258-121">`$Namespace`es el nombre de Hola de Hola de espacio de nombres de Bus de servicio con el que se desea toowork.</span><span class="sxs-lookup"><span data-stu-id="de258-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="de258-122">`$Location`identifica el centro de datos de hello en el que se ofrece el espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="de258-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="de258-123">`$CurrentNamespace`almacena el espacio de nombres de referencia de Hola que se recuperan (o crear).</span><span class="sxs-lookup"><span data-stu-id="de258-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="de258-124">En un script real, `$Namespace` y `$Location` se pueden pasar como parámetros.</span><span class="sxs-lookup"><span data-stu-id="de258-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="de258-125">Esta parte del script de Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="de258-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="de258-126">El nombre especificado de intentos tooretrieve un espacio de nombres de Bus de servicio con hello.</span><span class="sxs-lookup"><span data-stu-id="de258-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="de258-127">Si se encuentra el espacio de nombres de hello, informa de lo que se encontró.</span><span class="sxs-lookup"><span data-stu-id="de258-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="de258-128">Si no se encuentra el espacio de nombres de hello, se crea el espacio de nombres de hello y, a continuación, recupera Hola que acaba de crear espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="de258-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="de258-129">Creación de una regla de autorización de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="de258-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="de258-130">Hello en el ejemplo siguiente se muestra cómo usar las reglas de autorización de espacio de nombres de toomanage Hola [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Conjunto AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), y [cmdlets Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="de258-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
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

## <a name="create-a-queue"></a><span data-ttu-id="de258-131">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="de258-131">Create a queue</span></span>

<span data-ttu-id="de258-132">toocreate una cola o tema, realice una comprobación de espacio de nombres mediante el script de Hola en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="de258-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="de258-133">A continuación, cree la cola de hello:</span><span class="sxs-lookup"><span data-stu-id="de258-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="de258-134">Modificación de las propiedades de una cola</span><span class="sxs-lookup"><span data-stu-id="de258-134">Modify queue properties</span></span>

<span data-ttu-id="de258-135">Después de ejecutar script de Hola Hola sección anterior, puede usar hello [AzureRmServiceBusQueue conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) propiedades de hello tooupdate de cmdlet de una cola, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="de258-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="de258-136">Aprovisionamiento de otras entidades de Service Bus</span><span class="sxs-lookup"><span data-stu-id="de258-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="de258-137">Puede usar hello [módulo de PowerShell de Service Bus](/powershell/module/azurerm.servicebus) tooprovision otras entidades, como temas y suscripciones.</span><span class="sxs-lookup"><span data-stu-id="de258-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="de258-138">Estos cmdlets son sintácticamente similar cmdlets de creación de cola toohello mostrados en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="de258-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de258-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de258-139">Next steps</span></span>

- <span data-ttu-id="de258-140">Consulte documentación del módulo de PowerShell Administrador de recursos del Bus de servicio completa de hello [aquí](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="de258-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="de258-141">Esta página enumera todos los cmdlets disponibles.</span><span class="sxs-lookup"><span data-stu-id="de258-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="de258-142">Para obtener información sobre el uso de plantillas del Administrador de recursos de Azure, vea el artículo de hello [recursos de Bus de servicio crear usando plantillas del Administrador de recursos de Azure](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de258-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="de258-143">Información sobre las [bibliotecas de administración de .NET de Service Bus](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="de258-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="de258-144">Hay algunas formas alternativas toomanage entidades de Bus de servicio, como se describe en estas entradas de blog:</span><span class="sxs-lookup"><span data-stu-id="de258-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="de258-145">¿Cómo toocreate Service Bus colas, temas y suscripciones mediante un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="de258-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="de258-146">¿Cómo toocreate un Namespace de Bus de servicio y un centro de eventos mediante un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="de258-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="de258-147">Scripts de PowerShell de Service Bus</span><span class="sxs-lookup"><span data-stu-id="de258-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
