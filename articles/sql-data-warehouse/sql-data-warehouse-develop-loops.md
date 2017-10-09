---
title: "aaaLeverage T-SQL bucles en el almacén de datos de SQL de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="db9b9-103">Bucles en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="db9b9-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="db9b9-104">Almacenamiento de datos SQL admite hello [mientras][mientras] bucle para ejecutar repetidamente los bloques de instrucciones.</span><span class="sxs-lookup"><span data-stu-id="db9b9-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="db9b9-105">Esta operación continuará para mientras Hola especifica las condiciones son true o hasta que código de hello termina específicamente bucle de hello mediante hello `BREAK` palabra clave.</span><span class="sxs-lookup"><span data-stu-id="db9b9-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="db9b9-106">Los bucles son especialmente útiles para reemplazar los cursores definidos en código SQL.</span><span class="sxs-lookup"><span data-stu-id="db9b9-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="db9b9-107">Afortunadamente, casi todos los cursores que se escriben en el código SQL son de hello rápido hacia delante, de lectura solo diversos.</span><span class="sxs-lookup"><span data-stu-id="db9b9-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="db9b9-108">Por lo tanto, [mientras] bucles son una buena alternativa si descubre que tiene que tener tooreplace uno.</span><span class="sxs-lookup"><span data-stu-id="db9b9-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="db9b9-109">Aprovechamiento de bucles y sustitución de cursores en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="db9b9-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="db9b9-110">Sin embargo, antes de adentrarnos en head en primer lugar debe pregúntese lo siguiente: Hola siguiente pregunta: "este cursor se pudo volver a escribirse toouse operaciones basadas en conjuntos?".</span><span class="sxs-lookup"><span data-stu-id="db9b9-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="db9b9-111">En muchos casos respuesta Hola será Sí y a menudo es más recomendable Hola.</span><span class="sxs-lookup"><span data-stu-id="db9b9-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="db9b9-112">Una operación basada en conjunto a menudo se realiza bastante más rápido que un enfoque iterativo, fila a fila.</span><span class="sxs-lookup"><span data-stu-id="db9b9-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="db9b9-113">Los cursores de avance rápido y solo lectura se pueden reemplazar fácilmente por una construcción de bucle.</span><span class="sxs-lookup"><span data-stu-id="db9b9-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="db9b9-114">A continuación se muestra un ejemplo sencillo:</span><span class="sxs-lookup"><span data-stu-id="db9b9-114">Below is a simple example.</span></span> <span data-ttu-id="db9b9-115">Este ejemplo de código actualiza las estadísticas de Hola para todas las tablas de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="db9b9-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="db9b9-116">Una iteración sobre tablas de hello en bucle Hola se está tooexecute capaz de cada comando de la secuencia.</span><span class="sxs-lookup"><span data-stu-id="db9b9-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="db9b9-117">En primer lugar, cree una tabla temporal que contiene una fila única número tooidentify usado Hola instrucciones individuales:</span><span class="sxs-lookup"><span data-stu-id="db9b9-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

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

<span data-ttu-id="db9b9-118">En segundo lugar, inicializar el bucle de Hola de hello variables tooperform necesarios:</span><span class="sxs-lookup"><span data-stu-id="db9b9-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="db9b9-119">Ahora, recorra las instrucciones ejecutándolas de una en una:</span><span class="sxs-lookup"><span data-stu-id="db9b9-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="db9b9-120">Finalmente, descargará la tabla temporal de hello creada en el primer paso de Hola</span><span class="sxs-lookup"><span data-stu-id="db9b9-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="db9b9-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db9b9-121">Next steps</span></span>
<span data-ttu-id="db9b9-122">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="db9b9-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[mientras]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
