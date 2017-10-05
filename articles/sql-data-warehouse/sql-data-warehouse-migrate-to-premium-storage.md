---
title: "Migración de un almacenamiento de datos de Azure existente a Premium Storage | Microsoft Docs"
description: Instrucciones para migrar un almacenamiento de datos existente a Premium Storage
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
ms.openlocfilehash: 860e50b532b4b0a21d3be54f087730070b0e56bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a><span data-ttu-id="041ac-103">Migración del almacenamiento de datos a Premium Storage</span><span class="sxs-lookup"><span data-stu-id="041ac-103">Migrate your data warehouse to premium storage</span></span>
<span data-ttu-id="041ac-104">Azure SQL Data Warehouse ha introducido recientemente [Premium Storage para poder predecir el rendimiento de manera más eficaz][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="041ac-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="041ac-105">El almacenamiento de datos existente en el almacenamiento estándar se puede migrar a Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="041ac-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span></span> <span data-ttu-id="041ac-106">Puede aprovechar las ventajas de la migración automática, o si desea controlar cuándo realizar la migración (que implica cierto tiempo de inactividad), puede realizar la migración manualmente.</span><span class="sxs-lookup"><span data-stu-id="041ac-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span></span>

<span data-ttu-id="041ac-107">Si tiene más de un almacenamiento de datos, use el [programa de migración automática][automatic migration schedule] siguiente para determinar cuándo se migrará.</span><span class="sxs-lookup"><span data-stu-id="041ac-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="041ac-108">Determinación del tipo de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="041ac-108">Determine storage type</span></span>
<span data-ttu-id="041ac-109">Si creó un almacenamiento de datos antes de las fechas siguientes, significa que actualmente utiliza el almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="041ac-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="041ac-110">**Región**</span><span class="sxs-lookup"><span data-stu-id="041ac-110">**Region**</span></span> | <span data-ttu-id="041ac-111">**Almacenamiento de datos creado antes de esta fecha**</span><span class="sxs-lookup"><span data-stu-id="041ac-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="041ac-112">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="041ac-112">Australia East</span></span> |<span data-ttu-id="041ac-113">Premium Storage no está disponible todavía</span><span class="sxs-lookup"><span data-stu-id="041ac-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="041ac-114">Este de China</span><span class="sxs-lookup"><span data-stu-id="041ac-114">China East</span></span> |<span data-ttu-id="041ac-115">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="041ac-115">November 1, 2016</span></span> |
| <span data-ttu-id="041ac-116">Norte de China</span><span class="sxs-lookup"><span data-stu-id="041ac-116">China North</span></span> |<span data-ttu-id="041ac-117">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="041ac-117">November 1, 2016</span></span> |
| <span data-ttu-id="041ac-118">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="041ac-118">Germany Central</span></span> |<span data-ttu-id="041ac-119">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="041ac-119">November 1, 2016</span></span> |
| <span data-ttu-id="041ac-120">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="041ac-120">Germany Northeast</span></span> |<span data-ttu-id="041ac-121">1 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="041ac-121">November 1, 2016</span></span> |
| <span data-ttu-id="041ac-122">India occidental</span><span class="sxs-lookup"><span data-stu-id="041ac-122">India West</span></span> |<span data-ttu-id="041ac-123">Premium Storage no está disponible todavía</span><span class="sxs-lookup"><span data-stu-id="041ac-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="041ac-124">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="041ac-124">Japan West</span></span> |<span data-ttu-id="041ac-125">Premium Storage no está disponible todavía</span><span class="sxs-lookup"><span data-stu-id="041ac-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="041ac-126">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="041ac-126">North Central US</span></span> |<span data-ttu-id="041ac-127">10 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="041ac-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="041ac-128">Información de la migración automática</span><span class="sxs-lookup"><span data-stu-id="041ac-128">Automatic migration details</span></span>
<span data-ttu-id="041ac-129">De forma predeterminada, la base de datos se migrará automáticamente durante las 18:00 y las 6:00 en la hora local de su región durante la [programación de migración automática][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="041ac-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="041ac-130">No podrá usar el almacenamiento de datos existente durante la migración.</span><span class="sxs-lookup"><span data-stu-id="041ac-130">Your existing data warehouse will be unusable during the migration.</span></span> <span data-ttu-id="041ac-131">El proceso de migración durará aproximadamente una hora por cada terabyte de almacenamiento de cada almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="041ac-132">No se le cobrará nada en ningún momento de la migración automática.</span><span class="sxs-lookup"><span data-stu-id="041ac-132">You will not be charged during any portion of the automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="041ac-133">Cuando finalice la migración, el almacenamiento de datos volverá a estar en línea y utilizable.</span><span class="sxs-lookup"><span data-stu-id="041ac-133">When the migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="041ac-134">Microsoft está llevando a cabo los pasos siguientes para completar la migración (no se requiere ninguna intervención por parte del usuario).</span><span class="sxs-lookup"><span data-stu-id="041ac-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="041ac-135">Para este ejemplo, imagine que su almacenamiento de datos del almacenamiento estándar actualmente se llama "MiAD".</span><span class="sxs-lookup"><span data-stu-id="041ac-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="041ac-136">Microsoft cambia el nombre de "MiAD" por "MiAD_DO_NOT_USE_[Marca de tiempo]".</span><span class="sxs-lookup"><span data-stu-id="041ac-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="041ac-137">Microsoft pausa "MiAD_DO_NOT_USE_[Marca de tiempo]".</span><span class="sxs-lookup"><span data-stu-id="041ac-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="041ac-138">Durante este tiempo, se crea una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="041ac-138">During this time, a backup is taken.</span></span> <span data-ttu-id="041ac-139">Es posible que observe que se llevan a cabo varias tareas de pausa y reanudación si se producen problemas durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="041ac-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="041ac-140">Microsoft crea un nuevo almacenamiento de datos llamado "MiAD" en Premium Storage a partir de la copia de seguridad creada en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="041ac-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span></span> <span data-ttu-id="041ac-141">miAD no aparecerá hasta que acabe el proceso de restauración.</span><span class="sxs-lookup"><span data-stu-id="041ac-141">“MyDW” will not appear until after the restore is complete.</span></span>
4. <span data-ttu-id="041ac-142">Una vez que finalice, "MiAD" vuelve a las mismas unidades de almacenamiento de datos y al estado (en pausa o activo) que había antes de la migración.</span><span class="sxs-lookup"><span data-stu-id="041ac-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span></span>
5. <span data-ttu-id="041ac-143">Una vez que finaliza la migración, Microsoft elimina "MiAD_DO_NOT_USE_[Marca de tiempo]".</span><span class="sxs-lookup"><span data-stu-id="041ac-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="041ac-144">La configuración siguiente no se transmite como parte de la migración:</span><span class="sxs-lookup"><span data-stu-id="041ac-144">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="041ac-145">Se debe volver a habilitar la auditoría en el nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-145">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="041ac-146">Se deben volver a agregar las reglas de firewall del nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-146">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="041ac-147">Las reglas de firewall del nivel de servidor no se verán afectadas.</span><span class="sxs-lookup"><span data-stu-id="041ac-147">Firewall rules at the server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="041ac-148">programa de migración automática</span><span class="sxs-lookup"><span data-stu-id="041ac-148">Automatic migration schedule</span></span>
<span data-ttu-id="041ac-149">Las migraciones automáticas se llevan a cabo desde las 18:00 a las 6:00 (hora local por región) durante el programa de interrupción siguiente.</span><span class="sxs-lookup"><span data-stu-id="041ac-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span></span>

| <span data-ttu-id="041ac-150">**Región**</span><span class="sxs-lookup"><span data-stu-id="041ac-150">**Region**</span></span> | <span data-ttu-id="041ac-151">**Fecha de inicio estimada**</span><span class="sxs-lookup"><span data-stu-id="041ac-151">**Estimated start date**</span></span> | <span data-ttu-id="041ac-152">**Fecha de finalización estimada**</span><span class="sxs-lookup"><span data-stu-id="041ac-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="041ac-153">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="041ac-153">Australia East</span></span> |<span data-ttu-id="041ac-154">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="041ac-154">Not determined yet</span></span> |<span data-ttu-id="041ac-155">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="041ac-155">Not determined yet</span></span> |
| <span data-ttu-id="041ac-156">Este de China</span><span class="sxs-lookup"><span data-stu-id="041ac-156">China East</span></span> |<span data-ttu-id="041ac-157">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-157">January 9, 2017</span></span> |<span data-ttu-id="041ac-158">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-158">January 13, 2017</span></span> |
| <span data-ttu-id="041ac-159">Norte de China</span><span class="sxs-lookup"><span data-stu-id="041ac-159">China North</span></span> |<span data-ttu-id="041ac-160">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-160">January 9, 2017</span></span> |<span data-ttu-id="041ac-161">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-161">January 13, 2017</span></span> |
| <span data-ttu-id="041ac-162">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="041ac-162">Germany Central</span></span> |<span data-ttu-id="041ac-163">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-163">January 9, 2017</span></span> |<span data-ttu-id="041ac-164">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-164">January 13, 2017</span></span> |
| <span data-ttu-id="041ac-165">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="041ac-165">Germany Northeast</span></span> |<span data-ttu-id="041ac-166">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-166">January 9, 2017</span></span> |<span data-ttu-id="041ac-167">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-167">January 13, 2017</span></span> |
| <span data-ttu-id="041ac-168">India occidental</span><span class="sxs-lookup"><span data-stu-id="041ac-168">India West</span></span> |<span data-ttu-id="041ac-169">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="041ac-169">Not determined yet</span></span> |<span data-ttu-id="041ac-170">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="041ac-170">Not determined yet</span></span> |
| <span data-ttu-id="041ac-171">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="041ac-171">Japan West</span></span> |<span data-ttu-id="041ac-172">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="041ac-172">Not determined yet</span></span> |<span data-ttu-id="041ac-173">Sin determinar</span><span class="sxs-lookup"><span data-stu-id="041ac-173">Not determined yet</span></span> |
| <span data-ttu-id="041ac-174">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="041ac-174">North Central US</span></span> |<span data-ttu-id="041ac-175">9 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-175">January 9, 2017</span></span> |<span data-ttu-id="041ac-176">13 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="041ac-176">January 13, 2017</span></span> |

## <a name="self-migration-to-premium-storage"></a><span data-ttu-id="041ac-177">Migración manual a Premium Storage</span><span class="sxs-lookup"><span data-stu-id="041ac-177">Self-migration to premium storage</span></span>
<span data-ttu-id="041ac-178">Si desea controlar cuándo se producen los tiempos de inactividad, puede realizar los pasos siguientes para migrar un almacenamiento de datos existente del almacenamiento estándar a Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="041ac-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span></span> <span data-ttu-id="041ac-179">Si elige esta opción, debe completar la migración manual antes de que comience la migración automática en dicha región.</span><span class="sxs-lookup"><span data-stu-id="041ac-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span></span> <span data-ttu-id="041ac-180">Esto garantiza que se evite que cualquier riesgo de la migración automática cause algún conflicto (vea la [programación de la migración automática][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="041ac-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="041ac-181">Instrucciones de migración manual</span><span class="sxs-lookup"><span data-stu-id="041ac-181">Self-migration instructions</span></span>
<span data-ttu-id="041ac-182">Para migrar el almacenamiento de datos manualmente, utilice las características de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="041ac-182">To migrate your data warehouse yourself, use the backup and restore features.</span></span> <span data-ttu-id="041ac-183">Se espera que el componente de restauración de la migración dure una hora aproximadamente por cada terabyte de almacenamiento en cada almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="041ac-184">Si desea conservar el mismo nombre cuando se complete la migración, siga estos [pasos para cambiar el nombre durante la migración][steps to rename during migration].</span><span class="sxs-lookup"><span data-stu-id="041ac-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span></span>

1. <span data-ttu-id="041ac-185">[Detenga][Pause] el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="041ac-186">Esto realiza una copia de seguridad automática.</span><span class="sxs-lookup"><span data-stu-id="041ac-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="041ac-187">Lleve a cabo la [restauración][Restore] a partir de la instantánea más reciente.</span><span class="sxs-lookup"><span data-stu-id="041ac-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="041ac-188">Elimine el almacenamiento de datos existente del almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="041ac-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="041ac-189">**Si no puede realizar este paso, se le cobrará por los dos almacenamientos de datos.**</span><span class="sxs-lookup"><span data-stu-id="041ac-189">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="041ac-190">La configuración siguiente no se transmite como parte de la migración:</span><span class="sxs-lookup"><span data-stu-id="041ac-190">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="041ac-191">Se debe volver a habilitar la auditoría en el nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-191">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="041ac-192">Se deben volver a agregar las reglas de firewall del nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-192">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="041ac-193">Las reglas de firewall del nivel de servidor no se verán afectadas.</span><span class="sxs-lookup"><span data-stu-id="041ac-193">Firewall rules at the server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="041ac-194">Cambio del nombre del almacenamiento de datos durante la migración (opcional)</span><span class="sxs-lookup"><span data-stu-id="041ac-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="041ac-195">Dos bases de datos que se encuentren en el mismo servidor lógico no pueden tener el mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="041ac-195">Two databases on the same logical server cannot have the same name.</span></span> <span data-ttu-id="041ac-196">SQL Data Warehouse ahora permite cambiar el nombre de un almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span></span>

<span data-ttu-id="041ac-197">Para este ejemplo, imagine que su almacenamiento de datos del almacenamiento estándar actualmente se llama "MiAD".</span><span class="sxs-lookup"><span data-stu-id="041ac-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="041ac-198">Cambie el nombre "MiAD" con el comando ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="041ac-198">Rename "MyDW" by using the following ALTER DATABASE command.</span></span> <span data-ttu-id="041ac-199">(En este ejemplo, se cambia por "MyDW_BeforeMigration").  Este comando detiene todas las transacciones existentes y debe realizarse dentro de la base de datos maestra para que se lleve a cabo correctamente.</span><span class="sxs-lookup"><span data-stu-id="041ac-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="041ac-200">[Detenga][Pause] "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="041ac-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="041ac-201">Esto realiza una copia de seguridad automática.</span><span class="sxs-lookup"><span data-stu-id="041ac-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="041ac-202">Realice una [restauración][Restore] a partir de la instantánea más reciente de una nueva base de datos con el nombre que solía tener (por ejemplo: "MiAD").</span><span class="sxs-lookup"><span data-stu-id="041ac-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span></span>
4. <span data-ttu-id="041ac-203">Elimine "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="041ac-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="041ac-204">**Si no puede realizar este paso, se le cobrará por los dos almacenamientos de datos.**</span><span class="sxs-lookup"><span data-stu-id="041ac-204">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="041ac-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="041ac-205">Next steps</span></span>
<span data-ttu-id="041ac-206">Con la migración a Premium Storage, también se aumenta la cantidad de archivos de blob de base de datos en la arquitectura subyacente del almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="041ac-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span></span> <span data-ttu-id="041ac-207">Para maximizar las ventajas en el rendimiento que implica este cambio, recompile los índices de almacén de columnas en clúster con el script siguiente.</span><span class="sxs-lookup"><span data-stu-id="041ac-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span></span> <span data-ttu-id="041ac-208">El script funciona forzando algunos de los datos existentes a los blobs adicionales.</span><span class="sxs-lookup"><span data-stu-id="041ac-208">The script works by forcing some of your existing data to the additional blobs.</span></span> <span data-ttu-id="041ac-209">Si no realiza ninguna acción, los datos se redistribuirán naturalmente con el tiempo a medida que carga más datos en las tablas.</span><span class="sxs-lookup"><span data-stu-id="041ac-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="041ac-210">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="041ac-210">**Prerequisites:**</span></span>

- <span data-ttu-id="041ac-211">El almacenamiento de datos se debe ejecutar con 1000 unidades de almacenamiento de datos o más (vea el [escalado de la potencia de proceso][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="041ac-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="041ac-212">El usuario que ejecuta el script debe tener el [rol mediumrc][mediumrc role] o superior.</span><span class="sxs-lookup"><span data-stu-id="041ac-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="041ac-213">Para agregar un usuario a este rol, ejecute lo siguiente: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="041ac-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
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
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
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

<span data-ttu-id="041ac-214">Si tiene problemas con el almacenamiento de datos, [cree una incidencia de soporte técnico][create a support ticket] e indique que la posible causa es la "migración a Premium Storage".</span><span class="sxs-lookup"><span data-stu-id="041ac-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
