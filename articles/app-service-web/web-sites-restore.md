---
title: "aaaRestore una aplicación en Azure"
description: "Obtenga información acerca de cómo toorestore la aplicación desde una copia de seguridad."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a>Restaurar una aplicación en Azure
Este artículo muestra cómo toorestore una aplicación en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) que previamente ha realizado una copia (vea [copia de seguridad la aplicación en Azure](web-sites-backup.md)). Puede restaurar la aplicación con su estado anterior de bases de datos vinculadas a petición tooa o crear una nueva aplicación basada en una copia de seguridad de la aplicación original. Servicio de aplicaciones de Azure admite Hola siguiendo las bases de datos de copia de seguridad y restauración:
- [Base de datos SQL](https://azure.microsoft.com/en-us/services/sql-database/)
- [Azure Database for MySQL (versión preliminar)](https://azure.microsoft.com/en-us/services/mysql)
- [Azure Database for PostgreSQL (versión preliminar)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [MySQL en aplicación](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Restaurar a partir de copias de seguridad está disponible tooapps que se ejecuta en **estándar** y **Premium** capa. Para obtener más información sobre la escalación de su aplicación, vea [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md). **Premium** nivel permite a un número mayor de toobe de las copias de seguridad diarias realizada a **estándar** capa.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Restaurar una aplicación de una copia de seguridad existente
1. En hello **configuración** hoja de la aplicación Hola Portal de Azure, haga clic en **copias de seguridad** toodisplay hello **copias de seguridad** hoja. Haga clic en **Restaurar**.
   
    ![Elegir Restaurar ahora][ChooseRestoreNow]
2. Hola **restaurar** hoja, primer origen de copia de seguridad de hello select.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Hola **copia de seguridad de aplicación** opción muestra todas Hola copias de seguridad existentes de la aplicación actual de hello y puedan seleccionar fácilmente uno.
    Hola **almacenamiento** opción permite seleccionar cualquier archivo ZIP copia de seguridad de cualquier cuenta de almacenamiento de Azure y un contenedor en la suscripción existente.
    Si está intentando toorestore una copia de seguridad de otra aplicación, utilice hello **almacenamiento** opción.
3. A continuación, especifique el destino de hello de la restauración de la aplicación de hello en **destino de restauración**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Si elige **Sobrescribir**, se borrarán y sobrescribirán todos los datos existentes de la aplicación actual. Antes de hacer clic **Aceptar**, asegúrese de que es exactamente lo que desea toodo.
   > 
   > 
   
    Puede seleccionar **aplicación existente** aplicación Hola de toorestore tooanother de copia de seguridad de aplicaciones en hello mismo grupo de recurso. Antes de usar esta opción, debe ya ha creado otra aplicación en el grupo de recursos con la creación de reflejo de base de datos toohello de configuración definido en la copia de seguridad de aplicación Hola. También puede crear un **New** toorestore de aplicación de su contenido.

4. Haga clic en **Aceptar**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Descarga o eliminación de una copia de seguridad de una cuenta de almacenamiento
1. De hello principal **examinar** hoja de hello portal de Azure, seleccione **cuentas de almacenamiento**. Se mostrará una lista de las cuentas de almacenamiento existentes.
2. Seleccione la cuenta de almacenamiento de Hola que contiene la copia de seguridad de Hola que desea que se muestra la hoja de toodownload o delete.hello Hola cuenta de almacenamiento.
3. En la hoja de la cuenta de almacenamiento de hello, seleccione el contenedor de hello que desea
   
    ![Ver contenedores][ViewContainers]
4. Seleccione el archivo de copia de seguridad que desee toodownload o elimina.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Haga clic en **descargar** o **eliminar** según lo que desee toodo.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Supervisar una operación de restauración
toosee detalles sobre Hola éxito o error de operación de restauración de la aplicación de hello, navegue toohello **registro de actividad** hoja Hola portal de Azure.  
 

Desplácese hacia abajo de la restauración de toofind Hola deseado de operación y haga clic en tooselect se.

Hola Hola detalles hoja muestra disponible información relacionados con la operación de restauración de toohello.

## <a name="next-steps"></a>Pasos siguientes
Puede de copia de seguridad y restaurar aplicaciones de servicio de aplicaciones mediante API de REST (vea [tooback de REST de uso una copia de seguridad y restaurar aplicaciones de servicio de aplicaciones](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
