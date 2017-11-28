---
title: "aaaGuide para usar PolyBase en el almacén de datos de SQL | Documentos de Microsoft"
description: Directrices y recomendaciones para el uso de PolyBase en escenarios de Almacenamiento de datos SQL.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="f02a6-103">Guía para el uso de PolyBase en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f02a6-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="f02a6-104">Esta guía ofrece información práctica para el uso de PolyBase en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f02a6-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="f02a6-105">tooget iniciado, vea hello [carga los datos con PolyBase] [ Load data with PolyBase] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f02a6-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="f02a6-106">Rotación de claves de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f02a6-106">Rotating storage keys</span></span>
<span data-ttu-id="f02a6-107">Desde hora tootime le interesará almacenamiento de blobs de toochange Hola acceso tooyour clave por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f02a6-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="f02a6-108">Hola tooperform de manera más elegante que esta tarea es toofollow un proceso conocido como "rotación de claves de Hola".</span><span class="sxs-lookup"><span data-stu-id="f02a6-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="f02a6-109">Puede que haya observado que dispone de dos claves de almacenamiento para su cuenta de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f02a6-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="f02a6-110">Esto es para que puede realizar la transición.</span><span class="sxs-lookup"><span data-stu-id="f02a6-110">This is so that you can transition</span></span>

<span data-ttu-id="f02a6-111">La rotación de las claves de la cuenta de almacenamiento de Azure es un proceso sencillo de tres pasos</span><span class="sxs-lookup"><span data-stu-id="f02a6-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="f02a6-112">Cree la segunda credencial de ámbito de la base de datos basada en clave de acceso de almacenamiento secundaria Hola</span><span class="sxs-lookup"><span data-stu-id="f02a6-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="f02a6-113">Crear el segundo origen de datos externo basado en esta nueva credencial</span><span class="sxs-lookup"><span data-stu-id="f02a6-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="f02a6-114">Quitar y crear tablas externas Hola que señala toohello nuevo origen de datos externo</span><span class="sxs-lookup"><span data-stu-id="f02a6-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="f02a6-115">Cuando haya migrado todas las tablas externas toohello nuevo origen de datos externo, a continuación, puede realizar Hola limpiar tareas:</span><span class="sxs-lookup"><span data-stu-id="f02a6-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="f02a6-116">Quitar el primer origen de datos externo</span><span class="sxs-lookup"><span data-stu-id="f02a6-116">Drop first external data source</span></span>
2. <span data-ttu-id="f02a6-117">Quitar la base de datos primer ámbito credencial basada en clave de acceso de almacenamiento principal de Hola</span><span class="sxs-lookup"><span data-stu-id="f02a6-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="f02a6-118">Inicie sesión en Azure y regenerar la clave de acceso principal de hello lista para hello vuela</span><span class="sxs-lookup"><span data-stu-id="f02a6-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="f02a6-119">Consulta de datos en el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="f02a6-119">Query Azure blob storage data</span></span>
<span data-ttu-id="f02a6-120">Consultas en tablas externas usar simplemente el nombre de la tabla de hello como si fuese una tabla relacional.</span><span class="sxs-lookup"><span data-stu-id="f02a6-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="f02a6-121">Una consulta en una tabla externa puede producir un error de hello *"consulta anulado: se alcanzó el umbral de rechazo de máximo de Hola durante la lectura desde un origen externo"*.</span><span class="sxs-lookup"><span data-stu-id="f02a6-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="f02a6-122">Esto indica que sus datos externos contienen registros *con modificaciones* .</span><span class="sxs-lookup"><span data-stu-id="f02a6-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="f02a6-123">Un registro de datos se considera 'sucio' si hello, tipos de datos reales/número de columnas no coinciden con definiciones de columna de Hola de tabla externa de Hola o datos hello no cumplen el formato de archivo externo especificado toohello.</span><span class="sxs-lookup"><span data-stu-id="f02a6-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="f02a6-124">toofix esto, asegúrese de que la tabla externa y las definiciones de formato de archivo externo son correctas y que los datos externos ajustan a las definiciones de toothese.</span><span class="sxs-lookup"><span data-stu-id="f02a6-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="f02a6-125">En caso de que un subconjunto de registros de datos externos están desfasadas, puede elegir tooreject estos registros para las consultas con las opciones de rechazo de hello en CREATE DDL de tabla externa.</span><span class="sxs-lookup"><span data-stu-id="f02a6-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="f02a6-126">Carga de datos del almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="f02a6-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="f02a6-127">Este ejemplo carga datos de la base de datos Data Warehouse tooSQL de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f02a6-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="f02a6-128">Almacenar datos directamente quita Hola tiempo de transferencia de datos para las consultas.</span><span class="sxs-lookup"><span data-stu-id="f02a6-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="f02a6-129">Almacenamiento de datos con un índice columnstore mejora el rendimiento de consultas para las consultas de análisis por seguridad too10x.</span><span class="sxs-lookup"><span data-stu-id="f02a6-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="f02a6-130">Este ejemplo utiliza datos de tooload de instrucción CREATE TABLE AS SELECT Hola.</span><span class="sxs-lookup"><span data-stu-id="f02a6-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="f02a6-131">nueva tabla de Hello hereda columnas de hello mencionadas en consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="f02a6-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="f02a6-132">Definición de la tabla externa de hello hereda los tipos de datos de Hola de esas columnas.</span><span class="sxs-lookup"><span data-stu-id="f02a6-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="f02a6-133">CREATE TABLE AS SELECT es un rendimiento muy instrucción de Transact-SQL que carga datos de hello en paralelo tooall Hola nodos de almacenamiento de datos SQL de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f02a6-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="f02a6-134">Se desarrolló originalmente para el motor de procesamiento paralelo masivo (MPP) hello en el sistema de la plataforma de análisis y ahora está en el almacén de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="f02a6-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="f02a6-135">Vea [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="f02a6-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="f02a6-136">Crear estadísticas de los datos recién cargados</span><span class="sxs-lookup"><span data-stu-id="f02a6-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="f02a6-137">Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="f02a6-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="f02a6-138">En orden tooget Hola un mejor rendimiento de las consultas, es importante que las estadísticas se crean en todas las columnas de todas las tablas después de la primera carga de Hola o se producen cambios sustanciales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="f02a6-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="f02a6-139">Para obtener una explicación detallada de las estadísticas, vea hello [estadísticas] [ Statistics] tema en el grupo de desarrollo de Hola de temas.</span><span class="sxs-lookup"><span data-stu-id="f02a6-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="f02a6-140">A continuación se muestra un ejemplo rápido de cómo cargarán toocreate estadísticas en la tabla de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f02a6-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="f02a6-141">Exportar el almacenamiento de blobs de datos tooAzure</span><span class="sxs-lookup"><span data-stu-id="f02a6-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="f02a6-142">Esta sección muestra cómo el almacenamiento de blobs tooexport datos de tooAzure de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f02a6-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="f02a6-143">Este ejemplo utiliza CREATE externo TABLE AS SELECT que son una alta rendimiento Transact-SQL instrucción tooexport Hola datos en paralelo desde todos los nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="f02a6-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="f02a6-144">Hello en el ejemplo siguiente se crea una tabla externa Weblogs2014 con definiciones de columna y los datos de dbo. Tabla de blogs.</span><span class="sxs-lookup"><span data-stu-id="f02a6-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="f02a6-145">definición de tabla externa de Hola se almacena en el almacén de datos de SQL y los resultados de Hola de instrucción SELECT Hola son exportado toohello directory "/ Archivar/log2014 /" en el contenedor de blobs de hello especificado por el origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f02a6-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="f02a6-146">Hola datos se exportan en formato de archivo de texto especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="f02a6-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="f02a6-147">Aislar la carga de usuarios</span><span class="sxs-lookup"><span data-stu-id="f02a6-147">Isolate Loading Users</span></span>
<span data-ttu-id="f02a6-148">A menudo hay una necesidad toohave varios usuarios que pueden cargar datos en un almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="f02a6-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="f02a6-149">Dado que hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] requiere permisos de CONTROL de base de datos de hello, terminará con varios usuarios con acceso de control a través de todos los esquemas.</span><span class="sxs-lookup"><span data-stu-id="f02a6-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="f02a6-150">toolimit esto, puede usar la instrucción de CONTROL denegar Hola.</span><span class="sxs-lookup"><span data-stu-id="f02a6-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="f02a6-151">Ejemplo: tenemos los esquemas de base de datos schema_A para el departamento A, schema_B para el departamento B y los usuarios de PolyBase user_A y user_B con cargas en los departamentos A y B respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f02a6-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="f02a6-152">A ambos se les ha concedido permiso de CONTROL sobre la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f02a6-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="f02a6-153">creadores de Hola de esquema A y B ahora bloquear sus esquemas con DENY:</span><span class="sxs-lookup"><span data-stu-id="f02a6-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="f02a6-154">Con esto, userA y UserB deben ahora bloquearse de hello esquema de otro departamento.</span><span class="sxs-lookup"><span data-stu-id="f02a6-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="f02a6-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f02a6-155">Next steps</span></span>
<span data-ttu-id="f02a6-156">toolearn más información acerca de movimiento de datos de tooSQL almacenamiento de datos, vea hello [información general sobre la migración de datos][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="f02a6-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
