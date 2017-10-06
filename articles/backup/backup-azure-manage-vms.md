---
title: "las copias de seguridad implementado por el Administrador de recursos de máquina virtual de aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las copias de seguridad implementado por el Administrador de recursos de máquina virtual toomanage y monitor"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Administración de copias de seguridad de máquinas virtuales de Azure
> [!div class="op_single_selector"]
> * [Administrar copias de seguridad de máquina virtual de Azure](backup-azure-manage-vms.md)
> * [Administrar copias de seguridad de máquina virtual clásica](backup-azure-manage-vms-classic.md)
>
>

Este artículo proporciona instrucciones sobre cómo administrar las copias de seguridad de la máquina virtual y explica Hola información de alertas de copia de seguridad disponible en el panel del portal Hola. Guía de Hello en este artículo aplica a las máquinas virtuales de toousing con almacenes de servicios de recuperación. En este artículo no cubre la creación de hello de máquinas virtuales, ni explica cómo tooprotect las máquinas virtuales. Para instrucciones detalladas sobre la protección de máquinas virtuales implementadas por el Administrador de recursos de Azure en Azure con un almacén de servicios de recuperación, consulte [primer vistazo: copia de seguridad del almacén de servicios de recuperación de tooa de máquinas virtuales](backup-azure-vms-first-look-arm.md).

## <a name="manage-vaults-and-protected-virtual-machines"></a>Administración de almacenes y máquinas virtuales protegidas
Hola portal de Azure, panel de almacén de servicios de recuperación de hello proporciona acceso tooinformation acerca de la inclusión de almacén de hello:

* Hola última copia de seguridad de instantánea, que también es el punto de restauración más reciente de Hola < br\>
* Directiva de copia de seguridad de Hola < br\>
* el tamaño total de todas las instantáneas de copia de seguridad <br\>
* número de máquinas virtuales que están protegidas con el almacén de Hola < br\>

Muchas tareas de administración con una copia de seguridad de la máquina virtual comienzan por abrir almacén de hello en el panel de Hola. Sin embargo, dado que los almacenes pueden ser tooprotect usa varios elementos (o varias máquinas virtuales), tooview detalles sobre una máquina virtual concreta, abra Panel de elemento de almacén de Hola. Hello siguiente procedimiento muestra cómo hello tooopen *panel almacén* y, a continuación, continuar toohello *panel almacén de elemento*. Hay "sugerencias" en ambos procedimientos que destacan cómo tooadd Hola almacén y almacén elemento toohello panel de Azure mediante Hola Pin toodashboard comando. Toodashboard de PIN es una manera de crear un almacén de toohello de método abreviado o un elemento. También puede ejecutar comandos comunes de acceso directo de Hola.

> [!TIP]
> Si tiene varios paneles y abrir las hojas, use el control deslizante de azul oscuro de hello en parte inferior de Hola de Hola Hola de tooslide ventana Panel de Azure y hacia atrás.
>
>

![Vista completa con control deslizante](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>Abra un almacén de servicios de recuperación en el panel de hello:
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú del concentrador hello, haga clic en **examinar** y en la lista de Hola de recursos, escriba **servicios de recuperación**. Cuando empiece a escribir, Hola filtros de la lista con los datos especificados. Haga clic en **Almacén de Servicios de recuperación**.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    se muestra la lista de Hola de almacenes de servicios de recuperación.

    ![Lista de almacenes de Servicios de recuperación ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > Si ancla un panel de Azure de almacén toohello, ese almacén está accesible inmediatamente cuando se abre Hola portal de Azure. toopin un panel de toohello de almacén, en la lista de almacén de hello, haga clic en el almacén de Hola y seleccione **toodashboard Pin**.
   >
   >
3. En lista de Hola de almacenes de credenciales, seleccione Hola almacén tooopen su panel. Al seleccionar el almacén de hello, panel de almacén de Hola y Hola **configuración** hoja abierta. Hola después de la imagen, Hola **Contoso almacén** se resalta el panel.

    ![Abrir el panel del almacén y la hoja Configuración](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>Apertura del panel de un elemento del almacén
En el procedimiento anterior de hello abrir Panel de almacén de Hola. panel de elemento de almacén de Hola tooopen:

1. En panel de almacén de hello en hello **elementos de copia de seguridad** icono, haga clic en **máquinas virtuales de Azure**.

    ![Abrir el icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    Hola **elementos de copia de seguridad** hoja muestra el último trabajo de copia de seguridad Hola para cada elemento. En este ejemplo, hay una máquina virtual, demovm-markgal, protegida por este almacén.  

    ![Icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > Para facilitar el acceso, puede anclar un toohello de elemento de almacén panel de Azure. un elemento de almacén, en la lista de elementos del almacén de hello, elemento de menú contextual hello y seleccione toopin **toodashboard Pin**.
   >
   >
2. Hola **elementos de copia de seguridad** hoja, haga clic en panel de elemento de almacén de hello elemento tooopen Hola.

    ![Icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    panel de elemento de almacén de Hola y su **configuración** hoja abierta.

    ![Panel Elementos de copia de seguridad con hoja Configuración](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    En el panel de elemento de almacén de hello, puede realizar muchas tareas de administración de claves, como:

   * cambiar de directiva o crear una directiva de copia de seguridad<br\>
   * ver los puntos de restauración y su estado de coherencia <br\>
   * copia de seguridad a petición de una máquina virtual <br\>
   * detener la protección de máquinas virtuales <br\>
   * reanudar la protección de una máquina virtual <br\>
   * eliminar los datos de una copia de seguridad (o un punto de recuperación) <br\>
   * [restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  &lt;br\>

Para Hola procedimientos Hola punto de partida es panel de elemento de almacén de Hola.

## <a name="manage-backup-policies"></a>Administrar directivas de copia de seguridad
1. En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **toda la configuración de** tooopen hello **configuración** hoja.

    ![Hoja Directiva de copia de seguridad](./media/backup-azure-manage-vms/all-settings-button.png)
2. En hello **configuración** hoja, haga clic en **directiva de copia de seguridad** tooopen esa hoja.

    Hola copia de seguridad frecuencia y retención intervalo detalles aparecen en la hoja de hello.

    ![Hoja Directiva de copia de seguridad](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. De hello **elegir la directiva de copia de seguridad** menú:

   * toochange directivas, seleccione una directiva diferente y haga clic en **guardar**. nueva directiva de Hello es el almacén de toohello aplica inmediatamente. <br\>
   * toocreate una directiva, seleccione **crear nuevo**.

     ![Copia de seguridad de máquina virtual](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     Si quiere instrucciones para crear una directiva de copia de seguridad, consulte [Definición de una directiva de copia de seguridad](backup-azure-manage-vms.md#defining-a-backup-policy).

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> Al administrar directivas de copia de seguridad, asegúrese de que hello toofollow [prácticas recomendadas](backup-azure-vms-introduction.md#best-practices) obtener el máximo rendimiento de copia de seguridad
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>Copia de seguridad a petición de una máquina virtual
Puede realizar una copia de seguridad a petición de una máquina virtual una vez que esta esté configurada para la protección. Si está pendiente la copia de seguridad inicial de hello, copia de seguridad a petición crea una copia completa de la máquina virtual de Hola Hola que del almacén de servicios de recuperación. Si se realiza una copia de seguridad inicial de hello, una copia de seguridad a petición sólo enviará cambios desde la instantánea anterior de hello, toohello el almacén de servicios de recuperación. Es decir, las copias de seguridad posteriores siempre son incrementales.

> [!NOTE]
> duración de retención de Hola para una copia de seguridad a petición es el valor de retención de hello especificado para el punto de copia de seguridad diaria de hello en la directiva de Hola. Si no se selecciona ningún punto de copia de seguridad diaria, se utiliza el punto de copia de seguridad semanal Hola.
>
>

copia de seguridad de tootrigger una petición de una máquina virtual:

* En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **una copia de seguridad ahora**.

    ![Botón Realizar copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now-button.png)

    portal de Hola se asegura de que desea toostart un trabajo de copia de seguridad a petición. Haga clic en **Sí** trabajo de copia de seguridad de toostart Hola.

    ![Botón Realizar copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now-check.png)

    trabajo de copia de seguridad de Hello crea un punto de recuperación. duración de retención de Hola Hola del punto de recuperación es Hola igual a la duración de retención especificada en la directiva de hello asociado a la máquina virtual de Hola. progreso de hello tootrack de trabajo de hello, en panel de almacén de hello, haga clic en hello **trabajos de copia de seguridad** icono.  

## <a name="stop-protecting-virtual-machines"></a>Detener la protección de máquinas virtuales
Si elige toostop proteger una máquina virtual, se le preguntará si desea que los puntos de recuperación de tooretain Hola. Hay dos maneras en las máquinas virtuales de la protección toostop:

* detener todos los trabajos futuros de copia de seguridad y eliminar todos los puntos de recuperación, o
* detener todos los futuros trabajos de copia de seguridad, pero dejar Hola puntos de recuperación <br/>

Hay un costo asociado dejando Hola puntos de recuperación en el almacenamiento. Sin embargo, ventaja de Hola de dejar Hola puntos de recuperación es que puede restaurar la máquina virtual de hello más adelante, si lo desea. Para obtener información sobre el costo de Hola de dejar Hola puntos de recuperación, vea hello [detalles de precios](https://azure.microsoft.com/pricing/details/backup/). Si elige toodelete todos los puntos de recuperación, no puede restaurar la máquina virtual de Hola.

protección de toostop para una máquina virtual:

1. En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Detener copia de seguridad**.

    ![Botón Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-button.png)

    se abre la hoja de Hello Detener copia de seguridad.

    ![Hoja Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. En hello **Detener copia de seguridad** hoja, elija si tooretain o delete Hola datos de copia de seguridad. cuadro de información de Hello ofrece información detallada acerca de su elección.

    ![Detener protección](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. Si elige datos de copia de seguridad de hello tooretain, omitir toostep 4. Si elige datos de copia de seguridad de toodelete, confirme que desea trabajos de copia de seguridad de toostop hello y eliminar puntos de recuperación de hello - nombre de Hola de tipo de elemento de Hola.

    ![Comprobación de la detención](./media/backup-azure-manage-vms/item-verification-box.png)

    Si no está seguro del nombre del elemento de hello, mantenga el mouse sobre el nombre de hello marca de exclamación tooview Hola. Además, es nombre Hola de elemento de hello en **Detener copia de seguridad** en parte superior de Hola de hoja de Hola.
4. Opcionalmente, añada un valor a los campos **Motivo** o **Comentario**.
5. Haga clic en trabajo de copia de seguridad de hello toostop para el elemento actual de hello, ![botón de Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    Un mensaje de notificación permite saber que se han detenido los trabajos de copia de seguridad de Hola.

    ![Confirmación de la detención de la protección](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>Reanudación de la protección de una máquina virtual
Si hello **conservar datos de copia de seguridad** opción se ha elegido cuando se detuvo la protección de máquina virtual de hello, es posible tooresume protección. Si hello **eliminar datos de copia de seguridad** se ha elegido la opción, a continuación, no se puede reanudar la protección de máquina virtual de Hola.

protección de tooresume para la máquina virtual de Hola

1. En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Reanudar copia de seguridad**.

    ![Reanudar protección](./media/backup-azure-manage-vms/resume-backup-button.png)

    se abre la hoja de la directiva de copia de seguridad de Hola.

   > [!NOTE]
   > Al volver a proteger máquinas virtuales de hello, puede elegir una directiva diferente a la directiva de hello con la que se protegió inicialmente máquina virtual.
   >
   >
2. Siga los pasos de hello en [administrar directivas de copia de seguridad](backup-azure-manage-vms.md#manage-backup-policies) tooassign directiva de hello para la máquina virtual de Hola.

    Una vez que Directiva de copia de seguridad de hello es un equipo virtual toohello aplicada, vea Hola siguiente mensaje.

    ![Máquina virtual protegida correctamente](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>Eliminación de datos de copia de seguridad
Puede eliminar los datos de copia de seguridad de hello asociados con una máquina virtual durante hello **Detener copia de seguridad** trabajo, o en cualquier momento después de hello ha completado el trabajo de copia de seguridad. Incluso puede ser beneficioso toowait días o semanas antes de eliminar los puntos de recuperación de Hola. A diferencia de restaurar los puntos de recuperación, cuando se elimina una copia de seguridad, no puede elegir toodelete de puntos de recuperación concreto. Si elige toodelete los datos de copia de seguridad, elimine todos los puntos de recuperación asociados con el elemento de Hola.

Hello siguiente procedimiento se da por supuesto trabajo de copia de seguridad de hello para la máquina virtual de Hola se ha detenido o deshabilitado. Una vez que se deshabilita el trabajo de copia de seguridad de hello, Hola **Reanudar copia de seguridad** y **copia de seguridad de Delete** opciones están disponibles en el panel de elemento de almacén de Hola.

![Botones Reanudar y Eliminar](./media/backup-azure-manage-vms/resume-delete-buttons.png)

datos de copia de seguridad de toodelete en una máquina virtual con hello *deshabilitado de copia de seguridad*:

1. En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **copia de seguridad de Delete**.

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    Hola **eliminar datos de copia de seguridad** abre la hoja.

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. Nombre del tipo hello de hello elemento tooconfirm desea puntos de recuperación de toodelete Hola.

    ![Comprobación de la detención](./media/backup-azure-manage-vms/item-verification-box.png)

    Si no está seguro del nombre del elemento de hello, mantenga el mouse sobre el nombre de hello marca de exclamación tooview Hola. Además, es nombre Hola de elemento de hello en **eliminar datos de copia de seguridad** en parte superior de Hola de hoja de Hola.
3. Opcionalmente, añada un valor a los campos **Motivo** o **Comentario**.
4. Haga clic en datos de copia de seguridad de hello toodelete para el elemento actual de hello, ![botón de Detener copia de seguridad](./media/backup-azure-manage-vms/delete-button.png)

    Un mensaje de notificación permite saber que se ha eliminado los datos de copia de seguridad de saludo.

## <a name="next-steps"></a>Pasos siguientes
Para información sobre cómo volver a crear una máquina virtual a partir de un punto de recuperación, consulte [Restauración de máquinas virtuales en Azure](backup-azure-restore-vms.md). Si necesita información sobre la protección de las máquinas virtuales, consulte [primer vistazo: copia de seguridad del almacén de servicios de recuperación de tooa de máquinas virtuales](backup-azure-vms-first-look-arm.md). Para más información sobre la supervisión de eventos, consulte [Supervisión de alertas de copias de seguridad de máquinas virtuales de Azure](backup-azure-monitor-vms.md).
