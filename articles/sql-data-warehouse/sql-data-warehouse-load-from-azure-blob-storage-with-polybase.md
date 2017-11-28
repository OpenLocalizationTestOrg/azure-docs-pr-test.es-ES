---
title: aaaLoad de almacenamiento de datos de blob de Azure tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse datos de tooload de PolyBase de Azure almacenamiento de blobs en almacenamiento de datos de SQL. Cargar algunas tablas de datos públicos en el esquema de almacenamiento de datos de Contoso Retail Hola."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="e7ebb-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase) [Carga de datos de Almacenamiento de blobs de Azure en Almacenamiento de datos SQL (PolyBase)]</span><span class="sxs-lookup"><span data-stu-id="e7ebb-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7ebb-105">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="e7ebb-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="e7ebb-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="e7ebb-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="e7ebb-107">Use PolyBase y T-SQL comandos tooload datos desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="e7ebb-108">tookeep simple, este tutorial carga dos tablas de un Blob de almacenamiento de Azure público en el esquema de almacenamiento de datos de Contoso Retail Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="e7ebb-109">tooload Hola completo conjunto de datos, ejecutar el ejemplo de Hola [carga Hola completa almacenamiento de datos de Contoso Retail] [ Load hello full Contoso Retail Data Warehouse] del repositorio de ejemplos de Microsoft SQL Server Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="e7ebb-110">En este tutorial, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7ebb-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="e7ebb-111">Configurar PolyBase tooload desde el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="e7ebb-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="e7ebb-112">Carga de datos públicos en su base de datos</span><span class="sxs-lookup"><span data-stu-id="e7ebb-112">Load public data into your database</span></span>
3. <span data-ttu-id="e7ebb-113">Una vez finalizada la carga de hello, realizar las optimizaciones.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e7ebb-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e7ebb-114">Before you begin</span></span>
<span data-ttu-id="e7ebb-115">toorun este tutorial, necesita una cuenta de Azure que ya tiene una base de datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="e7ebb-116">Si todavía no la tiene, consulte [Creación de una instancia de SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e7ebb-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="e7ebb-117">1. Configurar origen de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="e7ebb-117">1. Configure hello data source</span></span>
<span data-ttu-id="e7ebb-118">PolyBase usa la ubicación de T-SQL objetos externos toodefine hello y atributos de datos externos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="e7ebb-119">las definiciones de objeto externo Hola se almacenan en el almacén de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="e7ebb-120">datos Hello en sí se almacenan externamente.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="e7ebb-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-121">1.1.</span></span> <span data-ttu-id="e7ebb-122">Creación de una credencial</span><span class="sxs-lookup"><span data-stu-id="e7ebb-122">Create a credential</span></span>
<span data-ttu-id="e7ebb-123">**Omita este paso** si va a cargar los datos públicos de hello Contoso.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="e7ebb-124">No necesita datos públicos de un acceso seguro toohello porque ya está tooanyone accesible.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="e7ebb-125">**No omita este paso** si va a usar este tutorial como plantilla para cargar sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="e7ebb-126">tooaccess datos a través de una credencial, Hola de uso después de credencial toocreate un ámbito de base de datos de secuencias de comandos y, a continuación, utilizarlo al definir la ubicación de Hola Hola del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="e7ebb-127">Omitir toostep 2.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="e7ebb-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-128">1.2.</span></span> <span data-ttu-id="e7ebb-129">Crear origen de datos externo de Hola</span><span class="sxs-lookup"><span data-stu-id="e7ebb-129">Create hello external data source</span></span>
<span data-ttu-id="e7ebb-130">Utilícelo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando ubicación de hello toostore de datos de Hola y tipo de Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="e7ebb-131">Si elige toomake el público de contenedores de almacenamiento de blobs de azure, recuerde que como propietario de los datos Hola se le cobrará por datos cargos de salida cuando los datos dejan de centro de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="e7ebb-132">2. Configuración del formato de datos</span><span class="sxs-lookup"><span data-stu-id="e7ebb-132">2. Configure data format</span></span>
<span data-ttu-id="e7ebb-133">Hola datos se almacenan en archivos de texto en el almacenamiento de blobs de Azure, y cada campo se separa con un delimitador.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="e7ebb-134">Ejecute este [crear formato de archivo externo] [ CREATE EXTERNAL FILE FORMAT] formato de comando toospecify Hola de datos de Hola Hola en archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="e7ebb-135">Hola datos de Contoso se descomprime y delimitado por canalización.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="e7ebb-136">3. Crear tablas externas de Hola</span><span class="sxs-lookup"><span data-stu-id="e7ebb-136">3. Create hello external tables</span></span>
<span data-ttu-id="e7ebb-137">Ahora que ha especificado el formato de origen y el archivo de datos de hello, son tablas externas de hello toocreate listo.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="e7ebb-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-138">3.1.</span></span> <span data-ttu-id="e7ebb-139">Crear un esquema para los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-139">Create a schema for hello data.</span></span>
<span data-ttu-id="e7ebb-140">toocreate un Hola de toostore lugar datos de Contoso en la base de datos, crear un esquema.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="e7ebb-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-141">3.2.</span></span> <span data-ttu-id="e7ebb-142">Crear tablas externas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-142">Create hello external tables.</span></span>
<span data-ttu-id="e7ebb-143">Ejecute este hello toocreate de secuencia de comandos DimProduct y FactOnlineSales tablas externas.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="e7ebb-144">Lo que estamos haciendo aquí es definir nombres de columna y tipos de datos y enlazarlos toohello ubicación y el formato de archivos de almacenamiento de blobs de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="e7ebb-145">Hola definición se almacena en el almacén de datos de SQL y datos de hello aún están en hello Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="e7ebb-146">Hola **ubicación** parámetro es la carpeta de hello en carpeta de raíz de Hola Hola Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="e7ebb-147">Cada tabla está en una carpeta diferente.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-147">Each table is in a different folder.</span></span>

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a><span data-ttu-id="e7ebb-148">4. Cargar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="e7ebb-148">4. Load hello data</span></span>
<span data-ttu-id="e7ebb-149">No hay datos externos de tooaccess de maneras diferentes.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="e7ebb-150">Puede consultar los datos directamente desde la tabla externa de hello, cargar datos de hello en tablas de base de datos nueva o agregar tablas de base de datos de tooexisting datos externos.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="e7ebb-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-151">4.1.</span></span> <span data-ttu-id="e7ebb-152">Creación de un nuevo esquema</span><span class="sxs-lookup"><span data-stu-id="e7ebb-152">Create a new schema</span></span>
<span data-ttu-id="e7ebb-153">CTAS crea una nueva tabla que contiene datos.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="e7ebb-154">En primer lugar, cree un esquema para los datos de contoso Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="e7ebb-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-155">4.2.</span></span> <span data-ttu-id="e7ebb-156">Cargar datos de hello en nuevas tablas</span><span class="sxs-lookup"><span data-stu-id="e7ebb-156">Load hello data into new tables</span></span>
<span data-ttu-id="e7ebb-157">datos de tooload de Azure almacenamiento de blobs y guardarlo en una tabla dentro de la base de datos, utilice hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrucción.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="e7ebb-158">Cargando la CTAS aprovecha Hola fuertemente tipadas tablas externas tienen created.tooload simplemente Hola datos en tablas nuevas, utilice uno [CTAS] [ CTAS] instrucción por tabla.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="e7ebb-159">CTAS crea una nueva tabla y lo rellena con resultados de Hola de una instrucción select.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="e7ebb-160">CTAS define Hola nueva tabla toohave Hola mismos tipos de datos y columnas como resultados de Hola de hello instrucción select.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="e7ebb-161">Si selecciona todas las columnas de hello en una tabla externa, tabla nueva Hola será una réplica de columnas de Hola y tipos de datos en la tabla externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="e7ebb-162">En este ejemplo, creamos dimensión hello y tabla de hechos de hello como hash tablas distribuidas.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="e7ebb-163">4.3 seguir el progreso de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="e7ebb-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="e7ebb-164">Pueda seguir el progreso de saludo de la carga mediante vistas de administración dinámica (DMV).</span><span class="sxs-lookup"><span data-stu-id="e7ebb-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="e7ebb-165">5. Optimización de compresión de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="e7ebb-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="e7ebb-166">De forma predeterminada, almacenamiento de datos de SQL almacena la tabla de Hola como un índice de almacén de columnas agrupado.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="e7ebb-167">Una vez completada una carga, algunas de las filas de datos de hello podrían no va a comprimir con almacén de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="e7ebb-168">Existen varios motivos por los que esto puede ocurrir.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="e7ebb-169">más información, consulte toolearn [administrar índices de almacén de columnas][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="e7ebb-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="e7ebb-170">rendimiento de las consultas toooptimize y compresión de almacén de columnas después de una carga, vuelva a generar toocompress de índice de almacén de columnas de hello tabla tooforce Hola todas las filas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="e7ebb-171">Para obtener más información sobre el mantenimiento de índices de almacén de columnas, vea hello [administrar índices de almacén de columnas] [ manage columnstore indexes] artículo.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="e7ebb-172">6. Optimización de estadísticas</span><span class="sxs-lookup"><span data-stu-id="e7ebb-172">6. Optimize statistics</span></span>
<span data-ttu-id="e7ebb-173">Es mejor estadísticas de columna única de toocreate inmediatamente después de una carga.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="e7ebb-174">Hay algunas opciones para las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-174">There are some choices for statistics.</span></span> <span data-ttu-id="e7ebb-175">Por ejemplo, si crea estadísticas de columna única en todas las columnas puede tardar un toorebuild mucho tiempo todas las estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="e7ebb-176">Si sabe que las columnas que no van toobe predicados de consulta, puede ir creando estadísticas sobre esas columnas.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="e7ebb-177">Si decide toocreate estadísticas de columna única en todas las columnas de cada tabla, puede usar el ejemplo de código de procedimiento almacenado Hola `prc_sqldw_create_stats` en hello [estadísticas] [ statistics] artículo.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="e7ebb-178">Hola siguiente ejemplo es un buen punto de partida para crear las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="e7ebb-179">Crea estadísticas de columna única en cada columna de tabla de dimensiones de Hola y en cada columna de combinación en las tablas de hechos Hola.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="e7ebb-180">Siempre puede agregar columnas de la tabla de hechos de uno o varias columnas de estadísticas tooother más adelante.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a><span data-ttu-id="e7ebb-181">Logro conseguido.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-181">Achievement unlocked!</span></span>
<span data-ttu-id="e7ebb-182">Ha cargado correctamente datos públicos en Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e7ebb-183">Buen trabajo.</span><span class="sxs-lookup"><span data-stu-id="e7ebb-183">Great job!</span></span>

<span data-ttu-id="e7ebb-184">Ahora puede comenzar a realizar consultas en tablas de hello mediante consultas como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7ebb-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="e7ebb-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7ebb-185">Next steps</span></span>
<span data-ttu-id="e7ebb-186">datos tooload Hola completa almacenamiento de datos de Contoso Retail, use el script de Hola en para obtener más sugerencias de desarrollo, consulte [Introducción al desarrollo de almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e7ebb-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
