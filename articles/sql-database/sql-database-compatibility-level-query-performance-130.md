---
title: nivel de compatibilidad de aaaDatabase 130 - base de datos de SQL de Azure | Documentos de Microsoft
description: "En este artículo, nos explore Hola ventajas de ejecutar la base de datos de SQL Azure en el nivel de compatibilidad 130 y aprovechar las ventajas de Hola de nuevo el optimizador de consultas de Hola y características del procesador de consultas. También tratamos Hola posibles efectos secundarios en el rendimiento de las consultas para las aplicaciones existentes de SQL Hola Hola."
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
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="e264a-104">Rendimiento mejorado de consultas con el nivel de compatibilidad 130 en Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="e264a-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="e264a-105">La base de datos de SQL Azure se ejecuta transparente cientos de miles de bases de datos en varios niveles de compatibilidad diferentes, conservar y garantizan toohello de versión correspondiente de Microsoft SQL Server para la compatibilidad con versiones anteriores Hola a todos sus clientes!</span><span class="sxs-lookup"><span data-stu-id="e264a-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="e264a-106">En este artículo, nos explore Hola ventajas de la ejecución de su base de datos de SQL Azure en el nivel de compatibilidad 130 y aprovechar las ventajas de Hola de nuevo el optimizador de consultas de Hola y características del procesador de consultas.</span><span class="sxs-lookup"><span data-stu-id="e264a-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="e264a-107">También tratamos Hola posibles efectos secundarios en el rendimiento de las consultas para las aplicaciones existentes de SQL Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="e264a-108">Como recordatorio del historial, la alineación de Hola de niveles de compatibilidad de toodefault de versiones SQL son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e264a-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="e264a-109">100: en SQL Server 2008 y Base de datos SQL de Azure V11.</span><span class="sxs-lookup"><span data-stu-id="e264a-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="e264a-110">110: en SQL Server 2012 y Base de datos SQL de Azure V11.</span><span class="sxs-lookup"><span data-stu-id="e264a-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="e264a-111">120: en SQL Server 2014 y Base de datos SQL de Azure V12.</span><span class="sxs-lookup"><span data-stu-id="e264a-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="e264a-112">130: en SQL Server 2016 y Base de datos SQL de Azure V12.</span><span class="sxs-lookup"><span data-stu-id="e264a-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e264a-113">A partir de **mid junio de 2016**, en la base de datos de SQL Azure, nivel de compatibilidad de hello predeterminado será 130 en lugar de 120 para **recién creado** bases de datos.</span><span class="sxs-lookup"><span data-stu-id="e264a-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="e264a-114">Las bases de datos creadas antes de mediados de junio de 2016 *no* se verán afectadas y mantendrán su nivel de compatibilidad actual (100, 110 o 120).</span><span class="sxs-lookup"><span data-stu-id="e264a-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="e264a-115">Bases de datos que se migran de la base de datos de SQL Azure versión V11 tooV12 tendrá un nivel de compatibilidad de 100 o 110.</span><span class="sxs-lookup"><span data-stu-id="e264a-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="e264a-116">Acerca del nivel de compatibilidad 130</span><span class="sxs-lookup"><span data-stu-id="e264a-116">About compatibility level 130</span></span>
<span data-ttu-id="e264a-117">En primer lugar, si desea que el nivel tooknow Hola de compatibilidad actual de la base de datos, ejecute hello después de la instrucción Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="e264a-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="e264a-118">Antes de este cambio se produce para los toolevel 130 **recién** crear bases de datos, vamos a revisar lo que este cambio consiste en ver algunos ejemplos de consulta muy básica y ver cómo cualquiera puede beneficiarse de él.</span><span class="sxs-lookup"><span data-stu-id="e264a-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="e264a-119">Procesamiento de consultas en bases de datos relacionales puede ser muy complejo y puede provocar toolots de equipo informática y matemáticas toounderstand Hola inherentes a las opciones de diseño y comportamientos.</span><span class="sxs-lookup"><span data-stu-id="e264a-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="e264a-120">En este documento, contenido de hello ha sido tooensure intencionadamente simplificada que cualquier persona con algunos conocimientos técnicos mínimos puede comprender el impacto del cambio del nivel de compatibilidad Hola Hola y determinar cómo puede beneficiar a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e264a-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="e264a-121">Echemos un vistazo qué nivel de compatibilidad de hello 130 pone en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="e264a-122">Puede encontrar más detalles en [Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), pero aquí tiene un breve resumen:</span><span class="sxs-lookup"><span data-stu-id="e264a-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="e264a-123">pueden ser multiproceso Hello operación de inserción de una instrucción Insert select o puede tener un plan paralelo, mientras que antes de que esta operación se un único subproceso.</span><span class="sxs-lookup"><span data-stu-id="e264a-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="e264a-124">Las consultas de tabla con optimización de memoria y variables de tabla pueden tener ahora planes paralelos, mientras que antes esta operación también era de subproceso único.</span><span class="sxs-lookup"><span data-stu-id="e264a-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="e264a-125">Las estadísticas de una tabla con optimización de memoria ahora pueden muestrearse y se actualizan de forma automática.</span><span class="sxs-lookup"><span data-stu-id="e264a-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="e264a-126">Consulte [Novedades (motor de base de datos): OLTP en memoria](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para más detalles.</span><span class="sxs-lookup"><span data-stu-id="e264a-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="e264a-127">El modo por lotes frente al modo de fila cambia con los índices de almacenamiento de columnas</span><span class="sxs-lookup"><span data-stu-id="e264a-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="e264a-128">Las ordenaciones en una tabla con un índice de almacenamiento de columnas están ahora en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="e264a-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="e264a-129">Los agregados basados en ventanas operan ahora en modo por lotes, tal como instrucciones de TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="e264a-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="e264a-130">Las consultas en tablas de almacenamiento de columnas con varias cláusulas Distinct funcionan en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="e264a-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="e264a-131">Las consultas que se ejecutan en DOP = 1 o con un plan en serie también se ejecutan en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="e264a-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="e264a-132">Por último, mejoras de estimación de cardinalidad proceden realmente con el nivel de compatibilidad 120, pero para los que ejecutar en una compatibilidad más bajo nivel (es decir, 100 o 110), hello move toocompatibility nivel 130 también aparecerá estas mejoras y los usuarios pueden también mejorar el rendimiento de la consulta de Hola de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e264a-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="e264a-133">Prácticas con el nivel de compatibilidad 130</span><span class="sxs-lookup"><span data-stu-id="e264a-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="e264a-134">Primero vamos a algunas tablas, índices y datos aleatorios creados toopractice algunas de estas nuevas capacidades.</span><span class="sxs-lookup"><span data-stu-id="e264a-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="e264a-135">ejemplos de script de Hola TSQL se pueden ejecutar en SQL Server 2016 o base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e264a-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="e264a-136">Sin embargo, al crear una base de datos de SQL Azure, asegúrese de que elija en el mínimo de hello P2 de base de datos porque necesita al menos un par de núcleos tooallow subprocesamiento múltiple y por lo tanto beneficiarse de estas características.</span><span class="sxs-lookup"><span data-stu-id="e264a-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

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


<span data-ttu-id="e264a-137">Ahora, echemos un toosome del aspecto de las características de procesamiento de consultas de hello procedentes con nivel de compatibilidad 130.</span><span class="sxs-lookup"><span data-stu-id="e264a-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="e264a-138">INSERT en paralelo</span><span class="sxs-lookup"><span data-stu-id="e264a-138">Parallel INSERT</span></span>
<span data-ttu-id="e264a-139">Ejecutar instrucciones de TSQL Hola siguiente ejecuta Hola operación de INSERCIÓN en el nivel de compatibilidad 120 y 130, que ejecuta respectivamente Hola operación de INSERCIÓN en un único modelo de subproceso (120) y en un modelo multiproceso (130).</span><span class="sxs-lookup"><span data-stu-id="e264a-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="e264a-140">Solicitando el plan de consulta de Hola Hola real, examinando su representación gráfica o su contenido XML, puede determinar qué función se encuentra en la reproducción de estimación de cardinalidad.</span><span class="sxs-lookup"><span data-stu-id="e264a-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="e264a-141">Examinando los planes de hello en paralelo en la figura 1, podemos ver claramente que Hola insertar de la tienda en la columna ejecución va de serie en 120 tooparallel en 130.</span><span class="sxs-lookup"><span data-stu-id="e264a-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="e264a-142">Además, tenga en cuenta ese cambio Hola del icono de iterador de hello en plan 130 Hola que muestra dos flechas paralelas, que ilustra el hecho de Hola que ahora Hola ejecución de iterador es realmente paralela.</span><span class="sxs-lookup"><span data-stu-id="e264a-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="e264a-143">Si tiene grande toocomplete de operaciones de INSERCIÓN, Hola la ejecución en paralelo, vinculado toohello número de núcleos que tiene a su disposición para base de datos de hello, llevará a cabo mejor; seguridad tooa 100 veces más rápido dependiendo de su situación.</span><span class="sxs-lookup"><span data-stu-id="e264a-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="e264a-144">*Figura 1: Inserte los cambios de la operación de tooparallel serie con el nivel de compatibilidad 130.*</span><span class="sxs-lookup"><span data-stu-id="e264a-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![En la Ilustración 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="e264a-146">Modo por lotes EN SERIE</span><span class="sxs-lookup"><span data-stu-id="e264a-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="e264a-147">De forma similar, mover el nivel de toocompatibility 130 al procesar las filas de datos permite el procesamiento de modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="e264a-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="e264a-148">En primer lugar, las operaciones en modo por lotes solo están disponibles cuando tenga un índice de almacenamiento de columnas preparado.</span><span class="sxs-lookup"><span data-stu-id="e264a-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="e264a-149">En segundo lugar, un lote que normalmente representa aproximadamente 900 filas y utiliza una lógica de código optimizada para varios núcleos de CPU, un mayor rendimiento de memoria y directamente aprovecha Hola datos comprimidos de hello almacén de columnas siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="e264a-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="e264a-150">En estas condiciones, SQL Server 2016 puede procesar aproximadamente 900 filas a la vez, en lugar de 1 fila en el momento de hello, y en consecuencia, hello coste total general de operación de hello ahora compartida por lote completo de hello, reducir Hola general costo por fila.</span><span class="sxs-lookup"><span data-stu-id="e264a-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="e264a-151">Esta cantidad de operaciones combinadas con compresión de almacén de columnas de hello básicamente compartida reduce la latencia de hello implicada en una operación de modo por lotes SELECT.</span><span class="sxs-lookup"><span data-stu-id="e264a-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="e264a-152">Puede encontrar más detalles sobre el almacén de columnas de hello y procesar por lotes en el modo en [Guía de índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="e264a-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="e264a-153">Como visible a continuación, mediante la observación de hello consulta planes side-by-side en la figura 2, podemos ver que ha cambiado el modo de procesamiento de hello con nivel de compatibilidad de hello y, en consecuencia, al ejecutar consultas de hello en el nivel de compatibilidad de ambos por completo, podemos ver que la mayoría del tiempo de procesamiento de Hola se invierte en fila modo (86%) en comparación con toohello modo por lotes (14%), donde se han procesado 2 lotes.</span><span class="sxs-lookup"><span data-stu-id="e264a-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="e264a-154">Aumentar el conjunto de datos de hello, hello beneficio aumentará.</span><span class="sxs-lookup"><span data-stu-id="e264a-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="e264a-155">*Figura 2: Seleccione los cambios de operación del modo serie toobatch con nivel de compatibilidad 130.*</span><span class="sxs-lookup"><span data-stu-id="e264a-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Ilustración 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="e264a-157">Modo por lotes en ejecución SORT</span><span class="sxs-lookup"><span data-stu-id="e264a-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="e264a-158">Toohello similar anterior, pero la operación de ordenación aplicada tooa, transición Hola de fila (nivel de compatibilidad 120) toobatch modo (nivel de compatibilidad 130) mejora el rendimiento de Hola de hello operación de ordenación para hello las mismas razones.</span><span class="sxs-lookup"><span data-stu-id="e264a-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="e264a-159">Visible side-by-side en la figura 3, podemos ver que operación de ordenación de hello en el modo de fila representa 81% de hello un costo, mientras que en modo por lotes Hola solo representa 19% del costo de hello (respectivamente 81% y % de 56 en ordenación Hola propio).</span><span class="sxs-lookup"><span data-stu-id="e264a-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="e264a-160">*Figura 3: Operación de ordenación cambia de modo de fila toobatch con nivel de compatibilidad 130.*</span><span class="sxs-lookup"><span data-stu-id="e264a-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Ilustración 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="e264a-162">Evidentemente, estos ejemplos sólo contienen decenas de miles de filas, que es nada cuando se examinan datos Hola disponibles en la mayoría de los servidores SQL de hoy en día.</span><span class="sxs-lookup"><span data-stu-id="e264a-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="e264a-163">Simplemente proyecto estos en millones de filas en su lugar, y esto puede convertir en varios minutos de ejecución ahorran cada día pendiente naturaleza hello de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e264a-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="e264a-164">Mejoras de estimación de cardinalidad (CE)</span><span class="sxs-lookup"><span data-stu-id="e264a-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="e264a-165">Se introdujo con SQL Server 2014, cualquier base de datos que se ejecute en un nivel de compatibilidad 120 o superior hará que el uso de la nueva funcionalidad de estimación de cardinalidad Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="e264a-166">En esencia, estimación de cardinalidad es lógica hello usa toodetermine cómo SQL server ejecutará una consulta basada en su costo estimado.</span><span class="sxs-lookup"><span data-stu-id="e264a-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="e264a-167">estimación de Hola se calcula con la entrada de las estadísticas asociadas con los objetos implicados en la consulta.</span><span class="sxs-lookup"><span data-stu-id="e264a-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="e264a-168">En la práctica, en un alto nivel, las funciones de estimación de cardinalidad son estimaciones de recuento de filas junto con información sobre la distribución de Hola de valores de hello, recuentos de valores distintos, y recuentos duplicados contenidos en Hola tablas y objetos que se hace referencia en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="e264a-169">Obtener estas estimaciones incorrecto, puede provocar la E/S de disco toounnecessary debido concesiones de memoria tooinsufficient (es decir, los volcados de TempDB), o ejecutar, tooname el plan de selección de tooa de la ejecución de un plan en serie a través de un paralelo algunas.</span><span class="sxs-lookup"><span data-stu-id="e264a-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="e264a-170">Conclusión, estimaciones incorrectas pueden provocar tooan degradación del rendimiento general de la ejecución de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="e264a-171">En hello otro lado, mejor las estimaciones, estimaciones más precisas, las ejecuciones de consulta de clientes potenciales toobetter!</span><span class="sxs-lookup"><span data-stu-id="e264a-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="e264a-172">Como se mencionó antes, optimizaciones de consultas y las estimaciones son un asunto complejo, pero si desea más información acerca de los planes de consulta y Estimador de cardinalidad toolearn, puede hacer referencia a documento toohello en [optimizar los planes de consulta con hello SQL Server 2014 Estimador de cardinalidad](https://msdn.microsoft.com/library/dn673537.aspx) para un análisis más profundo.</span><span class="sxs-lookup"><span data-stu-id="e264a-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="e264a-173">¿Qué estimación de cardinalidad está usando actualmente?</span><span class="sxs-lookup"><span data-stu-id="e264a-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="e264a-174">toodetermine bajo qué estimaciones de cardinalidad se ejecutan las consultas, vamos a usar solo la consulta de hello ejemplos a continuación.</span><span class="sxs-lookup"><span data-stu-id="e264a-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="e264a-175">Tenga en cuenta que este primer ejemplo se ejecutará en el nivel de compatibilidad 110, lo que implica el uso de Hola de funciones de estimación de cardinalidad anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="e264a-176">Una vez completada la ejecución, haga clic en el vínculo XML de Hola y examine las propiedades de Hola de iterador primera Hola tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e264a-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="e264a-177">Nombre de la propiedad de nota Hola llama CardinalityEstimationModelVersion actualmente establecido en 70.</span><span class="sxs-lookup"><span data-stu-id="e264a-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="e264a-178">Eso no significa que nivel de compatibilidad de base de datos de Hola se establece la versión de SQL Server 7.0 toohello (se establece en 110 como visible en las instrucciones de TSQL Hola anteriores), pero valor Hola 70 simplemente representa la funcionalidad de estimación de cardinalidad heredada de hello disponible desde SQL Server 7.0, que no tenía ningún revisiones principales hasta que SQL Server 2014 (que se incluye con un nivel de compatibilidad de 120).</span><span class="sxs-lookup"><span data-stu-id="e264a-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="e264a-179">*Figura 4: Hola CardinalityEstimationModelVersion se establece too70 cuando se usa un nivel de compatibilidad de 110 o inferior.*</span><span class="sxs-lookup"><span data-stu-id="e264a-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Ilustración 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="e264a-181">Como alternativa, puede cambiar too130 de nivel de compatibilidad de Hola y deshabilitar el uso de Hola de función de hello nueva estimación de cardinalidad mediante el uso de hello LEGACY_CARDINALITY_ESTIMATION establecer tooON con [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="e264a-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="e264a-182">Esto se puede exactamente Hola igual que utilizando 110 desde un punto de vista de la función de estimación de cardinalidad, mientras que usa el nivel de compatibilidad de procesamiento de consultas más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="e264a-183">De esta forma, puede beneficiarse de nuevas con el nivel de compatibilidad más reciente de hello (es decir, el modo por lotes) características de procesamiento de consultas nuevo de hello, pero aun así, delegar en la funcionalidad de estimación de cardinalidad anterior Hola si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e264a-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="e264a-184">Mover simplemente toohello de nivel de compatibilidad 120 o 130 habilita la funcionalidad de estimación de cardinalidad nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="e264a-185">En tal caso, el predeterminado hello CardinalityEstimationModelVersion se establecerá en consecuencia too120 o 130 como visible.</span><span class="sxs-lookup"><span data-stu-id="e264a-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="e264a-186">*Figura 5: Hola CardinalityEstimationModelVersion se establece too130 cuando se usa un nivel de compatibilidad de 130.*</span><span class="sxs-lookup"><span data-stu-id="e264a-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Ilustración 5.](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="e264a-188">Diferencias de estimación de cardinalidad de Hola que hayan presenciado</span><span class="sxs-lookup"><span data-stu-id="e264a-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="e264a-189">Ahora, vamos a ejecutar ligeramente más complejo que implica una operación INNER JOIN con una cláusula WHERE con algunos de los predicados de consulta y echemos un vistazo a Hola estimación del recuento de filas en función de estimación de cardinalidad anterior hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="e264a-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="e264a-190">Para ejecutar esta consulta eficazmente devuelve 200.704 filas, mientras la estimación de la fila de hello con funcionalidad de estimación de cardinalidad anterior Hola notificaciones 194,284 filas.</span><span class="sxs-lookup"><span data-stu-id="e264a-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="e264a-191">Obviamente, como hemos comentado, estos resultados de recuento de filas también dependerán de la frecuencia con ejecutó Hola ejemplos anteriores, que rellena las tablas de ejemplo de Hola y otra vez en cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="e264a-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="e264a-192">Obviamente, los predicados de hello en la consulta también tendrá una influencia en la estimación real de hello excepto en forma de tabla de hello, el contenido de datos y cómo estos datos realmente correlación entre sí.</span><span class="sxs-lookup"><span data-stu-id="e264a-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="e264a-193">*Figura 6: estimación del recuento de filas Hola procede 194,284 o 6.000 filas desactivar 200.704 filas Hola esperado.*</span><span class="sxs-lookup"><span data-stu-id="e264a-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Ilustración 6.](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="e264a-195">Hola igual, vamos a ejecutar ahora Hola misma consulta con la nueva funcionalidad de estimación de cardinalidad Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="e264a-196">Examinando Hola a continuación, se pueden ver que el cálculo de esa fila de hello es 202,877, o mucho más cercano y superiores a Hola estimación de cardinalidad anterior.</span><span class="sxs-lookup"><span data-stu-id="e264a-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="e264a-197">*Figura 7: estimación del recuento de filas Hola ahora es 202,877, en lugar de 194,284.*</span><span class="sxs-lookup"><span data-stu-id="e264a-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Ilustración 7.](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="e264a-199">En realidad, el conjunto de resultados de hello es 200.704 filas (pero completamente depende de la frecuencia con ejecutó ejemplos anteriores de consultas Hola de hello, pero es más importante, porque Hola TSQL utiliza la instrucción de RAND() hello, devueltos los valores reales Hola pueden variar desde una toohello de ejecución junto).</span><span class="sxs-lookup"><span data-stu-id="e264a-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="e264a-200">Por consiguiente, en este ejemplo concreto, hello nueva estimación de cardinalidad no más eficaces al calcular el número de Hola de filas porque 202,877 es mucho más cerca de too200, 704, que 194,284!</span><span class="sxs-lookup"><span data-stu-id="e264a-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="e264a-201">Por último, si cambia hello tooequality de predicados de la cláusula WHERE (en lugar de ">" por ejemplo), esto podría realizar estimaciones de hello entre Hola antigua y nueva función de cardinalidad incluso más diferentes, dependiendo de cuántas coincidencias que puedas.</span><span class="sxs-lookup"><span data-stu-id="e264a-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="e264a-202">En este caso, una diferencia de aproximadamente 6000 filas con respecto recuento real, en algunas situaciones no representa una gran cantidad de datos.</span><span class="sxs-lookup"><span data-stu-id="e264a-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="e264a-203">Ahora, transponer este toomillions de filas a través de varias tablas y consultas más complejas, y en ocasiones Hola estimación puede ser incorrecta millones de filas y por lo tanto, Hola a riesgo de Hola de selección de seguridad incorrecto de plan de ejecución, o la solicitud de memoria insuficiente concede inicial los volcados de tooTempDB y por lo que más i/OS, son mucho mayores.</span><span class="sxs-lookup"><span data-stu-id="e264a-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="e264a-204">Si tiene la oportunidad de hello, esta comparación con las consultas más frecuentes y los conjuntos de datos de procedimientos y descubrir por sí mismo cuánto algunas de las estimaciones nuevos y antiguos de Hola se ven afectados, mientras que algunos simplemente dejen de estar más desactivado en realidad de Hola o algunos otros simplemente Cuanto más se acerque toohello real de la fila cuenta realmente devueltos en los conjuntos de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="e264a-205">Completamente dependerán de la forma de Hola de consultas, las características de base de datos de SQL Azure Hola, naturaleza Hola y tamaño de Hola de conjuntos de datos y estadísticas de hello disponibles sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="e264a-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="e264a-206">Si acaba de crear la instancia de base de datos de SQL Azure, realice una consulta de hello optimizador tendrá toobuild ejecuta su conocimiento desde cero en lugar de reutilizar las estadísticas formadas consulta anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="e264a-207">Por lo tanto, las estimaciones de hello son situación de servidor y la aplicación de tooevery muy contextuales y casi específico.</span><span class="sxs-lookup"><span data-stu-id="e264a-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="e264a-208">Es un tookeep aspecto importante en mente.</span><span class="sxs-lookup"><span data-stu-id="e264a-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="e264a-209">Algunos tootake consideraciones en cuenta</span><span class="sxs-lookup"><span data-stu-id="e264a-209">Some considerations tootake into account</span></span>
<span data-ttu-id="e264a-210">Aunque la mayoría de las cargas de trabajo se beneficiarían de nivel de compatibilidad de hello 130, antes de la adopción de nivel de compatibilidad de hello para el entorno de producción, básicamente tiene 3 opciones:</span><span class="sxs-lookup"><span data-stu-id="e264a-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="e264a-211">Mover el nivel de toocompatibility 130 y vea cómo realizan cosas.</span><span class="sxs-lookup"><span data-stu-id="e264a-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="e264a-212">En caso de que observe algunas regresiones, simplemente establezca tooits atrás de hello compatibilidad nivel nivel original, o mantener 130 y sólo invertir modo heredado de hello estimación de cardinalidad toohello back-(como se explicó anteriormente, esto solo podría solucionar Hola problema).</span><span class="sxs-lookup"><span data-stu-id="e264a-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="e264a-213">Probar exhaustivamente las aplicaciones existentes en la carga de producción similares, ajustar y validar el rendimiento de hello antes de ir tooproduction.</span><span class="sxs-lookup"><span data-stu-id="e264a-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="e264a-214">En el caso de problemas, igual que el anterior, puede siempre volver atrás toohello nivel de compatibilidad original, o simplemente invertir modo heredado de hello estimación de cardinalidad toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="e264a-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="e264a-215">Como última opción y Hola tooaddress más reciente de manera estas preguntas, es el almacén de consultas de hello tooleverage.</span><span class="sxs-lookup"><span data-stu-id="e264a-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="e264a-216">Esta es la opción recomendada en este momento.</span><span class="sxs-lookup"><span data-stu-id="e264a-216">That’s today’s recommended option!</span></span> <span data-ttu-id="e264a-217">análisis de hello tooassist de las consultas con la compatibilidad con nivel 120 o por debajo frente a 130, no le recomendamos suficiente toouse almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="e264a-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="e264a-218">Almacén de consultas está disponible con la versión más reciente de Hola de V12 de base de datos de SQL Azure, y está diseñada toohelp, con la solución de problemas de rendimiento de consulta.</span><span class="sxs-lookup"><span data-stu-id="e264a-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="e264a-219">Considerar Hola almacén de consultas como una caja negra de datos para la base de datos, recopilar y presentar información histórica detallada sobre todas las consultas.</span><span class="sxs-lookup"><span data-stu-id="e264a-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="e264a-220">En gran medida Esto simplifica el análisis forense de rendimiento reduciendo Hola tiempo toodiagnose y resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="e264a-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="e264a-221">Puede encontrar más información en [A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)(Una caja negra para la base de datos).</span><span class="sxs-lookup"><span data-stu-id="e264a-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="e264a-222">En alto nivel, si ya tiene un conjunto de bases de datos que se ejecuta en el nivel de compatibilidad 120 o por debajo y planear toomove Hola algunas de ellas too130, o porque la carga de trabajo aprovisionar automáticamente nuevas bases de datos que se va convertirse establecido por too130 de manera predeterminada, considere la posibilidad de siguiente Hello:</span><span class="sxs-lookup"><span data-stu-id="e264a-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="e264a-223">Antes de cambiar toohello nuevo nivel de compatibilidad en producción, habilite el almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="e264a-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="e264a-224">Puede hacer referencia demasiado[cambiar el almacén de consultas de Hola de modo de compatibilidad de base de datos y el uso hello](https://msdn.microsoft.com/library/bb895281.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e264a-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="e264a-225">A continuación, pruebe todas estas cargas de trabajo con datos representativos y las consultas de un entorno de producción similar y compare el rendimiento de hello experimentó así como información proporcionada por el almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="e264a-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="e264a-226">Si se producen algunas regresiones, puede identificar Hola consultas devueltas con hello almacén de consultas y usar la opción de almacén de consultas de forzado de plan de hello (también conocido como plan de anclaje).</span><span class="sxs-lookup"><span data-stu-id="e264a-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="e264a-227">En tal caso, definitivamente permanecerá con el nivel de compatibilidad de hello 130 y utilizar el plan de consulta anterior de hello tal como se sugiere por hello almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="e264a-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="e264a-228">Si desea tooleverage nuevas características y funcionalidad de la base de datos de SQL de Azure (que se está ejecutando SQL Server 2016), pero son confidenciales toochanges pone el nivel de compatibilidad de hello 130, como último recurso, podría considerar la posibilidad de forzar el nivel de compatibilidad Hola nivel de toohello que se ajuste a la carga de trabajo mediante el uso de una instrucción ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="e264a-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="e264a-229">Pero en primer lugar, tenga en cuenta ese plan de almacén de consultas de hello fijar opción es la mejor opción porque no utiliza 130 básicamente se mantiene en el nivel de funcionalidad de Hola de una versión anterior de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e264a-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="e264a-230">Si tiene aplicaciones para varios inquilinos que abarcan varias bases de datos, es posible hello tooupdate necesarios aprovisionamiento lógica de su tooensure de bases de datos un nivel de compatibilidad coherente en todas las bases de datos; los antiguos y recién suministrados.</span><span class="sxs-lookup"><span data-stu-id="e264a-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="e264a-231">El rendimiento de carga de trabajo de la aplicación podría ser hechos toohello confidenciales que algunas bases de datos se ejecutan en los niveles de compatibilidad diferentes, y por lo tanto, podría ser necesaria la coherencia de nivel de compatibilidad a través de cualquier base de datos en orden tooprovide Hola igual experiencia de clientes tooyour todo en el tablero de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="e264a-232">Tenga en cuenta que no es obligatorio, realmente depende de cómo su aplicación se ve afectada por el nivel de compatibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="e264a-233">Por último, con respecto a la estimación de cardinalidad de hello y, como cambiar el nivel de compatibilidad de hello, antes de continuar en producción, es recomendable tootest la carga de trabajo de producción en hello nuevas condiciones toodetermine si su aplicación se beneficia de mejoras de estimación de cardinalidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e264a-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e264a-234">Conclusión</span><span class="sxs-lookup"><span data-stu-id="e264a-234">Conclusion</span></span>
<span data-ttu-id="e264a-235">Uso de base de datos de SQL Azure toobenefit de todas las mejoras de SQL Server 2016 puede mejorar claramente las ejecuciones de la consulta.</span><span class="sxs-lookup"><span data-stu-id="e264a-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="e264a-236">Así de simple.</span><span class="sxs-lookup"><span data-stu-id="e264a-236">Just as-is!</span></span> <span data-ttu-id="e264a-237">Por supuesto, como ocurre con cualquier característica nueva, una evaluación adecuada debe realizarse en la que la carga de trabajo de la base de datos funciona Hola mejor condiciones toodetermine Hola exactas.</span><span class="sxs-lookup"><span data-stu-id="e264a-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="e264a-238">Experiencia muestra que la mayoría de la carga de trabajo son tooat esperado menos ejecutan de forma transparente en el nivel de compatibilidad 130, mientras aprovecha las funciones y la nueva estimación de cardinalidad de procesamiento de consultas nuevas.</span><span class="sxs-lookup"><span data-stu-id="e264a-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="e264a-239">Que dice, de forma realista, siempre hay algunas excepciones y realizar vencimiento apropiado diligencia es un toodetermine de evaluación importante cuánto puede beneficiarse de estas mejoras.</span><span class="sxs-lookup"><span data-stu-id="e264a-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="e264a-240">Y una vez más, almacén de consultas de Hola de puede ser de gran ayuda para realizar este trabajo.</span><span class="sxs-lookup"><span data-stu-id="e264a-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="e264a-241">Medida que evoluciona SQL Azure, puede esperar un nivel de compatibilidad 140 Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="e264a-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="e264a-242">Cuando el momento sea apropiado, empezaremos a hablar de lo que aportará este futuro nivel de compatibilidad 140, igual que hemos explicado brevemente aquí lo que el nivel de compatibilidad 130 aporta hoy.</span><span class="sxs-lookup"><span data-stu-id="e264a-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="e264a-243">Por ahora, no se olvide, a partir de junio de 2016, base de datos de SQL Azure dejará nivel de compatibilidad de saludo predeterminado de 120 too130 para bases de datos recién creadas.</span><span class="sxs-lookup"><span data-stu-id="e264a-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="e264a-244">¡Prepárese!</span><span class="sxs-lookup"><span data-stu-id="e264a-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="e264a-245">Referencias</span><span class="sxs-lookup"><span data-stu-id="e264a-245">References</span></span>
* [<span data-ttu-id="e264a-246">Novedades (motor de base de datos)</span><span class="sxs-lookup"><span data-stu-id="e264a-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="e264a-247">Blog: Query Store: A flight data recorder for your database (Almacén de consultas: Una caja negra para la base de datos) por Borko Novakovic, 8 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="e264a-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="e264a-248">Nivel de compatibilidad de ALTER TABLE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="e264a-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="e264a-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="e264a-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="e264a-250">Compatibility Level 130 for Azure SQL Database V12</span><span class="sxs-lookup"><span data-stu-id="e264a-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="e264a-251">Optimizar los planes de consulta con hello Estimador de cardinalidad de SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e264a-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="e264a-252">Descripción de los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="e264a-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="e264a-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database (Rendimiento mejorado de consultas con el nivel de compatibilidad 130 en Base de datos SQL de Azure) por Alain Lissoir, 6 de mayo de 2016</span><span class="sxs-lookup"><span data-stu-id="e264a-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
