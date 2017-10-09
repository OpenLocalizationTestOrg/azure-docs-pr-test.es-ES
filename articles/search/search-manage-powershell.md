---
title: "aaaManage búsqueda de Azure con scripts de Powershell | Documentos de Microsoft"
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
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a>Administración del servicio Búsqueda de Azure con PowerShell
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

Este tema describe tooperform de comandos de PowerShell de hello muchas de las tareas de administración de Hola para los servicios de búsqueda de Azure. Se le guiará por la creación de un servicio de búsqueda, su escalado y la administración de sus claves de API.
Estos comandos en paralelo opciones de administración de hello disponibles en hello [API de REST de administración de búsqueda de Azure](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Requisitos previos
* Debe tener Azure PowerShell 1.0 o versiones posteriores. Para obtener más información, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).
* Debe haber iniciado sesión tooyour suscripción de Azure en PowerShell, tal y como se describe a continuación.

En primer lugar, debe tooAzure de inicio de sesión con este comando:

    Login-AzureRmAccount

Especifique la dirección de correo electrónico de Hola de su cuenta de Azure y su contraseña en el cuadro de diálogo de inicio de sesión de Microsoft Azure de Hola.

También puede [iniciar sesión de forma no interactiva con una entidad de servicio](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Si tiene varias suscripciones de Azure, deberá tooset su suscripción de Azure. toosee una lista de las suscripciones actuales, ejecute este comando.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

suscripción de hello toospecify, ejecute el siguiente comando de Hola. En el siguiente ejemplo de Hola, es el nombre de la suscripción de hello `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Toohelp comandos empezar
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
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

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
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
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a>Pasos siguientes
Ahora que se crea el servicio, puede realizar pasos de hello: compilar un [índice](search-what-is-an-index.md), [consultar un índice](search-query-overview.md)y por último, crear y administrar su propia aplicación de búsqueda que usa búsqueda de Azure.

* [Crear un índice de búsqueda de Azure en hello portal de Azure](search-create-index-portal.md)
* [Consultar un índice de búsqueda de Azure mediante el Explorador de búsqueda en hello portal de Azure](search-explorer.md)
* [Programa de instalación de un indizador tooload de datos de otros servicios](search-indexer-overview.md)
* [Cómo toouse búsqueda de Azure en .NET](search-howto-dotnet-sdk.md)
* [Analizar el tráfico de Búsqueda de Azure](search-traffic-analytics.md)

