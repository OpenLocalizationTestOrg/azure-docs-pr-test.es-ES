---
title: OLTP en memoria mejora el rendimiento de transacciones SQL | Microsoft Docs
description: "Adopción de In-Memory OLTP para mejorar el rendimiento transaccional en una Base de datos SQL ya existente."
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
ms.openlocfilehash: 50eed9aed417778bd497f55e20c8e732fdae9cf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="334fc-103">Use OLTP en memoria para mejorar el rendimiento de las aplicaciones en SQL Database</span><span class="sxs-lookup"><span data-stu-id="334fc-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="334fc-104">[OLTP en memoria](sql-database-in-memory.md) puede utilizarse para mejorar el rendimiento del procesamiento de transacciones, la ingesta de datos y los escenarios de datos transitorios, en instancias [premium](sql-database-service-tiers.md) de Azure SQL Database sin aumentar el plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="334fc-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="334fc-105">Más información sobre cómo [Quorum duplica cargas de trabajo clave de las bases de datos a la vez que reduce las DTU en un 70 % con SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="334fc-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="334fc-106">Siga estos pasos para adoptar In-Memory OLTP en la base de datos existente.</span><span class="sxs-lookup"><span data-stu-id="334fc-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="334fc-107">Paso 1: Asegúrese de estar utilizando una base de datos premium</span><span class="sxs-lookup"><span data-stu-id="334fc-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="334fc-108">OLTP en memoria solo se admite en bases de datos premium.</span><span class="sxs-lookup"><span data-stu-id="334fc-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="334fc-109">Se admite In-Memory si el resultado devuelto es 1 (no 0):</span><span class="sxs-lookup"><span data-stu-id="334fc-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="334fc-110">*XTP* son las siglas de *Extreme Transaction Processing*.</span><span class="sxs-lookup"><span data-stu-id="334fc-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="334fc-111">Paso 2: identificar objetos para migrar a In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="334fc-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="334fc-112">SSMS incluye un informe de **información general del análisis de rendimiento de transacciones** que se pueden ejecutar en una base de datos con una carga de trabajo activo.</span><span class="sxs-lookup"><span data-stu-id="334fc-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="334fc-113">El informe identifica las tablas y los procedimientos almacenados que son candidatos para la migración a In-Memory OLTP.</span><span class="sxs-lookup"><span data-stu-id="334fc-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="334fc-114">En SSMS, para generar el informe:</span><span class="sxs-lookup"><span data-stu-id="334fc-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="334fc-115">En el **Explorador de objetos**, haga clic con el botón derecho en el nodo de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="334fc-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="334fc-116">Haga clic en **Informes** > **Informes estándar** > **Información general de análisis de rendimiento de transacciones**.</span><span class="sxs-lookup"><span data-stu-id="334fc-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="334fc-117">Para obtener más información, consulte [Determinar si una tabla o un procedimiento almacenado se debe pasar a In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="334fc-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="334fc-118">Paso 3: Crear una base de datos de prueba comparables</span><span class="sxs-lookup"><span data-stu-id="334fc-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="334fc-119">Supongamos que el informe indica que la base de datos tiene una tabla que se beneficiaría de convertirse en una tabla optimizada en memoria.</span><span class="sxs-lookup"><span data-stu-id="334fc-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="334fc-120">Se recomienda que la pruebe primero para confirmar la indicación.</span><span class="sxs-lookup"><span data-stu-id="334fc-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="334fc-121">Necesitará una copia de prueba de la base de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="334fc-121">You need a test copy of your production database.</span></span> <span data-ttu-id="334fc-122">La base de datos de prueba debe estar en el mismo nivel de servicio que la base de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="334fc-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="334fc-123">Para facilitar las pruebas, ajuste la base de datos de prueba de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="334fc-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="334fc-124">Conéctese a la base de datos de prueba con SSMS.</span><span class="sxs-lookup"><span data-stu-id="334fc-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="334fc-125">Para evitar la necesidad de usar la opción WITH (SNAPSHOT) en las consultas, establezca la opción de base de datos tal como se muestra en la siguiente instrucción T-SQL:</span><span class="sxs-lookup"><span data-stu-id="334fc-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="334fc-126">Paso 4: Migrar tablas</span><span class="sxs-lookup"><span data-stu-id="334fc-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="334fc-127">Debe crear y rellenar una copia optimizada en memoria de la tabla que desea probar.</span><span class="sxs-lookup"><span data-stu-id="334fc-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="334fc-128">Se puede crear mediante:</span><span class="sxs-lookup"><span data-stu-id="334fc-128">You can create it by using either:</span></span>

* <span data-ttu-id="334fc-129">El práctico Asistente para optimización de memoria en SSMS.</span><span class="sxs-lookup"><span data-stu-id="334fc-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="334fc-130">T-SQL manual.</span><span class="sxs-lookup"><span data-stu-id="334fc-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="334fc-131">Asistente para optimización de memoria en SSMS</span><span class="sxs-lookup"><span data-stu-id="334fc-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="334fc-132">Para usar esta opción de migración:</span><span class="sxs-lookup"><span data-stu-id="334fc-132">To use this migration option:</span></span>

1. <span data-ttu-id="334fc-133">Conéctese a la base de datos de prueba con SSMS.</span><span class="sxs-lookup"><span data-stu-id="334fc-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="334fc-134">En el **Explorador de objetos**, haga clic con el botón derecho en la tabla y después haga clic en **Asistente de optimización de memoria**.</span><span class="sxs-lookup"><span data-stu-id="334fc-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="334fc-135">Se muestra el asistente **Asesor del optimizador de memoria de tablas** .</span><span class="sxs-lookup"><span data-stu-id="334fc-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="334fc-136">En el asistente, haga clic en **Validación de migración** (o en el botón **Siguiente**) para ver si la tabla tiene las características no admitidas en las tablas optimizadas en memoria.</span><span class="sxs-lookup"><span data-stu-id="334fc-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="334fc-137">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="334fc-137">For more information, see:</span></span>
   
   * <span data-ttu-id="334fc-138">La *lista de comprobación de optimización de memoria* en [Asesor de optimización de memoria](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="334fc-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="334fc-139">[Construcciones de transact-SQL no admitidas por In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="334fc-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="334fc-140">[Migración a In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="334fc-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="334fc-141">Si la tabla no tiene características no admitidas, el asesor puede realizar el esquema real y la migración de datos.</span><span class="sxs-lookup"><span data-stu-id="334fc-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="334fc-142">T-SQL manual</span><span class="sxs-lookup"><span data-stu-id="334fc-142">Manual T-SQL</span></span>
<span data-ttu-id="334fc-143">Para usar esta opción de migración:</span><span class="sxs-lookup"><span data-stu-id="334fc-143">To use this migration option:</span></span>

1. <span data-ttu-id="334fc-144">Conéctese a la base de datos de prueba mediante SSMS (o una utilidad similar).</span><span class="sxs-lookup"><span data-stu-id="334fc-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="334fc-145">Obtenga el script T-SQL completo para la tabla y sus índices.</span><span class="sxs-lookup"><span data-stu-id="334fc-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="334fc-146">En SSMS, haga clic con el botón derecho en el nodo de tabla.</span><span class="sxs-lookup"><span data-stu-id="334fc-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="334fc-147">Haga clic en **Incluir tabla como** > **Crear en** > **Nueva ventana de consulta**.</span><span class="sxs-lookup"><span data-stu-id="334fc-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="334fc-148">En la ventana de script, agregue WITH (MEMORY_OPTIMIZED = ON) a la instrucción CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="334fc-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="334fc-149">Si hay un índice CLUSTERD, cámbielo a NONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="334fc-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="334fc-150">Cambie el nombre de la tabla existente mediante SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="334fc-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="334fc-151">Cree la nueva copia de la tabla optimizada en memoria mediante la ejecución del script CREATE TABLE editado.</span><span class="sxs-lookup"><span data-stu-id="334fc-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="334fc-152">Copie los datos en la tabla optimizada en memoria mediante INSERT... SELECT * INTO:</span><span class="sxs-lookup"><span data-stu-id="334fc-152">Copy the data to your memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="334fc-153">Paso 5 (opcional): Migrar los procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="334fc-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="334fc-154">La característica In-Memory también puede modificar un procedimiento almacenado para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="334fc-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="334fc-155">Consideraciones con procedimientos almacenados compilados de forma nativa</span><span class="sxs-lookup"><span data-stu-id="334fc-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="334fc-156">Un procedimiento almacenado compilado de forma nativa debe tener las siguientes opciones en su cláusula T-SQL WITH:</span><span class="sxs-lookup"><span data-stu-id="334fc-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="334fc-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="334fc-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="334fc-158">SCHEMABINDING: son las tablas cuyas definiciones de columna no puede cambiar de ninguna forma el procedimiento almacenado que pueda afectar al procedimiento almacenado, a menos que quite el procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="334fc-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="334fc-159">Un módulo nativo debe usar un gran [bloque ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para la administración de transacciones.</span><span class="sxs-lookup"><span data-stu-id="334fc-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="334fc-160">No hay ningún rol para una instrucción BEGIN TRANSACTION o ROLLBACK TRANSACTION explícita.</span><span class="sxs-lookup"><span data-stu-id="334fc-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="334fc-161">Si el código detecta una infracción de una regla de negocio, puede finalizar el bloque ATOMIC con una instrucción [THROW](http://msdn.microsoft.com/library/ee677615.aspx) .</span><span class="sxs-lookup"><span data-stu-id="334fc-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="334fc-162">CREATE PROCEDURE típico para compilar de forma nativa</span><span class="sxs-lookup"><span data-stu-id="334fc-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="334fc-163">Normalmente el T-SQL para crear un procedimiento almacenado compilado de forma nativa es similar a la siguiente plantilla:</span><span class="sxs-lookup"><span data-stu-id="334fc-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

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

* <span data-ttu-id="334fc-164">Para TRANSACTION_ISOLATION_LEVEL, SNAPSHOT es el valor más común para el procedimiento almacenado compilado de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="334fc-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="334fc-165">Sin embargo, también se admite un subconjunto de los demás valores:</span><span class="sxs-lookup"><span data-stu-id="334fc-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="334fc-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="334fc-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="334fc-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="334fc-167">SERIALIZABLE</span></span>
* <span data-ttu-id="334fc-168">El valor LANGUAGE debe estar presente en la vista sys.languages.</span><span class="sxs-lookup"><span data-stu-id="334fc-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="334fc-169">Migración de un procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="334fc-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="334fc-170">Los pasos de migración son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="334fc-170">The migration steps are:</span></span>

1. <span data-ttu-id="334fc-171">Obtenga el script CREATE PROCEDURE para el procedimiento almacenado regular interpretado.</span><span class="sxs-lookup"><span data-stu-id="334fc-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="334fc-172">Vuelva a escribir el encabezado para que coincida con la plantilla anterior.</span><span class="sxs-lookup"><span data-stu-id="334fc-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="334fc-173">Determine si el código T-SQL del procedimiento almacenado usa las características que no se admiten para los procedimientos almacenados compilados de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="334fc-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="334fc-174">Implemente soluciones alternativas si es necesario.</span><span class="sxs-lookup"><span data-stu-id="334fc-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="334fc-175">Para obtener información detallada, consulte [Problemas de migración para los procedimientos almacenados compilados de forma nativa](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="334fc-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="334fc-176">Cambie el nombre del procedimiento almacenado anterior por SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="334fc-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="334fc-177">O bien, simplemente quítelo con la instrucción DROP.</span><span class="sxs-lookup"><span data-stu-id="334fc-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="334fc-178">Ejecute el script CREATE PROCEDURE T-SQL editado.</span><span class="sxs-lookup"><span data-stu-id="334fc-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="334fc-179">Paso 6: Ejecutar la carga de trabajo en la prueba</span><span class="sxs-lookup"><span data-stu-id="334fc-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="334fc-180">Ejecutar una carga de trabajo en la base de datos de prueba es similar a la carga de trabajo que se ejecuta en la base de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="334fc-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="334fc-181">Esto debería mostrar la mejora del rendimiento conseguida mediante el uso de la característica In-Memory para tablas y procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="334fc-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="334fc-182">Los atributos principales de la carga de trabajo son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="334fc-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="334fc-183">Número de conexiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="334fc-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="334fc-184">Relación de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="334fc-184">Read/write ratio.</span></span>

<span data-ttu-id="334fc-185">Para personalizar y ejecutar la carga de trabajo de prueba, considere el uso de la práctica herramienta ostress.exe, que se muestra [aquí](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="334fc-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="334fc-186">Para minimizar la latencia de red, ejecute la prueba en la misma región geográfica de Azure donde existe la base de datos.</span><span class="sxs-lookup"><span data-stu-id="334fc-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="334fc-187">Paso 7: Supervisión postimplementación</span><span class="sxs-lookup"><span data-stu-id="334fc-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="334fc-188">Considere la posibilidad de supervisar los efectos de rendimiento de las implementaciones In-Memory en producción:</span><span class="sxs-lookup"><span data-stu-id="334fc-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="334fc-189">[Supervisión del almacenamiento In-Memory](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="334fc-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="334fc-190">Supervisión de Base de datos SQL de Azure con vistas de administración dinámica</span><span class="sxs-lookup"><span data-stu-id="334fc-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="334fc-191">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="334fc-191">Related links</span></span>
* [<span data-ttu-id="334fc-192">In-Memory OLTP (optimización In-Memory)</span><span class="sxs-lookup"><span data-stu-id="334fc-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="334fc-193">Introducción a los procedimientos almacenados compilados de forma nativa</span><span class="sxs-lookup"><span data-stu-id="334fc-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="334fc-194">Asesor de optimización en memoria</span><span class="sxs-lookup"><span data-stu-id="334fc-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

