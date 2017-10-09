---
title: OLTP aaaIn memoria mejora el rendimiento de transacciones SQL | Documentos de Microsoft
description: OLTP en memoria de adoptar tooimprove performance de las transacciones en una base de datos SQL existente.
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="85bed-103">Use In-Memory OLTP tooimprove el rendimiento de la aplicación en la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="85bed-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="85bed-104">[OLTP en memoria](sql-database-in-memory.md) puede ser usado tooimprove Hola rendimiento de procesamiento de transacciones, recopilación de datos y los escenarios de datos transitorios, en [Premium](sql-database-service-tiers.md) Hola a bases de datos de SQL de Azure sin aumentar el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="85bed-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="85bed-105">Más información sobre cómo [Quorum duplica cargas de trabajo clave de las bases de datos a la vez que reduce las DTU en un 70 % con SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="85bed-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="85bed-106">Siga estos pasos tooadopt OLTP en memoria en la base de datos existente.</span><span class="sxs-lookup"><span data-stu-id="85bed-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="85bed-107">Paso 1: Asegúrese de estar utilizando una base de datos premium</span><span class="sxs-lookup"><span data-stu-id="85bed-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="85bed-108">OLTP en memoria solo se admite en bases de datos premium.</span><span class="sxs-lookup"><span data-stu-id="85bed-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="85bed-109">Se admite en memoria si Hola devuelve el resultado es 1 (no 0):</span><span class="sxs-lookup"><span data-stu-id="85bed-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="85bed-110">*XTP* son las siglas de *Extreme Transaction Processing*.</span><span class="sxs-lookup"><span data-stu-id="85bed-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="85bed-111">Paso 2: Identificar objetos de toomigrate tooIn memoria OLTP</span><span class="sxs-lookup"><span data-stu-id="85bed-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="85bed-112">SSMS incluye un informe de **información general del análisis de rendimiento de transacciones** que se pueden ejecutar en una base de datos con una carga de trabajo activo.</span><span class="sxs-lookup"><span data-stu-id="85bed-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="85bed-113">informe de Hello identifica las tablas y procedimientos almacenados que son candidatos para la migración de OLTP tooIn memoria.</span><span class="sxs-lookup"><span data-stu-id="85bed-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="85bed-114">En SSMS, informe de Hola toogenerate:</span><span class="sxs-lookup"><span data-stu-id="85bed-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="85bed-115">Hola **Explorador de objetos**, haga clic en el nodo de base de datos.</span><span class="sxs-lookup"><span data-stu-id="85bed-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="85bed-116">Haga clic en **Informes** > **Informes estándar** > **Información general de análisis de rendimiento de transacciones**.</span><span class="sxs-lookup"><span data-stu-id="85bed-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="85bed-117">Para obtener más información, consulte [determinar si una tabla o un procedimiento almacenado debe ser pasar OLTP de memoria tooIn](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="85bed-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="85bed-118">Paso 3: Crear una base de datos de prueba comparables</span><span class="sxs-lookup"><span data-stu-id="85bed-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="85bed-119">Imagine que informe de hello indica la base de datos ha una tabla que se beneficiaría de la que se va a convertir tabla optimizada en memoria de tooa.</span><span class="sxs-lookup"><span data-stu-id="85bed-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="85bed-120">Le recomendamos que pruebe en primer lugar indicación de hello tooconfirm probando.</span><span class="sxs-lookup"><span data-stu-id="85bed-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="85bed-121">Necesitará una copia de prueba de la base de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="85bed-121">You need a test copy of your production database.</span></span> <span data-ttu-id="85bed-122">Hello base de datos de prueba debe ser en hello mismo nivel de servicio como la base de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="85bed-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="85bed-123">tooease probar, ajustar la base de datos de prueba como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="85bed-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="85bed-124">Conectar la base de datos de prueba de toohello mediante SSMS.</span><span class="sxs-lookup"><span data-stu-id="85bed-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="85bed-125">tooavoid necesidad Hola opción WITH (SNAPSHOT) en las consultas, establezca la opción de base de datos de hello como se muestra en hello después de la instrucción T-SQL:</span><span class="sxs-lookup"><span data-stu-id="85bed-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="85bed-126">Paso 4: Migrar tablas</span><span class="sxs-lookup"><span data-stu-id="85bed-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="85bed-127">Debe crear y rellenar una copia con optimización para memoria de tabla Hola desea tootest.</span><span class="sxs-lookup"><span data-stu-id="85bed-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="85bed-128">Se puede crear mediante:</span><span class="sxs-lookup"><span data-stu-id="85bed-128">You can create it by using either:</span></span>

* <span data-ttu-id="85bed-129">Hola práctica Asistente de optimización de memoria en SSMS.</span><span class="sxs-lookup"><span data-stu-id="85bed-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="85bed-130">T-SQL manual.</span><span class="sxs-lookup"><span data-stu-id="85bed-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="85bed-131">Asistente para optimización de memoria en SSMS</span><span class="sxs-lookup"><span data-stu-id="85bed-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="85bed-132">toouse esta opción de migración:</span><span class="sxs-lookup"><span data-stu-id="85bed-132">toouse this migration option:</span></span>

1. <span data-ttu-id="85bed-133">Conectar la base de datos de prueba de toohello con SSMS.</span><span class="sxs-lookup"><span data-stu-id="85bed-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="85bed-134">Hola **Explorador de objetos**, haga doble clic en la tabla de hello y, a continuación, haga clic en **Memory Optimization Advisor**.</span><span class="sxs-lookup"><span data-stu-id="85bed-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="85bed-135">Hola **Asistente de optimizador de memoria de tablas** se muestra el asistente.</span><span class="sxs-lookup"><span data-stu-id="85bed-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="85bed-136">En el Asistente de hello, haga clic en **validación migración** (o hello **siguiente** botón) toosee si tabla hello tiene alguna no admite características que no se admiten en tablas optimizadas en memoria.</span><span class="sxs-lookup"><span data-stu-id="85bed-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="85bed-137">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="85bed-137">For more information, see:</span></span>
   
   * <span data-ttu-id="85bed-138">Hola *lista de comprobación de optimización de memoria* en [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="85bed-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="85bed-139">[Construcciones de transact-SQL no admitidas por In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="85bed-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="85bed-140">[Migrar OLTP de memoria tooIn](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="85bed-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="85bed-141">Si Hola tabla no tiene ninguna característica no admitida, Asesor de hello puede realizar esquema real de Hola y migración de datos.</span><span class="sxs-lookup"><span data-stu-id="85bed-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="85bed-142">T-SQL manual</span><span class="sxs-lookup"><span data-stu-id="85bed-142">Manual T-SQL</span></span>
<span data-ttu-id="85bed-143">toouse esta opción de migración:</span><span class="sxs-lookup"><span data-stu-id="85bed-143">toouse this migration option:</span></span>

1. <span data-ttu-id="85bed-144">Conectar la base de datos de prueba de tooyour mediante SSMS (o una utilidad similar).</span><span class="sxs-lookup"><span data-stu-id="85bed-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="85bed-145">Obtenga el script de T-SQL completo de hello para la tabla y sus índices.</span><span class="sxs-lookup"><span data-stu-id="85bed-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="85bed-146">En SSMS, haga clic con el botón derecho en el nodo de tabla.</span><span class="sxs-lookup"><span data-stu-id="85bed-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="85bed-147">Haga clic en **Incluir tabla como** > **Crear en** > **Nueva ventana de consulta**.</span><span class="sxs-lookup"><span data-stu-id="85bed-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="85bed-148">En la ventana de script de Hola, agregue WITH (MEMORY_OPTIMIZED = ON) toohello instrucción CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="85bed-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="85bed-149">Si hay un índice agrupado, cámbielo tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="85bed-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="85bed-150">Cambiar el nombre de tabla existente de hello mediante SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="85bed-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="85bed-151">Crear copia optimizadas en memoria nueva Hola de tabla de Hola ejecutando el script CREATE TABLE editado.</span><span class="sxs-lookup"><span data-stu-id="85bed-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="85bed-152">Copiar la tabla optimizada en memoria de hello datos tooyour mediante INSERT... SELECCIONE * EN:</span><span class="sxs-lookup"><span data-stu-id="85bed-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="85bed-153">Paso 5 (opcional): Migrar los procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="85bed-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="85bed-154">característica de Hello en memoria también puede modificar un procedimiento almacenado para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="85bed-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="85bed-155">Consideraciones con procedimientos almacenados compilados de forma nativa</span><span class="sxs-lookup"><span data-stu-id="85bed-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="85bed-156">Un procedimiento almacenado compilado de forma nativa debe tener Hola siguientes opciones en su cláusula T-SQL con:</span><span class="sxs-lookup"><span data-stu-id="85bed-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="85bed-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="85bed-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="85bed-158">SCHEMABINDING: tablas de significado que Hola procedimiento almacenado no pueden tener sus definiciones de columna cambia de cualquier forma que afectaría al procedimiento almacenado de hello, a menos que se coloque el procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="85bed-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="85bed-159">Un módulo nativo debe usar un gran [bloque ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para la administración de transacciones.</span><span class="sxs-lookup"><span data-stu-id="85bed-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="85bed-160">No hay ningún rol para una instrucción BEGIN TRANSACTION o ROLLBACK TRANSACTION explícita.</span><span class="sxs-lookup"><span data-stu-id="85bed-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="85bed-161">Si el código detecta una infracción de una regla de negocios, puede finalizar el bloque atomic Hola con un [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instrucción.</span><span class="sxs-lookup"><span data-stu-id="85bed-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="85bed-162">CREATE PROCEDURE típico para compilar de forma nativa</span><span class="sxs-lookup"><span data-stu-id="85bed-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="85bed-163">Hola T-SQL toocreate un procedimiento almacenado compilado de forma nativa suele ser similar toohello después de plantilla:</span><span class="sxs-lookup"><span data-stu-id="85bed-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="85bed-164">Para hello TRANSACTION_ISOLATION_LEVEL, instantánea es procedimiento más habitual de valor para hello compilado de forma nativa almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="85bed-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="85bed-165">Sin embargo, un subconjunto de Hola otros valores también se admiten:</span><span class="sxs-lookup"><span data-stu-id="85bed-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="85bed-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="85bed-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="85bed-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="85bed-167">SERIALIZABLE</span></span>
* <span data-ttu-id="85bed-168">Hola valor de idioma debe estar presente en la vista de sys.languages Hola.</span><span class="sxs-lookup"><span data-stu-id="85bed-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="85bed-169">¿Cómo toomigrate un procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="85bed-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="85bed-170">pasos de migración de Hello son:</span><span class="sxs-lookup"><span data-stu-id="85bed-170">hello migration steps are:</span></span>

1. <span data-ttu-id="85bed-171">Obtener Hola CREATE PROCEDURE script toohello procedimiento almacenado interpretado normal.</span><span class="sxs-lookup"><span data-stu-id="85bed-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="85bed-172">Vuelva a escribir su plantilla anterior de encabezado toomatch Hola.</span><span class="sxs-lookup"><span data-stu-id="85bed-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="85bed-173">Determinar si el procedimiento de hello almacenado código T-SQL utiliza las características que no se admiten para los procedimientos almacenados compilados de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="85bed-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="85bed-174">Implemente soluciones alternativas si es necesario.</span><span class="sxs-lookup"><span data-stu-id="85bed-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="85bed-175">Para obtener información detallada, consulte [Problemas de migración para los procedimientos almacenados compilados de forma nativa](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="85bed-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="85bed-176">Cambiar el nombre de procedimiento almacenado antiguo de hello mediante SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="85bed-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="85bed-177">O bien, simplemente quítelo con la instrucción DROP.</span><span class="sxs-lookup"><span data-stu-id="85bed-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="85bed-178">Ejecute el script CREATE PROCEDURE T-SQL editado.</span><span class="sxs-lookup"><span data-stu-id="85bed-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="85bed-179">Paso 6: Ejecutar la carga de trabajo en la prueba</span><span class="sxs-lookup"><span data-stu-id="85bed-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="85bed-180">Ejecutar una carga de trabajo en la base de datos de prueba de la carga de trabajo de toohello similares que se ejecuta en la base de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="85bed-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="85bed-181">Esto debería aclarar mejora del rendimiento Hola logrado mediante el uso de la característica de hello en memoria de tablas y procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="85bed-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="85bed-182">Los atributos principales de carga de trabajo de hello son:</span><span class="sxs-lookup"><span data-stu-id="85bed-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="85bed-183">Número de conexiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="85bed-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="85bed-184">Relación de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="85bed-184">Read/write ratio.</span></span>

<span data-ttu-id="85bed-185">tootailor y carga de trabajo de prueba de ejecución hello, considere el uso de la herramienta de práctica ostress.exe hello, que se muestra en [aquí](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="85bed-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="85bed-186">latencia de red toominimize, ejecute la prueba en hello misma región geográfica Azure donde existe la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="85bed-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="85bed-187">Paso 7: Supervisión postimplementación</span><span class="sxs-lookup"><span data-stu-id="85bed-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="85bed-188">Considere la posibilidad de supervisar los efectos en el rendimiento de sus implementaciones en memoria en producción hello:</span><span class="sxs-lookup"><span data-stu-id="85bed-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="85bed-189">[Supervisión del almacenamiento In-Memory](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="85bed-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="85bed-190">Supervisión de Base de datos SQL de Azure con vistas de administración dinámica</span><span class="sxs-lookup"><span data-stu-id="85bed-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="85bed-191">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="85bed-191">Related links</span></span>
* [<span data-ttu-id="85bed-192">In-Memory OLTP (optimización In-Memory)</span><span class="sxs-lookup"><span data-stu-id="85bed-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="85bed-193">Introducción tooNatively Compiled Stored Procedures</span><span class="sxs-lookup"><span data-stu-id="85bed-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="85bed-194">Asesor de optimización en memoria</span><span class="sxs-lookup"><span data-stu-id="85bed-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

