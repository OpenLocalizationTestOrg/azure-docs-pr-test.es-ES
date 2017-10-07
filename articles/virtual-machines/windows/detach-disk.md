---
title: "aaaDetach un disco de datos de una máquina virtual de Windows - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de un disco de datos de una máquina virtual en Azure mediante el modelo de implementación del Administrador de recursos de hello toodetach."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Cómo toodetach datos de un disco de una máquina virtual de Windows
Cuando ya no necesita un disco de datos que es un equipo virtual tooa conectados, puede separar fácilmente. Esto quita el disco de saludo de la máquina virtual de hello, pero no elimina del almacenamiento.

> [!WARNING]
> Si se desconecta un disco, no se elimina automáticamente. Si se ha suscrito tooPremium almacenamiento, se le seguirán cargas de almacenamiento tooincur disco Hola. Para obtener más información, consulte demasiado[precios y facturación al usar almacenamiento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).
>
>

Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.

## <a name="detach-a-data-disk-using-hello-portal"></a>Desconectar un disco de datos mediante el portal de Hola
1. En el concentrador de portal de hello, seleccione **máquinas virtuales**.
2. Seleccionar máquina virtual de Hola que tiene un disco de datos de Hola que desee toodetach y haga clic en **detener** toodeallocate Hola máquina virtual.
3. En la hoja de la máquina virtual de hello, seleccione **discos**.
4. En parte superior de Hola de hello **discos** hoja, seleccione **editar**.
5. Hola **discos** hoja, toohello más a la derecha del disco de datos de Hola que desearía toodetach, haga clic en hello ![imagen del botón separar](./media/detach-disk/detach.png) botón Desasociar.
5. Después de que se ha quitado el disco de hello, haga clic en Guardar en la parte superior de Hola de hoja de Hola.
6. En la hoja de la máquina virtual de hello, haga clic en **Introducción** y, a continuación, haga clic en hello **iniciar** situado en parte superior de Hola de toorestart Hola VM de hello hoja.



disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.

## <a name="detach-a-data-disk-using-powershell"></a>Desconexión de un disco de datos con PowerShell
En este ejemplo, Hola el primer comando obtiene Hola máquina virtual denominada **MyVM07** en hello **RG11** grupo de recursos mediante el cmdlet Get-AzureRmVM Hola. Hola comando almacenes Hola máquina virtual en hello **$VirtualMachine** variable.

Hola segundo comando quita Hola datos de un disco con el nombre de la máquina virtual de hello DataDisk3.

comando final Hola actualiza estado de Hola de proceso de hello toocomplete Hola de máquina virtual de la eliminación de disco de datos de Hola.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

Para obtener más información, consulte [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Pasos siguientes
Si desea que el disco de datos de tooreuse hello, acaba [adjuntar tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

