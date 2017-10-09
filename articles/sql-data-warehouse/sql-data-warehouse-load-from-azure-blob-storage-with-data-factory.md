---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "almacenamiento de blobs de datos de aaaLoad de Azure en almacenamiento de datos de SQL Azure (factoría de datos de Azure) | Documentos de Microsoft"
description: "Obtenga información acerca de los datos de tooload con Data Factory de Azure"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a>Carga de datos del Almacenamiento de blobs de Azure en Almacenamiento de datos SQL de Azure (Data Factory de Azure)
> [!div class="op_single_selector"]
> * [Factoría de datos](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 Este tutorial muestra cómo toocreate una canalización de datos de Data Factory de Azure toomove desde tooSQL almacenamiento de datos de Blob de almacenamiento de Azure. Con hello pasos hará lo siguiente:

* Configurar datos de ejemplo en un blob de Almacenamiento de Azure.
* Conectar recursos tooAzure factoría de datos.
* Crear una canalización de datos de toomove de Blobs de almacenamiento tooSQL almacenamiento de datos.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Antes de empezar
toofamiliarize usted mismo con Data Factory de Azure, consulte [tooAzure Introducción factoría de datos][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Creación o identificación de recursos
Antes de iniciar este tutorial, necesita hello toohave recursos siguientes.

* **Blob de almacenamiento de Azure**: este tutorial utiliza el Blob de almacenamiento de Azure como origen de datos de hello de la canalización de factoría de datos de Azure de hello y, por lo que necesita datos de ejemplo de toohave una disponible toostore Hola. Si no tiene ninguno todavía, obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento][Create a storage account].
* **Almacenamiento de datos SQL**: este tutorial mueve Hola los datos de Blob de almacenamiento de Azure demasiado almacenamiento de datos SQL de modo que necesitan un almacenamiento de datos en línea que se ha cargado con datos de ejemplo AdventureWorksDW hello toohave. Si no dispone de un almacén de datos, obtenga información acerca de cómo demasiado[aprovisionar una][Create a SQL Data Warehouse]. Si tiene un almacén de datos pero no lo aprovisiona con datos de ejemplo de Hola, puede [cargarlos manualmente][Load sample data into SQL Data Warehouse].
* **Factoría de datos de Azure**: Data Factory de Azure se completará la carga real de Hola y por lo que deberá toohave uno que puede usar la canalización de movimiento de datos de toobuild Hola. Si no tiene ninguno todavía, obtenga información acerca de cómo toocreate uno en el paso 1 de [Introducción a Data Factory de Azure (Editor de generador de datos)][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: necesita datos de ejemplo de Hola de AZCopy toocopy de su tooyour de cliente local Blob de almacenamiento de Azure. Para obtener instrucciones de instalación, vea hello [AZCopy documentación][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Paso 1: Copiar datos de ejemplo tooAzure Blob de almacenamiento
Una vez que tenga todas las fichas de hello listo, son tooyour de datos de ejemplo listo toocopy Blob de almacenamiento de Azure.

1. [Descargue los datos de ejemplo][Download sample data]. Estos datos agregarán otro tres años de datos de ventas tooyour datos de ejemplo AdventureWorksDW.
2. Utilice este comando de AZCopy toocopy hello tres años de tooyour de datos Blob de almacenamiento de Azure.

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a>Paso 2: Conectar recursos tooAzure factoría de datos
Ahora que los datos de hello están en su lugar podemos crear datos de saludo de hello Data Factory de Azure canalización toomove desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL.

tooget iniciado, abra hello [portal de Azure] [ Azure portal] y seleccione su factoría de datos en el menú izquierdo Hola.

### <a name="step-21-create-linked-service"></a>Paso 2.1: Creación del servicio vinculado
Vincular su cuenta de almacenamiento de Azure y la factoría de datos de almacenamiento de datos de SQL tooyour.  

1. En primer lugar, comenzar el proceso de registro de hello haciendo clic en la sección de hello 'Servicios vinculados' de la factoría de datos y, a continuación, haga clic en 'Nuevo almacén de datos'. Elija un nombre tooregister su almacenamiento de azure en, seleccione el almacenamiento de Azure como su tipo y, a continuación, escriba el nombre de cuenta y la clave de cuenta.
2. tooregister almacenamiento de datos SQL vaya toohello 'Autor e implementar' sección, seleccione 'Nuevo almacén de datos' y, a continuación, 'Almacenamiento de datos de SQL de Azure'. Copie y pegue en esta plantilla y, a continuación, rellene su información específica.

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-hello-dataset"></a>Paso 2.2: Definir el conjunto de datos de Hola
Después de crear Hola servicios vinculados, tenemos conjuntos de datos de toodefine Hola.  Aquí, esto significa definir Hola estructura de datos de Hola que se ha movido desde el almacenamiento de datos de tooyour de almacenamiento.  Puede leer más sobre creación.

1. Iniciar este proceso, vaya toohello sección 'Crear e implementar' de la factoría de datos.
2. Haga clic en 'Nuevo conjunto de datos' y, a continuación, 'Almacenamiento de blobs de Azure' toolink su factoría de datos de tooyour de almacenamiento.  Puede usar Hola por debajo de la secuencia de comandos toodefine los datos en el almacenamiento de blobs de Azure:

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
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


1. Ahora definiremos también nuestro conjunto de datos para Almacenamiento de datos SQL.  Comenzamos en hello igual, haciendo clic en 'Nuevo conjunto de datos' y, a continuación, 'Almacenamiento de datos de SQL de Azure'.

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a>Paso 3: Creación y ejecución de la canalización
Por último, haremos canalización Hola de instalación y ejecución de factoría de datos de Azure.  Se trata de una operación de Hola que se completará el movimiento de datos reales de Hola.  Puede encontrar una vista completa de las operaciones de Hola que puede completar con el almacenamiento de datos de SQL y Data Factory de Azure [aquí][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

En sección 'Crear e implementar' de hello ahora haga clic en 'Más comandos' y, a continuación, 'Nueva canalización'.  Después de crear la canalización de hello, puede usar hello debajo de almacenamiento de datos de código tootransfer Hola datos tooyour:

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más, inicio, consulte:

* [Ruta de aprendizaje para Azure Data Factory][Azure Data Factory learning path].
* [Conector de Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector]. Se trata de un tema de referencia de núcleo de hello para el uso de Data Factory de Azure con almacenamiento de datos de SQL Azure.

En estos temas se proporciona información detallada sobre Data Factory de Azure. Debaten HDinsight o base de datos de SQL Azure, pero también aplica la información de hello tooAzure almacenamiento de datos SQL.

* [Tutorial: Introducción a Data Factory de Azure] [ Tutorial: Get started with Azure Data Factory] se trata de tutorial de núcleo de hello para el procesamiento de datos con Data Factory de Azure. En este tutorial se compile su primera canalización que usa tootransform de HDInsight y analizar registros web mensualmente. Tenga en cuenta que no hay ninguna actividad de copia en este tutorial.
* [Tutorial: Copiar los datos de Blob de almacenamiento de Azure tooAzure base de datos SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. En este tutorial, creará una canalización de datos de Data Factory de Azure toocopy de Blob de almacenamiento de Azure tooAzure base de datos SQL.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
