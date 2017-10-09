---
title: aaaMigrate toopremium almacenamiento del almacenamiento de los datos existentes de Azure | Documentos de Microsoft
description: "Instrucciones para migrar un almacenamiento de toopremium de almacén de datos existente"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="14cf6-103">Migrar el almacenamiento de toopremium de almacén de datos</span><span class="sxs-lookup"><span data-stu-id="14cf6-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="14cf6-104">Azure SQL Data Warehouse ha introducido recientemente [Premium Storage para poder predecir el rendimiento de manera más eficaz][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="14cf6-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="14cf6-105">Ahora pueden ser almacenamientos actualmente en almacenamiento estándar los datos existentes migran toopremium almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="14cf6-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="14cf6-106">Puede aprovechar las ventajas de la migración automática, o si prefiere toocontrol cuando toomigrate (que implican cierto tiempo de inactividad), puede hacer Hola migración usted mismo.</span><span class="sxs-lookup"><span data-stu-id="14cf6-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="14cf6-107">Si tiene más de un almacén de datos, usar hello [programación de la migración automática] [ automatic migration schedule] toodetermine cuando también se migrarán.</span><span class="sxs-lookup"><span data-stu-id="14cf6-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="14cf6-108">Determinación del tipo de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="14cf6-108">Determine storage type</span></span>
<span data-ttu-id="14cf6-109">Si ha creado un almacén de datos antes de hello siguiendo las fechas, están usando actualmente almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="14cf6-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="14cf6-110">**Región**</span><span class="sxs-lookup"><span data-stu-id="14cf6-110">**Region**</span></span> | <span data-ttu-id="14cf6-111">**Almacenamiento de datos creado antes de esta fecha**</span><span class="sxs-lookup"><span data-stu-id="14cf6-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="14cf6-112">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="14cf6-112">Australia East</span></span> |<span data-ttu-id="14cf6-113">Premium Storage no está disponible todavía</span><span class="sxs-lookup"><span data-stu-id="14cf6-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="14cf6-114">Este de China</span><span class="sxs-lookup"><span data-stu-id="14cf6-114">China East</span></span> |<span data-ttu-id="14cf6-115">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="14cf6-115">November 1, 2016</span></span> |
| <span data-ttu-id="14cf6-116">Norte de China</span><span class="sxs-lookup"><span data-stu-id="14cf6-116">China North</span></span> |<span data-ttu-id="14cf6-117">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="14cf6-117">November 1, 2016</span></span> |
| <span data-ttu-id="14cf6-118">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="14cf6-118">Germany Central</span></span> |<span data-ttu-id="14cf6-119">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="14cf6-119">November 1, 2016</span></span> |
| <span data-ttu-id="14cf6-120">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="14cf6-120">Germany Northeast</span></span> |<span data-ttu-id="14cf6-121">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="14cf6-121">November 1, 2016</span></span> |
| <span data-ttu-id="14cf6-122">India occidental</span><span class="sxs-lookup"><span data-stu-id="14cf6-122">India West</span></span> |<span data-ttu-id="14cf6-123">Premium Storage no está disponible todavía</span><span class="sxs-lookup"><span data-stu-id="14cf6-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="14cf6-124">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="14cf6-124">Japan West</span></span> |<span data-ttu-id="14cf6-125">Premium Storage no está disponible todavía</span><span class="sxs-lookup"><span data-stu-id="14cf6-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="14cf6-126">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="14cf6-126">North Central US</span></span> |<span data-ttu-id="14cf6-127">10 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="14cf6-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="14cf6-128">Información de la migración automática</span><span class="sxs-lookup"><span data-stu-id="14cf6-128">Automatic migration details</span></span>
<span data-ttu-id="14cf6-129">De forma predeterminada, se migrará la base de datos automáticamente entre 6:00 P.M. y las 6:00 A.M. en hora local de su región durante Hola [programación de la migración automática][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="14cf6-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="14cf6-130">Durante la migración de hello será inutilizable el almacenamiento de datos existente.</span><span class="sxs-lookup"><span data-stu-id="14cf6-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="14cf6-131">migración de Hello tardará aproximadamente una hora por terabyte de almacenamiento de cada almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="14cf6-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="14cf6-132">No se le cobrará durante cualquier parte de la migración automática de Hola.</span><span class="sxs-lookup"><span data-stu-id="14cf6-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="14cf6-133">Una vez completada la migración de hello, será el almacenamiento de datos nuevo en línea y se puede usar.</span><span class="sxs-lookup"><span data-stu-id="14cf6-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="14cf6-134">Microsoft está llevando a cabo Hola después de la migración de hello toocomplete pasos (estos archivos no requieren ninguna intervención por parte del usuario).</span><span class="sxs-lookup"><span data-stu-id="14cf6-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="14cf6-135">Para este ejemplo, imagine que su almacenamiento de datos del almacenamiento estándar actualmente se llama "MiAD".</span><span class="sxs-lookup"><span data-stu-id="14cf6-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="14cf6-136">Microsoft cambia el nombre "MyDW" demasiado "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="14cf6-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="14cf6-137">Microsoft pausa "MiAD_DO_NOT_USE_[Marca de tiempo]".</span><span class="sxs-lookup"><span data-stu-id="14cf6-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="14cf6-138">Durante este tiempo, se crea una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="14cf6-138">During this time, a backup is taken.</span></span> <span data-ttu-id="14cf6-139">Es posible que observe que se llevan a cabo varias tareas de pausa y reanudación si se producen problemas durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="14cf6-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="14cf6-140">Microsoft crea un nuevo almacén de datos denominado "MyDW" en almacenamiento premium, desde la copia de seguridad de hello realizada en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="14cf6-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="14cf6-141">"MyDW" no aparecerá hasta que una vez completada la restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="14cf6-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="14cf6-142">Una vez completada la restauración de hello, "MyDW" devuelve toohello unidades del almacenamiento de datos mismo y estado (en pausa o activa) que se encontraba antes de la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="14cf6-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="14cf6-143">Una vez completada la migración de hello, Microsoft elimina "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="14cf6-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="14cf6-144">Hello valores siguientes no se mantienen como parte de la migración de hello:</span><span class="sxs-lookup"><span data-stu-id="14cf6-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="14cf6-145">Auditoría de nivel de base de datos de hello debe toobe vuelve a habilitar.</span><span class="sxs-lookup"><span data-stu-id="14cf6-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="14cf6-146">Las reglas de Firewall en el nivel de base de datos de hello necesitan toobe agregarse de nuevo.</span><span class="sxs-lookup"><span data-stu-id="14cf6-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="14cf6-147">Las reglas de Firewall en el nivel de servidor hello no se ven afectadas.</span><span class="sxs-lookup"><span data-stu-id="14cf6-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="14cf6-148">programa de migración automática</span><span class="sxs-lookup"><span data-stu-id="14cf6-148">Automatic migration schedule</span></span>
<span data-ttu-id="14cf6-149">Migraciones automáticas se producen entre las 6:00 P.M. y las 6:00 A.M. (hora local por región) durante Hola siguiendo la programación de interrupción.</span><span class="sxs-lookup"><span data-stu-id="14cf6-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="14cf6-150">**Región**</span><span class="sxs-lookup"><span data-stu-id="14cf6-150">**Region**</span></span> | <span data-ttu-id="14cf6-151">**Fecha de inicio estimada**</span><span class="sxs-lookup"><span data-stu-id="14cf6-151">**Estimated start date**</span></span> | <span data-ttu-id="14cf6-152">**Fecha de finalización estimada**</span><span class="sxs-lookup"><span data-stu-id="14cf6-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="14cf6-153">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="14cf6-153">Australia East</span></span> |<span data-ttu-id="14cf6-154">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="14cf6-154">Not determined yet</span></span> |<span data-ttu-id="14cf6-155">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="14cf6-155">Not determined yet</span></span> |
| <span data-ttu-id="14cf6-156">Este de China</span><span class="sxs-lookup"><span data-stu-id="14cf6-156">China East</span></span> |<span data-ttu-id="14cf6-157">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-157">January 9, 2017</span></span> |<span data-ttu-id="14cf6-158">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-158">January 13, 2017</span></span> |
| <span data-ttu-id="14cf6-159">Norte de China</span><span class="sxs-lookup"><span data-stu-id="14cf6-159">China North</span></span> |<span data-ttu-id="14cf6-160">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-160">January 9, 2017</span></span> |<span data-ttu-id="14cf6-161">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-161">January 13, 2017</span></span> |
| <span data-ttu-id="14cf6-162">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="14cf6-162">Germany Central</span></span> |<span data-ttu-id="14cf6-163">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-163">January 9, 2017</span></span> |<span data-ttu-id="14cf6-164">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-164">January 13, 2017</span></span> |
| <span data-ttu-id="14cf6-165">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="14cf6-165">Germany Northeast</span></span> |<span data-ttu-id="14cf6-166">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-166">January 9, 2017</span></span> |<span data-ttu-id="14cf6-167">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-167">January 13, 2017</span></span> |
| <span data-ttu-id="14cf6-168">India occidental</span><span class="sxs-lookup"><span data-stu-id="14cf6-168">India West</span></span> |<span data-ttu-id="14cf6-169">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="14cf6-169">Not determined yet</span></span> |<span data-ttu-id="14cf6-170">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="14cf6-170">Not determined yet</span></span> |
| <span data-ttu-id="14cf6-171">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="14cf6-171">Japan West</span></span> |<span data-ttu-id="14cf6-172">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="14cf6-172">Not determined yet</span></span> |<span data-ttu-id="14cf6-173">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="14cf6-173">Not determined yet</span></span> |
| <span data-ttu-id="14cf6-174">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="14cf6-174">North Central US</span></span> |<span data-ttu-id="14cf6-175">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-175">January 9, 2017</span></span> |<span data-ttu-id="14cf6-176">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="14cf6-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="14cf6-177">Almacenamiento de migración automática toopremium</span><span class="sxs-lookup"><span data-stu-id="14cf6-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="14cf6-178">Si desea toocontrol cuando se producirá el tiempo de inactividad, puede usar Hola siguiendo los pasos toomigrate un almacén de datos existente en el almacenamiento de toopremium de almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="14cf6-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="14cf6-179">Si elige esta opción, debe completar la migración automática de Hola de antes de que comience la migración automática de hello en dicha región.</span><span class="sxs-lookup"><span data-stu-id="14cf6-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="14cf6-180">Esto garantiza que evitar los riesgos de la migración automática de hello causando un conflicto (consulte toohello [programación de la migración automática][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="14cf6-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="14cf6-181">Instrucciones de migración manual</span><span class="sxs-lookup"><span data-stu-id="14cf6-181">Self-migration instructions</span></span>
<span data-ttu-id="14cf6-182">toomigrate los datos del almacenamiento de usted mismo, usar copia de seguridad de Hola y restauración características.</span><span class="sxs-lookup"><span data-stu-id="14cf6-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="14cf6-183">parte de restauración de Hola de migración de hello es tootake esperado alrededor de una hora por terabyte de almacenamiento al almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="14cf6-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="14cf6-184">Si desea que hello tookeep mismo nombre una vez completada la migración, siga hello [toorename pasos durante la migración][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="14cf6-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="14cf6-185">[Detenga][Pause] el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="14cf6-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="14cf6-186">Esto realiza una copia de seguridad automática.</span><span class="sxs-lookup"><span data-stu-id="14cf6-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="14cf6-187">Lleve a cabo la [restauración][Restore] a partir de la instantánea más reciente.</span><span class="sxs-lookup"><span data-stu-id="14cf6-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="14cf6-188">Elimine el almacenamiento de datos existente del almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="14cf6-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="14cf6-189">**Si se produce un error toodo este paso, se le cobrará por ambos almacenes de datos.**</span><span class="sxs-lookup"><span data-stu-id="14cf6-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="14cf6-190">Hello valores siguientes no se mantienen como parte de la migración de hello:</span><span class="sxs-lookup"><span data-stu-id="14cf6-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="14cf6-191">Auditoría de nivel de base de datos de hello debe toobe vuelve a habilitar.</span><span class="sxs-lookup"><span data-stu-id="14cf6-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="14cf6-192">Las reglas de Firewall en el nivel de base de datos de hello necesitan toobe agregarse de nuevo.</span><span class="sxs-lookup"><span data-stu-id="14cf6-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="14cf6-193">Las reglas de Firewall en el nivel de servidor hello no se ven afectadas.</span><span class="sxs-lookup"><span data-stu-id="14cf6-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="14cf6-194">Cambio del nombre del almacenamiento de datos durante la migración (opcional)</span><span class="sxs-lookup"><span data-stu-id="14cf6-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="14cf6-195">Dos bases de datos no puede tener el mismo servidor lógico de Hola Hola el mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="14cf6-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="14cf6-196">Almacenamiento de datos SQL admite ahora Hola capacidad toorename un almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="14cf6-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="14cf6-197">Para este ejemplo, imagine que su almacenamiento de datos del almacenamiento estándar actualmente se llama "MiAD".</span><span class="sxs-lookup"><span data-stu-id="14cf6-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="14cf6-198">Cambiar el nombre "MyDW" mediante Hola siguiente comando ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="14cf6-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="14cf6-199">(En este ejemplo, se podrá cambiarlo "MyDW_BeforeMigration.")  Este comando detiene todas las transacciones existentes y debe realizarse en hello toosucceed de base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="14cf6-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="14cf6-200">[Detenga][Pause] "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="14cf6-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="14cf6-201">Esto realiza una copia de seguridad automática.</span><span class="sxs-lookup"><span data-stu-id="14cf6-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="14cf6-202">[Restaurar] [ Restore] desde la instantánea más reciente de una base de datos con nombre de Hola usa toobe (por ejemplo, "MyDW").</span><span class="sxs-lookup"><span data-stu-id="14cf6-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="14cf6-203">Elimine "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="14cf6-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="14cf6-204">**Si se produce un error toodo este paso, se le cobrará por ambos almacenes de datos.**</span><span class="sxs-lookup"><span data-stu-id="14cf6-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="14cf6-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14cf6-205">Next steps</span></span>
<span data-ttu-id="14cf6-206">Almacenamiento toopremium los cambios de hello, también tendrá un mayor número de archivos de blob de base de datos en la arquitectura subyacente de Hola de su almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="14cf6-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="14cf6-207">ventajas de rendimiento de hello toomaximize de este cambio, vuelva a generar los índices de almacén de columnas agrupado mediante el uso de hello siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="14cf6-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="14cf6-208">script de Hola funciona forzar el uso de algunos de los blobs adicionales de toohello de datos existente.</span><span class="sxs-lookup"><span data-stu-id="14cf6-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="14cf6-209">Si no realiza ninguna acción, volverá a datos Hola naturalmente distribuir con el tiempo como cargar más datos en las tablas.</span><span class="sxs-lookup"><span data-stu-id="14cf6-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="14cf6-210">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="14cf6-210">**Prerequisites:**</span></span>

- <span data-ttu-id="14cf6-211">Hello almacenamiento de datos debe ejecutarse con unidades de almacenamiento de datos de 1000 o superior (vea [capacidad de cálculo de escala][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="14cf6-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="14cf6-212">usuario que ejecuta el script de Hola Hola debe ser una en hello [mediumrc rol] [ mediumrc role] o superior.</span><span class="sxs-lookup"><span data-stu-id="14cf6-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="14cf6-213">tooadd un rol de usuario toothis, ejecute el siguiente hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="14cf6-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="14cf6-214">Si tiene algún problema con el almacenamiento de datos, [crear una incidencia de soporte técnico] [ create a support ticket] y hacer referencia a "almacenamiento de migración toopremium" como posible causa de Hola.</span><span class="sxs-lookup"><span data-stu-id="14cf6-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
