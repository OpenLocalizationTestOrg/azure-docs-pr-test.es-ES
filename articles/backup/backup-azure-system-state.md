---
title: aaaBack una tooAzure de estado de sistema de Windows | Documentos de Microsoft
description: "Obtenga información acerca de tooback el estado de sistema de Hola de Windows Server o tooAzure de equipos de Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "¿Cómo toobackup; ¿Cómo tooback; las carpetas y archivos de copia de seguridad"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Copias de seguridad del estado del sistema de Windows en la implementación de Resource Manager
Este artículo explica cómo tooback el sistema de Windows Server estado tooAzure. Es un tutorial toowalk previsto le guían a través de los conceptos básicos de Hola.

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

    * Seleccione **crear nuevo** si desea que toocreate un grupo de recursos.
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

Ahora que ha creado un almacén, configúrelo para realizar copias de seguridad del estado del sistema de Windows.

## <a name="configure-hello-vault"></a>Configurar el almacén de Hola
1. Hola hoja de almacén de servicios de recuperación (hello para el almacén de que acaba de crear), en la sección de introducción de hello en, haga clic en **copia de seguridad**, a continuación, en hello **Introducción a la copia de seguridad** hoja, seleccione  **Objetivo de copia de seguridad**.

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Hola **objetivo de copia de seguridad** abre la hoja.

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. De hello **donde se está ejecutando la carga de trabajo?** menú desplegable, seleccione **local**.

    Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.

3. De hello **especifique qué desea toobackup?** menú, seleccione **estado del sistema**y haga clic en **Aceptar**.

    ![Configuración de archivos y carpetas](./media/backup-azure-system-state/backup-goal-system-state.png)

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
> Habilitar copia de seguridad a través del portal de Azure Hola todavía no está disponible. Utilice tooback de agente de servicios de recuperación de Microsoft Azure Hola el estado de sistema de Windows Server.
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

## <a name="back-up-windows-server-system-state-preview"></a>Copia de seguridad del estado del sistema de Windows Server (versión preliminar)
copia de seguridad inicial de Hello incluye tres tareas:

* Habilitar la copia de seguridad de estado de sistema con hello Azure Backup agent
* Programar copias de seguridad de Hola
* Realizar una copia de archivos y carpetas de hello primera vez

toocomplete Hola copia de seguridad inicial, agente de servicios de recuperación de Microsoft Azure Hola de uso.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>tooenable de copia de seguridad de estado del sistema con el agente de copia de seguridad de Azure Hola

1. En una sesión de PowerShell, ejecute hello después de motor de copia de seguridad de Azure de comando toostop Hola.

  ```
  PS C:\> Net stop obengine
  ```

2. Abra Hola del registro de Windows.

  ```
  PS C:\> regedit.exe
  ```

3. Agregar Hola después de la clave del registro con hello especificado valor DWord.

  | Ruta de acceso del Registro | Clave del Registro | Valor DWord |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Reinicie el motor de copia de seguridad de hello ejecutando el siguiente comando en un símbolo del sistema con privilegios elevados de Hola.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>trabajo de copia de seguridad de hello tooschedule

1. Abra el agente de servicios de recuperación de Microsoft Azure de Hola. Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.

    ![Iniciar el agente de servicios de recuperación de Azure de Hola](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. En el agente de servicios de recuperación de hello, haga clic en **programar copias de seguridad**.

    ![Programación de una copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. En hello Introducción a la página de hello Asistente para la programación de copia de seguridad, haga clic en **siguiente**.

4. En la página de tooBackup de seleccionar elementos de hello, haga clic en **agregar elementos**.

5. Seleccione **Estado del sistema** y haga clic en **Aceptar**.

6. Haga clic en **Siguiente**.

7. Hello programación de copia de seguridad de estado del sistema y de retención se establece automáticamente tooback seguridad de todos los domingos a 9:00 P.M., hora local, y se establece el período de retención de hello too60 días.

   > [!NOTE]
   > La directiva de retención y copia de seguridad del estado del sistema se configura automáticamente. Si hace una copia archivos y carpetas además toohello Windows Server System State, especifique la única directiva de copia de seguridad y retención de Hola para copias de seguridad de archivos de Asistente de Hola. 
   >

8. En la página de confirmación de hello, revise la información de hello y, a continuación, haga clic en **finalizar**.

9. Cuando finalice el Asistente de hello, crear la programación de copia de seguridad de hello, haga clic en **cerrar**.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>tooback el estado de sistema de Windows Server para hello primera vez

1. Asegúrese de que no hay actualizaciones pendientes para Windows Server que requieran un reinicio.

2. En el agente de servicios de recuperación de hello, haga clic en **Back Up Now** toocomplete Hola inicial de la propagación a través de red de Hola.

    ![Copia de seguridad de Windows Server ahora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. En la página de confirmación de hello, revise la configuración Hola que Hola a ahora Asistente de Back Up usará tooback máquina Hola. Luego, haga clic en **Crear copia de seguridad**.

4. Haga clic en **cerrar** Asistente de hello tooclose. Si cierra al Asistente de hello antes de que finalice el proceso de copia de seguridad de hello, Asistente Hola continúa toorun en segundo plano de Hola.

5. Si hace una copia archivos y carpetas en el servidor, además toohello Windows Server System State, Asistente de copia de seguridad ahora Hola realizará solo una copia de archivos. tooperform un estado del sistema ad hoc realizar copias de seguridad, Hola de uso siguiente comando de PowerShell:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Una vez completada la copia de seguridad inicial de hello, Hola **ha completado el trabajo** estado aparece en la consola de copia de seguridad de Hola.

  ![IR completado](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

Hello siguientes preguntas y respuestas proporcionan información complementaria.

### <a name="what-is-hello-staging-volume"></a>¿Cuál es el volumen de almacenamiento provisional de Hola?

Hola volumen de almacenamiento provisional representa ubicación intermedia Hola donde hello disponible de forma nativa, copias de seguridad de Windows Server crea etapas en hello copia de seguridad de estado del sistema. Agente de copia de seguridad de Azure, a continuación, comprime y cifra esta copia de seguridad intermedio y envía que esta a través de secure toohello de protocolo HTTPS configurado el almacén de servicios de recuperación. **Se recomienda que establecer Hola volumen de almacenamiento provisional en un volumen sin sistema operativo Windows. Si observa problemas con las copias de seguridad de estado de sistema, comprobando ubicación Hola de su volumen de almacenamiento provisional es el primer paso de solución de problemas Hola.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>¿Cómo se puede cambiar Hola ruta de acceso de volumen de almacenamiento provisional especificada en el agente de copia de seguridad de Azure de hello?

Hola volumen de almacenamiento provisional se encuentra en la carpeta de caché de Hola de forma predeterminada. 

1. toochange esta ubicación, Hola de uso siguiente comando (en un símbolo del sistema con privilegios elevados):
  ```
  PS C:\> Net stop obengine
  ```

2. A continuación, actualice Hola siguiendo las entradas del registro con la carpeta Hola ruta toohello nuevo volumen de almacenamiento provisional.

  |Ruta de acceso del Registro|Clave del Registro|Valor|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | nueva ubicación del volumen de almacenamiento provisional |

Hola ruta de acceso de almacenamiento provisional distingue mayúsculas de minúsculas y debe ser Hola exacta mismo mayúsculas y minúsculas como lo que existe en el servidor de Hola. 

3. Una vez que cambie la ruta de acceso del volumen de almacenamiento provisional de hello, reinicie el motor de copia de seguridad de hello:
  ```
  PS C:\> Net start obengine
  ```
4. toopick ruta de acceso de hello cambiado, agente de servicios de recuperación de Microsoft Azure Hola abierto y desencadenador una copia de seguridad ad hoc de estado del sistema.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>¿Por qué es el estado de sistema de hello tiempo predeterminado de retención establecido too60 días?

vida útil de Hola de una copia de seguridad de estado del sistema es Hola igual a la configuración de hello, "tombstone lifetime" para el rol de Windows Server Active Directory Hola. valor predeterminado de Hello para la entrada de duración de objetos de desecho de hello es de 60 días. Este valor se puede establecer en el objeto de configuración del servicio de directorio (NTDS) Hola.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>¿Cómo cambio predeterminado Hola copia de seguridad y directiva de retención para el estado del sistema?

predeterminado de hello toochange copia de seguridad y directiva de retención para el estado del sistema:
1. Detenga el motor de copia de seguridad de Hola. Ejecute hello siguiente comando desde un símbolo del sistema con privilegios elevados.

  ```
  PS C:\> Net stop obengine
  ```

2. Agregar o actualizar Hola siguientes entradas de la clave del registro en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Backup\Config\CloudBackupProvider de Azure.

  |Nombre en el Registro|Descripción|Valor|
  |-------------|-----------|-----|
  |SSBScheduleTime|Utiliza el tiempo de hello tooconfigure de copia de seguridad de Hola. El valor predeterminado es 9 p. m. (hora local).|DWord: Formato HHMM (decimal), por ejemplo 2130 para 9:30 p. m. (hora local)|
  |SSBScheduleDays|Especificar los días de hello tooconfigure usado cuando debe realizarse la copia de seguridad de estado del sistema en hello tiempo. Dígitos individuales especifican los días de la semana de Hola. 0 representa el domingo, 1 es el lunes y así sucesivamente. El día predeterminado para hacer la copia de seguridad es el domingo.|DWord: días de copia de seguridad de hello semana toorun (decimal), por ejemplo 1230 programa copias de seguridad en el lunes, el martes, el miércoles y el domingo.|
  |SSBRetentionDays|Tooconfigure usado Hola días tooretain copia de seguridad. El valor predeterminado es 60. El valor máximo permitido es 180.|DWord: Días tooretain copia de seguridad (decimal).|

3. Usar hello después de motor de copia de seguridad de comando toorestart Hola.
    ```
    PS C:\> Net start obengine
    ```

4. Abra el agente de servicios de recuperación de Microsoft de Hola.

5. Haga clic en **programar copias de seguridad** y, a continuación, haga clic en **siguiente** hasta que vea cambios Hola reflejados.

6. Haga clic en **finalizar** cambios de hello tooapply.


## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de cómo [realizar copias de seguridad de máquinas Windows](backup-configure-vault.md).
* Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).
* Si necesita toorestore una copia de seguridad, use este artículo demasiado[restaurar archivos tooa Windows máquina](backup-azure-restore-windows-server.md).
