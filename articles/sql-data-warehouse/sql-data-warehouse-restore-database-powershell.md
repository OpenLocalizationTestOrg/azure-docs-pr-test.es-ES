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
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="1333f-103">Restauración de instancias de Almacenamiento de datos SQL de Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="1333f-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="1333f-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="1333f-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="1333f-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="1333f-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="1333f-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="1333f-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="1333f-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="1333f-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="1333f-108">En este artículo, aprenderá cómo toorestore un Azure almacenamiento de datos SQL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1333f-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1333f-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1333f-109">Before you begin</span></span>
<span data-ttu-id="1333f-110">**Compruebe la capacidad DTU**.</span><span class="sxs-lookup"><span data-stu-id="1333f-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="1333f-111">Cada instancia de Almacenamiento de datos SQL está hospedada en un servidor SQL Server (p. ej., myserver.database.windows.net) que tiene una cuota de DTU predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1333f-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="1333f-112">Para poder restaurar un almacén de datos de SQL, compruebe que Hola que su SQL server tiene restante suficiente cuota DTU para base de datos de Hola que se va a restaurar.</span><span class="sxs-lookup"><span data-stu-id="1333f-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="1333f-113">toolearn cómo necesarios toocalculate DTU o toorequest más DTU, consulte [solicitar un cambio de cuota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="1333f-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="1333f-114">Instale PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1333f-114">Install PowerShell</span></span>
<span data-ttu-id="1333f-115">En orden toouse PowerShell de Azure con el almacenamiento de datos de SQL, deberá tooinstall PowerShell de Azure versión 1.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="1333f-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="1333f-116">Puede comprobar la versión ejecutando **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="1333f-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="1333f-117">se puede instalar la versión más reciente de Hola desde [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="1333f-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="1333f-118">Para obtener más información acerca de cómo instalar la versión más reciente de hello, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="1333f-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="1333f-119">Restauración de una base de datos activa o en pausa</span><span class="sxs-lookup"><span data-stu-id="1333f-119">Restore an active or paused database</span></span>
<span data-ttu-id="1333f-120">toorestore una base de datos desde una instantánea usar hello [restauración AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1333f-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="1333f-121">Abra Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1333f-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="1333f-122">Conecte tooyour cuenta de Azure y mostrar todas las suscripciones de hello asociadas a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1333f-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="1333f-123">Seleccione la suscripción de Hola que contiene hello toobe de base de datos restaurado.</span><span class="sxs-lookup"><span data-stu-id="1333f-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="1333f-124">Hola lista puntos para base de datos de Hola de restauración.</span><span class="sxs-lookup"><span data-stu-id="1333f-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="1333f-125">Seleccionar punto de restauración de hello deseado mediante hello RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="1333f-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="1333f-126">Restaurar el punto de restauración de toohello deseado de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1333f-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="1333f-127">Compruebe que dicha base de datos de hello restaurado está en línea.</span><span class="sxs-lookup"><span data-stu-id="1333f-127">Verify that hello restored database is online.</span></span>

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
> <span data-ttu-id="1333f-128">Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="1333f-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="1333f-129">Restauración de una base de datos eliminada</span><span class="sxs-lookup"><span data-stu-id="1333f-129">Restore a deleted database</span></span>
<span data-ttu-id="1333f-130">toorestore una base de datos eliminada, usar hello [restauración AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1333f-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="1333f-131">Abra Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1333f-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="1333f-132">Conecte tooyour cuenta de Azure y mostrar todas las suscripciones de hello asociadas a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1333f-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="1333f-133">La suscripción Hola SELECT que contiene Hola elimina toobe de base de datos restaurado.</span><span class="sxs-lookup"><span data-stu-id="1333f-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="1333f-134">Obtener base de datos de hello específico eliminado.</span><span class="sxs-lookup"><span data-stu-id="1333f-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="1333f-135">Restaurar base de datos de hello eliminado.</span><span class="sxs-lookup"><span data-stu-id="1333f-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="1333f-136">Compruebe que dicha base de datos de hello restaurado está en línea.</span><span class="sxs-lookup"><span data-stu-id="1333f-136">Verify that hello restored database is online.</span></span>

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
> <span data-ttu-id="1333f-137">Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="1333f-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="1333f-138">Restauración dese una región geográfica de Azure</span><span class="sxs-lookup"><span data-stu-id="1333f-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="1333f-139">toorecover una base de datos, usar hello [restauración AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1333f-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="1333f-140">Abra Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1333f-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="1333f-141">Conecte tooyour cuenta de Azure y mostrar todas las suscripciones de hello asociadas a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1333f-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="1333f-142">Seleccione la suscripción de Hola que contiene hello toobe de base de datos restaurado.</span><span class="sxs-lookup"><span data-stu-id="1333f-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="1333f-143">Obtener base de datos de hello que desea toorecover.</span><span class="sxs-lookup"><span data-stu-id="1333f-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="1333f-144">Crear solicitud de recuperación de Hola para base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1333f-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="1333f-145">Comprobar estado de Hola de base de datos restaurado geográfica Hola.</span><span class="sxs-lookup"><span data-stu-id="1333f-145">Verify hello status of hello geo-restored database.</span></span>

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
> <span data-ttu-id="1333f-146">consulta de la base de datos una vez finalizada la restauración de hello, tooconfigure [configurar la base de datos después de la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="1333f-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="1333f-147">base de datos recuperada Hola estará habilitada para TDE si base de datos de origen de hello tiene habilitado el TDE.</span><span class="sxs-lookup"><span data-stu-id="1333f-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1333f-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1333f-148">Next steps</span></span>
<span data-ttu-id="1333f-149">toolearn acerca de las características de continuidad de negocio de Hola de ediciones de base de datos de SQL Azure, lea hello [información general sobre la continuidad de negocio de base de datos de SQL Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="1333f-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
