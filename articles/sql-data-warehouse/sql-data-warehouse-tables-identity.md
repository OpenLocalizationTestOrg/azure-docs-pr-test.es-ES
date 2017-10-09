---
title: las claves suplentes de aaaCreate mediante identidad | Documentos de Microsoft
description: "Obtenga información acerca de cómo las claves suplentes de toouse identidad toocreate en las tablas."
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
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="db2fa-103">Creación de claves suplentes mediante IDENTITY</span><span class="sxs-lookup"><span data-stu-id="db2fa-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="db2fa-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="db2fa-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="db2fa-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="db2fa-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="db2fa-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="db2fa-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="db2fa-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="db2fa-107">[Index][Index]</span></span>
> * <span data-ttu-id="db2fa-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="db2fa-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="db2fa-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="db2fa-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="db2fa-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="db2fa-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="db2fa-111">[Identidad][Identity]</span><span class="sxs-lookup"><span data-stu-id="db2fa-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="db2fa-112">Muchos de los modeladores de datos, como las claves suplentes de toocreate en sus tablas cuando diseñan modelos de almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="db2fa-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="db2fa-113">Puede usar tooachieve de propiedad de identidad de hello este objetivo simple y eficaz sin afectar al rendimiento de carga.</span><span class="sxs-lookup"><span data-stu-id="db2fa-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="db2fa-114">Introducción a IDENTITY</span><span class="sxs-lookup"><span data-stu-id="db2fa-114">Get started with IDENTITY</span></span>
<span data-ttu-id="db2fa-115">Puede definir una tabla como con la propiedad de identidad de hello cuando primero crear tabla de hello mediante la sintaxis que sea similar toohello siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="db2fa-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

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

<span data-ttu-id="db2fa-116">A continuación, puede usar `INSERT..SELECT` tabla de hello toopopulate.</span><span class="sxs-lookup"><span data-stu-id="db2fa-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="db2fa-117">Comportamiento</span><span class="sxs-lookup"><span data-stu-id="db2fa-117">Behavior</span></span>
<span data-ttu-id="db2fa-118">Hola propiedad IDENTITY es diseñada tooscale out en todas las distribuciones de Hola Hola almacenamiento de datos sin afectar al rendimiento de carga.</span><span class="sxs-lookup"><span data-stu-id="db2fa-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="db2fa-119">Por lo tanto, la implementación de Hola de identidad es orientada a lograr estos objetivos.</span><span class="sxs-lookup"><span data-stu-id="db2fa-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="db2fa-120">Esta sección resalta los matices de Hola de hello implementación toohelp entienda más completa.</span><span class="sxs-lookup"><span data-stu-id="db2fa-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="db2fa-121">Asignación de valores</span><span class="sxs-lookup"><span data-stu-id="db2fa-121">Allocation of values</span></span>
<span data-ttu-id="db2fa-122">Hola propiedad IDENTITY no garantiza el orden de hello en qué Hola se asignan los valores de suplente, que reflejan el comportamiento de Hola de SQL Server y base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="db2fa-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="db2fa-123">Sin embargo, en el almacén de datos de SQL Azure, ausencia de Hola de garantía es mayor.</span><span class="sxs-lookup"><span data-stu-id="db2fa-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="db2fa-124">Hola siguiente ejemplo es una ilustración:</span><span class="sxs-lookup"><span data-stu-id="db2fa-124">hello following example is an illustration:</span></span>

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

<span data-ttu-id="db2fa-125">En el anterior ejemplo de Hola, dos filas desembarquen en la distribución de 1.</span><span class="sxs-lookup"><span data-stu-id="db2fa-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="db2fa-126">primera fila de Hello tiene el valor de suplente de Hola de 1 en la columna `C1`, y Hola segunda fila tiene el valor de suplente de Hola de 61.</span><span class="sxs-lookup"><span data-stu-id="db2fa-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="db2fa-127">Estos dos valores generados por hello propiedad IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="db2fa-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="db2fa-128">Sin embargo, la asignación de Hola de valores de hello no es contiguo.</span><span class="sxs-lookup"><span data-stu-id="db2fa-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="db2fa-129">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="db2fa-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="db2fa-130">Datos sesgados</span><span class="sxs-lookup"><span data-stu-id="db2fa-130">Skewed data</span></span> 
<span data-ttu-id="db2fa-131">intervalo de Hola de valores de tipo de datos de hello están repartidos por igual entre las distribuciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="db2fa-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="db2fa-132">Si se produce una tabla distribuida de datos sesgados, Hola, a continuación, el intervalo de valores disponibles toohello tipo de datos se puede agotar prematuramente.</span><span class="sxs-lookup"><span data-stu-id="db2fa-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="db2fa-133">Por ejemplo, si todos los datos de hello terminan en una sola distribución, a continuación, eficazmente Hola tabla tiene acceso tooonly sesentavo de uno de los valores de Hola Hola del tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="db2fa-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="db2fa-134">Por esta razón, Hola propiedad de identidad se limita demasiado`INT` y `BIGINT` sólo los tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="db2fa-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="db2fa-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="db2fa-135">SELECT..INTO</span></span>
<span data-ttu-id="db2fa-136">Cuando se selecciona una columna de identidad existente en una tabla nueva, Hola nueva columna hereda propiedades de identidad de hello, a menos que una de hello condiciones siguientes es verdadera:</span><span class="sxs-lookup"><span data-stu-id="db2fa-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="db2fa-137">instrucción SELECT de Hello contiene una combinación.</span><span class="sxs-lookup"><span data-stu-id="db2fa-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="db2fa-138">Varias instrucciones SELECT se combinan mediante UNION.</span><span class="sxs-lookup"><span data-stu-id="db2fa-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="db2fa-139">columna de identidad de Hello aparece más de una vez en la lista de selección de Hola.</span><span class="sxs-lookup"><span data-stu-id="db2fa-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="db2fa-140">columna de identidad de Hello es parte de una expresión.</span><span class="sxs-lookup"><span data-stu-id="db2fa-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="db2fa-141">Si alguna de estas condiciones es true, columna Hola se crea NOT NULL en lugar de heredar la propiedad IDENTITY de Hola.</span><span class="sxs-lookup"><span data-stu-id="db2fa-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="db2fa-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="db2fa-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="db2fa-143">Crear tabla AS seleccione (CTAS) sigue Hola mismo comportamiento SQL Server que se documenta para SELECT... A.</span><span class="sxs-lookup"><span data-stu-id="db2fa-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="db2fa-144">Sin embargo, no se puede especificar una propiedad de identidad en la definición de columna de Hola de hello `CREATE TABLE` forma parte de la instrucción de Hola.</span><span class="sxs-lookup"><span data-stu-id="db2fa-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="db2fa-145">Tampoco puede utilizar función de identidad de hello en hello `SELECT` forma parte de hello CTAS.</span><span class="sxs-lookup"><span data-stu-id="db2fa-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="db2fa-146">toopopulate una tabla, deberá toouse `CREATE TABLE` seguido de la tabla de hello toodefine `INSERT..SELECT` toopopulate lo.</span><span class="sxs-lookup"><span data-stu-id="db2fa-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="db2fa-147">Inserción explícita de valores en una columna IDENTITY</span><span class="sxs-lookup"><span data-stu-id="db2fa-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="db2fa-148">SQL Data Warehouse admite la sintaxis `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="db2fa-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="db2fa-149">Puede usar este sintaxis tooexplicitly insertar los valores en la columna de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="db2fa-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="db2fa-150">Muchos modeladores de datos como toouse predefinidos negativo para ciertos valores de filas en sus dimensiones.</span><span class="sxs-lookup"><span data-stu-id="db2fa-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="db2fa-151">Un ejemplo es Hola -1 o fila de "miembro desconocido".</span><span class="sxs-lookup"><span data-stu-id="db2fa-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="db2fa-152">script de Hola siguiente muestra cómo tooexplicitly agrega esta fila mediante el uso de SET IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="db2fa-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

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

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="db2fa-153">Carga de datos en una tabla con IDENTITY</span><span class="sxs-lookup"><span data-stu-id="db2fa-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="db2fa-154">presencia de Hola de hello propiedad de identidad tiene algún código de carga de datos de tooyour implicaciones.</span><span class="sxs-lookup"><span data-stu-id="db2fa-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="db2fa-155">En esta sección se resaltan algunos patrones básicos para cargar datos en tablas mediante IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="db2fa-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="db2fa-156">Carga de datos con PolyBase</span><span class="sxs-lookup"><span data-stu-id="db2fa-156">Load data with PolyBase</span></span>
<span data-ttu-id="db2fa-157">datos de tooload en una tabla y generar una clave suplente mediante el uso de identidad, crear tabla de hello y, a continuación, utilice INSERT... SELECT o INSERT... VALORES tooperform Hola carga.</span><span class="sxs-lookup"><span data-stu-id="db2fa-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="db2fa-158">Hello en el ejemplo siguiente se resalta patrón básico de hello:</span><span class="sxs-lookup"><span data-stu-id="db2fa-158">hello following example highlights hello basic pattern:</span></span>
 
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

--Use INSERT..SELECT toopopulate hello table from an external table
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
> <span data-ttu-id="db2fa-159">No es posible toouse `CREATE TABLE AS SELECT` actualmente al cargar datos en una tabla con una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="db2fa-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="db2fa-160">Para obtener más información sobre cómo cargar datos mediante el uso de la herramienta de programa de (copia masiva BCP) de copia masiva de hello, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="db2fa-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="db2fa-161">[Carga con PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="db2fa-162">[Procedimientos recomendados para PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="db2fa-163">Carga de datos con BCP</span><span class="sxs-lookup"><span data-stu-id="db2fa-163">Load data with BCP</span></span>
<span data-ttu-id="db2fa-164">BCP es una herramienta de línea de comandos que puede utilizar datos de tooload en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="db2fa-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="db2fa-165">Uno de sus parámetros (-E) controles Hola comportamiento de BCP al cargar datos en una tabla con una columna de identidad.</span><span class="sxs-lookup"><span data-stu-id="db2fa-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="db2fa-166">Cuando se especifica -E, se conservan los valores de hello mantenidos en archivo de entrada de hello para la columna de hello con la identidad.</span><span class="sxs-lookup"><span data-stu-id="db2fa-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="db2fa-167">Si es -E *no* se especifica, se omiten los valores de hello en esta columna.</span><span class="sxs-lookup"><span data-stu-id="db2fa-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="db2fa-168">Si no se incluye la columna de identidad de hello, datos de Hola se cargan con normalidad.</span><span class="sxs-lookup"><span data-stu-id="db2fa-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="db2fa-169">se generan valores de Hello según la directiva de incremento y el valor de inicialización de toohello de propiedad Hola.</span><span class="sxs-lookup"><span data-stu-id="db2fa-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="db2fa-170">Para obtener más información sobre cómo cargar datos mediante la utilidad BCP, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="db2fa-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="db2fa-171">[Carga con BCP][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-171">[Load with BCP][]</span></span>
- <span data-ttu-id="db2fa-172">[BCP en MSDN][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="db2fa-173">Vistas de catálogo</span><span class="sxs-lookup"><span data-stu-id="db2fa-173">Catalog views</span></span>
<span data-ttu-id="db2fa-174">Almacenamiento de datos SQL admite hello `sys.identity_columns` vista de catálogo.</span><span class="sxs-lookup"><span data-stu-id="db2fa-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="db2fa-175">Esta vista puede ser tooidentify usa una columna que tiene la propiedad de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="db2fa-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="db2fa-176">toohelp se comprender mejor el esquema de base de datos de hello, este ejemplo se muestra cómo toointegrate `sys.identity_columns` con otras vistas de catálogo del sistema:</span><span class="sxs-lookup"><span data-stu-id="db2fa-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

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

## <a name="limitations"></a><span data-ttu-id="db2fa-177">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="db2fa-177">Limitations</span></span>
<span data-ttu-id="db2fa-178">Hola propiedad IDENTITY no se puede usar en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="db2fa-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="db2fa-179">En tipo de datos de columna de hello no es INT o BIGINT</span><span class="sxs-lookup"><span data-stu-id="db2fa-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="db2fa-180">Donde la columna de hello también es la clave de distribución de Hola</span><span class="sxs-lookup"><span data-stu-id="db2fa-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="db2fa-181">En la tabla hello es una tabla externa</span><span class="sxs-lookup"><span data-stu-id="db2fa-181">Where hello table is an external table</span></span> 

<span data-ttu-id="db2fa-182">Hola siguientes funciones relacionadas no se admite en el almacén de datos de SQL:</span><span class="sxs-lookup"><span data-stu-id="db2fa-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="db2fa-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="db2fa-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="db2fa-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="db2fa-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="db2fa-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="db2fa-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="db2fa-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="db2fa-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="db2fa-190">Tareas</span><span class="sxs-lookup"><span data-stu-id="db2fa-190">Tasks</span></span>

<span data-ttu-id="db2fa-191">Esta sección proporciona ejemplos de código puede usar tareas comunes de tooperform cuando se trabaja con las columnas de identidad.</span><span class="sxs-lookup"><span data-stu-id="db2fa-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="db2fa-192">Columna C1 es hello identidad Hola todas las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="db2fa-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="db2fa-193">Buscar el valor de hello más alto asignado para una tabla</span><span class="sxs-lookup"><span data-stu-id="db2fa-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="db2fa-194">Hola de uso `MAX()` función toodetermine Hola valor más alto asignado para una tabla distribuida:</span><span class="sxs-lookup"><span data-stu-id="db2fa-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="db2fa-195">Busque Hola inicialización e incremento Hola propiedad IDENTITY</span><span class="sxs-lookup"><span data-stu-id="db2fa-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="db2fa-196">Puede usar Hola catálogo vistas toodiscover Hola identidad de incremento y valor de inicialización de valores de configuración para una tabla mediante Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="db2fa-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="db2fa-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db2fa-197">Next steps</span></span>

* <span data-ttu-id="db2fa-198">toolearn más sobre el desarrollo de tablas, vea [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Una tabla de índice][Index], [crear particiones de una tabla][Partition], y [ Tablas temporales][Temporary].</span><span class="sxs-lookup"><span data-stu-id="db2fa-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="db2fa-199">Para más información sobre los procedimientos recomendados, vea [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="db2fa-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

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

[Carga con BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Carga con PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Procedimientos recomendados para PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP en MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
