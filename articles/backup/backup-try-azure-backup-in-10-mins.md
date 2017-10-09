---
title: aaaBack la tooAzure de archivos y carpetas de Windows (Administrador de recursos) | Documentos de Microsoft
description: "Obtenga información acerca de tooback una tooAzure de archivos y carpetas de Windows en una implementación de administrador de recursos."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "¿Cómo toobackup; ¿Cómo tooback; las carpetas y archivos de copia de seguridad"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a>Primer análisis: Copia de seguridad de archivos y carpetas en la implementación de Resource Manager
Este artículo se explica cómo tooback su servidor de Windows (o equipo de Windows) tooAzure de archivos y carpetas mediante una implementación del Administrador de recursos. Es un tutorial toowalk previsto le guían a través de los conceptos básicos de Hola. Si desea tooget iniciado mediante copia de seguridad de Azure, está en un lugar incorrecto Hola.

Si desea más información acerca de la copia de seguridad de Azure tooknow, lea esta [Introducción](backup-introduction-to-azure-backup.md).

Si no tiene una suscripción de Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) que le permita acceder a todos los servicios de Azure.

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Servicios de recuperación
tooback seguridad de archivos y carpetas, deberá toocreate un almacén de servicios de recuperación de la región de Hola donde desea toostore Hola datos. También debe toodetermine cómo desea que su almacenamiento replicado.

### <a name="toocreate-a-recovery-services-vault"></a>toocreate un almacén de servicios de recuperación
1. Si aún no lo ha hecho, inicie sesión en toohello [Portal de Azure](https://portal.azure.com/) con su suscripción de Azure.
2. En el menú del concentrador hello, haga clic en **más servicios** y en la lista de Hola de recursos, escriba **servicios de recuperación** y haga clic en **servicios de recuperación de los almacenes de credenciales**.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Si no hay almacenes de servicios de recuperación de la suscripción de hello, se enumeran los almacenes de Hola.
3. En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo. nombre de Hello debe toobe único para hello suscripción de Azure. Escriba un nombre que tenga entre 2 y 50 caracteres. Debe comenzar por una letra y solo puede contener letras, números y guiones.

5. Hola **suscripción** sección, usar Hola menú desplegable toochoose hello suscripción de Azure. Si usa una sola suscripción, que aparece de la suscripción y puede omitir el paso siguiente toohello. Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción. Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.

6. Hola **grupo de recursos** sección:

    * Seleccione **crear nuevo** si desea que toocreate un nuevo grupo de recursos.
    O
    * Seleccione **utilizar existente** y haga clic en hello menú desplegable toosee Hola disponible lista de grupos de recursos.

  Para obtener información completa sobre los grupos de recursos, vea hello [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola. Esta opción determina dónde se envían los datos de copia de seguridad de región geográfica Hola.

8. En la parte inferior de Hola de hoja de almacén de servicios de recuperación de hello, haga clic en **crear**.

    Puede tardar varios minutos para hello que toobe creado del almacén de servicios de recuperación. Supervisar las notificaciones de estado de hello en el área superior derecha de hello del portal de Hola. Una vez creado el almacén, aparece en la lista de Hola de almacenes de servicios de recuperación. Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).

    ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Una vez que vea el almacén en la lista de Hola de almacenes de servicios de recuperación, son redundancia de almacenamiento de hello tooset listo.

### <a name="set-storage-redundancy-for-hello-vault"></a>Establecer la redundancia de almacenamiento para el almacén de Hola
Cuando se crea un almacén de servicios de recuperación, asegúrese de redundancia de almacenamiento está configurado Hola que quieras.

1. De hello **servicios de recuperación de los almacenes de credenciales** hoja, haga clic en nuevo almacén de Hola.

    ![Seleccione el nuevo almacén de Hola de lista de Hola de almacén de servicios de recuperación](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Cuando se selecciona el almacén de hello, Hola **del almacén de servicios de recuperación** permite delimitar hoja y hoja de configuración de hello (*que tiene el nombre de Hola de almacén de hello en la parte superior de hello*) y hoja de detalles de almacén de hello abierto.

    ![Configuración de almacenamiento de vista Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. En la hoja de configuración del nuevo almacén de hello, hello tooscroll de desplazamiento vertical hacia abajo toohello sección administrar y haga clic en **infraestructura de copia de seguridad**.
    se abre la hoja de la infraestructura de copia de seguridad de Hola.
3. En la hoja de la infraestructura de copia de seguridad de hello, haga clic en **configuración de copia de seguridad** tooopen hello **configuración de copia de seguridad** hoja.

    ![Establecer configuración de almacenamiento de Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Elija la opción de replicación de almacenamiento apropiada de hello para el almacén.

    ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica. Si utiliza Azure como un punto de conexión de almacenamiento principal de copia de seguridad, continúe toouse **con redundancia geográfica**. Si no utiliza Azure como un punto de conexión de almacenamiento de copia de seguridad principal, a continuación, elija **localmente redundante**, lo que reduce los costos de almacenamiento de Azure de Hola. En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).

Ahora que ha creado un almacén, configúrelo para realizar copias de seguridad de archivos y carpetas.

## <a name="configure-hello-vault"></a>Configurar el almacén de Hola
1. Hola hoja de almacén de servicios de recuperación (hello para el almacén de que acaba de crear), en la sección de introducción de hello en, haga clic en **copia de seguridad**, a continuación, en hello **Introducción a la copia de seguridad** hoja, seleccione  **Objetivo de copia de seguridad**.

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Hola **objetivo de copia de seguridad** abre la hoja.

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. De hello **donde se está ejecutando la carga de trabajo?** menú desplegable, seleccione **local**.

    Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.

3. De hello **especifique qué desea toobackup?** menú, seleccione **archivos y carpetas**y haga clic en **Aceptar**.

    ![Configuración de archivos y carpetas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    Después de hacer clic en Aceptar, aparece una marca siguiente demasiado**objetivo de copia de seguridad**, hello y **preparar infraestructura** abre la hoja.

    ![Objetivo de copia de seguridad configurado, a continuación, prepare la infraestructura](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. En hello **preparar infraestructura** hoja, haga clic en **descargar agente para Windows Server o cliente de Windows**.

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    Si usa Windows Server esencial, a continuación, elija a agente de hello toodownload para Windows Server esenciales. Un menú emergente le pide que toorun o guardar MARSAgentInstaller.exe.

    ![Cuadro de diálogo de MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. En el menú emergente de descarga de hello, haga clic en **guardar**.

    De forma predeterminada, Hola **MARSagentinstaller.exe** archivo se guarda la carpeta de descargas de tooyour. Cuando se completa el instalador de hello, verá una ventana emergente que pregunta si desea que el instalador de toorun hello, o Abrir carpeta Hola.

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    No es necesario a tooinstall agente de hello todavía. Puede instalar a agente de hello después de haber descargado las credenciales de almacén de Hola.

6. En hello **preparar infraestructura** hoja, haga clic en **descargar**.

    ![descargar las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    carpeta de descargas de tooyour de descarga de las credenciales de almacén de Hola. Después de que las credenciales de almacén de hello termine la descarga, verá una ventana emergente que pregunta si desea tooopen o guardar las credenciales de Hola. Haga clic en **Guardar**. Si hace clic en accidentalmente **abiertos**, permitir que el cuadro de diálogo de Hola que trata las credenciales de almacén de hello tooopen, producirá un error. No se puede abrir las credenciales de almacén de Hola. Continúe toohello siguiente paso. las credenciales de almacén de Hola están en la carpeta de descargas de Hola.   

    ![finalizó la descarga de las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>Instalar y registrar el agente de Hola

> [!NOTE]
> Habilitar copia de seguridad a través del portal de Azure Hola todavía no está disponible. Utilice tooback de agente de servicios de recuperación de Microsoft Azure Hola seguridad de archivos y carpetas.
>

1. Busque y haga doble clic en hello **MARSagentinstaller.exe** desde la carpeta de descargas de hello (u otra ubicación de almacenamiento).

    instalador de Hello proporciona una serie de mensajes cuando extrae, instala y registra el agente de servicios de recuperación de Hola.

    ![ejecutar las credenciales del instalador del agente de Recovery Services](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Asistente para la instalación de Microsoft Azure Recovery Services agente de hello completa. Asistente de hello toocomplete, debe:

   * Elegir una ubicación para la carpeta de instalación y de caché de Hola.
   * Proporcionar la proxy información al servidor si usa un toohello de tooconnect de servidor proxy internet.
   * Si usa un servidor proxy autenticado, escriba los detalles de nombre y contraseña del usuario.
   * Proporcione las credenciales de almacén de hello descargado
   * Guarde la frase de contraseña de cifrado de hello en una ubicación segura.

     > [!NOTE]
     > Si pierde u olvida la frase de contraseña de hello, Microsoft no puede ayudar a recuperar datos de copia de seguridad de saludo. Guarde el archivo hello en una ubicación segura. Es necesario toorestore una copia de seguridad.
     >
     >

Ahora está instalado el agente de Hola y su equipo es el almacén de toohello registrados. Está listo tooconfigure y programar la copia de seguridad.

## <a name="network-and-connectivity-requirements"></a>Requisitos de conectividad y de red

Si el máquina/proxy ha limitado el acceso a internet, asegúrese de que la configuración de firewall en hello mcahine/proxy es hello tooallow configurado las siguientes direcciones URL: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne

## <a name="back-up-your-files-and-folders"></a>Realización de copias de seguridad de archivos y carpetas.
copia de seguridad inicial de Hello incluye dos tareas fundamentales:

* Programar copias de seguridad de Hola
* Realizar una copia de archivos y carpetas de hello primera vez

toocomplete Hola copia de seguridad inicial, agente de servicios de recuperación de Microsoft Azure Hola de uso.

### <a name="tooschedule-hello-backup-job"></a>trabajo de copia de seguridad de hello tooschedule
1. Abra el agente de servicios de recuperación de Microsoft Azure de Hola. Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.

    ![Iniciar el agente de servicios de recuperación de Azure de Hola](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. En el agente de servicios de recuperación de hello, haga clic en **programar copias de seguridad**.

    ![Programación de una copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. En hello Introducción a la página de hello Asistente para la programación de copia de seguridad, haga clic en **siguiente**.
4. En la página de tooBackup de seleccionar elementos de hello, haga clic en **agregar elementos**.
5. Seleccionar archivos de Hola y las carpetas que desea tooback seguridad y, a continuación, haga clic en **bien**.
6. Haga clic en **Siguiente**.
7. En hello **especificar una programación de copia de seguridad** página, especifique hello **programar copia de seguridad** y haga clic en **siguiente**.

    Puede programar copias de seguridad diarias (con una frecuencia máxima de tres veces al día) o semanales.

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > Para obtener más información acerca de cómo toospecify Hola programar copia de seguridad, vea el artículo de hello [tooreplace utilice Azure Backup su infraestructura de cinta](backup-azure-backup-cloud-as-tape.md).
   >

8. En hello **Seleccionar directiva de retención** página, seleccione hello **directiva de retención** para copia de seguridad de Hola.

    Directiva de retención de Hello especifica cuánto tiempo se almacenan los datos de copia de seguridad de saludo. En vez de especificar una "directiva" para todos los puntos de copia de seguridad, puede especificar las directivas de retención diferente en función de cuando se produce la copia de seguridad de Hola. Puede modificar toomeet de directivas de retención diaria, semanal, mensual y anual de hello sus necesidades.
9. En la página Elegir tipo de copia de seguridad inicial de hello, elija el tipo de copia de seguridad inicial de Hola. Deje la opción de hello **automáticamente a través de la red de hello** seleccionada y, a continuación, haga clic en **siguiente**.

    Hacer copias de seguridad automáticamente a través de red de hello, o puede realizar una copia sin conexión. resto de Hola de este artículo describe proceso Hola para realizar copias de seguridad automáticamente. Si lo prefiere toodo una copia de seguridad sin conexión, revise el artículo de hello [flujo de trabajo de copia de seguridad sin conexión en copia de seguridad de Azure](backup-azure-backup-import-export.md) para obtener información adicional.
10. En la página de confirmación de hello, revise la información de hello y, a continuación, haga clic en **finalizar**.
11. Cuando finalice el Asistente de hello, crear la programación de copia de seguridad de hello, haga clic en **cerrar**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback seguridad de archivos y carpetas para hello primera vez
1. En el agente de servicios de recuperación de hello, haga clic en **Back Up Now** toocomplete Hola inicial de la propagación a través de red de Hola.

    ![Copia de seguridad de Windows Server ahora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. En la página de confirmación de hello, revise la configuración Hola que Hola a ahora Asistente de Back Up usará tooback máquina Hola. Luego, haga clic en **Crear copia de seguridad**.
3. Haga clic en **cerrar** Asistente de hello tooclose. Si cierra al Asistente de hello antes de que finalice el proceso de copia de seguridad de hello, Asistente Hola continúa toorun en segundo plano de Hola.

Una vez completada la copia de seguridad inicial de hello, Hola **ha completado el trabajo** estado aparece en la consola de copia de seguridad de Hola.

![IR completado](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de cómo [realizar copias de seguridad de máquinas Windows](backup-configure-vault.md).
* Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).
* Si necesita toorestore una copia de seguridad, use este artículo demasiado[restaurar archivos tooa Windows máquina](backup-azure-restore-windows-server.md).
