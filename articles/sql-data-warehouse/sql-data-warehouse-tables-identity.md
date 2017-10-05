---
title: "Creación de claves suplentes mediante IDENTIDAD | Microsoft Docs"
description: Aprenda a usar IDENTIDAD para crear claves suplentes en las tablas.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 3ab5d159e6eaeb830135fe134e108b0e4de4b7d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="df00c-103">Creación de claves suplentes mediante IDENTITY</span><span class="sxs-lookup"><span data-stu-id="df00c-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="df00c-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="df00c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="df00c-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="df00c-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="df00c-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="df00c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="df00c-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="df00c-107">[Index][Index]</span></span>
> * <span data-ttu-id="df00c-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="df00c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="df00c-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="df00c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="df00c-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="df00c-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="df00c-111">[Identidad][Identity]</span><span class="sxs-lookup"><span data-stu-id="df00c-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="df00c-112">A muchos modeladores de datos les gusta crear claves suplentes en las tablas cuando diseñan modelos de almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="df00c-112">Many data modelers like to create surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="df00c-113">Puede usar la propiedad IDENTITY para lograr este objetivo de manera sencilla y eficaz sin afectar al rendimiento de carga.</span><span class="sxs-lookup"><span data-stu-id="df00c-113">You can use the IDENTITY property to achieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="df00c-114">Introducción a IDENTITY</span><span class="sxs-lookup"><span data-stu-id="df00c-114">Get started with IDENTITY</span></span>
<span data-ttu-id="df00c-115">Puede definir una tabla que tenga la propiedad IDENTITY al crear la tabla mediante una sintaxis similar a la de la siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="df00c-115">You can define a table as having the IDENTITY property when you first create the table by using syntax that is similar to the following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="df00c-116">Luego puede usar `INSERT..SELECT` para rellenar la tabla.</span><span class="sxs-lookup"><span data-stu-id="df00c-116">You can then use `INSERT..SELECT` to populate the table.</span></span>

## <a name="behavior"></a><span data-ttu-id="df00c-117">Comportamiento</span><span class="sxs-lookup"><span data-stu-id="df00c-117">Behavior</span></span>
<span data-ttu-id="df00c-118">La propiedad IDENTITY está diseñada para escalar horizontalmente en todas las distribuciones de almacenamiento de datos sin afectar al rendimiento de carga.</span><span class="sxs-lookup"><span data-stu-id="df00c-118">The IDENTITY property is designed to scale out across all the distributions in the data warehouse without affecting load performance.</span></span> <span data-ttu-id="df00c-119">Por consiguiente, la implementación de IDENTITY está orientada a la consecución de estos objetivos.</span><span class="sxs-lookup"><span data-stu-id="df00c-119">Therefore, the implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="df00c-120">En esta sección se resaltan los matices de la implementación para ayudarle a comprenderlos de manera más completa.</span><span class="sxs-lookup"><span data-stu-id="df00c-120">This section highlights the nuances of the implementation to help you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="df00c-121">Asignación de valores</span><span class="sxs-lookup"><span data-stu-id="df00c-121">Allocation of values</span></span>
<span data-ttu-id="df00c-122">La propiedad IDENTITY no garantiza el orden en que se asignan las claves suplentes, lo que refleja el comportamiento de SQL Server y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="df00c-122">The IDENTITY property doesn't guarantee the order in which the surrogate values are allocated, which reflects the behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="df00c-123">Pero, en Azure SQL Data Warehouse, la ausencia de garantías es más marcada.</span><span class="sxs-lookup"><span data-stu-id="df00c-123">However, in Azure SQL Data Warehouse, the absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="df00c-124">El ejemplo siguiente sirve de muestra:</span><span class="sxs-lookup"><span data-stu-id="df00c-124">The following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="df00c-125">En el ejemplo anterior, dos filas quedaron en la distribución 1.</span><span class="sxs-lookup"><span data-stu-id="df00c-125">In the preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="df00c-126">La primera fila tiene el valor suplente de 1 en la columna `C1` y la segunda fila tiene el valor suplente de 61.</span><span class="sxs-lookup"><span data-stu-id="df00c-126">The first row has the surrogate value of 1 in column `C1`, and the second row has the surrogate value of 61.</span></span> <span data-ttu-id="df00c-127">Estos dos valores se generaron con la propiedad IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-127">Both of these values were generated by the IDENTITY property.</span></span> <span data-ttu-id="df00c-128">Pero la asignación de los valores no es contigua.</span><span class="sxs-lookup"><span data-stu-id="df00c-128">However, the allocation of the values is not contiguous.</span></span> <span data-ttu-id="df00c-129">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="df00c-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="df00c-130">Datos sesgados</span><span class="sxs-lookup"><span data-stu-id="df00c-130">Skewed data</span></span> 
<span data-ttu-id="df00c-131">El intervalo de valores del tipo de datos se reparte uniformemente entre las distribuciones.</span><span class="sxs-lookup"><span data-stu-id="df00c-131">The range of values for the data type are spread evenly across the distributions.</span></span> <span data-ttu-id="df00c-132">Si una tabla distribuida adolece de datos sesgados, el intervalo de valores disponible para el tipo de datos se puede agotar antes de tiempo.</span><span class="sxs-lookup"><span data-stu-id="df00c-132">If a distributed table suffers from skewed data, then the range of values available to the datatype can be exhausted prematurely.</span></span> <span data-ttu-id="df00c-133">Por ejemplo, si todos los datos terminan en una sola distribución, en la práctica, la tabla tiene acceso a únicamente la sexta parte de los valores del tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="df00c-133">For example, if all the data ends up in a single distribution, then effectively the table has access to only one-sixtieth of the values of the data type.</span></span> <span data-ttu-id="df00c-134">Por este motivo, la propiedad IDENTITY se limita exclusivamente a los tipos de datos `INT` y `BIGINT`.</span><span class="sxs-lookup"><span data-stu-id="df00c-134">For this reason, the IDENTITY property is limited to `INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="df00c-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="df00c-135">SELECT..INTO</span></span>
<span data-ttu-id="df00c-136">Cuando se selecciona una columna IDENTITY existente en una nueva tabla, la nueva columna hereda la propiedad IDENTITY, a no ser que se cumpla alguna de las siguientes condiciones:</span><span class="sxs-lookup"><span data-stu-id="df00c-136">When an existing IDENTITY column is selected into a new table, the new column inherits the IDENTITY property, unless one of the following conditions is true:</span></span>
- <span data-ttu-id="df00c-137">La instrucción SELECT contiene una combinación.</span><span class="sxs-lookup"><span data-stu-id="df00c-137">The SELECT statement contains a join.</span></span>
- <span data-ttu-id="df00c-138">Varias instrucciones SELECT se combinan mediante UNION.</span><span class="sxs-lookup"><span data-stu-id="df00c-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="df00c-139">La columna IDENTITY aparece más de una vez en la lista de SELECT.</span><span class="sxs-lookup"><span data-stu-id="df00c-139">The IDENTITY column is listed more than one time in the SELECT list.</span></span>
- <span data-ttu-id="df00c-140">La columna IDENTITY forma parte de una expresión.</span><span class="sxs-lookup"><span data-stu-id="df00c-140">The IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="df00c-141">Si ninguna de estas condiciones se cumple, la columna se crea como NOT NULL en lugar de heredar la propiedad IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-141">If any one of these conditions is true, the column is created NOT NULL instead of inheriting the IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="df00c-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="df00c-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="df00c-143">CREATE TABLE AS SELECT (CTAS) sigue el mismo comportamiento de SQL Server que se documenta para SELECT..INTO.</span><span class="sxs-lookup"><span data-stu-id="df00c-143">CREATE TABLE AS SELECT (CTAS) follows the same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="df00c-144">Pero no se puede especificar una propiedad IDENTITY en la definición de columna de la parte `CREATE TABLE` de la instrucción.</span><span class="sxs-lookup"><span data-stu-id="df00c-144">However, you can't specify an IDENTITY property in the column definition of the `CREATE TABLE` part of the statement.</span></span> <span data-ttu-id="df00c-145">Tampoco se puede usar la función IDENTITY en la parte `SELECT` de la CTAS.</span><span class="sxs-lookup"><span data-stu-id="df00c-145">You also can't use the IDENTITY function in the `SELECT` part of the CTAS.</span></span> <span data-ttu-id="df00c-146">Para rellenar una tabla, hay que usar `CREATE TABLE` para definir la tabla seguido de `INSERT..SELECT` para rellenarla.</span><span class="sxs-lookup"><span data-stu-id="df00c-146">To populate a table, you need to use `CREATE TABLE` to define the table followed by `INSERT..SELECT` to populate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="df00c-147">Inserción explícita de valores en una columna IDENTITY</span><span class="sxs-lookup"><span data-stu-id="df00c-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="df00c-148">SQL Data Warehouse admite la sintaxis `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="df00c-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="df00c-149">Puede usarse esta sintaxis para insertar valores explícitamente en la columna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-149">You can use this syntax to explicitly insert values into the IDENTITY column.</span></span>

<span data-ttu-id="df00c-150">A muchos modeladores de datos les gusta usar valores negativos predefinidos para determinadas filas en las dimensiones.</span><span class="sxs-lookup"><span data-stu-id="df00c-150">Many data modelers like to use predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="df00c-151">Un ejemplo es el valor -1 de la fila de "miembro desconocido".</span><span class="sxs-lookup"><span data-stu-id="df00c-151">An example is the -1 or "unknown member" row.</span></span> 

<span data-ttu-id="df00c-152">En el siguiente script se muestra cómo agregar explícitamente esta fila mediante SET IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="df00c-152">The next script shows how to explicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="df00c-153">Carga de datos en una tabla con IDENTITY</span><span class="sxs-lookup"><span data-stu-id="df00c-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="df00c-154">La presencia de la propiedad IDENTITY tiene algunas implicaciones en el código de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="df00c-154">The presence of the IDENTITY property has some implications to your data-loading code.</span></span> <span data-ttu-id="df00c-155">En esta sección se resaltan algunos patrones básicos para cargar datos en tablas mediante IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="df00c-156">Carga de datos con PolyBase</span><span class="sxs-lookup"><span data-stu-id="df00c-156">Load data with PolyBase</span></span>
<span data-ttu-id="df00c-157">Para cargar datos en una tabla y generar una clave suplente mediante IDENTITY, cree la tabla y use INSERT..SELECT o INSERT..VALUES para realizar la carga.</span><span class="sxs-lookup"><span data-stu-id="df00c-157">To load data into a table and generate a surrogate key by using IDENTITY, create the table and then use INSERT..SELECT or INSERT..VALUES to perform the load.</span></span>

<span data-ttu-id="df00c-158">En el siguiente ejemplo se resalta el patrón básico:</span><span class="sxs-lookup"><span data-stu-id="df00c-158">The following example highlights the basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT to populate the table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="df00c-159">Actualmente no se puede usar `CREATE TABLE AS SELECT` al cargar datos en una tabla con una columna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-159">It's not possible to use `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="df00c-160">Para más información sobre cómo cargar datos mediante la herramienta programa de copia masiva (BCP), vea los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="df00c-160">For more information on loading data by using the bulk copy program (BCP) tool, see the following articles:</span></span>

- <span data-ttu-id="df00c-161">[Carga con PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="df00c-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="df00c-162">[Procedimientos recomendados para PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="df00c-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="df00c-163">Carga de datos con BCP</span><span class="sxs-lookup"><span data-stu-id="df00c-163">Load data with BCP</span></span>
<span data-ttu-id="df00c-164">BCP es una herramienta de línea de comandos que se puede usar para cargar datos en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df00c-164">BCP is a command-line tool that you can use to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="df00c-165">Uno de sus parámetros (-E) controla el comportamiento de BCP al cargar datos en una tabla con una columna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-165">One of its parameters (-E) controls the behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="df00c-166">Cuando se especifica -E, se conservan los valores contenidos en el archivo de entrada para la columna con IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-166">When -E is specified, the values held in the input file for the column with IDENTITY are retained.</span></span> <span data-ttu-id="df00c-167">Si -E *no* se especifica, se omiten los valores de esta columna.</span><span class="sxs-lookup"><span data-stu-id="df00c-167">If -E is *not* specified, then the values in this column are ignored.</span></span> <span data-ttu-id="df00c-168">Si no se incluye la columna IDENTITY, los datos se cargan con normalidad.</span><span class="sxs-lookup"><span data-stu-id="df00c-168">If the identity column is not included, then the data is loaded as normal.</span></span> <span data-ttu-id="df00c-169">Los valores se generan según la política de inicialización e incremento de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="df00c-169">The values are generated according to the increment and seed policy of the property.</span></span>

<span data-ttu-id="df00c-170">Para más información sobre cómo cargar datos mediante BCP, vea los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="df00c-170">For more information on loading data by using BCP, see the following articles:</span></span>

- <span data-ttu-id="df00c-171">[Carga con BCP][]</span><span class="sxs-lookup"><span data-stu-id="df00c-171">[Load with BCP][]</span></span>
- <span data-ttu-id="df00c-172">[BCP en MSDN][]</span><span class="sxs-lookup"><span data-stu-id="df00c-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="df00c-173">Vistas de catálogo</span><span class="sxs-lookup"><span data-stu-id="df00c-173">Catalog views</span></span>
<span data-ttu-id="df00c-174">SQL Data Warehouse admite la vista de catálogo `sys.identity_columns`.</span><span class="sxs-lookup"><span data-stu-id="df00c-174">SQL Data Warehouse supports the `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="df00c-175">Esta vista puede usarse para identificar una columna que tiene la propiedad IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-175">This view can be used to identify a column that has the IDENTITY property.</span></span>

<span data-ttu-id="df00c-176">Para ayudarle a comprender mejor el esquema de la base de datos, en este ejemplo se muestra cómo integrar `sys.identity_columns` con otras vistas de catálogo del sistema:</span><span class="sxs-lookup"><span data-stu-id="df00c-176">To help you better understand the database schema, this example shows how to integrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="df00c-177">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="df00c-177">Limitations</span></span>
<span data-ttu-id="df00c-178">La propiedad IDENTITY no se puede usar en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="df00c-178">The IDENTITY property can't be used in the following scenarios:</span></span>
- <span data-ttu-id="df00c-179">Cuando el tipo de datos de la columna no es INT ni BIGINT</span><span class="sxs-lookup"><span data-stu-id="df00c-179">Where the column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="df00c-180">Cuando la columna es también la clave de distribución</span><span class="sxs-lookup"><span data-stu-id="df00c-180">Where the column is also the distribution key</span></span>
- <span data-ttu-id="df00c-181">Cuando la tabla es una tabla externa</span><span class="sxs-lookup"><span data-stu-id="df00c-181">Where the table is an external table</span></span> 

<span data-ttu-id="df00c-182">No se admiten las siguientes funciones relacionadas en SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="df00c-182">The following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="df00c-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="df00c-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="df00c-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="df00c-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="df00c-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="df00c-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="df00c-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="df00c-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="df00c-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="df00c-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="df00c-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="df00c-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="df00c-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="df00c-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="df00c-190">Tareas</span><span class="sxs-lookup"><span data-stu-id="df00c-190">Tasks</span></span>

<span data-ttu-id="df00c-191">En esta sección se ofrecen algunos ejemplos de código que se pueden usar para realizar tareas comunes al trabajar con columnas IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="df00c-191">This section provides some sample code you can use to perform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="df00c-192">La columna C1 es la de IDENTITY en todas las tareas siguientes.</span><span class="sxs-lookup"><span data-stu-id="df00c-192">Column C1 is the IDENTITY in all the following tasks.</span></span>
> 
 
### <a name="find-the-highest-allocated-value-for-a-table"></a><span data-ttu-id="df00c-193">Búsqueda del valor más alto asignado en una tabla</span><span class="sxs-lookup"><span data-stu-id="df00c-193">Find the highest allocated value for a table</span></span>
<span data-ttu-id="df00c-194">Use la función `MAX()` para determinar el valor más alto asignado en una tabla distribuida:</span><span class="sxs-lookup"><span data-stu-id="df00c-194">Use the `MAX()` function to determine the highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-the-seed-and-increment-for-the-identity-property"></a><span data-ttu-id="df00c-195">Búsqueda del valor de inicialización e incremento de la propiedad IDENTITY</span><span class="sxs-lookup"><span data-stu-id="df00c-195">Find the seed and increment for the IDENTITY property</span></span>
<span data-ttu-id="df00c-196">Puede usar las vistas de catálogo para detectar los valores de configuración de inicialización e incremento de identidad en una tabla mediante la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="df00c-196">You can use the catalog views to discover the identity increment and seed configuration values for a table by using the following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="df00c-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df00c-197">Next steps</span></span>

* <span data-ttu-id="df00c-198">Para obtener más información sobre el desarrollo de tablas, vea [Introducción a las tablas][Overview], [Tipos de datos de tabla][Data Types], [Distribución de tablas][Distribute], [Indexación de tablas][Index], [Creación de particiones de tabla][Partition] y [Tablas temporales][Temporary].</span><span class="sxs-lookup"><span data-stu-id="df00c-198">To learn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="df00c-199">Para más información sobre los procedimientos recomendados, vea [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="df00c-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<span data-ttu-id="df00c-200">[Carga con BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span><span class="sxs-lookup"><span data-stu-id="df00c-200">[Load with bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span></span>
<span data-ttu-id="df00c-201">[Carga con PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span><span class="sxs-lookup"><span data-stu-id="df00c-201">[Load with PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span></span>
<span data-ttu-id="df00c-202">[Procedimientos recomendados para PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span><span class="sxs-lookup"><span data-stu-id="df00c-202">[PolyBase best practices]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span></span>


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
<span data-ttu-id="df00c-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span></span>
<span data-ttu-id="df00c-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span></span>
<span data-ttu-id="df00c-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span></span>
<span data-ttu-id="df00c-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span></span>
<span data-ttu-id="df00c-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span></span>
<span data-ttu-id="df00c-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span></span>
<span data-ttu-id="df00c-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span></span>

<span data-ttu-id="df00c-210">[BCP en MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span><span class="sxs-lookup"><span data-stu-id="df00c-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span></span>
  

<!--Other Web references-->  
