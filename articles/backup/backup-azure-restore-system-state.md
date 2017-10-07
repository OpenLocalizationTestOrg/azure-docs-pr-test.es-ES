---
title: "Copia de seguridad de Azure: Tooa de estado del sistema de restauración Windows Server | Documentos de Microsoft"
description: "Explicación detallada para restaurar el estado de sistema de Windows Server a partir de una copia de seguridad en Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>Estado del sistema de restauración tooWindows Server

Este artículo explica cómo del almacén de copias de seguridad de estado del sistema de Windows Server de toorestore desde los servicios de recuperación de Azure. toorestore estado del sistema, debe tener una copia de seguridad de estado del sistema (creadas utilizando las instrucciones de hello en [estado del sistema de copia de seguridad](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) y asegúrese de que ha instalado hello [versión más reciente del programa Hola a Microsoft Azure Recovery El agente de servicios (MARS)](http://aka.ms/azurebackup_agent). La recuperación de datos del estado de sistema de Windows Server a partir de un almacén de Azure Recovery Services es un proceso que consta de dos pasos:

1. Restaurar el estado del sistema como archivos a partir de Azure Backup. Al restaurar el estado del sistema como archivos a partir de Azure Backup, puede:
  * Estado del sistema de restauración toohello mismo servidor donde se han realizado copias de seguridad de hello, o
  * Servidor alternativo de estado del sistema de restauración archivo tooan.

2. Aplicar tooa de archivos de hello Restaurar estado del sistema Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Recuperar el estado del sistema de archivos toohello mismo servidor
Hola pasos explica cómo hacer copia de su estado anterior de Windows Server configuration tooa tooroll. Poner al servidor de configuración tooa espera, estable estado conocido, puede ser muy importante. Hola después de estado del sistema del servidor de pasos restauración Hola desde un almacén de servicios de recuperación. 

1. Abra hello **copia de seguridad de Microsoft Azure** complemento. Si no sabe donde se instaló el complemento hello, buscar Hola equipo o servidor para **copia de seguridad de Microsoft Azure**.

    aplicación de escritorio de Hello debe aparecer en los resultados de búsqueda de Hola.

2. Haga clic en **recuperar datos** Asistente de hello toostart.

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

3. En hello **Introducción** panel, toorestore Hola datos toohello mismo servidor o equipo, seleccione **este servidor (`<server name>`)** y haga clic en **siguiente**.

    ![Elija este toohello de datos de servidor opción toorestore Hola mismo equipo](./media/backup-azure-restore-system-state/samemachine.png)

4. En hello **seleccionar modo de recuperación** panel, elija **estado del sistema** y, a continuación, haga clic en **siguiente**.

    ![Examinar archivos](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. En el calendario de hello en **Seleccionar volumen y fecha** punto del panel, seleccione una recuperación. 

    Puede realizar la restauración desde cualquier momento dado de recuperación. Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación. Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.

    ![Fecha y volumen](./media/backup-azure-restore-system-state/select-date.png)

6. Una vez que haya elegido toorestore de punto de recuperación de hello, haga clic en **siguiente**.

    Copia de seguridad de Azure monta el punto de recuperación local de Hola y lo utiliza como un volumen de recuperación.

7. En el panel siguiente de hello, especifique el destino de Hola para hello recupera archivos de estado del sistema y haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee. Hola opción, **crear copias para tener ambas versiones**, crea copias de los archivos individuales en un archivo de archivo de estado del sistema existente en lugar de crear la copia de hello del archivo de estado del sistema completo de Hola.

    ![Opciones de recuperación](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Compruebe los detalles de Hola de recuperación en hello **confirmación** panel y haga clic en **recuperar**.

   ![Haga clic en recuperar tooacknowledge Hola recuperar acción](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Hola copia *WindowsImageBackup* directorio hello las no críticas volumen de tooa del destino de recuperación del servidor de Hola. Hola volumen del sistema operativo de Windows suele ser de los volúmenes imprescindibles Hola.

10. Una vez que la recuperación de hello es correcta, siga los pasos de hello en la sección de hello, [aplicar restaura toohello de archivos de estado del sistema Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), hello toocomplete proceso de recuperación de estado del sistema.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Recuperar el estado del sistema de archivos de servidor alternativo tooan

Si el servidor de Windows está dañado o es inaccesible y desea toorestore lo Hola de estado estable de tooa mediante la recuperación de estado de sistema de Windows Server, puede restaurar el estado del sistema del servidor dañado Hola desde otro servidor. Usar hello siguiendo los pasos para restaurar toohello estado del sistema en un servidor independiente.  

terminología de Hola que se usa en estos pasos se incluye:

- *Máquina de origen* : tomada máquina original de Hola desde la copia de seguridad de Hola y que no está disponible actualmente.
- *El equipo de destino* : se va a recuperar datos de saludo máquina toowhich Hola.
- *Almacén de ejemplo* : Hola Hola de toowhich de almacén de servicios de recuperación *máquina de origen* y *equipo de destino* están registrados. <br/>

> [!NOTE]
> Copias de seguridad de un equipo no pueden ser máquina restaurada tooa ejecuta una versión anterior del sistema operativo de Hola. Por ejemplo, copias de seguridad realizadas desde un equipo no puede ser de Windows Server 2016 restauran tooWindows Server 2012 R2. Sin embargo, la inversa de hello es posible. Puede usar copias de seguridad de Windows Server 2012 R2 toorestore Windows Server 2016.
>

1. Abra hello **copia de seguridad de Microsoft Azure** complemento en hello *equipo de destino*.
2. Asegúrese de que hello *equipo de destino* hello y *máquina de origen* están registrado toohello mismos servicios de recuperación del almacén.
3. Haga clic en **recuperar datos** el flujo de trabajo de tooinitiate Hola.

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Seleccione **Otro servidor**

    ![Otro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. Proporcione el archivo de credenciales de almacén de hello correspondiente toohello *el almacén de ejemplo*. Si el archivo de credenciales de almacén de hello es válida (o expiró), descargue un nuevo archivo de credenciales de almacén de hello *almacén ejemplo* Hola portal de Azure. Una vez que se proporciona el archivo de credenciales de almacén de hello, aparece el almacén de servicios de recuperación de hello asociado con el archivo de credenciales de almacén de Hola.

6. En el panel de seleccionar el servidor de copia de seguridad de hello, seleccione hello *máquina de origen* en lista de Hola de máquinas mostradas.

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. En el panel de seleccionar el modo de recuperación de hello, elija **estado del sistema** y haga clic en **siguiente**. 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. En el calendario de Hola Hola **Seleccionar volumen y fecha** punto del panel, seleccione una recuperación. Puede realizar la restauración desde cualquier momento dado de recuperación. Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación. Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable. 

    ![Buscar artículos](./media/backup-azure-restore-system-state/select-date.png)

9. Una vez que haya elegido toorestore de punto de recuperación de hello, haga clic en **siguiente**.

10. En hello **seleccionar un modo de recuperación de estado de sistema** panel, especificar destino de hello en el que desea toobe recuperar archivos de estado del sistema, a continuación, haga clic en **siguiente**.

    ![Cifrado](./media/backup-azure-restore-system-state/recover-as-files.png)

    Hola opción, **crear copias para tener ambas versiones**, crea copias de los archivos individuales en un archivo de archivo de estado del sistema existente en lugar de crear la copia de hello del archivo de estado del sistema completo de Hola.

11. Compruebe los detalles de Hola de recuperación en el panel de la confirmación de Hola y haga clic en **recuperar**. 

    ![Haga clic en el proceso de recuperación de hello recuperar botón tooconfirm Hola](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Hola copia *WindowsImageBackup* tooa no críticos volumen de directorio del servidor de hello (por ejemplo, D:\). Hola volumen del sistema operativo de Windows suele ser de los volúmenes imprescindibles Hola.

13. proceso de recuperación de toocomplete hello, use siguiente de hello sección demasiado[Hola restaurar archivos de estado del sistema en un servidor de Windows se aplican](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Aplicación del estado del sistema restaurado a Windows Server

Una vez se ha recuperado el estado del sistema como archivos con el agente de servicios de recuperación de Azure, use Hola copias de seguridad de Windows Server utilidad tooapply Hola recuperarse tooWindows de estado del sistema servidor. Hola utilidad de copia de seguridad de Windows Server ya está disponible en el servidor de Hola. Hola pasos explica cómo hello tooapply recupera el estado del sistema.

1. Siguiente de hello use comandos tooreboot el servidor en *modo de reparación de servicios de directorio*. En un símbolo del sistema con privilegios elevados:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Después del reinicio de hello, abra complemento Hola copias de seguridad de Windows Server. Si no sabe donde se instaló el complemento hello, buscar Hola equipo o servidor para **copias de seguridad de Windows Server**.

    aplicación de escritorio de Hello aparece en los resultados de búsqueda de Hola.

3. En el complemento de hello, seleccione **copia de seguridad Local**.

    ![Seleccione toorestore de copia de seguridad Local desde allí](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. En la consola de copia de seguridad Local de hello, Hola **panel acciones**, haga clic en **recuperar** tooopen Hola Asistente para recuperación.

5. Seleccione la opción de hello, **una copia de seguridad almacenada en otra ubicación**y haga clic en **siguiente**.

   ![Elija otro servidor de toorecover tooa](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Cuando se especifica el tipo de ubicación de hello, seleccione **carpeta compartida remota** si la copia de seguridad de estado del sistema se ha recuperado tooanother server. Si el estado del sistema se recuperó localmente, seleccione **Unidades locales**. 

    ![Seleccione si toorecovery desde el servidor local o en otro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Escriba Hola ruta de acceso toohello *WindowsImageBackup* directorio, o elija Hola unidad local que contiene este directorio (por ejemplo, D:\WindowsImageBackup), que se recupera como parte de la recuperación de archivos de estado del sistema de hello mediante la recuperación de Azure Servicios de agente y haga clic en **siguiente**.

    ![ruta de acceso compartido archivo de toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Versión de estado del sistema seleccione Hola que desee toorestore y haga clic en **siguiente**.

9. En panel de hello Seleccionar tipo de recuperación, seleccione **estado del sistema** y haga clic en **siguiente**.

10. Para la ubicación de Hola de hello recuperación del estado del sistema, seleccione **ubicación Original**y haga clic en **siguiente**.

11. Revise los detalles de confirmación de hello, compruebe la configuración de reinicio de Hola y haga clic en **recuperar** tooapplly Hola restaura archivos de estado del sistema.

    ![Hola iniciar Restaurar archivos de estado del sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Consideraciones especiales para la recuperación del estado del sistema en el servidor de Active Directory

La copia de seguridad del estado del sistema incluye datos de Active Directory. Usar hello siguiendo los pasos toorestore los servicios de dominio de Active Directory (AD DS) de su estado anterior de tooa de estado actual.

1. Reinicie el controlador de dominio de hello en el modo de restauración de servicios de directorio (DSRM).
2. Siga los pasos de hello [aquí](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover de cmdlets de copias de seguridad de Windows Server toouse AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Solución de problemas en la restauración del estado del sistema

Si el proceso anterior de Hola de aplicar el estado del sistema no se completa correctamente, use hello toorecover de entorno de recuperación de Windows (Windows RE) el servidor de Windows. Hello pasos siguientes se explica cómo toorecover con Windows RE. Utilice esta opción solo si Windows Server no se inicia normalmente después de una restauración del estado del sistema. Hola siguiendo proceso borra datos no son del sistema, tenga cuidado. 

1. Arranque el servidor de Windows en hello entorno de recuperación de Windows (Windows RE).

2. Seleccione la solución de problemas de tres opciones disponibles de Hola.

    ![Apertura del menú](./media/backup-azure-restore-system-state/winre-1.png)

3. De hello **opciones avanzadas** pantalla, seleccione **símbolo** y proporcione el nombre de usuario de administrador de servidor de hello y una contraseña.

   ![Apertura del menú](./media/backup-azure-restore-system-state/winre-2.png)

4. Proporcionar el nombre de usuario de administrador de servidor de hello y una contraseña.

    ![Apertura del menú](./media/backup-azure-restore-system-state/winre-3.png)

5. Al abrir símbolo del sistema de hello en modo de administrador, ejecutar las siguientes versiones de copia de seguridad de estado del sistema de comando tooget Hola.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. Ejecute hello después comando tooget todos los volúmenes disponibles en la copia de seguridad de Hola.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. Hello comando siguiente recupera todos los volúmenes que forman parte del programa Hola a copia de seguridad de estado del sistema. Tenga en cuenta que este paso recupera solo Hola volúmenes críticos que forman parte del estado del sistema Hola. Se borran todos los datos que no son del sistema.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Pasos siguientes
* Ahora que ha recuperado los archivos y las carpetas, puede [administrar las copias de seguridad](backup-azure-manage-windows-server.md).
