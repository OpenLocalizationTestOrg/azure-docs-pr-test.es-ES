---
title: "Asegúrese de Hola unidad D: de una máquina virtual un disco de datos | Documentos de Microsoft"
description: "Describe cómo letras de unidad de toochange para una máquina virtual de Windows para que puedan utilizar unidad D: de hello como una unidad de datos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Usar la unidad D: de hello como una unidad de datos en una máquina virtual de Windows
Si la aplicación necesita hello toouse datos de toostore la unidad D, siga estas toouse instrucciones otra letra de unidad de disco temporal de Hola. Nunca use Hola disco temporal toostore datos que necesita tookeep.

Si se cambia el tamaño o **detener (desasignar)** una máquina virtual, esto puede desencadenar una selección de ubicación de hello máquina virtual tooa nuevo hipervisor. Un evento de mantenimiento planificado o no planificado también puede desencadenar esta colocación. En este escenario, disco temporal de hello será toohello reasignarse primera letra de unidad disponible. Si tiene una aplicación que requiera específicamente la unidad D: de hello, necesita toofollow estos pasos tootemporarily movimiento Hola pagefile.sys, conectar un disco de datos nuevo y asignarle Hola letra D y, a continuación, mover Hola pagefile.sys hacer copia de unidad temporal de toohello. Una vez completado, Azure no tendrá volver Hola D: si Hola VM mueve tooa diferentes hipervisor.

Para obtener más información acerca de cómo Azure utiliza disco temporal de hello, consulte [descripción de la unidad temporal de hello en máquinas virtuales de Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Adjuntar disco de datos de Hola
En primer lugar, necesitará la máquina virtual de toohello de disco de datos de tooattach Hola. toodo este mediante el portal de hello, consulte [cómo disco tooattach un datos administrados en el portal de Azure de hello](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Mover temporalmente pagefile.sys tooC unidad
1. Conectar la máquina virtual de toohello. 
2. Menú contextual hello **iniciar** menú y seleccione **System**.
3. En el menú izquierdo de hello, seleccione **configuración avanzada del sistema**.
4. Hola **rendimiento** sección, seleccione **configuración**.
5. Seleccione hello **avanzadas** ficha.
6. Hola **memoria Virtual** sección, seleccione **cambio**.
7. Seleccione hello **C** unidad y, a continuación, haga clic en **tamaño administrado por el sistema** y, a continuación, haga clic en **establecer**.
8. Seleccione hello **d.** unidad y, a continuación, haga clic en **ningún archivo de paginación** y, a continuación, haga clic en **establecer**.
9. Haga clic en Aplicar. Recibirá una advertencia que ese equipo Hola debe toobe reiniciar Hola cambios tootake efecto.
10. Reinicie la máquina virtual de Hola.

## <a name="change-hello-drive-letters"></a>Letras de unidad de cambio Hola
1. Una vez Hola VM se haya reiniciado, vuelva a iniciarla toohello máquina virtual.
2. Haga clic en hello **iniciar** menú y tipo **diskmgmt.msc** y presione ENTRAR. Se iniciará la Administración de discos.
3. Haga doble clic en **d.**, unidad de almacenamiento temporal de Hola y seleccione **cambiar la letra de unidad y rutas de acceso**.
4. En Letra de unidad, seleccione una unidad nueva como, por ejemplo, **T** y haga clic en**Aceptar**. 
5. Haga doble clic en el disco de datos de Hola y seleccione **cambiar la letra de unidad y rutas de acceso**.
6. En Letra de unidad, seleccione la unidad **D** y haga clic en**Aceptar**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Mover la unidad de almacenamiento temporal de pagefile.sys toohello atrás
1. Menú contextual hello **iniciar** menú y seleccione **sistema**
2. En el menú izquierdo de hello, seleccione **configuración avanzada del sistema**.
3. Hola **rendimiento** sección, seleccione **configuración**.
4. Seleccione hello **avanzadas** ficha.
5. Hola **memoria Virtual** sección, seleccione **cambio**.
6. Seleccione unidad Hola OS **C** y haga clic en **ningún archivo de paginación** y, a continuación, haga clic en **establecer**.
7. Seleccione la unidad de almacenamiento temporal de hello **T** y, a continuación, haga clic en **tamaño administrado por el sistema** y, a continuación, haga clic en **establecer**.
8. Haga clic en **Apply**. Recibirá una advertencia que ese equipo Hola debe toobe reiniciar Hola cambios tootake efecto.
9. Reinicie la máquina virtual de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Puede aumentar el almacenamiento de máquina virtual hello tooyour disponible por [adjuntar un disco de datos adicionales](attach-managed-disk-portal.md).

