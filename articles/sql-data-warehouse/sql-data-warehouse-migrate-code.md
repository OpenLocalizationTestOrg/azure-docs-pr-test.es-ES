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
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>Migrar su tooSQL de código SQL almacenamiento de datos
En este artículo se explica los cambios de código probablemente necesitará toomake al migrar el código de otra base de datos tooSQL almacenamiento de datos. Algunas características de almacenamiento de datos SQL pueden mejorar significativamente el rendimiento tal como están toowork diseñada de manera distribuida. Sin embargo, toomaintain rendimiento y escala, algunas características también no están disponibles.

## <a name="common-t-sql-limitations"></a>Limitaciones comunes de T-SQL
Hola lista siguiente resume las características más comunes de Hola que no admiten el almacenamiento de datos de SQL. los vínculos de Hello permitirán tooworkarounds para características de hello no admitido:

* [ANSI JOINS en UPDATE][ANSI joins on updates]
* [ANSI JOINS en DELETE][ANSI joins on deletes]
* [Instrucción MERGE][merge statement]
* combinaciones entre bases de datos
* [Cursores][cursors]
* <seg>
  [INSERT..EXEC][INSERT..EXEC]</seg>
* cláusula OUTPUT
* funciones insertadas definidas por el usuario
* funciones de múltiples instrucciones
* [expresiones de tabla comunes](#Common-table-expressions)
* [expresiones de tabla común recursivas (CTE)](#Recursive-common-table-expressions-(CTE)
* procedimientos y funciones CLR
* función $partition
* variables de tabla
* parámetros de valor de tabla
* transacciones distribuidas
* trabajo con COMMIT/ROLLBACK
* SAVE TRANSACTION
* contextos de ejecución (EXECUTE AS)
* [cláusula GROUP BY con opciones ROLLUP/CUBE/GROUPING SETS][group by clause with rollup / cube / grouping sets options]
* [anidación de niveles más allá de 8][nesting levels beyond 8]
* [actualización a través de vistas][updating through views]
* [uso de SELECT para la asignación de variables][use of select for variable assignment]
* [No escriba ningún tipo de datos MAX en cadenas de SQL dinámico][no MAX data type for dynamic SQL strings]

Afortunadamente, la mayoría de estas limitaciones se puede solucionar. Explicaciones se proporcionan en los artículos de desarrollo relevantes de hello mencionadas anteriormente.

## <a name="supported-cte-features"></a>Características admitidas de las CTE
Las expresiones de tabla común (CTE) se admiten parcialmente en Almacenamiento de datos SQL.  Hola siguientes CTE características es compatibles actualmente:

* Se puede especificar una CTE en una instrucción SELECT.
* Se puede especificar una CTE en una instrucción CREATE VIEW.
* Se puede especificar una CTE en una instrucción CREATE TABLE AS SELECT (CTAS) .
* Se puede especificar una CTE en una instrucción CREATE REMOTE TABLE AS SELECT (CRTAS).
* Se puede especificar una CTE en una instrucción CREATE EXTERNAL TABLE AS SELECT (CETAS).
* Se puede hacer referencia a una tabla remota desde una CTE.
* Se puede hacer referencia a una tabla externa desde una CTE.
* Se pueden incluir varias definiciones de consulta CTE en una CTE.

## <a name="cte-limitations"></a>Limitaciones de las CTE
Estas son algunas de las limitaciones de las expresiones de tabla comunes en Almacenamiento de datos SQL:

* Una CTE debe ir seguida de una sola instrucción SELECT. No se admiten las instrucciones INSERT, UPDATE, DELETE y MERGE.
* No se admite la expresión de tabla común que incluya referencias tooitself (una expresión de tabla común de recursiva) (consulte la siguiente sección).
* No se permite especificar más de una cláusula WITH en una CTE. Por ejemplo, si una definición de consulta CTE contiene una subconsulta, esta no puede contener una cláusula WITH anidada que defina otra CTE.
* Una cláusula ORDER BY no se pueden usar en hello definiciones, excepto cuando se especifica una cláusula TOP.
* Cuando se usa una CTE en una instrucción que forma parte de un lote, instrucción de hello antes de que debe ir seguida de un punto y coma.
* Cuando se utiliza en instrucciones preparadas que sp_prepare, las CTE comportarán Hola igual que otras instrucciones SELECT en PDW. Sin embargo, si las CTE se utilizan como parte de CETAS preparadas que sp_prepare, comportamiento de hello puede diferir de SQL Server y otras instrucciones PDW debido a la manera de hello enlace se implementa para sp_prepare. Si seleccionar que las referencias CTE está utilizando una columna incorrecta que no existe en la CTE, Hola sp_prepare pasará sin detectar errores de hello, pero se producirá el error de Hola durante sp_execute en su lugar.

## <a name="recursive-ctes"></a>CTE recursivas
Las CTE recursivas no se admiten en Almacenamiento de datos SQL.  migración de Hola de CTE recursiva puede ser bastante compleja y proceso de mejor hello toobreak en varios pasos. Normalmente, puede usar un bucle y rellenar una tabla temporal tal y como se recorra en iteración las consultas de hello recursivas provisional. Una vez que se rellena la tabla temporal de hello, a continuación, puede devolver los datos de Hola como un único conjunto de resultados. Un enfoque similar ha sido usado toosolve `GROUP BY WITH CUBE` en hello [cláusula con el consolidado de group by / cubo / opciones de conjuntos de agrupamiento] [ group by clause with rollup / cube / grouping sets options] artículo.

## <a name="unsupported-system-functions"></a>Funciones de sistema no compatibles
También hay algunas funciones del sistema que no son compatibles. Algunas de hello principales que normalmente es posible utilizado en el almacenamiento de datos son:

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

Algunos de estos problemas se pueden solucionar.

## <a name="rowcount-workaround"></a>Solución alternativa para @@ROWCOUNT
toowork alrededor de falta de compatibilidad con @@ROWCOUNT, cree un procedimiento almacenado que recuperará Hola último recuento de filas de sys.dm_pdw_request_steps y, a continuación, ejecute `EXEC LastRowCount` después de una instrucción DML.

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

## <a name="next-steps"></a>Pasos siguientes
Para ver una lista completa de todas las instrucciones de T-SQL admitidas, vea [Temas de Transact-SQL][Transact-SQL topics].

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
