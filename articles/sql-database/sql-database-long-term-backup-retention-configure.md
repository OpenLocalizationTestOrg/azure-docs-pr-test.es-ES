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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="6f60c-103">Configuración de la retención de copias de seguridad a largo plazo de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6f60c-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="6f60c-104">Puede configurar copias de seguridad de SQL Azure de hello servicios de recuperación de Azure almacén toostore y, a continuación, recuperar una base de datos con copias de seguridad se conserva en hello almacén con Hola portal de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f60c-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="6f60c-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6f60c-105">Azure portal</span></span>

<span data-ttu-id="6f60c-106">Hola siguientes secciones muestra también cómo almacén toouse Hola tooconfigure portal Azure Hola servicios de recuperación de Azure, ver las copias de seguridad en el almacén de Hola y restaurar desde el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="6f60c-107">Configurar el almacén de hello, Registrar servidor hello y seleccione las bases de datos</span><span class="sxs-lookup"><span data-stu-id="6f60c-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="6f60c-108">Se [configurar un copias de seguridad de servicios de recuperación de Azure almacén tooretain automatizada](sql-database-long-term-retention.md) para un periodo superior al período de retención de hello para el nivel de servicio.</span><span class="sxs-lookup"><span data-stu-id="6f60c-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="6f60c-109">Abra hello **SQL Server** página del servidor.</span><span class="sxs-lookup"><span data-stu-id="6f60c-109">Open hello **SQL Server** page for your server.</span></span>

   ![página de sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="6f60c-111">Haga clic en **Long-term backup retention** (Retención de copia de seguridad a largo plazo).</span><span class="sxs-lookup"><span data-stu-id="6f60c-111">Click **Long-term backup retention**.</span></span>

   ![vínculo de retención de copia de seguridad a largo plazo](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="6f60c-113">En hello **retención de copia de seguridad a largo plazo** página para el servidor, revise y acepte los términos de vista previa de hello (a menos que aún lo ha hecho - o esta característica ya no está en vista previa).</span><span class="sxs-lookup"><span data-stu-id="6f60c-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![Acepte los términos de vista previa de Hola](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="6f60c-115">retención de copia de seguridad a largo plazo de tooconfigure, seleccione esa base de datos en la cuadrícula de hello y, a continuación, haga clic en **configurar** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![seleccionar base de datos para retención de copia de seguridad a largo plazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="6f60c-117">En hello **configurar** página, haga clic en **establecer configuración obligatoria** en **almacén del servicio de recuperación de**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![vínculo para configurar almacén](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="6f60c-119">En hello **almacén de servicios de recuperación** , seleccione un almacén existente, si existe.</span><span class="sxs-lookup"><span data-stu-id="6f60c-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="6f60c-120">En caso contrario, si ningún almacén de servicios de recuperación encontró para la suscripción, haga clic en el flujo de hello tooexit y crear un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="6f60c-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![crear vinculo de almacén](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="6f60c-122">En hello **servicios de recuperación de los almacenes de credenciales** página, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![agregar vinculo de almacén](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="6f60c-124">En hello **del almacén de servicios de recuperación** , proporcione un nombre válido para el almacén de servicios de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![nuevo nombre de almacén](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="6f60c-126">Seleccione la suscripción y el grupo de recursos y, a continuación, seleccione la ubicación de hello para el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="6f60c-127">Cuando termine, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-127">When done, click **Create**.</span></span>

   ![crear almacén](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="6f60c-129">almacén de Hello debe estar ubicado en Hola misma región que el servidor lógico de SQL Azure de Hola y debe usar Hola mismo grupo de recursos que el servidor lógico de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="6f60c-130">Después de crea el nuevo almacén de hello, ejecute hello pasos necesarios tooreturn toohello **almacén de servicios de recuperación** página.</span><span class="sxs-lookup"><span data-stu-id="6f60c-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="6f60c-131">En hello **almacén de servicios de recuperación** página, haga clic en el almacén de hello y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![seleccionar almacén existente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="6f60c-133">En hello **configurar** página, proporcione un nombre válido para la nueva directiva de retención hello, modificar la directiva de retención predeterminada de hello según corresponda y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![definir directiva de retención](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="6f60c-135">En hello **retención de copia de seguridad a largo plazo** página de la base de datos, haga clic en **guardar** y, a continuación, haga clic en **Aceptar** tooapply Hola a largo plazo tooall de directiva de retención de copia de seguridad seleccionada bases de datos.</span><span class="sxs-lookup"><span data-stu-id="6f60c-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![definir directiva de retención](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="6f60c-137">Haga clic en **guardar** tooenable retención de copia de seguridad a largo plazo con este nuevo almacén de servicios de recuperación de Azure de toohello de directiva que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="6f60c-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![definir directiva de retención](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="6f60c-139">Una vez configurado, las copias de seguridad aparecen en el almacén de hello en siete días siguientes.</span><span class="sxs-lookup"><span data-stu-id="6f60c-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="6f60c-140">No continúe con este tutorial hasta que las copias de seguridad que se mostrarán en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="6f60c-141">Visualización de copias de seguridad en retención a largo plazo mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6f60c-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="6f60c-142">Visualización de información acerca de las copias de seguridad de su base de datos en la [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="6f60c-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="6f60c-143">En el portal de Azure de Hola, abrir el almacén de servicios de recuperación de Azure para las copias de seguridad de base de datos (ir demasiado**todos los recursos** y selecciónelo en la lista de Hola de los recursos de su suscripción) tooview cantidad de Hola de almacenamiento utilizado por la base de datos copias de seguridad en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![ver almacén de servicios de recuperación con copias de seguridad](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="6f60c-145">Abra hello **base de datos SQL** página de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6f60c-145">Open hello **SQL database** page for your database.</span></span>

   ![página nueva de base de datos de ejemplo](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="6f60c-147">En la barra de herramientas de hello, haga clic en **restaurar**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-147">On hello toolbar, click **Restore**.</span></span>

   ![barra de herramientas restaurar](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="6f60c-149">En la página de la restauración de hello, haga clic en **a largo plazo**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="6f60c-150">En copias de seguridad del almacén de Azure, haga clic en **Seleccionar copia de seguridad** tooview copias de seguridad de bases de datos disponibles de hello en retención de copia de seguridad a largo plazo.</span><span class="sxs-lookup"><span data-stu-id="6f60c-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![copias de seguridad en almacén](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="6f60c-152">Restaurar una base de datos desde una copia de seguridad de retención de copia de seguridad a largo plazo con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6f60c-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="6f60c-153">Restaurar hello tooa nueva base de datos desde una copia de seguridad en hello que del almacén de servicios de recuperación de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f60c-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="6f60c-154">En hello **copias de seguridad del almacén de Azure** página, haga clic en toorestore de copia de seguridad de hello y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="6f60c-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![seleccionar copia de seguridad en almacén](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="6f60c-156">Hola **nombre de base de datos** texto cuadro, proporcione el nombre hello para la base de datos de hello restaurado.</span><span class="sxs-lookup"><span data-stu-id="6f60c-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![nombre de nueva base de datos](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="6f60c-158">Haga clic en **Aceptar** toorestore la base de datos de copia de seguridad de Hola Hola almacén toohello nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="6f60c-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="6f60c-159">En la barra de herramientas de hello, haga clic en estado hello tooview de icono de notificación de Hola de trabajo de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![progreso de trabajo de restauración del almacén](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="6f60c-161">Cuando se completa el trabajo de restauración de hello, abra hello **bases de datos SQL** base de datos de página tooview Hola recién restaurado.</span><span class="sxs-lookup"><span data-stu-id="6f60c-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![base de datos restaurada desde almacén](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="6f60c-163">Desde aquí, puede conectarse toohello Restaurar base de datos mediante las tareas de SQL Server Management Studio tooperform necesitado, como demasiado[extraer una porción de datos de toocopy de hello Restaurar base de datos en la base de datos existente de Hola o toodelete Hola existente base de datos y cambiar el nombre hello Restaurar base de datos toohello existente en nombre de base de datos](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="6f60c-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="6f60c-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f60c-164">PowerShell</span></span>

<span data-ttu-id="6f60c-165">Hola las secciones siguientes muestra cómo ver las copias de seguridad en el almacén de hello toouse PowerShell tooconfigure Hola el almacén de servicios de recuperación de Azure y restaurar desde el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6f60c-166">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="6f60c-166">Create a recovery services vault</span></span>

<span data-ttu-id="6f60c-167">Hola de uso [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate una recuperación del almacén de servicios.</span><span class="sxs-lookup"><span data-stu-id="6f60c-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f60c-168">almacén de Hello debe estar ubicado en Hola misma región que el servidor lógico de SQL Azure de Hola y debe usar Hola mismo grupo de recursos que el servidor lógico de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="6f60c-169">Establecer el almacén de recuperación de servidor toouse Hola para sus copias de seguridad de retención a largo plazo</span><span class="sxs-lookup"><span data-stu-id="6f60c-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="6f60c-170">Hola de uso [AzureRmSqlServerBackupLongTermRetentionVault conjunto](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate cmdlet creado anteriormente con un servidor SQL Azure específico del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="6f60c-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="6f60c-171">Creación de una directiva de retención</span><span class="sxs-lookup"><span data-stu-id="6f60c-171">Create a retention policy</span></span>

<span data-ttu-id="6f60c-172">Una directiva de retención es donde se establece tookeep cuánto tiempo una copia de seguridad de base de datos.</span><span class="sxs-lookup"><span data-stu-id="6f60c-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="6f60c-173">Hola de uso [AzureRmRecoveryServicesBackupRetentionPolicyObject Get](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet toouse de directiva de retención tooget Hola predeterminado como plantilla de Hola para crear directivas de.</span><span class="sxs-lookup"><span data-stu-id="6f60c-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="6f60c-174">En esta plantilla, se establece el período de retención de Hola durante dos años.</span><span class="sxs-lookup"><span data-stu-id="6f60c-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="6f60c-175">A continuación, ejecute hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Crear directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="6f60c-176">Algunos cmdlets requieren que se establece el contexto de almacén de hello antes de ejecutar ([AzureRmRecoveryServicesVaultContext Set](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) para ver este cmdlet en algunos fragmentos de código relacionados.</span><span class="sxs-lookup"><span data-stu-id="6f60c-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="6f60c-177">Para establecer el contexto de hello porque la directiva de hello es parte del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f60c-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="6f60c-178">Puede crear varias directivas de retención para cada almacén y, a continuación, aplicar las bases de datos de hello deseado directiva toospecific.</span><span class="sxs-lookup"><span data-stu-id="6f60c-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="6f60c-179">Configurar una directiva de retención de base de datos toouse Hola definido anteriormente</span><span class="sxs-lookup"><span data-stu-id="6f60c-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="6f60c-180">Hola de uso [AzureRmSqlDatabaseBackupLongTermRetentionPolicy conjunto](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply Hola nueva directiva tooa base de datos específica.</span><span class="sxs-lookup"><span data-stu-id="6f60c-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="6f60c-181">Visualización de la información sobre copias de seguridad y copias de seguridad con retención a largo plazo</span><span class="sxs-lookup"><span data-stu-id="6f60c-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="6f60c-182">Visualización de información acerca de las copias de seguridad de su base de datos en la [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="6f60c-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="6f60c-183">Usar hello siguiendo la información de copia de seguridad de tooview de cmdlets:</span><span class="sxs-lookup"><span data-stu-id="6f60c-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="6f60c-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="6f60c-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="6f60c-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="6f60c-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="6f60c-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="6f60c-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="6f60c-187">Restauración de una base de datos de una copia de seguridad con retención a largo plazo</span><span class="sxs-lookup"><span data-stu-id="6f60c-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="6f60c-188">Restaurar a partir de retención de copia de seguridad a largo plazo usa hello [AzureRmSqlDatabase restauración](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6f60c-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

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
> <span data-ttu-id="6f60c-189">Desde aquí, puede conectarse toohello Restaurar base de datos mediante las tareas de SQL Server Management Studio tooperform necesarios, como tooextract una porción de datos de hello restaura toocopy de base de datos en base de datos existente de Hola o base de datos existente de toodelete Hola y el nombre Hola restaura el nombre de base de datos existente de base de datos toohello.</span><span class="sxs-lookup"><span data-stu-id="6f60c-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="6f60c-190">Consulte la [restauración a un momento dado](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="6f60c-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f60c-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f60c-191">Next steps</span></span>

- <span data-ttu-id="6f60c-192">toolearn sobre generados por el servicio de copias de seguridad automáticas, consulte [copias de seguridad automáticas](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="6f60c-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="6f60c-193">toolearn acerca de la retención de copia de seguridad a largo plazo, vea [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="6f60c-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="6f60c-194">toolearn acerca de la restauración de copias de seguridad, consulte [restaurar copia de seguridad](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="6f60c-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
