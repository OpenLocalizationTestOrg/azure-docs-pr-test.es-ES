---
title: "Administración de Azure Search con scripts de PowerShell | Microsoft Docs"
description: "Administre el servicio Búsqueda de Azure con scripts de PowerShell. Creación o actualización del servicio Búsqueda de Azure y administración de las claves de administración de Búsqueda de Azure"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: aa51c846efef12461ec382274199bc049c42aaa3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="2dc8e-104">Administración del servicio Búsqueda de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dc8e-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2dc8e-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2dc8e-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="2dc8e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dc8e-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="2dc8e-107">En este tema se describen los comandos de PowerShell para realizar muchas de las tareas de administración del servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-107">This topic describes the PowerShell commands to perform many of the management tasks for Azure Search services.</span></span> <span data-ttu-id="2dc8e-108">Se le guiará por la creación de un servicio de búsqueda, su escalado y la administración de sus claves de API.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="2dc8e-109">Estos comandos equivalen a las opciones de administración disponibles en la [API de REST de administración de Búsqueda de Azure](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="2dc8e-109">These commands parallel the management options available in the [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dc8e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2dc8e-110">Prerequisites</span></span>
* <span data-ttu-id="2dc8e-111">Debe tener Azure PowerShell 1.0 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="2dc8e-112">Para obtener más información, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2dc8e-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="2dc8e-113">Debe iniciar sesión en su suscripción de Azure en PowerShell, tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-113">You must be logged in to your Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="2dc8e-114">En primer lugar, debe iniciar sesión en Azure con este comando.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-114">First, you must login to Azure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="2dc8e-115">Especifique la dirección de correo electrónico de la cuenta de Azure y su contraseña en el cuadro de diálogo de inicio de sesión de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-115">Specify the email address of your Azure account and its password in the Microsoft Azure login dialog.</span></span>

<span data-ttu-id="2dc8e-116">También puede [iniciar sesión de forma no interactiva con una entidad de servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="2dc8e-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="2dc8e-117">Si tiene varias suscripciones de Azure, deberá establecer la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-117">If you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="2dc8e-118">Para ver una lista de las suscripciones actuales, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-118">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="2dc8e-119">Para especificar la suscripción, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-119">To specify the subscription, run the following command.</span></span> <span data-ttu-id="2dc8e-120">En el ejemplo siguiente, el nombre de la suscripción es `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-120">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-to-help-you-get-started"></a><span data-ttu-id="2dc8e-121">Comandos para ayudarle a empezar a trabajar</span><span class="sxs-lookup"><span data-stu-id="2dc8e-121">Commands to help you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register the ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once the service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get the primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate the secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access to your indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until the operation is finished
    # It can take 15 minutes or more to provision the additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in the service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="2dc8e-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2dc8e-122">Next Steps</span></span>
<span data-ttu-id="2dc8e-123">Ahora que el servicio está creado, puede realizar los pasos siguientes: crear un [índice](search-what-is-an-index.md), [consultar un índice](search-query-overview.md) y, por último, crear y administrar su propia aplicación de búsqueda que usa Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2dc8e-123">Now that your service is created, you can take the next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="2dc8e-124">Creación de un índice de Búsqueda de Azure en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2dc8e-124">Create an Azure Search index in the Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="2dc8e-125">Consulta de un índice de Búsqueda de Azure mediante el Explorador de búsqueda en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2dc8e-125">Query an Azure Search index using Search Explorer in the Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="2dc8e-126">Configurar un indexador para cargar datos desde otros servicios</span><span class="sxs-lookup"><span data-stu-id="2dc8e-126">Setup an indexer to load data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="2dc8e-127">Cómo usar la Búsqueda de Azure en .NET</span><span class="sxs-lookup"><span data-stu-id="2dc8e-127">How to use Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="2dc8e-128">Analizar el tráfico de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="2dc8e-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

