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
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Carga de datos de Azure Data Lake Store en SQL Data Warehouse
Este documento ofrece todos los pasos necesarios tooload sus propios datos desde el almacén de Lake datos de Azure (ADLS) en almacenamiento de datos SQL mediante PolyBase.
Mientras estás toorun capaz de "ad hoc" consultas sobre datos de hello almacenados en ADLS con tablas externas de hello, como práctica recomendada se recomienda importar datos de Hola a Hola almacenamiento de datos de SQL.
Estimación del tiempo: 10 minutos, suponiendo que dispone de los requisitos previos de hello necesita toocomplete.
En este tutorial, aprenderá a:

1. Crear tooload de objetos de base de datos externa desde el almacén de Azure Data Lake.
2. Conectar tooan Lake almacén de directorio de datos de Azure.
3. Cargar datos en Azure SQL Data Warehouse

## <a name="before-you-begin"></a>Antes de empezar
toorun este tutorial, necesita:

* Azure toouse de aplicación de Active Directory para la autenticación de servicio al servicio. toocreate, siga [autenticación de Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> Necesita Id. de cliente de hello, clave y valor de punto de conexión de símbolo (token) de OAuth2.0 de su tooyour de tooconnect de Active Directory Application Azure Data Lake de almacenamiento de datos de SQL. Detalles de cómo tooget estos valores son en vínculo Hola anterior.
>Tenga en cuenta para el registro de aplicación de Azure Active Directory usar hello 'Identificador de la aplicación' como Hola identificador de cliente.

* SQL Server Management Studio o SQL Server Data Tools, toodownload SSMS y conectarse consulte [SSMS de consulta](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Toocreate uno de un almacén de datos de SQL Azure, siga: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Una instancia de Azure Data Lake Store, con o sin cifrado habilitado. uno siga de toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Configurar origen de datos de Hola
PolyBase usa la ubicación de T-SQL objetos externos toodefine hello y atributos de datos externos de Hola. objetos externos de Hola se almacenan en el almacén de datos SQL y referencia de los datos de hello que TH se almacena externamente.


###  <a name="create-a-credential"></a>Creación de una credencial
tooaccess su Azure Data Lake almacenar, necesitará toocreate una clave maestra de base de datos tooencrypt su secreto de credencial usado en el paso siguiente Hola.
A continuación, crear una credencial de ámbito de la base de datos, que almacena las credenciales principal del servicio Hola configuradas en AAD. Para aquellos que han utilizado PolyBase tooconnect tooWindows Blobs de almacenamiento de Azure, tenga en cuenta esa credencial Hola sintaxis es diferente.
tooconnect tooAzure almacén de Data Lake, debe **primer** crear una aplicación de Azure Active Directory, cree una clave de acceso y conceda recursos de Azure Data Lake de hello aplicación acceso toohello. Instrucitons tooperform estos pasos se encuentran [aquí](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

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


### <a name="create-hello-external-data-source"></a>Crear origen de datos externo de Hola
Utilícelo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando ubicación de hello toostore de datos de Hola y tipo de Hola de datos.
Puede encontrar Hola ADL URI en hello portal de Azure y www.portal.azure.com.

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



## <a name="configure-data-format"></a>Configuración del formato de datos
datos de hello tooimport de ADLS, deberá toospecify formato de archivo externo de Hola. Este comando no tiene opciones específicas del formato toodescribe los datos.
A continuación se muestra un ejemplo de un formato de archivo utilizado habitualmente que es un archivo de texto delimitado por canalización.
Examine la documentación de T-SQL para obtener una lista completa de [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]

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

## <a name="create-hello-external-tables"></a>Crear tablas externas de Hola
Ahora que ha especificado el formato de origen y el archivo de datos de hello, son tablas externas de hello toocreate listo. Las tablas externas indican cómo se interactúa con los datos externos. PolyBase usa tooread de recorrido de directorio recursiva todos los archivos de todos los subdirectorios del directorio de hello especificado en el parámetro de ubicación de Hola. Además, Hola de ejemplo siguiente muestra cómo toocreate Hola objeto. Necesita toocustomize Hola instrucción toowork con datos, hello en ADLS.

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

## <a name="external-table-considerations"></a>Consideraciones de las tablas externas
Crear una tabla externa es fácil, pero hay algunos matices que necesitan toobe descrito.

La carga de datos con PolyBase está fuertemente tipada. Esto significa que cada fila de datos de hello ingeridos que debe satisfacer definición de esquema de tabla de Hola.
Si una fila determinada no coincide con la definición de esquema de hello, fila Hola puede rechazarse desde carga Hola.

Hello REJECT_TYPE REJECT_VALUE opciones y le permiten toodefine el número de filas o el porcentaje de datos de Hola debe estar presente en la tabla final Hola.
Durante la carga, si se alcanza el valor de rechazo de hello, Hola carga sufre un error. causa más común de Hola de filas rechazadas es una inconsistencia de definición de esquema.
Por ejemplo, si una columna no se especifica incorrectamente esquema Hola de int cuando los datos de hello en el archivo hello están una cadena, cada fila se producirá un error tooload.

Hola ubicación especifica el directorio de nivel superior de Hola que desea tooread datos de.
En este caso, si hubiera subdirectorios /DimProduct/ PolyBase podrían importar todos los datos de hello en subdirectorios de Hola.

## <a name="load-hello-data"></a>Cargar datos de Hola
datos de tooload de almacén de Azure Data Lake usar hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrucción. Cargando la CTAS usa Hola fuertemente tipado tabla externa que ha creado.

CTAS crea una nueva tabla y lo rellena con resultados de Hola de una instrucción select. CTAS define Hola nueva tabla toohave Hola mismos tipos de datos y columnas como resultados de Hola de hello instrucción select. Si selecciona todas las columnas de hello en una tabla externa, tabla nueva hello es una réplica de columnas de Hola y tipos de datos en la tabla externa de Hola.

En este ejemplo, vamos a crear una tabla de hash distribuida llamada DimProduct desde nuestra tabla externa DimProduct_external.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Optimización de compresión de almacén de columnas
De forma predeterminada, almacenamiento de datos de SQL almacena la tabla de Hola como un índice de almacén de columnas agrupado. Una vez completada una carga, algunas de las filas de datos de hello podrían no va a comprimir con almacén de columnas de Hola.  Existen varios motivos por los que esto puede ocurrir. más información, consulte toolearn [administrar índices de almacén de columnas][manage columnstore indexes].

rendimiento de las consultas toooptimize y compresión de almacén de columnas después de una carga, vuelva a generar toocompress de índice de almacén de columnas de hello tabla tooforce Hola todas las filas de Hola.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Para obtener más información sobre el mantenimiento de índices de almacén de columnas, vea hello [administrar índices de almacén de columnas] [ manage columnstore indexes] artículo.

## <a name="optimize-statistics"></a>Optimización de estadísticas
Es mejor estadísticas de columna única de toocreate inmediatamente después de una carga. Hay algunas opciones para las estadísticas. Por ejemplo, si crea estadísticas de columna única en todas las columnas puede tardar un toorebuild mucho tiempo todas las estadísticas de Hola. Si sabe que las columnas que no van toobe predicados de consulta, puede ir creando estadísticas sobre esas columnas.

Si decide toocreate estadísticas de columna única en todas las columnas de cada tabla, puede usar el ejemplo de código de procedimiento almacenado Hola `prc_sqldw_create_stats` en hello [estadísticas] [ statistics] artículo.

Hola siguiente ejemplo es un buen punto de partida para crear las estadísticas. Crea estadísticas de columna única en cada columna de tabla de dimensiones de Hola y en cada columna de combinación en las tablas de hechos Hola. Siempre puede agregar columnas de la tabla de hechos de uno o varias columnas de estadísticas tooother más adelante.


## <a name="achievement-unlocked"></a>Logro conseguido.
Ha cargado correctamente datos en Azure SQL Data Warehouse. Buen trabajo.

##<a name="next-steps"></a>Pasos siguientes
La carga de datos es Hola primer paso toodeveloping una solución de almacenamiento de datos mediante almacenamiento de datos SQL. Consulte nuestros recursos de desarrollo en [Tablas](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) y [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


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
