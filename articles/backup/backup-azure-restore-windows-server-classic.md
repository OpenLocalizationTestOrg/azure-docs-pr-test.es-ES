---
title: "Hola a aaaRestore datos tooa Windows Server o cliente de Windows de Azure mediante el modelo de implementación clásica | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorestore desde un cliente de Windows o Windows Server."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>Restaurar archivos tooa Windows server o el equipo de cliente de Windows mediante el modelo de implementación clásica de Hola
> [!div class="op_single_selector"]
> * [Portal clásico](backup-azure-restore-windows-server-classic.md)
> * [Portal de Azure](backup-azure-restore-windows-server.md)
>
>

Este artículo explica cómo toorecover datos desde una copia de seguridad del almacén y restauración tooa servidor o equipo. A partir de marzo de 2017, ya no se pueden crear almacenes de copia de seguridad en el portal clásico de Hola.

> [!IMPORTANT]
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> **15 de octubre de 2017**, ya no estará almacenes de copia de seguridad de toocreate de toouse capaz de PowerShell. <br/> **A partir del 1 de noviembre de 2017**:
>- Los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

datos de toorestore, usar a Asistente para recuperar datos de hello en el agente de servicios de recuperación de Microsoft Azure (MARS) Hola. Al restaurar datos, es posible realizar las siguientes tareas:

* Restaurar datos toohello mismo equipo desde las copias de seguridad de Hola se tomaron.
* Restaurar datos tooan alternativo máquina.

En enero de 2017 Microsoft lanzó a un agente de MARS de toohello de actualización de vista previa. Junto con correcciones de errores, esta actualización permite restaurar instantánea, lo que permite toomount una instantánea de punto de recuperación puede escribir como un volumen de recuperación. A continuación, puede explorar Hola recuperación volumen y copia archivos tooa equipo local, por tanto, de forma selectiva restaurar archivos.

> [!NOTE]
> Hola [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) es necesario si desea toouse Restore instantáneo toorestore los datos. También se deben proteger los datos de copia de seguridad de hello en los almacenes en configuraciones regionales que aparecen en el artículo de soporte técnico de Hola. Consulte hello [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) para la lista más reciente de Hola de configuraciones regionales que admitan la restauración de instantánea. La restauración instantánea **no** está actualmente disponible en todas las configuraciones regionales.
>

Restauración de instantánea está disponible para su uso en los almacenes de servicios de recuperación en hello portal de Azure y almacenes de copia de seguridad en portal clásico de Hola. Si desea toouse Restore instantáneo, descargar la actualización de hello MARS y siga los procedimientos de Hola que mencionan restaurar instantánea.


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
    > Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante seis horas desde el momento de hello cuando donde se montó. No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola. Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.
    >


## <a name="recover-data-toohello-same-machine"></a>Recuperar datos toohello mismo equipo
Si ha eliminado accidentalmente un archivo y deseos toorestore se toohello al mismo equipo (de qué Hola se realiza copia de seguridad), Hola siguiendo los pasos le ayudarán a recuperar datos de Hola.

1. Abra hello **copia de seguridad de Microsoft Azure** ajuste en.
2. Haga clic en **recuperar datos** el flujo de trabajo de tooinitiate Hola.

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)
3. Seleccione hello  **este servidor (*nombreDelEquipo*) ** Hola de toorestore opción copia de archivo en hello misma máquina.

    ![Misma máquina](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. Elija demasiado**examinar archivos** o **buscar archivos**.

    Deje Hola predeterminado opción si tiene previsto toorestore uno o más archivos cuya ruta de acceso se conoce. Si no está seguro acerca de la estructura de carpetas de hello pero desea toosearch para un archivo, elegir hello **buscar archivos** opción. A fin de Hola de esta sección, se continuará con la opción predeterminada de Hola.

    ![Examinar archivos](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. Seleccione el volumen de Hola desde el que desea que el archivo de hello toorestore.

    Puede realizar la restauración a un momento dado. Las fechas que aparecen en **negrita** en control de calendario Hola indicar disponibilidad Hola de un punto de restauración. Una vez que se selecciona una fecha, en función de la programación de copia de seguridad (y el éxito de Hola de una operación de copia de seguridad), puede seleccionar un punto en el tiempo de hello **tiempo** de lista desplegable.

    ![Fecha y volumen](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. Seleccione Hola elementos toorecover. Puede seleccionar varias carpetas y archivos que se va toorestore.

    ![Seleccionar archivos](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. Especificar parámetros de recuperación de Hola.

    ![Opciones de recuperación](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * Tiene la opción de restauración toohello ubicación original (en qué Hola archivo o carpeta se sobrescribiría) o una ubicación de tooanother en hello mismo equipo.
   * Si Hola de archivo o carpeta que se va a toorestore existe en la ubicación de destino de hello, puede crear copias (dos versiones de hello mismo archivo), sobrescribir los archivos de hello en la ubicación de destino de Hola u omitir recuperación de Hola de archivos de Hola que existe en el destino de Hola.
   * Se recomienda que deje opción predeterminada Hola restaurar las ACL de hello en los archivos de Hola que se van a recuperar.
8. Una vez proporcionadas estas entradas, haga clic en **Siguiente**. Hola recuperación flujo de trabajo, que restaura una máquina de hello archivos toothis, se iniciará.

## <a name="recover-tooan-alternate-machine"></a>Recuperar máquina alternativo tooan
Si se pierde todo el servidor, todavía puede recuperar datos desde otro equipo de copia de seguridad de Azure tooa. Hola pasos muestra el flujo de trabajo de Hola.  

terminología de Hola que se usa en estos pasos se incluye:

* *Máquina de origen* : tomada máquina original de Hola desde la copia de seguridad de Hola y que no está disponible actualmente.
* *El equipo de destino* : se va a recuperar datos de saludo máquina toowhich Hola.
* *Almacén de ejemplo* : Hola Hola de toowhich de almacén de copia de seguridad *máquina de origen* y *equipo de destino* están registrados. <br/>

> [!NOTE]
> No se puede restaurar copias de seguridad realizadas desde un equipo en un equipo que está ejecutando una versión anterior del sistema operativo de Hola. Por ejemplo, si se realizan copias de seguridad de una máquina con Windows 7, esta puede restaurarse en un Windows 8 o una máquina con una versión superior. Sin embargo, al contrario de hello no cumplirse.
>
>

1. Abra hello **copia de seguridad de Microsoft Azure** ajuste en hello *equipo de destino*.
2. Asegúrese de que hello *equipo de destino* hello y *máquina de origen* están registrado toohello mismo almacén de copia de seguridad.
3. Haga clic en **recuperar datos** el flujo de trabajo de tooinitiate Hola.

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)
4. Seleccione **Otro servidor**

    ![Otro servidor](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. Proporcione el archivo de credenciales de almacén de hello correspondiente toohello *el almacén de ejemplo*. Si el archivo de credenciales de almacén de hello es válida (o expiró) descargar un nuevo archivo de credenciales de almacén de hello *almacén ejemplo* Hola portal de Azure clásico. Una vez que se proporciona el archivo de credenciales de almacén de hello, se muestra el almacén de copia de seguridad de hello en el archivo de credenciales de almacén de Hola.
6. Seleccione hello *máquina de origen* en lista de Hola de máquinas mostradas.

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. Seleccione cualquier hello **buscar archivos** o **examinar archivos** opción. Para el propósito de Hola de esta sección, se utilizará hello **buscar archivos** opción.

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. Seleccionar volumen hello y la fecha en la pantalla de bienvenida siguiente. Búsqueda de nombre de archivo/carpeta Hola desea toorestore.

    ![Buscar artículos](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. Seleccionar ubicación de Hola donde es necesario toobe restaurar archivos de Hola.

    ![Restaurar ubicación](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. Proporcione la frase de contraseña de cifrado de Hola que se proporcionó durante la *la máquina de origen* registro demasiado*el almacén de ejemplo*.

    ![Cifrado](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. Una vez que se proporciona la entrada de hello, haga clic en **recuperar**, qué desencadenadores Hola restauración de hello copia archivos toohello destino proporcionado.

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
    > Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante seis horas desde el momento de hello cuando donde se montó. No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola. Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.
    >


## <a name="next-steps"></a>Pasos siguientes
* [Preguntas más frecuentes de Copia de seguridad de Azure](backup-azure-backup-faq.md)
* Visite hello [foro de copia de seguridad de Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).

## <a name="learn-more"></a>Más información
* [Información general de Copia de seguridad de Azure](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [Copia de seguridad de máquinas virtuales de Azure](backup-azure-vms-introduction.md)
* [Copia de seguridad de las cargas de trabajo de Microsoft](backup-azure-dpm-introduction.md)
