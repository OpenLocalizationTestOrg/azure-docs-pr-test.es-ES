---
title: 'captura de paquetes de aaaManage con Monitor de red de Azure: portal de Azure | Documentos de Microsoft'
description: "Esta página explica cómo toomanage Hola característica de captura de paquetes de Monitor de red mediante el portal de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Administrar capturas de paquetes con Monitor de red de Azure mediante el portal de Hola

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-packet-capture-manage-portal.md)
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

Este artículo se supone que dispone de hello recursos siguientes:

- Una instancia del Monitor de red en la región de Hola que desea toocreate una captura de paquetes
- Una máquina virtual con el paquete de saludo capturar extensión habilitada.

> [!IMPORTANT]
> La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`. Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Extensión del agente de captura de paquetes a través del portal de Hola

captura de paquetes de saludo tooinstall agente de máquina virtual a través del portal de hello, navegar por la máquina virtual de tooyour, haga clic en **extensiones** > **agregar** y busque **agente del Monitor de red para Windows**

![Vista del agente][agent]

## <a name="packet-capture-overview"></a>Introducción a la captura de paquetes

Navegue toohello [portal de Azure](https://portal.azure.com) y haga clic en **red** > **Monitor de red** > **de captura de paquetes**

página de información general de Hello muestra una lista de todos los paquetes que existen independientemente del estado de hello captura.

> [!NOTE]
> Captura de paquetes requiere la cuenta de almacenamiento de toohello de conectividad en el puerto 443.

![Pantalla de introducción a la captura de paquetes][1]

## <a name="start-a-packet-capture"></a>Inicio de una captura de paquetes

Haga clic en **agregar** toocreate una captura de paquetes.

Hola las propiedades que se pueden definir en una captura de paquetes son:

**Configuración principal**

- **Suscripción** -este valor es la suscripción de Hola que se usa, se necesita una instancia del Monitor de red en cada suscripción.
- **Grupo de recursos** -grupo de recursos de Hola de máquina virtual de Hola que se destina.
- **Máquina virtual de destino** -Hola máquina que se está ejecutando la captura de paquetes de saludo
- **Nombre de la captura de paquetes** -este valor es el nombre de Hola de captura de paquetes de saludo.

**Configuración de captura**

- **Cuenta de almacenamiento**: determina si la captura de paquetes se guarda en una cuenta de almacenamiento.
- **Archivo** -determina si una captura de paquetes se guarda localmente en la máquina virtual de Hola.
- **Las cuentas de almacenamiento** -Hola seleccionado captura de paquetes de almacenamiento cuenta toosave hello en. La ubicación predeterminada es https://{nombre de la cuenta de almacenamiento}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{nombre del grupo de recursos}/providers/microsoft.compute/virtualmachines/{nombre de la máquina virtual}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap. (Solo se habilita si está seleccionada la opción **Almacenamiento**)
- **Ruta de acceso de archivo local** -ruta de acceso local de hello en una captura de paquetes de máquina virtual toosave Hola. (Solo se habilita si está seleccionada la opción **Archivo**). Se tiene que proporcionar una ruta de acceso válida
- **Número máximo de bytes por paquete** -Hola número de bytes de cada paquete que se capturan, se capturan todos los bytes si se deja en blanco.
- **Número máximo de bytes por sesión** : Total número de bytes que se capturan, una vez que se alcanza el valor de hello deja de captura de paquetes de Hola.
- **Límite de tiempo (segundos)** -establece un límite de tiempo para toostop de captura de paquetes de saludo. El valor predeterminado es 18 000 segundos.

> [!NOTE]
> Actualmente las cuentas de Premium Storage no se admiten para almacenar paquetes de captura.

**Filtrado (opcional)**

- **Protocolo** -Hola toofilter de protocolo para la captura de paquetes de saludo. los valores disponibles de Hello son TCP, UDP y ninguno.
- **La dirección IP local** -este valor filtra toopackets de captura de paquetes de saludo donde la dirección IP local Hola coincide con este valor de filtro.
- **Puerto local** -este valor filtra toopackets de captura de paquetes de saludo donde puerto local Hola coincide con este valor de filtro.
- **Dirección IP remota** -este valor filtra toopackets de captura de paquetes de saludo donde hello remoto IP coincide con este valor de filtro.
- **Puerto remoto** -este valor filtra toopackets de captura de paquetes de saludo donde puerto remoto hello coincide con este valor de filtro.

> [!NOTE]
> Los valores de dirección IP y puerto pueden ser un solo valor, un rango de valores o un conjunto. (es decir, 80-1024 para el puerto) Puede definir tantos filtros como desee.

Una vez que se rellenan los valores de hello, haga clic en **Aceptar** toocreate captura de paquetes de saludo.

![Creación de una captura de paquetes][2]

Después de establecer el límite de tiempo de hello en captura de paquetes de saludo ha expirado, captura de paquetes de saludo se detendrá y se puedan revisar. También puede detener manualmente sesiones de capturas de paquetes de Hola.

## <a name="delete-a-packet-capture"></a>Eliminación de una captura de paquetes

Paquete de saludo capturar vista, haga clic en hello **menú contextual** (...) o haga clic en y haga clic en **eliminar** captura de paquetes de saludo toostop

![Eliminación de una captura de paquetes][3]

> [!NOTE]
> Eliminar una captura de paquetes no elimina archivos hello en la cuenta de almacenamiento de Hola.

Se le pide tooconfirm desea toodelete captura de paquetes de saludo, haga clic en **sí**

![Confirmación][4]

## <a name="stop-a-packet-capture"></a>Detención de una captura de paquetes

Paquete de saludo capturar vista, haga clic en hello **menú contextual** (...) o haga clic en y haga clic en **detener** captura de paquetes de saludo toostop

## <a name="download-a-packet-capture"></a>Descarga de una captura de paquetes

Una vez que haya finalizado la sesión de captura de paquetes, Hola captura archivo es tooblob cargado tooa o almacenamiento local en hello máquina virtual. ubicación de almacenamiento de Hola de captura de paquetes de saludo se define en la creación de sesión de Hola. Una herramienta adecuada tooaccess estos capturar los archivos de cuenta de almacenamiento de tooa guardado es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/

Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)

Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













