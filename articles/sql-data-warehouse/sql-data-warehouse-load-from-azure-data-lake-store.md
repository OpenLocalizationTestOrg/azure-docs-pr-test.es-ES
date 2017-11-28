---
title: "aaaLoad - almacenamiento de datos del almacén de Azure Data Lake tooSQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tablas externas de PolyBase de toouse datos tooload de almacén de Data Lake de Azure en almacenamiento de datos de SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="57e2d-103">Carga de datos de Azure Data Lake Store en SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="57e2d-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="57e2d-104">Este documento ofrece todos los pasos necesarios tooload sus propios datos desde el almacén de Lake datos de Azure (ADLS) en almacenamiento de datos SQL mediante PolyBase.</span><span class="sxs-lookup"><span data-stu-id="57e2d-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="57e2d-105">Mientras estás toorun capaz de "ad hoc" consultas sobre datos de hello almacenados en ADLS con tablas externas de hello, como práctica recomendada se recomienda importar datos de Hola a Hola almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="57e2d-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="57e2d-106">Estimación del tiempo: 10 minutos, suponiendo que dispone de los requisitos previos de hello necesita toocomplete.</span><span class="sxs-lookup"><span data-stu-id="57e2d-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="57e2d-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="57e2d-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="57e2d-108">Crear tooload de objetos de base de datos externa desde el almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="57e2d-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="57e2d-109">Conectar tooan Lake almacén de directorio de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="57e2d-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="57e2d-110">Cargar datos en Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="57e2d-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="57e2d-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="57e2d-111">Before you begin</span></span>
<span data-ttu-id="57e2d-112">toorun este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="57e2d-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="57e2d-113">Azure toouse de aplicación de Active Directory para la autenticación de servicio al servicio.</span><span class="sxs-lookup"><span data-stu-id="57e2d-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="57e2d-114">toocreate, siga [autenticación de Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="57e2d-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="57e2d-115">Necesita Id. de cliente de hello, clave y valor de punto de conexión de símbolo (token) de OAuth2.0 de su tooyour de tooconnect de Active Directory Application Azure Data Lake de almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="57e2d-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="57e2d-116">Detalles de cómo tooget estos valores son en vínculo Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="57e2d-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="57e2d-117">Tenga en cuenta para el registro de aplicación de Azure Active Directory usar hello 'Identificador de la aplicación' como Hola identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="57e2d-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="57e2d-118">SQL Server Management Studio o SQL Server Data Tools, toodownload SSMS y conectarse consulte [SSMS de consulta](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="57e2d-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="57e2d-119">Toocreate uno de un almacén de datos de SQL Azure, siga: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="57e2d-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="57e2d-120">Una instancia de Azure Data Lake Store, con o sin cifrado habilitado.</span><span class="sxs-lookup"><span data-stu-id="57e2d-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="57e2d-121">uno siga de toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="57e2d-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="57e2d-122">Configurar origen de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="57e2d-122">Configure hello data source</span></span>
<span data-ttu-id="57e2d-123">PolyBase usa la ubicación de T-SQL objetos externos toodefine hello y atributos de datos externos de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="57e2d-124">objetos externos de Hola se almacenan en el almacén de datos SQL y referencia de los datos de hello que TH se almacena externamente.</span><span class="sxs-lookup"><span data-stu-id="57e2d-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="57e2d-125">Creación de una credencial</span><span class="sxs-lookup"><span data-stu-id="57e2d-125">Create a credential</span></span>
<span data-ttu-id="57e2d-126">tooaccess su Azure Data Lake almacenar, necesitará toocreate una clave maestra de base de datos tooencrypt su secreto de credencial usado en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="57e2d-127">A continuación, crear una credencial de ámbito de la base de datos, que almacena las credenciales principal del servicio Hola configuradas en AAD.</span><span class="sxs-lookup"><span data-stu-id="57e2d-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="57e2d-128">Para aquellos que han utilizado PolyBase tooconnect tooWindows Blobs de almacenamiento de Azure, tenga en cuenta esa credencial Hola sintaxis es diferente.</span><span class="sxs-lookup"><span data-stu-id="57e2d-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="57e2d-129">tooconnect tooAzure almacén de Data Lake, debe **primer** crear una aplicación de Azure Active Directory, cree una clave de acceso y conceda recursos de Azure Data Lake de hello aplicación acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="57e2d-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="57e2d-130">Instrucitons tooperform estos pasos se encuentran [aquí](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="57e2d-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a><span data-ttu-id="57e2d-131">Crear origen de datos externo de Hola</span><span class="sxs-lookup"><span data-stu-id="57e2d-131">Create hello external data source</span></span>
<span data-ttu-id="57e2d-132">Utilícelo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando ubicación de hello toostore de datos de Hola y tipo de Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="57e2d-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="57e2d-133">Puede encontrar Hola ADL URI en hello portal de Azure y www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="57e2d-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="57e2d-134">Configuración del formato de datos</span><span class="sxs-lookup"><span data-stu-id="57e2d-134">Configure data format</span></span>
<span data-ttu-id="57e2d-135">datos de hello tooimport de ADLS, deberá toospecify formato de archivo externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="57e2d-136">Este comando no tiene opciones específicas del formato toodescribe los datos.</span><span class="sxs-lookup"><span data-stu-id="57e2d-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="57e2d-137">A continuación se muestra un ejemplo de un formato de archivo utilizado habitualmente que es un archivo de texto delimitado por canalización.</span><span class="sxs-lookup"><span data-stu-id="57e2d-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="57e2d-138">Examine la documentación de T-SQL para obtener una lista completa de [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="57e2d-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="57e2d-139">Crear tablas externas de Hola</span><span class="sxs-lookup"><span data-stu-id="57e2d-139">Create hello external tables</span></span>
<span data-ttu-id="57e2d-140">Ahora que ha especificado el formato de origen y el archivo de datos de hello, son tablas externas de hello toocreate listo.</span><span class="sxs-lookup"><span data-stu-id="57e2d-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="57e2d-141">Las tablas externas indican cómo se interactúa con los datos externos.</span><span class="sxs-lookup"><span data-stu-id="57e2d-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="57e2d-142">PolyBase usa tooread de recorrido de directorio recursiva todos los archivos de todos los subdirectorios del directorio de hello especificado en el parámetro de ubicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="57e2d-143">Además, Hola de ejemplo siguiente muestra cómo toocreate Hola objeto.</span><span class="sxs-lookup"><span data-stu-id="57e2d-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="57e2d-144">Necesita toocustomize Hola instrucción toowork con datos, hello en ADLS.</span><span class="sxs-lookup"><span data-stu-id="57e2d-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a><span data-ttu-id="57e2d-145">Consideraciones de las tablas externas</span><span class="sxs-lookup"><span data-stu-id="57e2d-145">External Table Considerations</span></span>
<span data-ttu-id="57e2d-146">Crear una tabla externa es fácil, pero hay algunos matices que necesitan toobe descrito.</span><span class="sxs-lookup"><span data-stu-id="57e2d-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="57e2d-147">La carga de datos con PolyBase está fuertemente tipada.</span><span class="sxs-lookup"><span data-stu-id="57e2d-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="57e2d-148">Esto significa que cada fila de datos de hello ingeridos que debe satisfacer definición de esquema de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="57e2d-149">Si una fila determinada no coincide con la definición de esquema de hello, fila Hola puede rechazarse desde carga Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="57e2d-150">Hello REJECT_TYPE REJECT_VALUE opciones y le permiten toodefine el número de filas o el porcentaje de datos de Hola debe estar presente en la tabla final Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="57e2d-151">Durante la carga, si se alcanza el valor de rechazo de hello, Hola carga sufre un error.</span><span class="sxs-lookup"><span data-stu-id="57e2d-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="57e2d-152">causa más común de Hola de filas rechazadas es una inconsistencia de definición de esquema.</span><span class="sxs-lookup"><span data-stu-id="57e2d-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="57e2d-153">Por ejemplo, si una columna no se especifica incorrectamente esquema Hola de int cuando los datos de hello en el archivo hello están una cadena, cada fila se producirá un error tooload.</span><span class="sxs-lookup"><span data-stu-id="57e2d-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="57e2d-154">Hola ubicación especifica el directorio de nivel superior de Hola que desea tooread datos de.</span><span class="sxs-lookup"><span data-stu-id="57e2d-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="57e2d-155">En este caso, si hubiera subdirectorios /DimProduct/ PolyBase podrían importar todos los datos de hello en subdirectorios de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="57e2d-156">Cargar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="57e2d-156">Load hello data</span></span>
<span data-ttu-id="57e2d-157">datos de tooload de almacén de Azure Data Lake usar hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrucción.</span><span class="sxs-lookup"><span data-stu-id="57e2d-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="57e2d-158">Cargando la CTAS usa Hola fuertemente tipado tabla externa que ha creado.</span><span class="sxs-lookup"><span data-stu-id="57e2d-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="57e2d-159">CTAS crea una nueva tabla y lo rellena con resultados de Hola de una instrucción select.</span><span class="sxs-lookup"><span data-stu-id="57e2d-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="57e2d-160">CTAS define Hola nueva tabla toohave Hola mismos tipos de datos y columnas como resultados de Hola de hello instrucción select.</span><span class="sxs-lookup"><span data-stu-id="57e2d-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="57e2d-161">Si selecciona todas las columnas de hello en una tabla externa, tabla nueva hello es una réplica de columnas de Hola y tipos de datos en la tabla externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="57e2d-162">En este ejemplo, vamos a crear una tabla de hash distribuida llamada DimProduct desde nuestra tabla externa DimProduct_external.</span><span class="sxs-lookup"><span data-stu-id="57e2d-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="57e2d-163">Optimización de compresión de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="57e2d-163">Optimize columnstore compression</span></span>
<span data-ttu-id="57e2d-164">De forma predeterminada, almacenamiento de datos de SQL almacena la tabla de Hola como un índice de almacén de columnas agrupado.</span><span class="sxs-lookup"><span data-stu-id="57e2d-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="57e2d-165">Una vez completada una carga, algunas de las filas de datos de hello podrían no va a comprimir con almacén de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="57e2d-166">Existen varios motivos por los que esto puede ocurrir.</span><span class="sxs-lookup"><span data-stu-id="57e2d-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="57e2d-167">más información, consulte toolearn [administrar índices de almacén de columnas][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="57e2d-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="57e2d-168">rendimiento de las consultas toooptimize y compresión de almacén de columnas después de una carga, vuelva a generar toocompress de índice de almacén de columnas de hello tabla tooforce Hola todas las filas de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="57e2d-169">Para obtener más información sobre el mantenimiento de índices de almacén de columnas, vea hello [administrar índices de almacén de columnas] [ manage columnstore indexes] artículo.</span><span class="sxs-lookup"><span data-stu-id="57e2d-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="57e2d-170">Optimización de estadísticas</span><span class="sxs-lookup"><span data-stu-id="57e2d-170">Optimize statistics</span></span>
<span data-ttu-id="57e2d-171">Es mejor estadísticas de columna única de toocreate inmediatamente después de una carga.</span><span class="sxs-lookup"><span data-stu-id="57e2d-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="57e2d-172">Hay algunas opciones para las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="57e2d-172">There are some choices for statistics.</span></span> <span data-ttu-id="57e2d-173">Por ejemplo, si crea estadísticas de columna única en todas las columnas puede tardar un toorebuild mucho tiempo todas las estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="57e2d-174">Si sabe que las columnas que no van toobe predicados de consulta, puede ir creando estadísticas sobre esas columnas.</span><span class="sxs-lookup"><span data-stu-id="57e2d-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="57e2d-175">Si decide toocreate estadísticas de columna única en todas las columnas de cada tabla, puede usar el ejemplo de código de procedimiento almacenado Hola `prc_sqldw_create_stats` en hello [estadísticas] [ statistics] artículo.</span><span class="sxs-lookup"><span data-stu-id="57e2d-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="57e2d-176">Hola siguiente ejemplo es un buen punto de partida para crear las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="57e2d-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="57e2d-177">Crea estadísticas de columna única en cada columna de tabla de dimensiones de Hola y en cada columna de combinación en las tablas de hechos Hola.</span><span class="sxs-lookup"><span data-stu-id="57e2d-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="57e2d-178">Siempre puede agregar columnas de la tabla de hechos de uno o varias columnas de estadísticas tooother más adelante.</span><span class="sxs-lookup"><span data-stu-id="57e2d-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="57e2d-179">Logro conseguido.</span><span class="sxs-lookup"><span data-stu-id="57e2d-179">Achievement unlocked!</span></span>
<span data-ttu-id="57e2d-180">Ha cargado correctamente datos en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="57e2d-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="57e2d-181">Buen trabajo.</span><span class="sxs-lookup"><span data-stu-id="57e2d-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="57e2d-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57e2d-182">Next Steps</span></span>
<span data-ttu-id="57e2d-183">La carga de datos es Hola primer paso toodeveloping una solución de almacenamiento de datos mediante almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="57e2d-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="57e2d-184">Consulte nuestros recursos de desarrollo en [Tablas](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) y [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="57e2d-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
