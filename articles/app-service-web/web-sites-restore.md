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
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="8bd04-103">Restaurar una aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="8bd04-103">Restore an app in Azure</span></span>
<span data-ttu-id="8bd04-104">Este artículo muestra cómo toorestore una aplicación en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) que previamente ha realizado una copia (vea [copia de seguridad la aplicación en Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="8bd04-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="8bd04-105">Puede restaurar la aplicación con su estado anterior de bases de datos vinculadas a petición tooa o crear una nueva aplicación basada en una copia de seguridad de la aplicación original.</span><span class="sxs-lookup"><span data-stu-id="8bd04-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="8bd04-106">Servicio de aplicaciones de Azure admite Hola siguiendo las bases de datos de copia de seguridad y restauración:</span><span class="sxs-lookup"><span data-stu-id="8bd04-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="8bd04-107">Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="8bd04-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="8bd04-108">Azure Database for MySQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8bd04-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="8bd04-109">Azure Database for PostgreSQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8bd04-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="8bd04-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="8bd04-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="8bd04-111">MySQL en aplicación</span><span class="sxs-lookup"><span data-stu-id="8bd04-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="8bd04-112">Restaurar a partir de copias de seguridad está disponible tooapps que se ejecuta en **estándar** y **Premium** capa.</span><span class="sxs-lookup"><span data-stu-id="8bd04-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="8bd04-113">Para obtener más información sobre la escalación de su aplicación, vea [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="8bd04-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="8bd04-114">**Premium** nivel permite a un número mayor de toobe de las copias de seguridad diarias realizada a **estándar** capa.</span><span class="sxs-lookup"><span data-stu-id="8bd04-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="8bd04-115">Restaurar una aplicación de una copia de seguridad existente</span><span class="sxs-lookup"><span data-stu-id="8bd04-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="8bd04-116">En hello **configuración** hoja de la aplicación Hola Portal de Azure, haga clic en **copias de seguridad** toodisplay hello **copias de seguridad** hoja.</span><span class="sxs-lookup"><span data-stu-id="8bd04-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="8bd04-117">Haga clic en **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="8bd04-117">Then click **Restore**.</span></span>
   
    ![Elegir Restaurar ahora][ChooseRestoreNow]
2. <span data-ttu-id="8bd04-119">Hola **restaurar** hoja, primer origen de copia de seguridad de hello select.</span><span class="sxs-lookup"><span data-stu-id="8bd04-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="8bd04-120">Hola **copia de seguridad de aplicación** opción muestra todas Hola copias de seguridad existentes de la aplicación actual de hello y puedan seleccionar fácilmente uno.</span><span class="sxs-lookup"><span data-stu-id="8bd04-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="8bd04-121">Hola **almacenamiento** opción permite seleccionar cualquier archivo ZIP copia de seguridad de cualquier cuenta de almacenamiento de Azure y un contenedor en la suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="8bd04-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="8bd04-122">Si está intentando toorestore una copia de seguridad de otra aplicación, utilice hello **almacenamiento** opción.</span><span class="sxs-lookup"><span data-stu-id="8bd04-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="8bd04-123">A continuación, especifique el destino de hello de la restauración de la aplicación de hello en **destino de restauración**.</span><span class="sxs-lookup"><span data-stu-id="8bd04-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="8bd04-124">Si elige **Sobrescribir**, se borrarán y sobrescribirán todos los datos existentes de la aplicación actual.</span><span class="sxs-lookup"><span data-stu-id="8bd04-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="8bd04-125">Antes de hacer clic **Aceptar**, asegúrese de que es exactamente lo que desea toodo.</span><span class="sxs-lookup"><span data-stu-id="8bd04-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="8bd04-126">Puede seleccionar **aplicación existente** aplicación Hola de toorestore tooanother de copia de seguridad de aplicaciones en hello mismo grupo de recurso.</span><span class="sxs-lookup"><span data-stu-id="8bd04-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="8bd04-127">Antes de usar esta opción, debe ya ha creado otra aplicación en el grupo de recursos con la creación de reflejo de base de datos toohello de configuración definido en la copia de seguridad de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="8bd04-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="8bd04-128">También puede crear un **New** toorestore de aplicación de su contenido.</span><span class="sxs-lookup"><span data-stu-id="8bd04-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="8bd04-129">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8bd04-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="8bd04-130">Descarga o eliminación de una copia de seguridad de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8bd04-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="8bd04-131">De hello principal **examinar** hoja de hello portal de Azure, seleccione **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="8bd04-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="8bd04-132">Se mostrará una lista de las cuentas de almacenamiento existentes.</span><span class="sxs-lookup"><span data-stu-id="8bd04-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="8bd04-133">Seleccione la cuenta de almacenamiento de Hola que contiene la copia de seguridad de Hola que desea que se muestra la hoja de toodownload o delete.hello Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8bd04-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="8bd04-134">En la hoja de la cuenta de almacenamiento de hello, seleccione el contenedor de hello que desea</span><span class="sxs-lookup"><span data-stu-id="8bd04-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Ver contenedores][ViewContainers]
4. <span data-ttu-id="8bd04-136">Seleccione el archivo de copia de seguridad que desee toodownload o elimina.</span><span class="sxs-lookup"><span data-stu-id="8bd04-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="8bd04-138">Haga clic en **descargar** o **eliminar** según lo que desee toodo.</span><span class="sxs-lookup"><span data-stu-id="8bd04-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="8bd04-139">Supervisar una operación de restauración</span><span class="sxs-lookup"><span data-stu-id="8bd04-139">Monitor a restore operation</span></span>
<span data-ttu-id="8bd04-140">toosee detalles sobre Hola éxito o error de operación de restauración de la aplicación de hello, navegue toohello **registro de actividad** hoja Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd04-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="8bd04-141">Desplácese hacia abajo de la restauración de toofind Hola deseado de operación y haga clic en tooselect se.</span><span class="sxs-lookup"><span data-stu-id="8bd04-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="8bd04-142">Hola Hola detalles hoja muestra disponible información relacionados con la operación de restauración de toohello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bd04-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8bd04-143">Next Steps</span></span>
<span data-ttu-id="8bd04-144">Puede de copia de seguridad y restaurar aplicaciones de servicio de aplicaciones mediante API de REST (vea [tooback de REST de uso una copia de seguridad y restaurar aplicaciones de servicio de aplicaciones](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="8bd04-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
