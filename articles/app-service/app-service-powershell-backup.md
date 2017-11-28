---
title: Uso de PowerShell tanto para realizar copias de seguridad de aplicaciones del Servicio de aplicaciones como para restaurarlas
description: Aprenda a usar PowerShell para realizar copias de seguridad de las aplicaciones del Servicio de aplicaciones de Azure y restaurarlas
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
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="4ad22-103">Uso de PowerShell tanto para realizar copias de seguridad de aplicaciones del Servicio de aplicaciones como para restaurarlas</span><span class="sxs-lookup"><span data-stu-id="4ad22-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ad22-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ad22-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="4ad22-105">API DE REST</span><span class="sxs-lookup"><span data-stu-id="4ad22-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="4ad22-106">Aprenda a usar Azure PowerShell para realizar copias de seguridad de [aplicaciones de App Service](https://azure.microsoft.com/services/app-service/web/) y restaurarlas.</span><span class="sxs-lookup"><span data-stu-id="4ad22-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="4ad22-107">Para más información acerca de copias de seguridad de aplicaciones web, incluidos los requisitos y las restricciones, consulte [Realizar una copia de seguridad de la aplicación en Azure](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="4ad22-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ad22-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ad22-108">Prerequisites</span></span>
<span data-ttu-id="4ad22-109">Si quiere usar PowerShell para administrar las copias de seguridad de las aplicaciones, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ad22-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="4ad22-110">**Una dirección URL de SAS** que permita el acceso de lectura y escritura a un contenedor de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad22-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="4ad22-111">Para obtener más información sobre las direcciones URL de SAS, consulte [Descripción del modelo de firmas de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="4ad22-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="4ad22-112">Consulte [Usar Azure PowerShell con Almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md) para ver ejemplos de administración de Almacenamiento de Azure mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ad22-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="4ad22-113">**Una cadena de conexión de base de datos** si quiere realizar una copia de seguridad de una base de datos junto con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4ad22-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="4ad22-114">Procedimiento para generar una dirección URL de SAS que vaya a usarse con los cmdlets de copia de seguridad de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="4ad22-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="4ad22-115">Las direcciones URL de SAS pueden generarse con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ad22-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="4ad22-116">Este es un ejemplo de cómo generar una que pueda usarse con los cmdlets que se explican en este artículo.</span><span class="sxs-lookup"><span data-stu-id="4ad22-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="4ad22-117">Instalación de Azure PowerShell 1.3.2, o superior</span><span class="sxs-lookup"><span data-stu-id="4ad22-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="4ad22-118">Para obtener instrucciones sobre cómo instalar y utilizar Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="4ad22-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="4ad22-119">Creación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4ad22-119">Create a backup</span></span>
<span data-ttu-id="4ad22-120">Use el cmdlet New-AzureRmWebAppBackup para crear una copia de seguridad de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4ad22-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="4ad22-121">De esta forma, se crea una copia de seguridad con un nombre generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4ad22-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="4ad22-122">Si desea especificar un nombre para la copia de seguridad, utilice el parámetro opcional BackupName.</span><span class="sxs-lookup"><span data-stu-id="4ad22-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="4ad22-123">Para incluir una base de datos en la copia de seguridad, cree antes una configuración de copia de seguridad de bases de datos mediante el cmdlet New-AzureRmWebAppDatabaseBackupSetting y, después, especifique dicha configuración en el parámetro Databases del cmdlet New-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="4ad22-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="4ad22-124">El parámetro Databases acepta una matriz de la configuración de la base de datos, lo que le permite realizar copias de seguridad de más de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="4ad22-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="4ad22-125">Obtención de copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="4ad22-125">Get backups</span></span>
<span data-ttu-id="4ad22-126">El cmdlet Get-AzureRmWebAppBackupList devuelve una matriz de todas las copias de seguridad de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4ad22-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="4ad22-127">Debe especificar el nombre de la aplicación web y su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4ad22-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="4ad22-128">Para obtener una copia de seguridad específica, use el cmdlet Get-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="4ad22-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="4ad22-129">También puede canalizar un objeto de aplicación web en cualquiera de los cmdlets de administración de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4ad22-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="4ad22-130">Programación de copias de seguridad automáticas</span><span class="sxs-lookup"><span data-stu-id="4ad22-130">Schedule automatic backups</span></span>
<span data-ttu-id="4ad22-131">Puede programar se realicen automáticamente copias de seguridad a intervalos especificados.</span><span class="sxs-lookup"><span data-stu-id="4ad22-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="4ad22-132">Para configurar una programación de copias de seguridad, use el cmdlet Edit-AzureRmWebAppBackupConfiguration.</span><span class="sxs-lookup"><span data-stu-id="4ad22-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="4ad22-133">Este cmdlet acepta varios parámetros:</span><span class="sxs-lookup"><span data-stu-id="4ad22-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="4ad22-134">**Name** : el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4ad22-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="4ad22-135">**ResourceGroupName** : el nombre del grupo de recursos que contiene la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4ad22-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="4ad22-136">**Slot** : este parámetro es opcional.</span><span class="sxs-lookup"><span data-stu-id="4ad22-136">**Slot** - Optional.</span></span> <span data-ttu-id="4ad22-137">El nombre de la ranura de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4ad22-137">The name of the web app slot.</span></span>
* <span data-ttu-id="4ad22-138">**StorageAccountUrl** : la dirección URL de SAS del contenedor de Almacenamiento de Azure que se usa para almacenar las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4ad22-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="4ad22-139">**FrequencyInterval** : el valor numérico de la frecuencia con la que deben realizarse las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4ad22-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="4ad22-140">Debe ser un entero positivo.</span><span class="sxs-lookup"><span data-stu-id="4ad22-140">Must be a positive integer.</span></span>
* <span data-ttu-id="4ad22-141">**FrequencyUnit** : la unidad de tiempo de la frecuencia con la que deben realizarse las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4ad22-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="4ad22-142">Las opciones son por hora y por día.</span><span class="sxs-lookup"><span data-stu-id="4ad22-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="4ad22-143">**RetentionPeriodInDays** : el número de días que las copias de seguridad automáticas deben guardarse antes de eliminarse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4ad22-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="4ad22-144">**StartTime** : este parámetro es opcional.</span><span class="sxs-lookup"><span data-stu-id="4ad22-144">**StartTime** - Optional.</span></span> <span data-ttu-id="4ad22-145">La hora a la que deben iniciarse las copias de seguridad automáticas.</span><span class="sxs-lookup"><span data-stu-id="4ad22-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="4ad22-146">Si el valor es null, las copias de seguridad se iniciarán de inmediato.</span><span class="sxs-lookup"><span data-stu-id="4ad22-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="4ad22-147">Debe ser una fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="4ad22-147">Must be a DateTime.</span></span>
* <span data-ttu-id="4ad22-148">**Databases** : este parámetro es opcional.</span><span class="sxs-lookup"><span data-stu-id="4ad22-148">**Databases** - Optional.</span></span> <span data-ttu-id="4ad22-149">Una matriz de DatabaseBackupSettings para las bases de datos de las que se va a realizar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4ad22-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="4ad22-150">**KeepAtLeastOneBackup** : se trata de un parámetro conmutado opcional.</span><span class="sxs-lookup"><span data-stu-id="4ad22-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="4ad22-151">Especifíquelo si se debe mantener una copia de seguridad en la cuenta de almacenamiento en todo momento, independientemente de su antigüedad.</span><span class="sxs-lookup"><span data-stu-id="4ad22-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="4ad22-152">A continuación, verá un ejemplo de cómo usar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4ad22-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="4ad22-153">Para obtener la programación de copias de seguridad actual, use el cmdlet Get-AzureRmWebAppBackupConfiguration cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4ad22-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="4ad22-154">Puede resultar útil para modificar una programación que ya se ha configurado.</span><span class="sxs-lookup"><span data-stu-id="4ad22-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="4ad22-155">Restauración de una aplicación web desde una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4ad22-155">Restore a web app from a backup</span></span>
<span data-ttu-id="4ad22-156">Para restaurar una aplicación web desde una copia de seguridad, use el cmdlet Restore-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="4ad22-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="4ad22-157">La manera más fácil de usar este cmdlet es canalizarlo en un objeto de copia de seguridad recuperado del cmdlet Get-AzureRmWebAppBackup o del cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="4ad22-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="4ad22-158">Una vez que tenga un objeto de copia de seguridad, puede canalizarlo al cmdlet Restore-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="4ad22-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="4ad22-159">Especifique el parámetro Overwrite para indicar que quiere sobrescribir el contenido de la aplicación web por el de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4ad22-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="4ad22-160">Si la copia de seguridad contiene bases de datos, también se restaurarán.</span><span class="sxs-lookup"><span data-stu-id="4ad22-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="4ad22-161">A continuación, se muestra un ejemplo de cómo utilizar Restore-AzureRmWebAppBackup especificando todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="4ad22-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="4ad22-162">Eliminación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4ad22-162">Delete a backup</span></span>
<span data-ttu-id="4ad22-163">Para eliminar una copia de seguridad, use el cmdlet Remove-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="4ad22-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="4ad22-164">De esta forma, se elimina la copia de seguridad de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4ad22-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="4ad22-165">Especifique el nombre de la aplicación, su grupo de recursos y el identificador de la copia de seguridad que quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="4ad22-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="4ad22-166">También puede canalizar un objeto de copia de seguridad en el cmdlet Remove-AzureRmWebAppBackup para eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="4ad22-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
