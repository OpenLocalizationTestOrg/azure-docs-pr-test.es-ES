---
title: "Primer análisis: protección de máquinas virtuales de Azure con un almacén de Recovery Services | Microsoft Docs"
description: "Copia de seguridad de máquinas virtuales de Azure con ARM en un almacén de Servicios de recuperación. Usar copias de seguridad de máquinas virtuales implementadas por el Administrador de recursos, máquinas virtuales implementadas por el estándar y Premium almacenamiento máquinas virtuales, máquinas virtuales de cifrado, las máquinas virtuales en discos administrados tooprotect los datos. Cree y registre un almacén de Servicios de recuperación. Registre máquinas virtuales, cree directivas y proteja máquinas virtuales en Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Hacer copia de seguridad de almacenes de servicios de máquinas virtuales de Azure tooRecovery
> [!div class="op_single_selector"]
> * [Protección de máquinas virtuales con un almacén de Recovery Services](backup-azure-vms-first-look-arm.md)
> * [Protección de máquinas virtuales con un almacén de copia de seguridad](backup-azure-vms-first-look.md)
>
>

Este tutorial le guiará por los pasos de Hola para crear un almacén de servicios de recuperación y copia de seguridad de una máquina virtual (VM) de Azure. Los almacenes de Servicios de recuperación protegen:

* Máquinas virtuales implementadas en Azure Resource Manager
* Máquinas virtuales clásicas
* Máquinas virtuales de almacenamiento estándar
* Máquinas virtuales de almacenamiento premium
* Máquinas virtuales en ejecución en instancias de Managed Disks
* Máquinas virtuales cifradas mediante Azure Disk Encryption con BEK y KEK
* Copia de seguridad coherente con la aplicación de máquinas virtuales Windows mediante VSS y máquinas virtuales Linux con scripts personalizados previos a la instantánea y posteriores a la instantánea

Para obtener más información sobre la protección de almacenamiento Premium máquinas virtuales, vea el artículo de hello [copia de seguridad y restaurar las máquinas virtuales de almacenamiento Premium](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Para más información sobre la compatibilidad con máquinas virtuales de disco administrado, consulte el artículo sobre la [copia de seguridad y la restauración de máquinas virtuales en discos administrados](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). Para más información sobre el marco previo y posterior al script para copias de seguridad de máquinas virtuales Linux, consulte [Copia de seguridad coherente con la aplicación de máquinas virtuales Linux con scripts previos y posteriores] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

toofind más sobre lo que puede copia de seguridad y no, consulte [aquí](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> Este tutorial se da por supuesto que ya tiene una máquina virtual en su suscripción de Azure y que se ha tomado medidas tooallow Hola servicio copia de seguridad tooaccess Hola máquina virtual.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

Según el número de Hola de máquinas virtuales que desee tooprotect, puede comenzar desde diferentes puntos de partida. Si desea tooback seguridad de varias máquinas virtuales en una sola operación, vaya a almacén de servicios de recuperación de toohello y [trabajo de copia de seguridad de hello iniciar desde el panel de almacén de hello](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Si desea tooback una sola máquina virtual, puede iniciar el trabajo de copia de seguridad de Hola de hoja de administración de máquinas virtuales.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Configurar trabajo de copia de seguridad de Hola desde hoja de administración de máquinas virtuales de Hola

Usar hello siguiendo el trabajo de copia de seguridad de pasos tooconfigure Hola de hoja de administración de máquina virtual de Hola Hola portal de Azure. Estos pasos no aplican a máquinas virtuales de toohello en el portal clásico de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú del concentrador hello, haga clic en **más servicios** y en el cuadro de diálogo de filtro de hello, escriba **máquinas virtuales**. A medida que escribe, Hola lista de filtros de recursos. Cuando vea Máquinas virtuales, selecciónelo.

  ![En el menú del concentrador, haga clic en el cuadro de diálogo de servicios más tooopen texto y escriba máquinas virtuales](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  aparece en la lista de Hola de máquinas virtuales (VM) en la suscripción de hello.

  ![aparece en la lista de Hola de máquinas virtuales en la suscripción de Hola.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. En lista de hello, seleccione tooback de una máquina virtual.

  ![aparece en la lista de Hola de máquinas virtuales en la suscripción de Hola.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Cuando se selecciona Hola VM, lista Hola de máquinas virtuales desplaza toohello izquierda y hoja de administración de máquina virtual de Hola y el panel de la máquina virtual de hello, abrir. </br>
 ![Hoja de administración de máquinas virtuales](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. En la hoja de administración de máquinas virtuales de Hola Hola **configuración** sección, haga clic en **copia de seguridad**. </br>

  ![Opción de copia de seguridad de la hoja de administración de máquinas virtuales](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  se abre la hoja de Hello habilitar copia de seguridad.

  ![Opción de copia de seguridad de la hoja de administración de máquinas virtuales](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Para el almacén de servicios de recuperación de hello, haga clic en **seleccione existente** y elija Hola almacén desde la lista desplegable de Hola.

  ![Habilitar el Asistente para copia de seguridad](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Si no hay ningún almacenes de servicios de recuperación, o si desea toouse un nuevo almacén, haga clic en **crear nuevo** y proporcione el nombre de hello para el nuevo almacén de Hola. Se crea un nuevo almacén en hello mismo grupo de recursos y la misma ubicación que la máquina virtual de Hola. Si desea toocreate un almacén de servicios de recuperación con valores diferentes, vea Hola sección sobre cómo demasiado[crear un almacén de servicios de recuperación](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. detalles de hello tooview de hello directiva de copia de seguridad, haga clic en **directiva de copia de seguridad**.

  Hola **directiva de copia de seguridad** hoja se abre y proporciona detalles de Hola de directiva de hello seleccionado. Si existen otras directivas, utilice Hola menú desplegable toochoose una directiva de copia de seguridad diferente. Si desea toocreate una directiva, seleccione **crear nuevo** desde el menú desplegable de Hola. Si quiere instrucciones para definir una directiva de copia de seguridad, consulte [Definición de una directiva de copia de seguridad](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). Directiva de copia de seguridad de toosave Hola cambios toohello y hoja de toohello devuelto habilitar copia de seguridad, haga clic en **Aceptar**.

  ![Seleccionar directiva de copia de seguridad](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. En la hoja de hello habilitar copia de seguridad, haga clic en **habilitar la copia de seguridad** toodeploy directiva de Hola. Implementar Directiva de hello, asocia con el almacén de Hola y Hola las máquinas virtuales.

  ![Botón Enable Backup (Habilitar la copia de seguridad)](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Puede seguir el progreso de la configuración de Hola a través de notificaciones de Hola que aparecen en el portal de Hola. Hola de ejemplo siguiente se muestra que ha iniciado la implementación.

  ![Notificaciones de la opción Habilitar copia de seguridad](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Cuando haya completado el progreso de la configuración de hello, en la hoja de administración de máquinas virtuales de hello, haga clic en **copia de seguridad** hoja de elemento de la copia de seguridad de tooopen hello y vista Hola detalles.

  ![Vista de Elemento de copia de seguridad de la máquina virtual](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Hasta que haya completado la copia de seguridad inicial de hello, **último estado de copia de seguridad** se muestra como **advertencia (copia de seguridad inicial pendiente)**. toosee cuando Hola ha programado la próxima copia de seguridad se produce, en **directiva de copia de seguridad** haga clic en nombre de Hola de directiva de Hola. hoja de la directiva de copia de seguridad de Hola se abre y muestra el tiempo de Hola de copia de seguridad programada de Hola.

10. toorun una copia de seguridad del trabajo y crear punto de recuperación inicial de hello, en hello copia de seguridad del almacén de hoja haga clic en **una copia de seguridad ahora**.

  ![Haga clic en copia de seguridad ahora toorun Hola copia de seguridad inicial](./media/backup-azure-vms-first-look-arm/backup-now.png)

  se abre la hoja de copia de seguridad ahora Hola.

  ![Muestra la hoja de copia de seguridad ahora Hola](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. En hoja iniciar copia de seguridad de hello, haga clic en el icono de calendario de hello, usar Hola calendario control tooselect hello último día de este punto de recuperación se conservan y haga clic en **copia de seguridad**.

  ![se conserva el conjunto Hola último día Hola punto de recuperación de copia de seguridad ahora](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Las notificaciones de implementación le permiten saber se ha desencadenado el trabajo de copia de seguridad de Hola y que puede supervisar el progreso de hello del trabajo de hello en la página de trabajos de copia de seguridad de Hola.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Configurar trabajo de copia de seguridad de Hola desde Hola que del almacén de servicios de recuperación
trabajo de copia de seguridad de hello tooconfigure, completar Hola pasos.  

1. Cree un almacén de Recovery Services para una máquina virtual.
2. Hola tooselect portal Azure un escenario de uso establecer una directiva de copia de seguridad e identificar elementos tooprotect.
3. Ejecutar copia de seguridad inicial de Hola.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Creación de un almacén de Servicios de recuperación para una máquina virtual
Un almacén de servicios de recuperación es una entidad que almacena todas las copias de seguridad de Hola y puntos de recuperación que se han creado con el tiempo. Hello almacén de servicios de recuperación también contiene directivas de copia de seguridad de hello aplica toohello proteger las máquinas virtuales.

> [!NOTE]
> La copia de seguridad de máquinas virtuales es un proceso local. No se puede realizar copias de las máquinas virtuales del almacén de servicios de recuperación de una ubicación tooa en otra ubicación. Por lo tanto, para cada ubicación de Azure que tiene toobe de máquinas virtuales de copia de seguridad, debe existir al menos un almacén de servicios de recuperación en esa ubicación.
>
>

toocreate un almacén de servicios de recuperación:

1. Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com/) con su suscripción de Azure.
2. En el menú del concentrador hello, haga clic en **más servicios** y en el tipo de cuadro de diálogo de filtro de hello **servicios de recuperación**. A medida que escribe, Hola lista de filtros de recursos. Cuando vea almacenes de servicios de recuperación en la lista de hello, haga clic en él.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Si no hay almacenes de servicios de recuperación de la suscripción de hello, se enumeran los almacenes de Hola.

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo. nombre de Hello debe toobe único para hello suscripción de Azure. Escriba un nombre que tenga entre 2 y 50 caracteres. Debe comenzar por una letra y solo puede contener letras, números y guiones.

5. Hola **suscripción** sección, usar Hola menú desplegable toochoose hello suscripción de Azure. Si usa una sola suscripción, que aparece de la suscripción y puede omitir el paso siguiente toohello. Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción. Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.

6. Hola **grupo de recursos** sección:

    * Seleccione **crear nuevo** si desea que toocreate un grupo de recursos.
    O
    * Seleccione **utilizar existente** y haga clic en hello menú desplegable toosee Hola disponible lista de grupos de recursos.

  Para obtener información completa sobre los grupos de recursos, vea hello [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola. Esta opción determina dónde se envían los datos de copia de seguridad de región geográfica Hola.

  > [!IMPORTANT]
  > Si no está seguro de la ubicación de hello en el que existe la máquina virtual, cerrar el cuadro de diálogo de creación de almacén de Hola y vaya toohello lista de máquinas virtuales en el portal de Hola. Si tiene máquinas virtuales en varias regiones, cree un almacén de Recovery Services en cada una de ellas. Crear almacén de hello en la primera ubicación de Hola antes de pasar la ubicación siguiente toohello. No hay que ninguna cuenta de almacenamiento necesario toospecify hello usa datos de copia de seguridad de Hola toostore: almacén de servicios de recuperación de Hola y Hola servicio copia de seguridad de Azure controlan automáticamente el almacenamiento de Hola.
  >

8. En la parte inferior de Hola de hoja de almacén de servicios de recuperación de hello, haga clic en **crear**.

    Puede tardar varios minutos para hello que toobe creado del almacén de servicios de recuperación. Supervisar las notificaciones de estado de hello en el área superior derecha de hello del portal de Hola. Una vez creado el almacén, aparece en la lista de Hola de almacenes de servicios de recuperación. Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).

    ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Una vez que vea el almacén en la lista de Hola de almacenes de servicios de recuperación, son redundancia de almacenamiento de hello tooset listo.

Ahora que ha creado el almacén, obtenga información acerca de cómo tooset Hola replicación de almacenamiento.

### <a name="set-storage-replication"></a>Configuración de la replicación de almacenamiento
opción de replicación de almacenamiento de Hello permite toochoose entre el almacenamiento con redundancia geográfica y almacenamiento con redundancia local. De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica. Si hello del almacén de servicios de recuperación es la copia de seguridad principal, deje Hola storage replicación opción conjunto toogeo el almacenamiento con redundancia. Elija un almacenamiento con redundancia local si desea una opción más económica que no sea tan duradera. Obtenga más información sobre [con redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opciones de almacenamiento en hello [información general sobre la replicación de almacenamiento de Azure](../storage/common/storage-redundancy.md).

configuración de replicación de almacenamiento de Hola tooedit:

1. De hello **servicios de recuperación de los almacenes de credenciales** hoja, el nuevo almacén de hello select.

  ![Seleccione el nuevo almacén de Hola de lista de Hola de almacén de servicios de recuperación](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Cuando se selecciona el almacén de hello, Hola hoja de configuración (*que tiene el nombre del almacén de hello en la parte superior de hello*) y hoja de detalles de almacén de hello abierto.

  ![Configuración de almacenamiento de vista Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. En la hoja de configuración del nuevo almacén de hello, hello tooscroll de desplazamiento vertical hacia abajo toohello sección administrar y haga clic en **infraestructura de copia de seguridad**.
    se abre la hoja de la infraestructura de copia de seguridad de Hola.
3. En la hoja de la infraestructura de copia de seguridad de hello, haga clic en **configuración de copia de seguridad** tooopen hello **configuración de copia de seguridad** hoja.

    ![Establecer configuración de almacenamiento de Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Elija la opción de replicación de almacenamiento apropiada de hello para el almacén.

    ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica. Si utiliza Azure como un punto de conexión de almacenamiento principal de copia de seguridad, continúe toouse **con redundancia geográfica**. Si no utiliza Azure como un punto de conexión de almacenamiento de copia de seguridad principal, a continuación, elija **localmente redundante**, lo que reduce los costos de almacenamiento de Azure de Hola. En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Seleccione un objetivo de copia de seguridad, establecer una directiva y definir elementos tooprotect
Antes de registrar una máquina virtual con un almacén, ejecute tooensure de proceso de detección de Hola que se identifican las máquinas virtuales nuevas que se han agregado toohello suscripción. Hola procesar consultas Azure para la lista de Hola de máquinas virtuales de suscripción de hello, junto con información adicional como el nombre del servicio de nube de Hola y región Hola. Hola portal de Azure, escenario hace referencia toowhat va tooput en el almacén de servicios de recuperación de Hola. Directiva es la programación de hello para la frecuencia y cuándo se realizan puntos de recuperación. La directiva también incluye la duración de retención de Hola Hola puntos de recuperación.

1. Si ya dispone de los servicios de recuperación que abrir el almacén, continúe toostep 2. En caso contrario, haga clic en el menú del concentrador hello, **más servicios** y en la lista de Hola de recursos, escriba **servicios de recuperación** y haga clic en **servicios de recuperación de los almacenes de credenciales**.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    aparece en la lista de Hola de almacenes de servicios de recuperación.

    ![Lista de almacenes de credenciales de la vista de hello servicios de recuperación](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    En lista de Hola de almacenes de servicios de recuperación, seleccione un almacén tooopen su panel.

     ![Hoja del almacén abierta](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. En el menú del panel de almacén de hello, haga clic en **copia de seguridad** hoja de copia de seguridad de tooopen Hola.

    ![Hoja Backup abierta](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Abra las hojas de copia de seguridad y el objetivo de copia de seguridad de Hola.

    ![Hoja Escenario abierta](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. En el módulo de objetivo de copia de seguridad de hello, de hello **donde se está ejecutando la carga de trabajo** menú desplegable, elija Azure. De hello **especifique qué desea toobackup** lista desplegable, seleccione la máquina Virtual y haga clic en **Aceptar**.

    Estas acciones registrar extensión de máquina virtual de hello con almacén de Hola. Objetivo de copia de seguridad se cierra la hoja de Hola y Hola **directiva de copia de seguridad** abre la hoja.

    ![Hoja Escenario abierta](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. En la hoja de la directiva de copia de seguridad de hello, seleccione la directiva de copia de seguridad de Hola que desee tooapply toohello almacén.

    ![Seleccionar directiva de copia de seguridad](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    detalles de saludo de la directiva predeterminada de hello aparecen en el menú desplegable de Hola. Si desea toocreate una directiva, seleccione **crear nuevo** desde el menú desplegable de Hola. Si quiere instrucciones para definir una directiva de copia de seguridad, consulte [Definición de una directiva de copia de seguridad](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Haga clic en **Aceptar** directiva de copia de seguridad de hello tooassociate con el almacén de Hola.

    Hola hello y se cierra de hoja de directiva de copia de seguridad **seleccionar las máquinas virtuales** abre la hoja.
5. Hola **seleccionar las máquinas virtuales** hoja, elija hello tooassociate de máquinas virtuales con hello especifica la directiva y haga clic en **Aceptar**.

    ![Seleccionar carga de trabajo](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    máquina virtual de Hello seleccionado se valida. Si no ve Hola virtual máquinas que esperaba toosee, compruebe que existen en Hola misma ubicación de Azure como almacén de servicios de recuperación de Hola. se muestra la ubicación de Hola de hello que del almacén de servicios de recuperación en el panel del almacén de Hola.

6. Ahora que ha definido toda la configuración de almacén de hello, en la hoja de copia de seguridad de hello, haga clic en **habilitar la copia de seguridad** toodeploy Hola almacén de directiva toohello y Hola máquinas virtuales. Implementación de directiva de copia de seguridad de hello, no crear punto de recuperación inicial de hello para la máquina virtual de Hola.

    ![Habilitar copia de seguridad](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Después de habilitar correctamente la copia de seguridad de hello, la directiva de copia de seguridad se ejecutará en la programación. Sin embargo, continúe tooinitiate Hola primera copia de seguridad de tareas.

## <a name="initial-backup"></a>Copia de seguridad inicial
Una vez que se ha implementado una directiva de copia de seguridad en la máquina virtual de hello, que no significa que se han una copia de seguridad de datos de Hola. De forma predeterminada, Hola primera programada copia de seguridad (como se define en la directiva de copia de seguridad de hello) es Hola inicial. Hasta que se produzca la copia de seguridad inicial de hello, Hola último estado de copia de seguridad en hello **trabajos de copia de seguridad** hoja se muestra como **advertencia (copia de seguridad inicial pendiente)**.

![Copia de seguridad pendiente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

A menos que la copia de seguridad inicial vence toobegin pronto, se recomienda que ejecute **realizar una copia de seguridad ahora**.

toorun Hola trabajo inicial de copia de seguridad:

1. En el panel de almacén de hello, haga clic en número de hello en **elementos de copia de seguridad**, o haga clic en hello **elementos de copia de seguridad** icono. <br/>
  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hola **elementos de copia de seguridad** abre la hoja.

  ![Elementos de copias de seguridad](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. En hello **elementos de copia de seguridad** hoja, elemento de hello select.

  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hola **elementos de copia de seguridad** lista se abre. <br/>

  ![Trabajo de copia de seguridad desencadenado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. En hello **elementos de copia de seguridad** lista, haga clic en el botón de puntos suspensivos hello **...**  menú contextual de tooopen Hola.

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu.png)

  aparece el menú contextual de Hola.

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. En el menú contextual de hello, haga clic en **una copia de seguridad ahora**.

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  se abre la hoja de copia de seguridad ahora Hola.

  ![Muestra la hoja de copia de seguridad ahora Hola](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. En hoja iniciar copia de seguridad de hello, haga clic en el icono de calendario de hello, usar Hola calendario control tooselect hello último día de este punto de recuperación se conservan y haga clic en **copia de seguridad**.

  ![se conserva el conjunto Hola último día Hola punto de recuperación de copia de seguridad ahora](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Las notificaciones de implementación le permiten saber se ha desencadenado el trabajo de copia de seguridad de Hola y que puede supervisar el progreso de hello del trabajo de hello en la página de trabajos de copia de seguridad de Hola. Según el tamaño de saludo de la máquina virtual, crear copia de seguridad inicial de hello puede tardar unos instantes.

6. estado de hello tooview o el seguimiento de hello copia de seguridad inicial, en panel de almacén de hello, vaya a hello **trabajos de copia de seguridad** icono haga clic en **en curso**.

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  se abre la hoja de trabajos de copia de seguridad de Hola.

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Hola **trabajos de copia de seguridad** hoja, puede ver el estado de Hola de todos los trabajos. Compruebe si el trabajo de copia de seguridad de hello para la máquina virtual aún está en curso, o si se ha terminado. Cuando finaliza un trabajo de copia de seguridad, estado de hello es *completado*.

  > [!NOTE]
  > Como parte de la operación de copia de seguridad de hello, Hola servicio copia de seguridad de Azure emite una extensión de copia de seguridad de toohello de comando en cada tooflush VM todos escribe y tome una instantánea coherente.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar agente de máquina virtual de hello en la máquina virtual de Hola
Esta información se proporciona en caso de que sea necesaria. Hello Azure VM Agent debe instalarse en la máquina virtual de Azure para toowork de extensión de copia de seguridad de Hola Hola. Sin embargo, si se creó la máquina virtual de hello Galería de Azure, a continuación, Hola agente de máquina virtual ya está presente en la máquina virtual de Hola. Máquinas virtuales que se migran desde los centros de datos local, no habría instalado Hola agente de máquina virtual. En tal caso, Hola agente de máquina virtual debe toobe instalado. Si tiene problemas para realizar copias de seguridad Hola VM de Azure, compruebe que hello Azure VM Agent está instalado correctamente en la máquina virtual de hello (vea hello en la tabla siguiente). Si crea una máquina virtual personalizada, [Asegúrese hello **Hola instalar agente de máquina virtual** está seleccionada la casilla de verificación](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) antes de que se aprovisionó la máquina virtual de Hola.

Obtenga información acerca de hello [agente de máquina virtual](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) y [cómo tooinstall lo](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Hello en la tabla siguiente proporciona información adicional sobre Hola VM agente para Windows y las máquinas virtuales de Linux.

| **operación** | **Windows** | **Linux** |
| --- | --- | --- |
| Hola instalar agente de máquina virtual |<li>Descargue e instale hello [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Necesita la instalación de Hola de toocomplete de privilegios de administrador. <li>[Actualizar la propiedad de la máquina virtual de hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Hola agente está instalado. |<li> Instalar más reciente hello [agente Linux](https://github.com/Azure/WALinuxAgent) desde GitHub. Necesita la instalación de Hola de toocomplete de privilegios de administrador. <li> [Actualizar la propiedad de la máquina virtual de hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Hola agente está instalado. |
| Actualizar Hola agente de máquina virtual |Hola actualización de agente de máquina virtual es tan sencillo como Hola reinstalación [archivos binarios del agente de VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Asegúrese de que no se está ejecutando ninguna operación de copia de seguridad mientras se está actualizando el agente de máquina virtual de Hola. |Siga las instrucciones de hello en [actualizar Hola agente de máquina virtual Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Asegúrese de que no se está ejecutando ninguna operación de copia de seguridad al Hola que agente de máquina virtual se está actualizando. |
| Validar la instalación del agente de VM Hola |<li>Navegue toohello *C:\WindowsAzure\Packages* carpeta Hola VM de Azure. <li>Debería encontrar Hola WaAppAgent.exe archivo.<li> Haga clic en archivo hello, vaya demasiado**propiedades**y, a continuación, seleccione hello **detalles** campo de versión del producto de Hola de ficha debe ser 2.6.1198.718 o superior. |N/D |

### <a name="backup-extension"></a>Extensión de copia de seguridad
Una vez Hola que VM Agent esté instalado en la máquina virtual de hello, Hola servicio copia de seguridad de Azure instala Hola extensión de reserva toohello agente de máquina virtual. Hola servicio copia de seguridad de Azure sin problemas actualiza y revisiones de la extensión de copia de seguridad de hello sin intervención del usuario adicional.

servicio de copia de seguridad de Hello instala la extensión de copia de seguridad de hello, incluso si Hola VM no se está ejecutando. Una máquina virtual en ejecución proporciona mayor oportunidad de Hola de obtención de un punto de recuperación coherentes con la aplicación. Sin embargo, Hola servicio de copia de seguridad de Azure continúa tooback seguridad Hola VM incluso si se ha desactivado y no se pudo instalar la extensión de Hola. Este tipo de copia de seguridad se conoce como sin conexión de máquina virtual y punto de recuperación de hello *coherente de bloqueo*.

## <a name="troubleshooting-information"></a>Información para solución de problemas
Si tiene problemas para realizar algunas de las tareas de hello en este artículo, consulte el [Guía de solución de problemas](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Precios
costo de Hola de copia de seguridad de máquinas virtuales de Azure se basa en el número de Hola de instancias protegidas. Para obtener una definición de una instancia protegida, consulte [Descripción de una instancia protegida](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Para obtener un ejemplo de cálculo del costo de Hola de copia de seguridad de una máquina virtual, consulte [cómo se calculan las instancias protegidas](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Vea Hola precios de copia de seguridad de Azure página para obtener información acerca de [precios de copia de seguridad](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).
