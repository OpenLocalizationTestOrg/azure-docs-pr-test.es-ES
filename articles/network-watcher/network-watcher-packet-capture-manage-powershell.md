---
title: "Administración de capturas de paquetes con Azure Network Watcher (PowerShell) | Microsoft Docs"
description: "En esta página se explica cómo administrar la característica de captura de paquetes de Network Watcher mediante PowerShell."
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: b27e0684b0914764f22b59e050e75c7be3a82cc6
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>Administración de capturas de paquetes con Azure Network Watcher mediante PowerShell

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API de REST de Azure](network-watcher-packet-capture-manage-rest.md)

La captura de paquetes de Network Watcher permite crear sesiones de captura para realizar el seguimiento del tráfico hacia y desde una máquina virtual. La sesión de captura cuenta con filtros para asegurarse de capturar solo el tráfico que se desea. La captura de paquetes ayuda a diagnosticar anomalías de la red, tanto de forma activa como reactiva. Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros. Esta funcionalidad permite desencadenar capturas de paquetes de forma remota, lo que reduce la carga de tener que ejecutar una captura de paquetes manualmente y en el equipo deseado, y permite ahorrar tiempo.

Este artículo le guiará por las diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.

- [**Inicio de una captura de paquetes**](#start-a-packet-capture)
- [**Detención de una captura de paquetes**](#stop-a-packet-capture)
- [**Eliminación de una captura de paquetes**](#delete-a-packet-capture)
- [**Descarga de una captura de paquetes**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Antes de empezar

En este artículo se da por hecho que tiene los siguientes recursos:

* Una instancia de Network Watcher en la región donde desea crear una captura de paquetes.

* Una máquina virtual con la extensión de captura de paquetes habilitada.

> [!IMPORTANT]
> La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`. Para instalar la extensión en una máquina virtual Windows, visite [Extensión de máquina virtual del agente de Network Watcher para Windows](../virtual-machines/windows/extensions-nwa.md), y en una máquina virtual Linux, visite [Extensión de máquina virtual del agente de Network Watcher para Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>Instalación de la extensión de máquina virtual

### <a name="step-1"></a>Paso 1

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>Paso 2

En el ejemplo siguiente se recupera la información de extensión necesaria para ejecutar el cmdlet `Set-AzureRmVMExtension`. Este cmdlet instala el agente de captura de paquetes en la máquina virtual invitada.

> [!NOTE]
> El cmdlet `Set-AzureRmVMExtension` puede tardar varios minutos en completarse.

En las máquinas virtuales con Windows:

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

El ejemplo siguiente es una respuesta correcta después de ejecutar el cmdlet `Set-AzureRmVMExtension`.

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>Paso 3

Para asegurarse de que el agente está instalado, ejecute el cmdlet `Get-AzureRmVMExtension` y pásele el nombre de la máquina virtual y el nombre de extensión.

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

El siguiente es un ejemplo de la respuesta de la ejecución de `Get-AzureRmVMExtension`.

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

Una vez completados los pasos anteriores, el agente de captura de paquetes está instalado en la máquina virtual.

### <a name="step-1"></a>Paso 1

El siguiente paso es recuperar la instancia de Network Watcher. Esta variable se pasa al cmdlet `New-AzureRmNetworkWatcherPacketCapture` en el paso 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>Paso 2

Recupere una cuenta de almacenamiento. Esta cuenta de almacenamiento se utiliza para almacenar el archivo de captura de paquetes.

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>Paso 3

Se pueden usar filtros para limitar los datos que se almacenan en la captura de paquetes. En el ejemplo siguiente se configuran dos filtros.  Un filtro recopila el tráfico TCP saliente solo de la dirección IP local 10.0.0.3 a los puertos de destino 20, 80 y 443.  El segundo filtro recopila solo el tráfico UDP.

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> Se pueden definir varios filtros para una captura de paquetes.

### <a name="step-4"></a>Paso 4

Ejecute el cmdlet `New-AzureRmNetworkWatcherPacketCapture` para iniciar el proceso de captura de paquetes, pasando los valores necesarios recuperados en los pasos anteriores.
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filter $filter1, $filter2
```

El ejemplo siguiente es la salida esperada de la ejecución del cmdlet `New-AzureRmNetworkWatcherPacketCapture`.

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

Al ejecutar el cmdlet `Get-AzureRmNetworkWatcherPacketCapture` se recupera el estado de una captura de paquetes que se está ejecutando o se ha completado.

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

El ejemplo siguiente es la salida del cmdlet `Get-AzureRmNetworkWatcherPacketCapture`. El ejemplo siguiente es una vez completada la captura. El valor de PacketCaptureStatus es Stopped, con un valor de StopReason de TimeExceeded. Este valor muestra que la captura de paquetes fue correcta y agotó su tiempo.
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

Al ejecutar el cmdlet `Stop-AzureRmNetworkWatcherPacketCapture` se detiene una sesión si está en curso.

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> El cmdlet no devuelve ninguna respuesta cuando se ejecuta en una sesión de captura actualmente en ejecución o en una sesión que ya se ha detenido.

## <a name="delete-a-packet-capture"></a>Eliminación de una captura de paquetes

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Eliminar una captura de paquetes no elimina el archivo en la cuenta de almacenamiento.

## <a name="download-a-packet-capture"></a>Descarga de una captura de paquetes

Una vez finalizada la sesión de captura de paquetes, el archivo de captura se puede cargar en Blob Storage o en un archivo local en la máquina virtual. La ubicación de almacenamiento de la captura de paquetes se define al crear la sesión. Una herramienta práctica para acceder a estos archivos de captura guardados en una cuenta de almacenamiento es el Explorador de Microsoft Azure Storage, que puede descargarse aquí: http://storageexplorer.com/

Si se especifica una cuenta de almacenamiento, los archivos de captura de paquetes se guardan en una cuenta de almacenamiento en la siguiente ubicación:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de cómo automatizar capturas de paquetes con las alertas de máquina virtual, consulte cómo [crear una captura de paquetes desencadenada por alertas](network-watcher-alert-triggered-packet-capture.md).

Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar IP Flow Verify](network-watcher-check-ip-flow-verify-portal.md).

<!-- Image references -->














