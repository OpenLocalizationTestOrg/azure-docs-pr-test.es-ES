---
title: tooback de agente de copia de seguridad de Azure de aaaUse seguridad de archivos y carpetas | Documentos de Microsoft
description: "Utilice tooback de agente de copia de seguridad de Microsoft Azure Hola seguridad tooAzure de archivos y carpetas de Windows. Crear un almacén de servicios de recuperación, instalar el agente de copia de seguridad de hello, definir la directiva de copia de seguridad de Hola y ejecutar copia de seguridad inicial de hello en las carpetas y archivos de Hola."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "almacén de copia de seguridad; copia de seguridad de un equipo de Windows Server; ventanas de copia de seguridad;"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>Copia un tooAzure de Windows Server o cliente utilizando el modelo de implementación del Administrador de recursos de Hola
> [!div class="op_single_selector"]
> * [Portal de Azure](backup-configure-vault.md)
> * [Portal clásico](backup-configure-vault-classic.md)
>
>

Este artículo explica cómo tooback el servidor de Windows (o cliente de Windows) tooAzure de archivos y carpetas con el uso de copia de seguridad de Azure Hola modelo de implementación del Administrador de recursos.

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Pasos del proceso de copia de seguridad](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>Antes de comenzar
tooback un servidor o cliente tooAzure, necesita una cuenta de Azure. En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en tan solo unos minutos.

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services
Un almacén de servicios de recuperación es una entidad que almacena todas las copias de seguridad de Hola y puntos de recuperación que se crea con el tiempo. almacén de servicios de recuperación de Hello también contiene Hola directiva de copia de seguridad aplicada toohello protegida archivos y carpetas. Cuando se crea un almacén de servicios de recuperación, también debe seleccionar opción de redundancia de almacenamiento adecuada de Hola.

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


### <a name="set-storage-redundancy"></a>Establecimiento de la redundancia de almacenamiento
Al crear un almacén de Servicios de recuperación se determina cómo se replica el almacenamiento.

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

Ahora que ha creado un almacén, preparar su tooback de infraestructura de seguridad de archivos y carpetas, se descargan e instalar a agente de servicios de recuperación de Microsoft Azure hello, descargar las credenciales de almacén y, a continuación, usar esas credenciales tooregister Hola agente almacén de Hola.

## <a name="configure-hello-vault"></a>Configurar el almacén de Hola

1. Hola hoja de almacén de servicios de recuperación (hello para el almacén de que acaba de crear), en la sección de introducción de hello en, haga clic en **copia de seguridad**, a continuación, en hello **Introducción a la copia de seguridad** hoja, seleccione  **Objetivo de copia de seguridad**.

  ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  Hola **objetivo de copia de seguridad** abre la hoja. Si se ha configurado previamente Hola del almacén de servicios de recuperación, Hola **objetivo de copia de seguridad** hojas se abre al hacer clic en **copia de seguridad** en servicios de recuperación de hello del almacén de hoja.

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

Si el máquina/proxy tiene limitado el acceso a internet, asegúrese de que configuración de firewall en el proxy de la máquina hello es hello tooallow configurado las siguientes direcciones URL: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne


## <a name="create-hello-backup-policy"></a>Crear directiva de copia de seguridad de Hola
Directiva de copia de seguridad de Hello es la programación de hello cuando se realizan puntos de recuperación y Hola período de tiempo se conservan los puntos de recuperación de Hola. Usar la directiva copia de seguridad de hello copia de seguridad de Microsoft Azure agente toocreate Hola para archivos y carpetas.

### <a name="toocreate-a-backup-schedule"></a>toocreate una programación de copia de seguridad
1. Abra el agente de copia de seguridad de Microsoft Azure de Hola. Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.

    ![Iniciar el agente de copia de seguridad de Azure Hola](./media/backup-configure-vault/snap-in-search.png)
2. En el agente de copia de seguridad hello **acciones** panel, haga clic en **programar copias de seguridad** toolaunch Hola Asistente para la programación de copia de seguridad.

    ![Programar una copia de seguridad de Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. En hello **Introducción** página de hello Asistente para la programación de copia de seguridad, haga clic en **siguiente**.
4. En hello **seleccionar elementos tooBackup** página, haga clic en **agregar elementos**.

  se abre el cuadro de diálogo de Hello seleccionar elementos.

5. Seleccione Hola archivos y carpetas que desee tooprotect y, a continuación, haga clic en **Aceptar**.
6. Hola **seleccionar elementos tooBackup** página, haga clic en **siguiente**.
7. En hello **especificar una programación de copia de seguridad** página, especifique la programación de copia de seguridad de Hola y haga clic en **siguiente**.

    Puede programar copias de seguridad diarias (con una frecuencia máxima de tres veces al día) o semanales.

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > Para obtener más información acerca de cómo toospecify Hola programar copia de seguridad, vea el artículo de hello [tooreplace utilice Azure Backup su infraestructura de cinta](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. En hello **Seleccionar directiva de retención** página, elija Hola Hola de las directivas de retención específico para la copia de seguridad de Hola y haga clic en **siguiente**.

    Directiva de retención de Hello especifica duración Hola se almacena la copia de seguridad de Hola. En vez de simplemente especificar una "directiva" para todos los puntos de copia de seguridad, puede especificar las directivas de retención diferente en función de cuando se produce la copia de seguridad de Hola. Puede modificar toomeet de directivas de retención diaria, semanal, mensual y anual de hello sus necesidades.
9. En la página Elegir tipo de copia de seguridad inicial de hello, elija el tipo de copia de seguridad inicial de Hola. Deje la opción de hello **automáticamente a través de la red de hello** seleccionada y, a continuación, haga clic en **siguiente**.

    Hacer copias de seguridad automáticamente a través de red de hello, o puede realizar una copia sin conexión. resto de Hola de este artículo describe proceso Hola para realizar copias de seguridad automáticamente. Si lo prefiere toodo una copia de seguridad sin conexión, revise el artículo de hello [flujo de trabajo de copia de seguridad sin conexión en copia de seguridad de Azure](backup-azure-backup-import-export.md) para obtener información adicional.
10. En la página de confirmación de hello, revise la información de hello y, a continuación, haga clic en **finalizar**.
11. Cuando finalice el Asistente de hello, crear la programación de copia de seguridad de hello, haga clic en **cerrar**.

### <a name="enable-network-throttling"></a>Habilitación de la limitación de la red
agente de copia de seguridad de Microsoft Azure Hola proporciona el límite de red. Esta limitación controla cómo se utiliza el ancho de banda de red durante la transferencia de datos. Este control puede ser útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de Internet. La limitación se aplica tooback seguridad y restaurar las actividades.

> [!NOTE]
> La limitación de la red no está disponible en Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ni en Windows 7 (con Service Packs). característica de limitación de red de copia de seguridad de Azure de Hello involucre a calidad de servicio (QoS) en el sistema operativo local de Hola. Aunque la copia de seguridad de Azure puede proteger estos sistemas operativos, versión de Hola de QoS disponibles en estas plataformas no funciona con la limitación de red de copia de seguridad de Azure. La limitación de la red puede usarse en todos los demás [sistemas operativos admitidos](backup-azure-backup-faq.md).
>
>

**límite de red tooenable**

1. En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **cambiar las propiedades de**.

    ![Cambiar propiedades](./media/backup-configure-vault/change-properties.png)
2. En hello **limitación** ficha, seleccione hello **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet** casilla de verificación.

    ![Limitación de la red](./media/backup-configure-vault/throttling-dialog.png)
3. Después de haber habilitado la limitación, especifique Hola permitido ancho de banda para transfirieron datos de copia de seguridad durante la **horas laborables** y **horas de descanso**.

    los valores de ancho de banda de Hello comienzan en 512 kilobits por segundo (Kbps) y pueden crecer hasta too1, 023 megabytes por segundo (MBps). También puede designar el inicio de Hola y de fin para **horas laborables**, y qué días de la semana de hello son días laborables considerada. Las horas que se encuentran fuera de las horas laborables designadas se consideran como no laborables.
4. Haga clic en **Aceptar**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback seguridad de archivos y carpetas para hello primera vez
1. En el agente de copia de seguridad de hello, haga clic en **Back Up Now** toocomplete Hola inicial de la propagación a través de red de Hola.

    ![Realizar copia de seguridad de Windows Server ahora](./media/backup-configure-vault/backup-now.png)
2. En la página de confirmación de hello, revise la configuración Hola que Hola a ahora Asistente de Back Up usará tooback máquina Hola. Luego, haga clic en **Crear copia de seguridad**.
3. Haga clic en **cerrar** Asistente de hello tooclose. Si lo hace antes de que finalice el proceso de copia de seguridad de hello, Asistente Hola continúa toorun en segundo plano de Hola.

Una vez completada la copia de seguridad inicial de hello, Hola **ha completado el trabajo** estado aparece en la consola de copia de seguridad de Hola.

![IR completado](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre la copia de seguridad de máquinas virtuales u otras cargas de trabajo, consulte:

* Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).
* Si necesita toorestore una copia de seguridad, use este artículo demasiado[restaurar archivos tooa Windows máquina](backup-azure-restore-windows-server.md).
