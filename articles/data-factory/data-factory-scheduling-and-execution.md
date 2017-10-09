---
title: "aaaScheduling y la ejecución con factoría de datos | Documentos de Microsoft"
description: "Obtenga información sobre los aspectos de programación y ejecución del modelo de aplicación de Factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Programación y ejecución de Data Factory
En este artículo se explica los aspectos de programación y la ejecución de Hola Hola Data Factory de Azure del modelo de aplicación. En este artículo se presupone que comprende los conceptos básicos del modelo de aplicación de Data Factory, como la actividad, las canalizaciones, los servicios vinculados y los conjuntos de datos. Para los conceptos básicos de la factoría de datos de Azure, vea Hola siguientes artículos:

* [Introducción tooData generador](data-factory-introduction.md)
* [Procesos](data-factory-create-pipelines.md)
* [Conjuntos de datos](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Horas de inicio y finalización de la canalización
Una canalización solo está activa entre su hora de **inicio** y de **finalización**. No se ejecuta antes de la hora de inicio de Hola o después de la hora de finalización de Hola. Si se pausa la canalización de hello, no se ejecuta independientemente de su hora de inicio y finalización. Para una toorun de canalización, se debe no se produce la pausa. Encontrar estos valores (inicio, fin, en pausa) en la definición de la canalización de hello: 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Para más información sobre estas propiedades, vea el artículo sobre la [creación de canalizaciones](data-factory-create-pipelines.md). 


## <a name="specify-schedule-for-an-activity"></a>Definición de la programación de una actividad
No es canalización Hola que se ejecuta. Es actividades de Hola de canalización de Hola que se ejecutan en hello contexto general de canalización de Hola. Puede especificar una programación periódica para una actividad mediante hello **programador** sección de JSON de la actividad. Por ejemplo, puede programar una actividad toorun cada hora como sigue:  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Como se muestra en hello siguiente diagrama, especificar que una programación para una actividad crea una serie de ventanas de saltos de tamaño constante con Hola de canalización de inicio y finalización. Las ventanas de saltos de tamaño constante son series de intervalos de tiempo de tamaño fijo, no superpuestos y contiguos. Estas ventanas de saltos lógicas de tamaño constante para la actividad se denominan **ventanas de actividad**.

![Ejemplo de programador de actividades](media/data-factory-scheduling-and-execution/scheduler-example.png)

Hola **programador** propiedad para una actividad es opcional. Si se especifica esta propiedad, debe coincidir con el ritmo de hello especificado en la definición de hello del conjunto de datos de salida para la actividad de Hola. Actualmente, el conjunto de datos de salida es qué unidades Hola programación. Por lo tanto, debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado. 

## <a name="specify-schedule-for-a-dataset"></a>Definición de la programación de un conjunto de datos
Una actividad de una canalización de Data Factory puede tomar diversos **conjuntos de datos** de entrada, o ninguno, y generar uno o varios conjuntos de datos de salida. Para una actividad, puede especificar el ritmo de hello en qué Hola datos de entrada están disponibles o se generan los datos de salida de hello mediante hello **disponibilidad** sección en definiciones de conjunto de datos de Hola. 

**Frecuencia** en hello **disponibilidad** sección especifica la unidad de tiempo de Hola. Hola valores permitidos para la frecuencia son: minuto, hora, día, semana y mes. Hola **intervalo** propiedad en la sección de disponibilidad de hello especifica un multiplicador para la frecuencia. Por ejemplo: si establece frecuencia de hello tooDay e intervalo se establece too1 para un conjunto de datos de salida, los datos de salida de hello se generan cada día. Si especifica Hola frecuencia como minuto, se recomienda que establezca Hola intervalo toono inferior a 15. 

En el siguiente ejemplo de Hola, datos de entrada de hello están disponibles por hora y los datos de salida de hello se producen cada hora (`"frequency": "Hour", "interval": 1`). 

**Conjunto de datos de entrada:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Conjunto de datos de salida**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Actualmente, **programación de Hola de unidades de conjunto de datos de salida**. En otras palabras, programación de hello especificada para el conjunto de datos de salida de hello es toorun usa una actividad en tiempo de ejecución. Por lo tanto, debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado. Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada. 

En los siguientes Hola canalización definición, hello **programador** propiedad es programación toospecify usado para la actividad de Hola. Esta propiedad es opcional. Actualmente, programación de hello para la actividad de hello debe coincidir con programación de hello especificada para el conjunto de datos de salida de hello.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

En este ejemplo, cada hora se ejecuta de actividad de hello entre Hola hora inicial y final de la canalización de Hola. datos de salida de saludo se produce cada hora para windows de tres horas (8 A.M. - 9 AM, 9 a 10 AM y a 10 11 AM). 

Cada unidad de datos consumida o producida por la ejecución de una actividad se denomina **segmento de datos**. Hola siguiente diagrama muestra un ejemplo de una actividad con un conjunto de datos de entrada y un conjunto de datos de salida: 

![Programador de disponibilidad](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

diagrama de Hello muestra cada hora Hola segmentos de datos de Hola de entrada y salida de conjunto de datos. diagrama de Hello muestra tres segmentos de entrada que están listos para su procesamiento. actividad de 10-11 AM Hello está en curso, que produce el segmento de salida de hello 10-11 AM. 

Puede tener acceso a intervalo de tiempo de hello asociado con el intervalo actual de Hola Hola de conjunto de datos JSON mediante variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) y [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). De forma similar, puede tener acceso a intervalo de tiempo de hello asociado con una ventana de actividad utilizando hello WindowStart y WindowEnd. programación Hola de una actividad debe coincidir con la programación de hello del conjunto de datos de salida de hello para la actividad de Hola. Por lo tanto, Hola SliceStart y SliceEnd valores son Hola mismo como valores WindowStart y WindowEnd respectivamente. Para más información sobre estas variables, vea el artículo [Funciones y variables del sistema](data-factory-functions-variables.md#data-factory-system-variables).  

Puede usar estas variables para distintos fines en el JSON de actividad. Por ejemplo, puede utilizarlas tooselect datos de entrada y salida conjuntos de datos que representa datos de serie temporal (por ejemplo: ESTOY too9 de 8 A.M.). Este ejemplo también utiliza **WindowStart** y **WindowEnd** tooselect datos relevantes para una actividad ejecutar y cópielo tooa blob con hello adecuado **folderPath**. Hola **folderPath** es toohave con parámetros en una carpeta independiente para cada hora.  

En el anterior ejemplo de Hola, programación de hello especificada para los conjuntos de datos de entrada y salida se Hola igual (cada hora). Si Hola entrada conjunto de datos de actividad hello está disponible en una frecuencia distinta, digamos cada 15 minutos, actividad de hello generadas por este conjunto de datos de salida sigue ejecutándose una vez cada hora como conjunto de datos de salida de hello es qué unidades Hola programación de actividades. Para más información, vea [Modelado de conjuntos de datos con distintas frecuencias](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>Directivas y disponibilidad del conjunto de datos
Se muestra el uso de Hola de frecuencia y el intervalo de propiedades en la sección de disponibilidad de Hola de definición de conjunto de datos. Hay algunas propiedades que afectan a la programación de Hola y la ejecución de una actividad. 

### <a name="dataset-availability"></a>Conjunto de datos availability 
Hello tabla siguiente describen propiedades que puede utilizar en hello **disponibilidad** sección:

| Propiedad | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| frequency |Especifica la unidad de tiempo de hello para la producción de segmento del conjunto de datos.<br/><br/><b>Frecuencia admitida</b>: Minute, Hour, Day, Week, Month. |Sí |N/D |
| interval |Especifica un multiplicador para frecuencia<br/><br/>"Intervalo de frecuencia x" determina con qué frecuencia hello segmento se genera.<br/><br/>Si necesita hello toobe de conjunto de datos se crean sectores de cada hora, establecer <b>frecuencia</b> demasiado<b>hora</b>, y <b>intervalo</b> demasiado<b>1</b>.<br/><br/><b>Tenga en cuenta</b>: si especifica frecuencia como minuto, se recomienda que establezca Hola intervalo toono inferior a 15 |Sí |N/D |
| style |Especifica si se debe generar segmento hello en hello inicio/final del intervalo de saludo.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Si se establece la frecuencia de tooMonth y se establece el estilo tooEndOfInterval, Hola segmento se genera Hola último día del mes. Si se establece tooStartOfInterval en estilo de hello, Hola segmento se genera en hello primer día del mes.<br/><br/>Si se establece la frecuencia de tooDay y se establece el estilo tooEndOfInterval, segmento de Hola se genera en la última hora del día de Hola Hola.<br/><br/>Si se establece la frecuencia de tooHour y se establece el estilo tooEndOfInterval, segmento de Hola se genera al final de Hola de hora de Hola. Por ejemplo, para un intervalo durante el período de 1 P.M. – 2 P.M., segmento de Hola se genera a las 2 P.M.. |No |EndOfInterval |
| anchorDateTime |Define la posición absoluta de hello en el tiempo utilizado por los límites del sector de programador toocompute conjunto de datos. <br/><br/><b>Tenga en cuenta</b>: si hello AnchorDateTime tiene Dateparts más granulares que la frecuencia de hello, hello partes más pormenorizadas se omiten. <br/><br/>Por ejemplo, si hello <b>intervalo</b> es <b>cada hora</b> (frecuencia: hora e intervalo: 1) hello y <b>AnchorDateTime</b> contiene <b>minutos y segundos</b>, a continuación, Hola <b>minutos y segundos</b> partes de hello AnchorDateTime se omiten. |No |01/01/0001 |
| Offset |Intervalo de tiempo por qué Hola se desplazan inicial y final de todos los sectores de conjunto de datos. <br/><br/><b>Tenga en cuenta</b>: si se especifican anchorDateTime y offset, resultado de hello es Hola combinan MAYÚS. |No |N/D |

### <a name="offset-example"></a>Ejemplo de offset
De forma predeterminada, cada día (`"frequency": "Day", "interval": 1`) se inician los segmentos a las 24:00 UTC (medianoche). Si desea Hola inicio toobe 6: 00 UTC hora en su lugar, establezca Hola offset tal como se muestra en el siguiente fragmento de código de hello: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Ejemplo de anchorDateTime
En el siguiente ejemplo de Hola Hola conjunto de datos se produce una vez cada 23 horas. Hello primer sector comienza en tiempo de hello especificado por anchorDateTime hello, que se establece demasiado`2017-04-19T08:00:00` (hora UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Ejemplo de desplazamiento y estilo
es un conjunto de datos mensual Hello siguiente conjunto de datos y se genera en 3rd de cada mes a las 8:00 A.M. (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>Directiva del conjunto de datos
Un conjunto de datos puede tener una directiva de validación definida que especifica cómo se pueden validar los datos de hello generados por la ejecución de un segmento antes de que está listo para su uso. En tales casos, después de que ha terminado de ejecutarse, segmento de Hola Hola salida segmento se cambia el estado demasiado**espera** con un subestado de **validación**. Después de validan intervalos de hello, estado del sector Hola cambia demasiado**listo**. Si se ha generado un segmento de datos, pero no superó la validación de hello, no se procesan las ejecuciones de actividad de intervalos de nivel inferiores que dependen de este segmento. [Supervisar y administrar las canalizaciones](data-factory-monitor-manage-pipelines.md) portadas Hola diversos estados de segmentos de datos en la factoría de datos.

Hola **directiva** sección de definición de conjunto de datos define los criterios de Hola o debe cumplir la condición de Hola que Hola segmentos del conjunto de datos. Hello tabla siguiente describen propiedades que puede utilizar en hello **directiva** sección:

| Nombre de la directiva | Descripción | Aplica demasiado| Obligatorio | Valor predeterminado |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Valida datos hello en un **blobs de Azure** Hola de cumple los requisitos mínimos de tamaño (en megabytes). |Blob de Azure |No |N/D |
| minimumRows | Valida datos hello en un **base de datos SQL de Azure** o un **tabla de Azure** contiene Hola número mínimo de filas. |<ul><li>Azure SQL Database</li><li>tabla de Azure</li></ul> |No |N/D |

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

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Para consultar ejemplos y más información sobre estas propiedades, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md). 

## <a name="activity-policies"></a>Directivas de la actividad
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

Para más información, vea el artículo [Canalizaciones](data-factory-create-pipelines.md). 

## <a name="parallel-processing-of-data-slices"></a>Procesamiento en paralelo de segmentos de datos
Puede establecer fecha de inicio de hello para la canalización de Hola Hola anteriores. Al hacerlo, factoría de datos automáticamente calcula (rellenos atrás) todos los segmentos de datos en los último hello y empieza a procesarlos. Por ejemplo: si se crea una canalización con fecha de inicio de 2017-04-01 y Hola fecha actual es de 2017-04-10. Si cadencia de Hola de hello salida de conjunto de datos es diariamente, a continuación, inicia el generador de datos procesar todos los sectores de Hola de 2017-04-01 too2017-04-09 inmediatamente porque Hola fecha de inicio se encuentra Hola anterior. Hola segmento de 2017-04-10 no se procesó todavía porque Hola valor de propiedad de estilo en la sección de disponibilidad de hello EndOfInterval de forma predeterminada. Hello más antigua se procesa en primer lugar como valor predeterminado de hello valo executionPriorityOrder es OldestFirst. Para obtener una descripción de la propiedad de estilo de hello, consulte [disponibilidad del conjunto de datos](#dataset-availability) sección. Para obtener una descripción de la sección de executionPriorityOrder hello, vea hello [las directivas de actividad](#activity-policies) sección. 

Puede configurar toobe de sectores de datos se llene de back procesada en paralelo por establecer Hola **simultaneidad** propiedad Hola **directiva** sección de JSON de la actividad de Hola. Esta propiedad determina el número de Hola de ejecuciones paralelas que pueden ocurrir en distintos sectores. valor predeterminado de Hello para la propiedad de simultaneidad de hello es 1. Por tanto, se procesa un segmento a la vez de forma predeterminada. valor máximo de Hello es 10. Cuando una canalización debe toogo a través de un conjunto grande de datos disponibles, que tienen un valor mayor de simultaneidad acelera el procesamiento de datos de Hola. 

## <a name="rerun-a-failed-data-slice"></a>Volver a ejecutar un segmento de datos con errores
Cuando se produce un error durante el procesamiento de un segmento de datos, puede averiguar por qué no se pudo procesamiento Hola de un segmento mediante hojas de portal de Azure o supervisar y administrar aplicaciones. Consulte [Supervisión y administración de canalizaciones mediante hojas de Azure Portal](data-factory-monitor-manage-pipelines.md) o [Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) para más información.

Considere la posibilidad de hello siguiente ejemplo, que se muestra en dos actividades. Activity1 y Activity2. Activity1 consume un segmento de Dataset1 y genera un segmento del conjunto de datos 2, que consume como entrada Activity2 tooproduce un segmento de hello Final del conjunto de datos.

![Segmento con errores](./media/data-factory-scheduling-and-execution/failed-slice.png)

Hola diagrama muestra fuera de tres segmentos recientes, que se produjo un segmento de error productor Hola 9 y 10 AM para Dataset2. Factoría de datos realiza automáticamente un seguimiento de dependencia para el conjunto de datos de series de tiempo de Hola. Como resultado, no se inicia de sector de hello 9 y 10 AM siguen en la cadena de ejecución de la actividad de Hola.

Herramientas de administración y supervisión del generador de datos permiten toodrill en registros de diagnóstico de Hola para hello segmento erróneo tooeasily buscar Hola raíz causa de problema de Hola y de corregirlo. Una vez solucionado el problema de hello, puede iniciar fácilmente actividad hello ejecutar tooproduce Hola error segmento. Para obtener más información acerca de cómo toorerun y comprender las transiciones de estado para segmentos de datos, vea [supervisión y administración de canalizaciones mediante módulos de portal de Azure](data-factory-monitor-manage-pipelines.md) o [aplicación de supervisión y administración](data-factory-monitor-manage-app.md).

Después de volver a ejecutar Hola 9 y 10 AM segmentar de **Dataset2**, factoría de datos inicia Hola ejecute para el segmento de hello 9 y 10 AM dependientes en hello conjunto de datos final.

![Repetición de ejecución de un segmento con errores](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Varias actividades en una canalización
pero se pueden tener más de una actividad en una canalización. Si tiene varias actividades en una canalización y salida de hello de una actividad no es una entrada de otra actividad, las actividades de hello pueden ejecutar en paralelo si los segmentos de datos de entrada para las actividades de hello están listos.

Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Hola actividades pueden ser Hola misma canalización o en las canalizaciones diferentes. segunda actividad de Hola se ejecuta sólo cuando hello primero uno finaliza correctamente.

Por ejemplo, considere la posibilidad de hello siguiente caso donde una canalización tiene dos actividades:

1. La actividad A1 que requiere el conjunto de datos de entrada externo D1 y genera el conjunto de datos de salida D2.
2. La actividad A2 que requiere una entrada del conjunto de datos D2 y genera el conjunto de datos de salida D3.

En este escenario, las actividades de A1 y A2 se Hola misma canalización. actividad de Hello que a1 se ejecuta cuando los datos externos de hello están disponibles y se alcanza la frecuencia de disponibilidad de hello programado. Hello actividad A2 se ejecuta cuando hello intervalos programados desde D2 estén disponibles y hello frecuencia disponibilidad programada se alcanza. Si se produce un error en uno de los sectores de hello en el conjunto de datos D2, A2 no se ejecuta para dicho sector hasta que esté disponible.

Hola vista de diagrama con ambas actividades Hola misma canalización sería Hola siguiente diagrama:

![El encadenamiento de actividades en hello misma canalización](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Tal y como se mencionó anteriormente, las actividades de hello pueden estar en diferentes canalizaciones. En este escenario, vista de diagrama de hello sería Hola siguiente diagrama:

![Encadenamiento de las actividades de dos canalizaciones](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Vea hello [copiar secuencialmente](#copy-sequentially) sección en el apéndice de hello para obtener un ejemplo.

## <a name="model-datasets-with-different-frequencies"></a>Modelado de conjuntos de datos con distintas frecuencias
En los ejemplos de hello, las frecuencias de Hola de entrada y salida hello y conjuntos de datos de actividad ventana de programación se Hola mismo. Algunos escenarios requieren la salida de hello capacidad tooproduce a una frecuencia diferente a las frecuencias de Hola de una o más entradas. Data Factory admite el modelado de estos escenarios.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Ejemplo 1: Generación de un informe de salida diario para los datos de entrada que esté disponibles cada hora
Considere un escenario en el que tiene datos de medida de entrada de sensores disponibles cada hora en Azure Blob Storage. Desea tooproduce un informe diario agregado con estadísticas como Media, máximo y mínimo por día Hola con [actividad de hive de factoría de datos](data-factory-hive-activity.md).

A continuación, se muestra cómo puede modelar este escenario con Data Factory:

**Conjunto de datos de entrada**

Hola cada hora de entrada de archivos se colocan en la carpeta Hola Hola dado día. La disponibilidad para la entrada se establece en **Hour** (frecuencia: hora, intervalo: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Conjunto de datos de salida**

Se crea cada día en un archivo de salida en la carpeta del día de Hola. La disponibilidad de la salida se establece en **Day** (frecuencia: día e intervalo: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Actividad: actividad de Hive en una canalización**

script de hive Hola recibe Hola adecuado *DateTime* información como parámetros que utilizan hello **WindowStart** variable tal y como se muestra en el siguiente fragmento de código de hello. script de hive Hola emplea estos datos de hello tooload variable desde la carpeta correcta de Hola durante el día de Hola y la salida de hello agregación toogenerate Hola.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

Hello siguiente diagrama muestra el escenario de Hola desde un punto de vista de dependencia de los datos.

![Dependencia de los datos](./media/data-factory-scheduling-and-execution/data-dependency.png)

segmento de la salida de Hello para cada día depende de 24 sectores por hora de un conjunto de datos de entrada. Calcula de la factoría de datos estas dependencias automáticamente averiguando Hola segmentos de datos de entrada que se encuentran en hello mismo período de tiempo como Hola toobe de segmento de salida generado. Si cualquiera de los segmentos de entrada de hello 24 no está disponible, factoría de datos espera Hola segmento entrada toobe listo antes de iniciar la ejecución de actividad diaria de Hola.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Ejemplo 2: Especificación de la dependencia con expresiones y funciones de Data Factory
Consideremos otro escenario. Suponga que tiene una actividad de Hive que procesa dos conjuntos de datos de entrada. Uno de ellos tiene nuevos datos diariamente, pero otro obtiene datos nuevos cada semana. Suponga que desea toodo una combinación entre dos entradas de Hola y generar una salida de cada día.

método sencillo de Hello en el que factoría de datos automáticamente determina la entrada derecha Hola segmentos tooprocess alineando salida toohello tiempo del segmento de datos no funciona período.

Debe especificar que para cada ejecución de actividad, Hola factoría de datos debe utilizar el segmento de datos de la semana pasada para hello conjunto de datos de entrada semanal. Usar funciones de factoría de datos de Azure como se muestra en hello siguiente fragmento de código tooimplement este comportamiento.

**Input1: blob de Azure**

Hola primera entrada de hello blobs de Azure se actualiza diariamente.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Input2: blob de Azure**

Entrada2 es hello Azure blob que se actualiza semanalmente.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Salida: blob de Azure**

Un archivo de salida se crea cada día en la carpeta de Hola para día Hola. Disponibilidad de salida se establece demasiado**día** (frecuencia: día, intervalo: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Actividad: actividad de Hive en una canalización**

actividad de hive Hello toma dos entradas de Hola y genera un segmento de salida todos los días. Puede especificar toodepend de segmento de salida de cada día en Hola segmento de entrada de la semana anterior para la entrada semanal como se indica a continuación.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

Para conocer la lista de funciones y variables del sistema que admite Data Factory, consulte el artículo [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md) .

## <a name="appendix"></a>Anexo

### <a name="example-copy-sequentially"></a>Ejemplo: copia secuencial
Es posible toorun varias operaciones de copia uno tras otro de forma secuencial/ordenados. Por ejemplo, podría tener conjuntos de datos de salida de datos dos actividades de una canalización (CopyActivity1 y CopyActivity2) con hello después de entrada de copia:   

CopyActivity1

Entrada: Dataset. Salida: Dataset2.

CopyActivity2

Entrada: Dataset2.  Salida: Dataset3.

CopyActivity2 llevarían a cabo únicamente si se ha ejecutado correctamente hello CopyActivity1 y Dataset2 está disponible.

Aquí es JSON de la canalización de ejemplo Hola:

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

Observe que en el ejemplo de Hola, conjunto de datos de salida de hello de hello primera actividad de copia (Dataset2) se especifica como entrada para la segunda actividad de Hola. Por lo tanto, Hola segunda actividad se ejecuta sólo cuando el conjunto de datos de salida de hello desde la primera actividad de hello está listo.  

En el ejemplo de Hola, CopyActivity2 puede tener una entrada diferente, como Dataset3, pero se especifica Dataset2 como una entrada tooCopyActivity2, por lo que la actividad hello no se ejecuta hasta que finalice la CopyActivity1. Por ejemplo:

CopyActivity1

Entrada: Dataset1. Salida: Dataset2.

CopyActivity2

Entradas: Dataset3, Dataset2. Salida: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Tenga en cuenta que en el ejemplo de Hola, se especifican dos conjuntos de datos de entrada para la segunda actividad de copia de Hola. Cuando se especifican varias entradas, solo Hola primera entrada conjunto de datos se utiliza para copiar datos, pero otros conjuntos de datos se utilizan como dependencias. CopyActivity2 iniciaría solo después de hello condiciones siguientes se cumplen:

* ActividadCopia1 se ha completado correctamente y ConjuntoDatos2 está disponible. Este conjunto de datos no se utiliza cuando se copian datos tooDataset4. Solo actúa como una dependencia de programación de ActividadCopia2.   
* ConjuntoDatos3 está disponible. Este conjunto de datos representa los datos de Hola que constituye el destino de toohello copiada. 
