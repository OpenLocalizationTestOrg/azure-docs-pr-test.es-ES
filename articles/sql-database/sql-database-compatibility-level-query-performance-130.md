---
title: Nivel de compatibilidad 130 en bases de datos - Azure SQL Database | Microsoft Docs
description: "En este artículo, se exploran las ventajas de ejecutar Azure SQL Database en el nivel de compatibilidad 130 y se analiza cómo aprovechar las ventajas de las nuevas características del optimizador de consultas y del procesador de consultas. También se abordan los posibles efectos secundarios en el rendimiento de las consultas para las aplicaciones existentes de SQL."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: c08c0690df4f389416e4ed2e2df2dbb72d6fd567
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="6c9ac-104">Rendimiento mejorado de consultas con el nivel de compatibilidad 130 en Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="6c9ac-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="6c9ac-105">Base de datos SQL de Azure ejecuta de forma transparente cientos de miles de bases de datos en muchos niveles de compatibilidad diferentes, conservando y garantizando la compatibilidad con versiones anteriores para la versión correspondiente de Microsoft SQL Server para todos sus clientes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="6c9ac-106">En este artículo, se exploran las ventajas de ejecutar Azure SQL Database en el nivel de compatibilidad 130 y se analiza cómo aprovechar las ventajas de las nuevas características del optimizador de consultas y del procesador de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-106">In this article, we explore the benefits of running your Azure SQL Databse at compatibility level 130, and leveraging the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="6c9ac-107">También se abordan los posibles efectos secundarios en el rendimiento de las consultas para las aplicaciones existentes de SQL.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-107">We also address the possible side-effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="6c9ac-108">Como recordatorio del historial, la alineación de las versiones SQL con los niveles de compatibilidad predeterminados es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c9ac-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="6c9ac-109">100: en SQL Server 2008 y Base de datos SQL de Azure V11.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="6c9ac-110">110: en SQL Server 2012 y Base de datos SQL de Azure V11.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="6c9ac-111">120: en SQL Server 2014 y Base de datos SQL de Azure V12.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="6c9ac-112">130: en SQL Server 2016 y Base de datos SQL de Azure V12.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c9ac-113">A partir de **mediados de junio de 2016**, el nivel de compatibilidad predeterminado en Azure SQL Database será 130, en lugar de 120, para las bases de datos **de nueva creación**.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-113">Starting in **mid-June 2016**, in Azure SQL Database, the default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="6c9ac-114">Las bases de datos creadas antes de mediados de junio de 2016 *no* se verán afectadas y mantendrán su nivel de compatibilidad actual (100, 110 o 120).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="6c9ac-115">Las bases de datos migradas de la versión 11 de Azure SQL Database a la versión 12 tendrán un nivel de compatibilidad de 100 o 110.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-115">Databases that migrated from Azure SQL Database version V11 to V12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="6c9ac-116">Acerca del nivel de compatibilidad 130</span><span class="sxs-lookup"><span data-stu-id="6c9ac-116">About compatibility level 130</span></span>
<span data-ttu-id="6c9ac-117">En primer lugar, si desea conocer el nivel de compatibilidad actual de una base de datos, ejecute la siguiente instrucción de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-117">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="6c9ac-118">Antes de que se produzca este cambio al nivel 130 en las bases de datos **de nueva creación** , vamos a revisar en qué consiste este cambio a través de algunos ejemplos de consultas muy básicos y ver cómo cualquiera puede beneficiarse de él.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-118">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="6c9ac-119">El procesamiento de consultas en las bases de datos relacionales puede ser muy complejo y llevar al uso de un volumen importante de matemáticas y ciencias informáticas para poder comprender los comportamientos y opciones de diseño inherentes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-119">Query processing in relational databases can be very complex and can lead to lots of computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="6c9ac-120">En este documento, el contenido se ha simplificado intencionadamente para garantizar que cualquier persona con unos conocimientos técnicos mínimos pueda entender el impacto del cambio de nivel de compatibilidad y determinar cómo puede beneficiar a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-120">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="6c9ac-121">Echemos un vistazo a lo que aporta el nivel de compatibilidad 130.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-121">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="6c9ac-122">Puede encontrar más detalles en [Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), pero aquí tiene un breve resumen:</span><span class="sxs-lookup"><span data-stu-id="6c9ac-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="6c9ac-123">La operación Insert de una instrucción Insert-select puede ser de subprocesos múltiples o puede tener un plan paralelo, mientras que antes esta operación era de subproceso único.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-123">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="6c9ac-124">Las consultas de tabla con optimización de memoria y variables de tabla pueden tener ahora planes paralelos, mientras que antes esta operación también era de subproceso único.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="6c9ac-125">Las estadísticas de una tabla con optimización de memoria ahora pueden muestrearse y se actualizan de forma automática.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="6c9ac-126">Consulte [Novedades (motor de base de datos): OLTP en memoria](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para más detalles.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="6c9ac-127">El modo por lotes frente al modo de fila cambia con los índices de almacenamiento de columnas</span><span class="sxs-lookup"><span data-stu-id="6c9ac-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="6c9ac-128">Las ordenaciones en una tabla con un índice de almacenamiento de columnas están ahora en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="6c9ac-129">Los agregados basados en ventanas operan ahora en modo por lotes, tal como instrucciones de TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="6c9ac-130">Las consultas en tablas de almacenamiento de columnas con varias cláusulas Distinct funcionan en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="6c9ac-131">Las consultas que se ejecutan en DOP = 1 o con un plan en serie también se ejecutan en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="6c9ac-132">Por último, las mejoras de estimación de cardinalidad vienen con el nivel de compatibilidad 120, pero para aquellos que estén trabajando en un nivel de compatibilidad inferior (es decir, 100 o 110), el cambio al nivel de compatibilidad 130 también aportará estas mejoras, y éstas a su vez pueden beneficiar también al rendimiento de las consultas de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), the move to compatibility level 130 will also bring these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="6c9ac-133">Prácticas con el nivel de compatibilidad 130</span><span class="sxs-lookup"><span data-stu-id="6c9ac-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="6c9ac-134">Primero vamos a juntar algunas tablas, índices y datos aleatorios creados para practicar algunas de estas nuevas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-134">First let’s get some tables, indexes and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="6c9ac-135">Los ejemplos de script TSQL se pueden ejecutar en SQL Server 2016, o en Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-135">The TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="6c9ac-136">Sin embargo, al crear una base de datos SQL de Azure, asegúrese de que elige como mínimo una base de datos P2 porque necesita al menos un par de núcleos para permitir subprocesamiento múltiple y por lo tanto beneficiarse de estas características.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-136">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="6c9ac-137">Ahora, echemos un vistazo a algunas de las características de procesamiento de consultas que trae el nivel de compatibilidad de 130.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-137">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="6c9ac-138">INSERT en paralelo</span><span class="sxs-lookup"><span data-stu-id="6c9ac-138">Parallel INSERT</span></span>
<span data-ttu-id="6c9ac-139">La ejecución de las siguientes instrucciones de TSQL, ejecuta la operación INSERT en los niveles de compatibilidad 120 y 130, que ejecutan respectivamente la operación INSERT en un modelo de subproceso único (120) y en un modelo de subprocesos múltiples (130).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-139">Executing the TSQL statements below executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-140">Si solicita el estado del plan de consulta, y examina su representación gráfica o su contenido XML, puede determinar qué función de estimación de cardinalidad se está usando.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-140">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="6c9ac-141">Al examinar en paralelo los planes en la figura 1, podemos ver claramente que la ejecución del almacenamiento de columnas INSERT va de en serie en 120 a en paralelo en 130.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-141">Looking at the plans side-by-side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="6c9ac-142">Observe además el cambio del icono de iterador en el plan de 130 que muestra dos flechas paralelas, esto ilustra el hecho de que ahora la ejecución del iterador es realmente en paralelo.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-142">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="6c9ac-143">Si tiene que realizar grandes operaciones INSERT, la ejecución en paralelo, vinculada al número de núcleos que tiene a su disposición para la base de datos, le proporcionará un mejor rendimiento (hasta 100 veces más rápido, dependiendo de la situación).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-143">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, will perform better; up to a 100 times faster depending your situation!</span></span>

<span data-ttu-id="6c9ac-144">*Figura 1: Operación INSERT cambia de en serie a en paralelo con el nivel de compatibilidad 130.*</span><span class="sxs-lookup"><span data-stu-id="6c9ac-144">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![En la Ilustración 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="6c9ac-146">Modo por lotes EN SERIE</span><span class="sxs-lookup"><span data-stu-id="6c9ac-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="6c9ac-147">De forma similar, pasar al nivel de compatibilidad 130 para el procesamiento de filas de datos permite el procesamiento de modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-147">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="6c9ac-148">En primer lugar, las operaciones en modo por lotes solo están disponibles cuando tenga un índice de almacenamiento de columnas preparado.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="6c9ac-149">En segundo lugar, un lote normalmente representa aproximadamente 900 filas y utiliza una lógica de código optimizada para una CPU de varios núcleos, un mayor rendimiento de la memoria y aprovecha directamente los datos comprimidos del almacenamiento de columnas, siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="6c9ac-150">En estas condiciones, SQL Server 2016 puede procesar aproximadamente 900 filas a la vez, en lugar de la 1 fila de cada vez, y en consecuencia, los costos generales de la operación se comparten ahora entre todo el lote, lo que reduce el costo global por fila.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="6c9ac-151">Esta cantidad de operaciones compartidas combinadas con la compresión de almacenamiento de columnas, básicamente reduce la latencia implicada en una operación de modo por lotes SELECT.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-151">This shared amount of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="6c9ac-152">Puede encontrar más detalles sobre el almacenamiento de columnas y el modo por lotes en [Descripción de los índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-152">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-153">Como se ve a continuación observando los planes de consulta en paralelo en la figura 2, el modo de procesamiento ha cambiado con el nivel de compatibilidad y, como consecuencia, cuando se ejecutan las consultas juntas en el nivel de compatibilidad de ambos, podemos ver que la mayor parte del tiempo de procesamiento se dedica al modo de fila (86 %), en comparación con el modo por lotes (14 %), donde se han procesado 2 lotes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-153">As visible below, by observing the query plans side-by-side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="6c9ac-154">Al aumentar el conjunto de datos, aumentará el beneficio.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-154">Increase the dataset, the benefit will increase.</span></span>

<span data-ttu-id="6c9ac-155">*Figura 2: Operación SELECT cambia de modo en serie a modo por lotes con el nivel de compatibilidad 130.*</span><span class="sxs-lookup"><span data-stu-id="6c9ac-155">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![Ilustración 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="6c9ac-157">Modo por lotes en ejecución SORT</span><span class="sxs-lookup"><span data-stu-id="6c9ac-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="6c9ac-158">Similar a la anterior, pero aplicado a una operación SORT, la transición del modo de fila (nivel de compatibilidad 120) al modo por lotes (nivel de compatibilidad de 130) mejora el rendimiento de la operación SORT por las mismas razones.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-158">Similar to the above, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-159">En la figura 3, se puede ver en paralelo que la operación SORT en el modo de fila representa el 81 % del costo, mientras que el modo por lotes solo representa el 19 % del costo (respectivamente 81 % y 56 % en la ordenación).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-159">Visible side-by-side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="6c9ac-160">*Figura 3: Operación SORT cambia de modo de fila a modo por lotes con el nivel de compatibilidad 130.*</span><span class="sxs-lookup"><span data-stu-id="6c9ac-160">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![Ilustración 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="6c9ac-162">Obviamente, estos ejemplos solo contienen decenas de miles de filas, esto es una cantidad insignificante comparada con la de los datos disponibles en la mayoría de los servidores SQL de hoy en día.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="6c9ac-163">No hay más que pensar en estos resultados aplicados a millones de filas y veremos que esto podría traducirse en varios minutos de ejecución que se ahorrarían cada día, dependiendo de la naturaleza de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="6c9ac-164">Mejoras de estimación de cardinalidad (CE)</span><span class="sxs-lookup"><span data-stu-id="6c9ac-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="6c9ac-165">Desde que se introdujo con SQL Server 2014, cualquier base de datos que se ejecuta en un nivel de compatibilidad 120 o superior hace uso de la nueva funcionalidad de estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="6c9ac-166">Básicamente, la estimación de cardinalidad es la lógica utilizada para determinar cómo SQL Server ejecutará una consulta en base a su costo estimado.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-166">Essentially, cardinality estimation is the logic used to determine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="6c9ac-167">La estimación se calcula usando la entrada de datos de estadísticas asociadas con los objetos que participan en esa consulta.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-167">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="6c9ac-168">En la práctica, en un nivel alto, las funciones de estimación de cardinalidad son estimaciones de recuento de filas junto con información sobre la distribución de los valores, recuentos de valores distintos y recuentos duplicados, contenidas en las tablas y los objetos a los que se hace referencia en la consulta.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="6c9ac-169">Si se obtienen estimaciones incorrectas, se puede producir E/S de disco innecesarias debidas a concesiones de memoria insuficientes (es decir, vertidos TempDB), o a la selección de una ejecución de un plan en serie en lugar de una ejecución de plan paralelo, por solo mencionar algunos problemas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-169">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (i.e. TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="6c9ac-170">La conclusión es que las estimaciones incorrectas pueden provocar una degradación del rendimiento general de la ejecución de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-170">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="6c9ac-171">Por el contrario, las estimaciones mejoradas y más precisas, llevan a la mejora de las ejecuciones de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-171">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="6c9ac-172">Como se mencionó antes, las optimizaciones de consultas y las estimaciones son una cuestión compleja, pero si desea más información acerca de los planes de consulta y el calculador de cardinalidad, puede consultar el documento [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) (Optimización de los planes de consultas con el calculador de cardinalidad de SQL Server 2014) para un análisis más profundo.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="6c9ac-173">¿Qué estimación de cardinalidad está usando actualmente?</span><span class="sxs-lookup"><span data-stu-id="6c9ac-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="6c9ac-174">Para determinar con qué estimaciones de cardinalidad se ejecutan las consultas, usemos los siguientes ejemplos de consulta.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-174">To determine under which Cardinality Estimation your queries are running, let’s just use the query samples below.</span></span> <span data-ttu-id="6c9ac-175">Tenga en cuenta que este primer ejemplo se ejecutará en el nivel de compatibilidad 110, lo que implica el uso de las antiguas funciones de estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-175">Note that this first example will run under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-176">Una vez completada la ejecución, haga clic en el vínculo XML y examine las propiedades del primer iterador como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-176">Once execution is complete, click on the XML link, and look at the properties of the first iterator as shown below.</span></span> <span data-ttu-id="6c9ac-177">Tenga en cuenta el nombre de propiedad llamado CardinalityEstimationModelVersion establecido actualmente en 70.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-177">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="6c9ac-178">Esto no significa que el nivel de compatibilidad de base de datos está establecida en la versión 7.0 de SQL Server (se establece en 110 como puede verse en las instrucciones de TSQL anteriores), pero el valor 70 simplemente representa la funcionalidad heredada de estimación de cardinalidad disponible desde SQL Server 7.0, que no ha sufrido revisiones sustanciales hasta SQL Server 2014 (que viene con un nivel de compatibilidad de 120).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-178">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the TSQL statements above), but the value 70 simply represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="6c9ac-179">*Figura 4: CardinalityEstimationModelVersion está establecida en 70, cuando se usa un nivel de compatibilidad de 110 o inferior.*</span><span class="sxs-lookup"><span data-stu-id="6c9ac-179">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or below.*</span></span>

![Ilustración 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="6c9ac-181">Como alternativa, puede cambiar el nivel de compatibilidad a 130 y deshabilitar el uso de la nueva función de estimación de cardinalidad usando LEGACY_CARDINALITY_ESTIMATION establecido en ON con [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx) (Modificar configuración de ámbito de base de datos).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-181">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="6c9ac-182">Esto será exactamente lo mismo que usar 110 desde el punto de vista de una función de estimación de cardinalidad, mientras se utiliza el nivel de compatibilidad de procesamiento de consultas más reciente.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-182">This will be exactly the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="6c9ac-183">De esta forma, puede beneficiarse de las nuevas características de procesamiento de consultas que vienen con el nivel de compatibilidad más reciente (es decir, el modo por lotes), y a la vez seguir dependiendo de la funcionalidad de estimación de cardinalidad anterior si es necesario.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-183">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (i.e. batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-184">Basta con mover el nivel de compatibilidad 120 o 130 para habilitar la nueva funcionalidad de estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-184">Simply moving to the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="6c9ac-185">En tal caso, el valor predeterminado CardinalityEstimationModelVersion se configurará según corresponda a 120 o 130 como se puede ver a continuación.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-185">In such a case, the default CardinalityEstimationModelVersion will be set accordingly to 120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-186">*Figura 5: CardinalityEstimationModelVersion está establecida en 130, cuando se usa un nivel de compatibilidad de 130.*</span><span class="sxs-lookup"><span data-stu-id="6c9ac-186">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![Ilustración 5.](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="6c9ac-188">Observación de las diferencias de estimación de cardinalidad</span><span class="sxs-lookup"><span data-stu-id="6c9ac-188">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="6c9ac-189">Ahora, vamos a ejecutar una consulta un poco más compleja que implica una INNER JOIN con una cláusula WHERE con algunos predicados, y vamos a echar un vistazo en primer lugar a la estimación del recuento de filas de la antigua función de estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-190">La ejecución de esta consulta devuelve eficazmente 200.704 filas, mientras que la estimación de filas con la antigua funcionalidad de estimación de cardinalidad notifica 194.284 filas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-190">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="6c9ac-191">Obviamente, como ya se dijo antes, estos resultados del recuento de filas también dependerán de la frecuencia con la que haya ejecutado los ejemplos anteriores, que rellenan las tablas de ejemplo una y otra vez en cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-191">Obviously, as said before, these row count results will also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="6c9ac-192">Obviamente, los predicados de la consulta influirán también en la estimación real aparte de la forma de tabla, el contenido de datos, y la forma en la que estos datos s relacionan entre sí.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-192">Obviously, the predicates in your query will also have an influence on the actual estimation aside from the table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="6c9ac-193">*Figura 6: La estimación del número de filas es 194.284 es decir 6.000 filas menos de las 200.704 filas esperadas.*</span><span class="sxs-lookup"><span data-stu-id="6c9ac-193">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![Ilustración 6.](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="6c9ac-195">Del mismo modo, vamos ahora a ejecutar la misma consulta con la nueva funcionalidad de estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-195">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="6c9ac-196">Mirando a continuación vemos que la estimación de filas es 202.877, es decir mucho más cercana y superior que la antigua estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-196">Looking at the below, we now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="6c9ac-197">*Figura 7: La estimación del número de filas es ahora 202.877, en lugar de 194.284.*</span><span class="sxs-lookup"><span data-stu-id="6c9ac-197">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![Ilustración 7.](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="6c9ac-199">En realidad, el conjunto de resultados es 200.704 filas (pero todo depende de la frecuencia con la que se ejecutaron las consultas de los ejemplos anteriores, y lo que es más importante porque el TSQL utiliza la instrucción de RAND(), los valores reales que se devuelven pueden variar de una ejecución a la siguiente).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-199">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the TSQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="6c9ac-200">Por lo tanto, en este ejemplo concreto, la nueva estimación de cardinalidad hace una mejor estimación del número de filas, no cabe duda de que 202.877 está mucho más cerca de 200.704 que 194.284.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-200">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="6c9ac-201">Por último, si se cambian los predicados de la cláusula WHERE para igualdad (en lugar de ">" por ejemplo), esto podría hacer que haya incluso más diferencia entre las estimaciones de la antigua y la nueva función de cardinalidad, dependiendo de las coincidencias que se obtengan.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-201">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="6c9ac-202">En este caso, una diferencia de aproximadamente 6000 filas con respecto recuento real, en algunas situaciones no representa una gran cantidad de datos.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="6c9ac-203">Ahora, si se traspone esto a millones de filas en varias tablas y consultas más complejas, a veces, puede haber una diferencia de millones de filas en la estimación y, por lo tanto, el riesgo de seleccionar el plan de ejecución equivocado, o de solicitar concesiones de memoria insuficientes provocando desbordamientos de TempDB y con ello más operaciones de E/S, son mucho mayores.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-203">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows , and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="6c9ac-204">Si tiene oportunidad practique esta comparación con sus consultas y conjuntos de datos más habituales, y vea por usted mismo la diferencia entre las estimaciones nuevas y las antiguas, mientras que algunas se pueden alejar más de la realidad, en otras se acerca más al recuento real devuelto en los conjuntos de resultados.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-204">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of the old and new estimates are affected, while some could just become more off from the reality, or some others just simply closer to the actual row counts actually returned in the result sets.</span></span> <span data-ttu-id="6c9ac-205">Todo dependerá de la forma de las consultas, las características de base de datos SQL de Azure, la naturaleza y el tamaño de los conjuntos de datos y las estadísticas disponibles sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-205">All of it will depend of the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="6c9ac-206">Si acaba de crear la instancia de Base de datos SQL de Azure, el optimizador de consultas tendrá que generar su conocimiento desde cero en lugar de reutilizar las estadísticas de las ejecuciones de consultas anteriores.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-206">If you just created your Azure SQL Database instance, the query optimizer will have to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="6c9ac-207">Por lo tanto, las estimaciones son muy contextuales y casi específicas para cada situación de aplicación y servidor.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-207">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="6c9ac-208">Es un aspecto importante que no hay que olvidar.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-208">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="6c9ac-209">Algunas consideraciones a tener en cuenta</span><span class="sxs-lookup"><span data-stu-id="6c9ac-209">Some considerations to take into account</span></span>
<span data-ttu-id="6c9ac-210">Aunque la mayoría de las cargas se benefician del nivel de compatibilidad 130, antes de adoptar el nivel de compatibilidad para el entorno de producción, tiene básicamente 3 opciones:</span><span class="sxs-lookup"><span data-stu-id="6c9ac-210">Although most workloads would benefit from the compatibility level 130, before you adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="6c9ac-211">Mover al nivel de compatibilidad 130 y ver cómo funciona todo.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-211">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="6c9ac-212">Si nota algunas regresiones simplemente vuelva a establecer la compatibilidad de nivel en el nivel original, o mantenga el nivel 130 y devuelva solo la estimación de cardinalidad al modo heredado (como se explicó anteriormente, esto por sí solo podría solucionar el problema).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-212">In case you notice some regressions, you just simply set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As explained above, this alone could address the issue).</span></span>
2. <span data-ttu-id="6c9ac-213">Probar detalladamente las aplicaciones existentes con una carga similar a la de producción, ajustar y validar el rendimiento antes de pasar a producción.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-213">You thoroughly test your existing applications under similar production load, fine tune, and validate the performance before going to production.</span></span> <span data-ttu-id="6c9ac-214">En el caso de que aparezcan problemas, igual que en el caso anterior, siempre puede volver al nivel de compatibilidad original, o simplemente devolver la estimación de cardinalidad al modo heredado.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-214">In case of issues, same as above, you can always go back to the original compatibility level, or simply reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="6c9ac-215">Como última opción, y la forma más reciente resolver estas cuestiones, puede aprovechar el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-215">As a final option, and the most recent way to address these questions, is to leverage the Query Store.</span></span> <span data-ttu-id="6c9ac-216">Esta es la opción recomendada en este momento.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-216">That’s today’s recommended option!</span></span> <span data-ttu-id="6c9ac-217">Para ayudarle en el análisis de las consultas con el nivel de compatibilidad 120 o inferior frente al nivel 130, no podemos insistir lo suficiente en nuestra recomendación de que use el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-217">To assist the analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="6c9ac-218">El Almacén de consultas está disponible con la versión más reciente de Base de datos SQL de Azure V12 y se ha diseñado para ayudarle a solucionar problemas de rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-218">Query Store is available with the latest version of Azure SQL Database V12, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="6c9ac-219">Piense en el Almacén de consultas como una caja negra para la base de datos en donde se recopila y presenta información detallada del historial de todas las consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-219">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="6c9ac-220">Esto simplifica enormemente el análisis forense del rendimiento, reduciendo el tiempo de diagnóstico y la resolución de problemas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-220">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="6c9ac-221">Puede encontrar más información en [A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)(Una caja negra para la base de datos).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="6c9ac-222">En el nivel superior, si ya tiene un conjunto de bases de datos que se ejecuta en el nivel de compatibilidad 120 o por debajo y planea cambiar algunas de ellas a 130, o si la carga de trabajo aprovisiona automáticamente nuevas bases de datos que pronto se establecerán de forma predeterminada en el nivel 130, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c9ac-222">At the high-level, if you already have a set of databases running at compatibility level 120 or below, and plan to move some of them to 130, or because your workload automatically provision new databases that will be soon be set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="6c9ac-223">Antes de cambiar al nuevo nivel de compatibilidad en producción, habilite el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-223">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="6c9ac-224">Puede consultar [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) (Cambio del modo de compatibilidad de la base de datos y uso del Almacén de consultas) para más información.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-224">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="6c9ac-225">A continuación, pruebe todas las cargas de trabajo críticas con datos representativos y las consultas en un entorno similar al de producción y compare el rendimiento que ha experimentado y la información proporcionada por el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="6c9ac-226">Si se producen algunas regresiones, puede identificar las consultas con regresión con el Almacén de consultas y utilizar la opción para forzar el plan del Almacén de consultas (también conocido como plan de anclaje).</span><span class="sxs-lookup"><span data-stu-id="6c9ac-226">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="6c9ac-227">En este caso, permanezca con el nivel de compatibilidad 130 y use el plan de consulta anterior como sugiere el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-227">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="6c9ac-228">Si desea aprovechar las nuevas características y capacidades de Base de datos SQL de Azure (que ejecuta SQL Server 2016), pero es susceptible en relación a los cambios realizados por el nivel de compatibilidad 130, como último recurso, puede considerar la posibilidad de forzar el nivel de compatibilidad para volver al nivel que mejor se adapte a su carga de trabajo usando una instrucción ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-228">If you want to leverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="6c9ac-229">Pero en primer lugar, tenga en cuenta que la opción de anclaje de plan de Almacén de consultas es la mejor opción, porque no usar el nivel 130 es básicamente mantenerse en el nivel de funcionalidad de una versión anterior de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-229">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="6c9ac-230">Si tiene aplicaciones multiinquilinos que abarcan varias bases de datos, puede ser necesario actualizar la lógica de aprovisionamiento de las bases de datos para asegurar un nivel de compatibilidad coherente en todas las bases de datos, las antiguas y las creadas recientemente.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-230">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="6c9ac-231">El rendimiento de carga de trabajo de su aplicación podría ser sensible al hecho de que algunas bases de datos se ejecutan en niveles diferentes de compatibilidad y, por lo tanto, podría ser necesaria la coherencia de nivel de compatibilidad en cualquier base de datos con el fin de proporcionar la misma experiencia a todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-231">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="6c9ac-232">Tenga en cuenta que esto no es obligatorio, realmente depende de cómo afecte el nivel de compatibilidad a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-232">Note that it is not a mandate, it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="6c9ac-233">Por último, con respecto a la estimación de cardinalidad, igual que con el cambio de nivel de compatibilidad, antes de proceder con los cambios en el nivel de producción, se recomienda probar la carga de trabajo de producción en las nuevas condiciones para determinar si la aplicación se beneficia de las mejoras de estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-233">Last, regarding the Cardinality Estimation, and just like changing the compatibility level, before proceeding in production, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="6c9ac-234">Conclusión</span><span class="sxs-lookup"><span data-stu-id="6c9ac-234">Conclusion</span></span>
<span data-ttu-id="6c9ac-235">El uso de Base de datos SQL de Azure para beneficiarse de todas las mejoras de SQL Server 2016 puede mejorar claramente sus ejecuciones de consultas.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-235">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="6c9ac-236">Así de simple.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-236">Just as-is!</span></span> <span data-ttu-id="6c9ac-237">Por supuesto, al igual que con cualquier característica nueva, tiene que realizarse una evaluación adecuada para determinar las condiciones exactas en las que la carga de trabajo de la base de datos funciona mejor.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-237">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="6c9ac-238">La experiencia demuestra que es de esperar que la mayoría de las cargas de trabajo se ejecuten al menos de forma transparente en el nivel de compatibilidad 130, mientras se aprovechan las nuevas funciones de procesamiento de consultas y la nueva estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-238">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="6c9ac-239">De todas formas, siendo realistas, siempre hay algunas excepciones y actuar con la debida diligencia es una valoración importante para determinar cuánto puede beneficiarse de estas mejoras.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="6c9ac-240">Y repetimos que el Almacén de consultas puede ser una gran ayuda para realizar este trabajo.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-240">And again, the Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="6c9ac-241">A medida que SQL Azure evoluciona, se puede esperar un nivel de compatibilidad 140 en el futuro.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-241">As SQL Azure evolves, you can expect a compatibility level 140 in the future.</span></span> <span data-ttu-id="6c9ac-242">Cuando el momento sea apropiado, empezaremos a hablar de lo que aportará este futuro nivel de compatibilidad 140, igual que hemos explicado brevemente aquí lo que el nivel de compatibilidad 130 aporta hoy.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="6c9ac-243">Por ahora, no olvide que a partir de junio de 2016, Base de datos SQL de Azure cambiará el nivel de compatibilidad predeterminado de 120 a 130 para las bases de datos de nueva creación.</span><span class="sxs-lookup"><span data-stu-id="6c9ac-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change the default compatibility level from 120 to 130 for newly created databases.</span></span> <span data-ttu-id="6c9ac-244">¡Prepárese!</span><span class="sxs-lookup"><span data-stu-id="6c9ac-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="6c9ac-245">Referencias</span><span class="sxs-lookup"><span data-stu-id="6c9ac-245">References</span></span>
* [<span data-ttu-id="6c9ac-246">Novedades (motor de base de datos)</span><span class="sxs-lookup"><span data-stu-id="6c9ac-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="6c9ac-247">Blog: Query Store: A flight data recorder for your database (Almacén de consultas: Una caja negra para la base de datos) por Borko Novakovic, 8 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="6c9ac-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="6c9ac-248">Nivel de compatibilidad de ALTER TABLE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="6c9ac-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="6c9ac-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="6c9ac-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="6c9ac-250">Compatibility Level 130 for Azure SQL Database V12</span><span class="sxs-lookup"><span data-stu-id="6c9ac-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="6c9ac-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span><span class="sxs-lookup"><span data-stu-id="6c9ac-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="6c9ac-252">Descripción de los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="6c9ac-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="6c9ac-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database (Rendimiento mejorado de consultas con el nivel de compatibilidad 130 en Base de datos SQL de Azure) por Alain Lissoir, 6 de mayo de 2016</span><span class="sxs-lookup"><span data-stu-id="6c9ac-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
