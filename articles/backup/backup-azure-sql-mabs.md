---
title: aaaAzure copia de seguridad para las cargas de trabajo de SQL Server utilizando el servidor de copia de seguridad de Azure | Documentos de Microsoft
description: "Un toobacking de introducción de las bases de datos de SQL Server utilizando el servidor de copia de seguridad de Azure"
services: backup
documentationcenter: 
author: pvrk
manager: Shivamg
editor: 
ms.assetid: c8b1f7ec-26b1-4ef0-a3f2-91aec959daea
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3a94338e8aca3f9d8611a72bcd223397ffb96f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-with-azure-backup-server"></a>Hacer copia de seguridad de SQL Server tooAzure con el servidor de copia de seguridad de Azure
En este artículo le guiará por los pasos de configuración de Hola para copia de seguridad de bases de datos de SQL Server mediante la copia de seguridad servidor de Microsoft Azure (MABS).

administración de Hola de tooAzure de copia de seguridad de base de datos de SQL Server y la recuperación de Azure implica tres pasos:

1. Crear un tooAzure de bases de datos de SQL Server de tooprotect de directiva de copia de seguridad.
2. Crear copias de seguridad a petición tooAzure.
3. Recuperar base de datos de Hola de Azure.

## <a name="before-you-start"></a>Antes de comenzar
Antes de comenzar, asegúrese de que tiene [instalado y preparado Hola servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md).

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Crear un tooAzure de bases de datos de SQL Server de directiva de copia de seguridad tooprotect
1. En la interfaz de usuario del servidor de copia de seguridad de Azure hello, haga clic en hello **protección** área de trabajo.
2. En la cinta de opciones de herramienta de hello, haga clic en **New** toocreate un nuevo grupo de protección.

    ![Creación de un grupo de protección](./media/backup-azure-backup-sql/protection-group.png)
3. MABS muestra la pantalla de inicio de hello con las guías de hello acerca de cómo crear un **grupo de protección**. Haga clic en **Siguiente**.
4. Seleccione **Servidores**.

    ![Selección de tipo de grupo de protección - 'Servidores'](./media/backup-azure-backup-sql/pg-servers.png)
5. Expanda el equipo con SQL Server Hola donde hello las bases de datos toobe copia de seguridad están presentes. MABS muestra varios orígenes de datos de los que se puede hacer copias de seguridad desde ese servidor. Expanda hello **todos los recursos compartidos de SQL** y seleccione las bases de datos de hello (en este caso se seleccionan ReportServer$ MSDPM2012 y ReportServer$ MSDPM2012TempDB) toobe copia de seguridad. Haga clic en **Siguiente**.

    ![Selección de base de datos SQL](./media/backup-azure-backup-sql/pg-databases.png)
6. Proporcione un nombre para el grupo de protección de Hola y seleccione hello **deseo protección en línea** casilla de verificación.

    ![Método de protección de datos: disco a corto plazo y en línea de Azure](./media/backup-azure-backup-sql/pg-name.png)
7. Hola **especificar objetivos a corto plazo** pantalla, incluya Hola entradas necesarias toocreate puntos de copia de seguridad toodisk.

    Aquí vemos que **duración de retención** se establece demasiado*5 días*, **frecuencia de sincronización** se establece tooonce cada *15 minutos* que es hello frecuencia con la que se realizó la copia de seguridad. **Copia de seguridad completa rápida** se establece demasiado*8:00 P.M*.

    ![Objetivos a corto plazo](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > A las 8:00 P.M. (según la entrada de pantalla de toohello) se crea cada día a un punto de copia de seguridad mediante la transferencia de datos de Hola que se ha modificado de hello punto de copia de seguridad de 8:00 P.M. del día anterior. Este proceso se denomina **Copia de seguridad completa rápida**. Mientras se sincronizan los registros de transacciones de hello cada 15 minutos, si hay una base de datos de necesidad toorecover Hola a las 9:00 P.M. –, a continuación, se crea el punto de hello mediante la reproducción de registros de Hola de hello express última copia de seguridad completa, seleccione (8 pm en este caso).
   >
   >

8. Haga clic en **Siguiente**

    Se muestra en MABS Hola general espacio de almacenamiento disponible y utilización del espacio de disco posibles de Hola.

    ![Asignación de disco](./media/backup-azure-backup-sql/pg-storage.png)

    De forma predeterminada, MABS crea un volumen por origen de datos (base de datos de SQL Server) que se usa para la copia de seguridad inicial de Hola. Con este enfoque, el Administrador de discos lógicos (LDM) de Hola limita orígenes de datos de too300 MABS protección (bases de datos de SQL Server). toowork solucionar esta limitación, seleccione hello **colocar datos en bloque de almacenamiento de DPM**, opción. Si utiliza esta opción, MABS utiliza un único volumen para varios orígenes de datos, lo que permite MABS tooprotect seguridad too2000 bases de datos SQL.

    Si **expandir automáticamente los volúmenes de hello** opción está seleccionada, MABS puede tener en cuenta para el volumen de copia de seguridad de hello aumenta a medida que crecen de datos de producción de hello. Si **expandir automáticamente los volúmenes de hello** opción no está activada, MABS limita Hola orígenes de datos de toohello de almacenamiento de copia de seguridad utilizado en el grupo de protección de Hola.
9. Elección de Hola de transferencia de evitar esta congestión de ancho de banda tooavoid inicial de copia de seguridad manualmente (fuera de red) o a través de red de Hola se otorgan a los administradores. También puede configurar tiempo de hello en qué Hola puede ocurrir transferencia inicial. Haga clic en **Siguiente**.

    ![Método de replicación inicial](./media/backup-azure-backup-sql/pg-manual.png)

    copia de seguridad inicial de Hello requiere a transferencia Hola completa del origen de datos (base de datos de SQL Server) desde tooMABS (máquina de SQL Server) del servidor de producción. Estos datos pueden ser grandes y transferir datos de Hola por red Hola pudieron superar el ancho de banda. Por este motivo, los administradores pueden elegir la copia de seguridad inicial de tootransfer Hola: **manualmente** (mediante un medio extraíble) tooavoid congestión del ancho de banda, o **automáticamente a través de la red de hello** (en un determinado hora).

    Una vez completada la copia de seguridad inicial de hello, el resto de Hola de copias de seguridad de hello son copias de seguridad incrementales en la copia de seguridad inicial de Hola. Copias de seguridad incrementales suelen toobe pequeño y se transfieren fácilmente a través de la red de Hola.
10. Elija si desea que toorun de comprobación de coherencia de Hola y haga clic en **siguiente**.

    ![Comprobación de coherencia](./media/backup-azure-backup-sql/pg-consistent.png)

    MABS puede realizar una coherencia comprobar toocheck Hola la integridad del punto de copia de seguridad de Hola. Calcula la suma de comprobación de hello del archivo de copia de seguridad de hello en el servidor de producción de hello (máquina de SQL Server en este escenario) y datos de copia de seguridad de Hola para ese archivo en MABS. En caso de hello de conflicto, se supone que hello en MABS el archivo de copia de seguridad está dañado. MABS rectificar datos de copia de seguridad de hello mediante el envío de bloques de hello correspondiente toohello incoherencia de suma de comprobación. Como la comprobación de coherencia hello es una operación de rendimiento intensivo, los administradores tienen la opción de Hola de programación de comprobación de coherencia de Hola o ejecutarlo automáticamente.
11. toospecify protección en línea de orígenes de datos de hello, seleccione hello toobe de bases de datos protegido tooAzure y haga clic en **siguiente**.

    ![Selección de orígenes de datos](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Los administradores pueden elegir las programaciones de copia de seguridad y las directivas de retención que se ajusten a las directivas de la organización.

    ![Programación y retención](./media/backup-azure-backup-sql/pg-schedule.png)

    En este ejemplo, las copias de seguridad se realizan una vez al día a 12:00 P.M. y las 8 P.M. (parte inferior de la pantalla de bienvenida)

    > [!NOTE]
    > Es una buena práctica toohave algunos puntos de recuperación a corto plazo en disco para una rápida recuperación. Estos puntos de recuperación se utilizan para la "recuperación operacional". Azure actúa como una ubicación válida fuera de sitio con unos contratos de nivel de servicio mayores y una disponibilidad garantizada.
    >
    >

    **Procedimiento recomendado**: asegúrese de que se programan copias de seguridad de Azure tras la finalización de Hola de copias de seguridad de disco local con DPM. Esto permite hello tooAzure de toobe de copia de seguridad copia de disco más reciente.

13. Elegir programación hello de la directiva de retención. se proporcionan detalles de Hello sobre el funcionamiento de la directiva de retención de hello en [tooreplace de copia de seguridad de Azure Use el artículo de la infraestructura de cinta](backup-azure-backup-cloud-as-tape.md).

    ![Directiva de retención](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    En este ejemplo:

    * Las copias de seguridad se realizan una vez al día al 12:00 P.M. y las 8 P.M. (parte inferior de la pantalla de bienvenida) y se conservan durante 180 días.
    * copia de seguridad de Hello en sábado a las 12:00 p. M. se conserva durante 104 semanas
    * copia de seguridad de Hello en último sábado a las 12:00 p. M. se conserva durante 60 meses
    * copia de seguridad de Hello en último sábado de marzo a las 12:00 p. M. se conserva durante 10 años
14. Haga clic en **siguiente** y seleccione Hola opción apropiada para transferir hello tooAzure de copia de seguridad inicial. Puede elegir **automáticamente a través de la red de hello** o **copia de seguridad sin conexión**.

    * **Automáticamente a través de la red de hello** transferencias Hola tooAzure de datos de copia de seguridad según la programación de hello elegido para la copia de seguridad.
    * Se explica cómo funciona **Copia de seguridad sin conexión** en [Flujo de trabajo de copia de seguridad sin conexión en Copia de seguridad de Azure](backup-azure-backup-import-export.md).

    Seleccione Transferir relevante de hello tooAzure de copia de seguridad inicial de mecanismo toosend hello y haga clic en **siguiente**.
15. Una vez que revisar detalles de la directiva de Hola Hola **resumen** pantalla, haga clic en hello **crear grupo** el flujo de trabajo de botón toocomplete Hola. Puede hacer clic en hello **cerrar** botón y monitor de progreso del trabajo hello en el área de trabajo de supervisión.

    ![Creación de un grupo de protección en curso](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>Copia de seguridad a petición de una base de datos SQL Server
Aunque los pasos anteriores de hello crean una directiva de copia de seguridad, se crea un "punto de recuperación" solo cuando se produce la primera copia de seguridad de Hola. En lugar de esperar Hola programador tookick en, pasos de Hola por debajo de la creación de hello de desencadenador de una recuperación del punto de manualmente.

1. Espere hasta que se muestra el estado del grupo de protección de hello **Aceptar** de base de datos de hello antes de crear el punto de recuperación de Hola.

    ![Miembros del grupo de protección](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Haga doble clic en la base de datos de Hola y seleccione **crear punto de recuperación**.

    ![Creación de punto de recuperación en línea](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Elija **protección en línea** en el menú desplegable de Hola y haga clic en **Aceptar**. Creación de hello de un punto de recuperación se inicia en Azure.

    ![Crear punto de recuperación](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. Puede ver el progreso del trabajo de Hola Hola **supervisión** donde encontrará un curso en el área de trabajo del trabajo como una muestra en la figura siguiente Hola Hola.

    ![Consola de supervisión](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Recuperación de una base de datos SQL Server de Azure
Hello siguientes pasos son necesario toorecover una entidad protegida (base de datos de SQL Server) de Azure.

1. Abra la consola de administración del servidor DPM Hola. Navegue demasiado**recuperación** área de trabajo donde puede ver los servidores de hello respaldada por DPM. Examinar la base de datos necesarios de hello (en este caso ReportServer$ MSDPM2012). Seleccione una hora en **Recuperación desde** que finalice con **En línea**.

    ![Selección de punto de recuperación](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Haga clic en nombre de la base de datos de Hola y haga clic en **recuperar**.

    ![Recuperación desde Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. DPM muestra los detalles de Hola Hola del punto de recuperación. Haga clic en **Siguiente**. base de datos de toooverwrite hello, tipo de recuperación de hello seleccione **recuperar toooriginal instancia de SQL Server**. Haga clic en **Siguiente**.

    ![Recuperar tooOriginal ubicación](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    En este ejemplo, DPM permite la recuperación de la instancia de SQL Server de tooanother de base de datos de Hola o una carpeta de red de tooa independiente.
4. Hola **opciones de recuperación especificar** pantalla, puede seleccionar opciones de recuperación de hello como límite de ancho de banda de toothrottle Hola utilizado por recuperación de uso de ancho de banda de red. Haga clic en **Siguiente**.
5. Hola **resumen** pantalla, verá todas las configuraciones de recuperación de hello proporcionadas hasta ahora. Haga clic en **Recuperar**.

    Hola estado de recuperación muestra base de datos de Hola que se va a recuperar. Puede hacer clic en **cerrar** tooclose Hola asistente y vista Hola progreso Hola **supervisión** área de trabajo.

    ![Inicio de proceso de recuperación](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Una vez completada la recuperación de hello, base de datos de hello restaurado es coherente con la aplicación.

### <a name="next-steps"></a>Pasos siguientes:
•   [Preguntas más frecuentes de Azure Backup](backup-azure-backup-faq.md)
