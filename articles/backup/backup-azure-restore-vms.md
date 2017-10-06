---
title: "aaaRestore a máquinas virtuales desde la copia de seguridad | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorestore una máquina virtual de Azure de una recuperación del punto"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "restaurar copia de seguridad; ¿Cómo toorestore; punto de recuperación;"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Restauración de máquinas virtuales en Azure
> [!div class="op_single_selector"]
> * [Restauración de máquinas virtuales en el Portal de Azure](backup-azure-arm-restore-vms.md)
> * [Restauración de máquinas virtuales en el portal clásico](backup-azure-restore-vms.md)
>
>

Restaurar un tooa de máquina virtual nueva máquina virtual de copias de seguridad de hello almacenadas en un almacén de copia de seguridad de Azure con hello siguiendo los pasos.

> [!IMPORTANT]
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> **15 de octubre de 2017**, ya no estará almacenes de copia de seguridad de toocreate de toouse capaz de PowerShell. <br/> **A partir del 1 de noviembre de 2017**:
>- Los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

## <a name="restore-workflow"></a>Restauración del flujo de trabajo
### <a name="step-1-choose-an-item-toorestore"></a>Paso 1: Seleccione un elemento toorestore
1. Navegue toohello **elementos protegidos** ficha y seleccione Hola máquina virtual que desee toorestore tooa nueva máquina virtual.

    ![Elementos protegidos](./media/backup-azure-restore-vms/protected-items.png)

    Hola **punto de recuperación** columna Hola **elementos protegidos** página le indicará Hola número de puntos de recuperación para una máquina virtual. Hola **punto de recuperación más reciente** columna indica Hola Hola copia más reciente desde el que se puede restaurar una máquina virtual de.
2. Haga clic en **restaurar** tooopen hello **restaurar un elemento** asistente.

    ![restauración de un elemento](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Paso 2: Elección de un punto de recuperación
1. Hola **seleccionar un punto de recuperación** pantalla, puede restaurar desde el punto de recuperación más reciente de hello, o desde un punto anterior en el tiempo. Hola seleccionada cuando se abre el Asistente para la opción predeterminada es *punto de recuperación más reciente*.

    ![Seleccionar un punto de recuperación](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick un momento anterior en el tiempo, elija hello **Seleccionar fecha** opción en la lista desplegable de Hola y seleccione una fecha en el control de calendario Hola haciendo clic en hello **el icono de calendario**. En el control de hello, todas las fechas que tienen puntos de recuperación se rellenan con un tono de color gris claro y son seleccionables por el usuario de Hola.

    ![Seleccionar una fecha](./media/backup-azure-restore-vms/select-date.png)

    Tras hacer clic en una fecha en el control de calendario de hello, recuperación Hola apunta disponible en la que se mostrará la fecha en la siguiente tabla de puntos de recuperación. Hola **tiempo** columna indica el tiempo de hello en qué Hola se tomó la instantánea. Hola **tipo** columna muestra hello [coherencia](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) Hola punto de recuperación. encabezado de la tabla de Hello muestra hello de puntos de recuperación disponibles en ese día entre paréntesis.

    ![Puntos de recuperación](./media/backup-azure-restore-vms/recovery-points.png)
3. Seleccione el punto de recuperación de Hola de hello **puntos de recuperación** de tabla y haga clic en la pantalla siguiente de hello siguiente flecha toogo toohello.

### <a name="step-3-specify-a-destination-location"></a>Paso 3: Especificación de una ubicación de destino
1. Hola **Seleccionar instancia de restauración** pantalla Especifique los detalles de donde toorestore Hola máquina virtual.

   * Especifique el nombre de la máquina virtual de hello: en un servicio de nube especificada, el nombre de la máquina virtual de hello debe ser único. No admitimos la sobrescritura de máquinas virtuales existentes.
   * Seleccionar un servicio de nube para hello VM: este parámetro es obligatorio para la creación de una máquina virtual. Puede elegir tooeither utilice un servicio de nube existente o crear un nuevo servicio de nube.

        El nombre del servicio en la nube que se seleccione debe ser único global. Por lo general, nombre del servicio de nube de hello obtiene asociado a una dirección URL de acceso público en forma de Hola de [cloudservice]. cloudapp.net. Azure no le permitirá toocreate un nuevo servicio de nube si ya se ha utilizado el nombre de Hola. Si elige un nuevo servicio de nube toocreate, será dada Hola mismo nombre como máquina virtual de hello, en qué caso Hola VM nombre seleccionado debe ser lo suficientemente exclusivos como toobe aplica toohello asociado servicio en la nube.

        Solo se muestran servicios en la nube y redes virtuales que no están asociadas a los grupos de afinidad en hello restauración detalles de la instancia. [Más información](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Seleccione una cuenta de almacenamiento para VM hello: este parámetro es obligatorio para la creación de hello máquina virtual. Puede seleccionar de cuentas de almacenamiento existentes en hello misma región que el almacén de copia de seguridad de Azure Hola. No se admiten cuentas de almacenamiento redundantes de zona ni de almacenamiento Premium.

    Si no hay ninguna cuenta de almacenamiento con configuración compatible, cree una cuenta de almacenamiento de configuración admitidos toostarting anteriores de operación de restauración.

    ![Seleccionar una red virtual](./media/backup-azure-restore-vms/restore-sa.png)
3. Seleccione una red Virtual: red virtual de hello (VNET) para la máquina virtual de hello debe seleccionarse en tiempo de Hola de creación de VM de Hola. Hola restaurar interfaz de usuario muestra todas las redes virtuales de hello dentro de esta suscripción que se puede usar. No es obligatorio tooselect una red virtual para hello restaura VM: será capaz de tooconnect toohello restaurar virtual máquina sobre Hola internet aunque hello red virtual no se aplica.

    Si hello en la nube servicio seleccionado está asociado a una red virtual, a continuación, no se puede cambiar la red virtual de Hola.

    ![Seleccionar una red virtual](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Seleccione una subred: en caso de hello red virtual tiene subredes, de forma predeterminada primera subred de Hola se seleccionará. Elija una subred de Hola de su elección de opciones de lista desplegable de Hola. Para obtener más información de la subred, vaya tooNetworks extensión Hola [página principal del portal](https://manage.windowsazure.com/), vaya demasiado**redes virtuales** y red virtual seleccione hello y explorar en profundidad en los detalles de subred toosee de configurar.

    ![Seleccionar una subred](./media/backup-azure-restore-vms/select-subnet.png)
5. Haga clic en hello **enviar** icono en hello Asistente toosubmit Hola detalles y crear un trabajo de restauración.

## <a name="track-hello-restore-operation"></a>Realizar un seguimiento de la operación de restauración de Hola
Una vez que tiene toda la información en el Asistente para restauración de Hola Hola de entrada y lo ha enviado la copia de seguridad de Azure intentará toocreate una operación de restauración de trabajo tootrack Hola.

![Creación de un trabajo de restauración](./media/backup-azure-restore-vms/create-restore-job.png)

Si se realiza correctamente la creación de trabajos de hello, verá una notificación de notificación que indica que el trabajo de Hola se crea. Puede obtener más detalles, haga clic en hello **ver trabajo** botón que te lleve demasiado**trabajos** ficha.

![Trabajo de restauración creado](./media/backup-azure-restore-vms/restore-job-created.png)

Una vez finalizada la operación de restauración de hello, se marcará como completada en **trabajos** ficha.

![Trabajo de restauración completado](./media/backup-azure-restore-vms/restore-job-complete.png)

Después de restaurar Hola máquina virtual, es posible que tenga las extensiones de hello toore instalación existente en la VM original de Hola y [modificar extremos hello](../virtual-machines/windows/classic/setup-endpoints.md) de máquina virtual de Hola Hola portal de Azure.

## <a name="post-restore-steps"></a>Pasos posteriores a la restauración
Si utiliza una distribución de Linux basada en cloud-init, como Ubuntu, la contraseña se bloqueará después de la restauración por seguridad. Por favor, use la extensión VMAccess en hello restaura VM demasiado[Hola de restablecimiento de contraseña](../virtual-machines/linux/classic/reset-access.md). Se recomienda utilizar claves de SSH en estos tooavoid distribuciones restablecer contraseña post restauración.

## <a name="backup-for-restored-vms"></a>Copia de seguridad de máquinas virtuales restauradas
Si ha restaurado el servicio de nube VM toosame con hello homónimas copia originalmente la máquina virtual, copia de seguridad continuará en hello restauración post de máquina virtual. Si se ha restaurado el servicio de nube diferente de VM tooa o especifica un nombre diferente para la máquina virtual restaurada, esto se tratará como una nueva máquina virtual y deberá toosetup copia de seguridad para la máquina virtual restaurada.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restauración de una máquina virtual en caso de desastre de centro de datos de Azure
Copia de seguridad de Azure permite restaurar copia de seguridad el centro de datos emparejados toohello de máquinas virtuales en caso de que las máquinas virtuales ejecutan ante desastres de experiencias y configurado toobe de almacén de copia de seguridad con redundancia geográfica del centro de datos principal de Hola. Durante estos escenarios, necesita una cuenta de almacenamiento que está presente en el centro de datos emparejados tooselect y resto del proceso de restauración de hello permanece mismo. Copia de seguridad de Azure usa el servicio de proceso de la máquina virtual de replicación geográfica emparejada toocreate Hola restaurado. Más información sobre la [resistencia del centro de datos de Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restauración de máquinas virtuales de controlador de dominio
Copia de seguridad de las máquinas virtuales de controlador de dominio (DC) es un escenario admitido con Copia de seguridad de Azure. Sin embargo, debe tener cuidado durante el proceso de restauración de Hola. proceso de restauración correcta de Hello depende de la estructura de Hola de dominio Hola. En el caso más simple de hello tiene un único controlador de dominio en un único dominio. El caso más común en las cargas de producción es tener un solo dominio con varios DC y, quizás, algún DC local. Por último, puede tener un bosque con varios dominios.

Desde un Hola de perspectiva de Active Directory VM de Azure es como cualquier otra máquina virtual en un hipervisor compatible moderno. Hola diferencia principal con los hipervisores local es que no hay ninguna consola de máquina virtual disponible en Azure. Es necesaria una consola para determinados escenarios, como para una recuperación mediante una copia de seguridad de reconstrucción completa (BMR). Sin embargo, la restauración de la máquina virtual del almacén de copia de seguridad de Hola es una sustitución completa para BMR. El modo de restauración de Active Directory (DSRM) también está disponible, de modo que todos los escenarios de recuperación de Active Directory son viables. Para obtener más información general, consulte [Consideraciones relacionadas con la copia de seguridad y la restauración para controladores de dominio virtualizados](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) y [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx) (Planificación de la recuperación de bosques de Active Directory).

### <a name="single-dc-in-a-single-domain"></a>Controlador de dominio único en un solo dominio
Hello VM se puede restaurar (al igual que cualquier otra máquina virtual) de hello Azure portal o mediante PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Varios controladores de dominio en un solo dominio
Cuando otros controladores de dominio del mismo dominio puede tener acceso a través de Hola Hola red, se puede restaurar Hola DC como todas las máquinas virtuales. Si es Hola último DC restante en el dominio de Hola o se realiza una recuperación en una red aislada, se debe seguir un procedimiento de recuperación del bosque.

### <a name="multiple-domains-in-one-forest"></a>Varios dominios en un solo bosque
Cuando otros controladores de dominio del mismo dominio puede tener acceso a través de Hola Hola red, se puede restaurar Hola DC como todas las máquinas virtuales. Sin embargo, en el resto de casos se recomienda una recuperación de bosques.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Restauración de máquinas virtuales con configuraciones de red especiales
Copia de seguridad de Azure es compatible con copia de seguridad para las siguientes configuraciones de red especiales de máquinas virtuales.

* Máquinas virtuales en el equilibrador de carga (interno y externo)
* Máquinas virtuales con varias direcciones IP reservadas
* Paso 3: Creación de máquinas virtuales con varias NIC

Estas configuraciones exigen las siguientes consideraciones al restaurarlas.

> [!TIP]
> Use basadas en PowerShell restaurar flujo toorecreate Hola especiales de la red de la configuración de restauración de post de las máquinas virtuales.
>
>

### <a name="restoring-from-hello-ui"></a>Restaurar a partir de la interfaz de usuario de hello:
Al restaurar desde la interfaz de usuario, **elija siempre un nuevo servicio en la nube**. Por favor, tenga en cuenta que puesto que el portal solo toma los parámetros obligatorios durante el flujo de restauración, las máquinas virtuales restauran con interfaz de usuario perderá configuración de red especiales de hello poseen. En otras palabras, las máquinas virtuales restauradas serán máquinas virtuales normales sin configuración de equilibrador de carga ni de varias NIC o varias IP reservadas.

### <a name="restoring-from-powershell"></a>Restauración a partir de PowerShell:
PowerShell tiene Hola capacidad toojust restaurar discos de máquina virtual de hello copia de seguridad y no crear la máquina virtual de Hola. Esto resulta útil al restaurar máquinas virtuales que requieran las configuraciones de red especiales mencionadas anteriormente.

En orden toofully volver a crear la entrada de la máquina virtual de Hola restauración de discos, siga estos pasos:

1. Restaurar discos Hola de almacén de copia de seguridad con [PowerShell de copia de seguridad de Azure](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Crear configuración de VM de hello necesario para el equilibrador de carga / uso de varias NIC o varios IP reservadas Hola cmdlets de PowerShell y usar toocreate Hola VM de configuración deseada.

   * Creación de una máquina virtual en el servicio en la nube con el [equilibrador de carga interno ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Crear VM tooconnect demasiado[Internet orientada hacia el equilibrador de carga](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Creación de una máquina virtual con [varias NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Creación de una máquina virtual con [varias direcciones IP reservadas](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Pasos siguientes
* [Solución de errores](backup-azure-vms-troubleshoot.md#restore)
* [Administración de máquinas virtuales](backup-azure-manage-vms.md)
