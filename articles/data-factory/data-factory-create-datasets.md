---
title: "conjuntos de datos de aaaCreate de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo calcula el desplazamiento con ejemplos que utilizan propiedades como en Data Factory de Azure, los conjuntos de datos toocreate y anchorDateTime."
keywords: crear conjunto de datos, ejemplo de conjunto de datos, ejemplo con offset
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Conjuntos de datos en Azure Data Factory
En este artículo se describe qué son los conjuntos de datos, cómo se definen en formato JSON y cómo se usan en canalizaciones de Azure Data Factory. Proporciona detalles sobre cada sección (por ejemplo, estructura, disponibilidad y directiva) en la definición de JSON de conjunto de datos de Hola. Hello artículo también proporcionan ejemplos para usar hello **desplazamiento**, **anchorDateTime**, y **estilo** propiedades en una definición de JSON de conjunto de datos.

> [!NOTE]
> Si se tooData nueva fábrica, consulte [tooAzure Introducción factoría de datos](data-factory-introduction.md) para obtener información general. Si no tiene experiencia práctica con la creación de generadores de datos, puede obtener una mejor comprensión por leer hello [tutorial de transformación de datos](data-factory-build-your-first-pipeline.md) hello y [tutorial de movimiento de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Información general
Una factoría de datos puede tener una o más canalizaciones. Una **canalización** es una agrupación lógica de **actividades** que realizan una tarea. actividades de Hello en una canalización definen acciones tooperform en los datos. Por ejemplo, puede usar un datos de toocopy de actividad de copia de un tooAzure de SQL Server local almacenamiento de blobs. A continuación, puede usar una actividad de Hive que se ejecuta un script de Hive en un datos tooprocess de clúster de HDInsight de Azure de datos de salida de tooproduce de almacenamiento de blobs. Por último, puede usar una segunda copia actividad toocopy Hola salida datos tooAzure almacenamiento de datos de SQL, sobre qué inteligencia empresarial (BI) reporting soluciones se generan. Para más información sobre canalizaciones y actividades, consulte el artículo [Canalizaciones y actividades en Azure Data Factory](data-factory-create-pipelines.md).

Una actividad puede tomar diversos **conjuntos de datos** de entrada, o ninguno, y generar uno o varios conjuntos de datos de salida. Un conjunto de datos de entrada representa la entrada de Hola para una actividad de canalización de Hola y un conjunto de datos de salida representa la salida de hello para la actividad de Hola. Los conjuntos de datos identifican datos en distintos almacenes de datos, como tablas, archivos, carpetas y documentos. Por ejemplo, un conjunto de datos de Blob de Azure especifica contenedor de blob de Hola y la carpeta de almacenamiento de blobs de qué Hola canalización debe leer los datos de Hola. 

Antes de crear un conjunto de datos, crear un **servicio vinculado** toolink toohello factoría de datos de almacén de los datos. Servicios vinculados son muy similares a las cadenas de conexión, que definen la información de conexión de hello necesaria para los recursos de tooexternal tooconnect de factoría de datos. Conjuntos de datos para identificar datos dentro de los almacenes de datos de hello vinculado, como tablas SQL, archivos, carpetas y documentos. Por ejemplo, un almacenamiento de Azure había vinculada vínculos de servicio una factoría de datos de toohello de cuenta de almacenamiento. Un conjunto de datos de Blob de Azure representa contenedor de blobs de Hola y la carpeta de Hola que contiene Hola blobs entrada toobe procesado. 

Este es un escenario de ejemplo. datos de toocopy de base de datos SQL tooa de almacenamiento de blobs, crear dos servicios vinculados: almacenamiento de Azure y base de datos de SQL Azure. A continuación, cree dos conjuntos de datos: conjunto de datos de Blob de Azure (que hace referencia el servicio de almacenamiento de Azure vinculada de toohello) y un conjunto de tablas de SQL Azure (que hace la referencia de servicio de base de datos de Azure SQL vinculado toohello). Hola almacenamiento de Azure y base de datos de SQL de Azure servicios vinculados contienen cadenas de conexión utilizado por factoría de datos en tiempo de ejecución tooconnect tooyour almacenamiento de Azure y base de datos de SQL Azure, respectivamente. conjunto de datos de Blob de Azure de Hello especifica el contenedor de blob de Hola y la carpeta de blob que contiene el BLOB de entrada de hello en el almacenamiento de blobs. conjunto de datos de tabla de SQL Azure Hola especifica la tabla SQL de hello en los datos de Hola de toowhich de base de datos SQL es toobe copiado.

Hello diagrama siguiente muestra hello relaciones entre los servicios vinculados, actividad, conjunto de datos y canalización de factoría de datos: 

![Relación entre la canalización, la actividad, el conjunto de datos y los servicios vinculados](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>Conjunto de datos JSON
Un conjunto de datos de Data Factory se define con formato JSON de la manera siguiente:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Hello en la tabla siguiente describe propiedades Hola anterior JSON:   

| Propiedad | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| name |Nombre del conjunto de datos de Hola. Consulte [Azure Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para ver este tipo de reglas. |Sí |N/D |
| type |Tipo de conjunto de datos de Hola. Especifique uno de los tipos de hello admitidos factoría de datos (por ejemplo: AzureBlob, AzureSqlTable). <br/><br/>Para más información, consulte [Tipo de conjunto de datos](#Type). |Sí |N/D |
| structure |Esquema del conjunto de datos de Hola.<br/><br/>Para más información, consulte [Estructura del conjunto de datos](#Structure). |No |N/D |
| typeProperties | propiedades de tipo Hello son diferentes para cada tipo (por ejemplo: Azure Blob, tabla de SQL Azure). Para obtener más información sobre tipos de hello compatibles y sus propiedades, vea [tipo de conjunto de datos](#Type). |Sí |N/D |
| external | Un valor booleano marca toospecify si una canalización del generador de datos explícitamente genera un conjunto de datos o no. Si el conjunto de datos de entrada de Hola para una actividad no se crea por la canalización actual hello, establecer este tootrue de marca. Establecer este tootrue marca Hola entrada conjunto de datos de la primera actividad de hello en canalización Hola.  |No |false |
| availability | Define Hola ventana de procesamiento (por ejemplo, cada hora o diariamente) o hello segmentar el modelo para la producción de hello conjunto de datos. Cada unidad de datos consumida y producida por la ejecución de una actividad se denomina segmento de datos. Si la disponibilidad de Hola de un conjunto de datos de salida es conjunto toodaily (frecuencia - Day, intervalo - 1), se produce un segmento diariamente. <br/><br/>Para más información, consulte [Disponibilidad del conjunto de datos](#Availability). <br/><br/>Para obtener más información sobre el conjunto de datos de hello segmentar el modelo, vea hello [ejecución y programación](data-factory-scheduling-and-execution.md) artículo. |Sí |N/D |
| policy |Define los criterios de Hola o condición de Hola que deben cumplir los segmentos del conjunto de datos de Hola. <br/><br/>Para obtener más información, vea hello [directiva de conjunto de datos](#Policy) sección. |No |N/D |

## <a name="dataset-example"></a>Ejemplo de conjunto de datos
En el siguiente ejemplo de Hola Hola conjunto de datos representa una tabla denominada **MyTable** en una base de datos SQL.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Tenga en cuenta Hola siguientes puntos:

* **tipo** se establece tooAzureSqlTable.
* **tableName** propiedad type (tipo de tooAzureSqlTable específico) se establece tooMyTable.
* **linkedServiceName** hace referencia de servicio de tooa vinculado del tipo AzureSqlDatabase, que se define en el siguiente fragmento de JSON Hola. 
* **frecuencia de disponibilidad** se establece tooDay, y **intervalo** se establece too1. Esto significa que se produce ese segmento de conjunto de datos de hello diariamente.  

**AzureSqlLinkedService** se define de la siguiente forma:

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Hola anterior fragmento de JSON:

* **tipo** se establece tooAzureSqlDatabase.
* **connectionString** propiedad type especifica información tooconnect tooa base de datos SQL.  

Como puede ver, hello servicio vinculado define la base de datos SQL tooconnect tooa. conjunto de datos de Hello define qué tabla se utiliza como entrada y salida de actividad de hello en una canalización.   

> [!IMPORTANT]
> A menos que se está produciendo un conjunto de datos por la canalización de hello, se debe marcar como **externo**. Por lo general, esta configuración aplica tooinputs de primera actividad en una canalización.   


## <a name="Type"></a> Tipo de conjunto de datos
tipo de Hello del conjunto de datos de hello depende de almacén de datos de hello utilizado. Vea Hola para obtener una lista de almacenes de datos compatibles con factoría de datos en la tabla siguiente. Haga clic en un toolearn de almacén de datos cómo toocreate un servicio vinculado y un conjunto de datos para los datos de almacén.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Los almacenes de datos con * pueden ser locales o de infraestructura como servicio (IaaS) de Azure. Estos almacenes de datos requieren tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).

En el ejemplo hello en la sección anterior de hello, tipo de hello del conjunto de datos de Hola se establece demasiado**AzureSqlTable**. De forma similar, para un conjunto de datos Blob de Azure, Hola tipo del conjunto de datos de Hola se establece demasiado**AzureBlob**, tal y como se muestra en hello después JSON:

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <a name="Structure"></a>Estructura del conjunto de datos
Hola **estructura** sección es opcional. Define el esquema de hello del conjunto de datos de hello, que contiene una colección de nombres y tipos de datos de columnas. Utilice Hola estructura sección tooprovide información de tipo que es tooconvert usa tipos y asignar columnas de destino de hello origen toohello. En el siguiente ejemplo de Hola, conjunto de datos de hello tiene tres columnas: `slicetimestamp`, `projectname`, y `pageviews`. Estas columnas son del tipo String, String, y Decimal, respectivamente.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Cada columna de estructura de hello contiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| name |Nombre de columna de Hola. |Sí |
| type |Tipo de datos de columna de Hola.  |No |
| culture |. Toobe de las referencias culturales basada en red utilizado cuando el tipo de hello es un tipo .NET: `Datetime` o `Datetimeoffset`. valor predeterminado de Hello es `en-us`. |No |
| formato |Dar formato a toobe de cadena que se usa cuando el tipo de hello es un tipo .NET: `Datetime` o `Datetimeoffset`. |No |

Hello instrucciones siguientes le ayudarán a determinar cuando tooinclude estructurar la información y qué tooinclude Hola **estructura** sección.

* **Para los orígenes de datos estructurados**, especificar la sección de estructura de hello únicamente si desea asignar columnas de toosink de las columnas de origen y sus nombres no son Hola igual. Este tipo de origen de datos estructurados almacena información de esquema y el tipo de datos junto con los datos de hello propio. Ejemplos de orígenes de datos estructurados son SQL Server, Oracle y Azure Table. 
  
    Como la información de tipo ya está disponible para orígenes de datos estructurados, no debe incluir información de tipo cuando se incluye la sección sobre la estructura Hola.
* **Para el esquema en orígenes de datos de lectura (específicamente el almacenamiento de blobs)**, puede elegir toostore datos sin tener que almacenar cualquier información de tipo o esquema con datos de Hola. Para estos tipos de orígenes de datos, incluyen una estructura cuando desee que las columnas toosink de columnas de origen de toomap. También incluyen una estructura cuando hello es una entrada para una actividad de copia, y los tipos de datos del conjunto de datos de origen deben ser tipos toonative convertido para receptor de Hola. 
    
    Factoría de datos admite Hola siguientes valores para proporcionar información de tipo de estructura: **Int16, Int32, Int64, Single, Double, Decimal, bytes [], un valor booleano, cadena, Guid, Datetime, Datetimeoffset y Timespan**. Estos valores son valores de tipos basados en .NET compatibles con Common Language Specification (CLS).

Factoría de datos realiza automáticamente las conversiones de tipos al mover el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos. 
  

## <a name="dataset-availability"></a>Conjunto de datos availability
Hola **disponibilidad** sección en un conjunto de datos define la ventana de procesamiento de hello (por ejemplo, cada hora, diariamente, o semanal) para el conjunto de datos de Hola. Para más información sobre las ventanas de actividad, consulte el artículo sobre [programación y ejecución](data-factory-scheduling-and-execution.md).

Hola pasos de la sección de disponibilidad especifica que hello conjunto de datos de salida o generado por hora, o conjunto de datos de entrada de hello está disponible por hora:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Si canalización hello tiene Hola después de horas de inicio y finalización:  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Hello conjunto de datos de salida se genera cada hora en la canalización de hello hora inicial y final. Por lo tanto, esta canalización genera cinco segmentos de conjuntos de datos, uno por cada ventana de actividad (12 a.m. - 1 a.m., 1 a.m. - 2 a.m., 2 a.m. - 3 a.m., 3 a.m. - 4 a.m., 4 a.m. - 5 a.m.). 

Hello tabla siguiente describe propiedades que puede utilizar en la sección de disponibilidad de hello:

| Propiedad | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| frequency |Especifica la unidad de tiempo de hello para la producción de segmento del conjunto de datos.<br/><br/><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month. |Sí |N/D |
| interval |Especifica un multiplicador para "frequency".<br/><br/>"Intervalo de frecuencia x" determina con qué frecuencia hello segmento se genera. Por ejemplo, si necesita hello toobe de conjunto de datos se crean sectores de cada hora, establecer <b>frecuencia</b> demasiado<b>hora</b>, y <b>intervalo</b> demasiado<b>1</b>.<br/><br/>Tenga en cuenta que si especifica **frecuencia** como **minuto**, debe establecer Hola intervalo toono inferior a 15. |Sí |N/D |
| style |Especifica si se debe generar el segmento de hello al inicio de Hola o al final del intervalo de saludo.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Si **frecuencia** se establece demasiado**mes**, y **estilo** se establece demasiado**EndOfInterval**, Hola segmento se genera en hello último día del mes. Si **estilo** se establece demasiado**StartOfInterval**, se genera el segmento de hello en hello primer día del mes.<br/><br/>Si **frecuencia** se establece demasiado**día**, y **estilo** se establece demasiado**EndOfInterval**, Hola segmento se genera en la última hora del día de Hola Hola.<br/><br/>Si **frecuencia** se establece demasiado**hora**, y **estilo** se establece demasiado**EndOfInterval**, Hola segmento se genera al final de Hola de hora de Hola. Por ejemplo, para un intervalo de hello período 1 P.M. a 2 P.M., segmento de Hola se genera a las 2 P.M.. |No |EndOfInterval |
| anchorDateTime |Define la posición absoluta de hello en el tiempo utilizado por los límites del sector de hello programador toocompute conjunto de datos. <br/><br/>Tenga en cuenta que si esta propoerty tiene Dateparts más granulares de hello especifica la frecuencia, Hola partes más pormenorizadas se omiten. Por ejemplo, si hello **intervalo** es **cada hora** (frecuencia: hora e intervalo: 1), hello y **anchorDateTime** contiene **minutos y segundos**, a continuación, Hola partes minutos y segundos de **anchorDateTime** se omiten. |No |01/01/0001 |
| Offset |Intervalo de tiempo por qué Hola se desplazan inicial y final de todos los sectores de conjunto de datos. <br/><br/>Tenga en cuenta que, si ambos **anchorDateTime** y **desplazamiento** se especifican, resultado de hello es Hola combinan MAYÚS. |No |N/D |

### <a name="offset-example"></a>Ejemplo de offset
De forma predeterminada, los segmentos diarios (`"frequency": "Day", "interval": 1`) comienzan a las 12 p.m. (medianoche), Hora universal coordinada (UTC). Si desea Hola inicio toobe 6: 00 UTC hora en su lugar, establezca Hola offset tal como se muestra en el siguiente fragmento de código de hello: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Ejemplo de anchorDateTime
En el siguiente ejemplo de Hola Hola conjunto de datos se produce una vez cada 23 horas. Hello primer sector comienza en tiempo de hello especificado por **anchorDateTime**, que se establece demasiado`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Ejemplo de offset/style
Hola siguiente conjunto de datos es mensual y se genera en hello 3rd de cada mes a las 8:00 A.M. (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>Directiva del conjunto de datos
Hola **directiva** sección de definición de conjunto de datos de hello define los criterios de Hola o debe cumplir la condición de Hola que Hola segmentos del conjunto de datos.

### <a name="validation-policies"></a>Directivas de validación
| Nombre de la directiva | Descripción | Aplica demasiado| Obligatorio | Valor predeterminado |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valida datos hello en **almacenamiento de blobs de Azure** Hola de cumple los requisitos mínimos de tamaño (en megabytes). |Azure Blob Storage |No |N/D |
| minimumRows |Valida datos hello en un **base de datos SQL de Azure** o un **tabla de Azure** contiene Hola número mínimo de filas. |<ul><li>Azure SQL Database</li><li>Tabla de Azure</li></ul> |No |N/D |

#### <a name="examples"></a>Ejemplos
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>Conjuntos de datos externos
Conjuntos de datos externos son hello las que no producidos por una canalización de factoría de datos de hello en ejecución. Si el conjunto de datos de hello está marcado como **externo**, hello **ExternalData** directiva puede ser definido tooinfluence Hola comportamiento de la disponibilidad de segmento del conjunto de datos de Hola.

A menos que se esté produciendo un conjunto de datos mediante Data Factory, debe marcarse como **external**. Esta configuración normalmente aplica toohello entradas de la primera actividad en una canalización, a menos que se está usando la actividad o el encadenamiento de canalización.

| Nombre | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| dataDelay |tiempo de Hola Hola toodelay Comprobar disponibilidad de Hola de datos externos de Hola de hello proporciona segmento. Por ejemplo, puede retrasar una comprobación horaria mediante esta configuración.<br/><br/>Hola configuración solo aplica a toohello la hora actual.  Por ejemplo, si es 1:00 P.M. y este valor es 10 minutos, validación de hello comienza en 1:10 P.M..<br/><br/>Tenga en cuenta que esta configuración no afecta los segmentos en hello anterior. Los segmentos con **Slice End Time** + **dataDelay** < **Now** se procesan sin retraso.<br/><br/>Veces mayor que 23:59 horas deben especificarse mediante hello `day.hours:minutes:seconds` formato. Por ejemplo, toospecify 24 horas, no use 24:00:00. En su lugar, use 1.00:00:00. Si usa 24:00:00, se tratará como 24 días (24.00:00:00). Para 1 día y 4 horas, especifique 1:04:00:00. |No |0 |
| retryInterval |tiempo de espera de Hello entre un intento siguiente hello y error. Esta configuración aplica toopresent tiempo. Si no se pudo try anterior hello, siguiente intento de hello es tras hello **retryInterval** período. <br/><br/>Si es 1:00 P.M., comenzaremos Hola primer intento. Si Hola duración toocomplete Hola primera comprobación de validación es 1 minuto y error en la operación hello, Hola siguiente reintento es a 1:00 + 1 min (duración) + 1min (intervalo de reintento) = 1:02 PM. <br/><br/>Para los segmentos en hello anterior, no hay ningún retraso. reintento de Hello ocurre inmediatamente. |No |00:01:00 (1 minuto) |
| retryTimeout |tiempo de espera de Hola para cada reintento.<br/><br/>Si se establece esta propiedad too10 minutos, se debe completar la validación de hello dentro de 10 minutos. Si se tarda más tiempo que la validación de hello tooperform de 10 minutos, Hola vuelva a intentar agota el tiempo.<br/><br/>Si todos los intentos de validación Hola vencen, Hola segmento está marcado como **TimedOut**. |No |00:10:00 (10 minutos) |
| maximumRetry |número de Hola de tiempo toocheck para disponibilidad Hola de datos externos de Hola. Hola valor máximo permitido es 10. |No |3 |


## <a name="create-datasets"></a>Creación de conjuntos de datos
Puede crear conjuntos de datos mediante el uso de algunas de estas herramientas o SDK: 

- Asistente para copia 
- Azure Portal
- Visual Studio
- PowerShell
- Plantilla del Administrador de recursos de Azure
- API de REST
- API de .NET

Vea Hola tutoriales para obtener instrucciones paso a paso para crear canalizaciones y conjuntos de datos mediante una de estas herramientas o SDK:
 
- [Creación de una canalización con una actividad de transformación de datos](data-factory-build-your-first-pipeline.md)
- [Creación de una canalización con una actividad de movimiento de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Después de que se crea e implementa una canalización, puede administrar y supervisar sus canalizaciones mediante el uso de Hola hojas de portal de Azure, o una aplicación de supervisión y administración de Hola. Vea Hola temas para obtener instrucciones paso a paso siguientes: 

- [Supervisión y administración de canalizaciones con las hojas de Azure Portal](data-factory-monitor-manage-pipelines.md)
- [Supervisar y administrar las canalizaciones mediante el uso de la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Conjuntos de datos limitados
Puede crear conjuntos de datos con ámbito tooa canalización mediante el uso de hello **conjuntos de datos** propiedad. Estos conjuntos de datos solo los pueden usar las actividades dentro de esta canalización, pero no las actividades de otras canalizaciones. Hola siguiente ejemplo define una canalización con toobe (rdc InputDataset y OutputDataset rdc) de dos conjuntos de datos utilizado en la canalización de Hola.  

> [!IMPORTANT]
> Conjuntos de datos con ámbito solo son compatibles con las canalizaciones de un solo uso (donde **pipelineMode** se establece demasiado**OneTime**). Consulte la sección [Canalización de una vez](data-factory-create-pipelines.md#onetime-pipeline) para más información.
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
- Para más información sobre las canalizaciones, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md). 
- Para más información sobre cómo programar y ejecutar canalizaciones en Azure Data Factory, consulte [este artículo](data-factory-scheduling-and-execution.md). 
