---
title: aaaData generador de funciones y Variables del sistema | Documentos de Microsoft
description: Proporciona una lista de funciones y variables del sistema de Azure Data Factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure Data Factory: funciones y variables del sistema
Este artículo proporciona información sobre las funciones y las variables compatibles con Azure Data Factory.

## <a name="data-factory-system-variables"></a>Variables del sistema de Data Factory
| Nombre de la variable | Descripción | Ámbito del objeto | Ámbito JSON y casos de uso |
| --- | --- | --- | --- |
| WindowStart |Inicio del intervalo de tiempo para la ventana de ejecución de la actividad actual |activity |<ol><li>Especifique las consultas de selección de datos. Consulte los artículos de conector que se hace referencia en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo.</li> |
| WindowEnd |Final del intervalo de tiempo para la ventana de ejecución de actividad actual |activity |igual que WindowStart. |
| SliceStart |Inicio del intervalo de tiempo para el segmento de datos que se está generando |activity<br/>dataset |<ol><li>Especifique rutas de acceso dinámicas a carpetas y nombres de archivo mientras trabaja con [Azure Blob](data-factory-azure-blob-connector.md) y [conjuntos de archivos del sistema de archivos](data-factory-onprem-file-system-connector.md).</li><li>Especifique las dependencias de entrada con funciones de factoría de datos en la colección de entradas de la actividad.</li></ol> |
| SliceEnd |Fin del intervalo de tiempo del segmento de datos actual. |activity<br/>dataset |igual que SliceStart. |

> [!NOTE]
> En la actualidad factoría de datos requiere ese Hola programar Hola especificado en actividad coincide exactamente con programación de hello especificada en la disponibilidad del conjunto de datos de salida de hello. Por lo tanto, WindowStart, WindowEnd y SliceStart y SliceEnd siempre asignan toohello mismo tiempo período y un segmento de salida único.
> 

### <a name="example-for-using-a-system-variable"></a>Ejemplo de uso de una variable del sistema
Hola siguiente ejemplo, año, mes, día y hora de **SliceStart** se extraen en variables independientes que usan **folderPath** y **fileName** propiedades.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>Funciones de Data Factory
Puede utilizar funciones de factoría de datos junto con las variables del sistema para hello siguientes fines:

1. Especificar las consultas de selección de datos (consulte los artículos de conector al que hace referencia hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo.
   
   Hola tooinvoke de sintaxis es una función de la factoría de datos:  **$$ <function>**  para las consultas de selección de datos y otras propiedades en la actividad hello y conjuntos de datos.  
2. Especifique las dependencias de entrada con funciones de factoría de datos en la colección de entradas de la actividad.
   
    $$ no es necesario para especificar expresiones de dependencia de entrada.     

Hola según muestra, **sqlReaderQuery** propiedad en un archivo JSON se asigna el valor tooa devolviendo hello `Text.Format` función. Este ejemplo también utiliza una variable del sistema denominada **WindowStart**, que representa la hora de inicio de Hola de ventana de la ejecución de la actividad de Hola.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

Consulte el tema [Cadenas con formato de fecha y hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx), en el que se describen las diferentes opciones de formato que puede usar (por ejemplo: aa frente a aaaa). 

### <a name="functions"></a>Functions
Hola las tablas siguientes enumeran todas las funciones de hello en Data Factory de Azure:

| Categoría | Función | Parámetros | Descripción |
| --- | --- | --- | --- |
| Hora |AddHours(X,Y) |X: DateTime  <br/><br/>Y: int |Agrega Y horas toohello X momento dado. <br/><br/>Ejemplo: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Hora |AddMinutes(X,Y) |X: DateTime  <br/><br/>Y: int |Agrega Y minutos tooX.<br/><br/>Ejemplo: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Hora |StartOfHour(X) |X: DateTime  |Obtiene Hola hora de inicio de hora de hello representada por el componente de hora de Hola de X. <br/><br/>Ejemplo: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Date |AddDays(X,Y) |X: DateTime <br/><br/>Y: int |Agrega Y días tooX. <br/><br/>Ejemplo: 9/15/2013 12:00:00 PM + 2 días = 9/17/2013 12:00:00 PM.<br/><br/>También puede restar días especificando Y como un número negativo.<br/><br/>Ejemplo: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Date |AddMonths(X,Y) |X: DateTime <br/><br/>Y: int |Agrega Y meses tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.<br/><br/>También puede restar meses especificando Y como un número negativo.<br/><br/>Ejemplo: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Date |AddQuarters(X,Y) |X: DateTime  <br/><br/>Y: int |Suma Y * 3 meses tooX.<br/><br/>Ejemplo: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Date |AddWeeks(X,Y) |X: DateTime <br/><br/>Y: int |Suma Y * tooX de 7 días<br/><br/>Ejemplo: 9/15/2013 12:00:00 PM + 1 semana = 9/22/2013 12:00:00 PM<br/><br/>También puede restar semanas especificando Y como un número negativo.<br/><br/>Ejemplo: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Date |AddYears(X,Y) |X: DateTime <br/><br/>Y: int |Agrega Y años tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>También puede restar años especificando Y como un número negativo.<br/><br/>Ejemplo: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Date |Day(X) |X: DateTime  |Obtiene el componente de día de Hola de X.<br/><br/>Ejemplo: `Day of 9/15/2013 12:00:00 PM is 9`. |
| Date |DayOfWeek(X) |X: DateTime  |Obtiene el día de hello del componente de la semana de X.<br/><br/>Ejemplo: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Date |DayOfYear(X) |X: DateTime  |Obtiene el día de hello en el año de hello representado por el componente correspondiente al año Hola de X.<br/><br/>Ejemplos:<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Date |DaysInMonth(X) |X: DateTime  |Obtiene los días de hello en mes Hola representado por el componente de mes de hello del parámetro X.<br/><br/>Ejemplo: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Date |EndOfDay(X) |X: DateTime  |Obtiene la fecha y hora de Hola que representa el final de Hola de hello día (componente de día) de X.<br/><br/>Ejemplo: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Date |EndOfMonth(X) |X: DateTime  |Obtiene Hola final del mes de hello representado por el componente de mes del parámetro X. <br/><br/>Ejemplo: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (fecha y hora que representa Hola final del mes de septiembre) |
| Date |StartOfDay(X) |X: DateTime  |Obtiene Hola inicio del día de hello representado por el componente de día de hello del parámetro X.<br/><br/>Ejemplo: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| DateTime |From(X) |X: String |Analizar la cadena X tooa fecha y hora. |
| DateTime |Ticks(X) |X: DateTime  |Obtiene propiedad del parámetro hello X de tics de Hola. Un TIC es igual a 100 nanosegundos. valor de Hola de esta propiedad representa número de Hola de pasos que han transcurrido desde medianoche de 12:00:00 del 1 de enero de 0001. |
| Texto |Format(X) |X: String variable |Hola de formatos de texto (usar `\\'` tooescape de combinación `'` caracteres).|

> [!IMPORTANT]
> Cuando se usa una función dentro de otra función, no es necesario toouse  **$$**  prefijo de función interna de Hola. Por ejemplo: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' y RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)). En este ejemplo, observe que  **$$**  prefijo no se utiliza para hello **Time.AddHours** (función). 

#### <a name="example"></a>Ejemplo
Hola parámetros de entrada y salida de ejemplo siguientes para la actividad de Hive Hola se determinan mediante hello `Text.Format` funciones y variables de sistema SliceStart. 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>Ejemplo 2

En el siguiente ejemplo de Hola Hola Hola que actividad de procedimiento almacenado se determina mediante el texto hello en el parámetro DateTime. Función de formato y Hola SliceStart variable. 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>Ejemplo 3
tooread datos del día anterior en lugar de días representado por hello SliceStart, utilice la función de AddDays de hello tal y como se muestra en el siguiente ejemplo de Hola: 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

Consulte el tema [Cadenas con formato de fecha y hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx), en el que se describen las diferentes opciones de formato que puede usar (por ejemplo: aa frente a aaaa). 

