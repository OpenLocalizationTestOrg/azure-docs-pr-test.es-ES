---
title: 'datos de aaaTransform con actividad de Hive: Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo puede utilizar Hola actividad de Hive en un consultas de Hive de toorun de factoría de datos de Azure en un clúster de HDInsight en-petición/su propio."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Transformación de datos mediante la actividad de Hive en Azure Data Factory 
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

Hola actividad de HDInsight Hive en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta consultas de Hive en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) clúster de HDInsight basados en Windows/Linux. En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.

> [!NOTE] 
> Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo. 

## <a name="syntax"></a>Sintaxis

```JSON
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
## <a name="syntax-details"></a>Detalles de la sintaxis
| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| name |Nombre de actividad de Hola |Sí |
| description |Texto que describe qué actividad Hola se usa para |No |
| type |HDinsightHive |Sí |
| inputs |Entradas consumidos por la actividad de Hive hello |No |
| outputs |Resultados generados por la actividad de Hive hello |Sí |
| linkedServiceName |Clúster de HDInsight de referencia toohello registrado como un servicio vinculado de factoría de datos |Sí |
| script |Especifique el script de Hive de hello en línea |No |
| ruta de acceso de script |Hola de almacén en el almacenamiento de blobs de Azure de script de Hive y proporcionar Hola ruta toohello al archivo. Use la propiedad 'script' o 'scriptPath'. No se pueden usar las dos juntas. nombre de archivo de Hello distingue mayúsculas de minúsculas. |No |
| define los campos |Especificar parámetros como pares clave/valor para hacer referencia a dentro de script de Hive hello mediante 'hiveconf' |No |

## <a name="example"></a>Ejemplo
Veamos un ejemplo de juego registra análisis donde desea tooidentify Hola tiempo los usuarios jugar iniciadas por su empresa. 

Hello siguiente es un ejemplo juego registro, que es la coma (`,`) separados y contiene los siguientes campos: identificador de perfil, SessionStart, duración, SrcIPAddress y GameType de Hola.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hola **de script de Hive** tooprocess estos datos:

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

tooexecute secuencia de comandos de esta sección en una canalización de factoría de datos, necesita toodo Hola siguiente

1. Crear un servicio vinculado tooregister [su propio HDInsight clústerde](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o configurar [clúster de cálculo de HDInsight a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Llamaremos a este servicio vinculado "HDInsightLinkedService".
2. Crear un [servicio vinculado](data-factory-azure-blob-connector.md) almacenamiento de blobs de tooAzure en conexión de tooconfigure Hola hospeda los datos de Hola. Llamaremos a este servicio vinculado "StorageLinkedService"
3. Crear [conjuntos de datos](data-factory-create-datasets.md) que apunta hello y toohello entrada los datos de salida. Vamos a Hola llamada "HiveSampleIn" del conjunto de datos de entrada y Hola "HiveSampleOut" del conjunto de datos de salida
4. Copiar consulta de Hive Hola como un almacenamiento de blobs configurados en el paso 2 de # tooAzure de archivo. Si almacenamiento Hola para hospedar datos hello es diferente de hello uno aloja este archivo de consulta, cree un servicio vinculado de almacenamiento de Azure independiente y consulte tooit en actividad hello. Use ** scriptPath ** toospecify Hola ruta toohive consulta archivo y **scriptLinkedService** toospecify Hola almacenamiento de Azure que contiene el archivo de script de Hola. 
   
   > [!NOTE]
   > También puede proporcionar Hola Hive script en línea en la definición de actividad de hello mediante hello **script** propiedad. No se recomienda este enfoque como todos los caracteres especiales en el script de Hola en documento JSON de hello necesita toobe caracteres de escape y la posible causa problemas de depuración. práctica recomendada de Hello es toofollow paso #4.
   > 
   > 
5. Crear una canalización con hello HDInsightHive actividad. procesos de actividad Hello/transformaciones datos Hola.

    ```JSON   
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
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. Implementar la canalización de Hola. Consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md) para obtener más información. 
7. Supervisar la canalización de hello mediante la supervisión de la factoría de datos de Hola y vistas de administración. Consulte el artículo [Supervisión y administración de las canalizaciones de Factoría de datos](data-factory-monitor-manage-pipelines.md) para obtener más información. 

## <a name="specifying-parameters-for-a-hive-script"></a>Especificación de parámetros para un script de Hive
En este ejemplo, los registros de juegos se introducen diariamente en Azure Blob Storage y se almacenan en una carpeta dividida con fecha y hora. Desea script de Hive tooparameterize hello y pasar la ubicación de la carpeta de entrada de hello dinámicamente en tiempo de ejecución y también generar salida de hello particionado con la fecha y hora.

toouse parámetros de script de Hive, realice Hola después

* Definir los parámetros de hello en **define**.

    ```JSON  
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
* Hola Script de Hive, consulte toohello parámetro con **${hiveconf: ParameterName}**. 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a>Otras referencias
* [Actividad de Pig](data-factory-pig-activity.md)
* [Actividad MapReduce](data-factory-map-reduce.md)
* [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts de R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

