---
title: "tablas de aaaDistributing en el almacén de datos de SQL | Documentos de Microsoft"
description: "Introducción a la distribución de tablas en Almacenamiento de datos SQL de Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="b5961-103">Distribución de tablas en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="b5961-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b5961-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="b5961-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b5961-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="b5961-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="b5961-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="b5961-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="b5961-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="b5961-107">[Index][Index]</span></span>
> * <span data-ttu-id="b5961-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="b5961-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="b5961-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="b5961-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="b5961-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="b5961-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="b5961-111">El Almacenamiento de datos SQL es un sistema de base de datos distribuidas de procesamiento masivo en paralelo (MPP).</span><span class="sxs-lookup"><span data-stu-id="b5961-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="b5961-112">Al dividir los datos y la funcionalidad de procesamiento entre varios nodos, Almacenamiento de datos SQL puede ofrecer una gran escalabilidad, mucha más que cualquier sistema individual.</span><span class="sxs-lookup"><span data-stu-id="b5961-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="b5961-113">Decidir cómo toodistribute sus datos en el almacenamiento de datos de SQL están uno de los más importantes de hello factores tooachieving un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="b5961-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="b5961-114">rendimiento de Hello toooptimal clave es la minimización de movimiento de datos y a su vez el movimiento de datos de clave toominimizing hello es seleccionando estrategia de distribución adecuada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="b5961-115">Descripción del movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="b5961-115">Understanding data movement</span></span>
<span data-ttu-id="b5961-116">En un sistema MPP, datos de saludo de cada tabla se dividen entre varias bases de datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="b5961-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="b5961-117">las consultas de Hello más optimizado en un sistema MPP simplemente se pueden pasar a través de tooexecute Hola individuales bases de datos distribuidas sin interacción entre Hola otras bases de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="b5961-118">Por ejemplo, supongamos que tiene una base de datos con datos de ventas que contiene dos tablas, ventas y clientes.</span><span class="sxs-lookup"><span data-stu-id="b5961-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="b5961-119">Si tiene una consulta que necesite toojoin la tabla de clientes de tooyour de tabla de ventas y divide tanto los sales y las tablas de cliente de por número de cliente, colocar a cada cliente en una base de datos independiente, las consultas que unir ventas y el cliente se pueden resolver dentro de cada uno base de datos con ningún conocimiento de Hola a otras bases de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="b5961-120">En cambio, si divide los datos de ventas por número de pedido y los datos de clientes por número de cliente, a continuación, una base de datos no tendrá datos correspondientes de Hola para cada cliente y, por tanto, si deseara toojoin los datos de clientes de tooyour de datos de ventas, necesitará tooget Hola datos para cada cliente de hello otras bases de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="b5961-121">En este segundo ejemplo, el movimiento de datos necesitaría toooccur toomove Hola cliente datos toohello datos de ventas, para que se pueden combinar Hola dos tablas.</span><span class="sxs-lookup"><span data-stu-id="b5961-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="b5961-122">Movimiento de datos no es algo malo, a veces resulta necesario toosolve una consulta.</span><span class="sxs-lookup"><span data-stu-id="b5961-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="b5961-123">Pero si se puede evitar este paso adicional, evidentemente la consulta se ejecutará más rápido.</span><span class="sxs-lookup"><span data-stu-id="b5961-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="b5961-124">El movimiento de los datos surge normalmente cuando se unen tablas o se realizan agregaciones.</span><span class="sxs-lookup"><span data-stu-id="b5961-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="b5961-125">En muchos casos deberá toodo ambos, por lo que aunque es posible que pueda toooptimize para un escenario, como una combinación, que todavía necesita toohelp de movimiento de datos puede resolver para Hola otro escenario, como una agregación.</span><span class="sxs-lookup"><span data-stu-id="b5961-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="b5961-126">El truco de Hello es pensar en que es menos trabajo.</span><span class="sxs-lookup"><span data-stu-id="b5961-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="b5961-127">En la mayoría de los casos, distribuir grandes tablas de hechos en una columna frecuentemente combinada es Hola método más eficaz para reducir hello más movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="b5961-128">Distribución de los datos en columnas de combinación es un movimiento de datos de tooreduce método mucho más habitual de distribución de los datos en las columnas que intervienen en una agregación.</span><span class="sxs-lookup"><span data-stu-id="b5961-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="b5961-129">Selección del método de distribución</span><span class="sxs-lookup"><span data-stu-id="b5961-129">Select distribution method</span></span>
<span data-ttu-id="b5961-130">Entre bastidores de hello, almacenamiento de datos SQL divide los datos en bases de datos de 60.</span><span class="sxs-lookup"><span data-stu-id="b5961-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="b5961-131">Cada base de datos es que se hace referencia tooas una **distribución**.</span><span class="sxs-lookup"><span data-stu-id="b5961-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="b5961-132">Cuando se cargan datos en cada tabla, almacenamiento de datos de SQL tiene tooknow cómo toodivide los datos a través de las distribuciones de 60.</span><span class="sxs-lookup"><span data-stu-id="b5961-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="b5961-133">método de distribución de Hello se define en el nivel de tabla de Hola y actualmente hay dos opciones:</span><span class="sxs-lookup"><span data-stu-id="b5961-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="b5961-134">**Round Robin** , que distribuye los datos de manera uniforme, pero aleatoria.</span><span class="sxs-lookup"><span data-stu-id="b5961-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="b5961-135">**Distribuido por hash** , que distribuye datos en función de los valores de hash de una sola columna</span><span class="sxs-lookup"><span data-stu-id="b5961-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="b5961-136">De forma predeterminada, si no se define un método de distribución de datos, la tabla se distribuirán mediante hello **round-robin** método de distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="b5961-137">Sin embargo, se vuelven más sofisticadas en su implementación, deberá usar tooconsider **hash distribuida** toominimize el movimiento de datos que a su vez optimizará el rendimiento de las consultas de tablas.</span><span class="sxs-lookup"><span data-stu-id="b5961-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="b5961-138">Tablas Round Robin</span><span class="sxs-lookup"><span data-stu-id="b5961-138">Round Robin Tables</span></span>
<span data-ttu-id="b5961-139">Uso de hello método Round Robin de distribución de datos es demasiado cómo suena.</span><span class="sxs-lookup"><span data-stu-id="b5961-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="b5961-140">Medida que se cargan los datos, cada fila se envía simplemente toohello siguiente distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="b5961-141">Este método de distribución de los datos de hello siempre distribuirá aleatoriamente datos Hola muy uniformemente entre todas las distribuciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="b5961-142">No es decir, no existe ninguna ordenación done durante Hola round robin proceso que coloca los datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="b5961-143">Una distribución round robin a veces se denomina hash aleatorio por este motivo.</span><span class="sxs-lookup"><span data-stu-id="b5961-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="b5961-144">Con una tabla distribuida round robin no hay ningún dato de hello toounderstand necesidad.</span><span class="sxs-lookup"><span data-stu-id="b5961-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="b5961-145">Por este motivo, las tablas Round Robin suelen ser buenos objetivos para la carga.</span><span class="sxs-lookup"><span data-stu-id="b5961-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="b5961-146">De forma predeterminada, si no se selecciona ningún método de distribución, hello método de distribución de round robin se usará.</span><span class="sxs-lookup"><span data-stu-id="b5961-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="b5961-147">Sin embargo, mientras que las tablas de operación por turnos son toouse fácil, porque se distribuyen al azar en sistema Hola significa que el sistema de hello no puede garantizar qué distribución cada fila tiene en.</span><span class="sxs-lookup"><span data-stu-id="b5961-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="b5961-148">Como consecuencia, sistema de Hola a veces es necesario tooinvoke una toobetter de operación de movimiento de datos organizar los datos antes de que puede resolver una consulta.</span><span class="sxs-lookup"><span data-stu-id="b5961-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="b5961-149">Este paso adicional puede ralentizar las consultas.</span><span class="sxs-lookup"><span data-stu-id="b5961-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="b5961-150">Considere el uso de distribución de operación por turnos para la tabla en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="b5961-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="b5961-151">Cuando se empieza como un punto de partida sencillo.</span><span class="sxs-lookup"><span data-stu-id="b5961-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="b5961-152">Si no hay ninguna clave de combinación obvia.</span><span class="sxs-lookup"><span data-stu-id="b5961-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="b5961-153">Si no hay columna buena candidata para distribuir tabla Hola de hash</span><span class="sxs-lookup"><span data-stu-id="b5961-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="b5961-154">Si hello tabla no comparte una clave de combinación común con otras tablas</span><span class="sxs-lookup"><span data-stu-id="b5961-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="b5961-155">Si la combinación de hello es tan importante como otras combinaciones de consulta de Hola</span><span class="sxs-lookup"><span data-stu-id="b5961-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="b5961-156">Cuando la tabla de hello es una tabla de ensayo temporal</span><span class="sxs-lookup"><span data-stu-id="b5961-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="b5961-157">Ambos ejemplos crearán una tabla Round Robin:</span><span class="sxs-lookup"><span data-stu-id="b5961-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="b5961-158">Mientras round-robin es el tipo de tabla de hello predeterminado es explícito en el DDL se considera una práctica recomendada para que las intenciones de Hola de su diseño de la tabla estén tooothers desactive.</span><span class="sxs-lookup"><span data-stu-id="b5961-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="b5961-159">Tablas con distribución por hash</span><span class="sxs-lookup"><span data-stu-id="b5961-159">Hash Distributed Tables</span></span>
<span data-ttu-id="b5961-160">Con un **Hash distribuida** algoritmo toodistribute las tablas pueden mejorar el rendimiento de muchos escenarios reduciendo el movimiento de datos en tiempo de consulta.</span><span class="sxs-lookup"><span data-stu-id="b5961-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="b5961-161">Hash distribuidas tablas son tablas que se dividen entre Hola distribuye las bases de datos usando un algoritmo hash en una sola columna que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="b5961-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="b5961-162">columna de distribución de Hello es lo que determina cómo datos Hola se dividen en las bases de datos distribuidas.</span><span class="sxs-lookup"><span data-stu-id="b5961-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="b5961-163">función de hash de Hello usa Hola distribución columna tooassign filas toodistributions.</span><span class="sxs-lookup"><span data-stu-id="b5961-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="b5961-164">Hola algoritmo hash y la distribución resultante es determinista.</span><span class="sxs-lookup"><span data-stu-id="b5961-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="b5961-165">Es decir Hola mismo valor con hello al mismo tipo de datos usarán tiene toohello misma distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="b5961-166">En este ejemplo se creará una tabla distribuida en id.:</span><span class="sxs-lookup"><span data-stu-id="b5961-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="b5961-167">Selección de la columna de distribución</span><span class="sxs-lookup"><span data-stu-id="b5961-167">Select distribution column</span></span>
<span data-ttu-id="b5961-168">Cuando eliges demasiado**distribuir hash** una tabla, deberá tooselect una columna de distribución individuales.</span><span class="sxs-lookup"><span data-stu-id="b5961-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="b5961-169">Al seleccionar una columna de distribución, hay tres tooconsider de los factores más importantes.</span><span class="sxs-lookup"><span data-stu-id="b5961-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="b5961-170">Seleccione una sola columna que:</span><span class="sxs-lookup"><span data-stu-id="b5961-170">Select a single column which will:</span></span>

1. <span data-ttu-id="b5961-171">No se actualizará</span><span class="sxs-lookup"><span data-stu-id="b5961-171">Not be updated</span></span>
2. <span data-ttu-id="b5961-172">Distribuirá los datos uniformemente, con lo que se evita la asimetría de datos</span><span class="sxs-lookup"><span data-stu-id="b5961-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="b5961-173">Reducirá el movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="b5961-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="b5961-174">Selección de una columna de distribución que no se actualizará</span><span class="sxs-lookup"><span data-stu-id="b5961-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="b5961-175">Las columnas de distribución no se pueden actualizar; por lo tanto, seleccione una columna con valores estáticos.</span><span class="sxs-lookup"><span data-stu-id="b5961-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="b5961-176">Si una columna tendrá toobe actualizado, por lo general no resulta un candidato bueno de distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="b5961-177">Si hay un caso donde debe actualizar una columna de distribución, puede hacerlo eliminando primero fila hello y, a continuación, insertar una fila nueva.</span><span class="sxs-lookup"><span data-stu-id="b5961-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="b5961-178">Selección de una columna que distribuirá los datos de manera uniforme</span><span class="sxs-lookup"><span data-stu-id="b5961-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="b5961-179">Ya que un sistema distribuido realiza solo tan rápido como su distribución más lenta, es importante toodivide Hola trabajo uniformemente a través de las distribuciones de hello en orden tooachieve equilibrada ejecución todo sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="b5961-180">forma de Hola Hola trabajo se divide en un sistema distribuido se basa en donde residen los datos de Hola para cada distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="b5961-181">Esto facilita columna de distribución adecuada de hello tooselect muy importante para distribuir los datos de Hola para que cada distribución tiene trabajo igual y se toman Hola mismo toocomplete tiempo su parte del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="b5961-182">Cuando también se divide el trabajo en todo el sistema de Hola, datos Hola se equilibra entre las distribuciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="b5961-183">Cuando los datos no están equilibrados de manera uniforme, se conoce como **asimetría de datos**.</span><span class="sxs-lookup"><span data-stu-id="b5961-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="b5961-184">datos toodivide uniformemente y evitar el sesgo de datos, considere la siguiente Hola al seleccionar la columna de distribución:</span><span class="sxs-lookup"><span data-stu-id="b5961-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="b5961-185">Seleccione una columna que contenga un importante número de valores distintos.</span><span class="sxs-lookup"><span data-stu-id="b5961-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="b5961-186">Evite la distribución de los datos en las columnas con unos pocos valores distintivos.</span><span class="sxs-lookup"><span data-stu-id="b5961-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="b5961-187">Evite la distribución de los datos en las columnas con una alta frecuencia de valores NULL.</span><span class="sxs-lookup"><span data-stu-id="b5961-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="b5961-188">Evite la distribución de datos en columnas de fecha.</span><span class="sxs-lookup"><span data-stu-id="b5961-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="b5961-189">Dado que cada valor es too1 con hash de 60 distribuciones, distribución uniforme tooachieve le interesará tooselect una columna que es muy único y contiene más de 60 valores únicos.</span><span class="sxs-lookup"><span data-stu-id="b5961-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="b5961-190">tooillustrate, considere un caso donde una columna solamente tiene 40 valores únicos.</span><span class="sxs-lookup"><span data-stu-id="b5961-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="b5961-191">Si se ha seleccionado esta columna como clave de distribución de hello, datos de Hola para esa tabla llegaría en 40 distribuciones a lo sumo, dejando 20 distribuciones con ningún dato y no toodo de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="b5961-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="b5961-192">Por el contrario, hello otras 40 distribuciones tendría más toodo de trabajo que, si hello datos se distribuye uniformemente las distribuciones de más de 60.</span><span class="sxs-lookup"><span data-stu-id="b5961-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="b5961-193">Este escenario es un ejemplo de la asimetría de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="b5961-194">En el sistema MPP, cada paso de consulta espera toocomplete de todas las distribuciones su cuota de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="b5961-195">Si está realizando más trabajo que Hola otros distribución, Hola recursos de hello otras distribuciones que básicamente se pierde esperando en distribución ocupado Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="b5961-196">Si el trabajo no se distribuye de manera uniforme en todas las distribuciones, se denomina una **asimetría de procesamiento**.</span><span class="sxs-lookup"><span data-stu-id="b5961-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="b5961-197">Sesgo de procesamiento provocará toorun de las consultas más lenta que si carga de trabajo de hello puede se distribuyen uniformemente entre las distribuciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="b5961-198">Sesgo de datos dará lugar tooprocessing sesgado.</span><span class="sxs-lookup"><span data-stu-id="b5961-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="b5961-199">Evitar la distribución en la columna admite valores NULL alta como valores null de hello todos llegará a Hola mismo distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="b5961-200">Distribuir en una columna de fecha puede hacer procesamiento sesgo porque todos los datos de una fecha específica llegará a Hola mismo distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="b5961-201">Si varios usuarios ejecutan filtradas todas las consultas en hello misma fecha, a continuación, solo 1 de 60 distribuciones de Hola a realizar todo el trabajo de hello como una fecha determinada sólo estará en una distribución.</span><span class="sxs-lookup"><span data-stu-id="b5961-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="b5961-202">En este escenario, las consultas de hello es probable que se ejecutarán 60 veces más lentas que si datos Hola se distribuye equitativamente sobre todas las distribuciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="b5961-203">Cuando no existe ninguna columna de buena candidata, considere la posibilidad de usar round robin como método de distribución de hello.</span><span class="sxs-lookup"><span data-stu-id="b5961-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="b5961-204">Selección de una columna de distribución que minimizará el movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="b5961-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="b5961-205">Minimizar el movimiento de datos mediante la selección de columna de distribución adecuada de Hola es una de las estrategias más importantes de Hola para optimizar el rendimiento de su almacén de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="b5961-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="b5961-206">El movimiento de los datos surge normalmente cuando se unen tablas o se realizan agregaciones.</span><span class="sxs-lookup"><span data-stu-id="b5961-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="b5961-207">Las columnas usadas en las cláusulas `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` y `HAVING` son todas **buenas** candidatas para la distribución por hash.</span><span class="sxs-lookup"><span data-stu-id="b5961-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="b5961-208">Hola en otra parte, las columnas de hello `WHERE` cláusula realice **no** realizar para los candidatos de la columna de hash correcto porque limitar que las distribuciones participan en la consulta de hello, que produce el procesamiento de sesgado.</span><span class="sxs-lookup"><span data-stu-id="b5961-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="b5961-209">Un buen ejemplo de una columna que podría ser tentador toodistribute en, pero a menudo puede causar este procesamiento sesgo es una columna de fecha.</span><span class="sxs-lookup"><span data-stu-id="b5961-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="b5961-210">Por lo general, si tiene dos tablas de hechos de gran tamaño suelen incluirse en una combinación, dispondrá de hello máximo rendimiento mediante la distribución de ambas tablas en una de las columnas de combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="b5961-211">Si tiene una tabla que nunca se tooanother Unidos a un tabla de hechos de gran tamaño, a continuación, busque toocolumns que son a menudo en hello `GROUP BY` cláusula.</span><span class="sxs-lookup"><span data-stu-id="b5961-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="b5961-212">Hay unos criterios clave que deben ser tooavoid cumpla el movimiento de datos durante una combinación:</span><span class="sxs-lookup"><span data-stu-id="b5961-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="b5961-213">Hello tablas involucradas en la combinación de hello deben ser hash distribuida en **una** de columnas de Hola que participan en la combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="b5961-214">tipos de datos de Hola Hola de columnas de combinación deben coincidir entre las dos tablas.</span><span class="sxs-lookup"><span data-stu-id="b5961-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="b5961-215">columnas de Hello deben combinarse con un operador es igual a.</span><span class="sxs-lookup"><span data-stu-id="b5961-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="b5961-216">Hello tipo de combinación no sea un `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="b5961-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="b5961-217">Solución de problemas de asimetría de datos</span><span class="sxs-lookup"><span data-stu-id="b5961-217">Troubleshooting data skew</span></span>
<span data-ttu-id="b5961-218">Cuando los datos de la tabla se distribuyen mediante el método de distribución de hash de hello hay una posibilidad de que algunas distribuciones será sesgado toohave desproporcionadamente más datos que otras personas.</span><span class="sxs-lookup"><span data-stu-id="b5961-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="b5961-219">Exceso sesgo de datos pueden afectar al rendimiento de consulta dado resultado final de Hola de una consulta distribuida debe esperar a que toofinish de distribución de ejecución más larga de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="b5961-220">Lo dependiendo de grado de Hola de datos de hello sesgo que tendrá que tooaddress.</span><span class="sxs-lookup"><span data-stu-id="b5961-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="b5961-221">Identificación de la asimetría</span><span class="sxs-lookup"><span data-stu-id="b5961-221">Identifying skew</span></span>
<span data-ttu-id="b5961-222">Un tooidentify de forma sencilla una tabla como sesgado es toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="b5961-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="b5961-223">Se trata de una forma muy rápida y sencilla toosee Hola número de filas de tabla que se almacenan en cada una de las distribuciones de hello 60 de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="b5961-224">Recuerde que para obtener un rendimiento más equilibrada de hello, filas de hello en la tabla distribuida se deben distribuir uniformemente en todas las distribuciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="b5961-225">Sin embargo, si consulta las vistas de administración dinámica de almacenamiento de datos de SQL Azure hello (DMV) puede realizar un análisis más detallado.</span><span class="sxs-lookup"><span data-stu-id="b5961-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="b5961-226">toostart, crear vista de hello [dbo.vTableSizes] [ dbo.vTableSizes] ver con Hola SQL desde [información general de la tabla] [ Overview] artículo.</span><span class="sxs-lookup"><span data-stu-id="b5961-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="b5961-227">Una vez que se crea la vista de hello, ejecute este tooidentify consulta las tablas que tienen más de sesgo de datos de 10%.</span><span class="sxs-lookup"><span data-stu-id="b5961-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="b5961-228">Resolución de la asimetría de datos</span><span class="sxs-lookup"><span data-stu-id="b5961-228">Resolving data skew</span></span>
<span data-ttu-id="b5961-229">No todos los sesgado es suficiente toowarrant una corrección.</span><span class="sxs-lookup"><span data-stu-id="b5961-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="b5961-230">En algunos casos, rendimiento de Hola de una tabla en algunas consultas puede sobrepasar daños Hola de sesgo de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="b5961-231">toodecide si debe resolver los datos de sesgo en una tabla, debe comprender tanto como sea posible sobre los volúmenes de datos de Hola y consultas en la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b5961-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="b5961-232">Toolook unidireccional en el impacto de Hola de sesgo es toouse pasos Hola Hola [consulta supervisión] [ Query Monitoring] artículo impacto de hello toomonitor de sesgo en el rendimiento de las consultas y específicamente Hola consultas largas toohow de impacto Tome toocomplete distribuciones individuales Hola.</span><span class="sxs-lookup"><span data-stu-id="b5961-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="b5961-233">Distribución de los datos consiste en buscar el equilibrio adecuado de hello entre reducir al mínimo el sesgo de datos y minimizar el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="b5961-234">Estos pueden ser opuestas objetivos y a veces es conveniente tookeep datos sesgo en el movimiento de datos de tooreduce de orden.</span><span class="sxs-lookup"><span data-stu-id="b5961-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="b5961-235">Por ejemplo, cuando Hola distribución columna es con frecuencia Hola compartida de combinaciones y agregaciones, se puede minimizar movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="b5961-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="b5961-236">Hello ventaja de tener el movimiento de datos mínima Hola puede contrarrestar impacto de Hola de contar con datos de sesgo.</span><span class="sxs-lookup"><span data-stu-id="b5961-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="b5961-237">forma habitual de Hello sesgo de datos de tooresolve es toore-crear tabla de hello con una columna de distribución diferente.</span><span class="sxs-lookup"><span data-stu-id="b5961-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="b5961-238">Dado que no hay ninguna manera de columna de distribución de hello toochange en otra distribución de tablas, Hola forma toochange Hola de una tabla se toorecreate con un [] [CTAS].</span><span class="sxs-lookup"><span data-stu-id="b5961-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="b5961-239">Estos son dos ejemplos de cómo resolver la asimetría de datos:</span><span class="sxs-lookup"><span data-stu-id="b5961-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="b5961-240">Ejemplo 1: Volver a crear la tabla de hello con una nueva columna de distribución</span><span class="sxs-lookup"><span data-stu-id="b5961-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="b5961-241">Este ejemplo utiliza [CTAS] [] toore-crear una tabla con una columna de distribución de hash diferente.</span><span class="sxs-lookup"><span data-stu-id="b5961-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="b5961-242">Ejemplo 2: Volver a crear la tabla Hola usando la distribución de operación por turnos</span><span class="sxs-lookup"><span data-stu-id="b5961-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="b5961-243">Este ejemplo utiliza [CTAS] [] toore-crear una tabla con operación por turnos en lugar de una distribución de hash.</span><span class="sxs-lookup"><span data-stu-id="b5961-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="b5961-244">Este cambio producirá la distribución de datos incluso en el costo de Hola de movimiento de datos mayor.</span><span class="sxs-lookup"><span data-stu-id="b5961-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="b5961-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5961-245">Next steps</span></span>
<span data-ttu-id="b5961-246">toolearn más información acerca del diseño de tabla, vea hello [distribuir][Distribute], [índice][Index], [partición] [ Partition], [Tipos de datos][Data Types], [estadísticas] [ Statistics] y [tablas temporales] [ Temporary] artículos.</span><span class="sxs-lookup"><span data-stu-id="b5961-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="b5961-247">Para acceder a información general sobre los procedimientos recomendados, vea [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="b5961-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
