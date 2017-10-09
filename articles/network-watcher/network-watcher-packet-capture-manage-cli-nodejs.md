---
title: 'captura de paquetes de aaaManage con Monitor de red de Azure: 1.0 de CLI de Azure | Documentos de Microsoft'
description: "Esta página explica cómo toomanage Hola característica de captura de paquetes de Monitor de red mediante Azure CLI 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>Administración de capturas de paquetes con Azure Network Watcher mediante la CLI de Azure 1.0

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API de REST de Azure](network-watcher-packet-capture-manage-rest.md)

Captura de paquetes de Monitor de red le permite toocreate captura sesiones tootrack tráfico tooand desde una máquina virtual. Los filtros se proporcionan para tooensure de sesión de captura de hello que capturar solamente el tráfico de Hola que desee. Captura de paquetes le ayuda a anomalías de la red toodiagnose tanto de forma reactiva y proactiva. Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más. Al ser capaz de tooremotely capturas de paquetes de desencadenador, esta capacidad reduce la carga de Hola de una captura de paquetes en ejecución en el equipo deseado de hello, que permite ahorrar tiempo y manualmente.

En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.

En este artículo le guiará Hola diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.

- [**Inicio de una captura de paquetes**](#start-a-packet-capture)
- [**Detención de una captura de paquetes**](#stop-a-packet-capture)
- [**Eliminación de una captura de paquetes**](#delete-a-packet-capture)
- [**Descarga de una captura de paquetes**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Antes de empezar

En este artículo se supone que tiene Hola recursos siguientes:

- Una instancia del Monitor de red en la región de Hola que desea toocreate una captura de paquetes
- Una máquina virtual con el paquete de saludo capturar extensión habilitada.

> [!IMPORTANT]
> Captura de paquete requiere un toobe de agente que se ejecuta en la máquina virtual de Hola. Hola agente se instala como una extensión. Para más instrucciones acerca de las extensiones de máquina virtual, visite [Características y extensiones de las máquinas virtuales](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a>Instalación de la extensión de máquina virtual

### <a name="step-1"></a>Paso 1

Ejecute hello `azure vm extension set` agente de captura de paquetes cmdlet tooinstall hello en la máquina virtual de hello invitado.

En las máquinas virtuales Windows:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

En las máquinas virtuales Linux:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>Paso 2

tooensure que Hola agente está instalado, ejecute hello `vm extension get` cmdlet y pasarlo a grupo de recursos de Hola y el nombre de la máquina virtual. Compruebe Hola resultante lista tooensure Hola agente está instalado.

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

Hola según muestra es un ejemplo de respuesta de Hola de ejecución`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>Inicio de una captura de paquetes

Una vez hello pasos anteriores se completa, agente de captura de paquetes de saludo se instala en la máquina virtual de Hola.

### <a name="step-1"></a>Paso 1

Hola siguiente paso es instancia de Monitor de red de tooretrieve Hola. Esta variable se pasa toohello `network watcher show` cmdlet en el paso 4.

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>Paso 2

Recupere una cuenta de almacenamiento. Esta cuenta de almacenamiento es el archivo de captura de paquetes de hello toostore usado.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Paso 3

Los filtros pueden ser datos de Hola de toolimit usado almacenado por captura de paquetes de saludo. Hello en el ejemplo siguiente se configura una captura de paquetes con varios filtros.  Hello en primer lugar tres filtros recopilan el tráfico TCP saliente solo de local IP 10.0.0.3 toodestination puertos 20, 80 y 443.  último filtro de Hello recopila sólo el tráfico UDP.

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Se pueden definir varios filtros para una captura de paquetes. Si se utiliza una estructura de filtro complejas, es mejor filtros toouse como un errores de sintaxis de json archivo tooavoid. Por ejemplo, usar Hola marca "-r" (en lugar de "-f") y pase Hola ubicación de un archivo json que contiene Hola después de filtros:

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


el ejemplo siguiente se Hello es resultado de hello esperada de la ejecución hello `network watcher packet-capture create` cmdlet.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a>Obtención de una captura de paquetes

Ejecuta hello `network watcher packet-capture show` cmdlet, recupera el estado de saludo de una captura de paquetes que se está ejecutando o se han completado.

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

el ejemplo siguiente se Hello es resultado de hello de hello `network watcher packet-capture show` cmdlet. Hello siguiente ejemplo es una vez completada la captura de Hola. Hola PacketCaptureStatus valor se detiene, con un StopReason de TimeExceeded. Este valor muestra que captura de paquetes de saludo fue correcta y ejecutó su tiempo.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a>Detención de una captura de paquetes

Mediante la ejecución de hello `network watcher packet-capture stop` cmdlet, si una sesión de captura está en curso se detiene.

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Hola cmdlet no devuelve ninguna respuesta cuando se ejecutó en una sesión de captura actualmente en ejecución o una sesión existente que ya se ha detenido.

## <a name="delete-a-packet-capture"></a>Eliminación de una captura de paquetes

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
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

Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
