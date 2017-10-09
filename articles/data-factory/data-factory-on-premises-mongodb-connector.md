---
title: "datos de aaaMove de MongoDB utilizando factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de MongoDB base de datos con el generador de datos de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Movimiento de datos de MongoDB mediante Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de MongoDB local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos desde un almacén de datos local MongoDB datos almacén tooany admitida receptor. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos de datos MongoDB, pero no para mover los datos de otro almacén de datos de MongoDB del tooan de almacenes de datos. 

## <a name="prerequisites"></a>Requisitos previos
Para hello Data Factory de Azure servicio toobe tooconnect pueda tooyour local MongoDB base de datos, debe instalar Hola de los componentes siguientes:

- Versiones admitidas de MongoDB: 2.4, 2.6, 3.0 y 3.2.
- Data Management Gateway en Hola misma máquina esa base de datos de Hola de hosts o en un tooavoid máquina independiente que compiten por los recursos con la base de datos de Hola. Data Management Gateway es un software que se conecta a servicios de toocloud de orígenes de datos locales de forma segura y administrada. Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway. Vea [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello una canalización de datos toomove datos.

    Cuando se instala la puerta de enlace de hello, instala automáticamente un tooMongoDB de tooconnect del controlador que se usa Microsoft MongoDB ODBC.

    > [!NOTE]
    > Debe toouse Hola puerta de enlace tooconnect tooMongoDB incluso si está hospedado en máquinas virtuales de IaaS de Azure. Si está tratando de instancia de tooan tooconnect de MongoDB hospedada en la nube, también puede instalar instancia de puerta de enlace de Hola Hola IaaS VM.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con actividad de copia que mueva los datos desde un almacén de datos MongoDB local mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de MongoDB local, vea [ejemplo de JSON: copiar los datos de MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son origen de tooMongoDB específicos de entidades de toodefine usado factoría de datos:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello tabla siguiente proporciona descripción para los elementos JSON específicos demasiado**OnPremisesMongoDB** servicio vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **OnPremisesMongoDb** |Sí |
| Servidor |IP dirección o nombre de host del servidor de MongoDB Hola. |Sí |
| puerto |El puerto TCP que Hola MongoDB server usa toolisten para las conexiones de cliente. |Valor predeterminado opcional: 27017 |
| authenticationType |Básica o anónima. |Sí |
| nombre de usuario |Tooaccess de cuenta de usuario MongoDB. |Sí (si se usa la autenticación básica). |
| Contraseña |Contraseña de usuario de Hola. |Sí (si se usa la autenticación básica). |
| authSource |Nombre de base de datos de MongoDB de Hola que quiere toouse toocheck sus credenciales de autenticación. |Opcional (si se usa la autenticación básica). valor predeterminado: utiliza la cuenta de administrador de Hola y base de datos de hello especificada mediante la propiedad databaseName. |
| databaseName |Nombre de base de datos de MongoDB de Hola que desea tooaccess. |Sí |
| gatewayName |Nombre de puerta de enlace de Hola que tiene acceso a almacén de datos de Hola. |Sí |
| encryptedCredential |Credencial cifrada por la puerta de enlace. |Opcional |

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **MongoDbCollection** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| collectionName |Nombre de colección de hello en la base de datos de MongoDB. |Sí |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Propiedades disponibles en hello **typeProperties** sección de actividad de hello en hello varían con cada tipo de actividad en otra parte. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Cuando el origen de hello es del tipo **MongoDbSource** Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL-92. Por ejemplo: select * from MyTable. |No (si se especifica **collectionName** de **dataset**) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de MongoDB tooAzure Blob
Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestra cómo toocopy datos desde un tooan de MongoDB local almacenamiento de blobs de Azure. Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

1. Un servicio vinculado de tipo [OnPremisesMongoDB](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [MongoDbCollection](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [MongoDBSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de un resultado de consulta en el blob de tooa de base de datos de MongoDB cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

Como primer paso, el programa de instalación puerta de enlace de hello datos administración según las instrucciones de Hola Hola [Data Management Gateway](data-factory-data-management-gateway.md) artículo.

**Servicio vinculado de MongoDB:**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
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

**Conjunto de datos de entrada de MongoDB:** establecer "externo": "true" informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Actividad de copia en una canalización con el origen MongoDB y el receptor de blob:**

canalización de Hello contiene una actividad de copia que es hello toouse configurado por encima de los conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**MongoDbSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Esquema de Data Factory
Servicio de factoría de datos de Azure deduce el esquema de una colección de MongoDB mediante el uso de documentos de hello 100 más reciente en la colección de Hola. Si estos 100 documentos no incluyan esquema completo, algunas columnas pueden omitirse durante la operación de copia de Hola.

## <a name="type-mapping-for-mongodb"></a>Asignación de tipos para MongoDB
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover hello tooMongoDB de datos siguientes se usan asignaciones de tipos de too.NET de tipos de MongoDB.

| Tipo de MongoDB | Tipo .NET Framework |
| --- | --- |
| Binary |Byte[] |
| Booleano |Booleano |
| Date |DateTime |
| NumberDouble |Doble |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |String |
| String |String |
| UUID |Guid |
| Objeto |Renormalizado en columnas acopladas con “_” como separador anidado |

> [!NOTE]
> toolearn sobre la compatibilidad con matrices mediante tablas virtuales, consulte demasiado[admite para los tipos complejos con tablas virtuales](#support-for-complex-types-using-virtual-tables) sección más adelante.

Actualmente, no se admite los siguientes tipos de datos de MongoDB de hello: DBPointer, JavaScript, Max y Min clave, expresiones regulares, símbolo, marca de tiempo, sin definir

## <a name="support-for-complex-types-using-virtual-tables"></a>Compatibilidad para tipos complejos que usan tablas virtuales
Factoría de datos de Azure usa un integrados ODBC driver tooconnect tooand copiar datos desde la base de datos de MongoDB. Para los tipos complejos, como matrices u objetos con diferentes tipos en documentos de hello, controlador de hello normaliza volver a datos en las tablas virtuales correspondientes. En concreto, si una tabla contiene estas columnas, controlador de hello genera hello las tablas virtuales siguientes:

* A **tabla base**, que contiene Hola los mismos datos que la tabla real de hello excepto para las columnas de tipo complejo de Hola. tabla de base de Hello usa Hola mismo nombre como tabla real de Hola que representa.
* A **tabla virtual** para cada columna de tipo complejo, que expande datos Hola anidado. tablas virtuales Hola se denominan utilizando nombre Hola de tabla real de hello, un separador "_" y el nombre de Hola de objeto o matriz de Hola.

Tablas virtuales hacen referencia datos toohello en la tabla real Hola, habilitación Hola controlador tooaccess Hola datos sin normalizar. Consulte el ejemplo de la siguiente sección para más información. Puede tener acceso a contenido de Hola de matrices de MongoDB por consultar y combinar tablas virtuales Hola.

Puede usar hello [Asistente para copiar](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vista Hola lista de tablas de base de datos de MongoDB incluye tablas virtuales hello y obtener una vista previa de los datos de saludo dentro. También puede crear una consulta en el Asistente para copiar Hola y validar el resultado de hello toosee.

### <a name="example"></a>Ejemplo
Por ejemplo, la tabla “ExampleTable” que aparece a continuación es una tabla de MongoDB que tiene una columna con una matriz de objetos en cada celda: Facturas y una columna con una matriz de tipos escalares: Clasificaciones.

| _id | Nombre del cliente | Facturas | Nivel de servicios | Clasificaciones |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id:”123”, artículo:”tostadora”, precio:”456”, descuento:”0.2”}, {invoice_id:”124”, artículo:”horno”, precio: ”1235”, descuento: ”0.2”}] |Silver |[5,6] |
| 2222 |XYZ |[{invoice_id:”135”, artículo:”frigorífico”, precio: ”12543”, descuento: ”0.0”}] |Gold |[1,2] |

controlador de Hello generaría varios toorepresent tablas virtuales esta misma tabla. Hola primera virtual tabla es Hola base denominada "ExampleTable", se muestra a continuación. tabla de base de Hello contiene todos los datos de Hola de tabla original hello, pero los datos de Hola de matrices de Hola se ha omitido y se expanden en las tablas virtuales Hola.

| _id | Nombre del cliente | Nivel de servicios |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

Hello en las tablas siguientes muestran Hola tablas virtuales que representan matrices original de hello en el ejemplo de Hola. Estas tablas contienen siguiente de hello:

* Toohello columna de clave principal correspondiente toohello fila original de la matriz original Hola hacer copia de una referencia (a través de la columna de hello _id)
* Una indicación de posición de Hola de datos de hello dentro de la matriz original Hola
* Hola expande datos para cada elemento de matriz de Hola

Tabla “ExampleTable_Invoices”:

| _id | ExampleTable_Invoices_dim1_idx | invoice_id | item | price | Descuento |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |tostadora |456 |0,2 |
| 1111 |1 |124 |horno |1235 |0,2 |
| 2222 |0 |135 |frigorífico |12543 |0.0 |

Tabla “ExampleTable_Ratings”:

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.

## <a name="next-steps"></a>Pasos siguientes
Vea [mover datos entre local y nube](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso para crear una canalización de datos que mueve el almacén de datos de Azure tooan del almacén de datos desde un datos locales.
