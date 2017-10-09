---
title: aaaTroubleshoot puerta de enlace de red Virtual Azure y conexiones, PowerShell | Documentos de Microsoft
description: "Esta página explica cómo solucionar problemas de cmdlet de PowerShell hello toouse Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante PowerShell de Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API DE REST](network-watcher-troubleshoot-manage-rest.md)

Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure. Una de estas funcionalidades es la solución de problemas de recursos. Solución de problemas de recursos se puede llamar a través del portal de hello, PowerShell, CLI o API de REST. Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Información general

Solución de problemas de recursos de hello permite solucionar los problemas que surgen con puertas de enlace de red Virtual y las conexiones. Cuando se realiza una solicitud de solución de problemas de tooresource, los registros se va a consultar e inspeccionar. Una vez finalizada la inspección, se devuelven resultados de Hola. Solicitudes de recursos para solucionar problemas de las solicitudes son de largos ejecución, este proceso puede tardar varios tooreturn minutos un resultado. registros de Hola de solución de problemas se almacenan en un contenedor en una cuenta de almacenamiento especificado.

## <a name="retrieve-network-watcher"></a>Recuperación de Network Watcher

Hola primer paso es instancia de Monitor de red de tooretrieve Hola. Hola `$networkWatcher` pasa una variable toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet en el paso 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Recuperación de una conexión de puerta de enlace de Virtual Network

En este ejemplo, la solución de problemas de recursos se va a ejecutar en una conexión. También puede pasarla una puerta de enlace de Virtual Network.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento

Solución de problemas de recursos devuelve datos sobre el estado de saludo del recurso de hello, también guarda la cuenta de almacenamiento de registros tooa toobe revisado. En este paso, se crea una cuenta de almacenamiento; si ya existe una cuenta de almacenamiento, puede usarla.

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a>Ejecución de la solución de problemas de recursos Network Watcher

Solucionar problemas de recursos con hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. Se pasan el objeto de Monitor de red de hello cmdlet hello, Hola Id. de conexión de Hola o puerta de enlace de red Virtual, Id. de cuenta de almacenamiento de Hola y Hola ruta de acceso toostore Hola da.

> [!NOTE]
> Hola `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet es de larga ejecución y puede tardar unos toocomplete minutos.

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

Una vez que ejecute el cmdlet de hello, Monitor de red se revisan mantenimiento de hello recursos tooverify Hola. Devuelve los resultados de hello toohello shell y almacena los registros de los resultados de hello en hello cuenta de almacenamiento especificada.

## <a name="understanding-hello-results"></a>Descripción de los resultados de Hola

texto de acción de Hello ofrece instrucciones generales sobre cómo tooresolve Hola problema. Si el problema de Hola se pueda realizar una acción, se proporciona un vínculo con instrucciones adicionales. En caso de hello donde no haya ninguna orientación adicional, respuesta de hello proporciona Hola url tooopen un caso de soporte técnico.  Para obtener más información acerca de las propiedades de Hola de respuesta de Hola y qué se incluye, visite [información general de solución de problemas del Monitor de red](network-watcher-troubleshoot-overview.md)

Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Otra herramienta que se puede utilizar es el Explorador de Storage. Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)

## <a name="next-steps"></a>Pasos siguientes

Si se cambiaron las configuraciones que detenga la conectividad de VPN, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que pueden estar en cuestión.
