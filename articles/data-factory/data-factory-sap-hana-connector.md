---
title: datos de aaaMove de SAP HANA con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de SAP HANA con Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Movimiento de datos de SAP HANA mediante Azure Data Factory
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un local SAP HANA. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos desde un almacén de datos local SAP HANA datos almacén tooany admitida receptor. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Factoría de datos admite actualmente solo mover almacenes de datos de un dato de tooother de SAP HANA, pero no para mover los datos de otros datos de los almacenes tooan SAP HANA.

## <a name="supported-versions-and-installation"></a>Versiones compatibles e instalación
Este conector es compatible con cualquier versión de base de datos de SAP HANA. Admite la copia de datos de modelos de información de HANA (como las vistas de análisis y cálculo) y las tablas de fila o columna mediante consultas SQL.

tooenable Hola conectividad toohello instancia SAP HANA, instale Hola de los componentes siguientes:
- **Data Management Gateway**: conectar tooon local de datos de servicio de factoría de datos admite almacenes (incluidos SAP HANA) mediante un componente denominado Data Management Gateway. toolearn acerca de Data Management Gateway e instrucciones paso a paso para configurar la puerta de enlace de hello, consulte [toocloud almacén de datos del almacén de datos de movimiento entre los datos locales](data-factory-move-data-between-onprem-and-cloud.md) artículo. Puerta de enlace es necesaria incluso aunque Hola SAP HANA se hospeda en una máquina virtual de IaaS de Azure (VM). Puede instalar la puerta de enlace de hello en hello misma máquina virtual como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola se pueden conectar toohello base de datos.
- **Controlador ODBC de SAP HANA** en la máquina de puerta de enlace de Hola. Puede descargar el controlador de ODBC de SAP HANA Hola de hello [centro de descarga de Software de SAP](https://support.sap.com/swdc). Búsqueda con la palabra clave de hello **SAP HANA cliente para Windows**. 

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API. 

- toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido. 
- También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy de datos de un local SAP HANA, consulte [ejemplo de JSON: copiar los datos de SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de propiedades JSON que forman el almacén de datos de SAP HANA de toodefine usado factoría de datos entidades tooan específico:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSAP HANA servicio vinculado.

Propiedad | Descripción | Valores permitidos | Obligatorio
-------- | ----------- | -------------- | --------
Servidor | Nombre del servidor de hello en qué Hola SAP HANA reside la instancia. Si el servidor usa un puerto personalizado, especifique `server:port`. | string | Sí
authenticationType | Tipo de autenticación. | cadena. "Basic" o "Windows" | Sí 
nombre de usuario | Nombre de usuario de Hola que tiene el servidor de acceso toohello SAP | cadena | Sí
Contraseña | Contraseña de usuario de Hola. | cadena | Sí
gatewayName | Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la instancia de SAP HANA de tooconnect toohello local. | cadena | Sí
encryptedCredential | Hola cifra la cadena de credenciales. | cadena | No

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. No hay ninguna propiedad específica del tipo compatible con el conjunto de datos de SAP HANA de Hola de tipo **RelationalTable**. 


## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Cuando el origen de la actividad de copia es del tipo **RelationalSource** (que incluye SAP HANA), Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query | Especifica Hola SQL permite consultar tooread datos de instancia de SAP HANA Hola. | Consulta SQL. | Sí |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de SAP HANA tooAzure Blob
en el ejemplo siguiente Hello proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Este ejemplo se muestra cómo toocopy datos desde un tooan de SAP HANA local almacenamiento de blobs de Azure. Sin embargo, se pueden copiar datos **directamente** tooany de receptores de hello aparecen [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.  

> [!IMPORTANT]
> Este ejemplo proporciona fragmentos JSON. No incluye instrucciones paso a paso para la creación de factoría de datos de Hola. Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

1. Un servicio vinculado de tipo [SapHana](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo Hello copia datos de un tooan de la instancia de SAP HANA blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

Como primer paso, configurar la puerta de enlace de administración de datos de Hola. instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.

### <a name="sap-hana-linked-service"></a>Servicio vinculado de SAP HANA
Esto vincula los vínculos de servicio su factoría de datos de SAP HANA instancia toohello. propiedad de tipo Hello se establece demasiado**SapHana**. sección de Hello typeProperties proporciona información de conexión para la instancia de SAP HANA Hola.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a>Servicio vinculado de Azure Storage
Esto vincula los vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello. propiedad de tipo Hello se establece demasiado**AzureStorage**. sección de Hello typeProperties proporciona información de conexión para hello cuenta de almacenamiento de Azure.

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

### <a name="sap-hana-input-dataset"></a>Conjunto de datos de entrada de SAP HANA

Este conjunto de datos define el conjunto de datos de SAP HANA Hola. Se establece el tipo de saludo del conjunto de datos de hello factoría de datos demasiado**RelationalTable**. Actualmente, no establece ninguna propiedad específica de tipo para un conjunto de datos de SAP HANA. consulta de Hola Hola definición de actividad de copia especifica qué tooread de datos de instancia de SAP HANA Hola. 

Establecer la propiedad external tootrue informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

Propiedades de frecuencia y el intervalo define la programación de Hola. En este caso, los datos de Hola se leen desde la instancia de SAP HANA Hola cada hora. 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a>Conjunto de datos de salida de blob de Azure
Este conjunto de datos define el conjunto de datos de hello salida blobs de Azure. propiedad de tipo Hello se establece tooAzureBlob. sección de Hello typeProperties proporciona donde se almacenan los datos de hello copiados de la instancia de SAP HANA Hola. Hola se escriben los datos blob nuevo tooa cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>Canalización con actividad de copia

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** (para el origen de SAP HANA) y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>Asignación de tipos para SAP HANA
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover los datos de SAP HANA, se usa Hola siguiendo las asignaciones de tipos de too.NET de tipos de SAP HANA.

Tipo de SAP HANA | Tipo basado en .NET
------------- | ---------------
TINYINT | Byte
SMALLINT | Int16
INT | Int32
BIGINT | Int64
REAL | Single
DOUBLE | Single
DECIMAL | Decimal
BOOLEAN | Byte
VARCHAR | String
NVARCHAR | String
CLOB | Byte[]
ALPHANUM | String
BLOB | Byte[]
DATE | DateTime
TIME | timespan
TIMESTAMP | DateTime
SECONDDATE | DateTime

## <a name="known-limitations"></a>Limitaciones conocidas
Cuando se copian datos de SAP HANA, hay algunas limitaciones conocidas:

- Las cadenas NVARCHAR son longitud truncada toomaximum de 4.000 caracteres Unicode
- SMALLDECIMAL no se admite
- VARBINARY no se admite
- Las fechas válidas son las del intervalo entre 30/12/1899 y 31/12/9999

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
