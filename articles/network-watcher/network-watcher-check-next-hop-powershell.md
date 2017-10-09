---
title: "aaaFind próximo salto con Monitor Azure red próximo salto - PowerShell | Documentos de Microsoft"
description: "En este artículo se describe cómo puede encontrar qué Hola siguiente tipo de salto es y uso de dirección ip del próximo salto de uso de PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure con PowerShell

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API de REST de Azure](network-watcher-check-next-hop-rest.md)

Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada. Esta característica es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.

## <a name="before-you-begin"></a>Antes de empezar

En este escenario, utilizará Hola tipo toofind portal Azure Hola de próximo salto y la dirección IP.

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo usa próximo salto, una característica de Monitor de red que se determina el tipo de próximo salto hello y dirección IP para un recurso. toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Recuperación de Network Watcher

Hola primer paso es instancia de Monitor de red de tooretrieve Hola. Hola `$networkWatcher` pasa una variable toohello próximo salto comprobar cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Obtención de una máquina virtual

Próximo salto devuelve próximo salto de Hola y la dirección IP de hello del próximo salto de Hola desde una máquina virtual. Un identificador de una máquina virtual se requiere para hello cmdlet. Si ya conoce el identificador de Hola de hello toouse de máquina virtual, puede omitir este paso.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Salto siguiente requiere que el recurso de máquina virtual de Hola se asigna toorun.

## <a name="get-hello-network-interfaces"></a>Obtener interfaces de red de Hola

se necesita la dirección IP de Hola de una NIC en la máquina virtual de Hola, en este ejemplo recuperamos Hola NIC en una máquina virtual. Si ya sabe Hola IP de direcciones que desea tootest en la máquina virtual de hello, puede omitir este paso.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Obtención del próximo salto

Ahora se denomina hello `Get-AzureRmNetworkWatcherNextHop` cmdlet. Se pasa Hola cmdlet Hola Monitor de red, máquina virtual de Id., dirección IP y dirección IP de destino de código fuente. En este ejemplo, la dirección IP de destino de Hola es tooa máquina virtual en otra red virtual. Hay una puerta de enlace de red virtual entre las dos redes virtuales de Hola.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Revisión de los resultados

Cuando haya finalizado, se proporcionan los resultados de Hola. se devuelve la dirección IP del próximo salto Hello, así como de tipo hello del recurso es. En este escenario, es la dirección IP pública de Hola de puerta de enlace de red virtual de Hola.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

Hello lista siguiente muestra valores de hello disponibles actualmente NextHopType:

**Tipo de próximo salto**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooreview la configuración del grupo de seguridad de red mediante programación si visita [NSG auditoría con Monitor de red](network-watcher-nsg-auditing-powershell.md)

















