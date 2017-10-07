---
title: aaaPolyBase en Tutorial de almacenamiento de datos de SQL | Documentos de Microsoft
description: "Obtenga información acerca de qué es PolyBase y cómo toouse para escenarios de almacenamiento de datos."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>Carga de datos con PolyBase en Almacenamiento de datos SQL
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Factoría de datos](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Este tutorial se muestra cómo los datos de tooload en almacenamiento de datos de SQL con AzCopy y PolyBase. Cuando termine, sabrá cómo:

* Usar el almacenamiento de blobs de AzCopy toocopy datos tooAzure
* Crear objetos de base de datos de Hola de toodefine
* Ejecutar una consulta de T-SQL tooload Hola datos

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tutorial, necesita

* Una base de datos de Almacenamiento de datos SQL.
* Una cuenta de almacenamiento de Azure del tipo Almacenamiento con redundancia local estándar (LRS estándar), Almacenamiento con redundancia geográfica estándar (GRS estándar) o Almacenamiento con redundancia geográfica de acceso de lectura estándar  (RAGRS estándar).
* La utilidad de línea de comandos AzCopy. Descargue e instale hello [versión más reciente de AzCopy] [ latest version of AzCopy] que se instala con hello herramientas de almacenamiento de Microsoft Azure.
  
    ![Herramientas de almacenamiento de Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>Paso 1: Agregar almacenamiento de blobs de tooAzure de datos de ejemplo
Datos de pedidos tooload, necesitamos tooput algunos datos de ejemplo en un almacenamiento de blobs de Azure. En este paso, se rellena un almacenamiento de blobs de Azure con datos de ejemplo. Más adelante, usaremos PolyBase tooload estos datos de ejemplo en la base de datos de almacenamiento de datos SQL.

### <a name="a-prepare-a-sample-text-file"></a>A. Preparación de un archivo de texto de ejemplo
tooprepare un archivo de texto de ejemplo:

1. Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo. Guarde este directorio temporal de tooyour local como % temp%\DimDate2.txt.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a>B. Búsqueda del punto de conexión del servicio BLOB
toofind su extremo de servicio blob:

1. Desde el Portal de Azure Hola seleccione **examinar** > **cuentas de almacenamiento**.
2. Haga clic en la cuenta de almacenamiento de hello que desea toouse.
3. En la hoja de la cuenta de almacenamiento de hello, haga clic en Blobs
   
    ![Haga clic en Blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. Guardar la dirección URL del punto de conexión del servicio BLOB para usarla más adelante.
   
    ![Punto de conexión del servicio BLOB](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Búsqueda de la clave de almacenamiento de Azure
toofind su clave de almacenamiento de Azure:

1. En hello Portal de Azure, seleccione **examinar** > **cuentas de almacenamiento**.
2. Haga clic en la cuenta de almacenamiento de hello que desea toouse.
3. Seleccione **Toda la configuración** > **Claves de acceso**.
4. Haga clic en hello copia cuadro toocopy entre el Portapapeles de toohello de claves de acceso.
   
    ![Copie la clave de almacenamiento de Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Copie el almacenamiento de blobs de tooAzure de archivo de ejemplo de Hola
toocopy el almacenamiento de blobs de tooAzure de datos:

1. Abra un símbolo del sistema y cambie el directorio de instalación de directorios toohello AzCopy. Este comando cambia el directorio de instalación predeterminado de toohello en un cliente de Windows de 64 bits.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. Ejecute hello siguiente archivo de comandos tooupload Hola. Especifique la dirección URL del punto de conexión del servicio BLOB de <blob service endpoint URL> y la clave de la cuenta de almacenamiento de Azure de <azure_storage_account_key>.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

Vea también [Getting Started with Hola utilidad de línea de comandos de AzCopy][Getting Started with hello AzCopy Command-Line Utility].

### <a name="e-explore-your-blob-storage-container"></a>E. Exploración del contenedor de almacenamiento de blobs
archivo de hello toosee cargado tooblob almacenamiento:

1. Volver atrás tooyour módulo de servicio de Blob.
2. En Contenedores, haga doble clic en **datacontainer**.
3. datos de tooyour de tooexplore Hola ruta de acceso, haga clic en la carpeta de hello **datedimension** y verá el archivo cargado **DimDate2.txt**.
4. Haga clic en Propiedades de tooview, **DimDate2.txt**.
5. Tenga en cuenta que en la hoja de propiedades de Blob de hello, puede descargar o eliminar el archivo hello.
   
    ![Vea el blob de almacenamiento de Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>Paso 2: Crear una tabla externa para datos de ejemplo de Hola
En esta sección se creará una tabla externa que define los datos de ejemplo de Hola.

PolyBase usa datos de tablas externas tooaccess en el almacenamiento de blobs de Azure. Puesto que los datos de hello no se almacenan en el almacén de datos SQL, PolyBase controla datos externos de autenticación toohello mediante una credencial de ámbito de base de datos.

ejemplo de Hola en este paso usa estos toocreate de instrucciones de Transact-SQL una tabla externa.

* [Crear la clave maestra (Transact-SQL)] [ Create Master Key (Transact-SQL)] credencial con ámbito de secreto de hello tooencrypt de la base de datos.
* [Crear credencial con ámbito de base de datos (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify información de autenticación para su cuenta de almacenamiento de Azure.
* [Crear origen de datos externo (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify ubicación de Hola de su almacenamiento de blobs de Azure.
* [Crear formato de archivo externo (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify formato de Hola de los datos.
* [Crear tabla externa (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify definición de la tabla de Hola y la ubicación de Hola datos.

Ejecute esta consulta en la base de datos de Almacenamiento de datos SQL. Creará una tabla externa denominada DimDate2External en el esquema de dbo de Hola que señala toohello DimDate2.txt los datos de ejemplo en el almacenamiento de blobs de Azure Hola.

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


En el Explorador de objetos de SQL Server en Visual Studio, puede ver el formato de archivo externo de hello, origen de datos externo y tabla de DimDate2External Hola.

![Vea la tabla externa](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>Paso 3: Carga de datos en Almacenamiento de datos SQL
Una vez que se crea la tabla externa de hello, puede cargar los datos de hello en una tabla nueva o insertar en una tabla existente.

* datos de hello tooload en una nueva tabla, ejecute hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrucción. nueva tabla de Hello tiene columnas Hola mencionen en consulta Hola. tipos de datos de Hola de columnas de hello coincidirá con tipos de datos de hello en la definición de la tabla externa de Hola.
* datos de hello tooload en una tabla existente, use hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrucción.

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Paso 4: Crear estadísticas de los datos recién cargados
Almacenamiento de datos SQL no crea ni actualiza automáticamente las estadísticas. Por lo tanto, rendimiento de las consultas alta tooachieve, es importante toocreate estadísticas de cada columna de cada tabla después de hello cargar por primera vez. También es importante tooupdate estadísticas después de realizar cambios sustanciales en datos Hola.

Este ejemplo crea estadísticas de columna única en la nueva tabla de DimDate2 Hola.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

más información, consulte toolearn [estadísticas][Statistics].  

## <a name="next-steps"></a>Pasos siguientes
Vea hello [Guía de PolyBase] [ PolyBase guide] para obtener más información que debe conocer a medida que desarrolla una solución que usa PolyBase.

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
