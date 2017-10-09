---
title: "aaaBack una tooAzure de servidor o estación de trabajo de Windows (modelo clásico) | Documentos de Microsoft"
description: "Copia de seguridad Windows servidores o clientes tooa almacén en Azure. Vaya a través de los conceptos básicos para proteger archivos y carpetas tooa el almacén de copia de seguridad mediante el agente de copia de seguridad de Azure Hola."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "almacén de copia de seguridad; copia de seguridad de un equipo de Windows Server; ventanas de copia de seguridad;"
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Copia un tooAzure de servidor o estación de trabajo de Windows mediante el portal clásico de Hola
> [!div class="op_single_selector"]
> * [Portal clásico](backup-configure-vault-classic.md)
> * [Portal de Azure](backup-configure-vault.md)
>
>

En este artículo se describen los procedimientos de Hola que necesita toofollow tooprepare su entorno y hacer copia de seguridad de un tooAzure de servidor (o estación de trabajo) de Windows. También se describen los aspectos que se deben tener en cuenta al implementar la solución de copia de seguridad. Si está interesado en probar la copia de seguridad de Azure para hello primera vez, este artículo le guiará rápidamente por el proceso de Hola.

Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: el de Resource Manager y el clásico. Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

## <a name="before-you-start"></a>Antes de comenzar
tooback un servidor o cliente tooAzure, necesita una cuenta de Azure. En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en tan solo unos minutos.

## <a name="create-a-backup-vault"></a>Creación de un almacén de copia de seguridad
tooback seguridad de archivos y carpetas desde un servidor o cliente, deberá toocreate un almacén de copia de seguridad de la región geográfica Hola donde desea toostore Hola datos.

> [!IMPORTANT]
> A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.
>
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> **15 de octubre de 2017**, ya no estará almacenes de copia de seguridad de toocreate de toouse capaz de PowerShell. <br/> **A partir del 1 de noviembre de 2017**:
>- Los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>


## <a name="download-hello-vault-credential-file"></a>Descargar archivo de credenciales de almacén de Hola
máquina local de Hello debe toobe autenticado con un almacén de copia de seguridad antes de pueda respaldar tooAzure de datos. autenticación de Hola se consigue a través de *del almacén de credenciales*. archivo de credenciales de almacén de Hola se descarga a través de un canal seguro entre el portal clásico de Hola. clave privada del certificado de Hello no se conserva en el portal de Hola o servicio Hola.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>máquina local del tooa de archivos de toodownload Hola almacén credencial
1. En el panel de navegación izquierdo de hello, haga clic en **servicios de recuperación**y, a continuación, seleccione el almacén de copia de seguridad Hola que ha creado.

    ![IR completado](./media/backup-configure-vault-classic/rs-left-nav.png)
2. En la página de inicio rápido de hello, haga clic en **descargar credenciales de almacén**.

   portal clásico de Hello genera una credencial de almacén mediante una combinación de nombre de almacén de Hola y Hola fecha actual. archivo de credenciales de almacén de Hola se utiliza solo durante el flujo de trabajo de registro de hello y expira después de 48 horas.

   archivo de credenciales de almacén de Hello puede descargarse desde el portal de Hola.
3. Haga clic en **guardar** toodownload Hola almacén credencial toohello descargas cajón de cuenta local de Hola. También puede seleccionar **Guardar como** de hello **guardar** menú toospecify una ubicación para el archivo de credenciales de almacén de Hola.

   > [!NOTE]
   > Asegúrese de que el archivo de credenciales de almacén de Hola se guarda en una ubicación que sea accesible desde su equipo. Si se almacena en un bloque de mensajes de servidor o recurso compartido de archivo, compruebe que dispone de hello permisos tooaccess lo.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>Descargar, instalar y registrar el agente de copia de seguridad de Hola
Después de crear el almacén de copia de seguridad hello y archivo de credenciales de almacén de Hola de descarga, debe instalarse un agente en cada uno de los equipos de Windows.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, instalar y registrar el agente de Hola
1. Haga clic en **servicios de recuperación**y, a continuación, seleccione el almacén de copia de seguridad de Hola que desea tooregister con un servidor.
2. En la página de inicio rápido de hello, haga clic en agente de hello **agente para Windows Server o cliente de System Center Data Protection Manager o Windows**. A continuación, haga clic en **Guardar**.

    ![Guardar agente](./media/backup-configure-vault-classic/agent.png)
3. Después de que ha descargado el archivo de MARSagentinstaller.exe hello, haga clic en **ejecutar** (o haga doble clic en **MARSAgentInstaller.exe** de ubicación de hello guardado).
4. Elija la carpeta de instalación de Hola y la carpeta de caché que son necesarios para el agente de hello y, a continuación, haga clic en **siguiente**. ubicación de caché de Hola que especifique debe tener espacio libre igual tooat menos 5 por ciento de los datos de copia de seguridad de Hola.
5. Puede continuar tooconnect toohello Internet a través de la configuración de proxy de hello predeterminada.             Si utiliza un toohello de tooconnect de servidor proxy de Internet, en la página de configuración del Proxy de hello, seleccione hello **usar configuración de proxy personalizada** casilla de verificación y, a continuación, escriba los detalles del servidor proxy Hola. Si usa un proxy autenticado, escriba los detalles de nombre y la contraseña de usuario de hello y, a continuación, haga clic en **siguiente**.
6. Haga clic en **instalar** instalación del agente toobegin Hola. agente de copia de seguridad de Hello instala .NET Framework 4.5 y Windows PowerShell (si aún no está instalado) instalación de hello toocomplete.
7. Después de instalar el agente de hello, haga clic en **continuar tooRegistration** toocontinue con flujo de trabajo de Hola.
8. En la página de identificación del almacén de hello, examinar tooand archivo de credenciales de almacén de hello select que ha descargado anteriormente.

    archivo de credenciales de almacén de Hello es válido durante 48 horas solo después de descargarlo desde el portal de Hola. Si se produce un error en esta página (por ejemplo, "almacén de credenciales archivo proporcionado ha expirado"), inicie sesión en el portal de toohello y descargar el archivo de credenciales de almacén de Hola de nuevo.

    Asegúrese de que ese archivo de credenciales de almacén de hello está disponible en una ubicación que se puede acceder mediante la aplicación de instalación de Hola. Si se producen errores relacionados con el acceso, copie Hola almacén credencial archivo tooa ubicación temporal Hola mismo equipo y vuelva a intentar la operación de Hola.

    Si se produce un error de credenciales de almacén como "credenciales de almacén no válida proporcionadas", archivo hello está dañado o no haya Hola últimas credenciales asociadas con el servicio de recuperación de Hola. Vuelva a intentar la operación de hello después de descargar un nuevo archivo de credenciales de almacén desde el portal de Hola. Este error también puede producirse si un usuario hace clic en hello **descarga las credenciales del almacén** opción varias veces en una sucesión rápida. En este caso, solo Hola último almacén credencial archivo es válido.
9. En la página de configuración de cifrado de hello, puede generar una frase de contraseña o proporcione una frase de contraseña (con un mínimo de 16 caracteres). Recuerde la frase de contraseña de toosave hello en una ubicación segura.
10. Haga clic en **Finalizar** Asistente para registrar servidor Hello registra el servidor de hello con copia de seguridad.

    > [!WARNING]
    > Si pierde u olvida la frase de contraseña de hello, Microsoft no puede ayudarle a recuperar datos de copia de seguridad de saludo. Poseer Hola frase de contraseña y Microsoft no tiene visibilidad en la frase de contraseña de Hola que usar. Guarde el archivo hello en una ubicación segura ya que será necesario durante una operación de recuperación.
    >
    >

11. Después de establece la clave de cifrado de hello, deje hello **iniciar Microsoft Azure Backup Agent** casilla seleccionada y, a continuación, haga clic en **cerrar**.

## <a name="complete-hello-initial-backup"></a>Copia de seguridad inicial de hello completa
copia de seguridad inicial de Hello incluye dos tareas fundamentales:

* Crear programación de copia de seguridad de Hola
* Copia de seguridad de archivos y carpetas de hello primera vez

Al finalizar la directiva de copia de seguridad de hello copia de seguridad inicial de hello, crea puntos de copia de seguridad que puede utilizar si necesita toorecover Hola datos. Directiva de copia de seguridad de Hello lo hace en función de la programación de Hola que usted defina.

### <a name="tooschedule-hello-backup"></a>copia de seguridad de hello tooschedule
1. Abra el agente de copia de seguridad de Microsoft Azure de Hola. (Se abrirá automáticamente si se deja hello **iniciar Microsoft Azure Backup Agent** casilla de verificación activada al cerrar el Asistente para registrar servidor hello.) Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.

    ![Iniciar el agente de copia de seguridad de Azure Hola](./media/backup-configure-vault-classic/snap-in-search.png)
2. En el agente de copia de seguridad de hello, haga clic en **programar copias de seguridad**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. En hello Introducción a la página de hello Asistente para la programación de copia de seguridad, haga clic en **siguiente**.
4. En la página de tooBackup de seleccionar elementos de hello, haga clic en **agregar elementos**.
5. Seleccionar archivos de Hola y las carpetas que desea tooback seguridad y, a continuación, haga clic en **bien**.
6. Haga clic en **Siguiente**.
7. En hello **especificar una programación de copia de seguridad** página, especifique hello **programar copia de seguridad** y haga clic en **siguiente**.

    Puede programar copias de seguridad diarias (con una frecuencia máxima de tres veces al día) o semanales.

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Para obtener más información acerca de cómo toospecify Hola programar copia de seguridad, vea el artículo de hello [tooreplace utilice Azure Backup su infraestructura de cinta](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. En hello **Seleccionar directiva de retención** página, seleccione hello **directiva de retención** para copia de seguridad de Hola.

    Directiva de retención de Hello especifica duración hello para el que se almacenará la copia de seguridad de Hola. En vez de simplemente especificar una "directiva" para todos los puntos de copia de seguridad, puede especificar las directivas de retención diferente en función de cuando se produce la copia de seguridad de Hola. Puede modificar toomeet de directivas de retención diaria, semanal, mensual y anual de hello sus necesidades.
9. En la página Elegir tipo de copia de seguridad inicial de hello, elija el tipo de copia de seguridad inicial de Hola. Deje la opción de hello **automáticamente a través de la red de hello** seleccionada y, a continuación, haga clic en **siguiente**.

    Hacer copias de seguridad automáticamente a través de red de hello, o puede realizar una copia sin conexión. resto de Hola de este artículo describe proceso Hola para realizar copias de seguridad automáticamente. Si lo prefiere toodo una copia de seguridad sin conexión, revise el artículo de hello [flujo de trabajo de copia de seguridad sin conexión en copia de seguridad de Azure](backup-azure-backup-import-export.md) para obtener información adicional.
10. En la página de confirmación de hello, revise la información de hello y, a continuación, haga clic en **finalizar**.
11. Cuando finalice el Asistente de hello, crear la programación de copia de seguridad de hello, haga clic en **cerrar**.

### <a name="enable-network-throttling-optional"></a>Habilitación de la velocidad moderada de la red (opcional)
agente de copia de seguridad de Hola proporciona el límite de red. Esta limitación controla cómo se utiliza el ancho de banda de red durante la transferencia de datos. Este control puede ser útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de Internet. La limitación se aplica tooback seguridad y restaurar las actividades.

**límite de red tooenable**

1. En el agente de copia de seguridad de hello, haga clic en **cambiar las propiedades de**.

    ![Cambiar propiedades](./media/backup-configure-vault-classic/change-properties.png)
2. En hello **limitación** ficha, seleccione hello **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet** casilla de verificación.

    ![Limitación de la red](./media/backup-configure-vault-classic/throttling-dialog.png)
3. Después de haber habilitado la limitación, especifique Hola permitido ancho de banda para transfirieron datos de copia de seguridad durante la **horas laborables** y **horas de descanso**.

    los valores de ancho de banda de Hello comienzan en 512 kilobits por segundo (Kbps) y pueden crecer hasta too1, 023 megabytes por segundo (MBps). También puede designar el inicio de Hola y de fin para **horas laborables**, y qué días de la semana de hello son días laborables considerada. Las horas que se encuentran fuera de las horas laborables designadas se consideran como no laborables.
4. Haga clic en **Aceptar**.

### <a name="tooback-up-now"></a>tooback seguridad ahora
1. En el agente de copia de seguridad de hello, haga clic en **Back Up Now** toocomplete Hola inicial de la propagación a través de red de Hola.

    ![Realizar copia de seguridad de Windows Server ahora](./media/backup-configure-vault-classic/backup-now.png)
2. En la página de confirmación de hello, revise la configuración Hola que Hola a ahora Asistente de Back Up usará tooback máquina Hola. Luego, haga clic en **Crear copia de seguridad**.
3. Haga clic en **cerrar** Asistente de hello tooclose. Si lo hace antes de que finalice el proceso de copia de seguridad de hello, Asistente Hola continúa toorun en segundo plano de Hola.

Una vez completada la copia de seguridad inicial de hello, Hola **ha completado el trabajo** estado aparece en la consola de copia de seguridad de Hola.

![IR completado](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>Pasos siguientes
* Regístrese para obtener una [cuenta de Azure gratuita](https://azure.microsoft.com/free/).

Para más información sobre la copia de seguridad de máquinas virtuales u otras cargas de trabajo, consulte:

* [Preparación del entorno de copia de seguridad de máquinas virtuales de Azure](backup-azure-vms-prepare.md)
* [Hacer copia de seguridad tooAzure de cargas de trabajo con el servidor de copia de seguridad de Microsoft Azure](backup-azure-microsoft-azure-backup.md)
* [Hacer copia de seguridad de cargas de trabajo tooAzure con DPM](backup-azure-dpm-introduction.md)
