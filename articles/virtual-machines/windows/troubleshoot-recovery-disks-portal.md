---
title: "aaaUse una aplicación de Windows para solucionar problemas de VM de hello portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot problemas de máquina virtual de Windows en Azure por conexión Hola SO disco tooa recuperación VM mediante Hola portal de Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Solucionar problemas de una VM de Windows mediante la asociación de la máquina virtual de recuperación de tooa del disco de hello SO utilizando Hola portal de Azure
Si la máquina virtual de Windows (VM) en Azure detecta un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas. Un ejemplo común sería una actualización de la aplicación que ha fallado que impide que Hola VM se pueda tooboot correctamente. Este artículo se detalla cómo toouse Hola tooconnect portal Azure su virtual duro disco tooanother toofix de máquina virtual de Windows los errores, a continuación, volver a crea la máquina virtual original.

## <a name="recovery-process-overview"></a>Introducción al proceso de recuperación
proceso de solución de problemas de Hello es como sigue:

1. Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.
2. Adjuntar y montar tooanother de disco duro virtual de hello VM de Windows para solucionar problemas.
3. Conectar toohello solución de problemas de máquina virtual. Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.
4. Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.
5. Crear una máquina virtual mediante hello: disco duro virtual original.


## <a name="determine-boot-issues"></a>Determinación de los problemas de arranque
toodetermine ¿por qué la máquina virtual no es capaz de tooboot correctamente, examine el diagnóstico de arranque Hola captura de pantalla de máquina virtual. Un ejemplo habitual sería una actualización de aplicación con error o un disco duro virtual subyacente que se va a eliminar o mover.

Seleccione la máquina virtual en el portal de hello y, a continuación, desplácese hacia abajo de toohello **soporte técnico y solución de problemas** sección. Haga clic en **diagnósticos de arranque** tooview captura de pantalla de Hola. Tenga en cuenta todos los mensajes de error específico o códigos de error toohelp determinar por qué Hola VM experimenta un problema. Hello en el ejemplo siguiente se muestra una máquina virtual en espera de detención de servicios:

![Visualización de los registros de consola de diagnóstico de arranque](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

También puede hacer clic en **captura de pantalla de** toodownload una captura de hello captura de pantalla de máquina virtual.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualización de los detalles del disco duro virtual existente
Para poder adjuntar su tooanother de disco duro virtual, necesita tooidentify Hola nombre de disco duro virtual (VHD) de Hola. 

Seleccione el grupo de recursos desde el portal de hello, a continuación, seleccione la cuenta de almacenamiento. Haga clic en **Blobs**, como en el siguiente ejemplo de Hola:

![Selección de blobs de almacenamiento](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

Normalmente, suele tener un contenedor denominado **vhds** que almacena los discos duros virtuales. Seleccione el contenedor de hello tooview una lista de discos duros virtuales. Nombre de Hola de nota de su disco duro virtual (prefijo Hola suele Hola nombre de la máquina virtual):

![Identificación del disco duro virtual en el contenedor de almacenamiento](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Seleccione el disco duro virtual existente de la lista de Hola y copiar dirección URL de Hola para su uso en hello pasos:

![Copia de la dirección URL del disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Eliminación de la VM existente
Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure. Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones. Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC). Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual. Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual. concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.

Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio. Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento. Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.

Seleccione la máquina virtual en el portal de hello, a continuación, haga clic en **eliminar**:

![Captura de pantalla de diagnósticos de arranque de máquina virtual que muestran un error de arranque](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual. concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Adjuntar tooanother de disco duro virtual existente
Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas. Adjuntar toothis Hola de disco duro virtual existente toobrowse capaz de VM toobe de solución de problemas y editar el contenido del disco de Hola. Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo. Elija o cree otro toouse de máquina virtual para solucionar problemas.

1. Seleccione el grupo de recursos desde el portal de hello, a continuación, seleccione la máquina virtual para solucionar problemas. Seleccione **Discos** y, a continuación, haga clic en **Conectar existente**:

    ![Adjuntar disco existente en el portal de Hola](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect su disco duro virtual existente, haga clic en **archivo VHD**:

    ![Busque el disco duro virtual existente.](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Seleccione la cuenta de almacenamiento y el contenedor y, a continuación, haga clic en el disco duro virtual existente. Haga clic en hello **seleccione** botón tooconfirm su elección:

    ![Seleccione el disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Con un VHD ahora seleccionado, haga clic en **Aceptar** tooattach Hola disco duro virtual existente:

    ![Confirmación de la conexión del disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Después de unos segundos, Hola **discos** panel para la máquina virtual muestra el disco duro virtual existente conectado como disco de datos:

    ![Disco duro virtual existente conectado como disco de datos](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Montar el disco de datos adjuntos de Hola

1. Abra un tooyour de conexión de escritorio remoto máquina virtual. Seleccione la máquina virtual en el portal de Hola y haga clic en **conectar**. Descargue y abra el archivo de conexión de hello RDP. Escriba su credenciales toolog en tooyour VM como se indica a continuación:

    ![Inicie sesión en tooyour máquina virtual mediante Escritorio remoto](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. Abra **Administrador del servidor** y, a continuación, seleccione **Servicios de archivos y almacenamiento**. 

    ![Seleccione Servicios de archivos y almacenamiento en Administrador del servidor.](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. disco de datos de Hola se detecta automáticamente y se adjunta. toosee una lista de hello discos conectados, seleccione **discos**. Puede seleccionar la información de volumen de tooview del disco de datos, incluida la letra de unidad de Hola. Hola siguiente ejemplo se muestra hello disco de datos adjunto y utilizar **F:**:

    ![Disco conectado e información de volumen en Administrador del servidor](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Solución de problemas en el disco duro virtual original
Con hello disco duro virtual existente montado, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario. Una vez que se ha solucionado problemas hello, continúe con hello pasos.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmontaje y desconexión del disco duro virtual original
Una vez que se resuelven los errores, desconecte el disco duro virtual existente del saludo de la máquina virtual para solucionar problemas. No se puede usar el disco duro virtual con cualquier otra máquina virtual hasta que se libera la concesión de hello adjuntar toohello de disco duro virtual de hello VM de solución de problemas.

1. En hello RDP sesión tooyour máquina virtual, abra **el administrador del servidor**, a continuación, seleccione **File and Storage Services**:

    ![Seleccione Servicios de archivos y almacenamiento en Administrador del servidor.](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. Seleccione **Discos** y, a continuación, seleccione el disco de datos. Haga clic con el botón derecho en el disco de datos y seleccione **Desconectar**:

    ![Disco de datos de conjunto hello como sin conexión en el administrador del servidor](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. Ahora separar Hola de disco duro virtual de VM de Hola. Seleccione la máquina virtual en hello portal de Azure y haga clic en **discos**. Seleccione el disco duro virtual existente y, a continuación, haga clic en **Desasociar**:

    ![Desconecte el disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Espere hasta que Hola VM desconectó correctamente el disco de datos de hello antes de continuar.

## <a name="create-vm-from-original-hard-disk"></a>Creación de máquina virtual a partir del disco duro original
usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). plantilla de Hello implementa una máquina virtual en una red virtual existente, mediante Hola dirección URL del VHD de hello comando anteriormente. Haga clic en hello **implementar tooAzure** botón como sigue:

![Implementación de máquina virtual desde una plantilla de Github](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

plantilla de Hola se carga en hello portal de Azure para la implementación. Especificar nombres de hello para la nueva máquina virtual y los recursos de Azure existentes y pegue Hola URL tooyour disco duro virtual existente. implementación de hello toobegin, haga clic en **compra**:

![Implementación de una máquina virtual a partir de una plantilla](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Rehabilitación de los diagnósticos de arranque
Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente. toocheck Hola estado de diagnóstico de arranque y activar si es necesario, seleccione la máquina virtual en el portal de Hola. En **Supervisión**, haga clic en **Configuración de diagnóstico**. Asegúrese de estado de hello es **en**, y Hola marca de verificación junto a demasiado**diagnósticos de arranque** está seleccionada. Si realiza cambios, haga clic en **Guardar**:

![Actualización de la configuración de los diagnósticos de arranque](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas para conectarse tooyour VM, consulte [tooan de las conexiones RDP solucionar problemas de máquina virtual de Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para más información sobre el uso de Resource Manager, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).