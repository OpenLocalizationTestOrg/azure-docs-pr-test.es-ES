---
title: "Azure Backup: restauración del estado del sistema a Windows Server | Microsoft Docs"
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
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="restore-system-state-to-windows-server"></a>Restauración del estado del sistema a Windows Server

En este artículo se explica cómo restaurar copias de seguridad del estado del sistema de Windows Server a partir un almacén de Azure Recovery Services. Para restaurar el estado del sistema, debe tener una copia de seguridad de dicho estado (creada siguiendo las instrucciones de [Copia de seguridad del estado del sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) y asegurarse de que ha instalado la [versión más reciente del agente de Microsoft Azure Recovery Services (MARS)](http://aka.ms/azurebackup_agent). La recuperación de datos del estado de sistema de Windows Server a partir de un almacén de Azure Recovery Services es un proceso que consta de dos pasos:

1. Restaurar el estado del sistema como archivos a partir de Azure Backup. Al restaurar el estado del sistema como archivos a partir de Azure Backup, puede:
  * Restaurar el estado de sistema en el mismo servidor de donde se tomaron las copias de seguridad, o
  * Restaurar el archivo de estado del sistema a un servidor alternativo.

2. Aplicar los archivos de estado del sistema restaurados a Windows Server.


## <a name="recover-system-state-files-to-the-same-server"></a>Recuperación de archivos de estado del sistema al mismo servidor
En los pasos siguientes se explica cómo revertir la configuración de Windows Server a un estado anterior. Revertir la configuración del servidor a un estado conocido y estable, puede ser muy importante. En los pasos siguientes se restaura el estado del sistema del servidor de un almacén de Recovery Services. 

1. Abra el complemento **Microsoft Azure Backup**. Si no conoce la ubicación donde se instaló el complemento, busque el equipo o servidor para **Microsoft Azure Backup**.

    La aplicación de escritorio debe aparecer en los resultados de búsqueda.

2. Haga clic en **Recuperar datos** para iniciar el asistente.

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

3. En el panel **Introducción**, para restaurar los datos en el mismo servidor o equipo, seleccione **Este servidor (`<server name>`)** y haga clic en **Siguiente**.

    ![Elegir la opción Este servidor para restaurar los datos en la misma máquina](./media/backup-azure-restore-system-state/samemachine.png)

4. En el panel **Seleccionar modo de recuperación**, seleccione **Estado del sistema** y luego haga clic en **Siguiente**.

    ![Examinar archivos](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. En el calendario, en el panel **Seleccionar volumen y fecha**, seleccione un punto de recuperación. 

    Puede realizar la restauración desde cualquier momento dado de recuperación. Las fechas en **negrita** indican la disponibilidad de al menos un punto de recuperación. Cuando selecciona una fecha, si están disponibles varios puntos de recuperación, elija el punto de recuperación específico desde el menú desplegable **Hora**.

    ![Fecha y volumen](./media/backup-azure-restore-system-state/select-date.png)

6. Una vez que haya elegido el punto de recuperación para restaurar, haga clic en **Siguiente**.

    Azure Backup monta el punto de recuperación local y lo usa como volumen de recuperación.

7. En el siguiente panel, especifique el destino de los archivos de estado del sistema recuperados y haga clic en **Examinar** para abrir el Explorador de Windows y busque los archivos y carpetas que desea. La opción **Crear copias para tener ambas versiones** , crea copias de los archivos individuales en un conjunto de archivos de estado del sistema existente en lugar de crear la copia de todo ese conjunto de archivos.

    ![Opciones de recuperación](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Compruebe los detalles de recuperación en el panel **Confirmación** y haga clic en **Recuperar**.

   ![Hacer clic en Recuperar para confirmar la acción de recuperación](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Copie el directorio *WindowsImageBackup* del destino de recuperación en un volumen no crítico del servidor. Normalmente, el volumen del SO Windows es el volumen crítico.

10. Una vez que la recuperación se haya realizado correctamente, siga los pasos descritos en la sección [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server) (Aplicación de los archivos de estado del sistema restaurados en Windows Server), para completar el proceso de recuperación del estado del sistema.

## <a name="recover-system-state-files-to-an-alternate-server"></a>Recuperación de los archivos de estado del sistema a un servidor alternativo

Si Windows Server está dañado o no se puede acceder a él y desea restaurarlo a un estado estable recuperando el estado del sistema de Windows Server, puede restaurar el estado del sistema del servidor dañado desde otro servidor. Utilice los pasos siguientes para restaurar el estado del sistema en un servidor independiente.  

La terminología usada en estos pasos incluye:

- *Máquina de origen* : es la máquina original desde la que se realizó la copia de seguridad y que no está disponible actualmente.
- *Máquina de destino* : es la máquina en la que se recuperan los datos.
- *Almacén de ejemplo*: el almacén de Recovery Services en el que se registran la*máquina de origen* y la *máquina de destino*. <br/>

> [!NOTE]
> Las copias de seguridad tomadas de una máquina no se pueden restaurar en una máquina que esté ejecutando una versión anterior del sistema operativo. Por ejemplo, las copias de seguridad tomadas de una máquina con Windows Server 2016 no se pueden restaurar en Windows Server 2012 R2. Sin embargo, el proceso inverso sí es posible. Puede usar copias de seguridad de Windows Server 2012 R2 para restaurar Windows Server 2016.
>

1. Abra el complemento **Microsoft Azure Backup** en la *Máquina de destino*.
2. Asegúrese de que tanto la *máquina de destino* como la *máquina de origen* están registradas en el mismo almacén de Recovery Services.
3. Haga clic en **Recuperar datos** para iniciar el flujo de trabajo.

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Seleccione **Otro servidor**

    ![Otro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. Proporcione el archivo de credenciales de almacén que se corresponde con el *Almacén de ejemplo*. Si el archivo de credenciales de almacén no es válido (o ha expirado), descargue un nuevo archivo de credenciales de almacén desde el *Almacén de ejemplo* en Azure Portal. Después de proporcionar el archivo de credenciales del almacén, se muestra el almacén de Recovery Services asociado a dicho archivo.

6. En el panel Seleccionar servidor de copia de seguridad, seleccione la *máquina de origen* en la lista de máquinas mostradas.

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. En el panel Seleccionar modo de recuperación, seleccione **Estado del sistema** y, luego, haga clic en **Siguiente**. 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. En el calendario, en el panel **Seleccionar volumen y fecha**, seleccione un punto de recuperación. Puede realizar la restauración desde cualquier momento dado de recuperación. Las fechas en **negrita** indican la disponibilidad de al menos un punto de recuperación. Cuando selecciona una fecha, si están disponibles varios puntos de recuperación, elija el punto de recuperación específico desde el menú desplegable **Hora**. 

    ![Buscar artículos](./media/backup-azure-restore-system-state/select-date.png)

9. Una vez que haya elegido el punto de recuperación para restaurar, haga clic en **Siguiente**.

10. En el panel **Seleccionar el modo de recuperación del Estado de sistema**, especifique el destino donde desea que los archivos de estado del sistema se recuperen. A continuación, haga clic en **Siguiente**.

    ![Cifrado](./media/backup-azure-restore-system-state/recover-as-files.png)

    La opción **Crear copias para tener ambas versiones** , crea copias de los archivos individuales en un conjunto de archivos de estado del sistema existente en lugar de crear la copia de todo ese conjunto de archivos.

11. Compruebe los detalles de recuperación en el panel Confirmación y haga clic en **Recuperar**. 

    ![Hacer clic en el botón Recuperar para confirmar el proceso de recuperación](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Copie el directorio *WindowsImageBackup* en un volumen no crítico del servidor (por ejemplo, D:\). Normalmente, el volumen del SO Windows es el volumen crítico.

13. Para completar el proceso de recuperación, utilice la siguiente sección para [aplicar los archivos de estado del sistema restaurados en Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Aplicación del estado del sistema restaurado a Windows Server

Una vez que haya recuperado el estado del sistema como archivos con el agente de Azure Recovery Services, emplee la utilidad Copias de seguridad de Windows Server para aplicar el estado del sistema recuperado a Windows Server. La utilidad Copias de seguridad de Windows Server ya está disponible en el servidor. En los pasos siguientes se explica cómo aplicar el estado del sistema recuperado.

1. Use los siguientes comandos para reiniciar el servidor en *Modo de reparación de servicios de directorio*. En un símbolo del sistema con privilegios elevados:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Después del reinicio, abra el complemento Copias de seguridad de Windows Server. Si no conoce la ubicación donde se instaló el complemento, busque **Copias de seguridad de Windows Server** en el equipo o servidor.

    La aplicación de escritorio aparece en los resultados de la búsqueda.

3. En el complemento, seleccione **Copia de seguridad local**.

    ![Seleccionar la copia de seguridad local para restaurar desde aquí](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. En la consola Copia de seguridad Local, en **Panel acciones**, haga clic en **Recuperar** para abrir el Asistente para recuperación.

5. Seleccione la opción **Una copia de seguridad almacenada en otra ubicación** y haga clic en **Siguiente**.

   ![Optar por realizar la recuperación en un servidor diferente](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Cuando especifique el tipo de ubicación, seleccione **Carpeta compartida remota** si la copia de seguridad del estado del sistema se recuperó en otro servidor. Si el estado del sistema se recuperó localmente, seleccione **Unidades locales**. 

    ![Seleccionar si se desea realizar la recuperación desde el servidor local o desde otro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Escriba la ruta de acceso al directorio *WindowsImageBackup* o elija la unidad local que contiene este directorio (por ejemplo, D:\WindowsImageBackup), recuperado como parte de la recuperación de archivos de estado del sistema mediante el agente de Azure Recovery Services, y haga clic en **Siguiente**.

    ![Ruta de acceso al archivo compartido](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Seleccione la versión de estado del sistema que desea restaurar y haga clic en **Siguiente**.

9. En el panel Seleccionar tipo de recuperación, seleccione **Estado del sistema** y, luego, haga clic en **Siguiente**.

10. Para la ubicación de Recuperación de estado del sistema, seleccione **Ubicación original** y haga clic en **Siguiente**.

11. Revise los detalles de confirmación, compruebe la configuración de reinicio y haga clic en **Recuperar** para aplicar los archivos del estado del sistema restaurado.

    ![Inicio de la restauración de los archivos de estado del sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Consideraciones especiales para la recuperación del estado del sistema en el servidor de Active Directory

La copia de seguridad del estado del sistema incluye datos de Active Directory. Siga estos pasos para restaurar Active Directory Domain Services (AD DS) de su estado actual a un estado anterior.

1. Reinicie el controlador de dominio en Modo de restauración de servicios de directorio (DSRM).
2. Siga los pasos que aparecen [aquí](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) para usar cmdlets de Copias de seguridad de Windows Server para recuperar AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Solución de problemas en la restauración del estado del sistema

Si el proceso anterior consistente en aplicar el estado del sistema no se completa correctamente, use el Entorno de recuperación de Windows (Win RE) para recuperar Windows Server. En los siguientes pasos se explica cómo realizar la recuperación mediante Win RE. Utilice esta opción solo si Windows Server no se inicia normalmente después de una restauración del estado del sistema. El siguiente proceso borra datos que no son del sistema; extreme las precauciones. 

1. Arranque Windows Server en el Entorno de recuperación de Windows (Win RE).

2. En las tres opciones disponibles, seleccione Solucionar problemas.

    ![Apertura del menú](./media/backup-azure-restore-system-state/winre-1.png)

3. En la pantalla **Opciones avanzadas**, seleccione **Símbolo del sistema** y proporcione el nombre de usuario y la contraseña del administrador del servidor.

   ![Apertura del menú](./media/backup-azure-restore-system-state/winre-2.png)

4. Proporcione el nombre de usuario y la contraseña del administrador del servidor.

    ![Apertura del menú](./media/backup-azure-restore-system-state/winre-3.png)

5. Al abrir el símbolo del sistema en modo de administrador, ejecute el siguiente comando para obtener las versiones de copia de seguridad del estado del sistema.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. Ejecute el siguiente comando para obtener todos los volúmenes disponibles en la copia de seguridad.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. El comando siguiente recupera todos los volúmenes que forman parte de la copia de seguridad del estado del sistema. Tenga en cuenta que este paso solo recupera los volúmenes críticos que forman parte del estado del sistema. Se borran todos los datos que no son del sistema.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Pasos siguientes
* Ahora que ha recuperado los archivos y las carpetas, puede [administrar las copias de seguridad](backup-azure-manage-windows-server.md).
