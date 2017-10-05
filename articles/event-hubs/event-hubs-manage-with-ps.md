---
title: Uso de PowerShell para administrar recursos de Azure Event Hubs | Microsoft Docs
description: "Usar el módulo de PowerShell para crear y administrar Event Hubs"
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
ms.openlocfilehash: 2b49c01153b1104612e6ebf9c88566fc40d1f635
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-manage-event-hubs-resources"></a><span data-ttu-id="27bbf-103">Uso de PowerShell para administrar recursos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="27bbf-103">Use PowerShell to manage Event Hubs resources</span></span>

<span data-ttu-id="27bbf-104">Microsoft Azure PowerShell es un entorno de scripting que puede usar para controlar y automatizar la implementación y la administración de sus servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="27bbf-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="27bbf-105">Este artículo describe cómo utilizar el [módulo de PowerShell de Resource Manager de Event Hubs](/powershell/module/azurerm.eventhub) para aprovisionar y administrar entidades de Event Hubs (espacios de nombres, Event Hubs individuales y grupos de consumidores) mediante una consola o script de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27bbf-105">This article describes how to use the [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) to provision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="27bbf-106">También puede administrar los recursos de Event Hubs mediante plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="27bbf-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="27bbf-107">Para más información, consulte el artículo [Creación de un espacio de nombres de Event Hubs con un centro de eventos y un grupo de consumidores mediante una plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="27bbf-107">For more information, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27bbf-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="27bbf-108">Prerequisites</span></span>

<span data-ttu-id="27bbf-109">Antes de comenzar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="27bbf-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="27bbf-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="27bbf-110">An Azure subscription.</span></span> <span data-ttu-id="27bbf-111">Para obtener más información sobre cómo obtener una suscripción, consulte [Opciones de compra][purchase options], [ofertas para miembros][member offers] o [cuenta gratuita][free account].</span><span class="sxs-lookup"><span data-stu-id="27bbf-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="27bbf-112">Un equipo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27bbf-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="27bbf-113">Para obtener instrucciones, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="27bbf-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="27bbf-114">Conocimientos generales sobre los scripts de PowerShell, paquetes de NuGet y .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="27bbf-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="27bbf-115">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="27bbf-115">Get started</span></span>

<span data-ttu-id="27bbf-116">El primer paso es usar PowerShell para iniciar sesión en su cuenta de Azure y su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="27bbf-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="27bbf-117">Siga las instrucciones descritas en [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps) para iniciar sesión en su cuenta de Azure y recuperar y tener acceso a los recursos de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="27bbf-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, then retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="27bbf-118">Aprovisionamiento de un espacio de nombres de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="27bbf-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="27bbf-119">Al trabajar con espacios de nombres de Event Hubs, puede usar los cmdlets [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) y [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace).</span><span class="sxs-lookup"><span data-stu-id="27bbf-119">When working with Event Hubs namespaces, you can use the [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="27bbf-120">En este ejemplo se crean algunas variables locales en el script: `$Namespace` y `$Location`.</span><span class="sxs-lookup"><span data-stu-id="27bbf-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="27bbf-121">`$Namespace` es el nombre del espacio de nombres de Event Hubs con el que queremos trabajar.</span><span class="sxs-lookup"><span data-stu-id="27bbf-121">`$Namespace` is the name of the Event Hubs namespace with which we want to work.</span></span>
* <span data-ttu-id="27bbf-122">`$Location` identifica el centro de datos en el que aprovisionaremos el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="27bbf-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="27bbf-123">`$CurrentNamespace` almacena el espacio de nombres de referencia que vamos a recuperar (o crear).</span><span class="sxs-lookup"><span data-stu-id="27bbf-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="27bbf-124">En un script real, `$Namespace` y `$Location` se pueden pasar como parámetros.</span><span class="sxs-lookup"><span data-stu-id="27bbf-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="27bbf-125">Esta parte del script hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="27bbf-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="27bbf-126">Intenta recuperar un espacio de nombres de Event Hubs con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="27bbf-126">Attempts to retrieve an Event Hubs namespace with the specified name.</span></span>
2. <span data-ttu-id="27bbf-127">Si se encuentra el espacio de nombres, informa de lo que ha encontrado.</span><span class="sxs-lookup"><span data-stu-id="27bbf-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="27bbf-128">Si no se encuentra el espacio de nombres, lo crea y luego recupera el espacio de nombres recién creado.</span><span class="sxs-lookup"><span data-stu-id="27bbf-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>

    ```powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="27bbf-129">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="27bbf-129">Create an event hub</span></span>

<span data-ttu-id="27bbf-130">Para crear un centro de eventos, realice una comprobación de espacio de nombres mediante el script de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="27bbf-130">To create an event hub, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="27bbf-131">A continuación, use el cmdlet [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) para crear el centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="27bbf-131">Then, use the [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet to create the event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "The event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $EventHubName event hub does not exist."
    Write-Host "Creating the $EventHubName event hub in the $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $EventHubName event hub in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="27bbf-132">Creación de un grupo de consumidores</span><span class="sxs-lookup"><span data-stu-id="27bbf-132">Create a consumer group</span></span>

<span data-ttu-id="27bbf-133">Para crear un grupo de consumidores dentro de un centro de eventos, realice las comprobaciones de espacio de nombres y centro de eventos mediante los scripts de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="27bbf-133">To create a consumer group within an event hub, perform the namespace and event hub checks using the scripts in the previous section.</span></span> <span data-ttu-id="27bbf-134">A continuación, use el cmdlet [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) para crear el grupo de consumidores en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="27bbf-134">Then, use the [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet to create the consumer group within the event hub.</span></span> <span data-ttu-id="27bbf-135">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="27bbf-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "The consumer group $ConsumerGroupName in event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating the $ConsumerGroupName consumer group in the $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="27bbf-136">Establecimiento de los metadatos del usuario</span><span class="sxs-lookup"><span data-stu-id="27bbf-136">Set user metadata</span></span>

<span data-ttu-id="27bbf-137">Después de ejecutar los scripts de las secciones anteriores, puede usar el cmdlet [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) para actualizar las propiedades de un grupo de consumidores, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="27bbf-137">After executing the scripts in the preceding sections, you can use the [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet to update the properties of a consumer group, as in the following example:</span></span>

```powershell
# Set some user metadata on the CG
Write-Host "Setting the UserMetadata field to 'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="27bbf-138">Eliminación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="27bbf-138">Remove event hub</span></span>

<span data-ttu-id="27bbf-139">Para quitar las instancias de Event Hubs que creó, puede usar el cmdlet `Remove-*` como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="27bbf-139">To remove the event hubs you created, you can use the `Remove-*` cmdlets, as in the following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="27bbf-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="27bbf-140">Next steps</span></span>

- <span data-ttu-id="27bbf-141">Consulte la documentación completa del módulo de PowerShell de Resource Manager de Event Hubs [aquí](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="27bbf-141">See the complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="27bbf-142">Esta página enumera todos los cmdlets disponibles.</span><span class="sxs-lookup"><span data-stu-id="27bbf-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="27bbf-143">Para más información sobre el uso de plantillas de Azure Resource Manager, consulte el artículo [Creación de un espacio de nombres de Event Hubs con un centro de eventos y un grupo de consumidores mediante una plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="27bbf-143">For information about using Azure Resource Manager templates, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="27bbf-144">Información sobre las [bibliotecas de administración de .NET de Event Hubs](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="27bbf-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
