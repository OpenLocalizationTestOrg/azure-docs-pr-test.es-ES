---
title: "aaaPause, reanudar, escalar con T-SQL en el almacén de datos de SQL de Azure | Documentos de Microsoft"
description: Transact-SQL (T-SQL) tareas tooscale rendimiento mediante el ajuste a Dwu. Ahorre costes reduciendo el escalado fuera de horas punta.
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
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="55967-104">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="55967-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55967-105">Información general</span><span class="sxs-lookup"><span data-stu-id="55967-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="55967-106">Portal</span><span class="sxs-lookup"><span data-stu-id="55967-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="55967-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55967-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="55967-108">REST</span><span class="sxs-lookup"><span data-stu-id="55967-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="55967-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="55967-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="55967-110">Ver la configuración de DWU actual</span><span class="sxs-lookup"><span data-stu-id="55967-110">View current DWU settings</span></span>
<span data-ttu-id="55967-111">tooview hello DWU configuración actual de las bases de datos:</span><span class="sxs-lookup"><span data-stu-id="55967-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="55967-112">Abra el Explorador de objetos de SQL Server en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55967-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="55967-113">Conectar toohello base de datos maestra asociado con el servidor de base de datos SQL de hello lógico.</span><span class="sxs-lookup"><span data-stu-id="55967-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="55967-114">Seleccione en la vista de administración dinámica sys.database_service_objectives Hola.</span><span class="sxs-lookup"><span data-stu-id="55967-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="55967-115">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="55967-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="55967-116">Escalado de proceso</span><span class="sxs-lookup"><span data-stu-id="55967-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="55967-117">Hola toochange a Dwu:</span><span class="sxs-lookup"><span data-stu-id="55967-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="55967-118">Conectar toohello base de datos maestra asociado con el servidor lógico de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="55967-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="55967-119">Hola de uso [ALTER DATABASE] [ ALTER DATABASE] instrucción TSQL.</span><span class="sxs-lookup"><span data-stu-id="55967-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="55967-120">Hello en el ejemplo siguiente se establece tooDW1000 objetivo de hello servicio nivel de base de datos de hello MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="55967-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="55967-121">Comprobación del estado de la base de datos y del progreso de la operación</span><span class="sxs-lookup"><span data-stu-id="55967-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="55967-122">Conectar toohello base de datos maestra asociado con el servidor lógico de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="55967-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="55967-123">Enviar estado de base de datos de consulta toocheck</span><span class="sxs-lookup"><span data-stu-id="55967-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="55967-124">Consulta toocheck estado de operación de envío</span><span class="sxs-lookup"><span data-stu-id="55967-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="55967-125">Esta DMV devolverá información sobre varias operaciones de administración en el almacenamiento de datos de SQL como el estado de operación y Hola Hola de operación de hello, que será IN_PROGRESS o completado.</span><span class="sxs-lookup"><span data-stu-id="55967-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="55967-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55967-126">Next steps</span></span>
<span data-ttu-id="55967-127">Para otras tareas de administración, consulte [Información general de administración][Management overview].</span><span class="sxs-lookup"><span data-stu-id="55967-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
