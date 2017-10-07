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
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Load data from Azure blob storage into SQL Data Warehouse (PolyBase) [Carga de datos de Almacenamiento de blobs de Azure en Almacenamiento de datos SQL (PolyBase)]
> [!div class="op_single_selector"]
> * [Factoría de datos](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

Use PolyBase y T-SQL comandos tooload datos desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL Azure. 

tookeep simple, este tutorial carga dos tablas de un Blob de almacenamiento de Azure público en el esquema de almacenamiento de datos de Contoso Retail Hola. tooload Hola completo conjunto de datos, ejecutar el ejemplo de Hola [carga Hola completa almacenamiento de datos de Contoso Retail] [ Load hello full Contoso Retail Data Warehouse] del repositorio de ejemplos de Microsoft SQL Server Hola.

En este tutorial, aprenderá lo siguiente:

1. Configurar PolyBase tooload desde el almacenamiento de blobs de Azure
2. Carga de datos públicos en su base de datos
3. Una vez finalizada la carga de hello, realizar las optimizaciones.

## <a name="before-you-begin"></a>Antes de empezar
toorun este tutorial, necesita una cuenta de Azure que ya tiene una base de datos de almacenamiento de datos SQL. Si todavía no la tiene, consulte [Creación de una instancia de SQL Data Warehouse][Create a SQL Data Warehouse].

## <a name="1-configure-hello-data-source"></a>1. Configurar origen de datos de Hola
PolyBase usa la ubicación de T-SQL objetos externos toodefine hello y atributos de datos externos de Hola. las definiciones de objeto externo Hola se almacenan en el almacén de datos de SQL. datos Hello en sí se almacenan externamente.

### <a name="11-create-a-credential"></a>1.1. Creación de una credencial
**Omita este paso** si va a cargar los datos públicos de hello Contoso. No necesita datos públicos de un acceso seguro toohello porque ya está tooanyone accesible.

**No omita este paso** si va a usar este tutorial como plantilla para cargar sus propios datos. tooaccess datos a través de una credencial, Hola de uso después de credencial toocreate un ámbito de base de datos de secuencias de comandos y, a continuación, utilizarlo al definir la ubicación de Hola Hola del origen de datos.

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

Omitir toostep 2.

### <a name="12-create-hello-external-data-source"></a>1.2. Crear origen de datos externo de Hola
Utilícelo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando ubicación de hello toostore de datos de Hola y tipo de Hola de datos. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> Si elige toomake el público de contenedores de almacenamiento de blobs de azure, recuerde que como propietario de los datos Hola se le cobrará por datos cargos de salida cuando los datos dejan de centro de datos de Hola. 
> 
> 

## <a name="2-configure-data-format"></a>2. Configuración del formato de datos
Hola datos se almacenan en archivos de texto en el almacenamiento de blobs de Azure, y cada campo se separa con un delimitador. Ejecute este [crear formato de archivo externo] [ CREATE EXTERNAL FILE FORMAT] formato de comando toospecify Hola de datos de Hola Hola en archivos de texto. Hola datos de Contoso se descomprime y delimitado por canalización.

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

## <a name="3-create-hello-external-tables"></a>3. Crear tablas externas de Hola
Ahora que ha especificado el formato de origen y el archivo de datos de hello, son tablas externas de hello toocreate listo. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Crear un esquema para los datos de Hola.
toocreate un Hola de toostore lugar datos de Contoso en la base de datos, crear un esquema.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Crear tablas externas de Hola.
Ejecute este hello toocreate de secuencia de comandos DimProduct y FactOnlineSales tablas externas. Lo que estamos haciendo aquí es definir nombres de columna y tipos de datos y enlazarlos toohello ubicación y el formato de archivos de almacenamiento de blobs de Azure Hola. Hola definición se almacena en el almacén de datos de SQL y datos de hello aún están en hello Blob de almacenamiento de Azure.

Hola **ubicación** parámetro es la carpeta de hello en carpeta de raíz de Hola Hola Blob de almacenamiento de Azure. Cada tabla está en una carpeta diferente.

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

## <a name="4-load-hello-data"></a>4. Cargar datos de Hola
No hay datos externos de tooaccess de maneras diferentes.  Puede consultar los datos directamente desde la tabla externa de hello, cargar datos de hello en tablas de base de datos nueva o agregar tablas de base de datos de tooexisting datos externos.  

### <a name="41-create-a-new-schema"></a>4.1. Creación de un nuevo esquema
CTAS crea una nueva tabla que contiene datos.  En primer lugar, cree un esquema para los datos de contoso Hola.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Cargar datos de hello en nuevas tablas
datos de tooload de Azure almacenamiento de blobs y guardarlo en una tabla dentro de la base de datos, utilice hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrucción. Cargando la CTAS aprovecha Hola fuertemente tipadas tablas externas tienen created.tooload simplemente Hola datos en tablas nuevas, utilice uno [CTAS] [ CTAS] instrucción por tabla. 
 
CTAS crea una nueva tabla y lo rellena con resultados de Hola de una instrucción select. CTAS define Hola nueva tabla toohave Hola mismos tipos de datos y columnas como resultados de Hola de hello instrucción select. Si selecciona todas las columnas de hello en una tabla externa, tabla nueva Hola será una réplica de columnas de Hola y tipos de datos en la tabla externa de Hola.

En este ejemplo, creamos dimensión hello y tabla de hechos de hello como hash tablas distribuidas. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 seguir el progreso de carga de Hola
Pueda seguir el progreso de saludo de la carga mediante vistas de administración dinámica (DMV). 

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

## <a name="5-optimize-columnstore-compression"></a>5. Optimización de compresión de almacén de columnas
De forma predeterminada, almacenamiento de datos de SQL almacena la tabla de Hola como un índice de almacén de columnas agrupado. Una vez completada una carga, algunas de las filas de datos de hello podrían no va a comprimir con almacén de columnas de Hola.  Existen varios motivos por los que esto puede ocurrir. más información, consulte toolearn [administrar índices de almacén de columnas][manage columnstore indexes].

rendimiento de las consultas toooptimize y compresión de almacén de columnas después de una carga, vuelva a generar toocompress de índice de almacén de columnas de hello tabla tooforce Hola todas las filas de Hola. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Para obtener más información sobre el mantenimiento de índices de almacén de columnas, vea hello [administrar índices de almacén de columnas] [ manage columnstore indexes] artículo.

## <a name="6-optimize-statistics"></a>6. Optimización de estadísticas
Es mejor estadísticas de columna única de toocreate inmediatamente después de una carga. Hay algunas opciones para las estadísticas. Por ejemplo, si crea estadísticas de columna única en todas las columnas puede tardar un toorebuild mucho tiempo todas las estadísticas de Hola. Si sabe que las columnas que no van toobe predicados de consulta, puede ir creando estadísticas sobre esas columnas.

Si decide toocreate estadísticas de columna única en todas las columnas de cada tabla, puede usar el ejemplo de código de procedimiento almacenado Hola `prc_sqldw_create_stats` en hello [estadísticas] [ statistics] artículo.

Hola siguiente ejemplo es un buen punto de partida para crear las estadísticas. Crea estadísticas de columna única en cada columna de tabla de dimensiones de Hola y en cada columna de combinación en las tablas de hechos Hola. Siempre puede agregar columnas de la tabla de hechos de uno o varias columnas de estadísticas tooother más adelante.

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

## <a name="achievement-unlocked"></a>Logro conseguido.
Ha cargado correctamente datos públicos en Almacenamiento de datos SQL de Azure. Buen trabajo.

Ahora puede comenzar a realizar consultas en tablas de hello mediante consultas como Hola siguiente:

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>Pasos siguientes
datos tooload Hola completa almacenamiento de datos de Contoso Retail, use el script de Hola en para obtener más sugerencias de desarrollo, consulte [Introducción al desarrollo de almacenamiento de datos SQL][SQL Data Warehouse development overview].

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
