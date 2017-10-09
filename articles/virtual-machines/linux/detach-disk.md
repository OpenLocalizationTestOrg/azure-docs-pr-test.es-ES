---
title: aaaDetach un disco de datos de una VM Linux - Azure | Documentos de Microsoft
description: "Obtenga información acerca de toodetach un disco de datos de una máquina virtual en Azure con CLI 2.0 o hello portal de Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Cómo toodetach datos de un disco de una máquina virtual Linux

Cuando ya no necesita un disco de datos que es un equipo virtual tooa conectados, puede separar fácilmente. Esto quita el disco de saludo de la máquina virtual de hello, pero no elimina del almacenamiento. 

> [!WARNING]
> Si se desconecta un disco, no se elimina automáticamente. Si se ha suscrito tooPremium almacenamiento, se le seguirán cargas de almacenamiento tooincur disco Hola. Para obtener más información, consulte demasiado[precios y facturación al usar almacenamiento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing). 
> 
> 

Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.  

## <a name="detach-a-data-disk-using-cli-20"></a>Desconexión de un disco de datos con la CLI de 2.0

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.


## <a name="detach-a-data-disk-using-hello-portal"></a>Desconectar un disco de datos mediante el portal de Hola
1. En el concentrador de portal de hello, seleccione **máquinas virtuales**.
2. Seleccionar máquina virtual de Hola que tiene un disco de datos de Hola que desee toodetach y haga clic en **detener** toodeallocate Hola máquina virtual.
3. En la hoja de la máquina virtual de hello, seleccione **discos**.
4. En parte superior de Hola de hello **discos** hoja, seleccione **editar**.
5. Hola **discos** hoja, toohello más a la derecha del disco de datos de Hola que desearía toodetach, haga clic en hello ![imagen del botón separar](./media/detach-disk/detach.png) botón Desasociar.
5. Después de que se ha quitado el disco de hello, haga clic en Guardar en la parte superior de Hola de hoja de Hola.
6. En la hoja de la máquina virtual de hello, haga clic en **Introducción** y, a continuación, haga clic en hello **iniciar** situado en parte superior de Hola de toorestart Hola VM de hello hoja.

disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.








## <a name="next-steps"></a>Pasos siguientes
Si desea que el disco de datos de tooreuse hello, acaba [adjuntar tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

