---
title: "Restauración de Azure SQL Data Warehouse (Azure Portal) | Microsoft Docs"
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
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="a7b07-103">Restauración de Azure SQL Data Warehouse (Portal)</span><span class="sxs-lookup"><span data-stu-id="a7b07-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a7b07-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="a7b07-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a7b07-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="a7b07-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="a7b07-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a7b07-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="a7b07-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="a7b07-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="a7b07-108">En este artículo, obtendrá información sobre cómo restaurar Azure SQL Data Warehouse mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a7b07-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7b07-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="a7b07-109">Before you begin</span></span>
<span data-ttu-id="a7b07-110">**Compruebe la capacidad DTU**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="a7b07-111">Cada instancia de SQL Data Warehouse está hospedada en un servidor SQL Server (por ejemplo, myserver.database.windows.net) que tiene una cuota de unidad de rendimiento de datos (DTU) predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a7b07-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="a7b07-112">Antes de que pueda restaurar una instancia de SQL Data Warehouse, compruebe que su servidor SQL Server tiene suficientes cuotas de DTU restantes para la base de datos que va a restaurar.</span><span class="sxs-lookup"><span data-stu-id="a7b07-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="a7b07-113">Para obtener información sobre cómo calcular la cuota de DTU o para solicitar más DTU, vea cómo [solicitar un cambio de cuota de DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="a7b07-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="a7b07-114">Restauración de una base de datos activa o en pausa</span><span class="sxs-lookup"><span data-stu-id="a7b07-114">Restore an active or paused database</span></span>
<span data-ttu-id="a7b07-115">Para restaurar una base de datos:</span><span class="sxs-lookup"><span data-stu-id="a7b07-115">To restore a database:</span></span>

1. <span data-ttu-id="a7b07-116">Inicie sesión en [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a7b07-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a7b07-117">En el panel izquierdo, seleccione **Examinar** y, después, seleccione **Servidores SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Seleccione Examinar > Servidores SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="a7b07-119">Busque el servidor y, a continuación, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="a7b07-119">Find your server, and then select it.</span></span>

    ![Seleccione el servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="a7b07-121">Busque la instancia de SQL Data Warehouse desde la que desea realizar la restauración y selecciónela.</span><span class="sxs-lookup"><span data-stu-id="a7b07-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Seleccione la instancia de SQL Data Warehouse que desea restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="a7b07-123">En la parte superior de la hoja Data Warehouse, seleccione **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Seleccione Restaurar](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="a7b07-125">Especifique un nuevo **nombre de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="a7b07-126">Seleccione el último **punto de restauración**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="a7b07-127">No se olvide de elegir el punto de restauración más reciente.</span><span class="sxs-lookup"><span data-stu-id="a7b07-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="a7b07-128">Dado que los puntos de restauración se muestran con la hora universal coordinada (UTC), la opción predeterminada puede no ser el último punto de restauración.</span><span class="sxs-lookup"><span data-stu-id="a7b07-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Seleccione un punto de restauración](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="a7b07-130">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-130">Select **OK**.</span></span>
9. <span data-ttu-id="a7b07-131">El proceso de restauración de base de datos se iniciará, y puede usar **NOTIFICACIONES** para supervisar el proceso.</span><span class="sxs-lookup"><span data-stu-id="a7b07-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b07-132">Una vez finalizada la restauración, puede configurar la base de datos recuperada siguiendo la guía [Configuración de la base de datos después de realizar la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="a7b07-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="a7b07-133">Restauración de una base de datos eliminada</span><span class="sxs-lookup"><span data-stu-id="a7b07-133">Restore a deleted database</span></span>
<span data-ttu-id="a7b07-134">Para restaurar una base de datos eliminada, consulte:</span><span class="sxs-lookup"><span data-stu-id="a7b07-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="a7b07-135">Inicie sesión en [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a7b07-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a7b07-136">En el panel izquierdo, seleccione **Examinar** y, después, seleccione **Servidores SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Seleccione Examinar > Servidores SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="a7b07-138">Busque el servidor y, a continuación, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="a7b07-138">Find your server, and then select it.</span></span>

    ![Seleccione el servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="a7b07-140">Desplácese hacia abajo hasta la sección **Operaciones** de la hoja del servidor.</span><span class="sxs-lookup"><span data-stu-id="a7b07-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="a7b07-141">Seleccione el icono **Bases de datos eliminadas**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-141">Select the **Deleted databases** tile.</span></span>

    ![Seleccione el icono Bases de datos eliminadas](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="a7b07-143">Seleccione la base de datos eliminada que desea restaurar.</span><span class="sxs-lookup"><span data-stu-id="a7b07-143">Select the deleted database that you want to restore.</span></span>

    ![Selección de la base de datos que se va a restaurar](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="a7b07-145">Especifique un nuevo **nombre de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-145">Specify a new **Database name**.</span></span>

    ![Agregue un nombre para la base de datos](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="a7b07-147">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a7b07-147">Select **OK**.</span></span>
9. <span data-ttu-id="a7b07-148">El proceso de restauración de base de datos se iniciará, y puede usar **NOTIFICACIONES** para supervisar el proceso.</span><span class="sxs-lookup"><span data-stu-id="a7b07-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b07-149">Para configurar la base de datos después de que haya finalizado la restauración, vea [Configuración de la base de datos después de realizar la recuperación][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="a7b07-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a7b07-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a7b07-150">Next steps</span></span>
<span data-ttu-id="a7b07-151">Para obtener más información sobre las características de continuidad empresarial de las ediciones de Azure SQL Database, vea [Introducción a la continuidad empresarial con Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="a7b07-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
