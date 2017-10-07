---
title: aaaTroubleshoot conexiones - 1.0 de CLI de Azure y Azure puerta de enlace de red Virtual | Documentos de Microsoft
description: "Esta página explica cómo solucionar problemas de hello toouse Monitor de red de Azure 1.0 de CLI de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a>Solución de problemas de puerta de enlace y conexiones de Virtual Network mediante la CLI de Azure 1.0 de Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API DE REST](network-watcher-troubleshoot-manage-rest.md)

Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure. Una de estas funcionalidades es la solución de problemas de recursos. Solución de problemas de recursos se puede llamar a través del portal de hello, PowerShell, CLI o API de REST. Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.

En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux. 

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](/network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Información general

Solución de problemas de recursos de hello permite solucionar los problemas que surgen con puertas de enlace de red Virtual y las conexiones. Cuando se realiza una solicitud de solución de problemas de tooresource, los registros se va a consultar e inspeccionar. Una vez finalizada la inspección, se devuelven resultados de Hola. Solicitudes de recursos para solucionar problemas de las solicitudes son de largos ejecución, este proceso puede tardar varios tooreturn minutos un resultado. registros de Hola de solución de problemas se almacenan en un contenedor en una cuenta de almacenamiento especificado.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Recuperación de una conexión de puerta de enlace de Virtual Network

En este ejemplo, la solución de problemas de recursos se va a ejecutar en una conexión. También puede pasarla una puerta de enlace de Virtual Network. Hello siguiente cmdlet enumera Hola conexiones vpn en un grupo de recursos.

```azurecli
azure network vpn-connection list -g resourceGroupName
```

También puede ejecutar Hola comando toosee conexiones hello en una suscripción.

```azurecli
azure network vpn-connection list -s subscription
```

Una vez que tenga el nombre de Hola de conexión de hello, puede ejecutar este comando tooget su Id. de recurso:

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento

Solución de problemas de recursos devuelve datos sobre el estado de saludo del recurso de hello, también guarda la cuenta de almacenamiento de registros tooa toobe revisado. En este paso, se crea una cuenta de almacenamiento; si ya existe una cuenta de almacenamiento, puede usarla.

1. Crear cuenta de almacenamiento de Hola

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. Obtener claves de cuenta de almacenamiento de Hola

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. Crear contenedor de Hola

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Ejecución de la solución de problemas de recursos Network Watcher

Solucionar problemas de recursos con hello `network watcher troubleshoot` cmdlet. Pasamos el grupo de recursos de hello cmdlet hello, nombre de Monitor de red, Hola Id. de conexión de hello, hello Hola Hola Id. de cuenta de almacenamiento de Hola y Hola ruta de acceso toohello blob toostore Hola solucionar da como resultado.

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

Una vez que ejecute el cmdlet de hello, Monitor de red se revisan mantenimiento de hello recursos tooverify Hola. Devuelve los resultados de hello toohello shell y almacena los registros de los resultados de hello en hello cuenta de almacenamiento especificada.

## <a name="understanding-hello-results"></a>Descripción de los resultados de Hola

texto de acción de Hello ofrece instrucciones generales sobre cómo tooresolve Hola problema. Si el problema de Hola se pueda realizar una acción, se proporciona un vínculo con instrucciones adicionales. En caso de hello donde no haya ninguna orientación adicional, respuesta de hello proporciona Hola url tooopen un caso de soporte técnico.  Para obtener más información acerca de las propiedades de Hola de respuesta de Hola y qué se incluye, visite [información general de solución de problemas del Monitor de red](network-watcher-troubleshoot-overview.md)

Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Otra herramienta que se puede utilizar es el Explorador de Storage. Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)

## <a name="next-steps"></a>Pasos siguientes

Si se cambiaron las configuraciones que detenga la conectividad de VPN, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que pueden estar en cuestión.
