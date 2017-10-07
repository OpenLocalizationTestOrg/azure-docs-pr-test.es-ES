---
title: aaaRestore un almacenamiento de datos de SQL Azure (PowerShell) | Documentos de Microsoft
description: Tareas de PowerShell para restaurar una instancia de Almacenamiento de datos SQL de Azure.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Restauración de instancias de Almacenamiento de datos SQL de Azure (PowerShell)
> [!div class="op_single_selector"]
> * [Información general][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

En este artículo, aprenderá cómo toorestore un Azure almacenamiento de datos SQL mediante PowerShell.

## <a name="before-you-begin"></a>Antes de empezar
**Compruebe la capacidad DTU**. Cada instancia de Almacenamiento de datos SQL está hospedada en un servidor SQL Server (p. ej., myserver.database.windows.net) que tiene una cuota de DTU predeterminada.  Para poder restaurar un almacén de datos de SQL, compruebe que Hola que su SQL server tiene restante suficiente cuota DTU para base de datos de Hola que se va a restaurar. toolearn cómo necesarios toocalculate DTU o toorequest más DTU, consulte [solicitar un cambio de cuota DTU][Request a DTU quota change].

### <a name="install-powershell"></a>Instale PowerShell.
En orden toouse PowerShell de Azure con el almacenamiento de datos de SQL, deberá tooinstall PowerShell de Azure versión 1.0 o posterior.  Puede comprobar la versión ejecutando **Get-Module -ListAvailable -Name AzureRM**.  se puede instalar la versión más reciente de Hola desde [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].  Para obtener más información acerca de cómo instalar la versión más reciente de hello, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Restauración de una base de datos activa o en pausa
toorestore una base de datos desde una instantánea usar hello [restauración AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet de PowerShell.

1. Abra Windows PowerShell.
2. Conecte tooyour cuenta de Azure y mostrar todas las suscripciones de hello asociadas a su cuenta.
3. Seleccione la suscripción de Hola que contiene hello toobe de base de datos restaurado.
4. Hola lista puntos para base de datos de Hola de restauración.
5. Seleccionar punto de restauración de hello deseado mediante hello RestorePointCreationDate.
6. Restaurar el punto de restauración de toohello deseado de base de datos de Hola.
7. Compruebe que dicha base de datos de hello restaurado está en línea.

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Restauración de una base de datos eliminada
toorestore una base de datos eliminada, usar hello [restauración AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Abra Windows PowerShell.
2. Conecte tooyour cuenta de Azure y mostrar todas las suscripciones de hello asociadas a su cuenta.
3. La suscripción Hola SELECT que contiene Hola elimina toobe de base de datos restaurado.
4. Obtener base de datos de hello específico eliminado.
5. Restaurar base de datos de hello eliminado.
6. Compruebe que dicha base de datos de hello restaurado está en línea.

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Restauración dese una región geográfica de Azure
toorecover una base de datos, usar hello [restauración AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Abra Windows PowerShell.
2. Conecte tooyour cuenta de Azure y mostrar todas las suscripciones de hello asociadas a su cuenta.
3. Seleccione la suscripción de Hola que contiene hello toobe de base de datos restaurado.
4. Obtener base de datos de hello que desea toorecover.
5. Crear solicitud de recuperación de Hola para base de datos de Hola.
6. Comprobar estado de Hola de base de datos restaurado geográfica Hola.

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> consulta de la base de datos una vez finalizada la restauración de hello, tooconfigure [configurar la base de datos después de la recuperación][Configure your database after recovery].
> 
> 

base de datos recuperada Hola estará habilitada para TDE si base de datos de origen de hello tiene habilitado el TDE.

## <a name="next-steps"></a>Pasos siguientes
toolearn acerca de las características de continuidad de negocio de Hola de ediciones de base de datos de SQL Azure, lea hello [información general sobre la continuidad de negocio de base de datos de SQL Azure][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
