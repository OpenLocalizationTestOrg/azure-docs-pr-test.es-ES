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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (T-SQL)
> [!div class="op_single_selector"]
> * [Información general](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>Ver la configuración de DWU actual
tooview hello DWU configuración actual de las bases de datos:

1. Abra el Explorador de objetos de SQL Server en Visual Studio.
2. Conectar toohello base de datos maestra asociado con el servidor de base de datos SQL de hello lógico.
3. Seleccione en la vista de administración dinámica sys.database_service_objectives Hola. Aquí tiene un ejemplo: 

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

## <a name="scale-compute"></a>Escalado de proceso
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

Hola toochange a Dwu:

1. Conectar toohello base de datos maestra asociado con el servidor lógico de la base de datos SQL.
2. Hola de uso [ALTER DATABASE] [ ALTER DATABASE] instrucción TSQL. Hello en el ejemplo siguiente se establece tooDW1000 objetivo de hello servicio nivel de base de datos de hello MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Comprobación del estado de la base de datos y del progreso de la operación

1. Conectar toohello base de datos maestra asociado con el servidor lógico de la base de datos SQL.
2. Enviar estado de base de datos de consulta toocheck

```sql
SELECT *
FROM
sys.databases
```

3. Consulta toocheck estado de operación de envío

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Esta DMV devolverá información sobre varias operaciones de administración en el almacenamiento de datos de SQL como el estado de operación y Hola Hola de operación de hello, que será IN_PROGRESS o completado.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Pasos siguientes
Para otras tareas de administración, consulte [Información general de administración][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
