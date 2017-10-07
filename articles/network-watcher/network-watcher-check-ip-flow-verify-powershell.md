---
title: "tráfico de aaaverify con flujo de IP de Monitor de red de Azure Compruebe - PowerShell | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si tooor de tráfico de una máquina virtual se permite o deniega con PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Compruebe si el tráfico se permitirá o denegará tooor de una máquina virtual con el flujo de IP compruebe un componente de Monitor de red de Azure

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API de REST de Azure](network-watcher-check-ip-flow-verify-rest.md)


Flujo IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual. Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o back-end. Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG. Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red o tiene una instancia existente de Monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

Este flujo de escenario usa IP comprobar tooverify si una máquina virtual puede comunicarse conocidos tooa dirección IP de Bing. Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico. más información sobre el flujo IP comprobar, visite toolearn [flujo IP comprobar información general](network-watcher-ip-flow-verify-overview.md)

## <a name="retrieve-network-watcher"></a>Recuperación de Network Watcher

Hola primer paso es instancia de Monitor de red de tooretrieve Hola. Hola `$networkWatcher` pasa una variable toohello IP flujo comprobar cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Obtención de una máquina virtual

Flujo IP Compruebe tooor de tráfico de pruebas desde una dirección IP en un tooor de máquina virtual de un destino remoto. Un identificador de una máquina virtual se requiere para hello cmdlet. Si ya conoce el identificador de Hola de hello toouse de máquina virtual, puede omitir este paso.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a>Obtener Hola NIC

se necesita la dirección IP de Hola de una NIC en la máquina virtual de Hola, en este ejemplo recuperamos Hola NIC en una máquina virtual. Si ya sabe Hola IP de direcciones que desea tootest en la máquina virtual de hello, puede omitir este paso.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a>Ejecución de la Comprobación del flujo de IP

Ahora que tenemos información Hola necesarios toorun Hola cmdlet, ejecutamos hello `Test-AzureRmNetworkWatcherIPFlow` tráfico de cmdlet tootest Hola. En este ejemplo, estamos utilizando dirección IP de la primera hello en la NIC de hello primero.

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> Flujo IP comprobar requiere que el recurso de máquina virtual de Hola se asigna toorun.

## <a name="review-results"></a>Revisión de los resultados

Después de ejecutar `Test-AzureRmNetworkWatcherIPFlow` Hola resultados se devuelven, en el ejemplo siguiente se hello es Hola devuelva resultados de hello anterior paso.

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a>Pasos siguientes

Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













