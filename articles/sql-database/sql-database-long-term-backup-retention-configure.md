---
title: "Configuración de la retención de copias de seguridad a largo plazo (Azure SQL Database) | Microsoft Docs"
description: "Obtenga información acerca de cómo toostore automatizar las copias de seguridad en hello del almacén de servicios de recuperación de Azure y toorestore de hello que del almacén de servicios de recuperación de Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>Configuración de la retención de copias de seguridad a largo plazo de Azure SQL Database

Puede configurar copias de seguridad de SQL Azure de hello servicios de recuperación de Azure almacén toostore y, a continuación, recuperar una base de datos con copias de seguridad se conserva en hello almacén con Hola portal de Azure o PowerShell.

## <a name="azure-portal"></a>Azure Portal

Hola siguientes secciones muestra también cómo almacén toouse Hola tooconfigure portal Azure Hola servicios de recuperación de Azure, ver las copias de seguridad en el almacén de Hola y restaurar desde el almacén de Hola.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Configurar el almacén de hello, Registrar servidor hello y seleccione las bases de datos

Se [configurar un copias de seguridad de servicios de recuperación de Azure almacén tooretain automatizada](sql-database-long-term-retention.md) para un periodo superior al período de retención de hello para el nivel de servicio. 

1. Abra hello **SQL Server** página del servidor.

   ![página de sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. Haga clic en **Long-term backup retention** (Retención de copia de seguridad a largo plazo).

   ![vínculo de retención de copia de seguridad a largo plazo](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. En hello **retención de copia de seguridad a largo plazo** página para el servidor, revise y acepte los términos de vista previa de hello (a menos que aún lo ha hecho - o esta característica ya no está en vista previa).

   ![Acepte los términos de vista previa de Hola](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. retención de copia de seguridad a largo plazo de tooconfigure, seleccione esa base de datos en la cuadrícula de hello y, a continuación, haga clic en **configurar** en la barra de herramientas de Hola.

   ![seleccionar base de datos para retención de copia de seguridad a largo plazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. En hello **configurar** página, haga clic en **establecer configuración obligatoria** en **almacén del servicio de recuperación de**.

   ![vínculo para configurar almacén](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. En hello **almacén de servicios de recuperación** , seleccione un almacén existente, si existe. En caso contrario, si ningún almacén de servicios de recuperación encontró para la suscripción, haga clic en el flujo de hello tooexit y crear un almacén de servicios de recuperación.

   ![crear vinculo de almacén](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. En hello **servicios de recuperación de los almacenes de credenciales** página, haga clic en **agregar**.

   ![agregar vinculo de almacén](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. En hello **del almacén de servicios de recuperación** , proporcione un nombre válido para el almacén de servicios de recuperación de Hola.

   ![nuevo nombre de almacén](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Seleccione la suscripción y el grupo de recursos y, a continuación, seleccione la ubicación de hello para el almacén de Hola. Cuando termine, haga clic en **Crear**.

   ![crear almacén](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > almacén de Hello debe estar ubicado en Hola misma región que el servidor lógico de SQL Azure de Hola y debe usar Hola mismo grupo de recursos que el servidor lógico de Hola.
   >

10. Después de crea el nuevo almacén de hello, ejecute hello pasos necesarios tooreturn toohello **almacén de servicios de recuperación** página.

11. En hello **almacén de servicios de recuperación** página, haga clic en el almacén de hello y, a continuación, haga clic en **seleccione**.

   ![seleccionar almacén existente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. En hello **configurar** página, proporcione un nombre válido para la nueva directiva de retención hello, modificar la directiva de retención predeterminada de hello según corresponda y, a continuación, haga clic en **Aceptar**.

   ![definir directiva de retención](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. En hello **retención de copia de seguridad a largo plazo** página de la base de datos, haga clic en **guardar** y, a continuación, haga clic en **Aceptar** tooapply Hola a largo plazo tooall de directiva de retención de copia de seguridad seleccionada bases de datos.

   ![definir directiva de retención](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Haga clic en **guardar** tooenable retención de copia de seguridad a largo plazo con este nuevo almacén de servicios de recuperación de Azure de toohello de directiva que ha configurado.

   ![definir directiva de retención](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> Una vez configurado, las copias de seguridad aparecen en el almacén de hello en siete días siguientes. No continúe con este tutorial hasta que las copias de seguridad que se mostrarán en el almacén de Hola.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Visualización de copias de seguridad en retención a largo plazo mediante Azure Portal

Visualización de información acerca de las copias de seguridad de su base de datos en la [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md). 

1. En el portal de Azure de Hola, abrir el almacén de servicios de recuperación de Azure para las copias de seguridad de base de datos (ir demasiado**todos los recursos** y selecciónelo en la lista de Hola de los recursos de su suscripción) tooview cantidad de Hola de almacenamiento utilizado por la base de datos copias de seguridad en el almacén de Hola.

   ![ver almacén de servicios de recuperación con copias de seguridad](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Abra hello **base de datos SQL** página de la base de datos.

   ![página nueva de base de datos de ejemplo](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. En la barra de herramientas de hello, haga clic en **restaurar**.

   ![barra de herramientas restaurar](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. En la página de la restauración de hello, haga clic en **a largo plazo**.

5. En copias de seguridad del almacén de Azure, haga clic en **Seleccionar copia de seguridad** tooview copias de seguridad de bases de datos disponibles de hello en retención de copia de seguridad a largo plazo.

   ![copias de seguridad en almacén](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Restaurar una base de datos desde una copia de seguridad de retención de copia de seguridad a largo plazo con hello portal de Azure

Restaurar hello tooa nueva base de datos desde una copia de seguridad en hello que del almacén de servicios de recuperación de Azure.

1. En hello **copias de seguridad del almacén de Azure** página, haga clic en toorestore de copia de seguridad de hello y, a continuación, haga clic en **seleccione**.

   ![seleccionar copia de seguridad en almacén](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. Hola **nombre de base de datos** texto cuadro, proporcione el nombre hello para la base de datos de hello restaurado.

   ![nombre de nueva base de datos](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Haga clic en **Aceptar** toorestore la base de datos de copia de seguridad de Hola Hola almacén toohello nueva base de datos.

4. En la barra de herramientas de hello, haga clic en estado hello tooview de icono de notificación de Hola de trabajo de restauración de Hola.

   ![progreso de trabajo de restauración del almacén](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Cuando se completa el trabajo de restauración de hello, abra hello **bases de datos SQL** base de datos de página tooview Hola recién restaurado.

   ![base de datos restaurada desde almacén](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> Desde aquí, puede conectarse toohello Restaurar base de datos mediante las tareas de SQL Server Management Studio tooperform necesitado, como demasiado[extraer una porción de datos de toocopy de hello Restaurar base de datos en la base de datos existente de Hola o toodelete Hola existente base de datos y cambiar el nombre hello Restaurar base de datos toohello existente en nombre de base de datos](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

Hola las secciones siguientes muestra cómo ver las copias de seguridad en el almacén de hello toouse PowerShell tooconfigure Hola el almacén de servicios de recuperación de Azure y restaurar desde el almacén de Hola.

### <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Servicios de recuperación

Hola de uso [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate una recuperación del almacén de servicios.

> [!IMPORTANT]
> almacén de Hello debe estar ubicado en Hola misma región que el servidor lógico de SQL Azure de Hola y debe usar Hola mismo grupo de recursos que el servidor lógico de Hola.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Establecer el almacén de recuperación de servidor toouse Hola para sus copias de seguridad de retención a largo plazo

Hola de uso [AzureRmSqlServerBackupLongTermRetentionVault conjunto](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate cmdlet creado anteriormente con un servidor SQL Azure específico del almacén de servicios de recuperación.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Creación de una directiva de retención

Una directiva de retención es donde se establece tookeep cuánto tiempo una copia de seguridad de base de datos. Hola de uso [AzureRmRecoveryServicesBackupRetentionPolicyObject Get](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet toouse de directiva de retención tooget Hola predeterminado como plantilla de Hola para crear directivas de. En esta plantilla, se establece el período de retención de Hola durante dos años. A continuación, ejecute hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Crear directiva de Hola. 

> [!NOTE]
> Algunos cmdlets requieren que se establece el contexto de almacén de hello antes de ejecutar ([AzureRmRecoveryServicesVaultContext Set](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) para ver este cmdlet en algunos fragmentos de código relacionados. Para establecer el contexto de hello porque la directiva de hello es parte del almacén de Hola. Puede crear varias directivas de retención para cada almacén y, a continuación, aplicar las bases de datos de hello deseado directiva toospecific. 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Configurar una directiva de retención de base de datos toouse Hola definido anteriormente

Hola de uso [AzureRmSqlDatabaseBackupLongTermRetentionPolicy conjunto](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply Hola nueva directiva tooa base de datos específica.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Visualización de la información sobre copias de seguridad y copias de seguridad con retención a largo plazo

Visualización de información acerca de las copias de seguridad de su base de datos en la [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md). 

Usar hello siguiendo la información de copia de seguridad de tooview de cmdlets:

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Restauración de una base de datos de una copia de seguridad con retención a largo plazo

Restaurar a partir de retención de copia de seguridad a largo plazo usa hello [AzureRmSqlDatabase restauración](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> Desde aquí, puede conectarse toohello Restaurar base de datos mediante las tareas de SQL Server Management Studio tooperform necesarios, como tooextract una porción de datos de hello restaura toocopy de base de datos en base de datos existente de Hola o base de datos existente de toodelete Hola y el nombre Hola restaura el nombre de base de datos existente de base de datos toohello. Consulte la [restauración a un momento dado](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Pasos siguientes

- toolearn sobre generados por el servicio de copias de seguridad automáticas, consulte [copias de seguridad automáticas](sql-database-automated-backups.md)
- toolearn acerca de la retención de copia de seguridad a largo plazo, vea [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md)
- toolearn acerca de la restauración de copias de seguridad, consulte [restaurar copia de seguridad](sql-database-recovery-using-backups.md)
