---
title: "Guía de tipos de datos - Azure SQL Data Warehouse | Microsoft Docs"
description: Recomendaciones para definir tipos de datos compatibles con SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 5c24c71af16bd9851d9caf15fecfa4bb76f5f77e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="90758-103">Guía para definir los tipos de datos para las tablas en SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="90758-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="90758-104">Siga estas recomendaciones para definir los tipos de datos para tablas compatibles con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="90758-104">Use these recommendations to define table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="90758-105">Además de compatibilidad, minimizar el tamaño de los tipos de datos mejora el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="90758-105">In addition to compatibility, minimizing the size of data types improves query performance.</span></span>

<span data-ttu-id="90758-106">Almacenamiento de datos SQL admite los tipos de datos usados más frecuentemente.</span><span class="sxs-lookup"><span data-stu-id="90758-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="90758-107">Para obtener una lista de los tipos de datos admitidos, consulte [tipos de datos](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) en la instrucción CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="90758-107">For a list of the supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in the CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="90758-108">Minimizar la longitud de fila</span><span class="sxs-lookup"><span data-stu-id="90758-108">Minimize row length</span></span>
<span data-ttu-id="90758-109">Minimizar el tamaño de los tipos de datos acorta la longitud de fila, lo que conduce a un mejor rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="90758-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="90758-110">Utilice el tipo de datos más pequeño que sirva para los datos.</span><span class="sxs-lookup"><span data-stu-id="90758-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="90758-111">Evite definir las columnas de caracteres con una longitud predeterminada de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="90758-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="90758-112">Por ejemplo, si el valor más largo es de 25 caracteres, defina la columna como VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="90758-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="90758-113">Evite el uso de [NVARCHAR][NVARCHAR] cuando solo necesite VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="90758-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="90758-114">Utilice NVARCHAR(4000) o VARCHAR(8000) cuando sea posible en lugar de NVARCHAR(MAX) o VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="90758-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="90758-115">Si usa Polybase para cargar las tablas, la longitud definida para la fila de la tabla no puede superar 1 MB.</span><span class="sxs-lookup"><span data-stu-id="90758-115">If you are using Polybase to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="90758-116">Cuando una fila con datos de longitud variable supera 1 MB, puede cargar la fila con BCP, pero no con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="90758-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="90758-117">Identificar los tipos de datos no admitidos</span><span class="sxs-lookup"><span data-stu-id="90758-117">Identify unsupported data types</span></span>
<span data-ttu-id="90758-118">Si va a migrar la base de datos desde otra base de datos SQL, puede encontrar tipos de datos no admitidos en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="90758-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="90758-119">Utilice esta consulta para detectar tipos de datos no admitidos en el esquema de SQL existente.</span><span class="sxs-lookup"><span data-stu-id="90758-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="90758-120"><a name="unsupported-data-types"></a>Usar soluciones alternativas para los tipos de datos no admitidos</span><span class="sxs-lookup"><span data-stu-id="90758-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="90758-121">La lista siguiente muestra los tipos de datos que SQL Data Warehouse no admite y proporciona alternativas que puede usar en lugar de los tipos de datos no admitidos.</span><span class="sxs-lookup"><span data-stu-id="90758-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="90758-122">Tipo de datos no admitido</span><span class="sxs-lookup"><span data-stu-id="90758-122">Unsupported data type</span></span> | <span data-ttu-id="90758-123">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="90758-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="90758-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="90758-124">[geometry][geometry]</span></span> |<span data-ttu-id="90758-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="90758-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="90758-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="90758-126">[geography][geography]</span></span> |<span data-ttu-id="90758-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="90758-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="90758-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="90758-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="90758-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="90758-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="90758-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="90758-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="90758-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="90758-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="90758-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="90758-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="90758-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="90758-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="90758-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="90758-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="90758-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="90758-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="90758-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="90758-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="90758-137">Divida la columna en varias columnas fuertemente tipadas.</span><span class="sxs-lookup"><span data-stu-id="90758-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="90758-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="90758-138">[table][table]</span></span> |<span data-ttu-id="90758-139">Convierta en tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="90758-139">Convert to temporary tables.</span></span> |
| <span data-ttu-id="90758-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="90758-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="90758-141">Vuelva a procesar el código para que use [datetime2][datetime2] y la función `CURRENT_TIMESTAMP`.</span><span class="sxs-lookup"><span data-stu-id="90758-141">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="90758-142">Solo se admiten las constantes como valores predeterminados, por lo tanto, current_timestamp no se puede definir como una restricción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="90758-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="90758-143">Si tiene que migrar valores de la versión de fila de una columna de tipo timestamp, use [BINARY][BINARY](8) o [VARBINARY][BINARY](8) para valores de versión de fila NOT NULL o NULL.</span><span class="sxs-lookup"><span data-stu-id="90758-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="90758-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="90758-144">[xml][xml]</span></span> |<span data-ttu-id="90758-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="90758-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="90758-146">[tipo definido por el usuario][user defined types]</span><span class="sxs-lookup"><span data-stu-id="90758-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="90758-147">Volver a convertir el tipo de datos nativo cuando sea posible.</span><span class="sxs-lookup"><span data-stu-id="90758-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="90758-148">valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="90758-148">default values</span></span> | <span data-ttu-id="90758-149">Los valores predeterminados solo admiten literales y constantes.</span><span class="sxs-lookup"><span data-stu-id="90758-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="90758-150">No se admiten funciones ni expresiones no deterministas, tales como `GETDATE()` o `CURRENT_TIMESTAMP`.</span><span class="sxs-lookup"><span data-stu-id="90758-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="90758-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90758-151">Next steps</span></span>
<span data-ttu-id="90758-152">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="90758-152">To learn more, see:</span></span>

- <span data-ttu-id="90758-153">[Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="90758-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="90758-154">[Información general sobre las tablas][Overview]</span><span class="sxs-lookup"><span data-stu-id="90758-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="90758-155">[Distribución de una tabla][Distribute]</span><span class="sxs-lookup"><span data-stu-id="90758-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="90758-156">[Indexación de una tabla][Index]</span><span class="sxs-lookup"><span data-stu-id="90758-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="90758-157">[Creación de particiones de una tabla][Partition]</span><span class="sxs-lookup"><span data-stu-id="90758-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="90758-158">[Mantenimiento de las estadísticas de tabla][Statistics]</span><span class="sxs-lookup"><span data-stu-id="90758-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="90758-159">[Tablas temporales][Temporary]</span><span class="sxs-lookup"><span data-stu-id="90758-159">[Temporary Tables][Temporary]</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
