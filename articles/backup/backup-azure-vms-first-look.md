---
title: "Primer vistazo: copia de seguridad de máquinas virtuales de Azure con un almacén de copia de seguridad | Microsoft Docs"
description: "Utilice tooback portal clásico de hello el almacén de copia de seguridad de máquinas virtuales de Azure tooa. Este tutorial le explica todas las fases incluidas crear almacén de copia de seguridad de hello, registrar máquinas virtuales de hello, creación de directiva de copia de seguridad y ejecuta el trabajo de copia de seguridad inicial de Hola."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>Primer contacto: copia de seguridad de máquinas virtuales de Azure
> [!div class="op_single_selector"]
> * [Protección de máquinas virtuales con un almacén de Recovery Services](backup-azure-vms-first-look-arm.md)
> * [Protección de máquinas virtuales con un almacén de copia de seguridad](backup-azure-vms-first-look.md)
>
>

Este tutorial le guiará por los pasos de Hola para copia de seguridad de un almacén de copia de seguridad de máquina virtual (VM) Azure tooa en Azure. Este artículo describe el modelo clásico de Hola o modelo de implementación de Service Manager, para realizar copias de seguridad de las máquinas virtuales. Hello pasos siguientes aplican solo los almacenes de tooBackup creados en portal clásico de Hola. Microsoft recomienda utilizar el modelo de administrador de recursos de Hola para nuevas implementaciones.

Si está interesado en copia de seguridad de un almacén de servicios de recuperación de tooa VM que pertenezca tooa grupo de recursos, consulte [primer vistazo: proteger las máquinas virtuales con un almacén de servicios de recuperación](backup-azure-vms-first-look-arm.md).

toosuccessfully completar siguiente Hola tutorial, deben existir en estos requisitos previos:

* Ha creado una máquina virtual en su suscripción de Azure.
* Hola VM tiene direcciones IP públicas de conectividad tooAzure. Para más información, consulte [Conectividad de red](backup-azure-vms-prepare.md#network-connectivity).


> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este tutorial es para su uso con las máquinas virtuales creadas en portal clásico de Hola.
>
>

## <a name="create-a-backup-vault"></a>Creación de un almacén de copia de seguridad
Un almacén de copia de seguridad es una entidad que almacena todas las copias de seguridad de Hola y puntos de recuperación que se han creado con el tiempo. almacén de copia de seguridad de Hello también contiene las directivas de copia de seguridad de hello son máquinas virtuales de toohello aplicado haciendo copias de seguridad.

> [!IMPORTANT]
> A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.
> Puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell. **El 1 de noviembre de 2017**:
>- Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Detección y registro de máquinas virtuales de Azure
Antes de registrar Hola VM a un almacén, ejecute tooidentify de proceso de detección de hello las nuevas máquinas virtuales. Esto devuelve una lista de máquinas virtuales en la suscripción de hello, junto con información adicional como el nombre del servicio de nube de Hola y región Hola.

1. Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com/)
2. Hola portal de Azure clásico, haga clic en **servicios de recuperación** tooopen lista de Hola de almacenes de servicios de recuperación.
    ![Seleccionar carga de trabajo](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. En lista de Hola de almacenes de credenciales, seleccione hello tooback de almacén de una máquina virtual.

    Cuando se selecciona el almacén, se abre en hello **inicio rápido** página
4. En el menú de almacén de hello, haga clic en **elementos registrados**.

    ![Seleccionar carga de trabajo](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. De hello **tipo** menú, seleccione **Máquina Virtual de Azure**.

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
6. Haga clic en **DISCOVER** final Hola de página Hola.
    ![Botón Detectar](./media/backup-azure-vms/discover-button-only.png)

    proceso de detección de Hello puede tardar unos minutos mientras se se tabulan hello las máquinas virtuales. Hay una notificación en la parte inferior de Hola de pantalla de bienvenida que le permite saber que se está ejecutando el proceso de Hola.

    ![Detectar máquinas virtuales](./media/backup-azure-vms/discovering-vms.png)

    notificación de Hello cambia cuando se complete el proceso de Hola.

    ![Detección realizada](./media/backup-azure-vms-first-look/discovery-complete.png)
7. Haga clic en **registrar** final Hola de página Hola.
    ![Botón Registrar](./media/backup-azure-vms-first-look/register-icon.png)
8. Hola **registrar elementos** menú contextual, seleccione hello las máquinas virtuales que desea tooregister.

   > [!TIP]
   > Se pueden registrar varias máquinas virtuales al mismo tiempo.
   >
   >

    Se crea un trabajo para cada máquina virtual que ha seleccionado.
9. Haga clic en **ver trabajo** en hello notificación toogo toohello **trabajos** página.

    ![Registrar trabajo](./media/backup-azure-vms/register-create-job.png)

    máquina virtual de Hola también aparece en la lista de Hola de los elementos registrados, junto con el estado de Hola de operación de registro de hello.

    ![Registrando estado 1](./media/backup-azure-vms/register-status01.png)

    Cuando se completa la operación de hello, estado de hello cambia hello tooreflect *registrado* estado.

    ![Registrando estado 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar agente de máquina virtual de hello en la máquina virtual de Hola
Hello Azure VM Agent debe instalarse en la máquina virtual de Azure para toowork de extensión de copia de seguridad de Hola Hola. Si la máquina virtual se creó desde Hola Galería de Azure, Hola agente de máquina virtual ya está presente en hello VM; puede omitir demasiado[protege las máquinas virtuales](backup-azure-vms-first-look.md#create-the-backup-policy).

Si la máquina virtual se migra desde un centro de datos local, Hola VM probablemente no tiene Hola instalado el agente de máquina virtual. Debe instalar Hola agente de máquina virtual en la máquina virtual de hello antes de Hola de tooprotect continuar máquina virtual. Para obtener pasos detallados acerca de cómo instalar hello agente de máquina virtual, vea hello [sección de agente de máquina virtual de artículo de máquinas virtuales de copia de seguridad de hello](backup-azure-vms-prepare.md#vm-agent).

## <a name="create-hello-backup-policy"></a>Crear directiva de copia de seguridad de Hola
Antes de desencadenar el trabajo de copia de seguridad inicial de hello, establecer la programación de hello cuando se realizan las instantáneas de copia de seguridad. programación de Hello cuando se toman las instantáneas de copia de seguridad; Hola tiempo de esas instantáneas conservan, son directiva de copia de seguridad de Hola. información de retención de Hola se basa en el esquema de rotación de copia de seguridad de su Abuelo-padre-hijo.

1. Navegar por el almacén de copia de seguridad toohello en **servicios de recuperación** en Hola portal de Azure clásico y haga clic en **elementos registrados**.
2. Seleccione **Máquina Virtual de Azure** desde el menú desplegable de Hola.

    ![Seleccionar carga de trabajo en el portal](./media/backup-azure-vms/select-workload.png)
3. Haga clic en **proteger** final Hola de página Hola.
    ![Haga clic en Proteger](./media/backup-azure-vms-first-look/protect-icon.png)

    Hola **Asistente para proteger elementos** aparece y muestra *sólo* máquinas virtuales que están registradas y no protegidas.

    ![Configuración de protección a escala](./media/backup-azure-vms/protect-at-scale.png)
4. Seleccione hello las máquinas virtuales que desea tooprotect.

    Si hay dos o más máquinas virtuales con hello mismo nombre, use hello toodistinguish de servicio en la nube entre las máquinas virtuales Hola.
5. En hello **configurar la protección** menú Seleccione una directiva existente o cree una nueva tooprotect directiva máquinas virtuales de Hola que identificó.

    Nuevos almacenes de copia de seguridad tienen una directiva predeterminada asociada con el almacén de Hola. Esta directiva tiene un diario de instantáneas cada noche e instantánea diaria Hola se conserva durante 30 días. Cada directiva de copia de seguridad puede tener asociadas varias máquinas virtuales. Sin embargo, Hola máquina virtual puede estar solo asociado a una directiva a la vez.

    ![Protección mediante nueva directiva](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Una directiva de copia de seguridad incluye un esquema de retención de copias de seguridad programada de Hola. Si selecciona una directiva de copia de seguridad existente, será opciones de retención no se puede toomodify hello en el paso siguiente Hola.
   >
   >
6. En **duración de retención** definir Hola ámbito diaria, semanal, mensual y anual de puntos de copia de seguridad específicos de Hola.

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/long-term-retention.png)

    Directiva de retención especifica Hola período de tiempo para almacenar una copia de seguridad. Puede especificar las directivas de retención diferentes en función de cuando se realizó la copia de seguridad de Hola.
7. Haga clic en **trabajos** lista de hello tooview de **configurar la protección** trabajos.

    ![Configurar trabajo de protección](./media/backup-azure-vms/protect-configureprotection.png)

    Ahora que ha establecido la directiva de Hola, vaya toohello siguiente paso y ejecutar copia de seguridad inicial de Hola.

## <a name="initial-backup"></a>Copia de seguridad inicial
Una vez que una máquina virtual se ha protegido con una directiva, puede ver esa relación en hello **elementos protegidos** ficha. Hasta que la copia de seguridad inicial de Hola se produce, hello **el estado de protección** se muestra como **Protected - (pendiente de copia de seguridad inicial)**. De forma predeterminada, copia de seguridad programada Hola primer es hello *copia de seguridad inicial*.

![Copia de seguridad pendiente](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart Hola copia de seguridad inicial ahora:

1. En hello **elementos protegidos** página, haga clic en **copia de seguridad ahora** final Hola de página Hola.
    ![Icono Realizar copia de seguridad ahora](./media/backup-azure-vms-first-look/backup-now-icon.png)

    Hola servicio copia de seguridad de Azure crea un trabajo de copia de seguridad para la operación de copia de seguridad inicial de Hola.
2. Haga clic en hello **trabajos** lista de pestañas tooview Hola de trabajos.

    ![Copia de seguridad en curso](./media/backup-azure-vms-first-look/protect-inprogress.png)

    Cuando la copia de seguridad inicial está completa, el estado de Hola de máquina virtual de Hola Hola **elementos protegidos** ficha es *Protected*.

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > La copia de seguridad de máquinas virtuales es un proceso local. No puede hacer copia de seguridad de máquinas virtuales desde un almacén de copia de seguridad de tooa región en otra región. Por lo tanto, para cada región de Azure que tiene máquinas virtuales que necesitan toobe copia de seguridad, al menos un almacén de copia de seguridad debe crearse en dicha región.
   >
   >

## <a name="next-steps"></a>Pasos siguientes
Una vez que se ha copiado correctamente una máquina virtual, hay varios pasos que pueden ser de interés. paso más lógica Hello es toofamiliarize usted mismo con la restauración de datos tooa máquina virtual. Sin embargo, hay tareas de administración que le ayudará a entender cómo tookeep los datos seguros y minimizar los costes.

* [Administración y supervisión de las máquinas virtuales](backup-azure-manage-vms.md)
* [Restauración de máquinas virtuales](backup-azure-restore-vms.md)
* [Guía de solución de problemas](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).
