---
title: Carga desde blob de Azure a un almacenamiento de datos de Azure | Microsoft Docs
description: "Aprenda a usar PolyBase para cargar datos de Almacenamiento de blobs de Azure en Almacenamiento de datos SQL. Cargue algunas tablas de datos públicos en el esquema Contoso Retail Data Warehouse."
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
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="0cfd1-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase) [Carga de datos de Almacenamiento de blobs de Azure en Almacenamiento de datos SQL (PolyBase)]</span><span class="sxs-lookup"><span data-stu-id="0cfd1-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cfd1-105">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="0cfd1-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="0cfd1-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="0cfd1-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="0cfd1-107">Use PolyBase y comandos de T-SQL para cargar datos de Almacenamiento de blobs de Azure en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="0cfd1-108">Para no complicarlo, este tutorial carga dos tablas de un Blob de almacenamiento de Azure público en el esquema Contoso Retail Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="0cfd1-109">Para cargar el conjunto de datos completo, ejecute el ejemplo [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] (Carga del esquema Contoso Retail Data Warehouse completo) del repositorio de ejemplos de Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="0cfd1-110">En este tutorial, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0cfd1-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="0cfd1-111">Configuración de PolyBase para realizar la carga desde Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="0cfd1-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="0cfd1-112">Carga de datos públicos en su base de datos</span><span class="sxs-lookup"><span data-stu-id="0cfd1-112">Load public data into your database</span></span>
3. <span data-ttu-id="0cfd1-113">Realización de optimizaciones una vez finalizada la carga</span><span class="sxs-lookup"><span data-stu-id="0cfd1-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0cfd1-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0cfd1-114">Before you begin</span></span>
<span data-ttu-id="0cfd1-115">Para ejecutar este tutorial, necesita una cuenta de Azure que cuente ya con una base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="0cfd1-116">Si todavía no la tiene, consulte [Creación de una instancia de SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0cfd1-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="0cfd1-117">1. Configuración del origen de datos</span><span class="sxs-lookup"><span data-stu-id="0cfd1-117">1. Configure the data source</span></span>
<span data-ttu-id="0cfd1-118">PolyBase usa objetos externos T-SQL para definir la ubicación y los atributos de los datos externos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="0cfd1-119">Las definiciones de objeto externo se almacenan en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="0cfd1-120">Los propios datos se almacenan externamente.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="0cfd1-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-121">1.1.</span></span> <span data-ttu-id="0cfd1-122">Creación de una credencial</span><span class="sxs-lookup"><span data-stu-id="0cfd1-122">Create a credential</span></span>
<span data-ttu-id="0cfd1-123">**Omita este paso** si va a cargar los datos públicos de Contoso.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="0cfd1-124">No es necesario un acceso seguro a los datos públicos, pues ya son accesibles para cualquier persona.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="0cfd1-125">**No omita este paso** si va a usar este tutorial como plantilla para cargar sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="0cfd1-126">Para tener acceso a los datos a través de una credencial, use el siguiente script para crear una credencial con ámbito de base de datos y utilizarla al definir la ubicación del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="0cfd1-127">Vaya al paso 2.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="0cfd1-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-128">1.2.</span></span> <span data-ttu-id="0cfd1-129">Creación del origen de datos externo</span><span class="sxs-lookup"><span data-stu-id="0cfd1-129">Create the external data source</span></span>
<span data-ttu-id="0cfd1-130">Utilice este comando [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] para almacenar la ubicación de los datos y el tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="0cfd1-131">Si decide que sus contenedores de Almacenamiento de blobs de Azure serán públicos, recuerde que, como propietario de los datos, se le aplicarán cargos de salida de datos cuando los datos dejen el centro de datos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="0cfd1-132">2. Configuración del formato de datos</span><span class="sxs-lookup"><span data-stu-id="0cfd1-132">2. Configure data format</span></span>
<span data-ttu-id="0cfd1-133">Los datos se almacenan en archivos de texto en Almacenamiento de blobs de Azure y un delimitador separa cada campo.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="0cfd1-134">Ejecute este comando [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] para especificar el formato de los datos en los archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="0cfd1-135">Los datos de Contoso no están comprimidos y están delimitados por canalización.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-135">The Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-the-external-tables"></a><span data-ttu-id="0cfd1-136">3. Creación de la tablas externas</span><span class="sxs-lookup"><span data-stu-id="0cfd1-136">3. Create the external tables</span></span>
<span data-ttu-id="0cfd1-137">Ahora que ha especificado el origen de datos y el formato de archivo, está listo para crear las tablas externas.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="0cfd1-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-138">3.1.</span></span> <span data-ttu-id="0cfd1-139">Creación de un esquema de los datos</span><span class="sxs-lookup"><span data-stu-id="0cfd1-139">Create a schema for the data.</span></span>
<span data-ttu-id="0cfd1-140">A fin de crear un lugar para almacenar los datos de Contoso en su base de datos, cree un esquema.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="0cfd1-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-141">3.2.</span></span> <span data-ttu-id="0cfd1-142">Creación de la tablas externas</span><span class="sxs-lookup"><span data-stu-id="0cfd1-142">Create the external tables.</span></span>
<span data-ttu-id="0cfd1-143">Ejecute este script para crear las tablas externas DimProduct y FactOnlineSales.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="0cfd1-144">Todo lo que hacemos aquí es definir nombres de columna y tipos de datos, que enlazamos a la ubicación y formato de los archivos de Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="0cfd1-145">La definición se almacena en Almacenamiento de datos SQL y los datos siguen en el Blob de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="0cfd1-146">El parámetro **LOCATION** es la carpeta situada bajo la carpeta raíz en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="0cfd1-147">Cada tabla está en una carpeta diferente.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-the-data"></a><span data-ttu-id="0cfd1-148">4. Carga de los datos</span><span class="sxs-lookup"><span data-stu-id="0cfd1-148">4. Load the data</span></span>
<span data-ttu-id="0cfd1-149">Hay diferentes maneras de obtener acceso a datos externos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-149">There's different ways to access external data.</span></span>  <span data-ttu-id="0cfd1-150">Puede consultar datos directamente en la tabla externa, cargar los datos en nuevas tablas de base de datos o agregar datos externos a tablas de base de datos existentes.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="0cfd1-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-151">4.1.</span></span> <span data-ttu-id="0cfd1-152">Creación de un nuevo esquema</span><span class="sxs-lookup"><span data-stu-id="0cfd1-152">Create a new schema</span></span>
<span data-ttu-id="0cfd1-153">CTAS crea una nueva tabla que contiene datos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="0cfd1-154">En primer lugar, cree un esquema de los datos de Contoso.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="0cfd1-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-155">4.2.</span></span> <span data-ttu-id="0cfd1-156">Carga de los datos en nuevas tablas</span><span class="sxs-lookup"><span data-stu-id="0cfd1-156">Load the data into new tables</span></span>
<span data-ttu-id="0cfd1-157">Para cargar datos de Azure Blob Storage y guardarlos en una tabla dentro de su base de datos, use la instrucción [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="0cfd1-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="0cfd1-158">Al realizarse la carga con CTAS, se aprovechan las tablas externas fuertemente tipadas que acaba de crear. Para cargar los datos en nuevas tablas, use una instrucción [CTAS][CTAS] por tabla.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="0cfd1-159">CTAS crea una nueva tabla y la rellena con los resultados de una instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="0cfd1-160">CTAS define la nueva tabla para tener las mismas columnas y tipos de datos que los resultados de la instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="0cfd1-161">Si selecciona todas las columnas de una tabla externa, la nueva tabla será una réplica de las columnas y los tipos de datos de la tabla externa.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="0cfd1-162">En este ejemplo, creamos la tabla de dimensiones y la de hechos como tablas hash distribuidas.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="0cfd1-163">4.3. Seguimiento del progreso de carga</span><span class="sxs-lookup"><span data-stu-id="0cfd1-163">4.3 Track the load progress</span></span>
<span data-ttu-id="0cfd1-164">Puede seguir el progreso de la carga con las vistas de administración dinámica (DMV).</span><span class="sxs-lookup"><span data-stu-id="0cfd1-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="0cfd1-165">5. Optimización de compresión de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="0cfd1-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="0cfd1-166">De forma predeterminada, Almacenamiento de datos SQL almacena la tabla como índice de almacén de columnas agrupado.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="0cfd1-167">Una vez completada una carga, puede que algunas de las filas de datos no se compriman en el almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="0cfd1-168">Existen varios motivos por los que esto puede ocurrir.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="0cfd1-169">Para aprender más, consulte el artículo sobre [administración de índices de almacén de columnas][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="0cfd1-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="0cfd1-170">Para optimizar el rendimiento de las consultas y la compresión de almacén de columnas después de una carga, vuelva a crear la tabla para obligar al índice de almacén de columnas a comprimir todas las filas.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="0cfd1-171">Para más información sobre el mantenimiento de los índices de almacén de columnas, consulte el artículo sobre [administración de índices de almacén de columnas][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="0cfd1-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="0cfd1-172">6. Optimización de estadísticas</span><span class="sxs-lookup"><span data-stu-id="0cfd1-172">6. Optimize statistics</span></span>
<span data-ttu-id="0cfd1-173">Es mejor crear estadísticas de columna única inmediatamente después de una carga.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="0cfd1-174">Hay algunas opciones para las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-174">There are some choices for statistics.</span></span> <span data-ttu-id="0cfd1-175">Por ejemplo, si crea estadísticas de columna única en cada columna, la recompilación de todas las estadísticas puede llevar mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="0cfd1-176">Si sabe que algunas columnas no van a estar en predicados de consulta, puede omitir la creación de estadísticas en dichas columnas.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="0cfd1-177">Si decide crear estadísticas de columna única en todas las columnas de cada una de las tablas, puede usar el ejemplo de código de procedimiento almacenado `prc_sqldw_create_stats` en el artículo sobre [estadísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="0cfd1-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="0cfd1-178">El ejemplo siguiente es un buen punto de partida para la creación de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="0cfd1-179">Crea estadísticas de columna única en cada una de las columnas de la tabla de dimensiones y en cada una de las columnas de combinación de las tablas de hechos.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="0cfd1-180">Siempre puede agregar estadísticas de columna única o de varias columnas a otras columnas de la tabla de hechos más adelante.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="0cfd1-181">Logro conseguido.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-181">Achievement unlocked!</span></span>
<span data-ttu-id="0cfd1-182">Ha cargado correctamente datos públicos en Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="0cfd1-183">Buen trabajo.</span><span class="sxs-lookup"><span data-stu-id="0cfd1-183">Great job!</span></span>

<span data-ttu-id="0cfd1-184">Ya puede empezar a consultar las tablas mediante consultas como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="0cfd1-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="0cfd1-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0cfd1-185">Next steps</span></span>
<span data-ttu-id="0cfd1-186">Para cargar todos los datos de Contoso Retail Data Warehouse, use el script que aparece. Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="0cfd1-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
