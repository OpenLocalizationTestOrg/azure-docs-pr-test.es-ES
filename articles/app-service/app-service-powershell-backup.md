---
title: aaaUse PowerShell tooback una copia de seguridad y restaurar aplicaciones de servicio de aplicaciones
description: "Obtenga información acerca de cómo toouse PowerShell tooback una copia de seguridad y restauración de una aplicación de servicio de aplicaciones de Azure"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="96e1a-103">Usar PowerShell tooback y restaurar aplicaciones de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="96e1a-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96e1a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96e1a-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="96e1a-105">API DE REST</span><span class="sxs-lookup"><span data-stu-id="96e1a-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="96e1a-106">Obtenga información acerca de cómo toouse Azure PowerShell tooback una copia de seguridad y restauración [aplicaciones de servicio de aplicaciones](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="96e1a-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="96e1a-107">Para más información acerca de copias de seguridad de aplicaciones web, incluidos los requisitos y las restricciones, consulte [Realizar una copia de seguridad de la aplicación en Azure](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="96e1a-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96e1a-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96e1a-108">Prerequisites</span></span>
<span data-ttu-id="96e1a-109">toouse PowerShell toomanage las copias de seguridad de la aplicación, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="96e1a-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="96e1a-110">**Una dirección URL SAS** que permite leer y contenedor de almacenamiento de Azure de tooan de acceso de escritura.</span><span class="sxs-lookup"><span data-stu-id="96e1a-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="96e1a-111">Vea [modelo SAS de descripción hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para obtener una explicación de las direcciones URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="96e1a-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="96e1a-112">Consulte [Usar Azure PowerShell con Almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md) para ver ejemplos de administración de Almacenamiento de Azure mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96e1a-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="96e1a-113">**Una cadena de conexión de base de datos** si desea tooback una base de datos junto con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="96e1a-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="96e1a-114">¿Cómo toogenerate una toouse de dirección URL de SAS con la aplicación web de hello backup cmdlets</span><span class="sxs-lookup"><span data-stu-id="96e1a-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="96e1a-115">Las direcciones URL de SAS pueden generarse con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96e1a-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="96e1a-116">Este es un ejemplo de cómo toogenerate que puede utilizarse con cmdlets de hello descrito en este artículo.</span><span class="sxs-lookup"><span data-stu-id="96e1a-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="96e1a-117">Instalación de Azure PowerShell 1.3.2, o superior</span><span class="sxs-lookup"><span data-stu-id="96e1a-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="96e1a-118">Para obtener instrucciones sobre cómo instalar y utilizar Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="96e1a-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="96e1a-119">Creación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="96e1a-119">Create a backup</span></span>
<span data-ttu-id="96e1a-120">Utilice hello AzureRmWebAppBackup nuevo cmdlet toocreate una copia de seguridad de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="96e1a-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="96e1a-121">De esta forma, se crea una copia de seguridad con un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="96e1a-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="96e1a-122">Si desea que tooprovide un nombre para la copia de seguridad, use el parámetro opcional de hello Nombrecopiadeseguridad.</span><span class="sxs-lookup"><span data-stu-id="96e1a-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="96e1a-123">tooinclude una base de datos de copia de seguridad de hello, primero cree una configuración de copia de seguridad de base de datos mediante el cmdlet New-AzureRmWebAppDatabaseBackupSetting de Hola y después proporcione ese parámetro en hello las bases de datos del cmdlet New-AzureRmWebAppBackup de Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="96e1a-124">parámetro de las bases de datos de Hello acepta una matriz de configuración de base de datos, permitiéndole tooback más de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="96e1a-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="96e1a-125">Obtención de copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="96e1a-125">Get backups</span></span>
<span data-ttu-id="96e1a-126">cmdlet Get-AzureRmWebAppBackupList de Hello devuelve una matriz de todas las copias de seguridad para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="96e1a-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="96e1a-127">Debe proporcionar el nombre de Hola de aplicación web de hello y su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="96e1a-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="96e1a-128">tooget una copia de seguridad específica, use el cmdlet de Get-AzureRmWebAppBackup Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="96e1a-129">También se puede canalizar un objeto de aplicación web en cualquiera de los cmdlets de administración de copia de seguridad de Hola para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="96e1a-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="96e1a-130">Programación de copias de seguridad automáticas</span><span class="sxs-lookup"><span data-stu-id="96e1a-130">Schedule automatic backups</span></span>
<span data-ttu-id="96e1a-131">Puede programar copias de seguridad toohappen automáticamente en un intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="96e1a-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="96e1a-132">tooconfigure una programación de copia de seguridad, use el cmdlet de hello AzureRmWebAppBackupConfiguration de edición.</span><span class="sxs-lookup"><span data-stu-id="96e1a-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="96e1a-133">Este cmdlet acepta varios parámetros:</span><span class="sxs-lookup"><span data-stu-id="96e1a-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="96e1a-134">**Nombre** : hello nombre de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="96e1a-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="96e1a-135">**ResourceGroupName** : hello nombre de aplicación Hola recursos grupo contenedor hello web.</span><span class="sxs-lookup"><span data-stu-id="96e1a-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="96e1a-136">**Slot** : este parámetro es opcional.</span><span class="sxs-lookup"><span data-stu-id="96e1a-136">**Slot** - Optional.</span></span> <span data-ttu-id="96e1a-137">nombre de Hola de ranura de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="96e1a-138">**StorageAccountUrl** -Hola URL de SAS para el contenedor de almacenamiento de Azure de hello utiliza copias de seguridad de toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="96e1a-139">**FrequencyInterval** -valor numérico para la frecuencia con hello las copias de seguridad deben realizarse.</span><span class="sxs-lookup"><span data-stu-id="96e1a-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="96e1a-140">Debe ser un entero positivo.</span><span class="sxs-lookup"><span data-stu-id="96e1a-140">Must be a positive integer.</span></span>
* <span data-ttu-id="96e1a-141">**FrequencyUnit** -unidad de tiempo para la frecuencia con hello las copias de seguridad deben realizarse.</span><span class="sxs-lookup"><span data-stu-id="96e1a-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="96e1a-142">Las opciones son por hora y por día.</span><span class="sxs-lookup"><span data-stu-id="96e1a-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="96e1a-143">**RetentionPeriodInDays** : ¿cuántos días se deben guardar copias de seguridad automáticas de hello antes de eliminarse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="96e1a-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="96e1a-144">**StartTime** : este parámetro es opcional.</span><span class="sxs-lookup"><span data-stu-id="96e1a-144">**StartTime** - Optional.</span></span> <span data-ttu-id="96e1a-145">hora de Hello deben empezar copias de seguridad automáticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="96e1a-146">Si el valor es null, las copias de seguridad se iniciarán de inmediato.</span><span class="sxs-lookup"><span data-stu-id="96e1a-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="96e1a-147">Debe ser una fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="96e1a-147">Must be a DateTime.</span></span>
* <span data-ttu-id="96e1a-148">**Databases** : este parámetro es opcional.</span><span class="sxs-lookup"><span data-stu-id="96e1a-148">**Databases** - Optional.</span></span> <span data-ttu-id="96e1a-149">Una matriz de DatabaseBackupSettings para hello toobackup de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="96e1a-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="96e1a-150">**KeepAtLeastOneBackup** : se trata de un parámetro conmutado opcional.</span><span class="sxs-lookup"><span data-stu-id="96e1a-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="96e1a-151">Esto si siempre se debe mantener una copia de seguridad Hola cuenta de almacenamiento, independientemente de su antigüedad es la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="96e1a-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="96e1a-152">Aquí te mostramos un ejemplo de cómo toouse este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96e1a-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="96e1a-153">tooget Hola actual programar copia de seguridad, use el cmdlet Get-AzureRmWebAppBackupConfiguration Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="96e1a-154">Puede resultar útil para modificar una programación que ya se ha configurado.</span><span class="sxs-lookup"><span data-stu-id="96e1a-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="96e1a-155">Restauración de una aplicación web desde una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="96e1a-155">Restore a web app from a backup</span></span>
<span data-ttu-id="96e1a-156">toorestore una aplicación web desde una copia de seguridad, use el cmdlet de hello AzureRmWebAppBackup de restauración.</span><span class="sxs-lookup"><span data-stu-id="96e1a-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="96e1a-157">toouse de manera más fácil de Hello este cmdlet es toopipe en un objeto de copia de seguridad que se recupera del cmdlet Get-AzureRmWebAppBackup Hola o el cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="96e1a-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="96e1a-158">Una vez que tenga un objeto de copia de seguridad, se pueden canalizar al cmdlet Restore-AzureRmWebAppBackup Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="96e1a-159">Especifique Hola sobrescribir conmutador parámetro tooindicate que piensa toooverwrite contenido de hello de la aplicación web con contenido de Hola de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="96e1a-160">Si la copia de seguridad de hello contiene las bases de datos, se restauran también las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="96e1a-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="96e1a-161">Aquí te mostramos un ejemplo de cómo toouse Hola restauración AzureRmWebAppBackup especificando todos los parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="96e1a-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="96e1a-162">Eliminación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="96e1a-162">Delete a backup</span></span>
<span data-ttu-id="96e1a-163">toodelete una copia de seguridad, use el cmdlet de hello Remove-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="96e1a-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="96e1a-164">Copia de seguridad de Hola se quitan de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="96e1a-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="96e1a-165">Especifique el nombre de la aplicación, su grupo de recursos, y Hola Id. del programa Hola a copia de seguridad que desee toodelete.</span><span class="sxs-lookup"><span data-stu-id="96e1a-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="96e1a-166">También puede canalizar un objeto de copia de seguridad en toodelete de cmdlet Remove-AzureRmWebAppBackup Hola se.</span><span class="sxs-lookup"><span data-stu-id="96e1a-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
