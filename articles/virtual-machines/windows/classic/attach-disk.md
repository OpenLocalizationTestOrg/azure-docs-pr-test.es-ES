---
title: "aaaAttach un tooa de disco virtual de Azure clásico | Documentos de Microsoft"
description: "Conectar una máquina de virtual datos disco tooa Windows creada con el modelo de implementación clásica de hello e inicializarlo."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Conectar una máquina de virtual datos disco tooa Windows creada con el modelo de implementación clásica de Hola
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

Este artículo muestra cómo los discos nuevos y existentes tooattach crean con hello clásico implementación modelo tooa máquina virtual de Windows con hello portal de Azure.

También puede [adjuntar un tooa de disco de datos VM de Linux en el portal de Azure hello](../../linux/attach-disk-portal.md).

Antes de conectar un disco, revise estas sugerencias:

* tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar. Para obtener más información, consulte [Tamaños de máquinas virtuales](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* toouse almacenamiento Premium, necesita una máquina virtual DS-series o GS-series. Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales. Almacenamiento premium está disponible en determinadas regiones. Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

* Para un disco nuevo, no es necesario toocreate lo primer porque Azure lo crea al adjuntarla.

También puede [conectar un disco de datos mediante Powershell](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Encontró la máquina virtual de Hola
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Hola seleccione la máquina virtual del recurso de hello aparece en el panel de Hola.
3. En el panel izquierdo de hello en **configuración**, haga clic en **discos**.

    ![Abrir configuración de disco](./media/attach-disk/virtualmachinedisks.png)

Continúe siguiendo las instrucciones para conectar un [nuevo disco](#option-1-attach-a-new-disk) o un [disco existente](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opción 1: adjunte e inicialice un disco nuevo

1. En hello **discos** hoja, haga clic en **adjuntar nuevas**.
2. Revise la configuración predeterminada de hello, actualizar según sea necesario y, a continuación, haga clic en **Aceptar**.

   ![Revisar configuración de disco](./media/attach-disk/attach-new.png)

3. Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.

### <a name="initialize-a-new-data-disk"></a>Inicio de un nuevo disco de datos

1. Conectar la máquina virtual de toohello. Para obtener instrucciones, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Una vez que ha iniciado sesión en la máquina virtual de toohello, abra **el administrador del servidor**. En el panel izquierdo de hello, seleccione **File and Storage Services**.

    ![Abrir Administrador de servidores](../media/attach-disk-portal/fileandstorageservices.png)

3. Seleccione **Discos**.
4. Hola **discos** sección enumera los discos de Hola. A menudo, una máquina virtual tiene los discos 0, 1 y 2. El disco 0 es el disco del sistema operativo de hello, disco 1 es el disco temporal de Hola y el disco 2 es el disco de datos de hello recién conectado toohello virtual machine. listas de disco de datos Hola Hola partición como **desconocido**.

 Haga clic en el disco de Hola y seleccione **inicializar**.

5. Se le notificará que se borrarán todos los datos cuando se inicializa el disco de Hola. Haga clic en **Sí** tooacknowledge disco de hello advertencia e inicialice Hola. Una vez completado, se enumerarán como partición de hello **GPT**. Haga clic en el disco de Hola de nuevo y seleccione **nuevo volumen**.

6. Asistente de hello completa con los valores predeterminados de Hola. Cuando se realiza el Asistente de hello, Hola **volúmenes** sección enumeran nuevo volumen de Hola. Hola disco ya está en línea y lista toostore datos.

    ![Volumen inicializado correctamente](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Opción 2: Conectar un disco existente
1. En hello **discos** hoja, haga clic en **adjuntar existente**.
2. En **Adjuntar un disco existente**, haga clic en **Ubicación**.

   ![Conectar disco existente](./media/attach-disk/attachexistingdisksettings.png)
3. En **cuentas de almacenamiento**, seleccione la cuenta de hello y contenedor que contiene el archivo .vhd de Hola.

   ![Buscar ubicación de VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Seleccione el archivo .vhd de Hola.
5. En **adjuntar el disco existente**, aparece el archivo hello que acaba de seleccionar en **archivo VHD**. Haga clic en **Aceptar**.
6. Después de que Azure asocia hello disco toohello virtual machine, aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.

## <a name="use-trim-with-standard-storage"></a>Uso de TRIM con el almacenamiento estándar

Si utiliza almacenamiento estándar (HDD), debe habilitar TRIM. TRIM descarta los bloques sin utilizar en el disco de Hola, por lo que solo se le facturará de almacenamiento que utiliza realmente. Puede ahorrar costos si usa TRIM, además de los bloques sin utilizar por eliminar archivos de gran tamaño.

Puede ejecutar esta opción de RECORTE de comando toocheck Hola. Abra un símbolo del sistema en su máquina virtual de Windows y escriba:

```
fsutil behavior query DisableDeleteNotify
```

Si el comando de hello devuelve 0, RECORTE está habilitada correctamente. Si devuelve 1, ejecute hello después tooenable comando RECORTE:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Pasos siguientes
Si la aplicación necesita datos de toostore de la unidad D: de toouse hello, puede [cambiar Hola la letra de unidad de disco temporal de Windows hello](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Recursos adicionales
[Acerca de los discos y los discos duros virtuales para máquinas virtuales](../../virtual-machines-linux-about-disks-vhds.md)
