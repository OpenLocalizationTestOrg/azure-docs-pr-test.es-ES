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
# <a name="use-powershell-toomanage-event-hubs-resources"></a>Usar recursos de centros de eventos de toomanage de PowerShell

Microsoft Azure PowerShell es un entorno de scripting que puede usar toocontrol y automatizar la implementación de Hola y administración de servicios de Azure. Este artículo se describe cómo hello toouse [módulo de PowerShell de administrador de recursos de centros de eventos](/powershell/module/azurerm.eventhub) tooprovision y administrar las entidades de los centros de eventos (espacios de nombres, los concentradores de eventos individuales y grupos de consumidores) usando una consola de PowerShell de Azure local o secuencia de comandos.

También puede administrar los recursos de Event Hubs mediante plantillas de Azure Resource Manager. Para obtener más información, vea el artículo de hello [crear un espacio de nombres de los centros de eventos con el grupo de concentrador y consumidor de eventos usando una plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, necesitará siguiente hello:

* Una suscripción de Azure. Para obtener más información sobre cómo obtener una suscripción, consulte [Opciones de compra][purchase options], [ofertas para miembros][member offers] o [cuenta gratuita][free account].
* Un equipo con Azure PowerShell. Para obtener instrucciones, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/get-started-azureps).
* Una descripción general de scripts de PowerShell, paquetes de NuGet y Hola .NET Framework.

## <a name="get-started"></a>Primeros pasos

Hola primer paso es toouse PowerShell toolog en tooyour cuenta de Azure y suscripción de Azure. Siga las instrucciones de hello en [empezar a trabajar con cmdlets de PowerShell de Azure](/powershell/azure/get-started-azureps) toolog en tooyour cuenta de Azure, a continuación, recuperar y tener acceso a recursos de hello en su suscripción de Azure.

## <a name="provision-an-event-hubs-namespace"></a>Aprovisionamiento de un espacio de nombres de Event Hubs

Al trabajar con espacios de nombres de los centros de eventos, puede usar hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , y [AzureRmEventHubNamespace conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.

Este ejemplo crea algunas variables locales en el script de Hola; `$Namespace` y `$Location`.

* `$Namespace`es el nombre de Hola de Hola de espacio de nombres de los centros de eventos con el que se desea toowork.
* `$Location`identifica el centro de datos de hello en el que se ofrece el espacio de nombres de Hola.
* `$CurrentNamespace`almacena el espacio de nombres de referencia de Hola que se recuperan (o crear).

En un script real, `$Namespace` y `$Location` se pueden pasar como parámetros.

Esta parte del script de Hola Hola siguientes:

1. El nombre especificado de intentos tooretrieve un espacio de nombres de los centros de eventos con hello.
2. Si se encuentra el espacio de nombres de hello, informa de lo que se encontró.
3. Si no se encuentra el espacio de nombres de hello, se crea el espacio de nombres de hello y, a continuación, recupera Hola que acaba de crear espacio de nombres.

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

## <a name="create-an-event-hub"></a>Creación de un centro de eventos

toocreate un concentrador de eventos, realice una comprobación de espacio de nombres mediante el script de Hola en la sección anterior de Hola. A continuación, usar hello [AzureRmEventHub New](/powershell/module/azurerm.eventhub/new-azurermeventhub) concentrador de eventos de cmdlet toocreate hello:

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

### <a name="create-a-consumer-group"></a>Creación de un grupo de consumidores

toocreate un grupo de consumidores dentro de un concentrador de eventos, realizar Hola espacio de nombres y eventos concentrador comprobaciones mediante secuencias de comandos de hello en la sección anterior de Hola. A continuación, usar hello [AzureRmEventHubConsumerGroup New](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) grupo de consumidores de cmdlet toocreate hello en el concentrador de eventos de Hola. Por ejemplo:

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

#### <a name="set-user-metadata"></a>Establecimiento de los metadatos del usuario

Después de ejecutar las secuencias de comandos de Hola Hola secciones anteriores, puede usar hello [AzureRmEventHubConsumerGroup conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) propiedades de hello tooupdate de cmdlet de un grupo de consumidores, como en el siguiente ejemplo de Hola:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Eliminación de un centro de eventos

centros de eventos de tooremove Hola que creó, puede usar hello `Remove-*` cmdlets, como en el siguiente ejemplo de Hola:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Pasos siguientes

- Vea Hola eventos concentradores Administrador de recursos PowerShell módulo la documentación completa [aquí](/powershell/module/azurerm.eventhub). Esta página enumera todos los cmdlets disponibles.
- Para obtener información sobre el uso de plantillas del Administrador de recursos de Azure, vea el artículo de hello [crear un espacio de nombres de los centros de eventos con el grupo de concentrador y consumidor de eventos usando una plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).
- Información sobre las [bibliotecas de administración de .NET de Event Hubs](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
