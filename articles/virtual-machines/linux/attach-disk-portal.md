---
title: aaaAttach un tooa de disco de datos VM de Linux | Documentos de Microsoft
description: "¿Cómo tooattach datos nuevos o existentes disco tooa VM de Linux en hello Azure portal mediante Hola modelo de implementación del Administrador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>¿Cómo tooattach datos de un disco tooa VM de Linux en hello portal de Azure
Este artículo muestra cómo tooattach nueva y existente discos de máquina virtual de Linux tooa a través de hello portal de Azure. También puede [adjuntar un tooa de disco de datos VM de Windows en el portal de Azure hello](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Puede elegir toouse en discos de Azure administrados o no administrada de discos. Discos administrados se controlan mediante la plataforma Windows Azure hello y no requieren ningún toostore los preparativos o ubicación ellos. Los discos no administrados requieren una cuenta de almacenamiento y tienen algunas [cuotas y límites que se deben aplicar](../../azure-subscription-service-limits.md#storage-limits). Para más información sobre Azure Managed Disks, consulte [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Introducción a Azure Managed Disks).

Antes de adjuntar discos tooyour VM, revise estas sugerencias:

* tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* toouse almacenamiento Premium, necesita una máquina virtual DS-series o GS-series. Puede usar discos Premium y Estándar con estas máquinas virtuales. Almacenamiento premium está disponible en determinadas regiones. Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Discos conectados toovirtual máquinas son realmente los archivos .vhd almacenados en Azure. Para obtener más información, vea [Acerca de los discos y los discos duros virtuales para máquinas virtuales](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Encontró la máquina virtual de Hola
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú del concentrador hello, haga clic en **máquinas virtuales**.
3. Seleccione la máquina virtual de Hola de lista de Hola.
4. toohello Virtual hoja, los equipos en **Essentials**, haga clic en **discos**.
   
    ![Abrir configuración de disco](./media/attach-disk-portal/find-disk-settings.png)

Para continuar, siga las instrucciones y conecte un [disco administrado](#use-azure-managed-disks) o un [disco no administrado](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Uso de Azure Managed Disks

### <a name="attach-a-new-disk"></a>Conexión de un disco nuevo

1. En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.
2. Haga clic en el menú desplegable de Hola para **nombre** y seleccione **crear disco**:

    ![Creación de disco administrado de Azure](./media/attach-disk-portal/create-new-md.png)

3. Escriba un nombre para el disco administrado. Revise la configuración predeterminada de hello, actualizar según sea necesario y, a continuación, haga clic en **crear**.
   
   ![Revisar configuración de disco](./media/attach-disk-portal/create-new-md-settings.png)

4. Haga clic en **guardar** toocreate Hola administrados disco y actualización de configuración de máquina virtual de hello:

   ![Guardado del nuevo Azure Managed Disk](./media/attach-disk-portal/confirm-create-new-md.png)

5. Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**. Como discos administrados son un recurso de nivel superior, disco de hello aparece en la raíz de Hola Hola del grupo de recursos:

   ![Azure Managed Disk en grupo de recursos](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>un disco existente
1. En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.
2. Haga clic en el menú desplegable de Hola para **nombre** tooview una lista de las administra discos accesible tooyour suscripción de Azure. Seleccione Hola administrado tooattach de disco:

   ![Conexión de un disco administrado de Azure existente](./media/attach-disk-portal/select-existing-md.png)

3. Haga clic en **guardar** tooattach Hola existente administrado disco y actualización de configuración de máquina virtual de hello:
   
   ![Guardado de las actualizaciones del disco administrado de Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Después de que Azure asocia hello disco toohello virtual machine, aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.

## <a name="use-unmanaged-disks"></a>Uso de discos no administrados

### <a name="attach-a-new-disk"></a>Conexión de un disco nuevo

1. En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.
2. Revise la configuración predeterminada de hello, actualizar según sea necesario y, a continuación, haga clic en **Aceptar**.
   
   ![Revisar configuración de disco](./media/attach-disk-portal/attach-new.png)
3. Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.

### <a name="attach-an-existing-disk"></a>un disco existente
1. En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.
2. En **Adjuntar un disco existente**, haga clic en **Archivo VHD**.
   
   ![Conectar disco existente](./media/attach-disk-portal/attach-existing.png)
3. En **cuentas de almacenamiento**, seleccione la cuenta de hello y contenedor que contiene el archivo .vhd de Hola.
   
   ![Buscar ubicación de VHD](./media/attach-disk-portal/find-storage-container.png)
4. Seleccione el archivo .vhd de Hola.
5. En **adjuntar el disco existente**, aparece el archivo hello que acaba de seleccionar en **archivo VHD**. Haga clic en **Aceptar**.
6. Después de que Azure asocia hello disco toohello virtual machine, aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.


## <a name="next-steps"></a>Pasos siguientes
Después de agrega el disco de hello, necesita tooprepare, para su uso. Para obtener más información, consulte [Inicio de un nuevo disco de datos](add-disk.md).
