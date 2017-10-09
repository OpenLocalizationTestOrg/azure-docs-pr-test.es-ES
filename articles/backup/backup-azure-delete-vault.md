---
title: " Eliminación de un almacén de Recovery Services en Azure | Microsoft Docs "
description: "¿Cómo toodelete una copia de seguridad de Azure y servicios de recuperación del almacén. A un almacén de Backup también se le puede denominar almacén en la nube de Azure o almacén de recuperación de Azure. Solución de problemas cuando no se puede eliminar un almacén de copia de seguridad en el portal clásico de Hola o portal de Azure."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Eliminación de un almacén de Recovery Services
Hola servicio de copia de seguridad de Azure tiene dos tipos de almacenes: almacén de copia de seguridad de Hola y Hola el almacén de servicios de recuperación. almacén de copia de seguridad de Hello aparece primero. A continuación, Hola del almacén de servicios de recuperación suministrada a lo largo de las implementaciones de administrador de recursos de toosupport Hola expandido. Dada Hola capacidades ampliadas y dependencias de la información de Hola que deben almacenarse en el almacén de hello, eliminar un almacén de copia de seguridad o los servicios de recuperación pueden resultar confusas. Este artículo explica cómo hello toodelete los almacenes de credenciales en el portal clásico de Hola y Hola portal de Azure.  

| **Tipo de implementación** | **Portal** | **Nombre del almacén** |
| --- | --- | --- |
| Clásico |Clásico |Almacén de copia de seguridad |
| Resource Manager |Las tablas de Azure |Almacén de Servicios de recuperación |

> [!NOTE]
> Los almacenes de copia de seguridad no pueden proteger soluciones implementadas con Resource Manager. Sin embargo, puede usar un almacén de servicios de recuperación tooprotect tradicionalmente implementar servidores y las máquinas virtuales.  
>

> [!IMPORTANT]
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> **15 de octubre de 2017**, ya no estará almacenes de copia de seguridad de toocreate de toouse capaz de PowerShell. <br/> **A partir del 1 de noviembre de 2017**:
>- Los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

En este artículo, usamos el término de hello, almacén, toorefer toohello formulario genérico del almacén de copia de seguridad de Hola o almacén de servicios de recuperación. Utilizamos nombre formal de hello, el almacén de copia de seguridad o el almacén de servicios de recuperación, cuando sea necesario toodistinguish entre almacenes de Hola.

## <a name="deleting-a-recovery-services-vault"></a>Eliminación de un almacén de Recovery Services
Eliminar un almacén de servicios de recuperación es un proceso de un solo paso - *proporcionado por el almacén de hello no contiene ningún recurso*. Antes de poder eliminar un almacén de servicios de recuperación, debe quitar o eliminar todos los recursos en el almacén de Hola. Si intentas toodelete un almacén que contiene los recursos, obtendrá un error como Hola después de imagen:

![Error de eliminación del almacén](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Hasta que haya borrado recursos Hola del almacén de hello, haga clic en **vuelva a intentar** produce Hola mismo error. Si está atascada en este mensaje de error, haga clic en **cancelar** y use Hola siguientes pasos le indican toodelete recursos de hello en el almacén de Hola.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>Quitar elementos de Hola de un almacén de protección de una máquina virtual
Si ya tiene servicios de recuperación de hello Abrir almacén, continúe toohello segundo paso.

1. Abra Hola portal de Azure y de hello panel almacén Hola desea toodelete.

   Si no tienes Hola del almacén de servicios de recuperación anclado toohello panel, en el menú del concentrador de hello, haga clic en **más servicios** y en la lista de Hola de recursos, escriba **servicios de recuperación**. Cuando empiece a escribir, Hola filtros de la lista con los datos especificados. Haga clic en **Almacenes de Servicios de recuperación**.

   ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   se muestra la lista de Hola de almacenes de servicios de recuperación. En lista de hello, seleccione almacén Hola desea toodelete.

   ![elegir el almacén en la lista](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. Hola del almacén de vista, busque en hello **Essentials** panel. toodelete un almacén, no puede haber ningún elemento protegido. Si aparece un número distinto de cero, bajo **elementos de copia de seguridad** o **servidores de administración de copia de seguridad**, debe quitar los elementos antes de poder eliminar el almacén de Hola.

    ![Consulta de los elementos protegidos en el panel Essentials](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    Las máquinas virtuales y archivos o carpetas se consideran elementos de copia de seguridad y se muestran en hello **elementos de copia de seguridad** área del panel de Essentials Hola. Un servidor DPM se muestra en hello **servidor de administración de copia de seguridad** área del panel de Essentials Hola. **Elementos de replicación** pertenecen toohello servicio Azure Site Recovery.
3. toobegin quitar Hola elementos protegidos del almacén de hello, buscar elementos de hello en el almacén de Hola. En el panel del almacén de hello, haga clic en **configuración**y, a continuación, haga clic en **elementos de copia de seguridad** tooopen esa hoja.

    ![elegir el almacén en la lista](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    Hola **elementos de copia de seguridad** hoja tiene listas independientes, en función de tipo de elemento de Hola: máquinas virtuales de Azure o carpetas de archivos (consulte la imagen). lista de tipo de elemento de Hola predeterminado que se muestra es máquinas virtuales de Azure. lista de hello tooview de elementos de carpetas de archivos en el almacén de hello, seleccione **carpetas de archivos** desde el menú desplegable de Hola.
4. Antes de poder eliminar un elemento del almacén de hello proteger una máquina virtual, debe detener el trabajo de copia de seguridad del elemento de Hola y eliminar datos de punto de recuperación de saludo. Para cada elemento en el almacén de hello, siga estos pasos:

    a. En hello **elementos de copia de seguridad** hoja, contextual hello y desde el menú contextual de hello, seleccione **Detener copia de seguridad**.

    ![detener el trabajo de copia de seguridad de Hola](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    se abre la hoja de Hello Detener copia de seguridad.

    b. En hello **Detener copia de seguridad** hoja de hello **elegir una opción** menú, seleccione **eliminar datos de copia de seguridad** > Hola nombre de tipo hello elemento > y haga clic en **detener copia de seguridad**.

    Nombre de Hola de tipo del elemento de hello, tooverify desea toodelete de él. Hola **Detener copia de seguridad** botón activa una vez verificado elemento Hola. Si no ve Hola diálogo cuadro tootype Hola nombre de elemento de copia de seguridad de hello, eligió hello **conservar datos de copia de seguridad** opción.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    Si lo desea, puede proporcionar una razón para que va a eliminar datos de hello y agrega comentarios. Tras hacer clic en **Detener copia de seguridad**, permitir Hola Eliminar trabajo toocomplete antes de intentar el almacén de hello toodelete. tooverify que Hola trabajo ha completado, compruebe los mensajes de Hola Azure ![eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/messages.png). <br/>
    Una vez completado el trabajo de hello, recibirá un mensaje que indica que se ha detenido el proceso de copia de seguridad de Hola y se han eliminado los datos de copia de seguridad de hello, para ese elemento.

    c. Después de eliminar un elemento de lista de hello, en hello **elementos de copia de seguridad** menú, haga clic en **actualizar** hello toosee restantes elementos en el almacén de Hola.

      ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/empty-items-list.png)

      Cuando no hay elementos en la lista de hello, desplácese toohello **Essentials** panel en la hoja de almacén de copia de seguridad de Hola. No debería haber **elementos de copia de seguridad**, **servidores de administración de copias de seguridad** ni **elementos replicados** en la lista. Si siguen aparecen elementos en el almacén de hello, devolver toostep tres y elija una lista de tipo de elemento diferente.  
5. Cuando no hay más elementos en la barra de herramientas de hello almacén, haga clic en **eliminar**.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/delete-vault.png)
6. Haga clic en tooverify que desea que el almacén de hello toodelete, **Sí**.

    se elimina el almacén de Hola y portal de hello devuelve toohello **New** menú de servicio.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>¿Qué ocurre si detiene el proceso de copia de seguridad de hello pero se conservan datos Hola?
Si detiene el proceso de copia de seguridad de hello pero accidentalmente *conservan* datos hello, debe eliminar datos de copia de seguridad de hello antes de poder eliminar el almacén de Hola. datos de copia de seguridad de Hola toodelete:

1. En hello **elementos de copia de seguridad** hoja, contextual hello y en el menú contextual de hello haga clic en **eliminar datos de copia de seguridad**.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    Hola **eliminar datos de copia de seguridad** abre la hoja.
2. En hello **eliminar datos de copia de seguridad** hoja, escriba un nombre Hola de elemento de Hola y haga clic en **eliminar**.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Una vez haya eliminado los datos de hello, devolver toostep 4c y continúe con el proceso de Hola.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>Eliminar un tooprotect almacén usa un servidor DPM
Antes de poder eliminar un tooprotect almacén usa un servidor DPM, debe borrar puntos de recuperación que se han creado y, a continuación, anular el registro del servidor de Hola de almacén de Hola.

datos de hello toodelete asociadas a un grupo de protección:

1. Hola consola de administrador DPM, haga clic en **protección** > seleccione un grupo de protección > seleccione Hola miembro del grupo de protección > y haga clic en la cinta de opciones de herramienta de hello, **quitar**.

  Hola de hello seleccione miembro del grupo de protección tooactivate **quitar** botón en la cinta de opciones de herramienta de Hola. En el ejemplo de Hola, es miembro de hello **dummyvm9**. tooselect varios miembros de grupo de protección de hello, mantenga presionada la tecla Ctrl de hello mientras hace clic en los miembros de Hola.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    Hola **detener protección** abre el cuadro de diálogo.
2. Hola **detener protección** cuadro de diálogo, seleccione **eliminar datos protegidos**y haga clic en **detener protección**.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete un almacén, debe borrar o eliminar, el almacén de Hola de los datos protegidos. Según el número de Hola de puntos de recuperación y los datos en el grupo de protección de hello, puede tardar en cualquier lugar de datos hello tooseveral minutos toodelete de unos segundos. Hola **detener protección** cuadro de diálogo muestra el estado de hello cuando se haya completado el trabajo de Hola.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. Repita este proceso para todos los miembros de todos los grupos de protección.

    Elimine todos los datos protegidos y grupos de protección.
4. Después de eliminar a todos los miembros del grupo de protección de hello, cambie toohello portal de Azure. Abra Panel de almacén de Hola y asegúrese de que no hay ningún **elementos de copia de seguridad**, **servidores de administración de copia de seguridad**, o **replican elementos**. En la barra de herramientas de almacén de hello, haga clic en **eliminar**.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/delete-vault.png)

    Si no hay servidores registrados toohello almacén de copia de seguridad administración, no se puede eliminar el almacén de hello incluso si no hay ningún dato en el almacén de Hola. Si se eliminan servidores de administración de copia de seguridad de hello asociados con el almacén de hello, pero hay servidores que se enumeran en hello **Essentials** panel, consulte [el almacén de credenciales de búsqueda Hola Backup administración servidores registrados toohello](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. Haga clic en tooverify que desea que el almacén de hello toodelete, **Sí**.

    se elimina el almacén de Hola y portal de hello devuelve toohello **New** menú de servicio.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>Eliminar un tooprotect almacén usa un servidor de producción
Antes de poder eliminar un tooprotect almacén usa un servidor de producción, debe eliminar o anular el registro del servidor de Hola de almacén de Hola.

servidor de producción de hello de toodelete asociada con el almacén de hello:

1. Hola portal de Azure, abra Panel de almacén de Hola y haga clic en **configuración** > **infraestructura de copia de seguridad** > **servidores de producción**.

    ![abrir la hoja Servidores de producción](./media/backup-azure-delete-vault/delete-production-server.png)

    Hola **servidores de producción** hoja se abre y muestra todos los servidores de producción en el almacén de Hola.

    ![lista de servidores de producción](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. En hello **servidores de producción** hoja, haga doble clic en el servidor de Hola y haga clic en **eliminar**.

    ![eliminar servidor de producción ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    Hola **eliminar** abre la hoja.

    ![eliminar servidor de producción ](./media/backup-azure-delete-vault/delete-blade.png)
3. En hello **eliminar** hoja, confirme el nombre del servidor de Hola y haga clic en **eliminar**. Correctamente debe asignar un nombre servidor hello, hello tooactivate **eliminar** botón.

    Una vez que se elimina el almacén de hello, recibirá un mensaje que indica que se ha eliminado el almacén de Hola. Después de eliminar todos los servidores en el almacén de hello, desplácese toohello back-panel de Essentials en el panel del almacén de Hola.
4. En el panel de almacén de hello, asegúrese de que no hay ningún **elementos de copia de seguridad**, **servidores de administración de copia de seguridad**, o **replican elementos**. En la barra de herramientas de almacén de hello, haga clic en **eliminar**.
5. Haga clic en tooverify que desea que el almacén de hello toodelete, **Sí**.

    se elimina el almacén de Hola y portal de hello devuelve toohello **New** menú de servicio.

## <a name="delete-a-backup-vault-in-classic-portal"></a>Eliminación de un almacén de Backup en el Portal de Azure clásico
Hello instrucciones siguientes sirven para eliminar un almacén de copia de seguridad en el portal clásico de Hola. Antes de poder eliminar el almacén de copia de seguridad de hello, debe eliminar los puntos de recuperación de hello, o la copia de seguridad de elementos y quitar servidores registrado de Hola. Hello servidores registrados son Hola Windows Server, estación de trabajo o máquinas virtuales que había registrado toohello almacén.

1. Abra hello [portal clásico](https://manage.windowsazure.com).

2. En lista de Hola de almacenes de copia de seguridad, seleccione almacén Hola desea toodelete.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    se abrirá el panel de almacén de Hola. Busque Hola número de servidores de Windows o Azure máquinas virtuales asociada con el almacén de Hola. Además, mirar almacenamiento total Hola usado en Azure. Detenga todos los trabajos de copia de seguridad y elimine todos los datos antes de eliminar el almacén de Hola.

3. Haga clic en hello **elementos protegidos** ficha y, a continuación, haga clic en **detener la protección**

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    Hola **detener la protección de "el almacén"** aparece el cuadro de diálogo.
4. Hola **detener la protección de "el almacén"** cuadro de diálogo, verificación **eliminar los datos de copia de seguridad asociados** y haga clic en ![marca de verificación](./media/backup-azure-delete-vault/checkmark.png). <br/>
    Si lo desea, puede elegir un motivo para detener la protección y proporcionar un comentario.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Después de eliminar elementos de hello en el almacén de hello, almacén de hello estará vacío.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. En la lista de Hola de pestañas, haga clic en **elementos registrados**. Hola **tipo** menú desplegable, permite toochoose Hola escriba del almacén de credenciales de servidor registrado toohello. Hola tipo puede ser Windows Server o la máquina Virtual de Azure. En el siguiente ejemplo de Hola, seleccione almacén toohello registrados de hello máquina virtual y haga clic en **Unregister**.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Si desea que el registro de hello toodelete para un servidor de Windows, de hello **tipo** menú desplegable, seleccione **Windows Server**, haga clic en ![marca de verificación](./media/backup-azure-delete-vault/checkmark.png) toorefresh pantalla de bienvenida, y, a continuación, haga clic en **eliminar**. <br/>

  ![Seleccionar Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. En la lista de Hola de pestañas, haga clic en **panel** tooopen que pestaña. Compruebe que no haya máquinas virtuales de Azure protegidas en la nube de hello ni los servidores registrados. Compruebe también que no hay ningún dato en el almacenamiento. Haga clic en **eliminar** toodelete el almacén de Hola.

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    se abre la pantalla de confirmación de almacén de Hello Eliminar copia de seguridad. Seleccione una opción de por qué se dispone a eliminar el almacén de Hola y haga clic en ![marca de verificación](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![Eliminar datos de copia de seguridad](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    se elimina el almacén de Hola y devolver toohello panel del portal clásico.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>Busque el almacén de toohello registrados de servidores de administración de copia de seguridad Hola
Si tiene varios servidores registrados tooa almacén, puede ser difícil tooremember ellos. servidores de hello toosee registrado toohello almacén y eliminar:

1. Panel de almacén de hello abierto.
2. Hola **Essentials** panel, haga clic en **configuración** tooopen esa hoja.

    ![abrir hoja Configuración](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. En hello **hoja de configuración de**, haga clic en **infraestructura de copia de seguridad**.
4. En hello **infraestructura de copia de seguridad** hoja, haga clic en **servidores de administración de copia de seguridad**. se abre la hoja de servidores de administración de copia de seguridad de Hola.

    ![lista Servidores de administración de copias de seguridad](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete un servidor de la lista de hello, haga clic en nombre de saludo del servidor de hello y, a continuación, haga clic en **eliminar**.
    Hola **eliminar** abre la hoja.
6. En hello **eliminar** hoja, proporcione Hola nombre del servidor de Hola. Si es un nombre largo, puede copiar y pegar desde lista Hola de servidores de administración de copia de seguridad. Después, haga clic en **Eliminar**.  
