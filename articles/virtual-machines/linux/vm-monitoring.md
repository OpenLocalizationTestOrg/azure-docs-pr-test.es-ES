---
title: "aaaEnable o deshabilitar la supervisión de VM de Azure"
description: "Describe cómo tooEnable o deshabilitar la supervisión de VM de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Habilitación o deshabilitación de la supervisión de máquinas virtuales de Azure

Esta sección describe cómo tooenable o deshabilitar la supervisión en Virtual equipos ejecutan en Azure. Puede habilitar o deshabilitar la supervisión mediante el portal de Hola o interfaz de línea de comandos de Azure para Mac, Linux y Windows (Hola CLI de Azure).

> [!IMPORTANT]
> Este documento describe la versión 2.3 de hello extensión de diagnóstico de Linux, que está en desuso. Se admitirá la versión 2.3 hasta el 30 de junio de 2018.
>
> Versión 3.0 de hello que extensión de diagnóstico de Linux pueden habilitarse en su lugar. Para obtener más información, consulte [Hola documentación](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Habilitar / deshabilitar la supervisión a través de hello portal de Azure

Puede habilitar la supervisión de la máquina virtual de Azure, que proporciona datos sobre la instancia en períodos de un minuto. (se aplican cambios de almacenamiento). Datos de diagnóstico detallada, a continuación, están disponibles para hello VM en gráficos de portal de Hola o a través de hello API. De forma predeterminada, Azure Portal permite la supervisión basada en host de un conjunto limitado de métricas. Puede habilitar la supervisión de las métricas desde dentro de una máquina virtual mientras Hola que VM esté en funcionamiento o en estado detenido.

* Abra hello Azure portal en [https://portal.azure.com](https://portal.azure.com).
* Hola barra de navegación izquierda, haga clic en máquinas virtuales.
* En máquinas virtuales de hello lista, seleccione una instancia de ejecución o detenida. se abre la hoja de "Máquina Virtual" Hola.
* Haga clic en Toda la configuración.
* Haga clic en Diagnóstico.
* Cambiar estado tooOn o desactivado. También puede elegir en este nivel de hoja Hola de detalles que le gustaría tener tooenable en la máquina virtual de supervisión.

![Habilitar / deshabilitar la supervisión a través de hello portal de Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Habilitación y deshabilitación de la supervisión con la CLI de Azure

tooenable de supervisión para una máquina virtual de Azure.

* Cree un archivo (con un nombre como PrivateConfig.json):

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Habilitar la extensión de hello mediante la CLI de Azure.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Para obtener más información, consulte [rendimiento y datos de diagnóstico de uso de la extensión de diagnóstico de Linux tooMonitor Linux VM](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
