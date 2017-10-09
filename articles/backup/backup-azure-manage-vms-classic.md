---
title: "aaaManage y monitor de copias de seguridad de máquina virtual de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage y monitor un virtual de Azure las copias de seguridad de máquinas"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>Administrar trabajos de copia de seguridad de Azure comunes y las alertas de desencadenador en el portal clásico de Hola
> [!div class="op_single_selector"]
> * [Administrar copias de seguridad de máquina virtual de Azure](backup-azure-manage-vms.md)
> * [Administrar copias de seguridad de máquina virtual clásica](backup-azure-manage-vms-classic.md)
>
>

Este artículo proporciona información acerca de las tareas de administración y supervisión comunes para las máquinas virtuales de modelo clásico protegidas en Azure.  

> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Vea [preparar su tooback entorno las máquinas virtuales de Azure](backup-azure-vms-prepare.md) para obtener más información acerca de cómo trabajar con la implementación estándar de modelo máquinas virtuales.
>
> [!IMPORTANT]
>A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.
>
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell. **El 1 de noviembre de 2017**:
>- Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.

## <a name="manage-protected-virtual-machines"></a>Administrar máquinas virtuales protegidas
toomanage máquinas virtuales protegidas:

1. tooview y administrar la configuración de copia de seguridad para una máquina virtual, haga clic en hello **elementos protegidos** ficha.
2. Haga clic en nombre de Hola de un saludo de toosee elemento protegido **detalles de la copia de seguridad** ficha, que muestra información acerca de la última copia de seguridad de Hola.

    ![Copia de seguridad de máquina virtual](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview y administrar la configuración de directiva de copia de seguridad para una máquina virtual, haga clic en hello **directivas** ficha.

    ![Directiva de máquina virtual](./media/backup-azure-manage-vms/manage-policy-settings.png)

    Hola **directivas de copia de seguridad** ficha muestra Hola directiva existente. Se puede modificar según sea necesario. Si necesita toocreate una nueva directiva, haga clic en **crear** en hello **directivas** página. Tenga en cuenta que si desea tooremove una directiva no debe tener las máquinas virtuales asociadas a él.

    ![Directiva de máquina virtual](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. Puede obtener más información sobre acciones o estado de una máquina virtual en hello **trabajos** página. Haga clic en un trabajo en hello lista tooget más detalles o filtre los trabajos de una máquina virtual específica.

    ![Trabajos](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>Copia de seguridad a petición de una máquina virtual
Puede realizar una copia de seguridad a petición de una máquina virtual una vez que esta esté configurada para la protección. Si la copia de seguridad inicial de hello está pendiente para la máquina virtual de hello, copia de seguridad a petición creará una copia completa de la máquina virtual de hello en el almacén de copia de seguridad de Azure. Si se ha completado la primera copia de seguridad, copia de seguridad de petición se solo almacén de envío de cambios desde la copia de seguridad de copia de seguridad tooAzure anterior, es decir, es siempre incremental.

> [!NOTE]
> Duración de retención de una copia de seguridad a petición se establece el valor tooretention especificado para la retención diaria en directiva de copia de seguridad correspondiente toohello VM.  
>
>

copia de seguridad de tootake una petición de una máquina virtual:

1. Navegue toohello **elementos protegidos** página y seleccione **Máquina Virtual de Azure** como **tipo** (si aún no está seleccionado) y haga clic en **seleccione**botón.

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. Seleccione la máquina virtual de hello en el que desea tootake a petición en copia de seguridad y haga clic en **copia de seguridad ahora** situado en la parte inferior de Hola de página de Hola.

    ![Copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now.png)

    Esto creará un trabajo de copia de seguridad en la máquina virtual de hello seleccionado. Duración de retención de punto de recuperación creado a través de este trabajo será igual a la que especificó en la directiva de hello asociado a la máquina virtual de Hola.

    ![Creación de trabajo de copia de seguridad](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > Directiva de hello tooview asociada a una máquina virtual, explorar hacia abajo en la máquina virtual en hello **elementos protegidos** toobackup vaya directiva fichas y páginas.
   >
   >
3. Una vez que se crea el trabajo de hello, puede hacer clic en **ver trabajo** botón de notificación de hello barra toosee trabajo de hello correspondiente en la página de trabajos de Hola.

    ![Trabajo de copia de seguridad creado](./media/backup-azure-manage-vms/created-job.png)
4. Tras finalizar correctamente el trabajo de hello, un punto de recuperación se creará que puede usar máquinas virtuales de toorestore Hola. Esto también incrementará el valor de columna de punto de recuperación de hello en 1 en **elementos protegidos** página.

## <a name="stop-protecting-virtual-machines"></a>Detener la protección de máquinas virtuales
Puede elegir toostop Hola copias de seguridad de una máquina virtual con hello siguientes opciones:

* Conservar los datos de copia de seguridad asociados a la máquina virtual en el almacén de copia de seguridad de Azure
* Eliminación de datos de copia de seguridad asociados a la máquina virtual

Si ha seleccionado los datos de copia de seguridad de tooretain asociados a la máquina virtual, puede usar máquina virtual de hello datos de copia de seguridad toorestore Hola. Para obtener más detalles sobre el precio de estas máquinas virtuales, haga clic [aquí](https://azure.microsoft.com/pricing/details/backup/).

protección de tooStop para una máquina virtual:

1. Navegue demasiado**elementos protegidos** página y seleccione **máquina virtual de Azure** como tipo de filtro de hello (si aún no está seleccionado) y haga clic en **seleccione** botón.

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. Seleccione la máquina virtual de Hola y haga clic en **detener protección** final Hola de página Hola.

    ![Detener protección](./media/backup-azure-manage-vms/stop-protection.png)
3. De forma predeterminada, copia de seguridad de Azure no se elimina datos de copia de seguridad de hello asociados a la máquina virtual de Hola.

    ![Confirmación de la detención de la protección](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Si desea que los datos de copia de seguridad de toodelete, active la casilla de verificación de Hola.

    ![Casilla de verificación](./media/backup-azure-manage-vms/checkbox.png)

    Seleccione un motivo para detener la copia de seguridad de Hola. Aunque esto es opcional, proporcionar un motivo ayuda toowork de copia de seguridad de Azure en los comentarios de Hola y dar prioridad a los escenarios de clientes de Hola.
4. Haga clic en **enviar** Hola de botón toosubmit **detener la protección** trabajo. Haga clic en **ver trabajo** toosee Hola trabajo Hola correspondiente en **trabajos** página.

    ![Detener protección](./media/backup-azure-manage-vms/stop-protect-success.png)

    Si no ha seleccionado **eliminar los datos de copia de seguridad asociados** opción durante la **detener protección** protección Asistente y, a continuación, complete el trabajo posterior, también cambia el estado**protección detiene**. datos de Hello permanecen con la copia de seguridad de Azure hasta que se elimine de forma explícita. Siempre se pueden eliminar datos de hello seleccionando la máquina virtual de Hola Hola **elementos protegidos** página y haga clic en **eliminar**.

    ![Protección detenida](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Si ha seleccionado hello **eliminar los datos de copia de seguridad asociados** opción, hello máquina virtual no formar parte del programa Hola a **elementos protegidos** página.

## <a name="re-protect-virtual-machine"></a>Volver a proteger la máquina virtual
Si no ha seleccionado hello **eliminar datos de copia de seguridad asociados** opción **detener protección**, poder volver a proteger máquinas virtuales de hello siguiendo Hola pasos similares toobacking seguridad registrado virtual máquinas. Una vez protegida, esta máquina virtual tendrá protección de datos de copia de seguridad almacenados toostop anterior y puntos de recuperación crean después de volver a proteger.

Después de volver a proteger, estado de protección de la máquina virtual Hola se cambiarán demasiado**Protected** si demasiado hay puntos de recuperación anterior**detener protección**.

  ![Máquina virtual protegida de nuevo](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Al volver a proteger máquinas virtuales de hello, puede elegir una directiva diferente a la directiva de hello con la que se protegió inicialmente máquina virtual.
>
>

## <a name="unregister-virtual-machines"></a>Anular registro de máquinas virtuales
Si desea que tooremove Hola virtual machine del almacén de copia de seguridad de hello:

1. Haga clic en hello **UNREGISTER** situado en la parte inferior de Hola de página de Hola.

    ![Deshabilitar protección](./media/backup-azure-manage-vms/unregister-button.png)

    Una notificación del sistema aparecerá en la parte inferior de Hola de pantalla de bienvenida que solicita confirmación. Haga clic en **Sí** toocontinue.

    ![Deshabilitar protección](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>Eliminación de datos de copia de seguridad
Puede eliminar los datos de copia de seguridad de hello asociados con una máquina virtual, ya sea:

* Durante el trabajo de detención de la protección
* Después de realizar un trabajo de detención de la protección en una máquina virtual

datos de copia de seguridad de toodelete en una máquina virtual, que se encuentra en hello *protección detiene* estado registrar la finalización correcta de un **Detener copia de seguridad** trabajo:

1. Navegue toohello **elementos protegidos** página y seleccione **Máquina Virtual de Azure** como *tipo* y haga clic en hello **seleccione** botón.

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. Seleccione la máquina virtual de Hola. máquina virtual de Hello estará en **protección detiene** estado.

    ![Protección detenida](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Haga clic en hello **eliminar** situado en la parte inferior de Hola de página de Hola.

    ![Eliminación de copia de seguridad](./media/backup-azure-manage-vms/delete-backup.png)
4. Hola **eliminar datos de copia de seguridad** asistente, seleccione un motivo para eliminar datos de copia de seguridad (muy recomendados) y haga clic en **enviar**.

    ![Eliminación de datos de copia de seguridad](./media/backup-azure-manage-vms/delete-backup-data.png)
5. Esto creará una copia de seguridad de datos de toodelete de trabajo de máquina virtual seleccionada. Haga clic en **ver trabajo** toosee trabajo correspondiente en la página trabajos.

    ![Eliminación de datos correcta](./media/backup-azure-manage-vms/delete-data-success.png)

    Una vez que se complete el trabajo de hello, Hola entrada correspondiente máquina virtual de toohello se quitarán de **elementos protegidos** página.

## <a name="dashboard"></a>Panel
En hello **panel** página puede revisar información sobre máquinas virtuales de Azure, su almacenamiento y los trabajos asociados con ellos en hello últimas 24 horas. Puede ver el estado de copia de seguridad y los errores de copia de seguridad asociados.

![Panel](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Los valores en el panel de Hola se actualizan una vez cada 24 horas.
>
>

## <a name="auditing-operations"></a>Operaciones de auditoría
Copia de seguridad de Azure proporciona revisión de Hola "registros de operaciones" de las operaciones de copia de seguridad desencadenados por cliente hello toosee fácil exactamente qué operaciones de administración se realizaron en el almacén de copia de seguridad de Hola para convertirla. Registros de operaciones Habilitar evaluación excelente y compatibilidad para las operaciones de copia de seguridad de Hola de auditoría.

Hola las siguientes operaciones se registra en los registros de operaciones:

* Registro
* Unregister 
* Configuración de protección
* Copia de seguridad (tanto programada como a petición mediante BackupNow)
* Restauración
* Detener protección
* Eliminación de datos de copia de seguridad
* Add policy
* Eliminación de directiva
* Actualización de directiva
* Cancelar trabajo

los registros de operaciones de tooview almacén de copia de seguridad tooa correspondiente:

1. Navegue demasiado**servicios de administración de** en el portal de Azure y, a continuación, haga clic en hello **registros de operaciones** ficha.

    ![Registros de operaciones](./media/backup-azure-manage-vms/ops-logs.png)
2. En filtros de hello, seleccione **copia de seguridad** como *tipo* y especifique el nombre del almacén de copia de seguridad de hello en *nombre del servicio* y haga clic en **enviar**.

    ![Filtro de registros de operaciones](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. En los registros de operaciones de hello, seleccione cualquier operación y haga clic en **detalles** toosee detalles operación tooan correspondiente.

    ![Detalles de obtención de registros de operaciones](./media/backup-azure-manage-vms/ops-logs-details.png)

    Hola **Asistente detalles** contiene información sobre Hola operación de desencadena, Id., uso de recursos en el que se desencadena esta operación y hora de inicio de la operación de Hola de trabajo.

    ![Detalles de la operación](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>Notificaciones de alerta
Puede obtener las notificaciones de alerta personalizadas para los trabajos de hello en el portal. Esto se consigue mediante la definición de reglas de alerta basadas en PowerShell en los eventos de registros operativos. Se recomienda usar *PowerShell versión 1.3.0 o posterior*.

toodefine un tooalert de notificación personalizada para errores de copia de seguridad, un comando de ejemplo será similar:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: puede obtenerlo en la ventana emergente de registros de operaciones tal como se describe en la sección anterior. ResourceUri en ventana emergente de detalles de una operación es Hola ResourceId toobe proporcionado para este cmdlet.

**OperationName**: se trata del formato de Hola "Microsoft.Backup/backupvault/<EventName>" donde EventName es uno de registrar, anular el registro, ConfigureProtection, copia de seguridad, restauración, StopProtection, DeleteBackupData, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy

**Status**: los valores admitidos son: Started, Succeeded y Failed.

**ResourceGroup**: grupo de recursos del recurso de hello en el que se desencadena la operación. Puede obtenerlo del valor de ResourceId. Valor entre campos */ResourceGroups /* y */providers/* en ResourceId valor es el valor de hello para el grupo de recursos.

**Nombre**: nombre de regla de alerta de Hola.

**CustomEmail**: especificar toowhich de dirección de correo electrónico personalizada hello desea toosend notificación de alerta

**SendToServiceOwners**: esta opción envía los administradores de tooall de notificación de alertas y los coadministradores tienen permisos de suscripción de Hola. Se puede utilizar en el cmdlet **New-AzureRmAlertRuleEmail** .

### <a name="limitations-on-alerts"></a>Limitaciones de las alertas
Alertas basadas en eventos son sometido toohello siguientes limitaciones:

1. Las alertas se activan en todas las máquinas virtuales en el almacén de copia de seguridad Hola. No se puede personalizar tooget alertas para un conjunto específico de máquinas virtuales en un almacén de copia de seguridad.
2. Esta característica se encuentra en versión preliminar. [Más información](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Recibirá las alertas de alerts-noreply@mail.windowsazure.com. Actualmente no se puede modificar el remitente del correo electrónico de Hola.

## <a name="next-steps"></a>Pasos siguientes
* [Restauración de máquinas virtuales de Azure](backup-azure-restore-vms.md)
