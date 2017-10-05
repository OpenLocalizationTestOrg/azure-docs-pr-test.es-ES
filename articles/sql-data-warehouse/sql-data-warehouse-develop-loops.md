---
title: Aprovechamiento de bucles T-SQL en Azure SQL Data Warehouse | Microsoft Docs
description: Sugerencias para los bucles de Transact-SQL en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 40a872ff310f48bfd543ac184fe7301b85b50258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="b1243-103">Bucles en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="b1243-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="b1243-104">SQL Data Warehouse admite el bucle [WHILE][WHILE] para ejecutar bloques de instrucciones de forma repetida.</span><span class="sxs-lookup"><span data-stu-id="b1243-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="b1243-105">Esta acción continuará siempre y cuando las condiciones especificadas se cumplan o hasta que el código termine específicamente el bucle con la palabra clave `BREAK` .</span><span class="sxs-lookup"><span data-stu-id="b1243-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span></span> <span data-ttu-id="b1243-106">Los bucles son especialmente útiles para reemplazar los cursores definidos en código SQL.</span><span class="sxs-lookup"><span data-stu-id="b1243-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="b1243-107">Afortunadamente, casi todos los cursores que están escritos en código SQL son de la variedad avance rápido y solo lectura.</span><span class="sxs-lookup"><span data-stu-id="b1243-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span></span> <span data-ttu-id="b1243-108">Por lo tanto, los bucles [WHILE] son una buena alternativa si se encuentra con que tiene que reemplazar uno.</span><span class="sxs-lookup"><span data-stu-id="b1243-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="b1243-109">Aprovechamiento de bucles y sustitución de cursores en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="b1243-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="b1243-110">Sin embargo, antes de profundizar en el tema, debe hacerse la siguiente pregunta: "¿Se pudo escribir de nuevo este cursor para usar operaciones basadas en conjunto?".</span><span class="sxs-lookup"><span data-stu-id="b1243-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span></span> <span data-ttu-id="b1243-111">En muchos casos, la respuesta será afirmativa y este suele ser el mejor enfoque.</span><span class="sxs-lookup"><span data-stu-id="b1243-111">In many cases the answer will be yes and is often the best approach.</span></span> <span data-ttu-id="b1243-112">Una operación basada en conjunto a menudo se realiza bastante más rápido que un enfoque iterativo, fila a fila.</span><span class="sxs-lookup"><span data-stu-id="b1243-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="b1243-113">Los cursores de avance rápido y solo lectura se pueden reemplazar fácilmente por una construcción de bucle.</span><span class="sxs-lookup"><span data-stu-id="b1243-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="b1243-114">A continuación se muestra un ejemplo sencillo:</span><span class="sxs-lookup"><span data-stu-id="b1243-114">Below is a simple example.</span></span> <span data-ttu-id="b1243-115">Este código de ejemplo actualiza las estadísticas de todas las tablas de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b1243-115">This code example updates the statistics for every table in the database.</span></span> <span data-ttu-id="b1243-116">Mediante la iteración a través de las tablas del bucle, podemos ejecutar cada comando en una secuencia.</span><span class="sxs-lookup"><span data-stu-id="b1243-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span></span>

<span data-ttu-id="b1243-117">En primer lugar, cree una tabla temporal que contenga un número de fila único usado para identificar las instrucciones individuales:</span><span class="sxs-lookup"><span data-stu-id="b1243-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span></span>

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

<span data-ttu-id="b1243-118">En segundo lugar, inicialice las variables necesarias para realizar el bucle:</span><span class="sxs-lookup"><span data-stu-id="b1243-118">Second, initialize the variables required to perform the loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="b1243-119">Ahora, recorra las instrucciones ejecutándolas de una en una:</span><span class="sxs-lookup"><span data-stu-id="b1243-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="b1243-120">Finalmente, elimine la tabla temporal creada en el primer paso</span><span class="sxs-lookup"><span data-stu-id="b1243-120">Finally drop the temporary table created in the first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="b1243-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1243-121">Next steps</span></span>
<span data-ttu-id="b1243-122">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="b1243-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
<span data-ttu-id="b1243-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span><span class="sxs-lookup"><span data-stu-id="b1243-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span></span>


<!--Other Web references-->
