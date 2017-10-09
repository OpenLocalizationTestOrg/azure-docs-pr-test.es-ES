---
title: aaaMove datos de PostgreSQL mediante Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de base de datos PostgreSQL mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a>Movimiento de datos de PostgreSQL mediante Factoría de datos de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de PostgreSQL local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos desde un almacén de datos local PostgreSQL datos almacén tooany admitida receptor. Para obtener una lista de almacenes de datos que se admiten como receptores por actividad de copia de hello, consulte [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Factoría de datos actualmente permite mover datos desde un PostgreSQL base de datos de almacenes de datos tooother, pero no para mover los datos de otros datos de los almacenes de datos de PostgreSQL tooan. 

## <a name="prerequisites"></a>requisitos previos

Servicio de factoría de datos admite conexión orígenes de PostgreSQL de tooon local mediante Hola Data Management Gateway. Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.

Puerta de enlace es necesario incluso si la base de datos de PostgreSQL Hola se hospeda en una máquina virtual de IaaS de Azure. Puerta de enlace se puede instalar en hello mismo IaaS VM como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola pueden conectar toohello base de datos.

> [!NOTE]
> Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.

## <a name="supported-versions-and-installation"></a>Versiones compatibles e instalación
Para Data Management Gateway tooconnect toohello base de datos PostgreSQL, instale hello [Ngpsql el proveedor de datos de PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 o por encima de Hola mismo sistema como Hola Data Management Gateway. Se admite la versión 7.4 o posterior de PostgreSQL.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos desde un almacén de datos de PostgreSQL local mediante el uso de diferentes herramientas o API. 

- toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido. 
- También puede usar Hola después herramientas toocreate una canalización: 
    - Azure Portal
    - Visual Studio
    - Azure PowerShell
    - Plantilla del Administrador de recursos de Azure
    - API de .NET
    - API de REST

     Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de PostgreSQL local, vea [ejemplo de JSON: copiar los datos de PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de propiedades JSON de almacén de datos de PostgreSQL de toodefine usado factoría de datos entidades tooa específica:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooPostgreSQL vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **OnPremisesPostgreSql** |Sí |
| Servidor |Nombre del servidor de hello PostgreSQL. |Sí |
| database |Nombre de base de datos de PostgreSQL Hola. |Sí |
| schema |Nombre del esquema de hello en la base de datos de Hola. nombre del esquema Hola distingue mayúsculas de minúsculas. |No |
| authenticationType |Tipo de autenticación que utiliza la base de datos de PostgreSQL tooconnect toohello. Los valores posibles son: Anonymous, Basic y Windows. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación Basic o Windows. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de PostgreSQL local de tooconnect toohello. |Sí |

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de PostgreSQL) tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola Hola instancia de base de datos PostgreSQL que hace referencia el servicio vinculado. Hola tableName distingue mayúsculas de minúsculas. |No (si se especifica **query** de **RelationalSource**) |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Cuando el origen es del tipo **RelationalSource** (que incluye PostgreSQL), Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: "query": "select * from \"MySchema\".\"MyTable\"". |No (si se especifica **tableName** de **dataset**) |

> [!NOTE]
> Los nombres de esquema y tabla distinguen mayúsculas de minúsculas. Encerrarlas entre `""` (comillas dobles) en la consulta de Hola.  

**Ejemplo:**

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de PostgreSQL tooAzure Blob
Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestra cómo la base de datos toocopy de PostgreSQL datos tooAzure almacenamiento de blobs. Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.   

> [!IMPORTANT]
> Este ejemplo proporciona fragmentos JSON. No incluye instrucciones paso a paso para la creación de factoría de datos de Hola. Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

1. Un servicio vinculado de tipo [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de un resultado de consulta en el blob de tooa de base de datos de PostgreSQL cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

Como primer paso, configurar la puerta de enlace de administración de datos de Hola. instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.

**Servicio vinculado de PostgreSQL:**

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
**Servicio vinculado de almacenamiento de blobs de Azure:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
**Conjunto de datos de entrada de PostgreSQL**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en PostgreSQL y contiene una columna denominada "timestamp" para los datos de serie temporal.

Establecer `"external": true` informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

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

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Canalización con actividad de copia:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola de tabla de public.usstates de hello en la base de datos de PostgreSQL Hola.

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a>Asignación de tipos para PostgreSQL
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover datos tooPostgreSQL, hello asignaciones siguientes sirven de PostgreSQL tipo too.NET.

| Tipo de Base de datos de PostgreSQL | Alias de PostgresSQL | Tipo .NET Framework |
| --- | --- | --- |
| abstime | |Datetime | &nbsp;
| bigint |int8 |Int64 |
| bigserial |serial8 |Int64 |
| bit | |Byte[], String | &nbsp;
| bit variable [(n)] |varbit |Byte[], String |
| boolean |booleano |boolean |
| Box | |Byte[], String |&nbsp;
| bytea | |Byte[], String |&nbsp;
| character [ (n) ] |char [ (n) ] |String |
| character varying [ (n) ] |varchar [ (n) ] |String |
| cid | |String |&nbsp;
| cidr | |String |&nbsp;
| circle | |Byte[], String |&nbsp;
| fecha | |Datetime |&nbsp;
| daterange | |String |&nbsp;
| double precision |float8 |Doble |
| inet | |Byte[], String |&nbsp;
| intarry | |String |&nbsp;
| int4range | |String |&nbsp;
| int8range | |String |&nbsp;
| integer |int, int4 |Int32 |
| interval [ fields ] [ (p) ] | |TimeSpan |&nbsp;
| json | |String |&nbsp;
| jsonb | |Byte[] |&nbsp;
| line | |Byte[], String |&nbsp;
| lseg | |Byte[], String |&nbsp;
| macaddr | |Byte[], String |&nbsp;
| money | |Decimal |&nbsp;
| numeric [ (p, s) ] |decimal [ (p, s) ] |Decimal |
| numrange | |String |&nbsp;
| oid | |Int32 |&nbsp;
| path | |Byte[], String |&nbsp;
| pg_lsn | |Int64 |&nbsp;
| point | |Byte[], String |&nbsp;
| polygon | |Byte[], String |&nbsp;
| real |float4 |Single |
| smallint |int2 |Int16 |
| smallserial |serial2 |Int16 |
| serial |serial4 |Int32 |
| text | |String |&nbsp;

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
