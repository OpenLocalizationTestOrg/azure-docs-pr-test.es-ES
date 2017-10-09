---
title: Almacenamiento de datos de SQL Azure (portal de Azure) aaaRestore | Documentos de Microsoft
description: Tareas de Azure Portal para restaurar Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="6c910-103">Restauración de Azure SQL Data Warehouse (Portal)</span><span class="sxs-lookup"><span data-stu-id="6c910-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="6c910-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="6c910-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="6c910-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="6c910-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="6c910-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="6c910-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="6c910-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="6c910-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="6c910-108">En este artículo, aprenderá cómo toorestore almacenamiento de datos de SQL Azure mediante el uso de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c910-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6c910-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="6c910-109">Before you begin</span></span>
<span data-ttu-id="6c910-110">**Compruebe la capacidad DTU**.</span><span class="sxs-lookup"><span data-stu-id="6c910-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="6c910-111">Cada instancia de SQL Data Warehouse está hospedada en un servidor SQL Server (por ejemplo, myserver.database.windows.net) que tiene una cuota de unidad de rendimiento de datos (DTU) predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6c910-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="6c910-112">Para poder restaurar el almacén de datos SQL, compruebe que SQL server tiene restante suficiente cuota DTU para la base de datos de Hola que va a restaurar.</span><span class="sxs-lookup"><span data-stu-id="6c910-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="6c910-113">toolearn la cuota de DTU de toocalculate o toorequest más Dtu, consulte [solicitar un cambio de cuota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="6c910-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="6c910-114">Restauración de una base de datos activa o en pausa</span><span class="sxs-lookup"><span data-stu-id="6c910-114">Restore an active or paused database</span></span>
<span data-ttu-id="6c910-115">toorestore una base de datos:</span><span class="sxs-lookup"><span data-stu-id="6c910-115">toorestore a database:</span></span>

1. <span data-ttu-id="6c910-116">Inicie sesión en toohello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6c910-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6c910-117">En el panel izquierdo de hello, seleccione **examinar**y, a continuación, seleccione **servidores SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6c910-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Seleccione Examinar > Servidores SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="6c910-119">Busque el servidor y, a continuación, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="6c910-119">Find your server, and then select it.</span></span>

    ![Seleccione el servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="6c910-121">Buscar instancia Hola de almacenamiento de datos de SQL que desee toorestore de y, a continuación, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="6c910-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Seleccionar instancia de Hola de toorestore de almacenamiento de datos SQL](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="6c910-123">Hola parte superior de hoja de almacén de datos de hello, seleccione **restaurar**.</span><span class="sxs-lookup"><span data-stu-id="6c910-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Seleccione Restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="6c910-125">Especifique un nuevo **nombre de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="6c910-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="6c910-126">Seleccione hello más reciente **punto de restauración**.</span><span class="sxs-lookup"><span data-stu-id="6c910-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="6c910-127">Asegúrese de que elegir punto de restauración más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c910-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="6c910-128">Dado que los puntos de restauración se muestran en hora Universal coordinada (UTC), opción predeterminada de hello podría no ser punto de restauración más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c910-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Seleccione un punto de restauración](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="6c910-130">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c910-130">Select **OK**.</span></span>
9. <span data-ttu-id="6c910-131">se iniciará el proceso de restauración de base de datos de Hola y puede usar **notificaciones** toomonitor proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c910-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="6c910-132">Una vez finalizada la restauración de hello, puede configurar la base de datos recuperada siguiendo [configurar la base de datos después de la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="6c910-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="6c910-133">Restauración de una base de datos eliminada</span><span class="sxs-lookup"><span data-stu-id="6c910-133">Restore a deleted database</span></span>
<span data-ttu-id="6c910-134">toorestore una base de datos eliminada:</span><span class="sxs-lookup"><span data-stu-id="6c910-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="6c910-135">Inicie sesión en toohello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6c910-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6c910-136">En el panel izquierdo de hello, seleccione **examinar**y, a continuación, seleccione **servidores SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6c910-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Seleccione Examinar > Servidores SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="6c910-138">Busque el servidor y, a continuación, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="6c910-138">Find your server, and then select it.</span></span>

    ![Seleccione el servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="6c910-140">Desplácese hacia abajo toohello **Operations** sección en la hoja del servidor.</span><span class="sxs-lookup"><span data-stu-id="6c910-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="6c910-141">Seleccione hello **elimina las bases de datos** icono.</span><span class="sxs-lookup"><span data-stu-id="6c910-141">Select hello **Deleted databases** tile.</span></span>

    ![Icono de hello seleccione eliminado las bases de datos](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="6c910-143">Hola seleccione elimina base de datos que desea toorestore.</span><span class="sxs-lookup"><span data-stu-id="6c910-143">Select hello deleted database that you want toorestore.</span></span>

    ![Seleccione una base de datos toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="6c910-145">Especifique un nuevo **nombre de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="6c910-145">Specify a new **Database name**.</span></span>

    ![Agregar un nombre de base de datos de Hola](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="6c910-147">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c910-147">Select **OK**.</span></span>
9. <span data-ttu-id="6c910-148">se iniciará el proceso de restauración de base de datos de Hola y puede usar **notificaciones** toomonitor proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c910-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="6c910-149">consulta de la base de datos una vez finalizada la restauración de hello, tooconfigure [configurar la base de datos después de la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="6c910-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6c910-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c910-150">Next steps</span></span>
<span data-ttu-id="6c910-151">toolearn acerca de las características de continuidad de negocio Hola de ediciones de base de datos de SQL Azure, lea hello [información general sobre la continuidad de negocio de base de datos de SQL Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="6c910-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
