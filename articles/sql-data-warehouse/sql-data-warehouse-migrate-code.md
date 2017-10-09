---
title: "aaaMigrate su tooSQL de código SQL datawarehouse | Documentos de Microsoft"
description: "Sugerencias para migrar su tooAzure de código SQL almacenamiento de datos SQL para desarrollar soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a><span data-ttu-id="b7371-103">Migrar su tooSQL de código SQL almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="b7371-103">Migrate your SQL code tooSQL Data Warehouse</span></span>
<span data-ttu-id="b7371-104">En este artículo se explica los cambios de código probablemente necesitará toomake al migrar el código de otra base de datos tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="b7371-104">This article explains code changes you will probably need toomake when migrating your code from another database tooSQL Data Warehouse.</span></span> <span data-ttu-id="b7371-105">Algunas características de almacenamiento de datos SQL pueden mejorar significativamente el rendimiento tal como están toowork diseñada de manera distribuida.</span><span class="sxs-lookup"><span data-stu-id="b7371-105">Some SQL Data Warehouse features can significantly improve performance as they are designed toowork in a distributed fashion.</span></span> <span data-ttu-id="b7371-106">Sin embargo, toomaintain rendimiento y escala, algunas características también no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="b7371-106">However, toomaintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="b7371-107">Limitaciones comunes de T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7371-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="b7371-108">Hola lista siguiente resume las características más comunes de Hola que no admiten el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="b7371-108">hello following list summarizes hello most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="b7371-109">los vínculos de Hello permitirán tooworkarounds para características de hello no admitido:</span><span class="sxs-lookup"><span data-stu-id="b7371-109">hello links take you tooworkarounds for hello unsupported features:</span></span>

* <span data-ttu-id="b7371-110">[ANSI JOINS en UPDATE][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="b7371-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="b7371-111">[ANSI JOINS en DELETE][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="b7371-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="b7371-112">[Instrucción MERGE][merge statement]</span><span class="sxs-lookup"><span data-stu-id="b7371-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="b7371-113">combinaciones entre bases de datos</span><span class="sxs-lookup"><span data-stu-id="b7371-113">cross-database joins</span></span>
* <span data-ttu-id="b7371-114">[Cursores][cursors]</span><span class="sxs-lookup"><span data-stu-id="b7371-114">[cursors][cursors]</span></span>
* <span data-ttu-id="b7371-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="b7371-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="b7371-116">cláusula OUTPUT</span><span class="sxs-lookup"><span data-stu-id="b7371-116">output clause</span></span>
* <span data-ttu-id="b7371-117">funciones insertadas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="b7371-117">inline user-defined functions</span></span>
* <span data-ttu-id="b7371-118">funciones de múltiples instrucciones</span><span class="sxs-lookup"><span data-stu-id="b7371-118">multi-statement functions</span></span>
* [<span data-ttu-id="b7371-119">expresiones de tabla comunes</span><span class="sxs-lookup"><span data-stu-id="b7371-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="b7371-120">[expresiones de tabla común recursivas (CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="b7371-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="b7371-121">procedimientos y funciones CLR</span><span class="sxs-lookup"><span data-stu-id="b7371-121">CLR functions and procedures</span></span>
* <span data-ttu-id="b7371-122">función $partition</span><span class="sxs-lookup"><span data-stu-id="b7371-122">$partition function</span></span>
* <span data-ttu-id="b7371-123">variables de tabla</span><span class="sxs-lookup"><span data-stu-id="b7371-123">table variables</span></span>
* <span data-ttu-id="b7371-124">parámetros de valor de tabla</span><span class="sxs-lookup"><span data-stu-id="b7371-124">table value parameters</span></span>
* <span data-ttu-id="b7371-125">transacciones distribuidas</span><span class="sxs-lookup"><span data-stu-id="b7371-125">distributed transactions</span></span>
* <span data-ttu-id="b7371-126">trabajo con COMMIT/ROLLBACK</span><span class="sxs-lookup"><span data-stu-id="b7371-126">commit / rollback work</span></span>
* <span data-ttu-id="b7371-127">SAVE TRANSACTION</span><span class="sxs-lookup"><span data-stu-id="b7371-127">save transaction</span></span>
* <span data-ttu-id="b7371-128">contextos de ejecución (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="b7371-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="b7371-129">[cláusula GROUP BY con opciones ROLLUP/CUBE/GROUPING SETS][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="b7371-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="b7371-130">[anidación de niveles más allá de 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="b7371-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="b7371-131">[actualización a través de vistas][updating through views]</span><span class="sxs-lookup"><span data-stu-id="b7371-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="b7371-132">[uso de SELECT para la asignación de variables][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="b7371-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="b7371-133">[No escriba ningún tipo de datos MAX en cadenas de SQL dinámico][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="b7371-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="b7371-134">Afortunadamente, la mayoría de estas limitaciones se puede solucionar.</span><span class="sxs-lookup"><span data-stu-id="b7371-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="b7371-135">Explicaciones se proporcionan en los artículos de desarrollo relevantes de hello mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b7371-135">Explanations are provided in hello relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="b7371-136">Características admitidas de las CTE</span><span class="sxs-lookup"><span data-stu-id="b7371-136">Supported CTE features</span></span>
<span data-ttu-id="b7371-137">Las expresiones de tabla común (CTE) se admiten parcialmente en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="b7371-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="b7371-138">Hola siguientes CTE características es compatibles actualmente:</span><span class="sxs-lookup"><span data-stu-id="b7371-138">hello following CTE features are currently supported:</span></span>

* <span data-ttu-id="b7371-139">Se puede especificar una CTE en una instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="b7371-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="b7371-140">Se puede especificar una CTE en una instrucción CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="b7371-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="b7371-141">Se puede especificar una CTE en una instrucción CREATE TABLE AS SELECT (CTAS) .</span><span class="sxs-lookup"><span data-stu-id="b7371-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="b7371-142">Se puede especificar una CTE en una instrucción CREATE REMOTE TABLE AS SELECT (CRTAS).</span><span class="sxs-lookup"><span data-stu-id="b7371-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="b7371-143">Se puede especificar una CTE en una instrucción CREATE EXTERNAL TABLE AS SELECT (CETAS).</span><span class="sxs-lookup"><span data-stu-id="b7371-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="b7371-144">Se puede hacer referencia a una tabla remota desde una CTE.</span><span class="sxs-lookup"><span data-stu-id="b7371-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="b7371-145">Se puede hacer referencia a una tabla externa desde una CTE.</span><span class="sxs-lookup"><span data-stu-id="b7371-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="b7371-146">Se pueden incluir varias definiciones de consulta CTE en una CTE.</span><span class="sxs-lookup"><span data-stu-id="b7371-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="b7371-147">Limitaciones de las CTE</span><span class="sxs-lookup"><span data-stu-id="b7371-147">CTE Limitations</span></span>
<span data-ttu-id="b7371-148">Estas son algunas de las limitaciones de las expresiones de tabla comunes en Almacenamiento de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="b7371-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="b7371-149">Una CTE debe ir seguida de una sola instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="b7371-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="b7371-150">No se admiten las instrucciones INSERT, UPDATE, DELETE y MERGE.</span><span class="sxs-lookup"><span data-stu-id="b7371-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="b7371-151">No se admite la expresión de tabla común que incluya referencias tooitself (una expresión de tabla común de recursiva) (consulte la siguiente sección).</span><span class="sxs-lookup"><span data-stu-id="b7371-151">A common table expression that includes references tooitself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="b7371-152">No se permite especificar más de una cláusula WITH en una CTE.</span><span class="sxs-lookup"><span data-stu-id="b7371-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="b7371-153">Por ejemplo, si una definición de consulta CTE contiene una subconsulta, esta no puede contener una cláusula WITH anidada que defina otra CTE.</span><span class="sxs-lookup"><span data-stu-id="b7371-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="b7371-154">Una cláusula ORDER BY no se pueden usar en hello definiciones, excepto cuando se especifica una cláusula TOP.</span><span class="sxs-lookup"><span data-stu-id="b7371-154">An ORDER BY clause cannot be used in hello CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="b7371-155">Cuando se usa una CTE en una instrucción que forma parte de un lote, instrucción de hello antes de que debe ir seguida de un punto y coma.</span><span class="sxs-lookup"><span data-stu-id="b7371-155">When a CTE is used in a statement that is part of a batch, hello statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="b7371-156">Cuando se utiliza en instrucciones preparadas que sp_prepare, las CTE comportarán Hola igual que otras instrucciones SELECT en PDW.</span><span class="sxs-lookup"><span data-stu-id="b7371-156">When used in statements prepared by sp_prepare, CTEs will behave hello same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="b7371-157">Sin embargo, si las CTE se utilizan como parte de CETAS preparadas que sp_prepare, comportamiento de hello puede diferir de SQL Server y otras instrucciones PDW debido a la manera de hello enlace se implementa para sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="b7371-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, hello behavior can defer from SQL Server and other PDW statements because of hello way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="b7371-158">Si seleccionar que las referencias CTE está utilizando una columna incorrecta que no existe en la CTE, Hola sp_prepare pasará sin detectar errores de hello, pero se producirá el error de Hola durante sp_execute en su lugar.</span><span class="sxs-lookup"><span data-stu-id="b7371-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, hello sp_prepare will pass without detecting hello error, but hello error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="b7371-159">CTE recursivas</span><span class="sxs-lookup"><span data-stu-id="b7371-159">Recursive CTEs</span></span>
<span data-ttu-id="b7371-160">Las CTE recursivas no se admiten en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="b7371-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="b7371-161">migración de Hola de CTE recursiva puede ser bastante compleja y proceso de mejor hello toobreak en varios pasos.</span><span class="sxs-lookup"><span data-stu-id="b7371-161">hello migration of recursive CTE can be somewhat complex and hello best process is toobreak it into multiple steps.</span></span> <span data-ttu-id="b7371-162">Normalmente, puede usar un bucle y rellenar una tabla temporal tal y como se recorra en iteración las consultas de hello recursivas provisional.</span><span class="sxs-lookup"><span data-stu-id="b7371-162">You can typically use a loop and populate a temporary table as you iterate over hello recursive interim queries.</span></span> <span data-ttu-id="b7371-163">Una vez que se rellena la tabla temporal de hello, a continuación, puede devolver los datos de Hola como un único conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="b7371-163">Once hello temporary table is populated you can then return hello data as a single result set.</span></span> <span data-ttu-id="b7371-164">Un enfoque similar ha sido usado toosolve `GROUP BY WITH CUBE` en hello [cláusula con el consolidado de group by / cubo / opciones de conjuntos de agrupamiento] [ group by clause with rollup / cube / grouping sets options] artículo.</span><span class="sxs-lookup"><span data-stu-id="b7371-164">A similar approach has been used toosolve `GROUP BY WITH CUBE` in hello [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="b7371-165">Funciones de sistema no compatibles</span><span class="sxs-lookup"><span data-stu-id="b7371-165">Unsupported system functions</span></span>
<span data-ttu-id="b7371-166">También hay algunas funciones del sistema que no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="b7371-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="b7371-167">Algunas de hello principales que normalmente es posible utilizado en el almacenamiento de datos son:</span><span class="sxs-lookup"><span data-stu-id="b7371-167">Some of hello main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="b7371-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="b7371-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="b7371-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="b7371-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="b7371-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="b7371-170">@@IDENTITY()</span></span>
* <span data-ttu-id="b7371-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="b7371-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="b7371-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="b7371-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="b7371-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="b7371-173">ERROR_LINE()</span></span>

<span data-ttu-id="b7371-174">Algunos de estos problemas se pueden solucionar.</span><span class="sxs-lookup"><span data-stu-id="b7371-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="b7371-175">Solución alternativa para @@ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="b7371-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="b7371-176">toowork alrededor de falta de compatibilidad con @@ROWCOUNT, cree un procedimiento almacenado que recuperará Hola último recuento de filas de sys.dm_pdw_request_steps y, a continuación, ejecute `EXEC LastRowCount` después de una instrucción DML.</span><span class="sxs-lookup"><span data-stu-id="b7371-176">toowork around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve hello last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="b7371-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7371-177">Next steps</span></span>
<span data-ttu-id="b7371-178">Para ver una lista completa de todas las instrucciones de T-SQL admitidas, vea [Temas de Transact-SQL][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="b7371-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
