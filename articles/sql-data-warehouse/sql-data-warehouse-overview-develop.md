---
title: aaaResources para desarrollar un almacenamiento de datos en Azure | Documentos de Microsoft
description: "Conceptos de desarrollo, decisiones de diseño, recomendaciones y técnicas de codificación para el Almacenamiento de datos SQL."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="bd02c-103">Decisiones de diseño y técnicas de codificación para el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="bd02c-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="bd02c-104">Eche un vistazo a través de estos artículos de desarrollo toobetter comprender las decisiones de diseño clave, recomendaciones y técnicas de codificación para el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="bd02c-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="bd02c-105">Decisiones de diseño clave</span><span class="sxs-lookup"><span data-stu-id="bd02c-105">Key design decisions</span></span>
<span data-ttu-id="bd02c-106">Hello artículos siguientes resaltan algunos de los conceptos básicos de Hola y decisiones de diseño que deberá toounderstand para el desarrollo de Hola de su almacén de datos distribuidos con almacenamiento de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="bd02c-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="bd02c-107">[conexiones][connections]</span><span class="sxs-lookup"><span data-stu-id="bd02c-107">[connections][connections]</span></span>
* <span data-ttu-id="bd02c-108">[simultaneidad][concurrency]</span><span class="sxs-lookup"><span data-stu-id="bd02c-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="bd02c-109">[transacciones][transactions]</span><span class="sxs-lookup"><span data-stu-id="bd02c-109">[transactions][transactions]</span></span>
* <span data-ttu-id="bd02c-110">[esquemas definidos por el usuario][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="bd02c-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="bd02c-111">[distribución de tablas][table distribution]</span><span class="sxs-lookup"><span data-stu-id="bd02c-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="bd02c-112">[índices de tabla][table indexes]</span><span class="sxs-lookup"><span data-stu-id="bd02c-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="bd02c-113">[particiones de tabla][table partitions]</span><span class="sxs-lookup"><span data-stu-id="bd02c-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="bd02c-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="bd02c-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="bd02c-115">[estadísticas][statistics]</span><span class="sxs-lookup"><span data-stu-id="bd02c-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="bd02c-116">Recomendaciones de desarrollo y técnicas de codificación</span><span class="sxs-lookup"><span data-stu-id="bd02c-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="bd02c-117">En estos artículos se abordan técnicas de codificación, sugerencias y recomendaciones específicas para el desarrollo de su Almacenamiento de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="bd02c-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="bd02c-118">[procedimientos almacenados][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="bd02c-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="bd02c-119">[etiquetas][labels]</span><span class="sxs-lookup"><span data-stu-id="bd02c-119">[labels][labels]</span></span>
* <span data-ttu-id="bd02c-120">[vistas][views]</span><span class="sxs-lookup"><span data-stu-id="bd02c-120">[views][views]</span></span>
* <span data-ttu-id="bd02c-121">[tablas temporales][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="bd02c-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="bd02c-122">[SQL dinámico][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="bd02c-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="bd02c-123">[bucle][looping]</span><span class="sxs-lookup"><span data-stu-id="bd02c-123">[looping][looping]</span></span>
* <span data-ttu-id="bd02c-124">[opciones de agrupar por][group by options]</span><span class="sxs-lookup"><span data-stu-id="bd02c-124">[group by options][group by options]</span></span>
* <span data-ttu-id="bd02c-125">[asignación de variables][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="bd02c-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd02c-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd02c-126">Next steps</span></span>
<span data-ttu-id="bd02c-127">Una vez que ha estado a través de los artículos de desarrollo de Hola, eche un vistazo a través de hello [referencia de Transact-SQL] [ Transact-SQL reference] página para obtener más información acerca de la sintaxis de hello compatible para almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="bd02c-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
