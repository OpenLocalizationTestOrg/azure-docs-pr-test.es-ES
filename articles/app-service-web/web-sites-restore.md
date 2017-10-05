---
title: "Restaurar una aplicación en Azure"
description: "Obtenga información sobre cómo restaurar la aplicación desde una copia de seguridad."
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
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="7fe58-103">Restaurar una aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="7fe58-103">Restore an app in Azure</span></span>
<span data-ttu-id="7fe58-104">En este artículo se muestra cómo restaurar una aplicación de [Azure App Service](../app-service/app-service-value-prop-what-is.md) de la que ha realizado previamente una copia de seguridad (consulte [Realizar una copia de seguridad de la aplicación en Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="7fe58-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="7fe58-105">Puede restaurar la aplicación con sus bases de datos vinculadas a petición a un estado anterior o crear una nueva aplicación basada en una copia de seguridad de la aplicación original.</span><span class="sxs-lookup"><span data-stu-id="7fe58-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="7fe58-106">Azure App Service admite las siguientes bases de datos para copia de seguridad y restauración:</span><span class="sxs-lookup"><span data-stu-id="7fe58-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="7fe58-107">Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="7fe58-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="7fe58-108">Azure Database for MySQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="7fe58-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="7fe58-109">Azure Database for PostgreSQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="7fe58-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="7fe58-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="7fe58-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="7fe58-111">MySQL en aplicación</span><span class="sxs-lookup"><span data-stu-id="7fe58-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="7fe58-112">La restauración de las copias de seguridad está disponible para las aplicaciones que se ejecutan en el nivel **Estándar** y **Premium**.</span><span class="sxs-lookup"><span data-stu-id="7fe58-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="7fe58-113">Para obtener más información sobre la escalación de su aplicación, vea [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7fe58-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="7fe58-114">El nivel **premium** permite realizar un mayor número de copias de seguridad diarias que se van a realizar en el nivel **estándar**.</span><span class="sxs-lookup"><span data-stu-id="7fe58-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="7fe58-115">Restaurar una aplicación de una copia de seguridad existente</span><span class="sxs-lookup"><span data-stu-id="7fe58-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="7fe58-116">En la hoja **Configuración** de la aplicación en Azure Portal, haga clic en la opción **Copias de seguridad** para mostrar la hoja **Copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="7fe58-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="7fe58-117">Haga clic en **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="7fe58-117">Then click **Restore**.</span></span>
   
    ![Elegir Restaurar ahora][ChooseRestoreNow]
2. <span data-ttu-id="7fe58-119">En la hoja **Restaurar** , seleccione primero el origen de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7fe58-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="7fe58-120">La opción **Copia de seguridad de aplicación** le muestra todas las copias de seguridad existentes de la aplicación actual y puede seleccionar una fácilmente.</span><span class="sxs-lookup"><span data-stu-id="7fe58-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="7fe58-121">La opción **Almacenamiento** le permite seleccionar cualquier archivo ZIP de copia de seguridad de cualquier cuenta de almacenamiento de Azure y contenedor existente de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="7fe58-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="7fe58-122">Si está intentando restaurar una copia de seguridad de otra aplicación, use la opción **Almacenamiento** .</span><span class="sxs-lookup"><span data-stu-id="7fe58-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="7fe58-123">A continuación, especifique el destino de la restauración de la aplicación en **Destino de restauración**.</span><span class="sxs-lookup"><span data-stu-id="7fe58-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="7fe58-124">Si elige **Sobrescribir**, se borrarán y sobrescribirán todos los datos existentes de la aplicación actual.</span><span class="sxs-lookup"><span data-stu-id="7fe58-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="7fe58-125">Antes de hacer clic en **Aceptar**, asegúrese de que es exactamente lo que desea.</span><span class="sxs-lookup"><span data-stu-id="7fe58-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="7fe58-126">Puede seleccionar **Aplicación existente** para restaurar la copia de seguridad de la aplicación a otra aplicación en el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7fe58-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="7fe58-127">Antes de utilizar esta opción, debe haber creado primero otra aplicación en el grupo de recursos con una configuración de base de datos reflejada en la definida en la copia de seguridad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7fe58-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="7fe58-128">También puede crear una aplicación **Nueva** en la cual restaurar el contenido.</span><span class="sxs-lookup"><span data-stu-id="7fe58-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="7fe58-129">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7fe58-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="7fe58-130">Descarga o eliminación de una copia de seguridad de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="7fe58-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="7fe58-131">En la hoja principal **Examinar** de Azure Portal, seleccione **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="7fe58-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="7fe58-132">Se mostrará una lista de las cuentas de almacenamiento existentes.</span><span class="sxs-lookup"><span data-stu-id="7fe58-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="7fe58-133">Seleccione la cuenta de almacenamiento que contiene la copia de seguridad que desea descargar o eliminar. Se muestra la hoja de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7fe58-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="7fe58-134">En la hoja de la cuenta de almacenamiento, seleccione el contenedor que quiere.</span><span class="sxs-lookup"><span data-stu-id="7fe58-134">In the storage account blade, select the container you want</span></span>
   
    ![Ver contenedores][ViewContainers]
4. <span data-ttu-id="7fe58-136">Seleccione el archivo de copia de seguridad que quiere descargar o eliminar.</span><span class="sxs-lookup"><span data-stu-id="7fe58-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="7fe58-138">Haga clic en **Descargar** o **Eliminar**, dependiendo de lo que quiera hacer.</span><span class="sxs-lookup"><span data-stu-id="7fe58-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="7fe58-139">Supervisar una operación de restauración</span><span class="sxs-lookup"><span data-stu-id="7fe58-139">Monitor a restore operation</span></span>
<span data-ttu-id="7fe58-140">Para detalles sobre si se ha realizado correctamente o no la operación de restauración de la aplicación, vaya a la hoja **Registro de actividades** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7fe58-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="7fe58-141">Desplácese hacia abajo para buscar la operación de restauración deseada y haga clic para seleccionarla.</span><span class="sxs-lookup"><span data-stu-id="7fe58-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="7fe58-142">La hoja de detalles muestra la información disponible relacionada con la operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="7fe58-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fe58-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7fe58-143">Next Steps</span></span>
<span data-ttu-id="7fe58-144">Puede crear una copia de seguridad de las aplicaciones de App Service y restaurar dicha copia mediante la API de REST (vea [Uso de REST para copia de seguridad y restauración de aplicaciones de App Service](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="7fe58-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
