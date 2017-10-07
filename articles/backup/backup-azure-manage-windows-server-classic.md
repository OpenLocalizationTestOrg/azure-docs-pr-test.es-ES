---
title: "almacenes de credenciales de copia de seguridad de Azure aaaManage y servidores Azure usando el modelo de implementación clásica de hello | Documentos de Microsoft"
description: "Use este tutorial toolearn cómo almacenes de credenciales toomanage copia de seguridad de Azure y los servidores."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Administrar servidores mediante el modelo de implementación clásica de Hola y almacenes de copia de seguridad de Azure
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Clásico](backup-azure-manage-windows-server-classic.md)
>
>

En este artículo encontrará información general sobre las tareas de administración de copia de seguridad de hello disponibles a través del portal de Azure clásico de Hola y el agente de copia de seguridad de Microsoft Azure Hola.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

> [!IMPORTANT]
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell. **El 1 de noviembre de 2017**:
>- Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

## <a name="management-portal-tasks"></a>Tareas del Portal de administración
1. Inicie sesión en toohello [Portal de administración](https://manage.windowsazure.com).
2. Haga clic en **servicios de recuperación**, a continuación, haga clic en nombre de Hola de página de inicio rápido de almacén de copia de seguridad tooview Hola.

    ![Servicios de recuperación](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Seleccionando las opciones de hello al principio de Hola de página de inicio rápido de hello, puede ver las tareas de administración disponibles Hola.

![Administración de pestañas](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>Panel
Seleccione **panel** información general del uso de Hola de toosee para servidor hello. Hola **información general del uso** incluye:

* número de Hola de servidores de Windows registrados toocloud
* número de Hello máquinas virtuales de Azure protegidas en la nube
* almacenamiento total Hola usado en Azure
* estado de Hola de trabajos recientes

Final de Hola de hello panel puede realizar Hola siguiente las tareas:

* **Administrar certificado** : si un certificado era tooregister usado Hola servidor, siga este certificado de hello tooupdate. Si usa credenciales de almacén, no utilice **Administrar certificado**.
* **Eliminar** -almacén de copia de seguridad actual de eliminaciones Hola. Si ya no se utiliza un almacén de copia de seguridad, puede eliminarla toofree liberar espacio de almacenamiento. **Eliminar** solo se habilita después de que todos los servidores registrados que se haya eliminado del almacén de Hola.

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Elementos registrados
Seleccione **elementos registrados** nombres de hello tooview de servidores de Hola que están registran toothis almacén.

![Elementos registrados](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Hola **tipo** tooAzure Máquina Virtual de valores predeterminados de filtro. nombres de hello tooview servidores Hola almacén toothis registrados, seleccione **Windows server** de hello menú desplegable.

Desde aquí puede realizar Hola siguientes tareas:

* **Permitir un nuevo registro** : cuando se selecciona esta opción para un servidor puede usar hello **Asistente para registro** en hello en copia de seguridad de Microsoft Azure agente tooregister Hola servidor local con el almacén de copia de seguridad de hello una segunda vez . Puede que tenga el registro toore debido a error de tooan en el certificado de Hola o si un servidor tuviera toobe vuelve a generar.
* **Eliminar** -elimina un servidor de almacén de copia de seguridad de Hola. Todos los datos de hello almacenado asociados con el servidor de Hola se elimina inmediatamente.

    ![Tareas de elementos registrados](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Elementos protegidos
Seleccione **elementos protegidos** elementos de hello tooview que hayan copias de seguridad de los servidores de Hola.

![Elementos protegidos](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Configuración
De hello **configurar** ficha puede seleccionar la opción de redundancia de almacenamiento adecuada de Hola. Hola mejor tiempo tooselect Hola almacenamiento redundancia opción es justo después de crear un almacén y antes de que todas las máquinas estén tooit registrado.

> [!WARNING]
> Una vez que un elemento se ha registrado toohello almacén, opción de redundancia de almacenamiento de hello está bloqueado y no se puede modificar.
>
>

![Configuración](./media/backup-azure-manage-windows-server-classic/configure.png)

Consulte este artículo para más información sobre la [redundancia de almacenamiento](../storage/common/storage-redundancy.md).

## <a name="microsoft-azure-backup-agent-tasks"></a>Tareas del agente de Copia de seguridad de Microsoft Azure
### <a name="console"></a>Consola
Abra hello **agente de copia de seguridad de Microsoft Azure** (puede encontrarlo buscando en el equipo para *copia de seguridad de Microsoft Azure*).

![Agente de copia de seguridad](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

De hello **acciones** disponible en hello derecha de la consola de agente de copia de seguridad de hello puede realizar Hola después de las tareas de administración:

* Registrar un servidor
* Programación de una copia de seguridad
* Realizar una copia de seguridad en ese momento
* Cambiar propiedades

![Acciones de la consola de agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> demasiado**recuperar datos**, consulte [restaurar archivos tooa Windows server o el equipo cliente de Windows](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Modificación de una copia de seguridad existente
1. En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. Hola **Asistente para la programación de copia de seguridad** deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.

    ![Modificación de una copia de seguridad programada](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Si desea tooadd o cambiar elementos en hello **seleccionar elementos tooBackup** pantalla haga clic en **agregar elementos**.

    También puede establecer **configuración de exclusión** desde esta página del Asistente para saludo. Si desea que los archivos tooexclude o tipos de archivo leen el procedimiento de Hola para agregar [configuración de exclusión](#exclusion-settings).
4. Seleccione Hola archivos y carpetas que desee tooback seguridad y haga clic en **bien**.

    ![Agregar elementos](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Especificar hello **programar copia de seguridad** y haga clic en **siguiente**.

    Puede programar copias de seguridad diarias (un máximo de 3 veces al día) o semanales.

    ![Especificación de la programación de copias de seguridad](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Especificar la programación de copia de seguridad de Hola se explica con detalle en esta [artículo](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Seleccione hello **directiva de retención** para copia de seguridad de Hola y haga clic en **siguiente**.

    ![Selección de la directiva de retención](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. En hello **confirmación** Hola revisar la información de la pantalla y haga clic en **finalizar**.
8. Una vez que el Asistente de hello finaliza la creación de hello **programar copia de seguridad**, haga clic en **cerrar**.

    Después de modificar la protección, puede confirmar que las copias de seguridad se activan correctamente por van toohello **trabajos** ficha y confirmar que los cambios se reflejan en hello trabajos de copia de seguridad.

### <a name="enable-network-throttling"></a>Habilitación de la limitación de la red
agente de copia de seguridad de Azure Hola incluye una pestaña de limitación que permite toocontrol uso de ancho de banda de red durante la transferencia de datos. Este control puede ser útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de internet. Limitación de datos transferencia aplica tooback seguridad y restaurar las actividades.  

tooenable limitación:

1. Hola **agente de copia de seguridad**, haga clic en **cambiar las propiedades de**.
2. Seleccione hello **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet** casilla de verificación.

    ![Limitación de la red](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. Una vez habilitada la limitación, especifique Hola permitido ancho de banda para transfirieron datos de copia de seguridad durante la **horas laborables** y **horas de descanso**.

    los valores de ancho de banda de Hello comienzan en 512 kilobytes por segundo (Kbps) y pueden crecer hasta too1023 megabytes por segundo (Mbps). También puede designar el inicio de Hola y de fin para **horas laborables**, y los días de la semana de Hola se consideran trabajo días. tiempo de Hello fuera Hola designado horas laborables es considerada toobe horas de descanso.
4. Haga clic en **Aceptar**.

## <a name="exclusion-settings"></a>Configuración de exclusión
1. Abra hello **agente de copia de seguridad de Microsoft Azure** (puede encontrarlo buscando en el equipo para *copia de seguridad de Microsoft Azure*).

    ![Apertura del agente de copia de seguridad](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. Hola Asistente para la programación de copia de seguridad deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.

    ![Modificación de una programación](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Haga clic en **Configuración de exclusión**.

    ![Selección de elementos tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Haga clic en **Agregar exclusión**.

    ![Adición de exclusiones](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Seleccionar ubicación de hello y, a continuación, haga clic en **Aceptar**.

    ![Selección de una ubicación para la exclusión](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Agregar extensión de archivo de Hola Hola **tipo de archivo** campo.

    ![Exclusión por tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    Adición de una extensión .mp3

    ![Ejemplo de tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd otra extensión, haga clic en **Agregar exclusión** y escriba otra extensión de tipo de archivo (agregar una extensión de JPEG).

    ![Otro ejemplo de tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. Cuando haya agregado todas las extensiones de hello, haga clic en **Aceptar**.
9. Continuar a través de hello Asistente para la programación de copia de seguridad haciendo clic en **siguiente** hasta hello **página de confirmación**, a continuación, haga clic en **finalizar**.

    ![Confirmación de exclusión](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Pasos siguientes
* [Restauración de Windows Server o el cliente de Windows desde Azure](backup-azure-restore-windows-server.md)
* toolearn más información acerca de la copia de seguridad de Azure, consulte [información general sobre la copia de seguridad de Azure](backup-introduction-to-azure-backup.md)
* Visite hello [foro de copia de seguridad de Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
