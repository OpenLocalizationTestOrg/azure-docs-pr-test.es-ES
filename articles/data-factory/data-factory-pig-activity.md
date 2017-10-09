---
title: "datos de aaaTransform con actividad de Pig de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo puede utilizar Hola actividad de Pig en un scripts de Pig de toorun de factoría de datos de Azure en un clúster de HDInsight en-petición/su propio."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Transformación de datos mediante la actividad de Pig en Azure Data Factory
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Actividad de Hive](data-factory-hive-activity.md) 
> * [Actividad de Pig](data-factory-pig-activity.md)
> * [Actividad MapReduce](data-factory-map-reduce.md)
> * [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Actividad de Spark](data-factory-spark.md)
> * [Actividad de ejecución de Batch de Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Actividad Actualizar recurso de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md)
> * [Actividad U-SQL de Data Lake Analytics](data-factory-usql-activity.md)
> * [Actividad personalizada de .NET](data-factory-use-custom-activities.md)

Hola actividad de HDInsight Pig en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta consultas de Pig en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) clúster de HDInsight basados en Windows/Linux. En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.

> [!NOTE] 
> Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo. 

## <a name="syntax"></a>Sintaxis

```JSON
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
## <a name="syntax-details"></a>Detalles de la sintaxis
| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| name |Nombre de actividad de Hola |Sí |
| description |Texto que describe qué actividad Hola se usa para |No |
| type |HDinsightPig |Sí |
| inputs |Una o más entradas consumen Hola actividad de Pig |No |
| outputs |Una o más salidas producidos por hello actividad de Pig |Sí |
| linkedServiceName |Clúster de HDInsight de referencia toohello registrado como un servicio vinculado de factoría de datos |Sí |
| script |Especifique el script de Pig de hello en línea |No |
| ruta de acceso de script |Almacenar el script de Pig hello en el almacenamiento de blobs de Azure y proporcionar Hola ruta toohello al archivo. Use la propiedad 'script' o 'scriptPath'. No se pueden usar las dos juntas. nombre de archivo de Hello distingue mayúsculas de minúsculas. |No |
| define los campos |Especificar parámetros como pares clave/valor para hacer referencia a dentro de hello script de Pig |No |

## <a name="example"></a>Ejemplo
Veamos un ejemplo de juego registra análisis donde desea tooidentify Hola tiempo reproductores jugar iniciadas por su empresa.

Hola siguiente muestra de registro de juego es un archivo de separados por comas (,). Contiene Hola siguientes campos: identificador de perfil, SessionStart, duración, SrcIPAddress y GameType.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hola **script de Pig** tooprocess estos datos:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

Hola tooexecute este Pig script en una canalización de factoría de datos, siga los pasos:

1. Crear un servicio vinculado tooregister [su propio HDInsight clústerde](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurar [clúster de cálculo de HDInsight a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Llamaremos a este servicio vinculado **HDInsightLinkedService**.
2. Crear un [servicio vinculado](data-factory-azure-blob-connector.md) almacenamiento de blobs de tooAzure en conexión de tooconfigure Hola hospeda los datos de Hola. Llamaremos a este servicio vinculado **StorageLinkedService**.
3. Crear [conjuntos de datos](data-factory-create-datasets.md) que apunta hello y toohello entrada los datos de salida. Vamos a llamar a conjunto de datos de entrada de hello **PigSampleIn** y conjunto de datos de salida de hello **PigSampleOut**.
4. Copiar consulta de Pig de hello en un almacenamiento de blobs de Azure configurado en el paso 2 de # Hola de archivo. Si almacenamiento de Azure que hospeda datos Hola Hola es diferente de hello uno que hospeda el archivo de consulta de hello, crear un servicio vinculado de almacenamiento de Azure independiente. Consulte servicio toohello vinculado en la configuración de la actividad de Hola. Use ** scriptPath ** archivo de script de toospecify Hola ruta de acceso toopig y **scriptLinkedService**. 
   
   > [!NOTE]
   > También puede proporcionar Hola Pig script en línea en la definición de actividad de hello mediante hello **script** propiedad. Sin embargo, no se recomienda este enfoque como todos los caracteres especiales en el script de Hola necesita toobe caracteres de escape y puede provocar problemas de depuración. práctica recomendada de Hello es toofollow paso #4.
   > 
   > 
5. Crear canalización Hola con hello HDInsightPig actividad. Esta actividad procesa los datos de entrada de hello mediante la ejecución de script de Pig en clúster de HDInsight.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
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
6. Implementar la canalización de Hola. Consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md) para obtener más información. 
7. Supervisar la canalización de hello mediante la supervisión de la factoría de datos de Hola y vistas de administración. Consulte el artículo [Supervisión y administración de las canalizaciones de Factoría de datos](data-factory-monitor-manage-pipelines.md) para obtener más información.

## <a name="specifying-parameters-for-a-pig-script"></a>Especificación de parámetros para un script de Pig
Considere el siguiente ejemplo de Hola: registros de juegos se ingestión diariamente en el almacenamiento de blobs de Azure y se almacenan en una carpeta fecha según con particiones y la hora. Desea que el script de Pig hello tooparameterize y pasa la ubicación de la carpeta de entrada de hello dinámicamente en tiempo de ejecución y también generar salida de hello particionado con la fecha y hora.

toouse parámetros de script de Pig, realice Hola siguientes:

* Definir los parámetros de hello en **define**.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
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
* En el Script de Pig hello, consulte parámetros toohello mediante '**$parameterName**' como se muestra en el siguiente ejemplo de Hola:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>Otras referencias
* [Actividad de Hive](data-factory-hive-activity.md)
* [Actividad MapReduce](data-factory-map-reduce.md)
* [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts de R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

