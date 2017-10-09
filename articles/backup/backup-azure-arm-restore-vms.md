---
title: "Copia de seguridad de Azure: Restaurar máquinas virtuales mediante Hola portal de Azure | Documentos de Microsoft"
description: "Restauración de una máquina virtual de Azure desde un punto de recuperación con el Portal de Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "restaurar copia de seguridad; ¿Cómo toorestore; punto de recuperación;"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Use máquinas virtuales de Azure toorestore portal
> [!div class="op_single_selector"]
> * [Restauración de máquinas virtuales en el portal clásico](backup-azure-restore-vms.md)
> * [Restauración de máquinas virtuales en el Portal de Azure](backup-azure-arm-restore-vms.md)
>
>

Proteja sus datos tomando instantáneas de sus datos a intervalos definidos. Estas instantáneas se denominan puntos de recuperación y se almacenan en almacenes de Servicios de recuperación. Si, o cuando es necesario toorepair o volver a generar una máquina virtual, puede restaurar Hola VM desde cualquiera de hello guarda puntos de recuperación. Cuando se restaura un punto de recuperación, puede crear una nueva máquina virtual que es una representación en el momento de la máquina virtual de copia de seguridad, o restaurar discos y usar la plantilla de Hola que viene con él hello toocustomize restaurar la máquina virtual o realizar una recuperación de archivos individuales. Este artículo se explica cómo toorestore tooa de una máquina virtual nueva máquina virtual o los discos de restaurar todas las copias de seguridad. Para la recuperación de archivos individuales, consulte demasiado[recuperar archivos de copia de seguridad de máquina virtual de Azure](backup-azure-restore-files-from-vm.md)

![3-ways-restore-from-vm-backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo proporciona información de Hola y procedimientos para restaurar máquinas virtuales implementadas mediante el modelo de administrador de recursos de Hola.
>
>

Para restaurar una máquina virtual o todos los discos a partir de copias de seguridad de máquinas virtuales, hay que realizar dos pasos:

1. Seleccionar un punto de restauración
2. Seleccionar Hola restaurar tipo: crear una nueva máquina virtual o restaurar discos y especificar los parámetros necesarios. 

## <a name="select-restore-point-for-restore"></a>Seleccionar el punto de restauración
1. Inicie sesión en toohello [portal de Azure](http://portal.azure.com/)
2. En el menú de Azure hello, haga clic en **examinar** y en la lista de hello de servicios, escriba **servicios de recuperación**. lista de Hello de servicios ajusta toowhat que escribe. Cuando vea la opción **Almacenes de Servicios de recuperación**, haga clic en ella.

    ![Abrir el almacén de Servicios de recuperación](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    se muestra la lista de Hola de almacenes en la suscripción de Hola.

    ![Lista de almacenes de Servicios de recuperación](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. En lista de hello, almacén Hola seleccione asociado Hola VM desea toorestore. Al hacer clic en el almacén de hello, abre su panel.

    ![Lista de almacenes de Servicios de recuperación](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Ahora que se encuentra en el panel del almacén de Hola. En hello **elementos de copia de seguridad** icono, haga clic en **máquinas virtuales de Azure** toodisplay Hola máquinas virtuales asociados con el almacén de Hola.

    ![panel del almacén](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Hola **elementos de copia de seguridad** hoja se abre y muestra la lista de Hola de máquinas virtuales de Azure.

    ![lista de máquinas virtuales en el almacén](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. En lista de hello, seleccione un panel de hello tooopen de máquina virtual. abrirá el panel de la máquina virtual de Hello toohello área de supervisión, que contiene el icono de puntos de restauración de Hola.

    ![lista de máquinas virtuales en el almacén](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. En el menú del panel de máquina virtual de hello, haga clic en **restaurar**

    ![lista de máquinas virtuales en el almacén](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    se abre la hoja de restauración de Hola.

    ![hoja de restauración](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. En hello **restaurar** hoja, haga clic en **punto de restauración** tooopen hello **punto de restauración del seleccione** hoja.

    ![hoja de restauración](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    De forma predeterminada, el cuadro de diálogo de hello muestra todos los puntos de restauración de hello últimos 30 días. Hola de uso **filtro** intervalo de tiempo de hello tooalter de hello restaurar los puntos de muestra. De forma predeterminada, se muestran los puntos de restauración de toda la coherencia. Modificar **restaurar todos los puntos** filtrar tooselect una coherencia específica de puntos de restauración. Para obtener más información sobre cada tipo de punto de restauración, vea la explicación de Hola de [coherencia de los datos](backup-azure-vms-introduction.md#data-consistency).  

   * **Coherencia del punto de restauración** , elija:
     * Puntos de restauración coherentes frente a bloqueos
     * Puntos de restauración coherentes con la aplicación
     * Puntos de restauración coherentes con el sistema de archivos
     * Todos los puntos de restauración.  
8. Elija un punto de restauración y haga clic en **Aceptar**.

    ![elegir punto de restauración](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Hola **restaurar** hoja muestra hello punto de restauración está establecida.

    ![se establece el punto de restauración](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. En hello **restaurar** hoja, **restaurar la configuración** se abre automáticamente después de establece el punto de restauración.

## <a name="choosing-a-vm-restore-configuration"></a>Elección de una configuración de restauración para una máquina virtual
Ahora que ha seleccionado el punto de restauración de hello, elija una configuración para la restauración de la máquina virtual. Las opciones para configurar Hola restauran VM son toouse: portal de Azure o PowerShell.

1. Si no se encuentra ya no existe, vaya a toohello **restaurar** hoja. Asegúrese de un [punto de restauración se ha seleccionado](#select-restore-point-for-restore)y haga clic en **restaurar la configuración** tooopen hello **configuración de recuperación** hoja.

    ![el asistente para configuración de recuperación está establecido](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. En hello **restaurar la configuración** hoja, tiene dos opciones:
   * Restaurar toda la máquina virtual.
   * Restaurar discos en copia de seguridad.

El Portal proporciona una opción de creación rápida para la máquina virtual restaurada. Si desea toocustomize configuración de máquina virtual de Hola o nombres de los recursos de hello creados como parte de una nueva opción de máquina virtual, use PowerShell o portal toorestore copias de seguridad discos y uso tooattach de comandos de PowerShell les toochoice de plantilla de configuración o el uso VM que viene con la restauración hello toocustomize de discos restaura la máquina virtual. Vea [restaurar una máquina virtual con las configuraciones de red especiales](#restoring-vms-with-special-network-configurations) para obtener más información acerca de cómo toorestore máquina virtual que tiene varios NIC o en el equilibrador de carga. Si la máquina virtual de Windows usa [concentrador licencias](../virtual-machines/windows/hybrid-use-benefit-licensing.md), necesita toorestore discos y usar PowerShell o una plantilla tal como se especifica a continuación toocreate Hola VM y asegúrese de especificar LicenseType como "Windows_Server" al crear la máquina virtual tooavail concentrador ventajas en la máquina virtual restaurada. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Creación de una nueva máquina virtual desde el punto de restauración
Si no aún está allí, [seleccionar un punto de restauración](#restoring-vms-with-special-network-configurations) antes de continuar toocreating una nueva máquina virtual de restauración de punto. Una vez que se selecciona el punto de restauración, en hello **restaurar la configuración** hoja, escriba o seleccione valores para cada uno de hello siguientes campos:

* **Tipo de restauración**: cree la máquina virtual.
* **Nombre de máquina virtual** -proporcione un nombre para hello máquina virtual. Hola nombre debe ser único toohello el grupo de recursos (para una VM implementada por el Administrador de recursos) o servicio en la nube (para una VM clásico). No puede reemplazar la máquina virtual de hello si ya existe en la suscripción de Hola.
* **Grupo de recursos** : use un grupo de recursos existente o cree uno. Si va a restaurar una máquina virtual clásico, use este nombre de campo toospecify Hola de un nuevo servicio de nube. Si va a crear un nuevo servicio de nube/grupo de recursos, nombre de hello debe ser único globalmente. Por lo general, nombre del servicio de nube de hello está asociado a una dirección URL pública: por ejemplo: [cloudservice]. cloudapp.net. Si intentas toouse un nombre de servicio de grupo o una nube de recursos de nube de Hola que ya se ha usado, servicio de nube/grupo de recursos de Azure asigna Hola Hola mismo nombre como Hola máquina virtual. Azure muestra servicios en la nube o grupos de recursos y máquinas virtuales no asociados a ningún grupo de afinidad. Para obtener más información, consulte [cómo toomigrate de grupos de afinidad tooa (VNet) de red Virtual Regional](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Red virtual** : seleccione esta opción Hola de red virtual de hello (VNET) al crear máquinas virtuales. campo de Hello proporciona todas las redes virtuales asociadas con suscripciones de Hola. Grupo de recursos de hello VM se muestra entre paréntesis.
* **Subred** -si Hola red virtual tiene subredes, primera subred de hello está activada de forma predeterminada. Si no hay subredes adicionales, seleccione subred Hola deseado.
* **Cuenta de almacenamiento** -este menú enumera las cuentas de almacenamiento de Hola Hola misma ubicación que hello del almacén de servicios de recuperación. No se admiten cuentas de almacenamiento con redundancia de zona. Si no hay ninguna cuenta de almacenamiento con hello misma ubicación que Hola servicios de recuperación del almacén, debe crear uno antes de iniciar la operación de restauración de Hola. tipo de replicación de la cuenta de almacenamiento de Hola se menciona entre paréntesis.

![el asistente para configuración de restauración está establecido](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Si va a restaurar una máquina virtual implementada mediante Resource Manager, debe identificar una red virtual (VNET). Una red virtual es opcional para una máquina virtual clásica.
> 2. Si va a restaurar las VM con Managed Disks, debe asegurarse de que la cuenta de almacenamiento seleccionada no está habilitada para el Cifrado del servicio de almacenamiento (SSE) durante su ciclo de vida.
> 3. Según el tipo de almacenamiento de Hola de cuenta de almacenamiento seleccionada (premium o estándar), todos los discos que se restauran será premium o los discos estándar. En este momento no se admite el modo mixto de los discos durante la restauración.  
>
>

En hello **restaurar la configuración** hoja, haga clic en **Aceptar** toofinalize Hola restaurar de la configuración. En hello **restaurar** hoja, haga clic en **restaurar** operación de restauración de tootrigger Hola.

## <a name="restore-backed-up-disks"></a>Restaurar discos en copia de seguridad.
Si desea que la máquina virtual de toocustomize Hola gustaría toocreate desde una copia de discos que lo que está presente en la hoja de configuración de restauración, seleccione **restaurar discos** como valor para **restaurar, escriba**. Esta opción solicita una cuenta de almacenamiento en la que se copiarán los discos desde las copias de seguridad. Al elegir una cuenta de almacenamiento, seleccione una cuenta que los recursos compartidos de Hola misma ubicación como almacén de servicios de recuperación de Hola. No se admiten cuentas de almacenamiento con redundancia de zona. Si no hay ninguna cuenta de almacenamiento con hello misma ubicación que Hola servicios de recuperación del almacén, debe crear uno antes de iniciar la operación de restauración de Hola. tipo de replicación de la cuenta de almacenamiento de Hola se menciona entre paréntesis.

Cuando termine la operación de restauración, puede realizar estas tareas:
* [Hola de toocustomize plantilla use restaura máquinas virtuales](#use-templates-to-customize-restore-vm)
* [Hola use restaura máquina de virtual existente de discos tooattach tooan](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Crear una máquina virtual con PowerShell desde discos restaurados](./backup-azure-vms-automation.md#restore-an-azure-vm)

En hello **restaurar la configuración** hoja, haga clic en **Aceptar** toofinalize Hola restaurar de la configuración. En hello **restaurar** hoja, haga clic en **restaurar** operación de restauración de tootrigger Hola.

![Configuración de recuperación completa](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Realizar un seguimiento de la operación de restauración de Hola
Una vez que se activa la operación de restauración de hello, Hola servicio de copia de seguridad crea un trabajo para el seguimiento de la operación de restauración de Hola. Hola servicio de copia de seguridad también crea y muestra temporalmente notificación de hello en el área de notificaciones del portal. Si no ve la notificación de hello, siempre puede pulsar Hola notificaciones icono tooview las notificaciones.

![Restauración desencadenada](./media/backup-azure-arm-restore-vms/restore-notification.png)

tooview Hola operación mientras se está procesando o tooview cuando completa, abra la lista de trabajos de copia de seguridad de Hola.

1. En el menú de Azure hello, haga clic en **examinar** y en la lista de hello de servicios, escriba **servicios de recuperación**. lista de Hello de servicios ajusta toowhat que escribe. Cuando vea la opción **Almacenes de Servicios de recuperación**, haga clic en ella.

    ![Abrir el almacén de Servicios de recuperación](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    se muestra la lista de Hola de almacenes en la suscripción de Hola.

    ![Lista de almacenes de Servicios de recuperación](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. En lista de hello, almacén Hola seleccione asociado Hola VM restaurada. Al hacer clic en el almacén de hello, abre su panel.
3. En panel de almacén de hello en hello **trabajos de copia de seguridad** icono, haga clic en **máquinas virtuales de Azure** trabajos de hello toodisplay asociados con el almacén de Hola.

    ![panel del almacén](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Hola **trabajos de copia de seguridad** hoja se abre y muestra la lista de Hola de trabajos.

    ![lista de máquinas virtuales en el almacén](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Usar plantillas toocustomize restauración vm
Una vez [se completa la operación de restauración discos](#Track-the-restore-operation), puede utilizar plantillas de Hola que se generan como parte de la operación de restauración toocreate una nueva máquina virtual con una configuración diferente de los nombres de configuración o toocustomize copia de seguridad de recursos crear como crear una nueva máquina virtual desde el punto de restauración. 

> [!NOTE]
> Las plantillas se agregarán como parte de los discos de restauración para los puntos de recuperación realizados a partir del 1 de marzo de 2017. Son aplicables para las máquinas virtuales de discos sin cifrar y sin administrar. La compatibilidad con las máquinas virtuales de discos cifrados y administrados estará disponible en las próximas versiones. 
>
>

plantilla de hello tooget generado como parte de la opción de discos de restauración,

1. Vaya toorestore detalles del trabajo correspondiente toohello trabajo. 
2. En la pantalla de detalles de trabajo de restauración de hello, haga clic en *implementar plantilla* botón tooinitiate implementación de plantilla. 

     ![Exploración en profundidad del trabajo de restauración](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
En la hoja de plantilla de implementación de Hola para implementaciones personalizadas, utilice una implementación de plantilla demasiado[editar e implementar la plantilla de hello](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) o agregar más personalizaciones por [crea una plantilla](../azure-resource-manager/resource-group-authoring-templates.md) antes de implementar. 

   ![Implementación mediante carga de plantilla](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Después de escribir los valores de hello necesario, acepte hello *términos y condiciones* y haga clic en **compra**.

   ![Envío de una implementación de plantillas](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Pasos posteriores a la restauración
* Si usa una distribución de Linux basada en cloud-init, como Ubuntu, la contraseña se bloquea después de la restauración por seguridad. Por favor, use la extensión VMAccess en hello restaura VM demasiado[Hola de restablecimiento de contraseña](../virtual-machines/linux/classic/reset-access.md). Se recomienda utilizar claves de SSH en estos tooavoid distribuciones restablecer contraseña post restauración.
* Se instalará extensiones presentes durante la configuración de copia de seguridad de hello, sin embargo, no habilitarse. Vuelva a instalar las extensiones si surge algún problema. 
* Si Hola copia de seguridad VM tiene la dirección IP estática, restauración de post, máquina virtual restaurada tendrá un conflicto de tooavoid IP dinámico al crear restaura la máquina virtual. Obtener más información acerca de cómo puede [agregar un toorestored IP estática VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* La máquina virtual restaurada no tendrá un conjunto de valores de disponibilidad. Se recomienda usar la opción de discos de restauración y [agregar un conjunto de disponibilidad](../virtual-machines/windows/tutorial-availability-sets.md) cuando se crea una máquina virtual desde PowerShell o plantillas mediante los discos restaurados. 


## <a name="backup-for-restored-vms"></a>Copia de seguridad de máquinas virtuales restauradas
Si ha restaurado VM toosame grupo de recursos con hello homónimas copia originalmente la máquina virtual, copia de seguridad continúa en hello restauración post de máquina virtual. Si ha restaurado el grupo de recursos de máquina virtual tooa diferente o especifica un nombre diferente para la máquina virtual restaurada, se trata como una nueva máquina virtual y necesita toosetup copia de seguridad para la máquina virtual restaurada.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restauración de una máquina virtual en caso de desastre de centro de datos de Azure
Copia de seguridad de Azure permite restaurar copia de seguridad el centro de datos emparejados toohello de máquinas virtuales en caso de que las máquinas virtuales ejecutan ante desastres de experiencias y configurado toobe de almacén de copia de seguridad con redundancia geográfica del centro de datos principal de Hola. Durante estos escenarios, necesita una cuenta de almacenamiento, que está presente en el centro de datos emparejados tooselect y resto del proceso de restauración de hello permanece mismo. Copia de seguridad de Azure usa el servicio de proceso de la máquina virtual de replicación geográfica emparejada toocreate Hola restaurado. Más información sobre la [resistencia del centro de datos de Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restauración de máquinas virtuales de controlador de dominio
Copia de seguridad de las máquinas virtuales de controlador de dominio (DC) es un escenario admitido con Copia de seguridad de Azure. Sin embargo, debe tener cuidado durante el proceso de restauración de Hola. proceso de restauración correcta de Hello depende de la estructura de Hola de dominio Hola. En el caso más simple de hello tiene un único controlador de dominio en un único dominio. El caso más común en las cargas de producción es tener un solo dominio con varios DC y, quizás, algún DC local. Por último, puede tener un bosque con varios dominios. 

Desde un Hola de perspectiva de Active Directory VM de Azure es como cualquier otra máquina virtual en un hipervisor compatible moderno. Hola diferencia principal con los hipervisores local es que no hay ninguna consola de máquina virtual disponible en Azure. Es necesaria una consola para determinados escenarios, como para una recuperación mediante una copia de seguridad de reconstrucción completa (BMR). Sin embargo, la restauración de la máquina virtual del almacén de copia de seguridad de Hola es una sustitución completa para BMR. El modo de restauración de Active Directory (DSRM) también está disponible, de modo que todos los escenarios de recuperación de Active Directory son viables. Para obtener más información general, consulte [Consideraciones relacionadas con la copia de seguridad y la restauración para controladores de dominio virtualizados](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) y [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx) (Planificación de la recuperación de bosques de Active Directory).

### <a name="single-dc-in-a-single-domain"></a>Controlador de dominio único en un solo dominio
Hello VM se puede restaurar (al igual que cualquier otra máquina virtual) de hello Azure portal o mediante PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Varios controladores de dominio en un solo dominio
Cuando otros controladores de dominio del mismo dominio puede tener acceso a través de Hola Hola red, se puede restaurar Hola DC como todas las máquinas virtuales. Si es Hola último DC restante en el dominio de Hola o se realiza una recuperación en una red aislada, se debe seguir un procedimiento de recuperación del bosque.

### <a name="multiple-domains-in-one-forest"></a>Varios dominios en un solo bosque
Cuando otros controladores de dominio del mismo dominio puede tener acceso a través de Hola Hola red, se puede restaurar Hola DC como todas las máquinas virtuales. Sin embargo, en el resto de casos se recomienda una recuperación de bosques.

## <a name="restoring-vms-with-special-network-configurations"></a>Restauración de máquinas virtuales con configuraciones de red especiales
Es posible tooback seguridad y restauración de máquinas virtuales con hello siguiendo las configuraciones de red especiales. Sin embargo, estas configuraciones requieren atención especial al pasar por el proceso de restauración de Hola.

* Máquinas virtuales en el equilibrador de carga (interno y externo)
* Máquinas virtuales con varias direcciones IP reservadas
* Paso 3: Creación de máquinas virtuales con varias NIC

> [!IMPORTANT]
> Al crear la configuración de red especiales de Hola para las máquinas virtuales, debe usar las máquinas virtuales de PowerShell toocreate de discos de hello restaurados.
>
>

Vuelva a crear las máquinas virtuales toofully Hola después de restaurar toodisk, siga estos pasos:

1. Restaurar discos Hola desde un almacén de servicios de recuperación con [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Crear configuración de VM de hello necesario para el equilibrador de carga / uso de varias NIC o varios IP reservadas Hola cmdlets de PowerShell y usar toocreate Hola VM de configuración deseada.

   * Creación de una máquina virtual en el servicio en la nube con el [equilibrador de carga interno ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Crear VM tooconnect demasiado[Internet orientada hacia el equilibrador de carga](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Creación de una máquina virtual con [varias NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Creación de una máquina virtual con [varias direcciones IP reservadas](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Pasos siguientes
Ahora que puede restaurar las máquinas virtuales, vea Hola artículo para obtener información sobre los errores comunes con las máquinas virtuales de la solución de problemas. Asimismo, consulte artículo Hola acerca de cómo administrar tareas con las máquinas virtuales.

* [Solución de errores](backup-azure-vms-troubleshoot.md#restore)
* [Administración de máquinas virtuales](backup-azure-manage-vms.md)
