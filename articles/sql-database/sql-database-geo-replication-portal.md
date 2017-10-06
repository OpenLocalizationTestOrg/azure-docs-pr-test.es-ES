---
title: "Azure Portal: replicación geográfica de SQL Database | Microsoft Docs"
description: "Configurar la replicación geográfica para la base de datos de SQL Azure en el portal de Azure de Hola y de conmutación por error de inicio"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="1b41c-103">Configurar la replicación geográfica activa para base de datos de SQL Azure en el portal de Azure de Hola y de conmutación por error de inicio</span><span class="sxs-lookup"><span data-stu-id="1b41c-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="1b41c-104">Este artículo muestra cómo tooconfigure replicación geográfica activa para base de datos SQL en hello [portal de Azure](http://portal.azure.com) y tooinitiate conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1b41c-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="1b41c-105">conmutación por error de tooinitiate con hello portal de Azure, consulte [iniciar una conmutación por error planeada o no planeada de la base de datos de SQL Azure con hello portal de Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b41c-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="1b41c-106">tooconfigure replicación geográfica activa mediante el uso de hello portal de Azure, necesita Hola siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="1b41c-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="1b41c-107">Una base de datos de SQL Azure: Hola base de datos principal que desea tooa tooreplicate otra región geográfica.</span><span class="sxs-lookup"><span data-stu-id="1b41c-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="1b41c-108">Replicación geográfica activa debe estar comprendido entre bases de datos de hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="1b41c-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="1b41c-109">Agregar una base de datos secundaria</span><span class="sxs-lookup"><span data-stu-id="1b41c-109">Add a secondary database</span></span>
<span data-ttu-id="1b41c-110">Hello pasos siguientes crea una nueva base de datos secundaria en una asociación de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="1b41c-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="1b41c-111">tooadd una base de datos secundaria, debe ser propietario de la suscripción de Hola o copropietario.</span><span class="sxs-lookup"><span data-stu-id="1b41c-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="1b41c-112">base de datos secundaria de Hello tiene el mismo nombre como base de datos principal de Hola de Hola y tiene, de forma predeterminada, Hola mismo nivel de servicio.</span><span class="sxs-lookup"><span data-stu-id="1b41c-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="1b41c-113">base de datos secundaria de Hello puede ser una sola base de datos o una base de datos en un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="1b41c-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="1b41c-114">Para obtener más información, consulte el artículo sobre [niveles de servicio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="1b41c-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="1b41c-115">Después de crear y propagado Hola secundaria, datos comienzan a replicarse de hello base de datos principal toohello nueva base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="1b41c-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="1b41c-116">Si la base de datos de hello asociado ya existe (por ejemplo, como resultado de terminación de una relación de replicación geográfica anterior) Hola comando produce un error.</span><span class="sxs-lookup"><span data-stu-id="1b41c-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="1b41c-117">Hola [portal de Azure](http://portal.azure.com), examinar la base de datos de toohello que desea tooset hacia arriba para replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="1b41c-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="1b41c-118">En la página de base de datos SQL de hello, seleccione **georreplicación**y, a continuación, seleccione Hola región toocreate Hola base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="1b41c-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="1b41c-119">Puede seleccionar una región distinta de región de Hola que hospeda la base de datos principal de hello, pero se recomienda hello [región emparejada](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="1b41c-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configuración de la replicación geográfica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="1b41c-121">Seleccione o configurar el servidor de Hola y el nivel de precios para base de datos secundaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Configuración de la secundaria](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="1b41c-123">Si lo desea, puede agregar un grupo elástico de base de datos secundaria tooan.</span><span class="sxs-lookup"><span data-stu-id="1b41c-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="1b41c-124">toocreate Hola base de datos secundaria un grupo, haga clic en **grupo elástico** y seleccione un grupo en el servidor de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="1b41c-125">Ya debe existir un grupo en el servidor de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="1b41c-126">Este flujo de trabajo no crea un grupo.</span><span class="sxs-lookup"><span data-stu-id="1b41c-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="1b41c-127">Haga clic en **crear** tooadd Hola secundaria.</span><span class="sxs-lookup"><span data-stu-id="1b41c-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="1b41c-128">se crea la base de datos secundaria de Hola y Hola propagación proceso comienza.</span><span class="sxs-lookup"><span data-stu-id="1b41c-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Configuración de la secundaria](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="1b41c-130">Una vez completada Hola proceso de transferencia, base de datos secundaria de hello muestra su estado.</span><span class="sxs-lookup"><span data-stu-id="1b41c-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Propagación completa](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="1b41c-132">Inicio de una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="1b41c-132">Initiate a failover</span></span>

<span data-ttu-id="1b41c-133">base de datos secundaria de Hello puede ser toobecome conmutada Hola principal.</span><span class="sxs-lookup"><span data-stu-id="1b41c-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="1b41c-134">Hola [portal de Azure](http://portal.azure.com), examinar toohello base de datos principal en colaboración de replicación geográfica de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="1b41c-135">En la hoja de la base de datos SQL de hello, seleccione **toda la configuración de** > **georreplicación**.</span><span class="sxs-lookup"><span data-stu-id="1b41c-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="1b41c-136">Hola **secundarias** lista, base de datos de hello seleccione desea toobecome Hola nuevo elemento principal y haga clic en **conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="1b41c-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![Conmutación por error](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="1b41c-138">Haga clic en **Sí** conmutación por error de toobegin Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="1b41c-139">comando de Hello cambia inmediatamente base de datos secundaria de hello en rol principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="1b41c-140">Hay un breve período durante el cual ambas bases de datos no están disponibles (en orden de Hola de 0 segundos too25) mientras conmutación de roles de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="1b41c-141">Si la base de datos principal de hello tiene varias bases de datos secundarias, comando hello automáticamente reconfigura Hola otro secundarias tooconnect toohello nuevo elemento principal.</span><span class="sxs-lookup"><span data-stu-id="1b41c-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="1b41c-142">toda operación de Hello tardará menos de un minuto toocomplete en circunstancias normales.</span><span class="sxs-lookup"><span data-stu-id="1b41c-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="1b41c-143">Este comando está diseñado para una rápida recuperación de base de datos de hello en el caso de una interrupción.</span><span class="sxs-lookup"><span data-stu-id="1b41c-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="1b41c-144">Desencadena una conmutación por error sin sincronización de datos (conmutación por error forzada).</span><span class="sxs-lookup"><span data-stu-id="1b41c-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="1b41c-145">Si Hola principal está en línea y confirmación de transacciones cuando se emite el comando de hello alguna pérdida de datos puede producir.</span><span class="sxs-lookup"><span data-stu-id="1b41c-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="1b41c-146">Elimine una base de datos secundaria</span><span class="sxs-lookup"><span data-stu-id="1b41c-146">Remove secondary database</span></span>
<span data-ttu-id="1b41c-147">Esta operación finaliza permanentemente la base de datos secundaria de hello replicación toohello y cambios Hola rol de base de datos de lectura y escritura normal de hello tooa secundaria.</span><span class="sxs-lookup"><span data-stu-id="1b41c-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="1b41c-148">Si se interrumpe la base de datos secundaria de hello conectividad toohello, comando Hola se realiza correctamente pero Hola secundaria hace que no se convierten en lectura y escritura hasta que una vez restaurada la conectividad.</span><span class="sxs-lookup"><span data-stu-id="1b41c-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="1b41c-149">Hola [portal de Azure](http://portal.azure.com), examinar toohello base de datos principal en colaboración de replicación geográfica de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="1b41c-150">En la página de base de datos SQL de hello, seleccione **georreplicación**.</span><span class="sxs-lookup"><span data-stu-id="1b41c-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="1b41c-151">Hola **secundarias** lista, base de datos de hello seleccione desea tooremove de perfil de replicación geográfica de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="1b41c-152">Haga clic en **Detener replicación**.</span><span class="sxs-lookup"><span data-stu-id="1b41c-152">Click **Stop Replication**.</span></span>
   
    ![Quitar secundaria](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="1b41c-154">Se abrirá una ventana de confirmación.</span><span class="sxs-lookup"><span data-stu-id="1b41c-154">A confirmation window opens.</span></span> <span data-ttu-id="1b41c-155">Haga clic en **Sí** base de datos de tooremove Hola de perfil de replicación geográfica de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b41c-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="1b41c-156">(Establecer base de datos de lectura y escritura de tooa no forma parte de ninguna replicación.)</span><span class="sxs-lookup"><span data-stu-id="1b41c-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b41c-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b41c-157">Next steps</span></span>
* <span data-ttu-id="1b41c-158">toolearn más información acerca de la replicación geográfica activa, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b41c-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="1b41c-159">Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="1b41c-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

