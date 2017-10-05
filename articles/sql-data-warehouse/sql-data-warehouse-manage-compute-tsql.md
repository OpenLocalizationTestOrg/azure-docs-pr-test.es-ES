---
title: "Pausa, reanudación y escalado con T-SQL en Azure SQL Data Warehouse | Microsoft Docs"
description: Tareas de Transact-SQL (T-SQL) para el escalado horizontal del rendimiento ajustando DWU. Ahorre costes reduciendo el escalado fuera de horas punta.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="c6d34-104">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="c6d34-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6d34-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c6d34-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="c6d34-106">Portal</span><span class="sxs-lookup"><span data-stu-id="c6d34-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="c6d34-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6d34-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="c6d34-108">REST</span><span class="sxs-lookup"><span data-stu-id="c6d34-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="c6d34-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="c6d34-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="c6d34-110">Ver la configuración de DWU actual</span><span class="sxs-lookup"><span data-stu-id="c6d34-110">View current DWU settings</span></span>
<span data-ttu-id="c6d34-111">Para ver la configuración actual de DWU para las bases de datos:</span><span class="sxs-lookup"><span data-stu-id="c6d34-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="c6d34-112">Abra el Explorador de objetos de SQL Server en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6d34-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="c6d34-113">Conéctese a la base de datos maestra asociada al servidor lógico de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c6d34-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="c6d34-114">Seleccione en la vista de administración dinámica sys.database_service_objectives.</span><span class="sxs-lookup"><span data-stu-id="c6d34-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="c6d34-115">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c6d34-115">Here is an example:</span></span> 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="c6d34-116">Escalado de proceso</span><span class="sxs-lookup"><span data-stu-id="c6d34-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="c6d34-117">Para cambiar las DWU:</span><span class="sxs-lookup"><span data-stu-id="c6d34-117">To change the DWUs:</span></span>

1. <span data-ttu-id="c6d34-118">Conéctese a la base de datos maestra asociada al servidor lógico de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c6d34-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="c6d34-119">Use la instrucción TSQL [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="c6d34-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="c6d34-120">En el ejemplo siguiente se establece el objetivo de nivel de servicio en DW1000 para la base de datos MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="c6d34-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="c6d34-121">Comprobación del estado de la base de datos y del progreso de la operación</span><span class="sxs-lookup"><span data-stu-id="c6d34-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="c6d34-122">Conéctese a la base de datos maestra asociada al servidor lógico de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c6d34-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="c6d34-123">Envío de una consulta para comprobar el estado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="c6d34-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="c6d34-124">Envío de una consulta para comprobar el estado de una operación</span><span class="sxs-lookup"><span data-stu-id="c6d34-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="c6d34-125">Esta DMV devolverá información sobre varias operaciones de administración en el almacenamiento de datos de SQL, como la operación y el estado de esta, que será IN_PROGRESS o COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="c6d34-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="c6d34-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6d34-126">Next steps</span></span>
<span data-ttu-id="c6d34-127">Para otras tareas de administración, consulte [Información general de administración][Management overview].</span><span class="sxs-lookup"><span data-stu-id="c6d34-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
