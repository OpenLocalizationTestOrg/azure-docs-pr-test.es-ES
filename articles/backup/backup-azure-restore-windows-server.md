---
title: aaaRestore datos en Azure tooa Windows Server o un equipo de Windows | Documentos de Microsoft
description: "Obtenga información acerca de cómo se almacenan los datos de toorestore en tooa Azure Windows Server o un equipo de Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>Restaurar archivos tooa Windows server o el equipo de cliente de Windows mediante el modelo de implementación del Administrador de recursos
> [!div class="op_single_selector"]
> * [Portal de Azure](backup-azure-restore-windows-server.md)
> * [Portal clásico](backup-azure-restore-windows-server-classic.md)
>
>

Este artículo se explica cómo toorestore datos desde un almacén de copia de seguridad. datos de toorestore, usar a Asistente para recuperar datos de hello en el agente de servicios de recuperación de Microsoft Azure (MARS) Hola. Al restaurar datos, es posible realizar las siguientes tareas:

* Restaurar datos toohello mismo equipo desde las copias de seguridad de Hola se tomaron.
* Restaurar datos tooan alternativo máquina.

En enero de 2017 Microsoft lanzó a un agente de MARS de toohello de actualización de vista previa. Junto con correcciones de errores, esta actualización permite restaurar instantánea, lo que permite toomount una instantánea de punto de recuperación puede escribir como un volumen de recuperación. A continuación, puede explorar Hola recuperación volumen y copia archivos tooa equipo local, por tanto, de forma selectiva restaurar archivos.

> [!NOTE]
> Hola [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) es necesario si desea toouse Restore instantáneo toorestore los datos. También se deben proteger los datos de copia de seguridad de hello en los almacenes en configuraciones regionales que aparecen en el artículo de soporte técnico de Hola. Consulte hello [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) para la lista más reciente de Hola de configuraciones regionales que admitan la restauración de instantánea. La restauración instantánea **no** está actualmente disponible en todas las configuraciones regionales.
>

Restauración de instantánea está disponible para su uso en los almacenes de servicios de recuperación en hello portal de Azure y almacenes de copia de seguridad en portal clásico de Hola. Si desea toouse Restore instantáneo, descargar la actualización de hello MARS y siga los procedimientos de Hola que mencionan restaurar instantánea.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Use Restore instantáneo toorecover datos toohello mismo equipo

Si ha eliminado accidentalmente un archivo y deseos toorestore se toohello al mismo equipo (de qué Hola se realiza copia de seguridad), Hola siguiendo los pasos le ayudarán a recuperar datos de Hola.

1. Abra hello **copia de seguridad de Microsoft Azure** ajuste en. Si no sabe que se instaló el complemento de hello en, buscar Hola equipo o servidor para **copia de seguridad de Microsoft Azure**.

    aplicación de escritorio de Hello debe aparecer en los resultados de búsqueda de Hola.

2. Haga clic en **recuperar datos** Asistente de hello toostart.

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

3. En hello **Introducción** panel, toorestore Hola datos toohello mismo servidor o equipo, seleccione **este servidor (`<server name>`)** y haga clic en **siguiente**.

    ![Elija este toohello de datos de servidor opción toorestore Hola mismo equipo](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. En hello **seleccionar modo de recuperación** panel, elija **archivos y carpetas individuales** y, a continuación, haga clic en **siguiente**.

    ![Examinar archivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. En hello **Seleccionar volumen y fecha** panel, volumen de hello select que contiene los archivos de Hola o carpetas que desee toorestore.

    En el calendario de hello, seleccione un punto de recuperación. Puede realizar la restauración desde cualquier momento dado de recuperación. Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación. Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.

    ![Fecha y volumen](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. Una vez que haya elegido toorestore de punto de recuperación de hello, haga clic en **montar**.

    Copia de seguridad de Azure monta el punto de recuperación local de Hola y lo utiliza como un volumen de recuperación.

7. En hello **examinar y recuperar archivos** panel, haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee.

    ![Opciones de recuperación](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. En el Explorador de Windows, copia Hola archivos o carpetas desea toorestore y péguelos tooany ubicación local toohello servidor o equipo. Puede abrir o transmitir Hola archivos directamente desde el volumen de recuperación de Hola y comprobar Hola correcto de las versiones recuperadas.

    ![Copie y pegue los archivos y carpetas desde la ubicación de toolocal volumen montado](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. Cuando termine de restaurar los archivos de Hola o las carpetas, en hello **examinar y recuperación** panel, haga clic en **desmontar**. A continuación, haga clic en **Sí** tooconfirm que desea que el volumen de hello toounmount.

    ![Desmonte el volumen de Hola y confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante 6 horas desde el momento de hello cuando donde se montó. Sin embargo, el tiempo de montaje de hello es extendido hasta un máximo de 24 horas en el caso de una copia de archivos en curso. No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola. Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>Use Restore instantáneo toorestore datos tooan alternativo máquina
Si se pierde todo el servidor, todavía puede recuperar datos desde otro equipo de copia de seguridad de Azure tooa. Hola pasos muestra el flujo de trabajo de Hola.


terminología de Hola que se usa en estos pasos se incluye:

* *Máquina de origen* : tomada máquina original de Hola desde la copia de seguridad de Hola y que no está disponible actualmente.
* *El equipo de destino* : se va a recuperar datos de saludo máquina toowhich Hola.
* *Almacén de ejemplo* : Hola Hola de toowhich de almacén de servicios de recuperación *máquina de origen* y *equipo de destino* están registrados. <br/>

> [!NOTE]
> Las copias de seguridad no pueden ser restaurada tooa equipo de destino ejecuta una versión anterior del sistema operativo de Hola. Por ejemplo, una copia de seguridad perteneciente a un equipo con Windows 7 se puede restaurar en un equipo con Windows 8 o posterior. Una copia de seguridad desde un equipo Windows 8 no puede ser el equipo restaurado tooa Windows 7.
>
>

1. Abra hello **copia de seguridad de Microsoft Azure** ajuste en hello *equipo de destino*.

2. Asegúrese de hello *equipo de destino* hello y *máquina de origen* están registrado toohello mismos servicios de recuperación del almacén.

3. Haga clic en **recuperar datos** tooopen hello **Asistente para recuperar datos**.

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

4. En hello **Introducción** panel, seleccione **otro servidor**

    ![Otro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Proporcione el archivo de credenciales de almacén de hello correspondiente toohello *almacén ejemplo*y haga clic en **siguiente**.

    Si el archivo de credenciales de almacén de hello es válida (o expiró), descargue un nuevo archivo de credenciales de almacén de hello *almacén ejemplo* Hola portal de Azure. Una vez que proporcione una credencial de almacén válido, el nombre de Hola de hello que aparece de almacén de copia de seguridad correspondiente.


6. En hello **Seleccionar servidor de copia de seguridad** panel, seleccione hello *máquina de origen* en lista de Hola de máquinas mostradas y proporcionar la frase de contraseña de Hola. A continuación, haga clic en **Siguiente**.

    ![Lista de máquinas](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. En hello **seleccionar modo de recuperación** panel, seleccione **archivos y carpetas individuales** y haga clic en **siguiente**.

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. En hello **Seleccionar volumen y fecha** panel, volumen de hello select que contiene los archivos de Hola o carpetas que desee toorestore.

    En el calendario de hello, seleccione un punto de recuperación. Puede realizar la restauración desde cualquier momento dado de recuperación. Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación. Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.

    ![Buscar artículos](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. Haga clic en **montar** toolocally montaje el punto de recuperación de Hola como un volumen de recuperación en el *equipo de destino*.

10. En hello **examinar y recuperar archivos** panel, haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee.

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. En el Explorador de Windows, copie Hola archivos o carpetas del volumen de recuperación de Hola y péguelos tooyour *equipo de destino* ubicación. Puede abrir o transmitir Hola archivos directamente desde el volumen de recuperación de Hola y comprobar Hola correcto de las versiones recuperadas.

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. Cuando termine de restaurar los archivos de Hola o las carpetas, en hello **examinar y recuperación** panel, haga clic en **desmontar**. A continuación, haga clic en **Sí** tooconfirm que desea que el volumen de hello toounmount.

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante 6 horas desde el momento de hello cuando donde se montó. Sin embargo, el tiempo de montaje de hello es extendido hasta un máximo de 24 horas en el caso de una copia de archivos en curso. No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola. Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.
    >

## <a name="troubleshooting"></a>Solución de problemas
Si copia de seguridad de Azure no correctamente montar volúmenes de recuperación de hello incluso después de hacer clic en varios minutos **montar** o se produce un error toomount Hola recuperación volumen con uno o varios errores, siga los pasos de hello debajo toobegin recuperación normalmente.

1.  Cancelar el proceso de montaje en curso de hello en caso de que se ha estado ejecutando durante varios minutos.

2.  Asegúrese de que se encuentra en la versión más reciente de Hola de agente de copia de seguridad de Azure Hola. toofind información de versión de Hola de agente de copia de seguridad de Azure, haga clic en **sobre Microsoft Azure Backup Agent** en hello **acciones** panel de copia de seguridad de Microsoft Azure de la consola y asegúrese de que hello  **Versión** número es igual tooor superior de la versión de Hola mencionada en [este artículo](https://go.microsoft.com/fwlink/?linkid=229525). Puede descargar la versión más reciente de Hola desde [aquí](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  Vaya demasiado**el Administrador de dispositivos** -> **controladores de almacenamiento** y asegurarse de que puede encontrar **iniciador iSCSI de Microsoft**. Si puede encontrarlo, vaya directamente toostep 7 siguiente. 

4.  Si no encuentra el servicio de iniciador iSCSI de Microsoft como se mencionó en el paso 3, compruebe toosee si puede encontrar una entrada en **el Administrador de dispositivos** -> **controladores de almacenamiento** llama  **Los dispositivos desconocidos** con el Id. de Hardware **ROOT\ISCSIPRT**.

5.  Haga clic con el botón derecho en **Dispositivo desconocido** y seleccione **Actualizar software de controlador**.

6.  Actualizar el controlador de hello seleccionando la opción de hello demasiado **buscar software de controlador actualizado automáticamente**. Debe cambiar la finalización de la actualización de hello **dispositivo desconocido** demasiado**iniciador iSCSI de Microsoft** tal y como se muestra a continuación. 

    ![Cifrado](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  Vaya demasiado**el Administrador de tareas** -> **servicios (Local)** -> **servicio del iniciador iSCSI de Microsoft**. 

    ![Cifrado](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Reinicie el servicio de iniciador iSCSI de Microsoft de hello con el botón secundario en servicio de hello, haga clic en **detener** y haga clic en nuevo y haga clic en obtener más **iniciar**.

9.  Vuelva a intentar la recuperación mediante la restauración instantánea. 

Si sigue sin funcionar recuperación hello, reinicie al cliente y el servidor. Si no es deseable un reinicio o recuperación Hola sigue sin funcionar incluso después de reiniciar el servidor de hello, intente recuperar desde un equipo alternativo y póngase en contacto con soporte técnico de Azure, vaya demasiado[Portal de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) y enviar una solicitud de soporte técnico.

## <a name="next-steps"></a>Pasos siguientes
* Ahora que ha recuperado los archivos y las carpetas, puede [administrar las copias de seguridad](backup-azure-manage-windows-server.md).
