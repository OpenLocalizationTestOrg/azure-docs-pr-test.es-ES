---
title: "aaaStore base de datos de SQL Azure copias de seguridad de los años too10 | Documentos de Microsoft"
description: "Obtenga información acerca de la base de datos de SQL Azure admite almacenar copias de seguridad para too10 años."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="ec494-103">Almacenar copias de seguridad de base de datos de SQL Azure para too10 años</span><span class="sxs-lookup"><span data-stu-id="ec494-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="ec494-104">Muchas aplicaciones tienen normativas, cumplimiento y otras empresas que requieren las copias de seguridad de base de datos de tooretain más allá de hello 7-35 días proporcionadas por base de datos de SQL Azure con fines [copias de seguridad automáticas](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="ec494-105">Mediante la característica de copia de seguridad de retención a largo plazo de Hola, puede almacenar las copias de seguridad de la base de datos SQL en un almacén de servicios de recuperación de Azure para too10 años.</span><span class="sxs-lookup"><span data-stu-id="ec494-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="ec494-106">Puede almacenar hasta too1, 000 bases de datos por almacén.</span><span class="sxs-lookup"><span data-stu-id="ec494-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="ec494-107">A continuación, puede seleccionar cualquier copia de seguridad en hello almacén toorestore como una base de datos.</span><span class="sxs-lookup"><span data-stu-id="ec494-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec494-108">Retención de copia de seguridad a largo plazo es actualmente en versión preliminar y está disponible en hello siguientes regiones: Australia Oriental, sudeste de Australia, sur de Brasil, Central EE. UU., Asia oriental, UU, UU 2, India Central, sur de India, este de Japón, oeste de Japón, Ee.uu. Central Norte, Norte Europa, sur Central US, sudeste de Asia, Europa occidental y oeste de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="ec494-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="ec494-109">Puede habilitar la seguridad de bases de datos de too200 por almacén durante un período de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ec494-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="ec494-110">Se recomienda que use un almacén independiente para cada impacto de hello toominimize de servidor de este límite.</span><span class="sxs-lookup"><span data-stu-id="ec494-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="ec494-111">¿Cómo funciona la retención de copias de seguridad a largo plazo de SQL Database?</span><span class="sxs-lookup"><span data-stu-id="ec494-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="ec494-112">Con la retención de copias de seguridad a largo plazo, puede asociar un servidor de bases de datos SQL a un almacén de Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="ec494-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="ec494-113">Debe crear el almacén de Hola Hola misma suscripción de Azure que crea Hola SQL server y en Hola mismo grupo de recursos y la región geográfico.</span><span class="sxs-lookup"><span data-stu-id="ec494-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="ec494-114">A continuación, configure una directiva de retención para cualquier base de datos.</span><span class="sxs-lookup"><span data-stu-id="ec494-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="ec494-115">toobe Hola directiva causas Hola semanal completa de la base de datos las copias de seguridad copia toohello el almacén de servicios de recuperación y se conserva durante el período de retención especificado hello (arriba too10 años).</span><span class="sxs-lookup"><span data-stu-id="ec494-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="ec494-116">A continuación, puede restaurar base de datos de Hola desde cualquiera de estas copias de seguridad tooa nueva base de datos en cualquier servidor de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="ec494-117">Almacenamiento de Azure crea una copia de las copias de seguridad existentes, y copia de hello no tiene ningún impacto en el rendimiento en la base de datos existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="ec494-118">Para un tooguide cómo, consulte [configurar y restauración de retención de copia de seguridad a largo plazo de base de datos de SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="ec494-119">Habilitación de la retención de copias de seguridad a largo plazo</span><span class="sxs-lookup"><span data-stu-id="ec494-119">Enable long-term backup retention</span></span>

<span data-ttu-id="ec494-120">tooconfigure retención de copia de seguridad a largo plazo para una base de datos:</span><span class="sxs-lookup"><span data-stu-id="ec494-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="ec494-121">Cree un almacén de servicios de recuperación de Azure en hello mismo grupo de recursos, región y suscripción que el servidor de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="ec494-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="ec494-122">Registrar el almacén de hello server toohello.</span><span class="sxs-lookup"><span data-stu-id="ec494-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="ec494-123">Cree una directiva de protección de Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="ec494-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="ec494-124">Aplicar Hola protección directiva toohello las bases de datos que requieren la retención de copia de seguridad a largo plazo.</span><span class="sxs-lookup"><span data-stu-id="ec494-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="ec494-125">tooconfigure, administrar y restaurar una base de datos de retención de copia de seguridad a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure, realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="ec494-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="ec494-126">Uso de Hola portal de Azure: haga clic en **retención de copia de seguridad a largo plazo**, seleccione una base de datos y, a continuación, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="ec494-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Seleccionar base de datos para retención de copias de seguridad a largo plazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="ec494-128">Uso de PowerShell: Vaya demasiado[configurar y restauración de retención de copia de seguridad a largo plazo de base de datos de SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="ec494-129">Restaurar una base de datos que se almacena junto con la característica de copia de seguridad de retención a largo plazo de Hola</span><span class="sxs-lookup"><span data-stu-id="ec494-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="ec494-130">toorecover desde una copia de seguridad a largo plazo de retención de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="ec494-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="ec494-131">Almacén de Hola de lista donde se almacena la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="ec494-132">Contenedor de Hola de lista es servidor lógico tooyour asignada.</span><span class="sxs-lookup"><span data-stu-id="ec494-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="ec494-133">Origen de datos de lista hello en el almacén de Hola que está asignada tooyour base de datos de.</span><span class="sxs-lookup"><span data-stu-id="ec494-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="ec494-134">Puntos de recuperación hello en el lista que están disponible toorestore.</span><span class="sxs-lookup"><span data-stu-id="ec494-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="ec494-135">Restaurar base de datos de Hola Hola recuperación toohello de punto de servidor de destino dentro de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="ec494-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="ec494-136">tooconfigure, administrar y restaurar una base de datos de retención de copia de seguridad a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure, realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="ec494-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="ec494-137">Uso de Hola portal de Azure: vaya demasiado[retención de copia de seguridad a largo plazo de administrar mediante Hola portal de Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="ec494-138">Uso de PowerShell: Vaya demasiado[administrar la retención de copia de seguridad a largo plazo con PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="ec494-139">Obtención de precios para la retención de copias de seguridad a largo plazo</span><span class="sxs-lookup"><span data-stu-id="ec494-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="ec494-140">Retención de copia de seguridad a largo plazo de una base de datos SQL se cobra según toohello [las tasas de precios de servicios de copia de seguridad Azure](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="ec494-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="ec494-141">Después de servidor de base de datos SQL de hello es el almacén de toohello registrado, se le cobra por almacenamiento total de Hola que usa Hola semanal copias de seguridad almacenadas en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="ec494-142">Consulta de las copias de seguridad disponibles almacenadas en retención de copias de seguridad a largo plazo</span><span class="sxs-lookup"><span data-stu-id="ec494-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="ec494-143">tooconfigure, administrar y restaurar una base de datos de retención de copia de seguridad a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure mediante Hola portal de Azure, realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="ec494-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="ec494-144">Uso de Hola portal de Azure: vaya demasiado[retención de copia de seguridad a largo plazo de administrar mediante Hola portal de Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="ec494-145">Uso de PowerShell: Vaya demasiado[administrar la retención de copia de seguridad a largo plazo con PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="ec494-146">Deshabilitación de la retención a largo plazo</span><span class="sxs-lookup"><span data-stu-id="ec494-146">Disable long-term retention</span></span>

<span data-ttu-id="ec494-147">servicio de recuperación de Hello controla automáticamente la limpieza de Hola de copias de seguridad según Hola proporcionada la directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="ec494-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="ec494-148">las copias de seguridad Hola envío toostop, para un depósito de toohello de base de datos específica, quite la directiva de retención de Hola para esa base de datos.</span><span class="sxs-lookup"><span data-stu-id="ec494-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="ec494-149">las copias de seguridad de Hola que ya están en el almacén de Hola se ven afectados.</span><span class="sxs-lookup"><span data-stu-id="ec494-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="ec494-150">Se eliminan automáticamente por el servicio de recuperación de hello cuando expira el período de retención.</span><span class="sxs-lookup"><span data-stu-id="ec494-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="ec494-151">Preguntas frecuentes sobre la retención de copias de seguridad a largo plazo</span><span class="sxs-lookup"><span data-stu-id="ec494-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="ec494-152">**¿Se puede eliminar manualmente las copias de seguridad específicos en el almacén de hello?**</span><span class="sxs-lookup"><span data-stu-id="ec494-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="ec494-153">Actualmente, no.</span><span class="sxs-lookup"><span data-stu-id="ec494-153">Not currently.</span></span> <span data-ttu-id="ec494-154">almacén de Hello limpia automáticamente las copias de seguridad cuando ha expirado el período de retención de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="ec494-155">**¿Puedo registrar mi toomore de copias de seguridad de servidor toostore a un depósito?**</span><span class="sxs-lookup"><span data-stu-id="ec494-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="ec494-156">No, actualmente puede almacenar un depósito de tooonly de las copias de seguridad a la vez.</span><span class="sxs-lookup"><span data-stu-id="ec494-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="ec494-157">**¿Puedo tener un almacén y un servidor en suscripciones distintas?**</span><span class="sxs-lookup"><span data-stu-id="ec494-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="ec494-158">No, actualmente el almacén de Hola y servidor deben estar en hello mismo grupo de recursos y de suscripción.</span><span class="sxs-lookup"><span data-stu-id="ec494-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="ec494-159">**¿Puedo usar un almacén que he creado en una región que es distinta a la de mi servidor?**</span><span class="sxs-lookup"><span data-stu-id="ec494-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="ec494-160">No, el almacén de Hola y servidor deben estar en hello mismo toominimize de región, copie el tiempo y evitar cargos de tráfico.</span><span class="sxs-lookup"><span data-stu-id="ec494-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="ec494-161">**¿Cuántas bases de datos puedo guardar en un almacén?**</span><span class="sxs-lookup"><span data-stu-id="ec494-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="ec494-162">Actualmente, se admiten la too1, 000 bases de datos por almacén.</span><span class="sxs-lookup"><span data-stu-id="ec494-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="ec494-163">**¿Cuántos almacenes puedo crear por suscripción?**</span><span class="sxs-lookup"><span data-stu-id="ec494-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="ec494-164">Puede crear hasta too25 almacenes por suscripción.</span><span class="sxs-lookup"><span data-stu-id="ec494-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="ec494-165">**¿Cuántas bases de datos puedo configurar diariamente por almacén?**</span><span class="sxs-lookup"><span data-stu-id="ec494-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="ec494-166">Puede configurar 200 bases de datos diariamente por almacén.</span><span class="sxs-lookup"><span data-stu-id="ec494-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="ec494-167">**¿La retención de copias de seguridad a largo plazo funciona con grupos elásticos?**</span><span class="sxs-lookup"><span data-stu-id="ec494-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="ec494-168">Sí.</span><span class="sxs-lookup"><span data-stu-id="ec494-168">Yes.</span></span> <span data-ttu-id="ec494-169">Cualquier base de datos en bloque de hello puede configurarse con la directiva de retención de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="ec494-170">**¿Se puede elegir tiempo hello en que se creó la copia de seguridad de hello?**</span><span class="sxs-lookup"><span data-stu-id="ec494-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="ec494-171">No, base de datos SQL controla Hola programar copia de seguridad toominimize Hola impacto en el rendimiento en las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="ec494-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="ec494-172">**Si dispone de cifrado de datos transparente habilitado para la base de datos. ¿Puedo utilizarlo con el almacén de hello?**</span><span class="sxs-lookup"><span data-stu-id="ec494-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="ec494-173">Si, se admite el cifrado de datos transparente.</span><span class="sxs-lookup"><span data-stu-id="ec494-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="ec494-174">Puede restaurar base de datos de hello del almacén de hello incluso si la base de datos original de hello ya no existe.</span><span class="sxs-lookup"><span data-stu-id="ec494-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="ec494-175">**¿Qué ocurre con las copias de seguridad de hello en el almacén de hello si se suspende mi suscripción?**</span><span class="sxs-lookup"><span data-stu-id="ec494-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="ec494-176">Si la suscripción está suspendida, se conservan las copias de seguridad y bases de datos existentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="ec494-177">Nuevas copias de seguridad no son almacén toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="ec494-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="ec494-178">Después de reactivar la suscripción de hello, servicio de hello vuelve a copiar el almacén de copias de seguridad toohello.</span><span class="sxs-lookup"><span data-stu-id="ec494-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="ec494-179">El almacén se convierte en operaciones de restauración toohello accesible mediante copias de seguridad de Hola que se copiaron existe antes de que se suspendió la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec494-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="ec494-180">**¿Puedo obtener acceso a archivos de copia de seguridad de base de datos SQL toohello para que puedo descargar o restaurarlas toohello SQL server?**</span><span class="sxs-lookup"><span data-stu-id="ec494-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="ec494-181">Actualmente, no.</span><span class="sxs-lookup"><span data-stu-id="ec494-181">No, not currently.</span></span>

<span data-ttu-id="ec494-182">**Es posible toohave todas las programaciones (diaria, semanal, mensual, anual) dentro de una directiva de retención SQL.**</span><span class="sxs-lookup"><span data-stu-id="ec494-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="ec494-183">No, actualmente solo están disponibles varias programaciones para las copias de seguridad de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ec494-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="ec494-184">**¿Qué ocurre si establecemos la retención de copias de seguridad a largo plazo en una base de datos secundaria con replicación geográfica activa?**</span><span class="sxs-lookup"><span data-stu-id="ec494-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="ec494-185">Dado que no creamos copias de seguridad de réplicas, actualmente no hay ninguna opción para la retención de copias de seguridad a largo plazo en bases de datos secundarias.</span><span class="sxs-lookup"><span data-stu-id="ec494-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="ec494-186">Sin embargo, es importante para los usuarios tooset una retención de copia de seguridad a largo plazo en una base de datos de replicación geográfica activa secundaria por estos motivos:</span><span class="sxs-lookup"><span data-stu-id="ec494-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="ec494-187">Cuando se produce una conmutación por error y la base de datos de Hola se convierte en una base de datos principal, se hace una completa de copia de seguridad, que es cargado toovault.</span><span class="sxs-lookup"><span data-stu-id="ec494-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="ec494-188">No hay ningún extra costos toohello cliente para configurar la retención de copia de seguridad a largo plazo en una base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="ec494-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec494-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec494-189">Next steps</span></span>
<span data-ttu-id="ec494-190">Dado que las copias de seguridad de bases de datos protegen los datos de eliminaciones o daños accidentales, son una parte esencial de cualquier estrategia de recuperación ante desastres y de continuidad empresarial.</span><span class="sxs-lookup"><span data-stu-id="ec494-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="ec494-191">toolearn aproximadamente Hola otras soluciones de continuidad del negocio de base de datos SQL, consulte [información general sobre la continuidad de negocio](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="ec494-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
