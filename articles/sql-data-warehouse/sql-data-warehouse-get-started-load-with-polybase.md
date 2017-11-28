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
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="3bb28-103">Carga de datos con PolyBase en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3bb28-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bb28-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="3bb28-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="3bb28-105">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="3bb28-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="3bb28-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="3bb28-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="3bb28-107">BCP</span><span class="sxs-lookup"><span data-stu-id="3bb28-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="3bb28-108">Este tutorial se muestra cómo los datos de tooload en almacenamiento de datos de SQL con AzCopy y PolyBase.</span><span class="sxs-lookup"><span data-stu-id="3bb28-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="3bb28-109">Cuando termine, sabrá cómo:</span><span class="sxs-lookup"><span data-stu-id="3bb28-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="3bb28-110">Usar el almacenamiento de blobs de AzCopy toocopy datos tooAzure</span><span class="sxs-lookup"><span data-stu-id="3bb28-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="3bb28-111">Crear objetos de base de datos de Hola de toodefine</span><span class="sxs-lookup"><span data-stu-id="3bb28-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="3bb28-112">Ejecutar una consulta de T-SQL tooload Hola datos</span><span class="sxs-lookup"><span data-stu-id="3bb28-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3bb28-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3bb28-113">Prerequisites</span></span>
<span data-ttu-id="3bb28-114">toostep a través de este tutorial, necesita</span><span class="sxs-lookup"><span data-stu-id="3bb28-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="3bb28-115">Una base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3bb28-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="3bb28-116">Una cuenta de almacenamiento de Azure del tipo Almacenamiento con redundancia local estándar (LRS estándar), Almacenamiento con redundancia geográfica estándar (GRS estándar) o Almacenamiento con redundancia geográfica de acceso de lectura estándar  (RAGRS estándar).</span><span class="sxs-lookup"><span data-stu-id="3bb28-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="3bb28-117">La utilidad de línea de comandos AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3bb28-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="3bb28-118">Descargue e instale hello [versión más reciente de AzCopy] [ latest version of AzCopy] que se instala con hello herramientas de almacenamiento de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb28-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Herramientas de almacenamiento de Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="3bb28-120">Paso 1: Agregar almacenamiento de blobs de tooAzure de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3bb28-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="3bb28-121">Datos de pedidos tooload, necesitamos tooput algunos datos de ejemplo en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb28-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="3bb28-122">En este paso, se rellena un almacenamiento de blobs de Azure con datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3bb28-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="3bb28-123">Más adelante, usaremos PolyBase tooload estos datos de ejemplo en la base de datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3bb28-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="3bb28-124">A.</span><span class="sxs-lookup"><span data-stu-id="3bb28-124">A.</span></span> <span data-ttu-id="3bb28-125">Preparación de un archivo de texto de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3bb28-125">Prepare a sample text file</span></span>
<span data-ttu-id="3bb28-126">tooprepare un archivo de texto de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3bb28-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="3bb28-127">Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="3bb28-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="3bb28-128">Guarde este directorio temporal de tooyour local como % temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="3bb28-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="3bb28-129">B.</span><span class="sxs-lookup"><span data-stu-id="3bb28-129">B.</span></span> <span data-ttu-id="3bb28-130">Búsqueda del punto de conexión del servicio BLOB</span><span class="sxs-lookup"><span data-stu-id="3bb28-130">Find your blob service endpoint</span></span>
<span data-ttu-id="3bb28-131">toofind su extremo de servicio blob:</span><span class="sxs-lookup"><span data-stu-id="3bb28-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="3bb28-132">Desde el Portal de Azure Hola seleccione **examinar** > **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="3bb28-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="3bb28-133">Haga clic en la cuenta de almacenamiento de hello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="3bb28-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="3bb28-134">En la hoja de la cuenta de almacenamiento de hello, haga clic en Blobs</span><span class="sxs-lookup"><span data-stu-id="3bb28-134">In hello Storage account blade, click Blobs</span></span>
   
    ![Haga clic en Blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="3bb28-136">Guardar la dirección URL del punto de conexión del servicio BLOB para usarla más adelante.</span><span class="sxs-lookup"><span data-stu-id="3bb28-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Punto de conexión del servicio BLOB](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="3bb28-138">C.</span><span class="sxs-lookup"><span data-stu-id="3bb28-138">C.</span></span> <span data-ttu-id="3bb28-139">Búsqueda de la clave de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="3bb28-139">Find your Azure storage key</span></span>
<span data-ttu-id="3bb28-140">toofind su clave de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="3bb28-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="3bb28-141">En hello Portal de Azure, seleccione **examinar** > **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="3bb28-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="3bb28-142">Haga clic en la cuenta de almacenamiento de hello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="3bb28-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="3bb28-143">Seleccione **Toda la configuración** > **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="3bb28-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="3bb28-144">Haga clic en hello copia cuadro toocopy entre el Portapapeles de toohello de claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="3bb28-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Copie la clave de almacenamiento de Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="3bb28-146">D.</span><span class="sxs-lookup"><span data-stu-id="3bb28-146">D.</span></span> <span data-ttu-id="3bb28-147">Copie el almacenamiento de blobs de tooAzure de archivo de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="3bb28-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="3bb28-148">toocopy el almacenamiento de blobs de tooAzure de datos:</span><span class="sxs-lookup"><span data-stu-id="3bb28-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="3bb28-149">Abra un símbolo del sistema y cambie el directorio de instalación de directorios toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3bb28-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="3bb28-150">Este comando cambia el directorio de instalación predeterminado de toohello en un cliente de Windows de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="3bb28-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="3bb28-151">Ejecute hello siguiente archivo de comandos tooupload Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="3bb28-152">Especifique la dirección URL del punto de conexión del servicio BLOB de <blob service endpoint URL> y la clave de la cuenta de almacenamiento de Azure de <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="3bb28-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="3bb28-153">Vea también [Getting Started with Hola utilidad de línea de comandos de AzCopy][Getting Started with hello AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="3bb28-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="3bb28-154">E.</span><span class="sxs-lookup"><span data-stu-id="3bb28-154">E.</span></span> <span data-ttu-id="3bb28-155">Exploración del contenedor de almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="3bb28-155">Explore your blob storage container</span></span>
<span data-ttu-id="3bb28-156">archivo de hello toosee cargado tooblob almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="3bb28-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="3bb28-157">Volver atrás tooyour módulo de servicio de Blob.</span><span class="sxs-lookup"><span data-stu-id="3bb28-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="3bb28-158">En Contenedores, haga doble clic en **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="3bb28-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="3bb28-159">datos de tooyour de tooexplore Hola ruta de acceso, haga clic en la carpeta de hello **datedimension** y verá el archivo cargado **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="3bb28-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="3bb28-160">Haga clic en Propiedades de tooview, **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="3bb28-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="3bb28-161">Tenga en cuenta que en la hoja de propiedades de Blob de hello, puede descargar o eliminar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="3bb28-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Vea el blob de almacenamiento de Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="3bb28-163">Paso 2: Crear una tabla externa para datos de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="3bb28-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="3bb28-164">En esta sección se creará una tabla externa que define los datos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="3bb28-165">PolyBase usa datos de tablas externas tooaccess en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb28-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="3bb28-166">Puesto que los datos de hello no se almacenan en el almacén de datos SQL, PolyBase controla datos externos de autenticación toohello mediante una credencial de ámbito de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3bb28-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="3bb28-167">ejemplo de Hola en este paso usa estos toocreate de instrucciones de Transact-SQL una tabla externa.</span><span class="sxs-lookup"><span data-stu-id="3bb28-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="3bb28-168">[Crear la clave maestra (Transact-SQL)] [ Create Master Key (Transact-SQL)] credencial con ámbito de secreto de hello tooencrypt de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3bb28-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="3bb28-169">[Crear credencial con ámbito de base de datos (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify información de autenticación para su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb28-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="3bb28-170">[Crear origen de datos externo (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify ubicación de Hola de su almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb28-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="3bb28-171">[Crear formato de archivo externo (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify formato de Hola de los datos.</span><span class="sxs-lookup"><span data-stu-id="3bb28-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="3bb28-172">[Crear tabla externa (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify definición de la tabla de Hola y la ubicación de Hola datos.</span><span class="sxs-lookup"><span data-stu-id="3bb28-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="3bb28-173">Ejecute esta consulta en la base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3bb28-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="3bb28-174">Creará una tabla externa denominada DimDate2External en el esquema de dbo de Hola que señala toohello DimDate2.txt los datos de ejemplo en el almacenamiento de blobs de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


<span data-ttu-id="3bb28-175">En el Explorador de objetos de SQL Server en Visual Studio, puede ver el formato de archivo externo de hello, origen de datos externo y tabla de DimDate2External Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Vea la tabla externa](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="3bb28-177">Paso 3: Carga de datos en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3bb28-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="3bb28-178">Una vez que se crea la tabla externa de hello, puede cargar los datos de hello en una tabla nueva o insertar en una tabla existente.</span><span class="sxs-lookup"><span data-stu-id="3bb28-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="3bb28-179">datos de hello tooload en una nueva tabla, ejecute hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrucción.</span><span class="sxs-lookup"><span data-stu-id="3bb28-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="3bb28-180">nueva tabla de Hello tiene columnas Hola mencionen en consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="3bb28-181">tipos de datos de Hola de columnas de hello coincidirá con tipos de datos de hello en la definición de la tabla externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="3bb28-182">datos de hello tooload en una tabla existente, use hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrucción.</span><span class="sxs-lookup"><span data-stu-id="3bb28-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="3bb28-183">Paso 4: Crear estadísticas de los datos recién cargados</span><span class="sxs-lookup"><span data-stu-id="3bb28-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="3bb28-184">Almacenamiento de datos SQL no crea ni actualiza automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="3bb28-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="3bb28-185">Por lo tanto, rendimiento de las consultas alta tooachieve, es importante toocreate estadísticas de cada columna de cada tabla después de hello cargar por primera vez.</span><span class="sxs-lookup"><span data-stu-id="3bb28-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="3bb28-186">También es importante tooupdate estadísticas después de realizar cambios sustanciales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="3bb28-187">Este ejemplo crea estadísticas de columna única en la nueva tabla de DimDate2 Hola.</span><span class="sxs-lookup"><span data-stu-id="3bb28-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="3bb28-188">más información, consulte toolearn [estadísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="3bb28-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3bb28-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bb28-189">Next steps</span></span>
<span data-ttu-id="3bb28-190">Vea hello [Guía de PolyBase] [ PolyBase guide] para obtener más información que debe conocer a medida que desarrolla una solución que usa PolyBase.</span><span class="sxs-lookup"><span data-stu-id="3bb28-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

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
