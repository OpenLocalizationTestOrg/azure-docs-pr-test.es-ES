---
title: tooback de servidor de copia de seguridad de Azure aaaUse seguridad un tooAzure de granja de servidores de SharePoint | Documentos de Microsoft
description: "Utilice tooback del servidor de copia de seguridad de Azure y restaurar los datos de SharePoint. Este artículo proporciona Hola información tooconfigure la granja de servidores de SharePoint para que los datos deseados pueden almacenarse en Azure. Puede restaurar los datos protegidos de SharePoint desde disco o desde Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Hacer copia de seguridad de un tooAzure de granja de servidores de SharePoint
Realizar copias de seguridad de SharePoint granja de servidores tooMicrosoft Azure mediante el uso de servidor de copia de seguridad de Microsoft Azure (MABS) en cantidad Hola igual que realice la copia de seguridad de otros orígenes de datos. Copia de seguridad de Azure proporciona flexibilidad en hello programar copia de seguridad toocreate puntos de copia de seguridad diarios, semanales, mensuales o anuales y proporciona opciones de directiva de retención para varios puntos de copia de seguridad. También proporciona copias de hello capacidad toostore disco local para los objetivos de tiempo de recuperación (RTO) rápidos y toostore copia tooAzure para la retención a largo plazo, económica.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Las versiones compatibles de SharePoint y relacionadas con escenarios de protección
Azure Backup para DPM admite Hola los escenarios siguientes:

| Carga de trabajo | Versión | Implementación de SharePoint | Protección y recuperación |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint implementado como un servidor físico o una máquina virtual de Hyper-V/VmWare <br> -------------- <br> SQL AlwaysOn | Opciones de protección de recuperación de la granja de SharePoint: granja de servidores de recuperación, base de datos y archivo, o elemento de la lista de puntos de recuperación de disco.  Recuperación de base de datos y granja de servidores a partir de puntos de recuperación de Azure. |

## <a name="before-you-start"></a>Antes de comenzar
Hay algunas cosas que debe tooconfirm antes de realizar la copia de seguridad de un tooAzure de granja de servidores de SharePoint.

### <a name="prerequisites"></a>Requisitos previos
Antes de continuar, asegúrese de que haya [instalado y preparado Hola servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) tooprotect cargas de trabajo.

### <a name="protection-agent"></a>Agente de protección
agente de protección de Hello debe instalarse en el servidor de Hola que ejecuta SharePoint, servidores de Hola que ejecutan SQL Server y todos los demás servidores que forman parte de la granja de servidores de SharePoint de Hola. Para obtener más información acerca de cómo tooset el agente de protección de hello, consulte [programa de instalación de agente de protección](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Hola única excepción es que instalar el agente de hello solo en los servidores front-end (WFE) web único. DPM necesita a agente hello en un WFE servidor solo tooserve como punto de entrada de hello para la protección.

### <a name="sharepoint-farm"></a>Granja de SharePoint
Para cada 10 millones de elementos en la granja de servidores de hello, debe haber al menos 2 GB de espacio en el volumen de Hola donde se encuentra la carpeta MABS Hola. Este espacio se requiere para la generación del catálogo. MABS toorecover elementos específicos (colecciones de sitios, sitios, listas, bibliotecas de documentos, carpetas, documentos individuales y elementos de lista), generación de catálogos crea una lista de direcciones URL de Hola que están dentro de cada base de datos de contenido. Puede ver lista de Hola de direcciones URL de panel de elementos recuperables de Hola Hola **recuperación** área de la consola de administrador de MABS de tareas.

### <a name="sql-server"></a>SQL Server
MABS se ejecuta como una cuenta LocalSystem. tooback seguridad bases de datos de SQL Server, MABS necesita privilegios de sysadmin en esa cuenta para servidor de Hola que ejecuta SQL Server. Establecer NT AUTHORITY\SYSTEM demasiado*sysadmin* en servidor hello que ejecuta SQL Server antes de realizar copias de seguridad.

Si la granja de servidores de SharePoint de hello tiene bases de datos de SQL Server que están configuradas con alias de SQL Server, instalar componentes de cliente de SQL Server de hello en el servidor Web front-end hello MABS protegerá.

### <a name="sharepoint-server"></a>SharePoint Server
Si bien el rendimiento depende de muchos factores, como el tamaño de la granja de SharePoint, de forma orientativa, un servidor MABS puede proteger una granja de SharePoint de 25 TB.

### <a name="whats-not-supported"></a>Lo que no se admite
* Que MABS proteja una granja de SharePoint y no proteja índices de búsqueda o bases de datos de servicios de aplicaciones. Necesitará tooconfigure protección de Hola de estas bases de datos por separado.
* Que MABS no proporcione copia de seguridad de bases de datos SQL Server de SharePoint hospedadas en recursos compartidos de servidor de archivos de escalabilidad horizontal (SOFS).

## <a name="configure-sharepoint-protection"></a>Configuración de la protección de SharePoint
Para poder usar MABS tooprotect SharePoint, debe configurar Hola VSS Writer de SharePoint (servicio WSS Writer) mediante **ConfigureSharePoint.exe**.

Puede encontrar **ConfigureSharePoint.exe** en carpeta \bin de hello [ruta de instalación de MABS] en el servidor web front-end de Hola. Esta herramienta proporciona el agente de protección de hello con credenciales de Hola para granja de SharePoint de Hola. Debe ejecutarlo en un solo servidor WFE. Si tiene varios servidores WFE, seleccione solo uno al configurar un grupo de protección.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>Hola tooconfigure servicio VSS Writer de SharePoint
1. En el servidor WFE hello, en un símbolo del sistema, vaya demasiado \bin\ [ubicación de instalación de MABS]
2. Escriba ConfigureSharePoint -EnableSharePointProtection.
3. Escriba las credenciales de administrador de granja de servidores de Hola. Esta cuenta debe ser miembro del grupo de administradores locales de hello en servidor WFE Hola. Si Administrador de granja de servidores de hello no es un Hola de concesión de administrador local los siguientes permisos en el servidor WFE hello:
   * GRANT hello WSS_Admin_WPG control total toohello DPM carpeta del grupo (% programa Files%\Microsoft Azure Backup\DPM).
   * GRANT hello WSS_Admin_WPG grupo acceso de lectura toohello DPM clave del registro (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Necesitará toorerun ConfigureSharePoint.exe cada vez que hay un cambio en las credenciales de administrador de granja de servidores de SharePoint de Hola.
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a>Realización de una copia de seguridad de una granja de SharePoint con MABS
Después de haber configurado MABS y Hola granja de SharePoint tal y como se ha explicado anteriormente, se puede proteger SharePoint por MABS.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect una granja de SharePoint
1. De hello **protección** ficha de hello consola de administrador de MABS, haga clic en **nuevo**.
    ![Nueva pestaña de protección](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. En hello **Seleccionar tipo de grupo de protección** página de hello **crear nuevo grupo de protección** asistente, seleccione **servidores**y, a continuación, haga clic en **siguiente** .

    ![Seleccionar tipo de grupo de protección](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. En hello **seleccionar miembros del grupo** pantalla, seleccione Hola casilla Hola de servidor de SharePoint que desee tooprotect y haga clic en **siguiente**.

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > Con instalado el agente de protección de hello, puede ver servidor hello en el Asistente de Hola. MABS también muestra su estructura. Porque ejecutó ConfigureSharePoint.exe, MABS se comunica con el servicio del escritor de VSS de SharePoint de Hola y sus correspondientes bases de datos de SQL Server y reconoce estructura hello de la granja de SharePoint, bases de datos de contenido y los elementos correspondientes de hello asociados.
   >
   >
4. En hello **Seleccionar método de protección de datos** escriba nombre Hola de hello **grupo de protección**y seleccione su preferido *métodos de protección*. Haga clic en **Siguiente**.

    ![Seleccionar método de protección de datos](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > método de protección de disco de Hello ayuda toomeet corto objetivos de tiempo de recuperación.
   >
   >
5. En hello **especificar objetivos a corto plazo** , seleccione su preferido **duración de retención** e identificar cuando desee que las copias de seguridad toooccur.

    ![Especificar objetivos a corto plazo](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > Porque recuperación con más frecuencia se requiere para los datos que tiene menos de cinco días de antigüedad, se selecciona un intervalo de retención de cinco días en el disco y se haya asegurado que esa copia de seguridad de hello sucede durante las horas no sea de producción, en este ejemplo.
   >
   >
6. Revise el espacio de disco del bloque de almacenamiento de hello asignado para el grupo de protección de Hola y haga clic en, a continuación, **siguiente**.
7. Para cada grupo de protección, MABS asigna toostore de espacio de disco y administrar las réplicas. En este momento, MABS debe crear una copia de datos de hello seleccionado. Seleccione cómo y cuándo desea réplica Hola creado y, a continuación, haga clic en **siguiente**.

    ![Elegir método de creación de réplica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > toomake seguro de que no se realiza el tráfico de red, seleccione una hora fuera del horario de producción.
   >
   >
8. MABS garantiza la integridad de datos mediante la realización de comprobaciones de coherencia en la réplica de Hola. Hay dos opciones disponibles. Puede definir una coherencia de toorun programación comprueba o DPM puede realizar comprobaciones de coherencia automáticamente en la réplica de hello cada vez que pasa a ser incoherente. Seleccione la opción que prefiera y haga clic en **Siguiente**.

    ![Comprobación de coherencia](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. En hello **especificar datos de protección en línea** , seleccione la granja de servidores de SharePoint de Hola que desee tooprotect y, a continuación, haga clic en **siguiente**.

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. En hello **especificar programación de copia de seguridad en línea** , seleccione la programación que prefiera y, a continuación, haga clic en **siguiente**.

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > MABS proporciona un máximo de dos tooAzure copias de seguridad diarias de Hola la disponibles punto de copia de seguridad de disco más reciente. Copia de seguridad de Azure también puede controlar la cantidad de Hola de ancho de banda WAN que puede usarse para copias de seguridad en las horas punta y horas de poca actividad mediante [límite de red de copia de seguridad de Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).
    >
    >
11. Según programación de copia de seguridad de Hola que ha seleccionado, en hello **especificar directiva de retención en línea** página Directiva de retención de hello select para puntos de copia de seguridad diarios, semanales, mensuales y anuales.

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > MABS emplea un esquema de retención abuelo-padre-hijo en el que se puede elegir una directiva de retención diferente para distintos puntos de copia de seguridad.
    >
    >
12. Toodisk similar, una réplica de punto de referencia inicial debe toobe creado en Azure. Seleccione su toocreate opción preferida un tooAzure de copia de seguridad inicial y, a continuación, haga clic en **siguiente**.

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Revise la configuración seleccionada en hello **resumen** página y, a continuación, haga clic en **crear grupo**. Verá un mensaje de confirmación una vez creado el grupo de protección de Hola.

    ![Resumen](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a>Restauración de un elemento de SharePoint desde un disco con MABS
En el siguiente ejemplo de Hola Hola *elemento de recuperación de SharePoint* se ha eliminado accidentalmente y necesita toobe recuperado.
![Protección de SharePoint con MABS4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Abra hello **consola de administrador DPM**. Se muestran todas las granjas de SharePoint que están protegidas por DPM en hello **protección** ficha.

    ![Protección de SharePoint con MABS3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. elemento de hello toobegin toorecover, seleccione hello **recuperación** ficha.

    ![Protección de SharePoint con MABS5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. Puede buscar en SharePoint el *elemento de recuperación* mediante caracteres comodín dentro un intervalo de puntos de recuperación.

    ![Protección de SharePoint con MABS6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Seleccione el punto de recuperación adecuado de Hola en resultados de búsqueda de hello, haga clic en el elemento de hello y, a continuación, seleccione **recuperar**.
5. También puede buscar en varios puntos de recuperación y seleccione una base de datos o elemento toorecover. Seleccione **fecha > tiempo de recuperación**y, a continuación, seleccione Hola correcto **base de datos > granja de SharePoint > punto de recuperación > elemento**.

    ![Protección de SharePoint con MABS7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Haga clic en el elemento de hello y, a continuación, seleccione **recuperar** tooopen hello **Asistente para recuperación**. Haga clic en **Siguiente**.

    ![Revisar selección de recuperación](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Seleccionar tipo de Hola de recuperación que desee tooperform y, a continuación, haga clic en **siguiente**.

    ![Tipo de recuperación](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > Hola selección de **recuperar toooriginal** Hola ejemplo recupera el sitio de SharePoint original de hello elemento toohello.
   >
   >
8. Seleccione hello **proceso de recuperación** que desea toouse.

   * Seleccione **recuperar sin utilizar una granja de servidores de recuperación** si no ha cambiado la granja de servidores de SharePoint de Hola y Hola igual que la recuperación de hello punto se restaura.
   * Seleccione **la recuperación mediante una granja de servidores de recuperación** si la granja de servidores de SharePoint de hello ha cambiado desde que se creó el punto de recuperación de Hola.

     ![proceso de recuperación](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Proporcionan un SQL Server instancia ubicación toorecover Hola base de datos provisional temporalmente y un recurso compartido de almacenamiento provisional en MABS y Hola el servidor que está ejecutando el elemento de SharePoint toorecover Hola.

    ![Ubicación provisional1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    MABS adjunta Hola contenido base de datos que hospeda la instancia de SQL Server temporal de hello SharePoint elemento toohello. De base de datos de contenido hello, recupera el elemento de Hola y lo coloca en hello en MABS la ubicación del archivo de almacenamiento provisional. Hola recupera el elemento que está en la ubicación de almacenamiento provisional ahora de hello necesidades toobe exportar toohello ubicación en la granja de servidores de SharePoint de Hola de almacenamiento provisional.

    ![Ubicación provisional2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Seleccione **especificar opciones de recuperación**y aplicar la configuración de seguridad toohello granja de SharePoint o aplicar la configuración de seguridad de Hola Hola del punto de recuperación. Haga clic en **Siguiente**.

    ![Opciones de recuperación](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > Puede elegir el uso de ancho de banda de red de toothrottle Hola. Esto reduce el servidor de producción de impacto toohello durante horas de producción.
    >
    >
11. Revise la información de resumen de hello y, a continuación, haga clic en **recuperar** toobegin recuperación de archivo hello.

    ![Resumen de recuperación](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Ahora seleccione hello **supervisión** ficha hello **consola de administrador de MABS** tooview hello **estado** de recuperación de Hola.

    ![Estado de recuperación](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > Ahora se restaura el archivo hello. Puede actualizar el archivo hello restaurar toocheck de hello SharePoint sitio.
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Restauración de una base de datos de SharePoint de Azure con DPM
1. toorecover una base de datos de contenido de SharePoint, vaya a través de varios puntos de recuperación (como se muestra anteriormente) y seleccione el punto de recuperación de Hola que desee toorestore.

    ![Protección de SharePoint con MABS8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Haga doble clic en hello SharePoint recuperación punto tooshow Hola disponible SharePoint información del catálogo.

   > [!NOTE]
   > Granja de SharePoint de hello está protegido para la retención a largo plazo en Azure, no hay información de catálogo (metadatos) está disponible en MABS. Como resultado, cada vez que una base de datos de contenido de SharePoint en un momento necesita toobe recuperado, granja de SharePoint de hello toocatalog se necesitará de nuevo.
   >
   >
3. Haga clic en **Volver a catalogar**.

    ![Protección de SharePoint con MABS10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    Hola **nube catalogar** abre la ventana de estado.

    ![Protección de SharePoint con MABS11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    Una vez finalizada la catalogación, también cambia el estado de hello*correcto*. Haga clic en **Cerrar**.

    ![Protección de SharePoint con MABS12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Haga clic en los objetos de SharePoint Hola se muestra en hello MABS **recuperación** pestaña estructura de contenido de la base de datos de tooget Hola. Haga clic en el elemento de hello y, a continuación, haga clic en **recuperar**.

    ![Protección de SharePoint con MABS13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. En este momento, siga hello [recuperación pasos anteriormente en este artículo](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover una base de datos de contenido de SharePoint desde el disco.

## <a name="faqs"></a>Preguntas más frecuentes
P: ¿puedo recuperar una ubicación original de SharePoint elemento toohello si SharePoint está configurada con AlwaysOn de SQL (con protección en disco)?<br>
R: Sí, elemento de hello puede ser recuperada toohello sitio de SharePoint original.

P: ¿puedo recuperar una ubicación en la toohello de base de datos de SharePoint original si SharePoint está configurada con AlwaysOn de SQL?<br>
R: dado que las bases de datos de SharePoint están configurados en AlwaysOn de SQL, no se puede modificar a menos que se quita el grupo de disponibilidad de Hola. Como resultado, MABS no puede restaurar una ubicación original de toohello de base de datos. Puede recuperar una instancia de SQL Server de tooanother de base de datos de SQL Server.

## <a name="next-steps"></a>Pasos siguientes
* Más información sobre la protección de SharePoint con MABS; consulte [Serie de vídeos: protección de SharePoint con DPM](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
