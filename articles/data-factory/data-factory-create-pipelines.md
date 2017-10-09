---
title: "Canalizaciones de aaaCreate/programación, las actividades de cadena de factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de una canalización de datos en Data Factory de Azure toomove toocreate y transformar datos. Crear una datos controlada por la información de flujo de trabajo tooproduce toouse listo."
keywords: "canalización de datos, flujo de trabajo controlado por datos"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Canalizaciones y actividades en Azure Data Factory
En este artículo le ayuda a comprender las canalizaciones y actividades de Data Factory de Azure y utilizar flujos de trabajo de datos de tooconstruct-to-end para el movimiento de datos y los escenarios de procesamiento de datos.  

> [!NOTE]
> En este artículo se da por supuesto que ha realizado a través de [tooAzure Introducción factoría de datos](data-factory-introduction.md). Si no tiene experiencia práctica con la creación de factorías de datos, repasar los tutoriales sobre [transformación](data-factory-build-your-first-pipeline.md) o [traslado de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) puede ayudarlo a comprender mejor este artículo.  

## <a name="overview"></a>Información general
Una factoría de datos puede tener una o más canalizaciones. Una canalización es una agrupación lógica de actividades que realizan una tarea. actividades de Hello en una canalización definen acciones tooperform en los datos. Por ejemplo, puede utilizar un datos de toocopy de actividad de copia de un tooan de SQL Server local almacenamiento de blobs de Azure. A continuación, utilice una actividad de Hive que se ejecuta un script de Hive en un tooprocess/transformar datos de clúster de HDInsight de Azure de datos de salida de tooproduce de almacenamiento de blob de Hola. Por último, use una segunda copia actividad toocopy Hola salida datos tooan Azure almacenamiento de datos SQL sobre qué inteligencia empresarial (BI) se crean soluciones de informes. 

Una actividad puede tomar diversos [conjuntos de datos](data-factory-create-datasets.md), o ninguno, y generar uno o varios [conjuntos de datos](data-factory-create-datasets.md). Hello siguiente diagrama muestra hello relación entre el conjunto de datos, la actividad y la canalización de factoría de datos: 

![Relación entre la canalización, la actividad y el conjunto de datos](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Una canalización permite toomanage actividades como un conjunto en lugar de cada uno de ellos individualmente. Por ejemplo, puede implementar, programar, suspender y reanudar una canalización, en lugar de trabajar con actividades de canalización de Hola por separado.

Data Factory admite dos tipos de actividades: actividades de movimiento de datos y actividades de transformación de datos. Cada actividad puede tener cero o más [conjuntos de datos](data-factory-create-datasets.md) de entrada y generar uno o más conjuntos de datos de salida.

Un conjunto de datos de entrada representa la entrada de Hola para una actividad de canalización de Hola y un conjunto de datos de salida representa la salida de hello para la actividad de Hola. Los conjuntos de datos identifican datos en distintos almacenes de datos, como tablas, archivos, carpetas y documentos. Después de crear un conjunto de datos, puede usarlo con las actividades de una canalización. Por ejemplo, un conjunto de datos puede ser un conjunto de datos de entrada y salida de una actividad de copia o una actividad de HDInsightHive. Para obtener más información sobre los conjuntos de datos, vea el artículo [Conjuntos de datos en Data Factory de Azure](data-factory-create-datasets.md).

### <a name="data-movement-activities"></a>Actividades de movimiento de datos
Actividad de copia de factoría de datos copia datos de un almacén de datos de origen datos almacén tooa receptor. Factoría de datos admite Hola siguientes almacenes de datos. Se pueden escribir datos de cualquier origen tooany receptor. Haga clic en un toolearn de almacén de datos cómo toocopy tooand de datos de ese almacén.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Almacenes de datos con * puede ser local o en IaaS de Azure y requieren tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) en una máquina de IaaS en local o de Azure.

Para más información, consulte el artículo sobre [actividades de movimiento de datos](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Actividades de transformación de datos
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Para más información, consulte el artículo sobre [actividades de transformación de datos](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Actividades personalizadas de .NET 
Si necesita datos toomove/de datos de un almacén que Hola actividad de copia no admite, o transformar datos mediante su propia lógica, cree un **actividad personalizada de .NET**. Consulte el artículo [Uso de actividades personalizadas en una canalización de Data Factory de Azure](data-factory-use-custom-activities.md)para obtener más información sobre la creación y el uso de una actividad personalizada.

## <a name="schedule-pipelines"></a>Programar canalizaciones
Una canalización solo está activa entre su hora de **inicio** y de **finalización**. No se ejecuta antes de la hora de inicio de Hola o después de la hora de finalización de Hola. Si se pausa la canalización de hello, no se ejecutan independientemente de su hora de inicio y finalización. Para una toorun de canalización, se debe no se produce la pausa. Vea [ejecución y programación](data-factory-scheduling-and-execution.md) toounderstand cómo funciona la programación y la ejecución de factoría de datos de Azure.

## <a name="pipeline-json"></a>JSON de canalización
Vamos a fijarnos un poco más en cómo se define una canalización en formato JSON. estructura genérica de Hola para una canalización tiene el siguiente aspecto:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Etiqueta | Description | Obligatorio |
| --- | --- | --- |
| name |Nombre de la canalización de Hola. Especifique un nombre que representa la acción de Hola que Hola canalización lleva a cabo. <br/><ul><li>Número máximo de caracteres: 260</li><li>Debe empezar en una letra, un número o un carácter de subrayado (_)</li><li>No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sí |
| description | Especificar el texto hello que describe qué canalización Hola se usa para. |Sí |
| actividades | Hola **actividades** sección puede tener una o varias actividades definidas en él. Vea la siguiente sección de Hola para obtener más información acerca de los elementos JSON de las actividades de Hola. | Sí |  
| start | Fecha y hora de inicio de la canalización de Hola. Debe estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: `2016-10-14T16:32:41Z`. <br/><br/>Es posible toospecify una hora local, por ejemplo una hora EST. Aquí tiene un ejemplo: `2016-02-27T06:00:00-05:00`, que es 06:00 EST.<br/><br/>Hello propiedades start y end juntos especifican el período activo de la canalización de Hola. Los segmentos de salida solo se producen en este período activo. |No<br/><br/>Si especifica un valor para la propiedad de finalización de hello, debe especificar el valor de propiedad de inicio de Hola.<br/><br/>Hello horas de inicio y finalización tanto pueden ser toocreate vacía una canalización. Debe especificar ambos valores tooset un período activo de hello canalización toorun. Si no especifica horas de inicio y finalización al crear una canalización, puede establecerlas mediante cmdlet Hola conjunto AzureRmDataFactoryPipelineActivePeriod más tarde. |
| end | Fecha y hora de final de la canalización de Hola. Si se especifica, debe estar en formato ISO. Por ejemplo: `2016-10-14T17:32:41Z` <br/><br/>Es posible toospecify una hora local, por ejemplo una hora EST. Aquí tiene un ejemplo: `2016-02-27T06:00:00-05:00`, que es 6 a. m. EST.<br/><br/>canalización de hello toorun indefinidamente, especifique 9999-09-09 como valor de hello para la propiedad de finalización de Hola. <br/><br/> Una canalización solo está activa entre su hora de inicio y de finalización. No se ejecuta antes de la hora de inicio de Hola o después de la hora de finalización de Hola. Si se pausa la canalización de hello, no se ejecutan independientemente de su hora de inicio y finalización. Para una toorun de canalización, se debe no se produce la pausa. Vea [ejecución y programación](data-factory-scheduling-and-execution.md) toounderstand cómo funciona la programación y la ejecución de factoría de datos de Azure. |No <br/><br/>Si especifica un valor para la propiedad de inicio de hello, debe especificar el valor de propiedad de finalización de Hola.<br/><br/>Vea las notas de hello **iniciar** propiedad. |
| isPaused | Si no se ejecuta set tootrue, canalización Hola. Ha de hello estado de pausa. Valor predeterminado = false. Puede usar esta propiedad tooenable o deshabilitar una canalización. |No |
| pipelineMode | método Hello para la programación se ejecuta para la canalización de Hola. Los valores permitidos son: scheduled (predeterminado).<br/><br/>'Programada' indica que esa canalización Hola se ejecuta en un intervalo de tiempo especificado según el período activo de tooits (hora de inicio y final). 'Tendrá que repetir' indica que esa canalización Hola se ejecuta solo una vez. Las canalizaciones creadas una sola vez no se pueden modificar ni actualizar actualmente. Consulte la sección [Canalización de una vez](#onetime-pipeline) para más información acerca de la configuración onetime. |No |
| expirationTime | Duración de tiempo después de la creación de qué hello [única canalización](#onetime-pipeline) es válida y debe permanecer aprovisionado. Si no tiene ningún activo, error, o pendientes se ejecuta, la canalización de hello es automáticamente una vez eliminado alcanza hora de expiración de Hola. valor predeterminado de Hello:`"expirationTime": "3.00:00:00"`|No |
| conjuntos de datos |Lista de toobe de conjuntos de datos utilizado por actividades definidas en la canalización de Hola. Esta propiedad puede ser conjuntos de datos usado toodefine canalización toothis específico y no definidos dentro de la factoría de datos de Hola. Los conjuntos de datos definidos dentro de esta canalización solo pueden utilizarse en ella y no se pueden compartir. Consulte la sección [Conjuntos de datos limitados](data-factory-create-datasets.md#scoped-datasets) para más información. |No |

## <a name="activity-json"></a>Actividad de JSON
Hola **actividades** sección puede tener una o varias actividades definidas en él. Cada actividad tiene Hola siguiendo la estructura de nivel superior:

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
    },
    "scheduler":
    {
    }
}
```

Tabla siguiente describe las propiedades de actividad de hello definición JSON:

| Etiqueta | Description | Obligatorio |
| --- | --- | --- |
| name | Nombre de actividad de Hola. Especifique un nombre que representa la acción de Hola que realiza la actividad hello. <br/><ul><li>Número máximo de caracteres: 260</li><li>Debe empezar en una letra, un número o un carácter de subrayado (_)</li><li>No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sí |
| description | Texto que describe qué Hola actividad o se usa para |Sí |
| type | Tipo de actividad de Hola. Vea hello [las actividades de movimiento de datos](#data-movement-activities) y [las actividades de transformación de datos](#data-transformation-activities) secciones para diferentes tipos de actividades. |Sí |
| inputs |Tablas de entrada utilizadas por actividad hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Sí |
| outputs |Tablas de salida utilizadas por actividad hello.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Sí |
| linkedServiceName |Nombre del servicio de hello vinculado utilizado por actividad hello. <br/><br/>Una actividad puede requerir que especifique servicio Hola vinculado que se vincula el entorno de proceso necesarios toohello. |Sí para actividad de HDInsight y actividad de puntuación por lotes de Machine Learning de Azure <br/><br/>No para todos los demás |
| typeProperties |Propiedades de hello **typeProperties** sección dependen del tipo de actividad de Hola. propiedades de tipos de toosee de una actividad, haga clic en la actividad de toohello de vínculos en la sección anterior de Hola. | No |
| policy |Directivas que afectan al comportamiento de tiempo de ejecución de Hola de actividad hello. Si no se especifica, se usan las directivas predeterminadas. |No |
| scheduler | propiedad "programador" es usado toodefine deseado de programación para la actividad de Hola. Sus subpropiedades se Hola igual que los de Hola Hola [propiedad de disponibilidad en un conjunto de datos](data-factory-create-datasets.md#dataset-availability). |No |


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

## <a name="sample-copy-pipeline"></a>Canalización de copia de ejemplo
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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Tenga en cuenta Hola siguientes puntos:

* En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.
* Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**. Vea el artículo [Conjuntos de datos](data-factory-create-datasets.md) para definir conjuntos de datos en JSON. 
* Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola. Hola [las actividades de movimiento de datos](#data-movement-activities) sección, haga clic en hello que desea toouse sea un origen o un receptor toolearn más acerca de cómo mover datos desde ese almacén de datos del almacén de datos. 

Para obtener un tutorial completo de creación de esta canalización, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Canalización de transformación de ejemplo
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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Tenga en cuenta Hola siguientes puntos: 

* En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**HDInsightHive**.
* archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **AzureStorageLinkedService**) y en  **secuencia de comandos** carpeta en el contenedor de hello **adfgetstarted**.
* Hola `defines` sección es la configuración de en tiempo de ejecución de hello toospecify utilizado que se pasa el script de hive toohello como valores de configuración de Hive (por ejemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Hola **typeProperties** sección es diferente para cada actividad de transformación. toolearn acerca de las propiedades de tipo compatible para una actividad de transformación, haga clic en la actividad de transformación de hello en hello [las actividades de transformación de datos](#data-transformation-activities) tabla. 

Para obtener un tutorial completo de creación de esta canalización, consulte [Tutorial: generar los datos primera canalización tooprocess con clúster de Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Varias actividades en una canalización
las canalizaciones de dos muestras anteriores Hola tengan sólo una actividad en ellos. pero se pueden tener más de una actividad en una canalización.  

Si tiene varias actividades en una canalización y salida de una actividad no es una entrada de otra actividad, las actividades de hello pueden ejecutar en paralelo si los segmentos de datos de entrada para las actividades de hello están listos. 

Dos actividades se puede encadenar haciendo que el conjunto de datos de salida de hello de una actividad como conjunto de datos de entrada de Hola de hello otra actividad. segunda actividad de Hola se ejecuta sólo cuando hello primero uno se completa correctamente.

![El encadenamiento de actividades en hello misma canalización](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

En este ejemplo, la canalización de hello tiene dos actividades: Activity1 y Activity2. Hola Activity1 toma Dataset1 como entrada y genera una salida Dataset2. Hello actividad tiene Dataset2 como entrada y genera un resultado Dataset3. Desde la salida de hello de Activity1 (Dataset2) es la entrada hello Activity2, hello Activity2 se ejecuta solo después de hello actividad se completa correctamente y genera Hola segmento Dataset2. Si Hola Activity1 se produce un error por algún motivo y no genera el segmento de hello Dataset2, Hola actividad 2 no se ejecuta para dicho sector (por ejemplo: ESTOY too10 de 9 AM). 

También puede encadenar actividades que se encuentran en diferentes canalizaciones.

![Encadenamiento de las actividades de dos canalizaciones](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

En este ejemplo, Pipeline1 solo tiene una actividad que toma Dataset1 como entrada y genera Dataset2 como salida. Hola Pipeline2 también tiene sólo una actividad que toma el conjunto de datos 2 como entrada y Dataset3 como salida. 

Para obtener más información, vea [Programación y ejecución](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Creación y supervisión de canalizaciones
Puede crear canalizaciones utilizando una de estas herramientas o SDK. 

- Asistente para copia 
- Azure Portal
- Visual Studio
- Azure PowerShell
- Plantilla del Administrador de recursos de Azure
- API de REST
- API de .NET

Vea Hola tutoriales para obtener instrucciones paso a paso para crear canalizaciones mediante una de estas herramientas o SDK.
 
- [Creación de una canalización con una actividad de transformación de datos](data-factory-build-your-first-pipeline.md)
- [Creación de una canalización con una actividad de movimiento de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Una vez que una canalización se crea/implementado, puede administrar y supervisar sus canalizaciones mediante el uso de Hola hojas de portal de Azure o supervisar y administrar aplicaciones. Vea Hola siguientes temas para obtener instrucciones paso a paso. 

- [Supervisión y administración de canalizaciones con las hojas de Azure Portal](data-factory-monitor-manage-pipelines.md)
- [Supervisión y administración de canalizaciones con la aplicación de supervisión y administración](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Canalización de una vez
Puede crear y programar una toorun canalización periódicamente (por ejemplo: por horas o días) hora que especifique en la definición de la canalización de hello en hello inicial y final. Para más información, consulte [Programación de actividades](#scheduling-and-execution) . También puede crear una canalización que se ejecute una sola vez. toodo por lo tanto, establecer hello **pipelineMode** propiedad Hola canalización definición demasiado**tendrá que repetir** tal como se muestra en hello según muestra JSON. valor predeterminado de Hola para esta propiedad es **programada**.

```json
{
    "name": "CopyPipeline",
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
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Tenga en cuenta los siguiente hello:

* **Iniciar** y **final** para la canalización de hello no están especificados.
* **Disponibilidad** de entrada y salida se especifica los conjuntos de datos (**frecuencia** y **intervalo**), incluso aunque factoría de datos no utiliza valores de hello.  
* La vista Diagrama no muestra las canalizaciones de una vez. Este comportamiento es así por diseño.
* Las canalizaciones de una vez no se pueden actualizar. También puede clonar una canalización de un solo uso, cambiarle el nombre, actualizar las propiedades e implementarlo toocreate otro.


## <a name="next-steps"></a>Pasos siguientes
- Para obtener más información sobre los conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md). 
- Si quiere conocer más detalles sobre cómo programar y ejecutar canalizaciones en Azure Data Factory, consulte [este artículo](data-factory-scheduling-and-execution.md). 
  

