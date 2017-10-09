---
title: "grandes cantidades de datos en el almacén de Data Lake mediante métodos sin conexión de aaaUpload | Documentos de Microsoft"
description: "TooData Lake almacén de blobs de hello uso AdlCopy datos de toocopy la herramienta desde el almacenamiento de Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Utilizar el servicio de importación y exportación de Azure de hello para la copia sin conexión del almacén de datos tooData Lake
En este artículo, aprenderá cómo establece datos enorme toocopy (> 200 GB) en un almacén de Azure Data Lake mediante el uso de métodos de copia sin conexión, como hello [servicio de importación y exportación de Azure](../storage/common/storage-import-export-service.md). En concreto, archivo hello utilizado como ejemplo en este artículo es 339,420,860,416 bytes, o aproximadamente 319 GB en el disco. Llamaremos a este archivo "319GB.tsv".

Hola servicio de importación y exportación de Azure le ayuda a tootransfer grandes cantidades de datos más segura tooAzure almacenamiento de blobs de disco duro de envío unidades tooan centro de datos de Azure.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* Una **cuenta de almacenamiento de Azure**.
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Preparar los datos de Hola
Antes de usar el servicio de importación/exportación de hello, transfiere salto Hola datos archivo toobe **en copias que son menos de 200 GB** de tamaño. herramienta de importación de Hello no funciona con archivos de más de 200 GB. En este tutorial, dividiremos archivo hello en fragmentos de 100 GB. Puede hacerlo si utiliza [Cygwin](https://cygwin.com/install.html). Cygwin admite comandos de Linux. En este caso, utilice Hola siguiente comando:

    split -b 100m 319GB.tsv

operación de división de Hello crea archivos con hello después de nombres.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Preparación de los discos con datos
Siga las instrucciones de hello en [mediante el servicio de importación y exportación de Azure de hello](../storage/common/storage-import-export-service.md) (en hello **preparar las unidades de disco** sección) tooprepare las unidades de disco duras. Aquí es hello secuencia general:

1. Adquiera un disco duro que cumpla Hola requisito toobe destinada Hola servicio de importación y exportación de Azure.
2. Identificar una cuenta de almacenamiento de Azure donde se copiarán los datos de hello una vez enviada toohello centro de datos de Azure.
3. Hola de uso [herramienta de importación y exportación de Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), una utilidad de línea de comandos. Este es un fragmento de código de ejemplo que muestra cómo toouse Hola herramienta.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Vea [mediante el servicio de importación y exportación de Azure de hello](../storage/common/storage-import-export-service.md) para varios fragmentos de código de ejemplo.
4. Hello comando anterior crea un diario de ubicación de archivo en hello especificada. Utilice este toocreate de archivo diario un trabajo de importación de hello [portal de Azure clásico](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Crear un trabajo de importación
Ahora puede crear un trabajo de importación mediante instrucciones de hello en [mediante el servicio de importación y exportación de Azure de hello](../storage/common/storage-import-export-service.md) (en hello **crear trabajo de importación de hello** sección). Para este trabajo de importación, con los otros detalles, proporcionar también archivo diario de hello creado durante la preparación de unidades de disco de Hola.

## <a name="physically-ship-hello-disks"></a>Enviar físicamente los discos de Hola
Ahora puede distribuir físicamente Hola discos tooan centro de datos de Azure. No existe, se copian datos de hello en blobs de almacenamiento de Azure toohello que proporcionó al crear un trabajo de importación de Hola. Además, al crear un trabajo de hello, si ha elegido hello tooprovide más adelante, la información de seguimiento puede ahora volver Hola de trabajo y actualización de la importación de tooyour número de seguimiento.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Copiar los datos de almacén de almacenamiento de Azure BLOB tooAzure Data Lake
Después de estado de Hola de hello trabajo de importación muestra que se completan, puede comprobar si hay datos de hello en blobs de almacenamiento de Azure de Hola que se había especificado. A continuación, puede utilizar una variedad de toomove de métodos que los datos de hello blobs tooAzure almacén de Data Lake. Para todos los hello las opciones disponibles para cargar los datos, consulte [introducción de datos en el almacén de Data Lake](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

En esta sección, se proporcionan con definiciones de hello JSON que puede usar toocreate una canalización del generador de datos de Azure para copiar datos. Puede utilizar estas definiciones de JSON de hello [portal de Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Servicio vinculado de origen (blob de Azure Storage)
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a>Servicio vinculado de destino (Azure Data Lake Store)
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a>Conjunto de datos de entrada
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a>Conjunto de datos de salida
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a>Canalización (actividad de copia)
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
Para obtener más información, consulte [mover datos desde el almacenamiento de Azure blob almacén de Data Lake tooAzure con Data Factory de Azure](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Reconstruir los archivos de datos de hello en el almacén de Azure Data Lake
Comenzamos con un archivo que 319 GB e interrumpió hacia abajo de en archivos de tamaño más pequeño para que puede transferirse mediante el servicio de importación y exportación de Hola. Ahora que los datos de hello están en el almacén de Data Lake de Azure, se puede reconstruir tamaño original del archivo tooits de Hola. Puede usar Hola después Azure PowerShell cmldts toodo por lo que.

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a>Pasos siguientes
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
