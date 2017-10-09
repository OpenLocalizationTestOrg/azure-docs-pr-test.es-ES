---
title: aaaMove datos de DB2 mediante el uso de Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde un DB2 local de base de datos mediante el uso de la actividad de copia de factoría de datos de Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Movimiento de datos de DB2 mediante la actividad de copia de Azure Data Factory
Este artículo describe cómo puede usar actividad de copia de datos de Data Factory de Azure toocopy desde un almacén de datos local tooa de base de datos de DB2. Puede copiar el almacén de datos de tooany que aparece como un receptor admitido en hello [las actividades de movimiento de datos de Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artículo. En este tema se basa en el artículo de factoría de datos de hello, que presenta una visión general de movimiento de datos mediante la actividad de copia y se incluyen combinaciones de almacén de datos de Hola admitida. 

Factoría de datos admite actualmente solo mover datos desde un tooa de base de datos de DB2 [almacén de datos del receptor compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Mover los datos de otros datos almacena tooa DB2 no se admite la base de datos.

## <a name="prerequisites"></a>Requisitos previos
Factoría de datos admite la base de datos DB2 de conexión tooan local mediante hello [puerta de enlace de administración de datos](data-factory-data-management-gateway.md). Para instrucciones paso a paso tooset los datos de la puerta de enlace de hello canalización toomove los datos, consulte hello [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo.

Una puerta de enlace es necesaria incluso aunque hello DB2 alojada en VM de IaaS de Azure. Puede instalar la puerta de enlace de hello en hello mismo IaaS VM como almacén de datos de Hola. Si la puerta de enlace de hello puede conectarse toohello base de datos, puede instalar puerta de enlace de hello en una máquina virtual diferente.

puerta de enlace de administración de datos de Hello proporciona un controlador DB2 integrado, por lo que no necesita toomanually instalar una datos toocopy del controlador de DB2.

> [!NOTE]
> Para obtener sugerencias sobre cómo solucionar problemas de la puerta de enlace y de conexión, vea hello [solucionar problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artículo.


## <a name="supported-versions"></a>Versiones compatibles
Conector de Hello DB2 de factoría de datos admite Hola siguientes plataformas IBM DB2 y las versiones con el Administrador de acceso de SQL de arquitectura de base de datos relacionales (DRDA) distribuidas versiones 9, 10 y 11:

* IBM DB2 para z/OS versión 11.1
* IBM DB2 para z/OS versión 10.1
* IBM DB2 para i (AS400) versión 7.2
* IBM DB2 para i (AS400) versión 7.1
* IBM DB2 para Linux, UNIX y (LUW) versión 11
* IBM DB2 para LUW versión 10.5
* IBM DB2 para LUW versión 10.1

> [!TIP]
> Si recibe el mensaje de error de saludo "hello paquete correspondiente tooan SQL instrucción solicitud de ejecución no se encontró. SQLSTATE = 51002 SQLCODE =-805, "motivo de hello no es se crea un paquete es necesario para el usuario normal de hello en hello SO. tooresolve este problema, siga estas instrucciones para el tipo de servidor DB2:
> - DB2 para i (AS400): permiten a un usuario avanzado Crear colección de hello para el usuario normal de hello antes de ejecutar la actividad de copia. colección de hello toocreate, use Hola comando:`create collection <username>`
> - DB2 para z/OS o LUW: utilice una cuenta con privilegios elevados: un usuario avanzado o administrador que tenga entidades de paquete y se ENLAZA, BINDADD, conceda permisos de tooPUBLIC EXECUTE: copia de hello toorun una vez. paquete necesario Hola se crea automáticamente durante la copia de Hola. A continuación, puede cambiar usuario normal toohello atrás para las ejecuciones de copia posteriores.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con datos de toomove de actividad de copia de un almacén de datos de DB2 local mediante distintas herramientas y API: 

- toocreate de manera más fácil de Hello una canalización es toouse Hola Asistente para copiar de factoría de datos de Azure. Para ver un tutorial rápido sobre cómo crear una canalización mediante Hola Asistente para copiar, vea hello [Tutorial: crear una canalización mediante Hola Asistente para copiar](data-factory-copy-data-wizard-tutorial.md). 
- También puede usar herramientas toocreate una canalización, incluidos Hola portal de Azure, Visual Studio, Azure PowerShell, una plantilla de Azure Resource Manager, Hola API de .NET y Hola API de REST. Para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia, consulte hello [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear la factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink de servicios vinculados.
2. Creación de conjuntos de datos toorepresent entrada y salida de datos para la operación de copia de Hola. 
3. Cree una canalización con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando usas Hola Asistente para copiar, definiciones de JSON para los servicios de la factoría de datos vinculado de Hola, conjuntos de datos y entidades de canalización se crean automáticamente para usted. Cuando usa herramientas o las API (excepto Hola API. NET), defina las entidades de hello factoría de datos con formato JSON de Hola. Hola [ejemplo de JSON: copiar los datos de DB2 tooAzure almacenamiento de blobs](#json-example-copy-data-from-db2-to-azure-blob) muestra las definiciones de JSON de Hola para hello las entidades de la factoría de datos que son toocopy usa datos de un almacén de datos de DB2 local.

Hola las secciones siguientes proporciona detalles sobre Hola propiedades JSON que son utilizados toodefine Hola factoría de datos entidades que son el almacén de datos específico tooa DB2.

## <a name="db2-linked-service-properties"></a>Propiedades del servicio vinculado de DB2
Hello en la tabla siguiente enumera propiedades JSON de Hola que son tooa específico del servicio vinculado DB2.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| **type** |Esta propiedad debe establecerse demasiado**OnPremisesDB2**. |Sí |
| **server** |nombre de saludo del servidor de hello DB2. |Sí |
| **database** |nombre de Hola de base de datos de DB2 Hola. |Sí |
| **schema** |nombre de Hello del esquema de hello en la base de datos de DB2 Hola. Esta propiedad distingue mayúsculas de minúsculas. |No |
| **authenticationType** |tipo de Hola de autenticación que es la base de datos de uso tooconnect toohello DB2. Hola los valores posibles son: anónima, básica y Windows. |Sí |
| **username** |nombre de Hello para la cuenta de usuario de hello si utiliza la autenticación básica o de Windows. |No |
| **password** |contraseña de Hello para la cuenta de usuario de Hola. |No |
| **gatewayName** |nombre de Hola de puerta de enlace de Hola Hola servicio Data Factory debe usar base de datos de DB2 de tooconnect toohello local. |Sí |

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista de secciones de Hola y propiedades que están disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones, como **estructura**, **disponibilidad**, hello y **directiva** para un conjunto de datos JSON son similares para todos los tipos de conjunto de datos (SQL Azure, almacenamiento de blobs de Azure, tabla de Azure almacenamiento y así sucesivamente).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola **typeProperties** sección para un conjunto de datos de tipo **RelationalTable**, que incluye el conjunto de datos de DB2 hello, tiene Hola después de propiedad:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| **tableName** |Hola nombre de tabla de hello en la instancia de base de datos de DB2 de Hola que Hola servicio vinculado hace referencia a. Esta propiedad distingue mayúsculas de minúsculas. |No (si hello **consulta** propiedad de una actividad de copia de tipo **RelationalSource** se especifica) |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista de secciones de Hola y propiedades que están disponibles para la definición de actividades de copia, consulte hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades de la actividad de copia, como **nombre**, **descripción**, tabla de **entradas**, tabla de **salidas** y **directiva**, están disponibles para todos los tipos de actividades. Hola propiedades que están disponibles en hello **typeProperties** sección de la actividad de Hola para cada tipo de actividad. Para la actividad de copia, propiedades de hello varían en función de tipos de hello receptores y orígenes de datos.

Para la actividad de copia, cuando el origen de hello es de tipo **RelationalSource** (que incluye DB2), Hola propiedades siguientes está disponible en hello **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| **consulta** |Usar datos de hello consulta personalizada tooread Hola. |Cadena de consulta SQL. Por ejemplo: `"query": "select * from "MySchema"."MyTable""` |No (si hello **tableName** se especifica la propiedad de un conjunto de datos) |

> [!NOTE]
> Los nombres de esquema y tabla distinguen mayúsculas de minúsculas. En la instrucción de consulta de hello, incluya los nombres de propiedad mediante el uso de "" (comillas dobles). Por ejemplo:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>Ejemplo de JSON: copiar los datos de DB2 tooAzure almacenamiento de blobs
Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). ejemplo de Hola muestra cómo la base de datos de toocopy de DB2 datos tooBlob almacenamiento. Sin embargo, se pueden copiar datos demasiado[todos los datos admitidos almacenan el tipo de receptor](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante el uso de la actividad de copia de factoría de datos de Azure.

ejemplo de Hola tiene Hola siguiendo las entidades de la factoría de datos:

- Un servicio vinculado DB2 de tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).
- Un servicio vinculado de Azure Blob Storage de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
- Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).
- Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
- A [canalización](data-factory-create-pipelines.md) con una actividad de copia que utiliza hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) propiedades

ejemplo Hello copia datos de un resultado de consulta en un tooan de base de datos DB2 blob de Azure cada hora. propiedades JSON de Hola que se usan en el ejemplo de Hola se describen en las secciones de Hola que siguen a las definiciones de entidad de Hola.

Como primer paso, instale y configure una puerta de enlace de datos. Las instrucciones están en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.

**Servicio vinculado DB2**

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

**Servicio vinculado de almacenamiento de blobs de Azure**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Conjunto de datos de entrada de DB2**

ejemplo de Hola se da por supuesto que ha creado una tabla de DB2 con el nombre "MyTable" que tiene una columna denominada "timestamp" para los datos de serie temporal de Hola.

Hola **externo** propiedad se establece demasiado "true". Esta configuración indica el servicio de factoría de datos de Hola que este conjunto de datos es externo toohello factoría de datos y no se crea una actividad de factoría de datos de Hola. Tenga en cuenta que hello **tipo** propiedad se establece demasiado**RelationalTable**.


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

**Conjunto de datos de salida de blob de Azure**

Los datos se escriben cada hora de tooa nuevo blob mediante configuración hello **frecuencia** propiedad demasiado hello y "Hora" **intervalo** too1 de propiedad. Hola **folderPath** propiedad de blob de Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y hora de Hola Hola hora de inicio.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Canalización para la actividad de copia de hello**

canalización de Hello contiene una actividad de copia que se configura toouse especifica los conjuntos de datos de entrada y salida y que es toorun programada cada hora. Hola definición JSON de la canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** hello y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos de Hola de tabla de Hola "Orders".

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>Asignación de tipos para DB2
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática del tipo de toosink de tipo de origen mediante Hola enfoque de dos pasos:

1. Convertir de un tipo de origen nativo tipo tooa .NET
2. Convertir de un tipo de receptor nativo de tooa de tipo .NET

Hello asignaciones siguientes se utilizan cuando copia actividad convierte datos de Hola de un tipo de .NET de DB2 tipo tooa:

| Tipo de base de datos DB2 | Tipo .NET Framework |
| --- | --- |
| SmallInt |Int16 |
| Entero |Int32 |
| BigInt |Int64 |
| Real |Single |
| Doble |Doble |
| Float |Doble |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Numeric |Decimal |
| Date |DateTime |
| Hora |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |
| VarChar |String |
| LongVarChar |String |
| DB2DynArray |String |
| Binary |Byte[] |
| VarBinary |Byte[] |
| LongVarBinary |Byte[] |
| Graphic |String |
| VarGraphic |String |
| LongVarGraphic |String |
| Clob |String |
| Blob |Byte[] |
| DbClob |String |
| SmallInt |Int16 |
| Entero |Int32 |
| BigInt |Int64 |
| Real |Single |
| Doble |Doble |
| Float |Doble |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Numeric |Decimal |
| Date |DateTime |
| Hora |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn toomap columnas en hello toocolumns de conjunto de datos de origen en el conjunto de datos de receptor de hello, vea [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Lecturas repetibles desde orígenes relacionales
Al copiar datos desde un almacén de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar reintento hello **directiva** propiedad para un toorerun un segmento cuando se produce un error de conjunto de datos. Asegúrese de que Hola mismo no se leen los datos importar cómo segmento de hello muchas veces se vuelva a ejecutar y, a continuación, independientemente de cómo volver a ejecutar el segmento de Hola. Para más información, consulte [Lecturas repetibles desde orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Obtenga información acerca de los factores claves que afectan al rendimiento de Hola de actividad de copia y maneras de rendimiento toooptimize en hello [copia actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).
