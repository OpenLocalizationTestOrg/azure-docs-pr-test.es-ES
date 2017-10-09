---
title: datos de aaaMove de fuentes de OData | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure de orígenes de datos de toomove de OData."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a>Movimiento de datos de un origen de OData mediante Factoría de datos de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un origen de OData. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos desde un almacén de datos de OData origen tooany admitida receptor. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Factoría de datos admite actualmente solo mover almacenes de datos desde una fuente de OData tooother datos, pero no para mover los datos de otros datos almacena el código fuente de OData de tooan. 

## <a name="supported-versions-and-authentication-types"></a>Versiones admitidas y tipos de autenticación
Este conector OData admite la versión de OData 3.0 y 4.0, y puede copiar datos de orígenes OData locales y en la nube. Para Hola este último debe tooinstall Hola Data Management Gateway. Consulte el artículo [Mover datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de Data Management Gateway.

Estos son los tipos de autenticación admitidos:

* tooaccess **nube** fuente de OData, puede usar anónima, básica (nombre de usuario y contraseña) o Azure Active Directory en la función de autenticación de OAuth.
* tooaccess **local** fuente de OData, puede usar anónima, básica (nombre de usuario y contraseña) o la autenticación de Windows.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos desde un origen OData mediante diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un origen OData, vea [ejemplo de JSON: copiar los datos de código fuente de OData tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son origen de tooOData específicos de entidades de toodefine usado factoría de datos:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooOData vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **OData** |Sí |
| url |Dirección URL del servicio OData Hola. |Sí |
| authenticationType |Tipo de autenticación usa tooconnect toohello OData origen. <br/><br/> Para OData en la nube, los valores posibles son Anonymous, Basic y OAuth (tenga en cuenta que Azure Data Factory en estos momentos solo admite la autenticación OAuth basada en Azure Active Directory). <br/><br/> Para OData local, los valores posibles son: Anonymous, Basic y Windows. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación básica. |Sí (solo si usa la autenticación básica) |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |Sí (solo si usa la autenticación básica) |
| authorizedCredential |Si usa OAuth, haga clic en **Authorize** botón en hello Asistente para copiar de factoría de datos o el Editor y escriba sus credenciales, valor de Hola de esta propiedad será generado automáticamente. |Sí (solo si usa la autenticación OAuth) |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el servicio de OData de tooconnect toohello local. Especifique solo si va a copiar datos del origen de OData local. |No |

### <a name="using-basic-authentication"></a>Uso de la autenticación básica
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Uso de autenticación anónima
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a>Uso de la autenticación de Windows para acceder al origen de OData local
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a>Uso de la autenticación OAuth para tener acceso al origen de OData en la nube
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **ODataResource** (que incluye el conjunto de datos de OData) tiene Hola propiedades siguientes

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| path |Ruta de acceso toohello recurso de OData |No |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Propiedades disponibles en la sección de typeProperties Hola de actividad de hello en hello otra parte varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Cuando el origen es del tipo **RelationalSource** (que incluye OData) Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Ejemplo | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |"?$select=Name, Description&$top=5" |No |

## <a name="type-mapping-for-odata"></a>Asignación de tipos para OData
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos.

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover los datos de OData, hello siguientes usan las asignaciones son de tipo de too.NET de tipos de OData.

| Tipo de datos OData | Tipo .NET |
| --- | --- |
| Edm.Binary |Byte[] |
| Edm.Boolean |Booleano |
| Edm.Byte |Byte[] |
| Edm.DateTime |DateTime |
| Edm.Decimal |Decimal |
| Edm.Double |Doble |
| Edm.Single |Single |
| Edm.Guid |Guid |
| Edm.Int16 |Int16 |
| Edm.Int32 |Int32 |
| Edm.Int64 |Int64 |
| Edm.SByte |Int16 |
| Edm.String |String |
| Edm.Time |TimeSpan |
| Edm.DateTimeOffset |Datetimeoffset |

> [!Note]
> Los tipos de datos complejos de OData, como por ejemplo, Object no se admiten.

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de código fuente de OData tooAzure Blob
Este ejemplo proporciona las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestra cómo tooan almacenamiento de blobs de Azure del origen de datos de toocopy desde una de OData. Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure. ejemplo de Hola tiene Hola siguiendo las entidades de la factoría de datos:

1. Un servicio vinculado de tipo [OData](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [ODataResource](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de realizar una consulta en un tooan de origen OData blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de OData:** en este ejemplo usa Hola autenticación anónima. Consulte la sección [Propiedades del servicio vinculado de OData](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
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

**Conjunto de datos de entrada de OData:**

Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

Especificar **ruta de acceso** en el conjunto de datos de hello definición es opcional.

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Actividad de copia en una canalización con origen OData y receptor blob:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos de (más recientes) más recientes de Hola de código fuente de OData de Hola.

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

Especificar **consulta** en canalización Hola definición es opcional. Hola **URL** es que el servicio de factoría de datos de hello utiliza datos tooretrieve: dirección URL especificada en Hola servicios vinculados (obligatorio) + ruta de acceso especificada en el conjunto de datos de hello (opcional) + consultar en la canalización de hello (opcional).


### <a name="type-mapping-for-odata"></a>Asignación de tipos para OData
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover los datos de almacenes de datos de OData, tipos de datos de OData son tipos de too.NET asignado.

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
