---
title: "aaaAzure factoría de datos: referencia de scripts JSON | Documentos de Microsoft"
description: Proporciona esquemas JSON para entidades de Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - Referencia de scripting JSON
Este artículo proporciona ejemplos y esquemas JSON para definir entidades de Azure Data Factory (canalización, actividad, conjunto de datos y servicio vinculado).  

## <a name="pipeline"></a>Canalización 
estructura de alto nivel de Hola para una definición de la canalización es como sigue: 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Tabla siguiente describe las propiedades de hello dentro de la canalización de hello definición JSON:

| Propiedad | Descripción | Obligatorio
-------- | ----------- | --------
| name | Nombre de la canalización de Hola. Especifique un nombre que representa la acción de Hola que Hola actividad o canalización es toodo configurado<br/><ul><li>Número máximo de caracteres: 260</li><li>Debe empezar en una letra, un número o un carácter de subrayado (_)</li><li>No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sí |
| description |Texto que describe qué actividad hello o canalización se usa para | No |
| actividades | Contiene una lista de actividades. | Sí |
| start |Fecha y hora de inicio de la canalización de Hola. Debe estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2014-10-14T16:32:41. <br/><br/>Es posible toospecify una hora local, por ejemplo una hora EST. Aquí tiene un ejemplo: `2016-02-27T06:00:00**-05:00`, que es 6 a. m. EST.<br/><br/>Hello propiedades start y end juntos especifican el período activo de la canalización de Hola. Los segmentos de salida solo se producen en este período activo. |No<br/><br/>Si especifica un valor para la propiedad de finalización de hello, debe especificar el valor de propiedad de inicio de Hola.<br/><br/>Hello horas de inicio y finalización tanto pueden ser toocreate vacía una canalización. Debe especificar ambos valores tooset un período activo de hello canalización toorun. Si no especifica horas de inicio y finalización al crear una canalización, puede establecerlas mediante cmdlet Hola conjunto AzureRmDataFactoryPipelineActivePeriod más tarde. |
| end |Fecha y hora de final de la canalización de Hola. Si se especifica, debe estar en formato ISO. Por ejemplo: 2014-10-14T17:32:41 <br/><br/>Es posible toospecify una hora local, por ejemplo una hora EST. Aquí tiene un ejemplo: `2016-02-27T06:00:00**-05:00`, que es 6 a. m. EST.<br/><br/>canalización de hello toorun indefinidamente, especifique 9999-09-09 como valor de hello para la propiedad de finalización de Hola. |No <br/><br/>Si especifica un valor para la propiedad de inicio de hello, debe especificar el valor de propiedad de finalización de Hola.<br/><br/>Vea las notas de hello **iniciar** propiedad. |
| isPaused |Si no se ejecuta la canalización de conjunto tootrue Hola. Valor predeterminado = false. Puede usar esta propiedad tooenable o deshabilitar. |No |
| pipelineMode |método Hello para la programación se ejecuta para la canalización de Hola. Los valores permitidos son: scheduled (predeterminado).<br/><br/>'Programada' indica que esa canalización Hola se ejecuta en un intervalo de tiempo especificado según el período activo de tooits (hora de inicio y final). 'Tendrá que repetir' indica que esa canalización Hola se ejecuta solo una vez. Las canalizaciones creadas una sola vez no se pueden modificar ni actualizar actualmente. Consulte la sección [Canalización de una vez](data-factory-create-pipelines.md#onetime-pipeline) para más información acerca de la configuración onetime. |No |
| expirationTime |Duración de tiempo después de la creación de qué Hola canalización es válida y debe permanecer aprovisionado. Si no tiene ningún activo, error, o pendientes se ejecuta, la canalización de Hola se elimina automáticamente una vez que llega la hora de expiración de Hola. |No |


## <a name="activity"></a>Actividad 
estructura de alto nivel de Hola para una actividad dentro de una definición de canalización (elemento de actividades) es la siguiente:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

Tabla siguiente describen las propiedades de hello dentro de la actividad de hello definición JSON:

| Etiqueta | Description | Obligatorio |
| --- | --- | --- |
| name |Nombre de actividad de Hola. Especifique un nombre que representa la acción Hola actividad hello configura toodo<br/><ul><li>Número máximo de caracteres: 260</li><li>Debe empezar en una letra, un número o un carácter de subrayado (_)</li><li>No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sí |
| description |Texto que describe qué actividad Hola se usa para. |Sí |
| type |Especifica el tipo de saludo de actividad hello. Vea hello [almacenes de datos](#data-stores) y [las actividades de transformación de datos](#data-transformation-activities) secciones para diferentes tipos de actividades. |Sí |
| inputs |Tablas de entrada utilizadas por actividad hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Sí |
| outputs |Tablas de salida utilizadas por actividad hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Sí |
| linkedServiceName |Nombre del servicio de hello vinculado utilizado por actividad hello. <br/><br/>Una actividad puede requerir que especifique servicio Hola vinculado que se vincula el entorno de proceso necesarios toohello. |Sí para las actividades de HDInsight, las actividades de Azure Machine Learning y las actividades del procedimiento almacenadas. <br/><br/>No para todos los demás |
| typeProperties |Propiedades de hello typeProperties sección dependen del tipo de actividad de Hola. |No |
| policy |Directivas que afectan al comportamiento de tiempo de ejecución de Hola de actividad hello. Si no se especifica, se usan las directivas predeterminadas. |No |
| scheduler |propiedad "programador" es usado toodefine deseado de programación para la actividad de Hola. Sus subpropiedades se Hola igual que los de Hola Hola [propiedad de disponibilidad en un conjunto de datos](data-factory-create-datasets.md#dataset-availability). |No |

### <a name="policies"></a>Directivas
Las directivas afectan al comportamiento de tiempo de ejecución de Hola de una actividad, específicamente cuando se procesa el sector de Hola de una tabla. Hello en la tabla siguiente proporciona detalles de Hola.

| Propiedad | Valores permitidos | Valor predeterminado | Description |
| --- | --- | --- | --- |
| simultaneidad |Entero  <br/><br/>Valor máximo: 10 |1 |Número de ejecuciones simultáneas de actividad hello.<br/><br/>Determina el número de Hola de ejecuciones paralelas que pueden ocurrir en distintos sectores. Por ejemplo, si una actividad tiene toogo a través de un conjunto grande de datos disponibles, que tienen un valor mayor de simultaneidad acelera el procesamiento de datos de Hola. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Determina Hola orden de los segmentos de datos que se están procesando.<br/><br/>Por ejemplo, si tiene 2 segmentos (que tienen lugar uno a las 4 p.m. y el otro a las 5 p.m.) y ambos están pendientes de ejecución. Si establece hello executionPriorityOrder toobe NewestFirst, segmento de Hola a las 5 P.M. se procesa en primer lugar. De forma similar si establece hello executionPriorityORder toobe OldestFIrst, segmento de Hola a las 4 P.M. se procesa. |
| retry |Entero <br/><br/>El valor máximo permitido es 10 |0 |Número de reintentos antes del procesamiento de datos de hello para el segmento de Hola se marca como completada con errores. Ejecución de actividad para un segmento de datos se vuelve a intentar la toohello especificada número de reintentos. Hola reintento se realiza tan pronto como sea posible después de error de Hola. |
| timeout |TimeSpan |00:00:00 |Tiempo de espera para la actividad de Hola. Ejemplo: 00:10:00 (implica un tiempo de espera de 10 minutos)<br/><br/>Si un valor no se especifica o es 0, el tiempo de espera de hello es infinito.<br/><br/>Si el tiempo de procesamiento de datos de hello en un sector supera el valor de tiempo de espera de hello, que se cancele y sistema de hello trata el procesamiento de hello tooretry. número de Hola de reintentos depende de la propiedad de reintento de Hola. Cuando se produce el tiempo de espera, el estado de Hola se establece tooTimedOut. |
| delay |TimeSpan |00:00:00 |Especificar el retraso de hello antes del procesamiento de datos de segmento Hola se inicia.<br/><br/>se inicia la ejecución de Hola de actividad para un segmento de datos una vez Hola retraso pasado Hola espera el tiempo de ejecución.<br/><br/>Ejemplo: 00:10:00 (implica un retraso de 10 minutos) |
| longRetry |Entero <br/><br/>Valor máximo: 10 |1 |número de Hola de reintentos largos intentos antes de que se error al ejecutar el segmento Hola.<br/><br/>Los intentos de longRetry se espacian de acuerdo a longRetryInterval. Por lo que si necesita toospecify un tiempo entre los reintentos, utilice longRetry. Si se especifican Retry y longRetry, cada intento de longRetry incluye los intentos de reintento y número máximo de Hola de intentos es reintento * longRetry.<br/><br/>Por ejemplo, si tenemos Hola después de la configuración de directiva de actividad de hello:<br/>Retry: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Suponemos que hay solo un tooexecute de segmento (estado de espera) y ejecución de la actividad de Hola se produce un error cada vez. Inicialmente habría tres intentos consecutivos de ejecución. Después de cada intento, estado del sector Hola sería Retry. Después de 3 primeros intentos superan el tiempo de espera, estado del sector Hola sería LongRetry.<br/><br/>Después de una hora (es decir, el valor de longRetryInteval), se produciría otro conjunto de 3 intentos consecutivos de ejecución. Después de eso, el estado del sector de hello podría ser Failed y no podría realizarse ningún reintento más. Por tanto, en total se realizaron 6 intentos.<br/><br/>Si cualquier ejecución se realiza correctamente, el estado del sector de hello sería Ready y no se realiza ningún reintento más.<br/><br/>longRetry puede utilizarse en situaciones donde llegan datos dependientes en momentos no determinista o hello entorno general es inestable en el procesamiento de datos que se produce. En tales casos, no es útil realizar reintentos uno tras otro y hacerlo después de un intervalo de tiempo provoca Hola deseado de salida.<br/><br/>Advertencia: No establezca valores altos para longRetry o longRetryInterval. Normalmente, los valores más altos implican otros problemas sistémicos. |
| longRetryInterval |TimeSpan |00:00:00 |retraso de Hello entre reintentos largos |

### <a name="typeproperties-section"></a>Sección typeProperties
sección de typeProperties Hello es diferente para cada actividad. Las actividades de transformación tienen propiedades de tipo hello solo. Vea la sección [Actividades de transformación de datos](#data-transformation-activities) de este artículo para obtener ejemplos JSON que definen las actividades de transformación en una canalización. 

**Actividad de copia** tiene dos subsecciones de sección de Hola typeProperties: **origen** y **receptor**. Vea [almacenes de datos](#data-stores) sección en este artículo para JSON ejemplos que muestran cómo almacenar toouse datos como un origen o receptor. 

### <a name="sample-copy-pipeline"></a>Canalización de copia de ejemplo
Hola después de canalización de ejemplo, hay una actividad de tipo **copia** en hello **actividades** sección. En este ejemplo, Hola [actividad de copia](data-factory-data-movement-activities.md) copia datos de una base de datos de SQL Azure del tooan de almacenamiento Blob de Azure. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Tenga en cuenta Hola siguientes puntos:

* En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.
* Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**.
* Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola.

Vea [almacenes de datos](#data-stores) sección en este artículo para JSON ejemplos que muestran cómo almacenar toouse datos como un origen o receptor.    

Para obtener un tutorial completo de creación de esta canalización, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Canalización de transformación de ejemplo
Hola después de canalización de ejemplo, hay una actividad de tipo **HDInsightHive** en hello **actividades** sección. En este ejemplo, Hola [actividad de HDInsight Hive](data-factory-hive-activity.md) transforma los datos de un almacenamiento de blobs de Azure mediante la ejecución de un archivo de script de Hive en un clúster de Hadoop de HDInsight de Azure. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Tenga en cuenta Hola siguientes puntos: 

* En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**HDInsightHive**.
* archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **AzureStorageLinkedService**) y en  **secuencia de comandos** carpeta en el contenedor de hello **adfgetstarted**.
* Hola **define** sección es la configuración de en tiempo de ejecución de hello toospecify utilizado que se pasa el script de hive toohello como valores de configuración de Hive (por ejemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Vea la sección [Actividades de transformación de datos](#data-transformation-activities) de este artículo para obtener ejemplos JSON que definen las actividades de transformación en una canalización.

Para obtener un tutorial completo de creación de esta canalización, consulte [Tutorial: generar los datos primera canalización tooprocess con clúster de Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Servicio vinculado
estructura de alto nivel de Hola para una definición de servicio vinculado es como sigue:

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Tabla siguiente describen las propiedades de hello dentro de la actividad de hello definición JSON:

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- | 
| name | Nombre del servicio de hello vinculado. | Sí | 
| propiedades - tipo | Tipo de servicio de hello vinculado. Por ejemplo: Azure Storage o Azure SQL Database. |
| typeProperties | sección de typeProperties Hello tiene elementos que son diferentes para cada almacén de datos o el entorno de proceso. Vea [almacenes de datos](#datastores) sección para todos los datos de hello almacenan servicios vinculados y [proceso entornos](#compute-environments) para hello todos los servicios vinculados de proceso |   

## <a name="dataset"></a>Dataset 
Un conjunto de datos en Data Factory de Azure se define como sigue:

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
| name | Nombre del conjunto de datos de Hola. Consulte [Azure Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para ver este tipo de reglas. |Sí |N/D |
| type | Tipo de conjunto de datos de Hola. Especifique uno de los tipos de hello compatibles con Data Factory de Azure (por ejemplo: AzureBlob, AzureSqlTable). Vea [almacenes de datos](#data-stores) sección de Hola a todos los tipos de conjunto de datos admitidos por el generador de datos y almacenes de datos. | 
| structure | Esquema del conjunto de datos de Hola. Contiene las columnas, sus tipos, etc. | No |N/D |
| typeProperties | Propiedades que corresponden toohello el tipo seleccionado. Vea la sección [ALMACENES DE DATOS](#data-stores) para consultar los tipos admitidos y sus propiedades. |Sí |N/D |
| external | Un valor booleano marca toospecify si una canalización del generador de datos explícitamente genera un conjunto de datos o no. |No |false |
| availability | Define Hola Hola segmentar el modelo para la producción de hello conjunto de datos o la ventana de procesamiento. Para obtener detalles sobre el conjunto de datos de hello segmentar el modelo, vea [ejecución y programación](data-factory-scheduling-and-execution.md) artículo. |Sí |N/D |
| policy |Define los criterios de Hola o condición de Hola que deben cumplir los segmentos del conjunto de datos de Hola. <br/><br/>Para más información, consulte la sección [Directiva del conjunto de datos](#Policy) . |No |N/D |

Cada columna de hello **estructura** sección contiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| name |Nombre de columna de Hola. |Sí |
| type |Tipo de datos de columna de Hola.  |No |
| culture |Toobe de referencia cultural que se usa cuando el tipo se especifica y es de tipo .NET basadas en .NET `Datetime` o `Datetimeoffset`. El valor predeterminado es `en-us`. |No |
| formato |Dar formato a toobe de cadena que se usa cuando el tipo se especifica y es de tipo .NET `Datetime` o `Datetimeoffset`. |No |

En el siguiente ejemplo de Hola, conjunto de datos de hello tiene tres columnas `slicetimestamp`, `projectname`, y `pageviews` y son del tipo: cadena, cadena y Decimal respectivamente.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Hello tabla siguiente describen propiedades que puede utilizar en hello **disponibilidad** sección:

| Propiedad | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| frequency |Especifica la unidad de tiempo de hello para la producción de segmento del conjunto de datos.<br/><br/><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month. |Sí |N/D |
| interval |Especifica un multiplicador para frecuencia<br/><br/>"Intervalo de frecuencia x" determina con qué frecuencia hello segmento se genera.<br/><br/>Si necesita hello toobe de conjunto de datos se crean sectores de cada hora, establecer <b>frecuencia</b> demasiado<b>hora</b>, y <b>intervalo</b> demasiado<b>1</b>.<br/><br/><b>Tenga en cuenta</b>: si especifica frecuencia como minuto, se recomienda que establezca Hola intervalo toono inferior a 15 |Sí |N/D |
| style |Especifica si se debe generar segmento hello en hello inicio/final del intervalo de saludo.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Si se establece la frecuencia de tooMonth y se establece el estilo tooEndOfInterval, Hola segmento se genera Hola último día del mes. Si se establece tooStartOfInterval en estilo de hello, Hola segmento se genera en hello primer día del mes.<br/><br/>Si se establece la frecuencia de tooDay y se establece el estilo tooEndOfInterval, segmento de Hola se genera en la última hora del día de Hola Hola.<br/><br/>Si se establece la frecuencia de tooHour y se establece el estilo tooEndOfInterval, segmento de Hola se genera al final de Hola de hora de Hola. Por ejemplo, para un intervalo durante el período de 1 P.M. – 2 P.M., segmento de Hola se genera a las 2 P.M.. |No |EndOfInterval |
| anchorDateTime |Define la posición absoluta de hello en el tiempo utilizado por los límites del sector de programador toocompute conjunto de datos. <br/><br/><b>Tenga en cuenta</b>: si hello AnchorDateTime tiene Dateparts más granulares que la frecuencia de hello, hello partes más pormenorizadas se omiten. <br/><br/>Por ejemplo, si hello <b>intervalo</b> es <b>cada hora</b> (frecuencia: hora e intervalo: 1) hello y <b>AnchorDateTime</b> contiene <b>minutos y segundos</b>, a continuación, Hola <b>minutos y segundos</b> partes de hello AnchorDateTime se omiten. |No |01/01/0001 |
| Offset |Intervalo de tiempo por qué Hola se desplazan inicial y final de todos los sectores de conjunto de datos. <br/><br/><b>Tenga en cuenta</b>: si se especifican anchorDateTime y offset, resultado de hello es Hola combinan MAYÚS. |No |N/D |

Hola pasos de la sección de disponibilidad especifica ese conjunto de datos de salida de hello es generado por hora (o) proporcionados por el conjunto de datos está disponible por hora:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Hola **directiva** sección de definición de conjunto de datos define los criterios de Hola o debe cumplir la condición de Hola que Hola segmentos del conjunto de datos.

| Nombre de la directiva | Descripción | Aplica demasiado| Obligatorio | Valor predeterminado |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valida datos hello en un **blobs de Azure** Hola de cumple los requisitos mínimos de tamaño (en megabytes). |Blob de Azure |No |N/D |
| minimumRows |Valida datos hello en un **base de datos SQL de Azure** o un **tabla de Azure** contiene Hola número mínimo de filas. |<ul><li>Azure SQL Database</li><li>tabla de Azure</li></ul> |No |N/D |

**Ejemplo:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

A menos que se esté produciendo un conjunto de datos mediante Data Factory de Azure, debe marcarse como **external**. Esta configuración normalmente aplica toohello entradas de la primera actividad en una canalización a menos que se está usando la actividad o el encadenamiento de canalización.

| Nombre | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| dataDelay |Comprobación de hello toodelay tiempo en la disponibilidad de Hola de datos externos de Hola para hello dado segmento. Por ejemplo, si Hola los datos están disponibles cada hora, datos externos de hello comprobación toosee Hola están disponibles y es el segmento correspondiente de Hola se puede retrasar listo utilizando dataDelay.<br/><br/>Solo se aplica toohello la hora actual.  Por ejemplo, si es 1:00 P.M. y este valor es 10 minutos, validación de hello comienza en 1:10 P.M..<br/><br/>Esta configuración no afecta los segmentos en hello anterior (segmentos con hora de finalización de segmento + dataDelay < ahora) se procesan sin ningún retraso.<br/><br/>Tiempo mayor que 23:59 horas necesitan toospecified con hello `day.hours:minutes:seconds` formato. Por ejemplo, toospecify 24 horas, no utilice 24:00:00; en su lugar, use 1.00:00:00. Si usa 24:00:00, se tratará como 24 días (24.00:00:00). Para 1 día y 4 horas, especifique 1:04:00:00. |No |0 |
| retryInterval |tiempo de espera de Hello entre un error y Hola siguiente reintento. Si se produce un error en un bloque try, el siguiente intento de hello es después retryInterval. <br/><br/>Si es 1:00 P.M., comenzaremos Hola primer intento. Si Hola duración toocomplete Hola primera comprobación de validación es 1 minuto y error en la operación hello, Hola siguiente reintento es a 1:00 + 1 min (duración) + 1 min (intervalo de reintento) = 1:02 PM. <br/><br/>Para los segmentos en hello anterior, no hay ningún retraso. reintento de Hello ocurre inmediatamente. |No |00:01:00 (1 minuto) |
| retryTimeout |tiempo de espera de Hola para cada reintento.<br/><br/>Si se establece esta propiedad too10 minutos, Hola validación necesidades toobe completar en 10 minutos. Si se tarda más tiempo que la validación de hello tooperform de 10 minutos, Hola vuelva a intentar agota el tiempo.<br/><br/>Si se agota el tiempo todos los intentos para la validación de hello, segmento de Hola se marca como TimedOut. |No |00:10:00 (10 minutos) |
| maximumRetry |Número de veces toocheck para disponibilidad Hola de datos externos de Hola. Hola permite el valor máximo es 10. |No |3 |


## <a name="data-stores"></a>ALMACENES DE DATOS
Hola [servicio vinculado](#linked-service) descripciones de la sección que se proporciona para los elementos JSON que son tipos de tooall comunes de los servicios vinculados. Esta sección proporciona detalles acerca de los elementos JSON que son el almacén de datos tooeach específica.

Hola [conjunto de datos](#dataset) descripciones de la sección que se proporciona para los elementos JSON que son tipos de tooall comunes de los conjuntos de datos. Esta sección proporciona detalles acerca de los elementos JSON que son el almacén de datos tooeach específica.

Hola [actividad](#activity) descripciones de la sección que se proporciona para los elementos JSON que son tipos de tooall comunes de actividades. Esta sección proporciona detalles sobre los elementos JSON que son almacén de datos tooeach específica cuando se utiliza como un origen/receptor de una actividad de copia.  

Haga clic en el vínculo de hello para la tienda de hello está interesado en esquemas JSON de hello toosee para servicios vinculados, conjunto de datos y Hola origen/receptor para la actividad de copia de Hola.

| Categoría | Almacén de datos 
|:--- |:--- |
| **Las tablas de Azure** |[Almacenamiento de blobs de Azure](#azure-blob-storage) |
| &nbsp; |[Almacén de Azure Data Lake](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Azure SQL Database](#azure-sql-database) |
| &nbsp; |[Azure SQL Data Warehouse](#azure-sql-data-warehouse) |
| &nbsp; |[Búsqueda de Azure](#azure-search) |
| &nbsp; |[Azure Table Storage](#azure-table-storage) |
| **Bases de datos** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **Archivo** |[Amazon S3](#amazon-s3) |
| &nbsp; |[Sistema de archivos](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Otros** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Tabla web](#web-table) |

## <a name="azure-blob-storage"></a>Almacenamiento de blobs de Azure

### <a name="linked-service"></a>Servicio vinculado
Hay dos tipos de servicios vinculados: servicio vinculado de Azure Storage y servicio vinculado de SAS de Azure Storage.

#### <a name="azure-storage-linked-service"></a>Servicio vinculado de Almacenamiento de Azure
toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de hello **clave de cuenta**, cree un servicio vinculado de almacenamiento de Azure. el servicio conjunto Hola vinculado de toodefine un almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorage**. A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| connectionString |Especifique la información necesaria tooconnect tooAzure almacenamiento para la propiedad connectionString de Hola. |Sí |

##### <a name="example"></a>Ejemplo  

```json
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

#### <a name="azure-storage-sas-linked-service"></a>Servicio vinculado de SAS de Azure Storage
Hola SAS de almacenamiento de Azure vinculada servicio permite toolink un generador de datos de Azure tooan cuenta de almacenamiento de Azure mediante una firma de acceso compartido (SAS). Proporciona factoría de datos de hello con acceso restringido tiempo enlazadas a recursos de tooall/específicos (blob o el contenedor) en el almacenamiento de Hola. toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de la firma de acceso compartido, cree un servicio de SAS de almacenamiento de Azure vinculada. el servicio conjunto Hola vinculado de toodefine una SAS de almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorageSas**. A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:   

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| sasUri |Especificar recursos de almacenamiento de Azure de toohello de URI de firma de acceso compartido como blob, contenedor o tabla. |Sí |

##### <a name="example"></a>Ejemplo

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos Blob de Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureBlob**. A continuación, especifique Hola siguientes propiedades específicas del Blob de Azure en hello **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Contenedor de toohello de ruta de acceso y la carpeta en el almacenamiento de blobs de Hola. Ejemplo: myblobcontainer\myblobfolder\ |Sí |
| fileName |Nombre del blob de Hola. La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.<br/><br/>Si especifica un nombre de archivo, funciona de la actividad (incluida la copia) de hello en Hola Blob en cuestión.<br/><br/>Cuando no se especifica el nombre de archivo, copia incluye todos los Blobs en folderPath hello para el conjunto de datos de entrada.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: datos. <Guid>.txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt |No |
| partitionedBy |partitionedBy es una propiedad opcional. Se pueden usar toospecify un folderPath dinámica y nombre de archivo de datos de series temporales. Por ejemplo, se puede parametrizar folderPath por cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

#### <a name="example"></a>Ejemplo

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


Para más información, consulte el artículo [Conector de Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="blobsource-in-copy-activity"></a>BlobSource en la actividad de copia
Si va a copiar datos desde un almacenamiento de blobs de Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**BlobSource**y especifique después propiedades Hola ** origen ** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola. |True (valor predeterminado), False |No |

#### <a name="example-blobsource"></a>Ejemplo: BlobSource**
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>BlobSink en la actividad de copia
Si va a copiar datos tooan almacenamiento de blobs de Azure, establezca hello **tipo de receptor** de hello actividad de copia demasiado**BlobSink**y especificar después de propiedades en hello **receptor** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| copyBehavior |Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos. |<b>PreserveHierarchy</b>: conserva Hola jerarquía de archivos en la carpeta de destino de Hola. ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola están en hello primero niveles de carpeta de destino. archivos de destino de Hello tienen nombre generado automáticamente. <br/><br/><b>MergeFiles (valor predeterminado):</b> combina todos los archivos del archivo de tooone de carpeta de origen de hello. Si se especifica Hola nombre de archivo o Blob, nombre de archivo combinado Hola sería Hola especificado de lo contrario, sería el nombre de archivo generado automáticamente. |No |

#### <a name="example-blobsink"></a>Ejemplo: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obtener más información, vea el artículo [Conector de Azure Blob](data-factory-azure-blob-connector.md#copy-activity-properties). 

## <a name="azure-data-lake-store"></a>Almacén de Azure Data Lake

### <a name="linked-service"></a>Servicio vinculado
toodefine un servicio de almacén de Azure Data Lake vinculado, Establece el tipo de saludo de hello servicio vinculado demasiado**AzureDataLakeStore**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type | propiedad de tipo Hello debe establecerse en: **AzureDataLakeStore** | Sí |
| dataLakeStoreUri | Especifique la información sobre Hola cuenta de almacén de Azure Data Lake. Se encuentra en hello siguiendo el formato: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`. | Sí |
| subscriptionId | Suscripción de Azure identificador toowhich almacén de Data Lake pertenece. | Necesario para el receptor |
| resourceGroupName | Toowhich de nombre de grupo de recursos de Azure almacén de Data Lake pertenece. | Necesario para el receptor |
| servicePrincipalId | Especifique el identificador de cliente de. la aplicación hello | Sí (para la autenticación de entidad de servicio) |
| servicePrincipalKey | Especifique la clave de la aplicación hello. | Sí (para la autenticación de entidad de servicio) |
| tenant | Especifique la información de inquilino de hello (inquilino o el nombre de identificador de dominio) en que se encuentra la aplicación. Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello portal de Azure. | Sí (para la autenticación de entidad de servicio) |
| authorization | Haga clic en **Authorize** botón en hello **Editor de generador de datos** y escriba sus credenciales que asigna la propiedad de hello autogenerada autorización URL toothis. | Sí (para la autenticación de credenciales de usuario)|
| sessionId | Identificador de sesión de OAuth de sesión de autorización de OAuth de Hola. Cada id. de sesión es único y solo se puede usar una vez. Esta configuración se genera automáticamente al usar el Editor de Data Factory. | Sí (para la autenticación de credenciales de usuario) |

#### <a name="example-using-service-principal-authentication"></a>Ejemplo: uso de la autenticación de entidad de servicio
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Ejemplo: uso de la autenticación de credenciales de usuario
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de almacén de Azure Data Lake conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureDataLakeStore**y especifique Hola propiedades Hola siguientes **typeProperties**sección: 

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| folderPath |Contenedor de toohello de ruta de acceso y la carpeta en hello Azure Data Lake almacenan. |Sí |
| fileName |Nombre del archivo de hello en el almacén de Azure Data Lake Hola. La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas. <br/><br/>Si especifica un nombre de archivo, actividad de hello (incluida la copia) funciona en archivos específicos de Hola.<br/><br/>Cuando no se especifica el nombre de archivo, copia incluye todos los archivos en folderPath hello para el conjunto de datos de entrada.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: datos. <Guid>.txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt |No |
| partitionedBy |partitionedBy es una propiedad opcional. Se pueden usar toospecify un folderPath dinámica y nombre de archivo de datos de series temporales. Por ejemplo, se puede parametrizar folderPath por cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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

Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties). 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Origen de Azure Data Lake Store en la actividad de copia
Si va a copiar datos desde un almacén de Data Lake de Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**AzureDataLakeStoreSource**y especificar después de propiedades en hello **origen**  sección:

**AzureDataLakeStoreSource** admite Hola propiedades siguientes **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola. |True (valor predeterminado), False |No |

#### <a name="example-azuredatalakestoresource"></a>Ejemplo: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Receptor de Azure Data Lake Store en la actividad de copia
Si va a copiar el almacén de datos tooan Azure Data Lake, establezca hello **tipo de receptor** de hello actividad de copia demasiado**AzureDataLakeStoreSink**y especificar después de propiedades en hello **receptor**sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| copyBehavior |Especifica el comportamiento de la copia de Hola. |<b>PreserveHierarchy</b>: conserva Hola jerarquía de archivos en la carpeta de destino de Hola. ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola se crean en el primer nivel de Hola de carpeta de destino. archivos de destino de Hola se crean con el nombre generado automáticamente.<br/><br/><b>MergeFiles</b>: combina todos los archivos del archivo de tooone de carpeta de origen de hello. Si se especifica Hola nombre de archivo o Blob, nombre de archivo combinado Hola sería Hola especificado de lo contrario, sería el nombre de archivo generado automáticamente. |No |

#### <a name="example-azuredatalakestoresink"></a>Ejemplo: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties). 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Servicio vinculado
toodefine una base de datos de Azure Cosmos el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**DocumentDb**y especificar después de propiedades en hello **typeProperties** sección:  

| **Propiedad** | **Descripción** | **Obligatorio** |
| --- | --- | --- |
| connectionString |Especifique la información necesaria de base de datos de tooconnect tooAzure Cosmos DB. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de la base de datos de Azure Cosmos, conjunto hello **tipo** del conjunto de datos de hello demasiado**DocumentDbCollection**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| **Propiedad** | **Descripción** | **Obligatorio** |
| --- | --- | --- |
| collectionName |Nombre de la colección de la base de datos de Azure Cosmos Hola. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Origen de la colección de Azure Cosmos DB en la actividad de copia
Si va a copiar datos desde una base de datos de Azure Cosmos, establezca hello **tipo de origen de** de hello actividad de copia demasiado**DocumentDbCollectionSource**y especificar después de propiedades en hello **origen** sección:


| **Propiedad** | **Descripción** | **Valores permitidos** | **Obligatorio** |
| --- | --- | --- | --- |
| query |Especifique los datos de hello consulta tooread. |Cadena de consulta admitida por Azure Cosmos DB. <br/><br/>Ejemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |No <br/><br/>Si no se especifica, Hola instrucción SQL que se ejecuta:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Tooindicate de carácter especial que Hola documento está anidada |Cualquier carácter. <br/><br/>Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas. Factoría de datos de Azure permite jerarquía toodenote de usuario a través de nestingSeparator, que es "." Hola por encima de los ejemplos. Con separador de hello, actividad de copia de hello generará un objeto de Hola "Name" con los elementos secundarios de tres too"Name.First primera, central y Last, función", "Name.Middle" y "Name.Last" Hola de definición de tabla. |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Receptor de la colección de Azure Cosmos DB en la actividad de copia
Si va a copiar datos tooAzure Cosmos DB, establezca hello **tipo de receptor** de hello actividad de copia demasiado**DocumentDbCollectionSink**y especificar después de propiedades en hello **receptor**sección:

| **Propiedad** | **Descripción** | **Valores permitidos** | **Obligatorio** |
| --- | --- | --- | --- |
| nestingSeparator |Se necesita un carácter especial en hello tooindicate de nombre de columna de origen que anidados de documento. <br/><br/>Por ejemplo anteriormente: `Name.First` en la salida de hello tabla genera Hola siguiendo la estructura JSON en el documento de base de datos de Cosmos hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Carácter que es usado tooseparate niveles de anidamiento.<br/><br/>El valor predeterminado es `.` (punto). |Carácter que es usado tooseparate niveles de anidamiento. <br/><br/>El valor predeterminado es `.` (punto). |
| writeBatchSize |Número de paralelo solicita documentos de toocreate de servicio de base de datos de Cosmos tooAzure.<br/><br/>Puede ajustar el rendimiento de hello cuando se copian datos de base de datos de Azure Cosmos mediante esta propiedad. Puede esperar un rendimiento mejor al aumentar el valor writeBatchSize porque se envían más solicitudes paralelas tooAzure Cosmos DB. Sin embargo deberá tooavoid limitación que puede producir mensajes de bienvenida del error: "Solicitud velocidad es grande".<br/><br/>La limitación de solicitudes se decide mediante una serie de factores, incluidos tamaño de los documentos, número de términos en los documentos, directiva de indexación de colección de destino, etc. Para las operaciones de copia, puede usar una mejor hello toohave de colección (por ejemplo, S3) mayoría rendimiento disponible (2500 solicitud unidades/segundo). |Entero |No (valor predeterminado: 5) |
| writeBatchTimeout |Tiempo de espera para hello operación toocomplete antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).

## <a name="azure-sql-database"></a>Base de datos SQL de Azure

### <a name="linked-service"></a>Servicio vinculado
toodefine una base de datos de SQL Azure vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**AzureSqlDatabase**y especificar después de propiedades en hello **typeProperties**sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| connectionString |Especifique la información necesaria la instancia de base de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola. |Sí |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de la base de datos de SQL Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureSqlTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Azure Hola que servicio vinculado hace referencia a. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
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
Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Origen de SQL en la actividad de copia
Si va a copiar datos desde una base de datos de SQL Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**SqlSource**y especificar después de propiedades en hello **origen** sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Ejemplo: `select * from MyTable`. |No |
| sqlReaderStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola. |Nombre del programa Hola a procedimiento almacenado. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```
Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Receptor de SQL en la actividad de copia
Si va a copiar datos tooAzure base de datos SQL, establezca hello **tipo de receptor** de hello actividad de copia demasiado**SqlSink**y especificar después de propiedades en hello **receptor** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |
| writeBatchSize |Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. |Entero (número de filas) |No (valor predeterminado = 10000) |
| sqlWriterCleanupScript |Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian. |Una instrucción de consulta. |No |
| sliceIdentifierColumnName |Especifique un nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar. |Nombre de columna de una columna con el tipo de datos binarios (32). |No |
| sqlWriterStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola. |Nombre del programa Hola a procedimiento almacenado. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |
| sqlWriterTableType |Especifique un toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola. Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla. Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes. |Un nombre de tipo de tabla. |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties). 

## <a name="azure-sql-data-warehouse"></a>Almacenamiento de datos SQL de Azure

### <a name="linked-service"></a>Servicio vinculado
toodefine un almacenamiento de datos de SQL Azure vinculado servicio, conjunto de hello **tipo** de hello servicio vinculado demasiado**AzureSqlDW**y especificar después de propiedades en hello **typeProperties**sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| connectionString |Especifique la información necesaria la instancia de almacenamiento de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola. |Sí |



#### <a name="example"></a>Ejemplo

```json
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

Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de almacenamiento de datos de SQL Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureSqlDWTable**y especifique Hola propiedades Hola siguientes **typeProperties**sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola o vista de base de datos de almacenamiento de datos de SQL Azure de Hola Hola servicio vinculado hace referencia a. |Sí |

#### <a name="example"></a>Ejemplo

```json
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

Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties). 

### <a name="sql-dw-source-in-copy-activity"></a>Origen de SQL DW en la actividad de copia
Si va a copiar datos desde almacenamiento de datos de SQL Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**SqlDWSource**y especificar después de propiedades en hello **origen**sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable`. |No |
| sqlReaderStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola. |Nombre del programa Hola a procedimiento almacenado. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

### <a name="sql-dw-sink-in-copy-activity"></a>Receptor de SQL DW en la actividad de copia
Si va a copiar datos tooAzure almacenamiento de datos SQL, establezca hello **tipo de receptor** de hello actividad de copia demasiado**SqlDWSink**y especificar después de propiedades en hello **receptor** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian. |Una instrucción de consulta. |No |
| allowPolyBase |Indica si toouse PolyBase (si procede) en lugar de mecanismo BULKINSERT. <br/><br/> **El uso de PolyBase es Hola recomendado de forma que los datos tooload en almacenamiento de datos de SQL.** |True <br/>False (valor predeterminado) |No |
| polyBaseSettings |Un grupo de propiedades que se pueden especificar cuando hello **allowPolybase** propiedad se establece demasiado**true**. |&nbsp; |No |
| rejectValue |Especifica el número de Hola o porcentaje de filas que se pueda rechazar antes de que se produce un error en la consulta de Hola. <br/><br/>Obtener más información acerca de hello PolyBase rechazan opciones Hola **argumentos** sección de [crear tabla externa (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tema. |0 (predeterminado), 1, 2, … |No |
| rejectType |Especifica si se especifica la opción de hello rejectValue como un valor literal o un porcentaje. |Valor (predeterminado), Porcentaje |No |
| rejectSampleValue |Determina el número de Hola de tooretrieve filas antes de hello PolyBase vuelve a calcular el porcentaje de Hola de filas rechazados. |1, 2, … |Sí, si el valor de **rejectType** es **percentage** |
| useTypeDefault |Especifica cómo toohandle valores que falten en archivos delimitados por texto cuando PolyBase recupera datos de archivo de texto hello.<br/><br/>Más información acerca de esta propiedad desde la sección de argumentos de hello en [crear EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (predeterminada) |No |
| writeBatchSize |Inserta los datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize |Entero (número de filas) |No (valor predeterminado = 10000) |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

## <a name="azure-search"></a>Búsqueda de Azure

### <a name="linked-service"></a>Servicio vinculado
el servicio conjunto Hola vinculado de toodefine una búsqueda de Azure **tipo** de hello servicio vinculado demasiado**AzureSearch**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| url | Dirección URL de hello servicio Búsqueda de Azure. | Sí |
| key | Clave de administrador de hello servicio Búsqueda de Azure. | Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de búsqueda de Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureSearchIndex**y especifique Hola propiedades Hola siguientes **typeProperties** sección : 

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| type | se debe establecer propiedad de tipo Hello demasiado**AzureSearchIndex**.| Sí |
| indexName | Nombre del índice de búsqueda de Azure Hola. Factoría de datos no crea el índice de Hola. índice de Hello debe existir en la búsqueda de Azure. | Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Para más información, consulte el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#dataset-properties).

### <a name="azure-search-index-sink-in-copy-activity"></a>Receptor del índice de Azure Search en la actividad de copia
Si va a copiar el índice de búsqueda de Azure de tooan de datos, establecer hello **tipo de receptor** de hello actividad de copia demasiado**AzureSearchIndexSink**y especificar después de propiedades en hello **receptor**sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Especifica si toomerge o reemplazar cuando un documento ya existe en el índice de Hola. | Combinar (predeterminado)<br/>Cargar| No |
| WriteBatchSize | Carga datos en el índice de búsqueda de Azure de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. | 1 too1, 000. El valor predeterminado es 1000. | No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
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
        }]
    }
}
```

Para obtener más información, vea el artículo [Conector de Azure Search](data-factory-azure-search-connector.md#copy-activity-properties).

## <a name="azure-table-storage"></a>Azure Table Storage

### <a name="linked-service"></a>Servicio vinculado
Hay dos tipos de servicios vinculados: servicio vinculado de Azure Storage y servicio vinculado de SAS de Azure Storage.

#### <a name="azure-storage-linked-service"></a>Servicio vinculado de Almacenamiento de Azure
toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de hello **clave de cuenta**, cree un servicio vinculado de almacenamiento de Azure. el servicio conjunto Hola vinculado de toodefine un almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorage**. A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type |propiedad de tipo Hello debe establecerse en: **azurestorage.** |Sí |
| connectionString |Especifique la información necesaria tooconnect tooAzure almacenamiento para la propiedad connectionString de Hola. |Sí |

**Ejemplo:**  

```json
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

#### <a name="azure-storage-sas-linked-service"></a>Servicio vinculado de SAS de Azure Storage
Hola SAS de almacenamiento de Azure vinculada servicio permite toolink un generador de datos de Azure tooan cuenta de almacenamiento de Azure mediante una firma de acceso compartido (SAS). Proporciona factoría de datos de hello con acceso restringido tiempo enlazadas a recursos de tooall/específicos (blob o el contenedor) en el almacenamiento de Hola. toolink su factoría de datos de almacenamiento de Azure cuenta tooa mediante el uso de la firma de acceso compartido, cree un servicio de SAS de almacenamiento de Azure vinculada. el servicio conjunto Hola vinculado de toodefine una SAS de almacenamiento de Azure **tipo** de hello servicio vinculado demasiado**AzureStorageSas**. A continuación, puede especificar siguientes propiedades en hello **typeProperties** sección:   

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type |propiedad de tipo Hello debe establecerse en: **AzureStorageSas** |Sí |
| sasUri |Especificar recursos de almacenamiento de Azure de toohello de URI de firma de acceso compartido como blob, contenedor o tabla. |Sí |

**Ejemplo:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Para más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de la tabla de Azure, conjunto hello **tipo** del conjunto de datos de hello demasiado**AzureTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en la instancia de base de datos de tabla de Azure de Hola que servicio vinculado que hace referencia a. |Sí. Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada. Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada. |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
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

Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#dataset-properties). 

### <a name="azure-table-source-in-copy-activity"></a>Origen de Azure Table en la actividad de copia
Si va a copiar datos desde el almacenamiento de tabla de Azure, establezca hello **tipo de origen de** de hello actividad de copia demasiado**AzureTableSource**y especificar después de propiedades en hello **origen**sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta de tabla de Azure. Vea los ejemplos en la sección siguiente Hola. |No. Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada. Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada. |
| azureTableSourceIgnoreTableNotFound |Indica si debe Hola excepción de tabla no existe. |TRUE<br/>FALSE |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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
        }]
    }
}
```

Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties). 

### <a name="azure-table-sink-in-copy-activity"></a>Receptor de Azure Table en la actividad de copia
Si va a copiar datos tooAzure almacenamiento de tabla, establecer hello **tipo de receptor** de hello actividad de copia demasiado**AzureTableSink**y especificar después de propiedades en hello **receptor** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Partición clave valor predeterminado que se puede usar en el receptor de Hola. |Valor de cadena. |No |
| azureTablePartitionKeyName |Especifique el nombre de columna de hello cuyos valores se usan como claves de partición. Si no se especifica, AzureTableDefaultPartitionKeyValue se usa como clave de partición de Hola. |Un nombre de columna. |No |
| azureTableRowKeyName |Especifique el nombre de columna de hello cuyos valores de columna se utilizan como clave de fila. Si no se especifica, use un GUID para cada fila. |Un nombre de columna. |No |
| azureTableInsertType |datos de tooinsert de modo de saludo en tabla de Azure.<br/><br/>Esta propiedad controla si las filas existentes en la tabla de salida de hello con claves de partición y fila coincidentes tienen sus valores reemplazará o se combinará. <br/><br/>toolearn acerca de cómo funcionan estas configuraciones (combinación y reemplazo), consulte [Insert o Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) y [insertar o reemplazar entidades](https://msdn.microsoft.com/library/azure/hh452242.aspx) temas. <br/><br> Esta configuración se aplica a nivel de fila de hello, no nivel de tabla de hello, y ninguna de estas opciones eliminan las filas de tabla de salida de hello que no existen en la entrada de Hola. |merge (predeterminado)<br/>replace |No |
| writeBatchSize |Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout. |Entero (número de filas) |No (valor predeterminado = 10000) |
| writeBatchTimeout |Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout |timespan<br/><br/>Ejemplo: "00:20:00" (20 minutos) |No (valor de tiempo de espera predeterminado toostorage cliente predeterminado 90 seg) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
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
        }]
    }
}
```
Para obtener más información sobre estos servicios vinculados, vea el artículo [Conector de Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties). 

## <a name="amazon-redshift"></a>Amazon RedShift

### <a name="linked-service"></a>Servicio vinculado
toodefine un Amazon Redshift el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**AmazonRedshift**y especificar después de propiedades en hello **typeProperties**sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Servidor |IP dirección o nombre de host del servidor de Amazon Redshift Hola. |Sí |
| puerto |número de Hola de puerto TCP Hola Hola Amazon Redshift server usa toolisten para las conexiones de cliente. |No, valor predeterminado: 5439 |
| database |Nombre de base de datos de Amazon Redshift Hola. |Sí |
| nombre de usuario |Nombre de usuario que tenga la base de datos de access toohello. |Sí |
| Contraseña |Contraseña de cuenta de usuario de Hola. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de Amazon Redshift conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en base de datos de Amazon Redshift de hello servicio vinculado que hace referencia a. |No (si se especifica **query** de **RelationalSource**) |


#### <a name="example"></a>Ejemplo

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia 
Si va a copiar datos de Amazon Redshift, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable`. |No (si se especifica **tableName** de **dataset**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Para más información, consulte el artículo [Conector de Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Servicio vinculado
el servicio conjunto Hola vinculado de toodefine un IBM DB2 **tipo** de hello servicio vinculado demasiado**OnPremisesDB2**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Servidor |Nombre del servidor de hello DB2. |Sí |
| database |Nombre de base de datos de DB2 Hola. |Sí |
| schema |Nombre del esquema de hello en la base de datos de Hola. nombre del esquema Hola distingue mayúsculas de minúsculas. |No |
| authenticationType |Tipo de autenticación que utiliza la base de datos de DB2 tooconnect toohello. Los valores posibles son: Anonymous, Basic y Windows. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación Basic o Windows. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de DB2 de tooconnect toohello local. |Sí |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
conjunto de datos de DB2 toodefine, Hola de conjunto **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en la instancia de base de datos DB2 de Hola que servicio vinculado que hace referencia a. Hola tableName distingue mayúsculas de minúsculas. |No (si se especifica **query** de **RelationalSource**) 

#### <a name="example"></a>Ejemplo
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos de IBM DB2, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `"query": "select * from "MySchema"."MyTable""`. |No (si se especifica **tableName** de **dataset**) |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Para más información, consulte el artículo [Conector de IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Servicio vinculado
toodefine MySQL el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesMySql**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Servidor |Nombre del servidor de MySQL Hola. |Sí |
| database |Nombre de base de datos de MySQL Hola. |Sí |
| schema |Nombre del esquema de hello en la base de datos de Hola. |No |
| authenticationType |Tipo de autenticación que utiliza la base de datos de MySQL tooconnect toohello. Los valores posibles son: `Basic`. |Sí |
| nombre de usuario |Especifique la base de datos MySQL toohello de tooconnect de nombre de usuario. |Sí |
| Contraseña |Especifique la contraseña de cuenta de usuario de hello especificada. |Sí |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de MySQL de tooconnect toohello local. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos MySQL, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola Hola instancia de base de datos MySQL que hace referencia el servicio vinculado. |No (si se especifica **query** de **RelationalSource**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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
Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos desde una base de datos MySQL, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable`. |No (si se especifica **tableName** de **dataset**) |


#### <a name="example"></a>Ejemplo
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties). 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Servicio vinculado
toodefine de Oracle vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**OnPremisesOracle**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| driverType | Especificar qué controlador toouse toocopy datos / tooOracle base de datos. Los valores permitidos son **Microsoft** u **ODP** (valor predeterminado). Consulte la sección [Versiones compatibles e instalación](#supported-versions-and-installation) para obtener información detallada sobre los controladores. | No |
| connectionString | Especifique la información necesaria la instancia de base de datos de Oracle toohello tooconnect para la propiedad connectionString de Hola. | Sí |
| gatewayName | Nombre de puerta de enlace de Hola que es usado tooconnect toohello servidor Oracle local |Sí |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de Oracle, conjunto hello **tipo** del conjunto de datos de hello demasiado**OracleTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola Hola base de datos de Oracle que Hola servicio vinculado que hace referencia a. |No (si se especifica **oracleReaderQuery** de **OracleSource**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
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
Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).

### <a name="oracle-source-in-copy-activity"></a>Origen de Oracle en la actividad de copia
Si va a copiar datos desde una base de datos de Oracle, establezca hello **tipo de origen de** de hello actividad de copia demasiado**OracleSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| oracleReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable` <br/><br/>Si no se especifica, Hola instrucción SQL que se ejecuta:`select * from MyTable` |No (si se especifica **tableName** de **dataset**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

### <a name="oracle-sink-in-copy-activity"></a>Receptor de Oracle en la actividad de copia
Si va a copiar la base de datos de Oracle de tooam de datos, establecer hello **tipo de receptor** de hello actividad de copia demasiado**OracleSink**y especificar después de propiedades en hello **receptor** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: 00:30:00 (30 minutos). |No |
| writeBatchSize |Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. |Entero (número de filas) |No (valor predeterminado: 100) |
| sqlWriterCleanupScript |Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian. |Una instrucción de consulta. |No |
| sliceIdentifierColumnName |Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar. |Nombre de columna de una columna con el tipo de datos binarios (32). |No |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Para más información, consulte el artículo [Conector de Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Servicio vinculado
toodefine un PostgreSQL el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesPostgreSql**y especificar después de propiedades en hello **typeProperties**sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Servidor |Nombre del servidor de hello PostgreSQL. |Sí |
| database |Nombre de base de datos de PostgreSQL Hola. |Sí |
| schema |Nombre del esquema de hello en la base de datos de Hola. nombre del esquema Hola distingue mayúsculas de minúsculas. |No |
| authenticationType |Tipo de autenticación que utiliza la base de datos de PostgreSQL tooconnect toohello. Los valores posibles son: Anonymous, Basic y Windows. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación Basic o Windows. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de PostgreSQL local de tooconnect toohello. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos PostgreSQL conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola Hola instancia de base de datos PostgreSQL que hace referencia el servicio vinculado. Hola tableName distingue mayúsculas de minúsculas. |No (si se especifica **query** de **RelationalSource**) |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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
Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos desde una base de datos PostgreSQL, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: "query": "select * from \"MySchema\".\"MyTable\"". |No (si se especifica **tableName** de **dataset**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Servicio vinculado
toodefine un almacenamiento de negocios de SAP (BW) el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**SapBw**y especificar después de propiedades en hello **typeProperties**sección:  

Propiedad | Descripción | Valores permitidos | Obligatorio
-------- | ----------- | -------------- | --------
Servidor | Nombre del servidor de hello en qué Hola SAP BW reside la instancia. | cadena | Sí
systemNumber | Número de sistema de hello sistema SAP BW. | Número decimal de dos dígitos que se representa en forma de cadena. | Sí
clientId | Identificador de cliente del cliente de Hola Hola sistema SAP W. | Número decimal de tres dígitos que se representa en forma de cadena. | Sí
nombre de usuario | Nombre de usuario de Hola que tiene el servidor de acceso toohello SAP | cadena | Sí
Contraseña | Contraseña de usuario de Hola. | cadena | Sí
gatewayName | Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la instancia de SAP BW de tooconnect toohello local. | cadena | Sí
encryptedCredential | Hola cifra la cadena de credenciales. | cadena | No

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de SAP BW, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**. No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP BW de Hola de tipo **RelationalTable**.  

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos de SAP Business Warehouse, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query | Especifica Hola MDX consultar tooread datos de instancia de SAP BW Hola. | Consulta MDX. | Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties). 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Servicio vinculado
toodefine un SAP HANA el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**SapHana**y especificar después de propiedades en hello **typeProperties** sección:  

Propiedad | Descripción | Valores permitidos | Obligatorio
-------- | ----------- | -------------- | --------
Servidor | Nombre del servidor de hello en qué Hola SAP HANA reside la instancia. Si el servidor usa un puerto personalizado, especifique `server:port`. | string | Sí
authenticationType | Tipo de autenticación. | cadena. "Basic" o "Windows" | Sí 
nombre de usuario | Nombre de usuario de Hola que tiene el servidor de acceso toohello SAP | cadena | Sí
Contraseña | Contraseña de usuario de Hola. | cadena | Sí
gatewayName | Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la instancia de SAP HANA de tooconnect toohello local. | cadena | Sí
encryptedCredential | Hola cifra la cadena de credenciales. | cadena | No

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).
 
### <a name="dataset"></a>Dataset
toodefine un conjunto de datos SAP HANA, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**. No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP HANA de Hola de tipo **RelationalTable**. 

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos desde un almacén de datos de SAP HANA, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query | Especifica Hola SQL permite consultar tooread datos de instancia de SAP HANA Hola. | Consulta SQL. | Sí |


#### <a name="example"></a>Ejemplo


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>Servicio vinculado
Crear un servicio vinculado de tipo **onpremisessqlserver** toolink una factoría de datos local tooa de base de datos de SQL Server. Hello en la tabla siguiente proporciona la descripción del servicio de SQL Server vinculado de JSON elementos tooon local específico.

Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSQL servicio del servidor vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **onpremisessqlserver**. |Sí |
| connectionString |Especificar información de connectionString necesaria tooconnect toohello en SQL Server base de datos local con autenticación de SQL o autenticación de Windows. |Sí |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de SQL Server de tooconnect toohello local. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación de Windows. Ejemplo: **nombreDeDominio\\nombreDeUsuario**. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |

Puede cifrar las credenciales con hello **New-AzureRmDataFactoryEncryptValue** cmdlet y usarlos en la cadena de conexión de hello tal y como se muestra en el siguiente ejemplo de Hola (**EncryptedCredential** propiedad):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Ejemplo: JSON para usar autenticación de SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Ejemplo: JSON para usar autenticación de Windows

Si se especifiquen el nombre de usuario y contraseña, puerta de enlace usa hello tooimpersonate base de datos de usuario especificado cuenta tooconnect toohello local SQL Server. En caso contrario, la puerta de enlace conecta toohello SQL Server directamente con el contexto de seguridad de Hola de puerta de enlace (su cuenta de inicio).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de SQL Server, conjunto de hello **tipo** del conjunto de datos de hello demasiado**SqlServerTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Server de Hola que servicio vinculado hace referencia a. |Sí |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
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

Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Origen de SQL en la actividad de copia
Si va a copiar datos desde una base de datos de SQL Server, establezca hello **tipo de origen de** de hello actividad de copia demasiado**SqlSource**y especificar después de propiedades en hello **origen** sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable`. Puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola. Si no se especifica, Hola instrucción SQL ejecutada: select from MyTable. |No |
| sqlReaderStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola. |Nombre del programa Hola a procedimiento almacenado. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |

Si hello **sqlReaderQuery** se especifica para hello SqlSource, hello actividad de copia ejecuta esta consulta en datos de Hola de hello base de datos de SQL Server origen tooget.

Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).

Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.

> [!NOTE]
> Cuando usas **sqlReaderStoredProcedureName**, seguirá necesitando toospecify un valor para hello **tableName** propiedad Hola de conjunto de datos JSON. Pero no se ha realizado ninguna validación en esta tabla.


#### <a name="example"></a>Ejemplo
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```

En este ejemplo, **sqlReaderQuery** se especifica para hello SqlSource. Hola actividad de copia ejecuta esta consulta contra Hola datos de saludo de tooget de origen de base de datos de SQL Server. Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros). Hola sqlReaderQuery puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola. No es limitado tooonly Hola tabla establecido como Hola typeProperty de nombre de tabla del conjunto de datos.

Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.

Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Receptor de SQL en la actividad de copia
Si va a copiar la base de datos de SQL Server de tooa de datos, establecer hello **tipo de receptor** de hello actividad de copia demasiado**SqlSink**y especificar después de propiedades en hello **receptor** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |
| writeBatchSize |Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. |Entero (número de filas) |No (valor predeterminado = 10000) |
| sqlWriterCleanupScript |Especificar la consulta para tooexecute de actividad de copia que se limpian los datos de un segmento específico. Consulte la [sección sobre repetibilidad](#repeatability-during-copy) para más información. |Una instrucción de consulta. |No |
| sliceIdentifierColumnName |Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar. Consulte la [sección sobre repetibilidad](#repeatability-during-copy) para más información. |Nombre de columna de una columna con el tipo de datos binarios (32). |No |
| sqlWriterStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola. |Nombre del programa Hola a procedimiento almacenado. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |
| sqlWriterTableType |Especifique toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola. Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla. Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes. |Un nombre de tipo de tabla. |No |

#### <a name="example"></a>Ejemplo
canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Servicio vinculado
toodefine un Sybase vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**OnPremisesSybase**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Servidor |Nombre del servidor de Sybase Hola. |Sí |
| database |Nombre de base de datos de Sybase Hola. |Sí |
| schema |Nombre del esquema de hello en la base de datos de Hola. |No |
| authenticationType |Tipo de autenticación usa tooconnect toohello bases de datos Sybase. Los valores posibles son: Anonymous, Basic y Windows. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación Basic o Windows. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de Sybase local de tooconnect toohello. |Sí |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de Sybase, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola Hola instancia de base de datos de Sybase que hace referencia el servicio vinculado. |No (si se especifica **query** de **RelationalSource**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos desde una base de datos de Sybase, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable`. |No (si se especifica **tableName** de **dataset**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Servicio vinculado
toodefine un Teradata el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesTeradata**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Servidor |Nombre del servidor de Teradata Hola. |Sí |
| authenticationType |Tipo de autenticación que utiliza la base de datos de Teradata tooconnect toohello. Los valores posibles son: Anonymous, Basic y Windows. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación Basic o Windows. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de Teradata local de tooconnect toohello. |Sí |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos Teradata Blob, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**. Actualmente, no hay ninguna propiedad de tipo compatible con el conjunto de datos de hello Teradata. 

#### <a name="example"></a>Ejemplo
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos desde una base de datos de Teradata, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen**sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable`. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Para más información, consulte el artículo [Conector de Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Servicio vinculado
toodefine un Casandra el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesCassandra**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| host |Una o varias direcciones IP o nombres de host de los servidores de Cassandra.<br/><br/>Especifique una lista separada por comas de direcciones IP o servidores de tooall de tooconnect de nombres de host al mismo tiempo. |Sí |
| puerto |Hola el puerto TCP que Hola server Casandra utiliza toolisten para las conexiones de cliente. |No. El valor predeterminado es 9042. |
| authenticationType |Básica o anónima |Sí |
| nombre de usuario |Especifique el nombre de usuario para la cuenta de usuario de Hola. |Sí, si authenticationType se establece tooBasic. |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola. |Sí, si authenticationType se establece tooBasic. |
| gatewayName |nombre de Hola de puerta de enlace de Hola que es la base de datos de uso tooconnect toohello local Casandra. |Sí |
| encryptedCredential |Credencial cifrada por la puerta de enlace de Hola. |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos Casandra conjunto hello **tipo** del conjunto de datos de hello demasiado**CassandraTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| keyspace |Nombre de keyspace de Hola o esquema de base de datos de Casandra. |Sí (si no hay definida ninguna **consulta** para **CassandraSource**). |
| tableName |Nombre de tabla de hello en la base de datos de Casandra. |Sí (si no hay definida ninguna **consulta** para **CassandraSource**). |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties). 

### <a name="cassandra-source-in-copy-activity"></a>Origen de Cassandra en la actividad de copia
Si va a copiar datos desde Casandra, establezca hello **tipo de origen de** de hello actividad de copia demasiado**CassandraSource**y especificar después de propiedades en hello **origen** sección :

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Consulta SQL-92 o consulta CQL. Vea la [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)(referencia de CQL). <br/><br/>Al usar una consulta SQL, especifique **keyspace name.table nombre** tabla de hello toorepresent desea tooquery. |No (si tableName y el espacio de claves del conjunto de datos están definidos). |
| consistencyLevel |el nivel de coherencia de Hello especifica cuántas réplicas debe responder tooa solicitud de lectura antes de devolver la aplicación de cliente de toohello de datos. Comprobaciones de Casandra Hola número de réplicas especificado para la solicitud de lectura de hello toosatisfy de datos. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Para más información, consulte [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configuración de la coherencia de datos). |No. El valor predeterminado es ONE. |

#### <a name="example"></a>Ejemplo
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Servicio vinculado
toodefine un MongoDB el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesMongoDB**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Servidor |IP dirección o nombre de host del servidor de MongoDB Hola. |Sí |
| puerto |El puerto TCP que Hola MongoDB server usa toolisten para las conexiones de cliente. |Valor predeterminado opcional: 27017 |
| authenticationType |Básica o anónima. |Sí |
| nombre de usuario |Tooaccess de cuenta de usuario MongoDB. |Sí (si se usa la autenticación básica). |
| Contraseña |Contraseña de usuario de Hola. |Sí (si se usa la autenticación básica). |
| authSource |Nombre de base de datos de MongoDB de Hola que quiere toouse toocheck sus credenciales de autenticación. |Opcional (si se usa la autenticación básica). valor predeterminado: utiliza la cuenta de administrador de Hola y base de datos de hello especificada mediante la propiedad databaseName. |
| databaseName |Nombre de base de datos de MongoDB de Hola que desea tooaccess. |Sí |
| gatewayName |Nombre de puerta de enlace de Hola que tiene acceso a almacén de datos de Hola. |Sí |
| encryptedCredential |Credencial cifrada por la puerta de enlace. |Opcional |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para obtener más información, vea el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos MongoDB, conjunto hello **tipo** del conjunto de datos de hello demasiado**MongoDbCollection**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| collectionName |Nombre de colección de hello en la base de datos de MongoDB. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

Para más información, consulte el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).

#### <a name="mongodb-source-in-copy-activity"></a>Origen de MongoDB en la actividad de copia
Si va a copiar datos de MongoDB, establezca hello **tipo de origen de** de hello actividad de copia demasiado**MongoDbSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL-92. Por ejemplo: `select * from MyTable`. |No (si se especifica **collectionName** de **dataset**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Servicio vinculado
toodefine un S3 Amazon el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**AwsAccessKey**y especificar después de propiedades en hello **typeProperties** sección :  

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| accessKeyID |Id. de clave de acceso de los secretos de Hola. |cadena |Sí |
| secretAccessKey |clave de acceso de los secretos de Hello propio. |Cadena secreta cifrada |Sí |

#### <a name="example"></a>Ejemplo
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
conjunto de datos de toodefine un S3 de Amazon, conjunto hello **tipo** del conjunto de datos de hello demasiado**AmazonS3**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| bucketName |nombre del depósito de Hello S3. |String |Sí |
| key |clave del objeto Hola S3. |String |No |
| prefix |Prefijo para la clave del objeto Hola S3. Se seleccionan objetos cuyas claves comienzan por este prefijo. Se aplica solo cuando la clave está vacía. |string |No |
| versión |versión de Hola del objeto de S3 si está habilitado el control de versiones de S3. |String |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No | |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Hola admitida niveles son: **óptimo** y **más rápido**. Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No | |


> [!NOTE]
> bucketName + clave especifica la ubicación de Hola Hola S3 de objeto de donde depósitos es el contenedor de raíz de Hola para S3 objetos y la clave es objeto de tooS3 de ruta de acceso completa de Hola.

#### <a name="example-sample-dataset-with-prefix"></a>Ejemplo: Conjunto de datos de ejemplo con prefijo

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>Ejemplo: Conjunto de datos de ejemplo (con versión)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>Ejemplo: Rutas de acceso dinámicas para S3
En el ejemplo de Hola, utilizamos valores fijos para las propiedades de clave y bucketName en el conjunto de datos de hello S3 de Amazon.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

Puede tener factoría de datos calcular clave hello y bucketName dinámicamente en tiempo de ejecución mediante el uso de variables del sistema como SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Puede hacer Hola mismo para la propiedad de prefijo de Hola de un conjunto de datos de Amazon S3. Consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md) para ver una lista de funciones y variables admitidas.

Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origen de Sistema de archivos en la actividad de copia
Si va a copiar datos de Amazon S3, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección :


| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Especifica si toorecursively lista S3 objetos en el directorio de Hola. |true/false |No |


#### <a name="example"></a>Ejemplo


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>Sistema de archivos


### <a name="linked-service"></a>Servicio vinculado
Puede vincular un generador de datos de Azure local tooan de sistema de archivo con hello **servidor de archivos local** servicio vinculado. Hello en la tabla siguiente proporciona descripciones para los elementos JSON que sean específico toohello servicio servidor de archivos local vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |Asegúrese de que la propiedad de tipo hello está establecido demasiado**OnPremisesFileServer**. |Sí |
| host |Especifica la ruta de acceso de raíz de Hola de carpeta de Hola que desea toocopy. Utilice el carácter de escape de hello ' \ ' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) . |Sí |
| userid |Especifique el identificador de Hola Hola del usuario de que tiene acceso toohello servidor. |No (si elige encryptedCredential) |
| Contraseña |Especifique la contraseña de hello para el usuario de hello (userid). |No (si elige encryptedCredential) |
| encryptedCredential |Especifique las credenciales de hello cifrada que pueden obtener ejecutando el cmdlet New-AzureRmDataFactoryEncryptValue Hola. |No (si elige toospecify identificador de usuario y una contraseña en texto sin formato) |
| gatewayName |Especifica el nombre de Hola de puerta de enlace de Hola que factoría de datos debe usar el servidor de archivos de tooconnect toohello local. |Sí |

#### <a name="sample-folder-path-definitions"></a>Definiciones de ruta de acceso a la carpeta de ejemplo 
| Escenario | Host en definición de servicio vinculado | folderPath en definición de conjunto de datos |
| --- | --- | --- |
| Carpeta local en la máquina de Data Management Gateway::  <br/><br/>Ejemplos: D:\\\* o D:\folder\subfolder\\* |D:\\\\ (para Data Management Gateway 2.0 y versiones posteriores) <br/><br/> localhost (para versiones anteriores a Data Management Gateway 2.0) |\\\\ o la carpeta\\\\subcarpeta (Data Management Gateway 2.0 y versiones posteriores) <br/><br/>D:\\\\ o D:\\\\carpeta\\\\subcarpeta (para versiones de la puerta de enlace interiores a 2.0) |
| Carpeta compartida remota:  <br/><br/>Ejemplos: \\\\myserver\\share\\\* o \\\\myserver\\share\\folder\\subfolder\\* |\\\\\\\\myserver\\\\ |.\\\\ o carpeta\\\\subcarpeta |


#### <a name="example-using-username-and-password-in-plain-text"></a>Ejemplo: uso de nombre de usuario y contraseña en texto sin formato

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Ejemplo: uso de encryptedcredential

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos del sistema de archivos, conjunto hello **tipo** del conjunto de datos de hello demasiado**FileShare**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Especifica la carpeta de hello subruta toohello. Utilice el carácter de escape de hello ' \' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .<br/><br/>Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin. |Sí |
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de Hola del archivo hello generado es Hola siguiendo el formato: <br/><br/>`Data.<Guid>.txt` (Ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |No |
| fileFilter |Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos. <br/><br/>Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).<br/><br/>Ejemplo 1: "fileFilter": "*.log"<br/>Ejemplo 2: "fileFilter": 2016-1-?.txt"<br/><br/>Tenga en cuenta que fileFilter es aplicable a un conjunto de datos de FileShare de entrada. |No |
| partitionedBy |Puede usar partitionedBy toospecify dinámica folderPath/nombre de archivo para los datos de serie temporal. Por ejemplo, folderPath se parametriza por cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido). consulte [Formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> No se puede usar fileName y fileFilter a la vez.

#### <a name="example"></a>Ejemplo

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
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

Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origen de Sistema de archivos en la actividad de copia
Si va a copiar datos de sistema de archivos, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si los datos de Hola es de lectura de forma recursiva de las subcarpetas de Hola o solo de la carpeta especificada de Hola. |True, False (predeterminada) |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
        }]
    }
}
```
Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>Receptor de Sistema de archivos en la actividad de copia
Si va a copiar datos tooFile sistema, establezca hello **tipo de receptor** de hello actividad de copia demasiado**FileSystemSink**y especificar después de propiedades en hello **receptor** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| copyBehavior |Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos. |**PreserveHierarchy:** conserva la jerarquía de archivos de hello en la carpeta de destino de Hola. Es decir, ruta de acceso relativa de Hola de carpeta de origen de toohello de archivo de origen de hello es Hola igual a la ruta de acceso relativa de Hola de carpeta de destino de toohello de archivo de destino de Hola.<br/><br/>**FlattenHierarchy:** todos los archivos de la carpeta de origen Hola se crean en el primer nivel de Hola de carpeta de destino. archivos de destino de Hola se crean con un nombre generado automáticamente.<br/><br/>**MergeFiles:** combina todos los archivos del archivo de tooone de carpeta de origen de hello. Si se especifica el nombre de blob/nombre de archivo de hello, nombre de archivo combinado de hello es nombre especificado de Hola. De lo contrario, es un nombre de archivo generado automáticamente. |No |
auto-

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para más información, consulte el artículo [Conector del sistema de archivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Servicio vinculado
toodefine FTP el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**FtpServer**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| host |Nombre o dirección IP del servidor FTP de Hola |Sí |&nbsp; |
| authenticationType |Especificar el tipo de autenticación |yes |Basic, Anonymous |
| nombre de usuario |Usuario que tiene acceso toohello FTP server |No |&nbsp; |
| Contraseña |Contraseña de usuario de hello (nombre de usuario) |No |&nbsp; |
| encryptedCredential |Servidor FTP de credenciales cifradas tooaccess Hola |No |&nbsp; |
| gatewayName |Nombre de puerta de enlace tooconnect tooan de hello Data Management Gateway servidor FTP local |No |&nbsp; |
| puerto |Puerto en qué Hola FTP está escuchando el servidor |No |21 |
| enableSsl |Especifique si toouse FTP a través de canal SSL/TLS |No |true |
| enableServerCertificateValidation |Especifica si, cuando se utiliza FTP a través de canal SSL/TLS, se validación de certificado de servidor SSL de tooenable |No |true |

#### <a name="example-using-anonymous-authentication"></a>Ejemplo: Uso de autenticación anónima

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Ejemplo: Uso de nombre de usuario y contraseña en texto sin formato para la autenticación básica

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Ejemplo: Uso de puerto, enableSsl, enableServerCertificateValidation

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Ejemplo: Uso de encryptedCredential para la autenticación y la puerta de enlace

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
conjunto de datos de toodefine FTP, conjunto de Hola **tipo** del conjunto de datos de Hola demasiado**recurso compartido de archivos**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Carpeta de toohello de ruta de acceso de Sub. Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .<br/><br/>Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin. |Sí 
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: <br/><br/>Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.<br/><br/>Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).<br/><br/>Ejemplos 1: `"fileFilter": "*.log"`<br/>Ejemplo 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter es aplicable a un conjunto de datos FileShare de entrada. Esta propiedad no es compatible con HDFS. |No |
| partitionedBy |partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales. Por ejemplo, folderPath se parametriza por cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido). Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Especifica si se usará el modo de transferencia binario. Su valor es true para el modo binario y false para ASCII. Valor predeterminado: true. Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer. |No |

> [!NOTE]
> filename y fileFilter no pueden usarse simultáneamente.

#### <a name="example"></a>Ejemplo

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origen de Sistema de archivos en la actividad de copia
Si va a copiar datos desde un servidor FTP, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola. |True, False (predeterminada) |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de FTP](data-factory-ftp-connector.md#copy-activity-properties).


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>Servicio vinculado
toodefine un HDFS el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**Hdfs**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **Hdfs** |Sí |
| URL |Dirección URL toohello HDFS |Sí |
| authenticationType |Anónima o Windows. <br><br> toouse **la autenticación Kerberos** para conector HDFS, consulte demasiado[en esta sección](#use-kerberos-authentication-for-hdfs-connector) tooset del entorno local en consecuencia. |Sí |
| userName |Nombre de usuario para la autenticación de Windows |Sí (para la autenticación de Windows) |
| contraseña |Contraseña para la autenticación de Windows |Sí (para la autenticación de Windows) |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar tooconnect toohello HDFS. |Sí |
| encryptedCredential |[Nueva AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) salida de credenciales de acceso de Hola. |No |

#### <a name="example-using-anonymous-authentication"></a>Ejemplo: Uso de autenticación anónima

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Ejemplo: Uso de autenticación de Windows

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos HDFS conjunto hello **tipo** del conjunto de datos de hello demasiado**FileShare**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Carpeta de toohello de ruta de acceso. Ejemplo: `myfolder`<br/><br/>Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola. Por ejemplo: para folder\subfolder, especifique la carpeta\\\\subcarpeta y para d:\samplefolder, especifique d:\\\\samplefolder.<br/><br/>Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin. |Sí |
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: <br/><br/>Data<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| partitionedBy |partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales. Por ejemplo, folderPath se parametriza para cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> filename y fileFilter no pueden usarse simultáneamente.

#### <a name="example"></a>Ejemplo

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Origen de Sistema de archivos en la actividad de copia
Si va a copiar datos desde HDFS, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:

**FileSystemSource** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola. |True, False (predeterminada) |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Servicio vinculado
toodefine un SFTP el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**Sftp**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- | --- |
| host | Nombre o dirección IP del servidor SFTP de Hola. |Sí |
| puerto |Puerto en qué Hola SFTP servidor está escuchando. es el valor predeterminado de Hello: 21 |No |
| authenticationType |Especifique el tipo de autenticación. Valores permitidos: **Básica**, **SshPublicKey**. <br><br> Consulte demasiado[mediante la autenticación básica](#using-basic-authentication) y [utilizando SSH autenticación de clave pública](#using-ssh-public-key-authentication) secciones en más propiedades y ejemplos JSON, respectivamente. |Sí |
| skipHostKeyValidation | Especificar si tooskip validación de clave de host. | No. Hola valor predeterminado: false |
| hostKeyFingerprint | Especifique la huella dactilar de Hola de clave de host de Hola. | Sí si hello `skipHostKeyValidation` se establece toofalse.  |
| gatewayName |Nombre de hello Data Management Gateway tooconnect tooan local servidor SFTP. | Sí, si va a copiar datos desde un servidor SFTP local. |
| encryptedCredential | Servidor de credenciales cifradas tooaccess Hola SFTP. Generado automáticamente cuando se especifica la autenticación básica (nombre de usuario y contraseña) o SshPublicKey (nombre de usuario + ruta de acceso de clave privada o contenido) en copia asistente o hello ClickOnce cuadro de diálogo emergente. | No. Se aplica solo cuando se copian datos desde un servidor SFTP local. |

#### <a name="example-using-basic-authentication"></a>Ejemplo: Uso de la autenticación básica

establecer la autenticación básica toouse, `authenticationType` como `Basic`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- | --- |
| nombre de usuario | Usuario que tiene el servidor de acceso toohello SFTP. |Sí |
| Contraseña | Contraseña de usuario de hello (nombre de usuario). | Sí |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Ejemplo: Autenticación básica con credenciales cifradas**

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>Uso de autenticación de clave pública SSH:**

establecer la autenticación básica toouse, `authenticationType` como `SshPublicKey`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- | --- |
| nombre de usuario |Usuario que tiene el servidor de acceso toohello SFTP |Sí |
| privateKeyPath | Especifique la ruta de acceso absoluta toohello archivo de clave privada que puede tener acceso esa puerta de enlace. | Especifique cualquier hello `privateKeyPath` o `privateKeyContent`. <br><br> Se aplica solo cuando se copian datos desde un servidor SFTP local. |
| privateKeyContent | Una cadena serializada de contenido de clave privada de Hola. Hola Asistente para copiar puede leer el archivo de clave privada de Hola y extraer contenido de clave privada de hello automáticamente. Si está utilizando cualquier otra herramienta/SDK, use en su lugar la propiedad privateKeyPath de Hola. | Especifique cualquier hello `privateKeyPath` o `privateKeyContent`. |
| passPhrase | Especificar clave privada de hello paso contraseña/frase toodecrypt Hola si el archivo de clave de hello está protegido por una frase de contraseña. | Sí, si el archivo de clave privada de hello está protegido por una frase de contraseña. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Ejemplo: Autenticación de SshPublicKey mediante contenido de clave privada**

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos SFTP, conjunto hello **tipo** del conjunto de datos de hello demasiado**FileShare**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Carpeta de toohello de ruta de acceso de Sub. Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .<br/><br/>Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin. |Sí |
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: <br/><br/>Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.<br/><br/>Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).<br/><br/>Ejemplos 1: `"fileFilter": "*.log"`<br/>Ejemplo 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter es aplicable a un conjunto de datos FileShare de entrada. Esta propiedad no es compatible con HDFS. |No |
| partitionedBy |partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales. Por ejemplo, folderPath se parametriza por cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Especifica si se usará el modo de transferencia binario. Su valor es true para el modo binario y false para ASCII. Valor predeterminado: true. Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer. |No |

> [!NOTE]
> filename y fileFilter no pueden usarse simultáneamente.

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Origen de Sistema de archivos en la actividad de copia
Si va a copiar datos desde un origen SFTP, establezca hello **tipo de origen de** de hello actividad de copia demasiado**FileSystemSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola. |True, False (predeterminada) |No |



#### <a name="example"></a>Ejemplo

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de SFTP](data-factory-sftp-connector.md#copy-activity-properties).


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Servicio vinculado
el servicio conjunto Hola vinculado de toodefine un HTTP **tipo** de hello servicio vinculado demasiado**Http**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| url | Basar la dirección URL toohello servidor Web | Sí |
| authenticationType | Especifica el tipo de autenticación de Hola. Los valores permitidos son: **Anonymous**, **Basic**, **Digest**, **Windows** y **ClientCertificate**. <br><br> Consulte toosections por debajo de esta tabla en más propiedades y ejemplos JSON para esos tipos de autenticación, respectivamente. | Sí |
| enableServerCertificateValidation | Especifique si el servidor de tooenable SSL la validación de certificados si el origen es el servidor de Web HTTPS | No, el valor predeterminado es True. |
| gatewayName | Nombre de hello Data Management Gateway tooconnect tooan local de origen HTTP. | Sí si va a copiar datos desde un origen HTTP local. |
| encryptedCredential | Credenciales cifradas tooaccess Hola extremo HTTP. Generado automáticamente al configurar la información de autenticación de hello en copia asistente o hello ClickOnce cuadro de diálogo emergente. | No. Se aplica solo cuando se copian datos desde un servidor HTTP local. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Ejemplo: Uso de la autenticación Basic, Digest o Windows
Establecer `authenticationType` como `Basic`, `Digest`, o `Windows`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| nombre de usuario | Nombre de usuario tooaccess Hola extremo HTTP. | Sí |
| Contraseña | Contraseña de usuario de hello (nombre de usuario). | Sí |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Ejemplo: Uso de la autenticación ClientCertificate

establecer la autenticación básica toouse, `authenticationType` como `ClientCertificate`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| embeddedCertData | contenido codificado en Base64 Hola de datos binarios del archivo de intercambio de información Personal (PFX) Hola. | Especifique cualquier hello `embeddedCertData` o `certThumbprint`. |
| certThumbprint | Hola huella digital del certificado de Hola que se instaló en el almacén de certificados de la máquina de la puerta de enlace. Se aplica solo cuando se copian datos desde un origen HTTP local. | Especifique cualquier hello `embeddedCertData` o `certThumbprint`. |
| Contraseña | Contraseña asociada con el certificado de Hola. | No |

Si usa `certThumbprint` para hello y autenticación de certificado está instalado en el almacén personal de hello del equipo local de hello, necesita que el servicio de puerta de enlace de toohello de toogrant Hola permiso de lectura:

1. Inicie Microsoft Management Console (MMC). Agregar hello **certificados** complemento ese Hola destinos **equipo Local**.
2. Expanda **Certificados**, **Personal** y haga clic en **Certificados**.
3. Haga clic en certificado Hola almacén personal de Hola y seleccione **todas las tareas**->**administrar claves privadas...**
3. En hello **seguridad** ficha, agregue la cuenta de usuario de hello en que se ejecuta el servicio de Host de Data Management Gateway con certificado de toohello de acceso de lectura de Hola.  

**Ejemplo: usar el certificado de cliente:** esto vinculado vínculos de servicio el servidor de web HTTP de datos generador tooan local. Utiliza un certificado de cliente que se instala en la máquina de hello con Data Management Gateway instalado.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Ejemplo: Uso del certificado de cliente en un archivo
Esto vincula vínculos de servicio el servidor de web HTTP de datos generador tooan local. Utiliza un archivo de certificado de cliente en la máquina de hello con Data Management Gateway instalado.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
conjunto de datos de toodefine un HTTP, conjunto hello **tipo** del conjunto de datos de hello demasiado**Http**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| relativeUrl | Un recurso de toohello de dirección URL relativo al que contiene los datos de Hola. Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola. <br><br> dirección URL dinámica tooconstruct, puede usar [funciones de factoría de datos y las variables del sistema](data-factory-functions-variables.md), ejemplo: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | No |
| requestMethod | Método HTTP. Los valores permitidos son **GET** o **POST**. | No. El valor predeterminado es `GET`. |
| additionalHeaders | Encabezados de solicitud HTTP adicionales. | No |
| requestBody | Cuerpo de la solicitud HTTP. | No |
| formato | Si desea que toosimply **recuperar datos de Hola de extremo HTTP como-es** sin analizarlo, omita esta configuración de formato. <br><br> Si desea tooparse Hola HTTP respuesta contenido durante la copia, se admite los siguientes tipos de formato de Hola: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

#### <a name="example-using-hello-get-default-method"></a>Ejemplo: usar el método de hello GET (valor predeterminado)

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Ejemplo: utilizar el método POST de Hola

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#dataset-properties).

### <a name="http-source-in-copy-activity"></a>Origen de HTTP en la actividad de copia
Si va a copiar datos desde un origen HTTP, establezca hello **tipo de origen de** de hello actividad de copia demasiado**HttpSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| httpRequestTimeout | Hola (TimeSpan) de tiempo de espera de solicitud tooget una respuesta de hello HTTP. Es tooget Hola de tiempo de espera una respuesta, datos de respuesta no Hola el tooread del tiempo de espera. | No. Valor predeterminado: 00:01:40 |


#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de HTTP](data-factory-http-connector.md#copy-activity-properties).

## <a name="odata"></a>OData

### <a name="linked-service"></a>Servicio vinculado
toodefine una OData el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OData**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| url |Dirección URL del servicio OData Hola. |Sí |
| authenticationType |Tipo de autenticación usa tooconnect toohello OData origen. <br/><br/> Para OData en la nube, los valores posibles son Anonymous, Basic y OAuth (tenga en cuenta que Azure Data Factory en estos momentos solo admite la autenticación OAuth basada en Azure Active Directory). <br/><br/> Para OData local, los valores posibles son: Anonymous, Basic y Windows. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación básica. |Sí (solo si usa la autenticación básica) |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |Sí (solo si usa la autenticación básica) |
| authorizedCredential |Si usa OAuth, haga clic en **Authorize** botón en hello Asistente para copiar de factoría de datos o el Editor y escriba sus credenciales, valor de Hola de esta propiedad será generado automáticamente. |Sí (solo si usa la autenticación OAuth) |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el servicio de OData de tooconnect toohello local. Especifique solo si va a copiar datos del origen de OData local. |No |

#### <a name="example---using-basic-authentication"></a>Ejemplo: Uso de la autenticación básica
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Ejemplo: Uso de autenticación anónima

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Ejemplo: Uso de la autenticación de Windows para acceder al origen de OData local

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Ejemplo: Uso de la autenticación OAuth para tener acceso al origen de OData en la nube
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#linked-service-properties).

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos OData, conjunto hello **tipo** del conjunto de datos de hello demasiado**ODataResource**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| path |Ruta de acceso toohello recurso de OData |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos desde un origen OData, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Ejemplo | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |"?$select=Name, Description&$top=5" |No |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Para más información, consulte el artículo [Conector de OData](data-factory-odata-connector.md#copy-activity-properties).


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Servicio vinculado
toodefine un ODBC el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**OnPremisesOdbc**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| connectionString |parte de credencial de acceso no Hola de cadena de conexión de Hola y opcional cifra credenciales. Vea los ejemplos de hello las secciones siguientes. |Sí |
| credential |Hola credencial parte de acceso a cadena de conexión de hello especificada en formato de valores de propiedad específicos del controlador. Ejemplo: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”. |No |
| authenticationType |Tipo de autenticación que utiliza el almacén de datos ODBC tooconnect toohello. Los valores posibles son: Anonymous y Basic. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación básica. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el almacén de datos ODBC tooconnect toohello. |Sí |

#### <a name="example---using-basic-authentication"></a>Ejemplo: Uso de la autenticación básica

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Ejemplo: Uso de la autenticación básica con credenciales cifradas
Puede cifrar las credenciales de hello con hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versión de PowerShell de Azure) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versión o una anterior de hello Azure PowerShell).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Ejemplo: Uso de autenticación anónima

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos ODBC, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en el almacén de datos ODBC Hola. |Sí |


#### <a name="example"></a>Ejemplo

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos desde un almacén de datos ODBC, establecer hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: `select * from MyTable`. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Para más información, consulte el artículo [Conector de ODBC](data-factory-odbc-connector.md#copy-activity-properties).

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>Servicio vinculado
toodefine un Salesforce el servicio conjunto Hola vinculado **tipo** de hello servicio vinculado demasiado**Salesforce**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| environmentUrl | Especifique la instancia de la dirección URL de Salesforce de Hola. <br><br> - La dirección predeterminada es "https://login.salesforce.com". <br> -toocopy datos de espacio aislado, especifique "https://test.salesforce.com". <br> -toocopy datos de dominio personalizado, especifique, por ejemplo, "https://[domain].my.salesforce.com". |No |
| nombre de usuario |Especifique un nombre de usuario de cuenta de usuario de Hola. |Sí |
| Contraseña |Especifique una contraseña para la cuenta de usuario de Hola. |Sí |
| securityToken |Especifique un token de seguridad para la cuenta de usuario de Hola. Vea [obtener token de seguridad](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obtener instrucciones sobre cómo tooreset/obtener un token de seguridad. en general, vea toolearn acerca de los tokens de seguridad [API hello y seguridad](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos de Salesforce, conjunto hello **tipo** del conjunto de datos de hello demasiado**RelationalTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en Salesforce. |No (si se especifica una **consulta** de **RelationalSource**) |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origen relacional en la actividad de copia
Si va a copiar datos de Salesforce, establezca hello **tipo de origen de** de hello actividad de copia demasiado**RelationalSource**y especificar después de propiedades en hello **origen** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Consulta de SQL-92 o de [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Por ejemplo: `select * from MyTable__c`. |No (si hello **tableName** de hello **conjunto de datos** se especifica) |

#### <a name="example"></a>Ejemplo  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
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
        }]
    }
}
```

> [!IMPORTANT]
> parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.

Para más información, consulte el artículo [Conector de Salesforce](data-factory-salesforce-connector.md#copy-activity-properties). 

## <a name="web-data"></a>Datos web 

### <a name="linked-service"></a>Servicio vinculado
el servicio conjunto Hola vinculado de toodefine un sitio Web **tipo** de hello servicio vinculado demasiado**Web**y especificar después de propiedades en hello **typeProperties** sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| URL |Origen de dirección URL toohello Web |Sí |
| authenticationType |Anonymous. |Sí |
 

#### <a name="example"></a>Ejemplo


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Dataset
toodefine un conjunto de datos Web, conjunto hello **tipo** del conjunto de datos de hello demasiado**WebTable**y especifique Hola propiedades Hola siguientes **typeProperties** sección: 

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type |Tipo de conjunto de datos de Hola. debe establecerse demasiado**WebTable** |Sí |
| path |Un recurso de toohello de dirección URL relativo al que contiene la tabla de Hola. |No. Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola. |
| index |índice de Hola de tabla de hello en recursos de Hola. Vea [Get índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) sección índice toogetting de pasos de una tabla en una página HTML. |Sí |

#### <a name="example"></a>Ejemplo

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#dataset-properties). 

### <a name="web-source-in-copy-activity"></a>Origen de Web en la actividad de copia
Si va a copiar datos de una tabla de web, establezca hello **tipo de origen de** de hello actividad de copia demasiado**WebSource**. Actualmente, al origen de hello en la actividad de copia es de tipo **WebSource**, no se admiten propiedades adicionales.

#### <a name="example"></a>Ejemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
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
        }]
    }
}
```

Para más información, consulte el artículo [Conector de Tabla web](data-factory-web-table-connector.md#copy-activity-properties). 

## <a name="compute-environments"></a>ENTORNOS DE PROCESO
Hello tabla siguiente enumeran los entornos de proceso Hola compatibles con actividades de transformación de hello y factoría de datos que se pueden ejecutar en ellos. Haga clic en el vínculo de hello para el proceso de hello está interesado en esquemas JSON de hello toosee para toolink de servicio vinculado tooa factoría de datos. 

| Entorno de procesos | Actividades |
| --- | --- |
| [Clúster de HDInsight a petición](#on-demand-azure-hdinsight-cluster) o [clúster HDInsight propio](#existing-azure-hdinsight-cluster) |[Actividad personalizada de .NET](#net-custom-activity), [actividad de Hive](#hdinsight-hive-activity), [actividad de Pig](#hdinsight-pig-activity, [actividad de MapReduce](#hdinsight-mapreduce-activity), [actividad de streaming de Hadoop](#hdinsight-streaming-activityd) y [actividad de Spark](#hdinsight-spark-activity) |
| [Azure Batch](#azure-batch) |[Actividad personalizada de .NET](#net-custom-activity) |
| [Azure Machine Learning](#azure-machine-learning) | [Actividad de ejecución de lotes de Machine Learning](#machine-learning-batch-execution-activity) y [actividad de recursos de actualización de Machine Learning](#machine-learning-update-resource-activity) |
| [Análisis con Azure Data Lake](#azure-data-lake-analytics) |[U-SQL de análisis con Data Lake](#data-lake-analytics-u-sql-activity) |
| [Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1) y [SQL Server](#sql-server-1) |[Procedimiento almacenado](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>Clúster de Azure HDInsight a petición
Hola servicio Data Factory de Azure puede crear automáticamente un basadas en Windows/Linux a petición HDInsight tooprocess datos del clúster. clúster Hola se crea en la misma región que la cuenta de almacenamiento de hello (propiedad linkedServiceName en hello JSON) asociada a clúster Hola de Hola. Puede ejecutar Hola seguir las actividades de transformación de este servicio vinculado: [actividad personalizada .NET](#net-custom-activity), [Hive actividad](#hdinsight-hive-activity), [actividad de Pig] (#-pig-actividad de hdinsight, [actividad MapReduce ](#hdinsight-mapreduce-activity), [Hadoop streaming actividad](#hdinsight-streaming-activityd), [inspirará actividad](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Servicio vinculado 
Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio de vinculado de HDInsight a petición.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |se debe establecer propiedad de tipo Hello demasiado**HDInsightOnDemand**. |Sí |
| clusterSize |Número de nodos de trabajador/datos en clúster de Hola. clúster de HDInsight de Hola se crea con 2 nodos principales junto con el número de Hola de nodos de trabajador que especifique para esta propiedad. nodos de Hello son de tamaño Standard_D3 que tiene 4 núcleos, por lo que un clúster de nodo de 4 trabajo tiene 24 núcleos (4\*para nodos de trabajador, además de 2 núcleos, 4 = 16\*4 = 8 núcleos para nodos principales). Vea [Hadoop basado en Linux crear clústeres de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para obtener más información acerca del nivel de hello Standard_D3. |Sí |
| timeToLive |Hola permitido de tiempo de inactividad para el clúster de HDInsight a petición Hola. Especifica cuánto tiempo permanece activo clúster de HDInsight a petición Hola tras la finalización de una actividad que se ejecutan si no hay otros trabajos activos en clúster de Hola.<br/><br/>Por ejemplo, si la ejecución de una actividad tiene 6 minutos y timetolive es establecer too5 minutos, Hola clúster permanece activo durante 5 minutos después de hello 6 minutos de procesamiento de ejecución de la actividad de Hola. Si se ejecuta otra actividad que se ejecute con la ventana de 6 minutos hello, que se procesa por hello mismo clúster.<br/><br/>Creación de un clúster de HDInsight a petición es una operación costosa (podría tardar un poco), por lo que use esta opción como sea necesario tooimprove de rendimiento de una factoría de datos mediante la reutilización de un clúster de HDInsight a petición.<br/><br/>Si establece too0 de valor timetolive, clúster Hola se elimina en cuanto ejecuta actividad hello procesados. En hello otra parte, si establece un valor alto, clúster de hello puede permanecer inactivo innecesariamente resultante en altos costos. Por lo tanto, es importante que establezca el valor adecuado de hello según sus necesidades.<br/><br/>Pueden compartir varias canalizaciones Hola la misma instancia de clúster de HDInsight a petición de hello si el valor de la propiedad timetolive Hola está configurado correctamente |Sí |
| versión |Versión Hola del clúster de HDInsight. Para obtener más información, consulte [Versiones admitidas de HDInsight en Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |No |
| linkedServiceName |Almacenamiento de Azure vinculada toobe servicio utilizado por clúster de petición de Hola para almacenar y procesar datos. <p>Actualmente, no se puede crear un clúster de HDInsight a petición que utiliza un almacén de Azure Data Lake como almacenamiento de Hola. Si desea que los datos del resultado de hello toostore de HDInsight de procesamiento en un almacén de Data Lake de Azure, use una actividad de copia toocopy Hola de datos de almacenamiento de blobs de Azure de hello toohello almacén de Azure Data Lake.</p>  | Sí |
| additionalLinkedServiceNames |Especifica las cuentas de almacenamiento adicional para hello HDInsight el servicio vinculado para que el servicio de factoría de datos de hello puede registrar en su nombre. |No |
| osType |Tipo de sistema operativo. Los valores permitidos son: Windows (predeterminado) y Linux |No |
| hcatalogLinkedServiceName |nombre de Hola de SQL Azure vinculado esa base de datos de HCatalog toohello de punto de servicio. clúster de HDInsight a petición Hola se crea mediante el uso de base de datos de SQL Azure hello como Hola tienda de metadatos. |No |

### <a name="json-example"></a>Ejemplo JSON
Hola después de JSON define un servicio de vinculado de HDInsight a petición basadas en Linux. Hola servicio factoría de datos crea automáticamente un **basados en Linux** clúster de HDInsight al procesar un segmento de datos. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Para más información, vea [Servicios vinculados de procesos](data-factory-compute-linked-services.md). 

## <a name="existing-azure-hdinsight-cluster"></a>Clúster de Azure HDInsight existente
Puede crear su propio clúster de HDInsight de un tooregister de servicio vinculado de HDInsight de Azure con factoría de datos. Puede ejecutar Hola siguiendo las actividades de transformación de datos en este servicio vinculado: [actividad personalizada .NET](#net-custom-activity), [Hive actividad](#hdinsight-hive-activity), [actividad de Pig] (#-pig-actividad de hdinsight, [MapReduce actividad](#hdinsight-mapreduce-activity), [Hadoop streaming actividad](#hdinsight-streaming-activityd), [inspirará actividad](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Servicio vinculado
Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio vinculado de HDInsight de Azure.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |se debe establecer propiedad de tipo Hello demasiado**HDInsight**. |Sí |
| clusterUri |Hola URI Hola del clúster de HDInsight. |Sí |
| nombre de usuario |Especificar nombre de Hola de hello usuario toobe usa clúster de HDInsight de tooconnect tooan existente. |Sí |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola. |Sí |
| linkedServiceName | Nombre del servicio vinculado de almacenamiento de Azure que hace referencia el almacenamiento de blobs de Azure toohello hello usa Hola clúster de HDInsight. <p>Actualmente, no se puede especificar un servicio vinculado de Azure Data Lake Store para esta propiedad. Puede tener acceso a datos en el almacén de Azure Data Lake Hola desde scripts de Pig/Hive si el clúster de HDInsight de hello tiene acceso toohello almacén de Data Lake. </p>  |Sí |

Para conocer las versiones de los clústeres de HDInsight admitidas, consulte [Versiones compatibles con HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Azure Batch
Puede crear un grupo de procesos de máquinas virtuales (VM) de un tooregister de servicio vinculado Azure Batch con una factoría de datos. Puede ejecutar actividades personalizadas .NET con Lote de Azure o HDInsight de Azure. Puede ejecutar una [actividad personalizada de .NET](#net-custom-activity) en este servicio vinculado. 

### <a name="linked-service"></a>Servicio vinculado
Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio vinculado Azure Batch.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |se debe establecer propiedad de tipo Hello demasiado**AzureBatch**. |Sí |
| accountName |Nombre de cuenta de Azure Batch Hola. |Sí |
| accessKey |Clave de acceso de hello cuenta de lote de Azure. |Sí |
| poolName |Nombre del grupo de Hola de máquinas virtuales. |Sí |
| linkedServiceName |Nombre del servicio vinculado de almacenamiento de Azure asociado a este servicio vinculado Azure Batch Hola. Este servicio vinculado se usa para archivos de almacenamiento provisional actividad de hello toorun y almacenar los registros de ejecución de actividad de hello necesarios. |Sí |


#### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Crear un tooregister de servicio vinculado de aprendizaje de automático de Azure de un lote de aprendizaje automático, la puntuación del punto de conexión con una factoría de datos. Se pueden ejecutar dos actividades de transformación de datos en este servicio vinculado: [actividad de ejecución de lotes de Machine Learning](#machine-learning-batch-execution-activity) y [actividad de recursos de actualización de Machine Learning](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Servicio vinculado
Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de hello Azure JSON de un servicio vinculado de aprendizaje de automático de Azure.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Tipo |propiedad de tipo Hello debe establecerse en: **AzureML**. |Sí |
| mlEndpoint |dirección URL de puntuación de lotes de Hola. |Sí |
| apiKey |Hola publica API del modelo de área de trabajo. |Sí |

#### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Análisis con Azure Data Lake
Crear un **análisis de Azure Data Lake** vinculado servicio toolink un generador de datos de Azure de tooan de servicio de análisis de Azure Data Lake proceso antes de usar hello [actividad de Data Lake Analytics U-SQL](data-factory-usql-activity.md) en una canalización .

### <a name="linked-service"></a>Servicio vinculado

Hello en la tabla siguiente proporciona descripciones de propiedades de hello utilizadas en la definición de JSON de Hola de un servicio de análisis de Azure Data Lake vinculado. 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| Tipo |propiedad de tipo Hello debe establecerse en: **AzureDataLakeAnalytics**. |Sí |
| accountName |Nombre de la cuenta de Análisis de Azure Data Lake |Sí |
| dataLakeAnalyticsUri |Identificador URI de Análisis de Azure Data Lake. |No |
| authorization |Código de autorización se recupera automáticamente después de hacer clic **Authorize** botón en hello Editor de generador de datos y el inicio de sesión de completando hello OAuth. |Sí |
| subscriptionId |Identificador de suscripción de Azure |No (si no se especifica, suscripción de Hola se usa la factoría de datos). |
| resourceGroupName |Nombre del grupo de recursos de Azure. |No (si no se especifica, el grupo de recursos de Hola se usa la factoría de datos). |
| sessionId |Id. de sesión de sesión de autorización de OAuth de Hola. Cada id. de sesión es único y solo se puede usar una vez. Cuando usas Hola Editor de generador de datos, este identificador es generado automáticamente. |Sí |


#### <a name="json-example"></a>Ejemplo JSON
Hola de ejemplo siguiente proporciona la definición de JSON para un servicio de análisis de Azure Data Lake vinculado.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Azure SQL Database
Crear un servicio vinculado de SQL Azure y usarlo con hello [actividad de procedimiento almacenado](#stored-procedure-activity) tooinvoke un procedimiento almacenado desde una canalización del generador de datos. 

### <a name="linked-service"></a>Servicio vinculado
toodefine una base de datos de SQL Azure vinculado servicio, conjunto hello **tipo** de hello servicio vinculado demasiado**AzureSqlDatabase**y especificar después de propiedades en hello **typeProperties**sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| connectionString |Especifique la información necesaria la instancia de base de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola. |Sí |

#### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Vea el artículo [Conector SQL de Azure](data-factory-azure-sql-connector.md#linked-service-properties) para más información sobre este servicio vinculado.

## <a name="azure-sql-data-warehouse"></a>Almacenamiento de datos SQL de Azure
Crear un servicio de almacenamiento de datos de SQL Azure vinculado y usarlo con hello [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) tooinvoke un procedimiento almacenado desde una canalización del generador de datos. 

### <a name="linked-service"></a>Servicio vinculado
toodefine un almacenamiento de datos de SQL Azure vinculado servicio, conjunto de hello **tipo** de hello servicio vinculado demasiado**AzureSqlDW**y especificar después de propiedades en hello **typeProperties**sección:  

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| connectionString |Especifique la información necesaria la instancia de almacenamiento de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola. |Sí |

#### <a name="json-example"></a>Ejemplo JSON

```json
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

Para más información, consulte el artículo [Conector de Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

## <a name="sql-server"></a>SQL Server 
Crear un servicio de SQL Server vinculado y usarlo con hello [actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) tooinvoke un procedimiento almacenado desde una canalización del generador de datos. 

### <a name="linked-service"></a>Servicio vinculado
Crear un servicio vinculado de tipo **onpremisessqlserver** toolink una factoría de datos local tooa de base de datos de SQL Server. Hello en la tabla siguiente proporciona la descripción del servicio de SQL Server vinculado de JSON elementos tooon local específico.

Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSQL servicio del servidor vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **onpremisessqlserver**. |Sí |
| connectionString |Especificar información de connectionString necesaria tooconnect toohello en SQL Server base de datos local con autenticación de SQL o autenticación de Windows. |Sí |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de SQL Server de tooconnect toohello local. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación de Windows. Ejemplo: **nombreDeDominio\\nombreDeUsuario**. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |

Puede cifrar las credenciales con hello **New-AzureRmDataFactoryEncryptValue** cmdlet y usarlos en la cadena de conexión de hello tal y como se muestra en el siguiente ejemplo de Hola (**EncryptedCredential** propiedad):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Ejemplo: JSON para usar autenticación de SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Ejemplo: JSON para usar autenticación de Windows

Si se especifiquen el nombre de usuario y contraseña, puerta de enlace usa hello tooimpersonate base de datos de usuario especificado cuenta tooconnect toohello local SQL Server. En caso contrario, la puerta de enlace conecta toohello SQL Server directamente con el contexto de seguridad de Hola de puerta de enlace (su cuenta de inicio).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para más información, consulte el artículo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).

## <a name="data-transformation-activities"></a>ACTIVIDADES DE TRANSFORMACIÓN DE DATOS

Actividad | Descripción
-------- | -----------
[Actividad de Hive de HDInsight](#hdinsight-hive-activity) | Hola actividad de HDInsight Hive en una canalización de factoría de datos ejecuta consultas de Hive por su cuenta o clúster de HDInsight basados en Windows/Linux a petición. 
[Actividad de Pig de HDInsight](#hdinsight-pig-activity) | Hola actividad de HDInsight Pig en una canalización de factoría de datos ejecuta consultas de Pig por su cuenta o clúster de HDInsight basados en Windows/Linux a petición.
[Actividad de MapReduce de HDInsight](#hdinsight-mapreduce-activity) | Hola actividad de HDInsight MapReduce en una canalización de factoría de datos ejecuta programas de MapReduce por su cuenta o clúster de HDInsight basados en Windows/Linux a petición.
[Actividad de streaming de HDInsight](#hdinsight-streaming-activity) | Hola actividad de transmisión por secuencias de HDInsight en una canalización de factoría de datos ejecuta programas de Streaming de Hadoop por su cuenta o clúster de HDInsight basados en Windows/Linux a petición.
[Actividad de HDInsight Spark](#hdinsight-spark-activity) | Hola actividad de HDInsight Spark en una canalización de factoría de datos ejecuta programas de Spark en su propio clúster de HDInsight. 
[Actividad de ejecución de Batch de Machine Learning](#machine-learning-batch-execution-activity) | Azure factoría de datos permite tooeasily crear canalizaciones que usan un aprendizaje automático de Azure publicada web service para realizar análisis predictivos. Hola la actividad de ejecución por lotes en una canalización de factoría de datos de Azure se pueden invocar un predicciones de toomake de servicio de web de aprendizaje automático en los datos de hello en lote. 
[Actividad Actualizar recurso de Machine Learning](#machine-learning-update-resource-activity) | Con el tiempo, los modelos de predicción de Hola Hola aprendizaje automático de experimentos puntuación necesitan toobe volver a entrenar con nueva entrada de conjuntos de datos. Cuando termine con reciclaje, desea hello tooupdate la puntuación del servicio web con hello volver a entrenar el modelo de aprendizaje automático. Puede usar servicio web de actualización de recursos de actividad tooupdate Hola Hola con hello recién entrenado modelo.
[Actividad de procedimiento almacenado](#stored-procedure-activity) | Puede usar la actividad de procedimiento almacenado de hello en un tooinvoke de canalización de factoría de datos en un procedimiento almacenado en uno de hello siguientes almacenes de datos: SQL de Azure, almacenamiento de datos de SQL Azure, base de datos de SQL Server en su empresa o una máquina virtual de Azure. 
[Actividad U-SQL de Data Lake Analytics](#data-lake-analytics-u-sql-activity) | La actividad de U-SQL de Data Lake Analytics ejecuta un script de U-SQL en un clúster de Azure Data Lake Analytics.  
[Actividad personalizada de .NET](#net-custom-activity) | Si necesita datos de tootransform de forma que no es compatible con la factoría de datos, puede crear una actividad personalizada con su propia lógica de procesamiento de datos y usar actividad hello en canalización Hola. Puede configurar Hola personalizada .NET actividad toorun mediante un servicio Azure Batch o un clúster de HDInsight de Azure. 

     
## <a name="hdinsight-hive-activity"></a>Actividad de Hive de HDInsight
Puede especificar Hola propiedades en una definición de JSON de actividad de Hive siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightHive**. Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightHive de actividad:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| script |Especifique el script de Hive de hello en línea |No |
| ruta de acceso de script |Hola de almacén en el almacenamiento de blobs de Azure de script de Hive y proporcionar Hola ruta toohello al archivo. Use la propiedad 'script' o 'scriptPath'. No se pueden usar las dos juntas. nombre de archivo de Hello distingue mayúsculas de minúsculas. |No |
| define los campos |Especificar parámetros como pares clave/valor para hacer referencia a dentro de script de Hive hello mediante 'hiveconf' |No |

Estas propiedades de tipo son toohello específico de actividad de Hive. Otras propiedades (fuera de la sección de hello typeProperties) son compatibles con todas las actividades.   

### <a name="json-example"></a>Ejemplo JSON
Hola después JSON define una actividad de Hive de HDInsight en una canalización.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

Para más información, consulte el artículo [Actividad de Hive](data-factory-hive-activity.md). 

## <a name="hdinsight-pig-activity"></a>Actividad de Pig de HDInsight
Puede especificar Hola propiedades en una definición de JSON de la actividad de Pig siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightPig**. Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightPig de actividad: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| script |Especifique el script de Pig de hello en línea |No |
| ruta de acceso de script |Almacenar el script de Pig hello en el almacenamiento de blobs de Azure y proporcionar Hola ruta toohello al archivo. Use la propiedad 'script' o 'scriptPath'. No se pueden usar las dos juntas. nombre de archivo de Hello distingue mayúsculas de minúsculas. |No |
| define los campos |Especificar parámetros como pares clave/valor para hacer referencia a dentro de hello script de Pig |No |

Estas propiedades de tipo son toohello específico de actividad de Pig. Otras propiedades (fuera de la sección de hello typeProperties) son compatibles con todas las actividades.   

### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

Para más información, consulte el artículo [Actividad de Pig](#data-factory-pig-activity.md). 

## <a name="hdinsight-mapreduce-activity"></a>Actividad de MapReduce de HDInsight
Puede especificar Hola propiedades en una definición de JSON de actividad MapReduce siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightMapReduce**. Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightMapReduce de actividad: 

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| jarLinkedService | Nombre del programa Hola a servicio de almacenamiento de Azure que contiene el archivo JAR de Hola Hola vinculado. | Sí |
| jarFilePath | Ruta de acceso toohello JAR el archivo en hello almacenamiento de Azure. | Sí | 
| className | Nombre de clase principal de hello en el archivo JAR de Hola. | Sí | 
| argumentos | Una lista de argumentos separados por comas para el programa de MapReduce Hola. En tiempo de ejecución, verá que algunos argumentos adicionales (por ejemplo: mapreduce.job.tags) de marco de trabajo de MapReduce Hola. toodifferentiate los argumentos con argumentos de MapReduce hello, considere el uso de opción y valor como argumentos tal como se muestra en el siguiente ejemplo de Hola (- s,--entrada,--salida etc., son opciones seguidos inmediatamente por sus valores) | No | 

### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Para más información, consulte el artículo [Actividad de MapReduce](data-factory-map-reduce.md). 

## <a name="hdinsight-streaming-activity"></a>Actividad de streaming de HDInsight
Puede especificar Hola propiedades en una definición de JSON de actividad de Streaming de Hadoop siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightStreaming**. Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightStreaming de actividad: 

| Propiedad | Descripción | 
| --- | --- |
| mapper | Nombre del ejecutable de asignador de Hola. En el ejemplo de Hola, cat.exe es el asignador de hello ejecutable.| 
| reducer | Nombre del reductor Hola ejecutable. En el ejemplo de Hola, wc.exe es reductor Hola ejecutable. | 
| input | Archivo de entrada (incluida la ubicación) para el asignador de Hola. En el ejemplo de Hola: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample es el contenedor de blob de hello, ejemplo/data/Gutenberg es la carpeta de Hola y davinci.txt es blob Hola. |
| output | Archivo de salida (incluida la ubicación) para el reductor Hola. salida de Hello de trabajo de Streaming de Hadoop de Hola se escribe ubicación toohello especificado para esta propiedad. |
| filePaths | Rutas de acceso para los ejecutables de asignador y reductor Hola. En el ejemplo de Hola: "adfsample/example/apps/wc.exe", adfsample es el contenedor de blob de hello, example/apps es la carpeta de Hola y wc.exe es ejecutable hello. | 
| fileLinkedService | Servicio vinculado de almacenamiento Azure que representa el almacenamiento de Azure que contiene archivos de hello especificados en la sección de filePaths Hola Hola. | 
| argumentos | Una lista de argumentos separados por comas para el programa de MapReduce Hola. En tiempo de ejecución, verá que algunos argumentos adicionales (por ejemplo: mapreduce.job.tags) de marco de trabajo de MapReduce Hola. toodifferentiate los argumentos con argumentos de MapReduce hello, considere el uso de opción y valor como argumentos tal como se muestra en el siguiente ejemplo de Hola (- s,--entrada,--salida etc., son opciones seguidos inmediatamente por sus valores) | 
| getDebugInfo | Un elemento opcional. Cuando se establece tooFailure, registros de Hola se descargan solo en caso de error. Cuando se establece tooAll, registros siempre se descargan independientemente del estado de ejecución de Hola. | 

> [!NOTE]
> Debe especificar un conjunto de datos de salida de hello Hadoop Streaming Activity para hello **genera** propiedad. Este conjunto de datos puede ser simplemente un dataset ficticio que es necesario toodrive Hola canalización programación (etcetera diariamente, cada hora,.). Si la actividad hello no toma una entrada, puede omitir especifica un conjunto de datos de entrada de la actividad de Hola de hello **entradas** propiedad.  

## <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Para más información, consulte el artículo [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md). 

## <a name="hdinsight-spark-activity"></a>Actividad de HDInsight Spark
Puede especificar Hola propiedades en una definición de JSON de la actividad de Spark siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **HDInsightSpark**. Debe crear primero un servicio vinculado de HDInsight y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooHDInsightSpark de actividad: 

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| rootPath | contenedor de blobs de Azure de Hola y la carpeta que contiene el archivo de hello Spark. nombre de archivo de Hello distingue mayúsculas de minúsculas. | Sí |
| entryFilePath | Carpeta de raíz de toohello de ruta de acceso relativa del programa Hola Spark/paquete de código. | Sí |
| className | Clase principal de Spark o Java de la aplicación. | No | 
| argumentos | Una lista de programas de Spark de toohello argumentos de línea de comandos. | No | 
| proxyUser | programa de Spark hello tooexecute de tooimpersonate de la cuenta de usuario de Hola | No | 
| sparkConfig | Propiedades de configuración de Spark. | No | 
| getDebugInfo | Especifica cuando los archivos de registro de hello Spark son copiado toohello utilizado por el clúster de HDInsight de almacenamiento de Azure (o) especificado por sparkJobLinkedService. Valores permitidos: Ninguno, Siempre o Error. Valor predeterminado: Ninguno. | No | 
| sparkJobLinkedService | Hola servicio vinculado de almacenamiento de Azure que contiene registros, las dependencias y archivo de trabajo de hello Spark.  Si no especifica un valor para esta propiedad, se usa almacenamiento de hello asociado con el clúster de HDInsight. | No |

### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Tenga en cuenta Hola siguientes puntos: 

- Hola **tipo** propiedad se establece demasiado**HDInsightSpark**.
- Hola **Ruta_raíz** se establece demasiado**adfspark\\pyFiles** donde adfspark es contenedor de blobs de Azure de Hola y pyFiles es la carpeta correctamente en ese contenedor. En este ejemplo, hello almacenamiento de blobs de Azure es hello uno que esté asociado con el clúster de Spark Hola. Puede cargar Hola archivo tooa almacenamiento de Azure diferente. Si lo hace, cree un toolink de servicio vinculado de almacenamiento de Azure que factoría de datos de toohello de cuenta de almacenamiento. A continuación, especificar nombre de Hola de servicio de hello vinculado como un valor de hello **sparkJobLinkedService** propiedad. Vea [propiedades de la actividad de Spark](#spark-activity-properties) para obtener más información acerca de esta propiedad y otras propiedades compatibles con hello Spark actividad.
- Hola **entryFilePath** se establece toohello **test.py**, que es el archivo de python de hello. 
- Hola **getDebugInfo** propiedad se establece demasiado**siempre**, lo que significa que los archivos de registro de hello siempre están generado (éxito o error).  

    > [!IMPORTANT]
    > Se recomienda que no establezca esta propiedad tooAlways en un entorno de producción a menos que esté solucionando un problema. 
- Hola **genera** sección tiene un conjunto de datos de salida. Debe especificar un conjunto de datos de salida, incluso si el programa de spark hello no genera ningún resultado. Hola salida dataset unidades Hola programación para canalización hello (etcetera diariamente, cada hora,.).

Para obtener más información acerca de la actividad de hello, consulte [Spark actividad](data-factory-spark.md) artículo.  

## <a name="machine-learning-batch-execution-activity"></a>Actividad de ejecución de Batch de Machine Learning
Puede especificar Hola propiedades en una definición de JSON de actividad de ejecución de lote de aprendizaje automático de Azure siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **AzureMLBatchExecution**. Debe crear una máquina de Azure en primer lugar, el servicio vinculado de aprendizaje y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooAzureMLBatchExecution de actividad:

Propiedad | Descripción | Obligatorio 
-------- | ----------- | --------
webServiceInput | Hola toobe de conjunto de datos se pasa como entrada para el servicio web de aprendizaje automático de Azure Hola. Este conjunto de datos también debe incluirse en las entradas de Hola para actividad de Hola. |Use webServiceInput o webServiceInputs. | 
webServiceInputs | Especificar los conjuntos de datos toobe pasadas como entradas para hello servicio web de aprendizaje automático de Azure. Si el servicio web de hello toma varias entradas, utilice la propiedad de webServiceInputs de hello en lugar de utilizar la propiedad de webServiceInput Hola. Conjuntos de datos que se hace referencia mediante hello **webServiceInputs** también debe incluirse en hello actividad **entradas**. | Use webServiceInput o webServiceInputs. | 
webServiceOutputs | Hola conjuntos de datos que se asignan como salidas para el servicio web de aprendizaje automático de Azure de Hola. servicio web de Hello devuelve datos de salida de este conjunto de datos. | Sí | 
globalParameters | Especificar valores para parámetros de servicio web de hello en esta sección. | No | 

### <a name="json-example"></a>Ejemplo JSON
En este ejemplo, actividad hello tiene el conjunto de datos de hello **MLSqlInput** como entrada y **MLSqlOutput** como salida de hello. Hola **MLSqlInput** se pasa como un servicio web de entrada toohello por mediante hello **webServiceInput** propiedad JSON. Hola **MLSqlOutput** se pasa como un servicio de Web de salida toohello por mediante hello **webServiceOutputs** propiedad JSON. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

En el ejemplo de Hola a JSON, Hola implementado Azure Machine Learning servicio Web utiliza un lector y un sistema de escritura módulo tooread/escribir datos de / tooan base de datos de SQL Azure. Este servicio Web expone Hola cuatro parámetros siguientes: nombre del servidor, nombre de base de datos, nombre de cuenta de usuario de servidor y contraseña de cuenta de usuario de servidor de base de datos.

> [!NOTE]
> Solo entradas y salidas de hello AzureMLBatchExecution actividad pueden pasarse como parámetros toohello servicio Web. Por ejemplo, en hello por encima del fragmento de JSON, MLSqlInput es una entrada toohello AzureMLBatchExecution actividad, que se pasa como un servicio Web de entrada toohello a través del parámetro webServiceInput.

## <a name="machine-learning-update-resource-activity"></a>Actividad de recursos de actualización de Machine Learning
Puede especificar Hola propiedades en una definición de JSON de actividad de recursos de actualización de aprendizaje automático de Azure siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **AzureMLUpdateResource**. Debe crear una máquina de Azure en primer lugar, el servicio vinculado de aprendizaje y especificar el nombre hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooAzureMLUpdateResource de actividad:

Propiedad | Descripción | Obligatorio 
-------- | ----------- | --------
trainedModelName | Nombre del programa Hola a volver a entrenar el modelo. | Sí |  
trainedModelDatasetName | Archivo conjunto de datos señalador toohello iLearner devuelto por la operación de reciclaje de Hola. | Sí | 

### <a name="json-example"></a>Ejemplo JSON
canalización de Hello tiene dos actividades: **AzureMLBatchExecution** y **AzureMLUpdateResource**. Hola actividad de ejecución de lotes de aprendizaje automático de Azure toma los datos de entrenamiento de hello como entrada y genera un archivo iLearner como salida. actividad Hello invoca el servicio web de aprendizaje hello (se expone como un servicio web experimento de entrenamiento) con los datos de entrenamiento de entradas de Hola y recibe el archivo ilearner de hello de hello webservice. Hola placeholderBlob es simplemente un conjunto de datos de salida ficticio requerido por la canalización de hello Data Factory de Azure servicio toorun Hola.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Actividad U-SQL de Análisis de Data Lake
Puede especificar Hola propiedades en una definición de JSON de la actividad de U-SQL siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **DataLakeAnalyticsU SQL**. Debe crear un servicio de análisis de Azure Data Lake vinculado y especifique el nombre de hello del mismo como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de actividad tooDataLakeAnalyticsU-SQL: 

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| scriptPath |Toofolder de ruta de acceso que contiene el script de Hola U-SQL. Nombre del archivo hello distingue mayúsculas de minúsculas. |No (si se utiliza el script) |
| scriptLinkedService |Servicio vinculado que se vincula el almacenamiento de Hola que contiene la factoría de datos de hello script toohello |No (si se utiliza el script) |
| script |Especifique el script en línea en lugar de scriptPath y scriptLinkedService. Por ejemplo: "script": "Prueba CREAR BASE DE DATOS". |No (si usa scriptPath y scriptLinkedService) |
| degreeOfParallelism |número máximo de Hola de nodos simultáneamente utiliza trabajo de hello toorun. |No |
| prioridad |Determina qué trabajos de todos los que se ponen en cola deberían estar seleccionado toorun en primer lugar. Hola Hola número inferior, prioridad Hola Hola. |No |
| parameters |Parámetros de script de Hola U-SQL |No |

### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Para más información, consulte [Actividad de U-SQL de Data Lake Analytics](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Actividad de procedimiento almacenado
Puede especificar propiedades en una definición de JSON de actividad de procedimiento almacenado siguientes de Hola. debe ser propiedad de tipo Hello para la actividad de hello: **SqlServerStoredProcedure**. Debe crear un uno de hello después servicios vinculados y especificar el nombre de Hola de servicio de hello vinculado como un valor de hello **linkedServiceName** propiedad:

- SQL Server 
- Base de datos SQL de Azure
- Almacenamiento de datos SQL de Azure

Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooSqlServerStoredProcedure de actividad:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| storedProcedureName |Especifique el nombre de hello del procedimiento de hello almacenado en la base de datos de SQL Azure de Hola o almacenamiento de datos de SQL de Azure que está representado por el servicio de hello vinculado que Hola usos de la tabla de salida. |Sí |
| storedProcedureParameters |Especifique valores para los parámetros del procedimiento almacenado. Si necesitas toopass null para un parámetro, use la sintaxis de hello: "param1": null (todas las minúsculas). Vea Hola después toolearn de ejemplo sobre el uso de esta propiedad. |No |

Si especifica un conjunto de datos de entrada, debe estar disponible (en estado "Listo") para hello almacenado toorun de actividad de procedimiento. conjunto de datos de entrada de Hola no puede ser consumida en el procedimiento de hello almacenado como un parámetro. Es solo usa toocheck Hola dependencia antes de actividad de procedimiento almacenado de saludo inicial. Debe especificar un conjunto de datos para una actividad de procedimiento almacenado. 

Conjunto de datos de salida especifica hello **programación** para hello almacenados actividad de procedimiento (cada hora, semanalmente, mensualmente, etcetera). Hello conjunto de datos de salida debe usar un **servicio vinculado** que hace referencia tooan base de datos de SQL Azure o un almacén de datos de SQL Azure o una base de datos de SQL Server en el que desea Hola toorun de procedimiento almacenado. Hello conjunto de datos de salida puede actuar como un resultado de hello de manera toopass del procedimiento de hello almacenan para su posterior procesamiento por otra actividad ([encadenamiento actividades](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) en la canalización de Hola. Sin embargo, factoría de datos no escribe automáticamente Hola un resultado de un conjunto de datos de toothis de procedimiento almacenado. Es el procedimiento almacenado Hola esa tabla SQL tooa de escrituras que Hola puntos de conjunto de datos de salida a. En algunos casos, puede ser el conjunto de datos de salida de hello un **conjunto de datos ficticio**, que se usa solo la programación de hello toospecify para ejecutar Hola actividad de procedimiento almacenado.  

### <a name="json-example"></a>Ejemplo JSON

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Para más información, consulte el artículo [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md). 

## <a name="net-custom-activity"></a>Actividad personalizada de .NET
Puede especificar Hola propiedades en una definición de JSON de actividad personalizada .NET siguientes. debe ser propiedad de tipo Hello para la actividad de hello: **DotNetActivity**. Debe crear un servicio vinculado de HDInsight de Azure o un lote de Azure vinculada de servicio y especificar el nombre de Hola de servicio de hello vinculado como un valor de hello **linkedServiceName** propiedad. Hello siguientes se admiten las propiedades en hello **typeProperties** sección cuando se establece el tipo de saludo de tooDotNetActivity de actividad:
 
| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| AssemblyName | Nombre del ensamblado de Hola. En el ejemplo de Hola, es: **MyDotnetActivity.dll**. | Sí |
| EntryPoint |Nombre de clase de Hola que implementa la interfaz de IDotNetActivity Hola. En el ejemplo de Hola, es: **MyDotNetActivityNS.MyDotNetActivity** donde MyDotNetActivityNS es el espacio de nombres de Hola y MyDotNetActivity es clase hello.  | Sí | 
| PackageLinkedService | Nombre del servicio vinculado de almacenamiento de Azure que señala el almacenamiento de blobs de toohello que contiene el archivo zip de actividad personalizada de Hola Hola. En el ejemplo de Hola, es: **AzureStorageLinkedService**.| Sí |
| PackageFile | Nombre del archivo zip de Hola. En el ejemplo de Hola, es: **customactivitycontainer/MyDotNetActivity.zip**. | Sí |
| extendedProperties | Propiedades extendidas que se pueden definir y pasar de código de .NET toohello. En este ejemplo, Hola **SliceStart** variable está establecida el valor de tooa en función de la variable del sistema SliceStart Hola. | No | 

### <a name="json-example"></a>Ejemplo JSON

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Para obtener información detallada, vea el artículo [Uso de actividades personalizadas en Data Factory](data-factory-use-custom-activities.md). 

## <a name="next-steps"></a>Pasos siguientes
Vea Hola tutoriales: 

- [Tutorial: crear una canalización con la actividad de copia](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Tutorial: crear una canalización con la actividad de hive](data-factory-build-your-first-pipeline-using-editor.md)