---
title: aaaAzure servidor de copia de seguridad protege el estado del sistema y restaura el sistema operativo toobare | Documentos de Microsoft
description: "Servidor de copia de seguridad de Azure tooback hay que usar el estado del sistema y proporcionar protección de reconstrucción completa (BMR)."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Copia de seguridad de estado del sistema y restaurar el sistema operativo toobare con el servidor de copia de seguridad de Azure

Azure Backup Server realiza una copia de seguridad del estado del sistema y proporciona protección de reconstrucción completa (BMR).

*   **Copia de seguridad de estado de sistema**: realiza una copia de archivos del sistema operativo, por lo que puede recuperar cuando se inicia un equipo, pero los archivos del sistema y el registro de hello se pierden. Una copia de seguridad del estado del sistema incluye lo siguiente:
    * Miembro de dominio: archivos de arranque, base de datos de registro de clase COM+, Registro.
    * Controlador de dominio: Windows Server Active Directory (NTDS), archivos de arranque, base de datos de registro de clase COM+, Registro, volumen del sistema (SYSVOL).
    * Equipo que ejecuta servicios de clúster: metadatos del servidor de clúster.
    * Equipo que ejecuta servicios de certificados: datos del certificado.
* **Copia de seguridad de reconstrucción completa**: realiza una copia de seguridad de los archivos del sistema operativo y de todos los datos de volúmenes críticos (excepto los datos de usuario). Por definición, una copia de seguridad de BMR incluye una copia de seguridad del estado del sistema. Proporciona protección cuando no se inicia un equipo y ha toorecover todo.

Hello en la tabla siguiente resume lo que puede realizar copias de y recuperar. Para obtener información detallada sobre las versiones de las aplicaciones que se pueden proteger con el estado del sistema y BMR, vea [los elementos de los que Azure Backup Server puede realizar una copia de seguridad](backup-mabs-protection-matrix.md).

|Backup|Problema|Recuperación a partir de una copia de seguridad de Azure Backup Server|Recuperación a partir de una copia de seguridad del estado de sistema|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**Datos de archivo**<br /><br />Copia de seguridad de datos normal<br /><br />BMR/Copia de seguridad del estado del sistema|Datos de archivo perdidos|Y|N|N|
|**Datos de archivo**<br /><br />Copia de seguridad de Azure Backup Server de los datos de archivo<br /><br />BMR/Copia de seguridad del estado del sistema|Sistema operativo dañado o perdido|N|Y|Y|
|**Datos de archivo**<br /><br />Copia de seguridad de Azure Backup Server de los datos de archivo<br /><br />BMR/Copia de seguridad del estado del sistema|Servidor perdido (volúmenes de datos intactos)|N|N|Y|
|**Datos de archivo**<br /><br />Copia de seguridad de Azure Backup Server de los datos de archivo<br /><br />BMR/Copia de seguridad del estado del sistema|Servidor perdido (volúmenes de datos perdidos)|Y|No|Sí (BMR, seguida de una recuperación normal de los datos de archivo de los que se ha realizado una copia de seguridad)|
|**Datos de SharePoint**:<br /><br />Copia de seguridad de Azure Backup Server de los datos de la granja<br /><br />BMR/Copia de seguridad del estado del sistema|Sitio, listas, elementos de lista y documentos perdidos|Y|N|N|
|**Datos de SharePoint**:<br /><br />Copia de seguridad de Azure Backup Server de los datos de la granja<br /><br />BMR/Copia de seguridad del estado del sistema|Sistema operativo dañado o perdido|N|Y|Y|
|**Datos de SharePoint**:<br /><br />Copia de seguridad de Azure Backup Server de los datos de la granja<br /><br />BMR/Copia de seguridad del estado del sistema|Recuperación ante desastres|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Copia de seguridad de Azure Backup Server del host o invitado de Hyper-V<br /><br />BMR/Copia de seguridad del estado del sistema del host|Máquina virtual perdida|Y|N|N|
|Hyper-V<br /><br />Copia de seguridad de Azure Backup Server del host o invitado de Hyper-V<br /><br />BMR/Copia de seguridad del estado del sistema del host|Sistema operativo dañado o perdido|N|Y|Y|
|Hyper-V<br /><br />Copia de seguridad de Azure Backup Server del host o invitado de Hyper-V<br /><br />BMR/Copia de seguridad del estado del sistema del host|Host de Hyper-V perdido (máquinas virtuales intactas)|N|N|Y|
|Hyper-V<br /><br />Copia de seguridad de Azure Backup Server del host o invitado de Hyper-V<br /><br />BMR/Copia de seguridad del estado del sistema del host|Host de Hyper-V perdido (máquinas virtuales perdidas)|N|N|Y<br /><br />BMR, seguida de una recuperación normal de Azure Backup Server|
|SQL Server/Exchange<br /><br />Copia de seguridad de aplicación de Azure Backup Server<br /><br />BMR/Copia de seguridad del estado del sistema|Datos de la aplicación perdidos|Y|N|N|
|SQL Server/Exchange<br /><br />Copia de seguridad de aplicación de Azure Backup Server<br /><br />BMR/Copia de seguridad del estado del sistema|Sistema operativo dañado o perdido|N|y|Y|
|SQL Server/Exchange<br /><br />Copia de seguridad de aplicación de Azure Backup Server<br /><br />BMR/Copia de seguridad del estado del sistema|Servidor perdido (base de datos/registros de transacciones intactos)|N|N|Y|
|SQL Server/Exchange<br /><br />Copia de seguridad de aplicación de Azure Backup Server<br /><br />BMR/Copia de seguridad del estado del sistema|Servidor perdido (base de datos/registros de transacciones perdidos)|N|N|Y<br /><br />BMR, seguida de una recuperación normal de Azure Backup Server|

## <a name="how-system-state-backup-works"></a>Cómo funciona la copia de seguridad del estado del sistema

Cuando se ejecuta una copia de seguridad de estado del sistema, copia de seguridad de servidor se comunica con toorequest copias de seguridad de Windows Server una copia de seguridad de estado del sistema del servidor de Hola. De forma predeterminada, el servidor de copia de seguridad y copia de seguridad de Windows Server usan unidad de Hola que tiene hello más espacio libre. Información acerca de esta unidad se guarda en el archivo PSDataSourceConfig.xml de Hola. Se trata de una unidad de Hola que copias de seguridad de Windows Server que se usa para las copias de seguridad.

Puede personalizar la unidad de Hola que usa el servidor de copia de seguridad para copia de seguridad de estado de sistema de Hola. En el servidor de hello protegido, vaya tooC:\Program Files\Microsoft Manager\MABS\Datasources de protección de datos. Abrir archivo de hello PSDataSourceConfig.xml para su edición. Hola de cambio \<FilesToProtect\> valor de letra de unidad de Hola. Guarde y cierre el archivo hello. Si hay que un grupo de protección establece tooprotect Hola estado del sistema Hola equipo, ejecute una comprobación de coherencia. Si se genera una alerta, seleccione **Modificar grupo de protección** de alerta de Hola y Asistente de hello, a continuación, completa. Después, ejecute otra comprobación de coherencia.

Tenga en cuenta que si el servidor de protección de hello está en un clúster, es posible que se seleccionará una unidad agrupada como unidad de hello con hello más espacio libre. Si esa propiedad de la unidad se ha conmutado tooanother nodo y se ejecuta una copia de seguridad de estado del sistema, unidad de hello no está disponible y se produce un error en la copia de seguridad de Hola. En este escenario, modifique toopoint PSDataSourceConfig.xml tooa la unidad local.

A continuación, copia de seguridad de Windows Server crea una carpeta llamada WindowsImageBackup en raíz de Hola de carpeta de restauración de Hola. Copias de seguridad de Windows Server crea copias de seguridad de hello, todos los datos de saludo se colocan en esta carpeta. Cuando haya finalizado la copia de seguridad de hello, archivo hello sea el equipo del servidor de copia de seguridad de toohello transferidos. Tenga en cuenta Hola siguiente información:

* Esta carpeta y su contenido no se limpia cuando finaliza la copia de seguridad de Hola o transferencia. Hola toothink de manera mejor de esta es que Hola se se reserva espacio para hello próxima vez que finaliza una copia de seguridad.
* Hola carpeta se crea cada vez que se realiza una copia de seguridad. marca de fecha y hora de Hello refleja el tiempo de saludo de la última copia de seguridad del estado de sistema.

## <a name="bmr-backup"></a>Copia de seguridad de BMR

Para BMR (incluida una copia de seguridad de estado del sistema), trabajo de copia de seguridad de Hola se guarda tooa compartir directamente en el equipo del servidor de copia de seguridad de Hola. No se guarda tooa carpeta en el servidor de hello protegido.

Servidor de copia de seguridad llama a copias de seguridad de Windows Server y comparte volumen de réplica de Hola para esa copia de seguridad de reconstrucción completa. En este caso, no indica a unidad de copia de seguridad de Windows Server toouse Hola con hello más espacio libre. En su lugar, utiliza el recurso compartido de Hola que se creó para el trabajo de Hola.

Cuando haya finalizado la copia de seguridad de hello, archivo hello sea el equipo del servidor de copia de seguridad de toohello transferidos. Los registros se almacenan en C:\Windows\Logs\WindowsServerBackup.

## <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones

-   No se admite BMR para los equipos que ejecutan Windows Server 2003 o para los equipos que ejecutan un sistema operativo cliente.

-   No se puede proteger BMR y estado de sistema para hello mismo equipo en diferentes grupos de protección.

-   Un equipo con Backup Server no puede protegerse a sí mismo para BMR.

-   Tootape de protección a corto plazo (disco a cinta o D2T) no se admite para BMR. Se admite tootape de almacenamiento a largo plazo (disco a disco a cinta o D2D2T).

-   Para la protección de BMR, copias de seguridad de Windows Server debe instalarse en el equipo de hello protegido.

-   Para la protección de BMR, a diferencia de para la protección de estado del sistema, copia de seguridad de servidor no tiene ningún requisito de espacio en el equipo de hello protegido. Copia de seguridad de Windows Server transfiere directamente el equipo del servidor de copia de seguridad de las copias de seguridad toohello. trabajo de copia de seguridad de transferencia de Hello no aparece en hello servidor de copia de seguridad **trabajos** vista.

-   Servidor de copia de seguridad reserva 30 GB de espacio en el volumen de réplica de Hola para BMR. Puede cambiar esta configuración en hello **asignación de disco** página en el Asistente Modificar grupo de protección de Hola o mediante Hola Get-DatasourceDiskAllocation y Set-DatasourceDiskAllocation cmdlets de PowerShell. En el volumen del punto de recuperación de hello, protección de BMR requiere unos 6 GB para una retención de cinco días.
    * Tenga en cuenta que no se puede reducir a Hola réplica volumen tamaño que no requiere herramientas de 15 GB.
    * Servidor de copia de seguridad no calcula el tamaño de Hola Hola reconstrucción completa del origen de datos. y da por supuesto que son 30 GB para todos los servidores. Cambiar valor de hello basado en tamaño de Hola de copias de seguridad de reconstrucción completa que esperan en el entorno. tamaño de Hola de una copia de seguridad de reconstrucción completa se puede calcular aproximadamente como suma Hola de espacio utilizado en todos los volúmenes críticos. Volúmenes críticos = volumen de arranque + volumen del sistema + volumen que hospeda los datos del estado del sistema, como Active Directory.

-   Si cambia de protección tooBMR protección de estado del sistema, protección de BMR requiere menos espacio en hello *volumen del punto de recuperación*. Sin embargo, hello espacio adicional en el volumen de hello no se recupera. Puede reducir manualmente el tamaño del volumen de hello en hello **modificar asignación de disco** página del Asistente para modificar grupo de protección de Hola o mediante el uso de hello Get-DatasourceDiskAllocation y Set-DatasourceDiskAllocation cmdlets de PowerShell.

    Si cambia de protección tooBMR protección de estado del sistema, protección de BMR requiere más espacio en hello *volumen de réplica*. automáticamente se extenderá el volumen de Hola. Si desea que las asignaciones de espacio predeterminadas toochange hello, utilice cmdlet de PowerShell Modify-DiskAllocation Hola.

-   Si cambia de la protección de estado de toosystem de protección de BMR, necesita más espacio en volumen de punto de recuperación de Hola. Servidor de copia de seguridad puede intentar tooautomatically aumentar el volumen de Hola. Si no hay suficiente espacio en el bloque de almacenamiento de hello, se produce un error.

    Si cambia de la protección de estado de toosystem de protección de BMR, necesitará espacio en el equipo de hello protegido. Esto es porque la protección de estado del sistema escribe primero el equipo local de hello réplica toohello y, a continuación, transfiere el equipo del servidor de copia de seguridad de toohello.

## <a name="before-you-begin"></a>Antes de empezar

1.  **Implemente Azure Backup Server**. Compruebe que Backup Server está implementado correctamente. Para más información, consulte:
    * [Requisitos del sistema para Azure Backup Server](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Matriz de protección de Backup Server](backup-mabs-protection-matrix.md)

2.  **Configure el almacenamiento**. Puede almacenar datos de copia de seguridad en disco, cinta y en nube Hola con Azure. Para obtener más información, vea [Prepare data storage](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage) (Preparar el almacenamiento de datos).

3.  **Configurar el agente de protección de hello**. Instalar a agente de protección de Hola Hola otro equipo tooback seguridad. Para obtener más información, consulte [agente de protección DPM implementar hello](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Copia de seguridad del estado del sistema y reconstrucción completa
Configure un grupo de protección como se describe en [Deploy protection groups](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups) (Implementar grupos de protección). Tenga en cuenta que no puede proteger BMR y estado de sistema para hello mismo equipo en diferentes grupos. Además, cuando se selecciona BMR, el estado del sistema se habilita automáticamente.


1.  Asistente para crear nuevo grupo de protección Hola de tooopen en la consola del administrador del servidor de copia de seguridad, seleccione hello **protección** > **acciones** > **crear grupo de protección Grupo**.

2.  En hello **Seleccionar tipo de grupo de protección** , seleccione **servidores**y, a continuación, seleccione **siguiente**.

3.  En hello **seleccionar miembros del grupo** página, expanda equipo hello y, a continuación, seleccione **BMR** o **estado del sistema**.

    Recuerde que no se puede proteger el estado de sistema y BMR para hello mismo equipo en diferentes grupos. Además, cuando se selecciona BMR, el estado del sistema se habilita automáticamente. Para obtener más información, vea [Deploy protection groups](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups) (Implementar grupos de protección).

4.  En hello **Seleccionar método de protección de datos** , seleccione cómo desea toohandle copia de seguridad a corto plazo y a largo plazo. Copia de seguridad a corto plazo siempre es toodisk en primer lugar, con la opción de Hola de copia de seguridad de disco de hello toohello Azure en la nube mediante Azure copia de seguridad (a corto o a largo plazo). Una nube de copia de seguridad toohello toolong-término alternativo es tooset seguridad a largo plazo tooa copia de seguridad independiente dispositivo o una cinta biblioteca de cintas que se ha conectado tooBackup Server.

5.  En hello **seleccionar objetivos a corto plazo** página, seleccione cómo desea que tooback el almacenamiento de término tooshort en disco:
    1. Para **duración de retención**, seleccione cuánto tiempo desea tookeep datos de hello en el disco. 
    2. Para **frecuencia de sincronización**, seleccione la frecuencia con la que desea toorun una toodisk de copia de seguridad incremental. Si no desea tooset un intervalo de copia de seguridad, puede comprobar hello **sólo antes de un punto de recuperación** opción. Backup Server ejecutará una copia de seguridad rápida y completa justo antes de la programación de cada punto de recuperación.

6.  Si desea que toostore datos en cinta para almacenamiento a largo plazo, en hello **especificar objetivos a largo plazo** , seleccione cuánto tiempo desea que los datos de la cinta de tookeep (1-99 años). 
    1. Para **frecuencia de copia de seguridad**, seleccione con qué frecuencia se debe ejecutar tootape copia de seguridad. frecuencia de Hola se basa en la duración de retención de Hola que ha seleccionado:
        * Cuando la duración de retención de hello es 1-99 años, puede seleccionar las copias de seguridad toooccur diaria, semanal, quincenal, mensual, trimestral, semestral o anual.
        * Cuando la duración de retención de hello es 1-11 meses, puede seleccionar las copias de seguridad toooccur diaria, semanal, bisemanal o mensual.
        * Cuando la duración de retención de hello es 1-4 semanas, puede seleccionar las copias de seguridad toooccur diaria o semanal.

    2. En hello **seleccionar detalles de biblioteca y cinta** página, seleccione hello toouse de biblioteca y cinta, y si los datos deben estar comprimidos y cifrados.

7.  En hello **Revisar asignación de disco** página, revise el espacio de disco de grupo de almacenamiento de Hola que se asigna para el grupo de protección de Hola.

    1. **Total de tamaño de los datos** es Hola tamaño de datos de hello desea tooback.
    2. **Toobe de espacio en disco aprovisionado en el servidor de copia de seguridad de Azure** Hola espacio recomendado por el servidor de copia de seguridad para el grupo de protección de Hola. Servidor de copia de seguridad elige en función de la configuración de Hola de volumen de copia de seguridad ideal Hola. Sin embargo, puede modificar las opciones de copia de seguridad del volumen de hello en **detalles de asignación de disco**. 
    3. Para las cargas de trabajo, en el menú desplegable de hello, seleccione Hola almacenamiento que prefiera. Las modificaciones cambiarán los valores de hello de **almacenamiento Total** y **espacio de almacenamiento** en hello **almacenamiento en disco disponible** panel. Espacio insuficiente es la cantidad de Hola de almacenamiento que el servidor de copia de seguridad sugiere que agregar toohello volumen, las copias de seguridad tooensure suave.

8.  En hello **Seleccionar método de creación de réplica** , seleccione cómo desea que la replicación de datos completa inicial de toohandle Hola. Si elige tooreplicate a través de red de hello, recomendamos que elija una hora de poca actividad. Para grandes cantidades de datos o las condiciones de red que no sean óptimas, considere la posibilidad de replicar datos Hola sin conexión mediante un medio extraíble.

9. En hello **elegir opciones de comprobación de coherencia** página, seleccione cómo desea que tooautomate las comprobaciones de coherencia. Puede elegir una comprobación de toorun solo cuando los datos de réplica se vuelvan incoherentes, o según una programación. Si no desea que la comprobación de coherencia automáticas tooconfigure, puede ejecutar una comprobación manual en cualquier momento. una comprobación manual en hello toorun **protección** área de hello consola de administrador del servidor de copia de seguridad, haga clic en protección de hello grupo y, a continuación, seleccione **realizar comprobación de coherencia**.

10. Si ha seleccionado tooback seguridad toohello en la nube mediante copia de seguridad de Azure, en hello **especificar datos de protección en línea** página, asegúrese de que selecciona las cargas de trabajo de hello desea tooback una tooAzure.

11. En hello **especificar programación de copia de seguridad en línea** , seleccione las copias de seguridad incrementales con qué frecuencia se producirá tooAzure. Puede programar copias de seguridad toorun cada día, semana, mes y año y seleccione Hola fecha y hora en que debe ejecutarse. Las copias de seguridad se pueden producir una tootwice un día. Cada vez que se ejecuta una copia de seguridad, un punto de recuperación de datos se crea en Azure desde copia de Hola de los datos de copia de seguridad de hello almacenados en disco del servidor de copia de seguridad de Hola.

12. En hello **especificar directiva de retención en línea** , seleccione cómo se conservan los puntos de recuperación de Hola que se crean a partir de copias de seguridad diarias, semanales, mensuales y anuales de hello en Azure.

13. En hello **elegir la replicación en línea** , seleccione cómo se produce la replicación completa inicial de Hola de datos. Puede replicar a través de la red de Hola o hacer sin conexión (propagación sin conexión) de la copia de seguridad. Copia de seguridad sin conexión usa la característica de importación de Azure Hola. Para obtener más información, vea [Flujo de trabajo de copia de seguridad sin conexión en Azure Backup](backup-azure-backup-import-export.md).

14. En hello **resumen** página, revise la configuración. Después de seleccionar **crear grupo**, se produce la replicación inicial de datos de Hola. Cuando finalice la replicación de datos, en hello **estado** página, es el estado del grupo de protección de hello **Aceptar**. Copia de seguridad, a continuación, realiza por protección de hello grupo configuración.

## <a name="recover-system-state-or-bmr"></a>Recuperar el estado del sistema o BMR
Puede recuperar la ubicación de red de tooa estado BMR o del sistema. Si ha realizado una copia seguridad BMR, usar el entorno de recuperación de Windows (WinRE) toostart el sistema y conectarlo toohello red. A continuación, utilice toorecover de copia de seguridad de Windows Server desde la ubicación de red de Hola. Si ha realizado una copia seguridad de estado del sistema, utilice únicamente toorecover de copia de seguridad de Windows Server desde la ubicación de red de Hola.

### <a name="restore-bmr"></a>Restaurar BME
Ejecutar la recuperación en el equipo del servidor de copia de seguridad de hello:

1.  Hola **recuperación** panel, el equipo de Hola de búsqueda que desee toorecover y, a continuación, seleccione **reconstrucción completa**.

2.  Puntos de recuperación disponibles se indican en negrita en el calendario de Hola. Seleccione Hola fecha y hora de punto de recuperación de Hola que desea toouse.

3.  En hello **Seleccionar tipo de recuperación** , seleccione **copiar la carpeta de red de tooa.**

4.  En hello **especificar destino** página, seleccione donde desea que los datos de Hola de toocopy. Recuerde que ese destino seleccionado Hola necesita toohave espacio suficiente. Le recomendamos que cree una carpeta nueva.

5.  En hello **especificar opciones de recuperación** page, tooapply de configuración de seguridad de hello select. A continuación, seleccione si desea que la red de área de almacenamiento (SAN) de toouse-según las instantáneas de hardware, para una recuperación más rápida. (Esto es una opción sólo si tiene una red SAN con esta funcionalidad está disponible y Hola toocreate de capacidad y dividir un clon toomake se puede escribir. In Addition, hello equipo protegido y el equipo del servidor de copia de seguridad deben estar conectado toohello misma red.)

6.  Configure las opciones de notificación. En hello **confirmación** página, seleccione **recuperar**.

Configure la ubicación del recurso compartido de hello:

1.  En la ubicación de restauración hello, vaya toohello carpeta cuya copia de seguridad de Hola.

2.  Comparta la carpeta de Hola que está un nivel anterior WindowsImageBackup, para que la raíz de la carpeta compartida de Hola Hola sea carpeta WindowsImageBackup de Hola. Si no lo hace, restauración no encontrará la copia de seguridad de Hola. tooconnect utilizando el entorno de recuperación de Windows (WinRE), necesita un recurso compartido que puede tener acceso en WinRE con las credenciales y la dirección IP correcta de Hola.

Restaurar sistema hello:

1.  Hola se inicia el equipo en el que desea que toorestore Hola imagen mediante el uso de hello DVD de Windows para el sistema de hello va a restaurar.

2.  En la primera página de hello, compruebe la configuración de idioma y configuración regional. En hello **instalar** página, seleccione **reparar el equipo**.

3.  En hello **opciones de recuperación del sistema** página, seleccione **restaure el equipo con una imagen de sistema que creó anteriormente**.

4.  En hello **seleccionar una copia de seguridad de la imagen de sistema** , seleccione **seleccionar una imagen de sistema** > **avanzadas** > **busque un sistema imagen de red de hello**. Si aparece una advertencia, seleccione **Sí**. Paso toohello ruta del recurso compartido, escriba las credenciales de hello y, a continuación, seleccione el punto de recuperación de Hola. De este modo, se buscan las copias de seguridad específicas que estén disponibles en ese punto de recuperación. Seleccione el punto de recuperación de Hola que desea toouse.

5.  En hello **elegir cómo Hola copia de seguridad toorestore** página, seleccione **formatear y volver a particionar discos**. En la página siguiente de hello, compruebe la configuración. 

6.  restauración de hello toobegin, seleccione **finalizar**. Es necesario reiniciar.

### <a name="restore-system-state"></a>Restaurar el estado del sistema

Ejecute la recuperación en Backup Server:

1.  Hola **recuperación** panel, equipo de Hola de búsqueda que desee toorecover y, a continuación, seleccione **reconstrucción completa**.

2.  Puntos de recuperación disponibles se indican en negrita en el calendario de Hola. Seleccione Hola fecha y hora de punto de recuperación de Hola que desea toouse.

3.  En hello **Seleccionar tipo de recuperación** , seleccione **copiar la carpeta de red de tooa**.

4.  En hello **especificar destino** página, seleccione dónde desea toocopy Hola datos. Recuerde que ese destino seleccionado Hola necesita espacio suficiente. Le recomendamos que cree una carpeta nueva.

5.  En hello **especificar opciones de recuperación** page, tooapply de configuración de seguridad de hello select. A continuación, seleccione si desea toouse instantáneas de hardware basadas en SAN para una recuperación más rápida. (Esta es una opción únicamente si tiene una red SAN con esta funcionalidad y capacidad toocreate de Hola y dividir un clon toomake se puede escribir. In Addition, Hola equipo protegido y servidores de copia de seguridad deben estar conectado toohello misma red.)

6.  Configure las opciones de notificación. En hello **confirmación** página, seleccione **recuperar**.

Ejecute Copias de seguridad de Windows Server:

1.  Seleccione **Acciones** > **Recuperar** > **Este servidor** > **Siguiente**.

2.  Seleccione **otro servidor**, seleccione hello **especificar tipo de ubicación** página y, a continuación, seleccione **carpeta compartida remota**. Escriba hello toohello ruta de acceso que contiene el punto de recuperación de Hola.

3.  En hello **Seleccionar tipo de recuperación** , seleccione **estado del sistema**. 

4. En hello **seleccionar la ubicación de recuperación del estado del sistema** , seleccione **ubicación Original**.

5.  En hello **confirmación** página, seleccione **recuperar**. Después de la restauración de hello, reinicie el servidor de Hola.

6.  También puede ejecutar Hola restauración del estado del sistema en un símbolo del sistema. toodo, inicie copia de seguridad de Windows Server en el equipo de hello desea toorecover. identificador de versión de hello tooget, en un símbolo del sistema, escriba:```wbadmin get versions -backuptarget \<servername\sharename\>```

    Use la restauración de estado del sistema de hello versión identificador toostart Hola. En hello símbolo del sistema, escriba:```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Confirme que desea que la recuperación de hello toostart. Puede ver el proceso de hello en la ventana de símbolo del sistema de hello. Se crea un registro de restauración. Después de la restauración de hello, reinicie el servidor de Hola.

