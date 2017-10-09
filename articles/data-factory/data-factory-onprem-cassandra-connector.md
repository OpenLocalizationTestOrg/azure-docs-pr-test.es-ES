---
title: datos de aaaMove de Casandra con el generador de datos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de un Casandra local de base de datos con el generador de datos de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Movimiento de datos desde una base de datos de Cassandra local con Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de Casandra local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos desde un almacén de datos local Casandra datos almacén tooany admitida receptor. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos desde una datos Casandra, pero no para mover los datos de otro almacén de datos de datos almacenes tooa Casandra. 

## <a name="supported-versions"></a>Versiones compatibles
Conector de Hello Casandra admite Hola después de las versiones de Casandra: 2.X.

## <a name="prerequisites"></a>Requisitos previos
Para hello Data Factory de Azure servicio toobe tooconnect pueda tooyour local Casandra base de datos, debe instalar una puerta de enlace de administración de datos en hello mismo esa base de datos de Hola de hosts de máquina o en un tooavoid máquina independiente que compiten por los recursos con hello base de datos. Data Management Gateway es un componente que se conecta a servicios de toocloud de orígenes de datos locales de forma segura y administrada. Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway. Vea [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello una canalización de datos toomove datos.

Debe usar hello tooconnect tooa Casandra la base de datos, incluso si la base de datos de Hola se hospeda en la nube de hello, por ejemplo, en una máquina virtual de IaaS de Azure. Y puede tener puerta de enlace de hello en Hola misma VM esa base de datos de Hola de hosts o en una máquina virtual independiente siempre y cuando la puerta de enlace de Hola se pueden conectar toohello base de datos.  

Cuando se instala la puerta de enlace de hello, instala automáticamente una base de datos de Microsoft Casandra ODBC driver utiliza tooconnect tooCassandra. Por lo tanto, no es necesario toomanually instalar ningún controlador en la máquina de puerta de enlace de hello cuando se copian datos de base de datos de hello Casandra. 

> [!NOTE]
> Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API. 

- toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido. 
- También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos local Casandra, consulte [ejemplo de JSON: copiar los datos de Blob del Casandra tooAzure](#json-example-copy-data-from-cassandra-to-azure-blob) sección de este artículo. 

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son el almacén de datos de uso toodefine factoría de datos entidades tooa específico Casandra:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooCassandra vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **OnPremisesCassandra** |Sí |
| host |Una o varias direcciones IP o nombres de host de los servidores de Cassandra.<br/><br/>Especifique una lista separada por comas de direcciones IP o servidores de tooall de tooconnect de nombres de host al mismo tiempo. |Sí |
| puerto |Hola el puerto TCP que Hola server Casandra utiliza toolisten para las conexiones de cliente. |No. El valor predeterminado es 9042. |
| authenticationType |Básica o anónima |Sí |
| nombre de usuario |Especifique el nombre de usuario para la cuenta de usuario de Hola. |Sí, si authenticationType se establece tooBasic. |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola. |Sí, si authenticationType se establece tooBasic. |
| gatewayName |nombre de Hola de puerta de enlace de Hola que es la base de datos de uso tooconnect toohello local Casandra. |Sí |
| encryptedCredential |Credencial cifrada por la puerta de enlace de Hola. |No |

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **CassandraTable** tiene Hola propiedades siguientes

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| keyspace |Nombre de keyspace de Hola o esquema de base de datos de Casandra. |Sí (si no hay definida ninguna **consulta** para **CassandraSource**). |
| tableName |Nombre de tabla de hello en la base de datos de Casandra. |Sí (si no hay definida ninguna **consulta** para **CassandraSource**). |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Cuando el origen es del tipo **CassandraSource**, Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Consulta SQL-92 o consulta CQL. Vea la [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)(referencia de CQL). <br/><br/>Al usar una consulta SQL, especifique **keyspace name.table nombre** tabla de hello toorepresent desea tooquery. |No (si tableName y el espacio de claves del conjunto de datos están definidos). |
| consistencyLevel |el nivel de coherencia de Hello especifica cuántas réplicas debe responder tooa solicitud de lectura antes de devolver la aplicación de cliente de toohello de datos. Comprobaciones de Casandra Hola número de réplicas especificado para la solicitud de lectura de hello toosatisfy de datos. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Para más información, consulte [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configuración de la coherencia de datos). |No. El valor predeterminado es ONE. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de Casandra tooAzure Blob
Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestra cómo la base de datos toocopy de un Casandra local datos tooan almacenamiento de blobs de Azure. Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

> [!IMPORTANT]
> Este ejemplo proporciona fragmentos JSON. No incluye instrucciones paso a paso para la creación de factoría de datos de Hola. Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

* Un servicio vinculado de tipo [OnPremisesCassandra](#linked-service-properties).
* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [CassandraTable](#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que use [CassandraSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Servicio vinculado de Cassandra**

Este ejemplo utiliza hello **Casandra** servicio vinculado. Vea [Casandra servicio vinculado](#linked-service-properties) sección de propiedades de hello admitidos por este servicio vinculado.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Servicio vinculado de Almacenamiento de Azure:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

**Conjunto de datos de entrada de Cassandra**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

Establecer **externo** demasiado**true** informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Actividad de copia en una canalización con el origen de Cassandra y el receptor de blob:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**CassandraSource** y **receptor** tipo está establecido demasiado**BlobSink**.

Vea [propiedades de tipo RelationalSource](#copy-activity-properties) para lista de Hola de propiedades admitidas por hello RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
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
        }
        ]    
    }
}
```

### <a name="type-mapping-for-cassandra"></a>Asignación de tipos de Cassandra
| Tipo de Cassandra | Tipo basado en .NET |
| --- | --- |
| ASCII |String |
| BIGINT |Int64 |
| BLOB |Byte[] |
| BOOLEAN |BOOLEAN |
| DECIMAL |DECIMAL |
| DOUBLE |DOUBLE |
| FLOAT |Single |
| INET |String |
| INT |Int32 |
| TEXT |String |
| TIMESTAMP |DateTime |
| TIMEUUID |Guid |
| UUID |Guid |
| VARCHAR |String |
| VARINT |Decimal |

> [!NOTE]
> Para la colección de tipos (mapa, conjunto, lista, etc.), consulte demasiado[trabajar con tipos de colección Casandra usando tabla virtual](#work-with-collections-using-virtual-table) sección.
>
> No se admiten tipos definidos por el usuario.
>
> longitud de Hola de longitudes de columna binaria y la columna de cadena no puede ser mayor que 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Uso de colecciones con tablas virtuales
Factoría de datos de Azure usa un integrados tooconnect tooand copia datos del controlador ODBC de la base de datos de Casandra. Para los tipos de colección incluida mapa, conjunto y una lista, controlador de hello Normalizar datos hello en tablas virtuales correspondientes. En concreto, si una tabla contiene las columnas de la colección, el controlador de hello genera hello las tablas virtuales siguientes:

* A **tabla base**, que contiene Hola los mismos datos como tabla real de hello excepto para las columnas del conjunto de Hola. tabla de base de Hello usa Hola mismo nombre como tabla real de Hola que representa.
* A **tabla virtual** para cada columna de la colección, que expande datos Hola anidado. tablas virtuales Hola que representan las colecciones se le asignó hello nombre de tabla real de hello, un separador de "*vt*" y el nombre de Hola de columna Hola.

Tablas virtuales hacen referencia datos toohello en la tabla real Hola, habilitación Hola controlador tooaccess Hola datos sin normalizar. Consulte la sección de ejemplo para más información. Puede tener acceso a contenido de Hola de colecciones de Casandra por consultar y combinar tablas virtuales Hola.

Puede usar hello [Asistente para copiar](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vista Hola lista de tablas de base de datos de Casandra incluye tablas virtuales hello y obtener una vista previa de los datos de saludo dentro. También puede crear una consulta en el Asistente para copiar Hola y validar el resultado de hello toosee.

### <a name="example"></a>Ejemplo
Por ejemplo, hello siguiente "ExampleTable" es una tabla de base de datos de Casandra que contiene una columna de clave de entero principal denominada "pk_int", una columna de texto con el nombre de valor, una columna de la lista, una columna de asignación y una columna del conjunto (denominado "StringSet").

| pk_int | Valor | Enumerar | Map | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"valor de ejemplo 1" |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"valor de ejemplo 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

controlador de Hello generaría varios toorepresent tablas virtuales esta misma tabla. Hello las columnas de clave externa en las tablas virtuales Hola hacen referencia a columnas de clave principal de hello en la tabla real de hello e indican qué real tabla fila Hola tabla virtual fila corresponde a.

la primera tabla virtual de Hello es la tabla de base de hello denominada "ExampleTable" se muestra en hello en la tabla siguiente. tabla de base de Hello contiene Hola mismos datos como tabla de base de datos original de hello excepto para las colecciones de hello, que se omite en esta tabla y se expanden en otras tablas virtuales.

| pk_int | Valor |
| --- | --- |
| 1 |"valor de ejemplo 1" |
| 3 |"valor de ejemplo 3" |

Hello en las tablas siguientes muestran tablas virtuales Hola que renormalize datos Hola de las columnas de lista y mapa, StringSet Hola. columnas de Hello con nombres que terminan con "_index" o "_clave" indican la posición de Hola de datos de hello dentro de la lista original de Hola o mapa. columnas de Hello con nombres que terminan con "_value" contienen datos de hello expandido de colección de Hola.

#### <a name="table-exampletablevtlist"></a>Tabla “ExampleTable_vt_List”:
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Tabla “ExampleTable_vt_Map”:
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |Una  |
| 1 |S2 |b |
| 3 |S1 |t |

#### <a name="table-exampletablevtstringset"></a>Tabla “ExampleTable_vt_StringSet”:
| pk_int | StringSet_value |
| --- | --- |
| 1 |Una  |
| 1 |b |
| 1 |C |
| 3 |Una  |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
