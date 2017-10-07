---
title: 'captura de paquetes de aaaManage con Monitor de red de Azure: PowerShell | Documentos de Microsoft'
description: "Esta página explica cómo la captura de paquete de saludo toomanage característica de Monitor de red con PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>Administración de capturas de paquetes con Azure Network Watcher mediante PowerShell

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API de REST de Azure](network-watcher-packet-capture-manage-rest.md)

Captura de paquetes de Monitor de red le permite toocreate captura sesiones tootrack tráfico tooand desde una máquina virtual. Los filtros se proporcionan para tooensure de sesión de captura de hello que capturar solamente el tráfico de Hola que desee. Captura de paquetes le ayuda a anomalías de la red toodiagnose tanto de forma reactiva y proactiva. Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más. Al ser capaz de tooremotely capturas de paquetes de desencadenador, esta capacidad reduce la carga de Hola de una captura de paquetes en ejecución en el equipo deseado de hello, que permite ahorrar tiempo y manualmente.

En este artículo le guiará Hola diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.

- [**Inicio de una captura de paquetes**](#start-a-packet-capture)
- [**Detención de una captura de paquetes**](#stop-a-packet-capture)
- [**Eliminación de una captura de paquetes**](#delete-a-packet-capture)
- [**Descarga de una captura de paquetes**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Antes de empezar

En este artículo se supone que tiene Hola recursos siguientes:

* Una instancia del Monitor de red en la región de Hola que desea toocreate una captura de paquetes

* Una máquina virtual con el paquete de saludo capturar extensión habilitada.

> [!IMPORTANT]
> La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`. Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>Instalación de la extensión de máquina virtual

### <a name="step-1"></a>Paso 1

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>Paso 2

el ejemplo siguiente se recupera información de la extensión de Hola Hola necesarios toorun hello `Set-AzureRmVMExtension` cmdlet. Este cmdlet instala el agente de captura de paquetes de saludo en la máquina virtual de hello invitado.

> [!NOTE]
> Hola `Set-AzureRmVMExtension` cmdlet puede tardar varios toocomplete minutos.

En las máquinas virtuales Windows:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

En las máquinas virtuales Linux:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

Hello ejemplo siguiente es una respuesta correcta después de ejecutar hello `Set-AzureRmVMExtension` cmdlet.

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>Paso 3

tooensure que Hola agente está instalado, ejecute hello `Get-AzureRmVMExtension` cmdlet y pasarlo a nombre de la máquina virtual de Hola y el nombre de la extensión de Hola.

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

Hola según muestra es un ejemplo de respuesta de Hola de ejecución`Get-AzureRmVMExtension`

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a>Inicio de una captura de paquetes

Una vez hello pasos anteriores se completa, agente de captura de paquetes de saludo se instala en la máquina virtual de Hola.

### <a name="step-1"></a>Paso 1

Hola siguiente paso es instancia de Monitor de red de tooretrieve Hola. Esta variable se pasa toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet en el paso 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>Paso 2

Recupere una cuenta de almacenamiento. Esta cuenta de almacenamiento es el archivo de captura de paquetes de hello toostore usado.

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>Paso 3

Los filtros pueden ser datos de Hola de toolimit usado almacenado por captura de paquetes de saludo. Hello en el ejemplo siguiente se configura dos filtros.  Recopila un filtro saliente TCP tráfico solo desde IP local 10.0.0.3 toodestination puertos 20, 80 y 443.  segundo filtro de Hello recopila sólo el tráfico UDP.

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> Se pueden definir varios filtros para una captura de paquetes.

### <a name="step-4"></a>Paso 4

Ejecute hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart Hola paquete proceso de captura, pasar valores de hello necesario recuperados Hola pasos anteriores.
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

el ejemplo siguiente se Hello es resultado de hello esperada de la ejecución hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a>Obtención de una captura de paquetes

Ejecuta hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, recupera el estado de saludo de una captura de paquetes que se está ejecutando o se han completado.

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

el ejemplo siguiente se Hello es resultado de hello de hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet. Hello siguiente ejemplo es una vez completada la captura de Hola. Hola PacketCaptureStatus valor se detiene, con un StopReason de TimeExceeded. Este valor muestra que captura de paquetes de saludo fue correcta y ejecutó su tiempo.
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a>Detención de una captura de paquetes

Mediante la ejecución de hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, si una sesión de captura está en curso se detiene.

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Hola cmdlet no devuelve ninguna respuesta cuando se ejecutó en una sesión de captura actualmente en ejecución o una sesión existente que ya se ha detenido.

## <a name="delete-a-packet-capture"></a>Eliminación de una captura de paquetes

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Eliminar una captura de paquetes no elimina archivos hello en la cuenta de almacenamiento de Hola.

## <a name="download-a-packet-capture"></a>Descarga de una captura de paquetes

Una vez que haya finalizado la sesión de captura de paquetes, archivo de captura de hello puede ser cargado tooblob almacenamiento o tooa archivo local Hola máquina virtual. ubicación de almacenamiento de Hola de captura de paquetes de saludo se define en la creación de sesión de Hola. Una herramienta adecuada tooaccess estos capturar los archivos de cuenta de almacenamiento de tooa guardado es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/

Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)

Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar IP Flow Verify](network-watcher-check-ip-flow-verify-portal.md).

<!-- Image references -->














