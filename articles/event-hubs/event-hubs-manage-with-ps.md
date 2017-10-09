---
title: recursos de centros de eventos de Azure de aaaUse PowerShell toomanage | Documentos de Microsoft
description: "Usar toocreate de módulo de PowerShell y administrar los centros de eventos"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="449e6-103">Usar recursos de centros de eventos de toomanage de PowerShell</span><span class="sxs-lookup"><span data-stu-id="449e6-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="449e6-104">Microsoft Azure PowerShell es un entorno de scripting que puede usar toocontrol y automatizar la implementación de Hola y administración de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="449e6-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="449e6-105">Este artículo se describe cómo hello toouse [módulo de PowerShell de administrador de recursos de centros de eventos](/powershell/module/azurerm.eventhub) tooprovision y administrar las entidades de los centros de eventos (espacios de nombres, los concentradores de eventos individuales y grupos de consumidores) usando una consola de PowerShell de Azure local o secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="449e6-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="449e6-106">También puede administrar los recursos de Event Hubs mediante plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="449e6-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="449e6-107">Para obtener más información, vea el artículo de hello [crear un espacio de nombres de los centros de eventos con el grupo de concentrador y consumidor de eventos usando una plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="449e6-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="449e6-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="449e6-108">Prerequisites</span></span>

<span data-ttu-id="449e6-109">Antes de empezar, necesitará siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="449e6-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="449e6-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="449e6-110">An Azure subscription.</span></span> <span data-ttu-id="449e6-111">Para obtener más información sobre cómo obtener una suscripción, consulte [Opciones de compra][purchase options], [ofertas para miembros][member offers] o [cuenta gratuita][free account].</span><span class="sxs-lookup"><span data-stu-id="449e6-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="449e6-112">Un equipo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="449e6-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="449e6-113">Para obtener instrucciones, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="449e6-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="449e6-114">Una descripción general de scripts de PowerShell, paquetes de NuGet y Hola .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="449e6-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="449e6-115">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="449e6-115">Get started</span></span>

<span data-ttu-id="449e6-116">Hola primer paso es toouse PowerShell toolog en tooyour cuenta de Azure y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="449e6-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="449e6-117">Siga las instrucciones de hello en [empezar a trabajar con cmdlets de PowerShell de Azure](/powershell/azure/get-started-azureps) toolog en tooyour cuenta de Azure, a continuación, recuperar y tener acceso a recursos de hello en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="449e6-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="449e6-118">Aprovisionamiento de un espacio de nombres de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="449e6-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="449e6-119">Al trabajar con espacios de nombres de los centros de eventos, puede usar hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , y [AzureRmEventHubNamespace conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="449e6-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="449e6-120">Este ejemplo crea algunas variables locales en el script de Hola; `$Namespace` y `$Location`.</span><span class="sxs-lookup"><span data-stu-id="449e6-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="449e6-121">`$Namespace`es el nombre de Hola de Hola de espacio de nombres de los centros de eventos con el que se desea toowork.</span><span class="sxs-lookup"><span data-stu-id="449e6-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="449e6-122">`$Location`identifica el centro de datos de hello en el que se ofrece el espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="449e6-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="449e6-123">`$CurrentNamespace`almacena el espacio de nombres de referencia de Hola que se recuperan (o crear).</span><span class="sxs-lookup"><span data-stu-id="449e6-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="449e6-124">En un script real, `$Namespace` y `$Location` se pueden pasar como parámetros.</span><span class="sxs-lookup"><span data-stu-id="449e6-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="449e6-125">Esta parte del script de Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="449e6-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="449e6-126">El nombre especificado de intentos tooretrieve un espacio de nombres de los centros de eventos con hello.</span><span class="sxs-lookup"><span data-stu-id="449e6-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="449e6-127">Si se encuentra el espacio de nombres de hello, informa de lo que se encontró.</span><span class="sxs-lookup"><span data-stu-id="449e6-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="449e6-128">Si no se encuentra el espacio de nombres de hello, se crea el espacio de nombres de hello y, a continuación, recupera Hola que acaba de crear espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="449e6-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="449e6-129">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="449e6-129">Create an event hub</span></span>

<span data-ttu-id="449e6-130">toocreate un concentrador de eventos, realice una comprobación de espacio de nombres mediante el script de Hola en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="449e6-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="449e6-131">A continuación, usar hello [AzureRmEventHub New](/powershell/module/azurerm.eventhub/new-azurermeventhub) concentrador de eventos de cmdlet toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="449e6-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="449e6-132">Creación de un grupo de consumidores</span><span class="sxs-lookup"><span data-stu-id="449e6-132">Create a consumer group</span></span>

<span data-ttu-id="449e6-133">toocreate un grupo de consumidores dentro de un concentrador de eventos, realizar Hola espacio de nombres y eventos concentrador comprobaciones mediante secuencias de comandos de hello en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="449e6-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="449e6-134">A continuación, usar hello [AzureRmEventHubConsumerGroup New](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) grupo de consumidores de cmdlet toocreate hello en el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="449e6-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="449e6-135">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="449e6-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="449e6-136">Establecimiento de los metadatos del usuario</span><span class="sxs-lookup"><span data-stu-id="449e6-136">Set user metadata</span></span>

<span data-ttu-id="449e6-137">Después de ejecutar las secuencias de comandos de Hola Hola secciones anteriores, puede usar hello [AzureRmEventHubConsumerGroup conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) propiedades de hello tooupdate de cmdlet de un grupo de consumidores, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="449e6-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="449e6-138">Eliminación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="449e6-138">Remove event hub</span></span>

<span data-ttu-id="449e6-139">centros de eventos de tooremove Hola que creó, puede usar hello `Remove-*` cmdlets, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="449e6-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="449e6-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="449e6-140">Next steps</span></span>

- <span data-ttu-id="449e6-141">Vea Hola eventos concentradores Administrador de recursos PowerShell módulo la documentación completa [aquí](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="449e6-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="449e6-142">Esta página enumera todos los cmdlets disponibles.</span><span class="sxs-lookup"><span data-stu-id="449e6-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="449e6-143">Para obtener información sobre el uso de plantillas del Administrador de recursos de Azure, vea el artículo de hello [crear un espacio de nombres de los centros de eventos con el grupo de concentrador y consumidor de eventos usando una plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="449e6-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="449e6-144">Información sobre las [bibliotecas de administración de .NET de Event Hubs](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="449e6-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
