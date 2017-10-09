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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>Usar PowerShell tooback y restaurar aplicaciones de servicio de aplicaciones
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [API DE REST](../app-service-web/websites-csm-backup.md)
> 
> 

Obtenga información acerca de cómo toouse Azure PowerShell tooback una copia de seguridad y restauración [aplicaciones de servicio de aplicaciones](https://azure.microsoft.com/services/app-service/web/). Para más información acerca de copias de seguridad de aplicaciones web, incluidos los requisitos y las restricciones, consulte [Realizar una copia de seguridad de la aplicación en Azure](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Requisitos previos
toouse PowerShell toomanage las copias de seguridad de la aplicación, necesita Hola siguientes:

* **Una dirección URL SAS** que permite leer y contenedor de almacenamiento de Azure de tooan de acceso de escritura. Vea [modelo SAS de descripción hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para obtener una explicación de las direcciones URL de SAS. Consulte [Usar Azure PowerShell con Almacenamiento de Azure](../storage/common/storage-powershell-guide-full.md) para ver ejemplos de administración de Almacenamiento de Azure mediante PowerShell.
* **Una cadena de conexión de base de datos** si desea tooback una base de datos junto con la aplicación web.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>¿Cómo toogenerate una toouse de dirección URL de SAS con la aplicación web de hello backup cmdlets
Las direcciones URL de SAS pueden generarse con PowerShell. Este es un ejemplo de cómo toogenerate que puede utilizarse con cmdlets de hello descrito en este artículo.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Instalación de Azure PowerShell 1.3.2, o superior
Para obtener instrucciones sobre cómo instalar y utilizar Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) .

## <a name="create-a-backup"></a>Creación de una copia de seguridad
Utilice hello AzureRmWebAppBackup nuevo cmdlet toocreate una copia de seguridad de una aplicación web.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

De esta forma, se crea una copia de seguridad con un nombre generado automáticamente. Si desea que tooprovide un nombre para la copia de seguridad, use el parámetro opcional de hello Nombrecopiadeseguridad.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude una base de datos de copia de seguridad de hello, primero cree una configuración de copia de seguridad de base de datos mediante el cmdlet New-AzureRmWebAppDatabaseBackupSetting de Hola y después proporcione ese parámetro en hello las bases de datos del cmdlet New-AzureRmWebAppBackup de Hola. parámetro de las bases de datos de Hello acepta una matriz de configuración de base de datos, permitiéndole tooback más de una base de datos.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Obtención de copias de seguridad
cmdlet Get-AzureRmWebAppBackupList de Hello devuelve una matriz de todas las copias de seguridad para una aplicación web. Debe proporcionar el nombre de Hola de aplicación web de hello y su grupo de recursos.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

tooget una copia de seguridad específica, use el cmdlet de Get-AzureRmWebAppBackup Hola.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

También se puede canalizar un objeto de aplicación web en cualquiera de los cmdlets de administración de copia de seguridad de Hola para su comodidad.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Programación de copias de seguridad automáticas
Puede programar copias de seguridad toohappen automáticamente en un intervalo especificado. tooconfigure una programación de copia de seguridad, use el cmdlet de hello AzureRmWebAppBackupConfiguration de edición. Este cmdlet acepta varios parámetros:

* **Nombre** : hello nombre de aplicación web de hello.
* **ResourceGroupName** : hello nombre de aplicación Hola recursos grupo contenedor hello web.
* **Slot** : este parámetro es opcional. nombre de Hola de ranura de aplicación web de Hola.
* **StorageAccountUrl** -Hola URL de SAS para el contenedor de almacenamiento de Azure de hello utiliza copias de seguridad de toostore Hola.
* **FrequencyInterval** -valor numérico para la frecuencia con hello las copias de seguridad deben realizarse. Debe ser un entero positivo.
* **FrequencyUnit** -unidad de tiempo para la frecuencia con hello las copias de seguridad deben realizarse. Las opciones son por hora y por día.
* **RetentionPeriodInDays** : ¿cuántos días se deben guardar copias de seguridad automáticas de hello antes de eliminarse automáticamente.
* **StartTime** : este parámetro es opcional. hora de Hello deben empezar copias de seguridad automáticas de Hola. Si el valor es null, las copias de seguridad se iniciarán de inmediato. Debe ser una fecha y hora.
* **Databases** : este parámetro es opcional. Una matriz de DatabaseBackupSettings para hello toobackup de bases de datos.
* **KeepAtLeastOneBackup** : se trata de un parámetro conmutado opcional. Esto si siempre se debe mantener una copia de seguridad Hola cuenta de almacenamiento, independientemente de su antigüedad es la fuente de alimentación.

Aquí te mostramos un ejemplo de cómo toouse este cmdlet.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget Hola actual programar copia de seguridad, use el cmdlet Get-AzureRmWebAppBackupConfiguration Hola. Puede resultar útil para modificar una programación que ya se ha configurado.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Restauración de una aplicación web desde una copia de seguridad
toorestore una aplicación web desde una copia de seguridad, use el cmdlet de hello AzureRmWebAppBackup de restauración. toouse de manera más fácil de Hello este cmdlet es toopipe en un objeto de copia de seguridad que se recupera del cmdlet Get-AzureRmWebAppBackup Hola o el cmdlet Get-AzureRmWebAppBackupList.

Una vez que tenga un objeto de copia de seguridad, se pueden canalizar al cmdlet Restore-AzureRmWebAppBackup Hola. Especifique Hola sobrescribir conmutador parámetro tooindicate que piensa toooverwrite contenido de hello de la aplicación web con contenido de Hola de copia de seguridad de Hola. Si la copia de seguridad de hello contiene las bases de datos, se restauran también las bases de datos.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Aquí te mostramos un ejemplo de cómo toouse Hola restauración AzureRmWebAppBackup especificando todos los parámetros de Hola.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Eliminación de una copia de seguridad
toodelete una copia de seguridad, use el cmdlet de hello Remove-AzureRmWebAppBackup. Copia de seguridad de Hola se quitan de la cuenta de almacenamiento. Especifique el nombre de la aplicación, su grupo de recursos, y Hola Id. del programa Hola a copia de seguridad que desee toodelete.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

También puede canalizar un objeto de copia de seguridad en toodelete de cmdlet Remove-AzureRmWebAppBackup Hola se.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
