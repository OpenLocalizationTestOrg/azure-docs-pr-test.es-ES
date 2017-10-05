---
title: "Azure Portal: replicación geográfica de SQL Database | Microsoft Docs"
description: "Configuración de replicación geográfica para Azure SQL Database en Azure Portal e inicio de la conmutación por error"
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
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="5874c-103">Configuración de replicación geográfica activa para Azure SQL Database en Azure Portal e inicio de la conmutación por error</span><span class="sxs-lookup"><span data-stu-id="5874c-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="5874c-104">En este artículo se muestra cómo configurar la replicación geográfica activa para SQL Database en [Azure Portal](http://portal.azure.com) y cómo iniciar la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="5874c-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="5874c-105">Para iniciar una conmutación por error planeada con el Portal de Azure, consulte [Inicio de una conmutación por error planeada o no planeada para Base de datos SQL de Azure con el Portal de Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5874c-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="5874c-106">Para configurar la replicación geográfica activa mediante Azure Portal, necesita el siguiente recurso:</span><span class="sxs-lookup"><span data-stu-id="5874c-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="5874c-107">Una instancia de Azure SQL Database: la base de datos principal que quiere replicar en una región geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="5874c-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="5874c-108">La replicación geográfica activa debe producirse entre bases de datos de la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="5874c-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="5874c-109">Agregar una base de datos secundaria</span><span class="sxs-lookup"><span data-stu-id="5874c-109">Add a secondary database</span></span>
<span data-ttu-id="5874c-110">Los pasos siguientes crean otra base de datos secundaria en una asociación de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="5874c-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="5874c-111">Para agregar una base de datos secundaria, debe ser el propietario o copropietario de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="5874c-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="5874c-112">La base de datos secundaria tiene el mismo nombre que la base de datos principal y, de forma predeterminada, presentan el mismo nivel de servicio.</span><span class="sxs-lookup"><span data-stu-id="5874c-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="5874c-113">La base de datos secundaria puede ser una base de datos única o una de un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="5874c-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="5874c-114">Para obtener más información, consulte el artículo sobre [niveles de servicio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="5874c-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="5874c-115">Después de crear e inicializar la base de datos secundaria, los datos comienzan a replicarse desde la base de datos principal a la nueva base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="5874c-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="5874c-116">Si la base de datos del asociado ya existe (por ejemplo, como resultado de la terminación de una relación de replicación geográfica anterior), se produce un error en el comando.</span><span class="sxs-lookup"><span data-stu-id="5874c-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="5874c-117">En [Azure Portal](http://portal.azure.com), vaya a la base de datos que desea configurar para replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="5874c-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="5874c-118">En la página de SQL Database, seleccione **Replicación geográfica** y, luego, seleccione la región para crear la base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="5874c-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="5874c-119">Puede seleccionar cualquier región menos la que hospeda la base de datos principal, pero se recomienda la [región emparejada](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="5874c-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configuración de la replicación geográfica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="5874c-121">Seleccione o configure el servidor y el plan de tarifa de la base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="5874c-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Configuración de la secundaria](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="5874c-123">También puede agregar una base de datos secundaria a un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="5874c-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="5874c-124">Para crear una base de datos secundaria en un grupo, haga clic en **Grupo elástico** y seleccione un grupo del servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="5874c-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="5874c-125">Ya debe existir un grupo en el servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="5874c-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="5874c-126">Este flujo de trabajo no crea un grupo.</span><span class="sxs-lookup"><span data-stu-id="5874c-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="5874c-127">Haga clic en **Crear** para agregar la base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="5874c-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="5874c-128">Se crea la base de datos secundaria y comienza el proceso de inicialización.</span><span class="sxs-lookup"><span data-stu-id="5874c-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![Configuración de la secundaria](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="5874c-130">Cuando se completa el proceso de propagación, la base de datos secundaria muestra su estado.</span><span class="sxs-lookup"><span data-stu-id="5874c-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Propagación completa](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="5874c-132">Inicio de una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="5874c-132">Initiate a failover</span></span>

<span data-ttu-id="5874c-133">La base de datos secundaria se puede cambiar para convertirse en la principal.</span><span class="sxs-lookup"><span data-stu-id="5874c-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="5874c-134">En [Azure Portal](http://portal.azure.com), vaya a la base de datos principal de la asociación de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="5874c-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="5874c-135">En la hoja SQL Database, seleccione **All settings** (Toda la configuración)  > **Replicación geográfica**.</span><span class="sxs-lookup"><span data-stu-id="5874c-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="5874c-136">En la lista **SECUNDARIAS**, seleccione la base de datos que quiere convertir en la nueva base de datos principal y haga clic en **Conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="5874c-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![Conmutación por error](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="5874c-138">Haga clic en **Sí** para iniciar la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="5874c-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="5874c-139">El comando cambiará inmediatamente la base de datos secundaria al rol principal.</span><span class="sxs-lookup"><span data-stu-id="5874c-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="5874c-140">Hay un breve período durante el que ambas bases de datos no están disponibles (del orden de 0 a 25 segundos) mientras se cambian los roles.</span><span class="sxs-lookup"><span data-stu-id="5874c-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="5874c-141">Si la base de datos principal tiene varias bases de datos secundarias, el comando reconfigura automáticamente las demás secundarias para conectarse a la nueva principal.</span><span class="sxs-lookup"><span data-stu-id="5874c-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="5874c-142">En circunstancias normales, toda la operación debería tardar menos de un minuto en completarse.</span><span class="sxs-lookup"><span data-stu-id="5874c-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="5874c-143">Este comando está diseñado para una rápida recuperación de la base de datos en el caso de una interrupción.</span><span class="sxs-lookup"><span data-stu-id="5874c-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="5874c-144">Desencadena una conmutación por error sin sincronización de datos (conmutación por error forzada).</span><span class="sxs-lookup"><span data-stu-id="5874c-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="5874c-145">Si la principal está conectada y confirmando transacciones cuando se emite el comando, es posible que produzca alguna pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="5874c-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="5874c-146">Elimine una base de datos secundaria</span><span class="sxs-lookup"><span data-stu-id="5874c-146">Remove secondary database</span></span>
<span data-ttu-id="5874c-147">Esta operación termina de forma permanente la replicación en la base de datos secundaria y el rol de la base de datos secundaria cambia al de una base de datos de lectura y escritura normal.</span><span class="sxs-lookup"><span data-stu-id="5874c-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="5874c-148">Si se interrumpe la conectividad con la base de datos secundaria, el comando se ejecuta correctamente, pero la base de datos secundaria no pasa a ser de lectura y escritura hasta después de restaurarse la conectividad.</span><span class="sxs-lookup"><span data-stu-id="5874c-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="5874c-149">En [Azure Portal](http://portal.azure.com), vaya a la base de datos principal de la asociación de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="5874c-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="5874c-150">En la página de SQL Database, seleccione **Replicación geográfica**.</span><span class="sxs-lookup"><span data-stu-id="5874c-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="5874c-151">En la lista **SECUNDARIAS**, seleccione la base de datos que desee quitar de la asociación de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="5874c-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="5874c-152">Haga clic en **Detener replicación**.</span><span class="sxs-lookup"><span data-stu-id="5874c-152">Click **Stop Replication**.</span></span>
   
    ![Quitar secundaria](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="5874c-154">Se abrirá una ventana de confirmación.</span><span class="sxs-lookup"><span data-stu-id="5874c-154">A confirmation window opens.</span></span> <span data-ttu-id="5874c-155">Haga clic en **Sí** para quitar la base de datos de la asociación de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="5874c-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="5874c-156">(Establezca el valor en una base de datos de lectura y escritura que no forme parte de ninguna replicación).</span><span class="sxs-lookup"><span data-stu-id="5874c-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5874c-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5874c-157">Next steps</span></span>
* <span data-ttu-id="5874c-158">Para obtener más información sobre la replicación geográfica activa, consulte [Replicación geográfica activa](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5874c-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="5874c-159">Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="5874c-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

