---
title: datos de aaaCopy hacia/desde el almacenamiento de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy datos hacia y desde el almacenamiento de datos de SQL Azure mediante Data Factory de Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Copiar datos tooand de almacenamiento de datos de SQL Azure mediante Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove de almacenamiento de datos de SQL Azure. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.  

> [!TIP]
> tooachieve el mejor rendimiento, utilice datos de PolyBase tooload en almacenamiento de datos de SQL Azure. Hola [datos de uso PolyBase tooload en almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sección con información detallada. Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede copiar datos **de almacenamiento de datos de SQL Azure** toohello siguientes almacenes de datos:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Puede copiar los datos de hello siguientes almacenes de datos **tooAzure almacenamiento de datos SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> Cuando se copian datos desde SQL Server o base de datos de SQL Azure tooAzure almacenamiento de datos de SQL, si no existe la tabla de hello en el almacén de destino de hello, factoría de datos puede crear automáticamente tabla hello en el almacén de datos de SQL mediante Hola un esquema de tabla de hello en origen Hola almacén de datos. Vea [Creación automática de tablas](#auto-table-creation) para obtener más información.

## <a name="supported-authentication-type"></a>Tipos de autenticación que se admiten
El conector de Azure SQL Data Warehouse admite la autenticación básica.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos con Azure SQL Data Warehouse como origen o destino mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización que copia los datos de almacenamiento de datos de SQL Azure es el Asistente para datos de copia de toouse Hola. Vea [Tutorial: cargar datos en almacenamiento de datos de SQL con factoría de datos](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o más canalizaciones. 
2. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink. Por ejemplo, si va a copiar datos desde un almacén de datos de Azure blob storage tooan SQL Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de almacenamiento de datos de SQL Azure. Para las propiedades de servicio vinculado que son específico tooAzure almacenamiento de datos SQL, consulte [vinculado propiedades del servicio](#linked-service-properties) sección. 
3. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola. Y crear otra tabla de hello toospecify de conjunto de datos en almacenamiento de datos de SQL Azure Hola que contiene los datos de hello copiados desde el almacenamiento de blobs de Hola. Para las propiedades de conjunto de datos que son específico tooAzure almacenamiento de datos SQL, consulte [propiedades de conjunto de datos](#dataset-properties) sección.
4. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y SqlDWSink como un receptor para la actividad de copia de Hola. De forma similar, si va a copiar desde el almacenamiento de datos de SQL Azure tooAzure almacenamiento de blobs, usar SqlDWSource y BlobSink de actividad de copia de Hola. Para copiar propiedades de actividad que son específico tooAzure almacenamiento de datos SQL, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección. Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy hacia/desde un almacén de datos de SQL Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sección de este artículo.

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure almacenamiento de datos SQL:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooAzure servicio de almacenamiento de datos de SQL vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **AzureSqlDW** |Sí |
| connectionString |Especifique la información necesaria la instancia de almacenamiento de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola. Solo se admite la autenticación básica. |Sí |

> [!IMPORTANT]
> Configurar [Firewall de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) y Hola servidor de base de datos demasiado[permitir servidor de servicios de Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Además, si va a copiar datos tooAzure almacenamiento de datos SQL de incluido Azure fuera de orígenes de datos local con la puerta de enlace de generador de datos, configurar el intervalo de direcciones IP adecuado para la máquina de Hola que está enviando datos tooAzure almacenamiento de datos SQL.

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola **typeProperties** sección Hola conjunto de datos de tipo **AzureSqlDWTable** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola o vista de base de datos de almacenamiento de datos de SQL Azure de Hola Hola servicio vinculado hace referencia a. |Sí |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

> [!NOTE]
> Hola actividad de copia toma solo una entrada y produce un único resultado.

Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

### <a name="sqldwsource"></a>SqlDWSource
Cuando el origen es del tipo **SqlDWSource**, Hola propiedades siguientes está disponible en **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: select * from MyTable. |No |
| sqlReaderStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola. |Nombre del programa Hola a procedimiento almacenado. Hola última instrucción de SQL debe ser una instrucción SELECT en el procedimiento almacenado de Hola. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |

Si hello **sqlReaderQuery** se especifica para hello SqlDWSource, hello actividad de copia se ejecuta esta consulta contra Hola datos de almacenamiento de datos de SQL Azure origen tooget Hola.

Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).

Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usado un toorun consulta contra Hola almacenamiento de datos de SQL Azure. Ejemplo: `select column1, column2 from mytable`. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.

#### <a name="sqldwsource-example"></a>Ejemplo de SqlDWSource

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
**Hola almacena la definición del procedimiento:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian. Consulte la [sección sobre repetibilidad](#repeatability-during-copy)para más información. |Una instrucción de consulta. |No |
| allowPolyBase |Indica si toouse PolyBase (si procede) en lugar de mecanismo BULKINSERT. <br/><br/> **El uso de PolyBase es Hola recomendado de forma que los datos tooload en almacenamiento de datos de SQL.** Vea [datos de uso PolyBase tooload en almacenamiento de datos de SQL Azure](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sección para las restricciones y los detalles. |True <br/>False (valor predeterminado) |No |
| polyBaseSettings |Un grupo de propiedades que se pueden especificar cuando hello **allowPolybase** propiedad se establece demasiado**true**. |&nbsp; |No |
| rejectValue |Especifica el número de Hola o porcentaje de filas que se pueda rechazar antes de que se produce un error en la consulta de Hola. <br/><br/>Obtener más información acerca de hello PolyBase rechazan opciones Hola **argumentos** sección de [crear tabla externa (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tema. |0 (predeterminado), 1, 2, … |No |
| rejectType |Especifica si se especifica la opción de hello rejectValue como un valor literal o un porcentaje. |Valor (predeterminado), Porcentaje |No |
| rejectSampleValue |Determina el número de Hola de tooretrieve filas antes de hello PolyBase vuelve a calcular el porcentaje de Hola de filas rechazados. |1, 2, … |Sí, si el valor de **rejectType** es **percentage** |
| useTypeDefault |Especifica cómo toohandle valores que falten en archivos delimitados por texto cuando PolyBase recupera datos de archivo de texto hello.<br/><br/>Más información acerca de esta propiedad desde la sección de argumentos de hello en [crear EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (predeterminada) |No |
| writeBatchSize |Inserta los datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize |Entero (número de filas) |No (valor predeterminado = 10000) |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |

#### <a name="sqldwsink-example"></a>Ejemplo de SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>Usar datos de PolyBase tooload en almacenamiento de datos de SQL Azure
Usar **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** es una manera eficaz de cargar grandes cantidades de datos en Azure SQL Data Warehouse con un alto rendimiento. Puede ver grande ganancia en rendimiento hello mediante PolyBase en lugar de mecanismo BULKINSERT Hola predeterminado. Vea la [copia del número de referencia de rendimiento](data-factory-copy-activity-performance.md#performance-reference) con una comparación detallada. Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).

* Si los datos de origen están en **blobs de Azure o almacén de Azure Data Lake**y formato de hello es compatible con PolyBase, puede copiar directamente tooAzure con PolyBase de almacenamiento de datos SQL. Consulte **[Copias directas con PolyBase](#direct-copy-using-polybase)** para detalles.
* Si el almacén de datos de origen y el formato no es compatible originalmente con PolyBase, puede usar hello  **[copia provisionalmente mediante PolyBase](#staged-copy-using-polybase)**  característica en su lugar. También proporciona un mejor rendimiento al convertir datos de hello en formato compatible con PolyBase y almacenar datos de hello en el almacenamiento de blobs de Azure automáticamente. Luego los carga en SQL Data Warehouse.

Conjunto hello `allowPolyBase` propiedad demasiado**true** tal y como se muestra en el siguiente ejemplo para Data Factory de Azure toouse PolyBase toocopy datos en almacenamiento de datos de SQL Azure de Hola. Al establecer allowPolyBase tootrue, puede especificar propiedades específicas de PolyBase con hello `polyBaseSettings` grupo de propiedades. vea hello [SqlDWSink](#SqlDWSink) sección para obtener más información acerca de las propiedades que puede usar con polyBaseSettings.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Copias directas con PolyBase
PolyBase de SQL Data Warehouse admite directamente Azure Blob y Azure Data Lake Store (con la entidad de servicio) como origen y con los requisitos de formato de archivo específico. Si los datos de origen cumplen los criterios de hello descritos en esta sección, puede copiar directamente de tooAzure de almacén de datos de origen que del almacenamiento de datos SQL con PolyBase. De lo contrario, puede usar [Copias almacenadas provisionalmente con PolyBase](#staged-copy-using-polybase).

> [!TIP]
> datos de toocopy de almacenamiento de datos del almacén de Data Lake tooSQL eficazmente, obtener más información en [Data Factory de Azure hace incluso más fácil y cómodo toouncover visión de datos cuando se usa el almacén de Data Lake con almacenamiento de datos de SQL](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Si no se cumplen los requisitos de hello, Data Factory de Azure comprueba la configuración de Hola y vuelve automáticamente mecanismo BULKINSERT toohello Hola para movimiento de datos.

1. El **servicio de origen vinculado** es de tipo **AzureStorage** o **AzureDataLakeStore con autenticación de la entidad de servicio**.  
2. Hola **conjunto de datos de entrada** es de tipo: **AzureBlob** o **AzureDataLakeStore**, y Hola tipo de formato en `type` propiedades es **OrcFormat** , o **TextFormat** con hello siguiendo configuraciones:

   1. `rowDelimiter` debe ser **\n**.
   2. `nullValue`se establece demasiado**una cadena vacía** (""), o `treatEmptyAsNull` se establece demasiado**true**.
   3. `encodingName`se establece demasiado**utf-8**, que es **predeterminado** valor.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader` y `skipLineCount` no se especifican.
   5. `compression` puede ser **no compression**, **GZip** o **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. No hay ningún `skipHeaderLineCount` en **BlobSource** o **AzureDataLakeStore** para la actividad de copia de canalización de Hola Hola.
4. No hay ningún `sliceIdentifierColumnName` en **SqlDWSink** para la actividad de copia de canalización de Hola Hola. (PolyBase garantiza que todos los datos se actualizan o que no se actualiza ninguno en una única ejecución. tooachieve **repetibilidad**, podría utilizar `sqlWriterCleanupScript`).
5. No hay ningún `columnMapping` que se usan en hello asociado en la actividad de copia.

### <a name="staged-copy-using-polybase"></a>Copias almacenadas provisionalmente con PolyBase
Cuando los datos de origen no cumplen los criterios de hello introducidos en la sección anterior de hello, puede habilitar la copia de datos a través de un almacenamiento de blobs de Azure ensayo provisional (no puede ser almacenamiento Premium). En este caso, Data Factory de Azure automáticamente realiza transformaciones en hello toomeet datos formato requisitos de datos de PolyBase y, a continuación, use datos de PolyBase tooload en almacenamiento de datos de SQL y en la última limpieza los datos temporales Hola del almacenamiento de blobs. Consulte [Copias almacenadas provisionalmente](data-factory-copy-activity-performance.md#staged-copy) para más información sobre cómo funciona en general la copia de datos por medio de un blob de Azure de almacenamiento provisional.

> [!NOTE]
> Cuando se copian datos desde un dato local almacenan en almacenamiento de datos de SQL Azure con PolyBase y el almacenamiento provisional, si la versión de Data Management Gateway está por debajo de 2.4, JRE (Java Runtime Environment) es necesario en la puerta de enlace automático que es tootransform usa los datos de origen en el formato correcto. Sugerir que actualizar su tooavoid más reciente de puerta de enlace toohello esta dependencia.
>

toouse esta característica, cree un [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) que hace referencia toohello cuenta de almacenamiento de Azure que tiene el almacenamiento de blobs provisionales de hello, a continuación, especifique hello `enableStaging` y `stagingSettings` propiedades de actividad de copia de Hola como se muestra en el siguiente código de hello:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>Procedimientos recomendados al usar PolyBase
Hello las secciones siguientes proporcionan toohello de prácticas recomendada adicionales que se mencionan en [prácticas recomendadas para el almacenamiento de datos de SQL Azure](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Permiso de base de datos necesario
toouse PolyBase, requiere Hola usuario está tooload usa datos en almacenamiento de datos de SQL se Hola [permiso "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) en base de datos de destino de Hola. Una manera de tooachieve que es tooadd ese usuario como miembro del rol "db_owner". Obtenga información acerca de cómo toodo que siguiendo [en esta sección](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Limitación del tipo de datos y del tamaño de fila
Cargas de Polybase se limitan tooloading ambas filas inferior **1 MB** y no se puede cargar tooVARCHR(MAX), nvarchar (max) o varbinary (max). Consulte demasiado[aquí](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Si tiene datos de origen con filas de un tamaño superior a 1 MB, puede que desee tablas de origen de hello toosplit verticalmente en varios pequeños donde mayor tamaño de fila Hola de cada uno de ellos no supere el límite de Hola. a continuación, se pueden cargar tablas más pequeñas de Hello mediante PolyBase y combinar juntos en el almacén de datos de SQL Azure.

### <a name="sql-data-warehouse-resource-class"></a>Clase de recursos de SQL Data Warehouse
tooachieve mejor rendimiento posible, considere la posibilidad de tooassign mayores recursos clase toohello usuario que se va a usar datos tooload en almacenamiento de datos de SQL a través de PolyBase. Obtenga información acerca de cómo toodo que siguiendo [cambiar un ejemplo de clase del recurso de usuario](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName en Almacenamiento de datos SQL de Azure
Hello tabla siguiente proporciona ejemplos sobre cómo hello toospecify **tableName** propiedad JSON de diversas combinaciones de nombre de esquema y tabla de conjunto de datos.

| Esquema de base de datos | Nombre de tabla | Propiedad JSON tableName |
| --- | --- | --- |
| dbo |MyTable |MyTable o dbo.MyTable o [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable o [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] o [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1].[My.Table] |

Si ve Hola tras error, es posible que un problema con el valor de Hola que especificó para la propiedad tableName de Hola. Consulte tabla Hola Hola forma correcta toospecify valores de propiedad JSON de hello tableName.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Columnas con valores predeterminados
Actualmente, solo acepta la característica de factoría de datos de PolyBase Hola mismo número de columnas como en la tabla de destino de Hola. Supongamos que tiene una tabla con cuatro columnas y una de ellas está definida con un valor predeterminado. datos de entrada de Hello todavía deben contener cuatro columnas. Proporciona un conjunto de datos de entrada de 3 columnas produciría un toohello de error similar siguiente mensaje:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
El valor NULL es una forma especial de valor predeterminado. Si la columna hello es que aceptan valores NULL, Hola entrada datos (blob) para esa columna pudieron estar vacías (no puede faltar de conjunto de datos de entrada de hello). PolyBase, inserta NULL para ellos en hello almacenamiento de datos de SQL Azure.  

## <a name="auto-table-creation"></a>Creación automáticamente de tablas
Si va a usar Asistente para copiar toocopy datos de SQL Server o base de datos de SQL Azure tooAzure hello y almacenamiento de datos SQL tabla correspondiente de la tabla de origen toohello no existen en el almacén de destino de hello, factoría de datos puede crear automáticamente la tabla de Hola Hola almacenamiento de datos mediante el uso de esquema de tabla de origen de Hola.

Factoría de datos crea la tabla de hello en el almacén de destino de hello con hello mismo nombre de la tabla en el almacén de datos de origen de Hola. tipos de datos de Hola para las columnas se eligen en función del Hola después de la asignación de tipos. Si es necesario, realiza toofix de conversiones de tipo las incompatibilidades entre los almacenes de origen y de destino. También se utiliza la distribución Round Robin.

| Tipo de columna de SQL Database de origen | Tipo de columna de SQL DataWarehouse de destino (limitación de tamaño) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| Bit | Bit |
| Decimal | Decimal |
| Numeric | Decimal |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| Binary | Binary |
| Varbinary | Varbinary (arriba too8000) |
| Date | Date |
| DateTime | DateTime |
| DateTime2 | DateTime2 |
| Hora | Hora |
| DateTimeOffset | DateTimeOffset |
| SmallDateTime | SmallDateTime |
| Texto | Varchar (arriba too8000) |
| NText | NVarChar (arriba too4000) |
| Imagen | VarBinary (arriba too8000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NChar | NChar |
| VarChar | VarChar (arriba too8000) |
| NVarChar | NVarChar (arriba too4000) |
| xml | Varchar (arriba too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Asignación de tipos para Almacenamiento de datos SQL de Azure
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Cuando se mueven datos demasiado & de almacenamiento de datos de SQL Azure, hello asignaciones siguientes se usan del tipo de too.NET de tipo SQL y viceversa.

asignación de Hello es el mismo que hello [asignación de tipo de datos de SQL Server para ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).

| Tipo de motor de base de datos SQL Server | Tipo .NET Framework |
| --- | --- |
| bigint |Int64 |
| binary |Byte[] |
| bit |Booleano |
| char |String, Char[] |
| fecha |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimal |Decimal |
| FILESTREAM attribute (varbinary(max)) |Byte[] |
| Float |Doble |
| imagen |Byte[] |
| int |Int32 |
| money |Decimal |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numeric |Decimal |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Decimal |
| sql_variant |Object * |
| text |String, Char[] |
| Twitter en tiempo |timespan |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

También puede asignar columnas de toocolumns de conjunto de datos de origen del conjunto de datos de receptor en la definición de actividad de copia de Hola. Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>Ejemplos JSON para copiar datos tooand de almacenamiento de datos SQL
Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy tooand de datos de almacenamiento de datos de SQL Azure y almacenamiento de blobs de Azure. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Ejemplo: Copiar los datos de Blob del almacenamiento de datos de SQL Azure tooAzure
ejemplo de Hola define Hola siguiendo las entidades de la factoría de datos:

1. Un servicio vinculado de tipo [AzureSqlDW](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlDWTable](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlDWSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de una tabla de blob de tooa de base de datos de almacenamiento de datos de SQL Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado del almacenamiento de datos SQL de Azure:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Servicio vinculado de almacenamiento de blobs de Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Conjunto de datos de entrada del almacenamiento de datos SQL de Azure:**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en el almacén de datos de SQL Azure y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.

Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Actividad de copia en una canalización con SqlDWSource y BlobSink:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlDWSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
> [!NOTE]
> En el ejemplo de Hola, **sqlReaderQuery** se especifica para hello SqlDWSource. Hola actividad de copia ejecuta esta consulta contra Hola datos de almacenamiento de datos de SQL Azure origen tooget Hola.
>
> Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).
>
> Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, columnas de hello definidas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usa una consulta (select column1, column2 de mytable) toorun contra Hola almacenamiento de datos de SQL Azure. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Ejemplo: Copiar los datos de Blob de Azure tooAzure almacenamiento de datos SQL
ejemplo de Hola define Hola siguiendo las entidades de la factoría de datos:

1. Un servicio vinculado de tipo [AzureSqlDW](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlDWTable](#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlDWSink](#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de tabla de tooa de blobs de Azure en la base de datos de almacenamiento de datos de SQL Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado del almacenamiento de datos SQL de Azure:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Servicio vinculado de almacenamiento de blobs de Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Conjunto de datos de entrada de blob de Azure:**

Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola. "externo": "true" configuración informa a servicio de factoría de datos de Hola que esta tabla es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Conjunto de datos de salida del almacenamiento de datos SQL de Azure:**

ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en el almacén de datos de SQL Azure. Crear tabla de hello en el almacén de datos de SQL Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola. Se agregan nuevas filas toohello tabla cada hora.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Actividad de copia en una canalización con BlobSource y SqlDWSink:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
Para obtener un tutorial, vea hello [cargar 1 TB en almacenamiento de datos de SQL Azure en 15 minutos con Data Factory de Azure](data-factory-load-sql-data-warehouse.md) y [carga los datos con Data Factory de Azure](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artículo Hola almacenamiento de datos de SQL Azure documentación.

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
