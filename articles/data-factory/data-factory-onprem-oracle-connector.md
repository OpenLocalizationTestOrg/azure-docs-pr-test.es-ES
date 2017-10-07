---
title: "aaaCopy datos de Oracle se realiza mediante la factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocopy datos de base de datos de Oracle que sea de manera local mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Copia de datos con una instancia local Oracle como origen o destino mediante Azure Data Factory
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de Oracle local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede copiar datos **desde una base de datos de Oracle** toohello siguientes almacenes de datos:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Puede copiar los datos de hello siguientes almacenes de datos **tooan base de datos de Oracle**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Requisitos previos
Factoría de datos admite conexión orígenes de Oracle de tooon locales mediante Hola Data Management Gateway. Vea [Data Management Gateway](data-factory-data-management-gateway.md) toolearn artículo acerca de Data Management Gateway y [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello una canalización de datos datos de toomove.

Puerta de enlace es necesaria incluso aunque hello Oracle hospedado en una VM de IaaS de Azure. Puede instalar la puerta de enlace de hello en Hola mismo IaaS VM como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola pueden conectar toohello base de datos.

> [!NOTE]
> Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.

## <a name="supported-versions-and-installation"></a>Versiones compatibles e instalación
Este conector de Oracle admite dos versiones de controladores:

- **Controlador de Microsoft para Oracle (recomendado)**: a partir de Data Management Gateway versión 2.7, un controlador de Microsoft para Oracle se instala automáticamente junto con la puerta de enlace de hello, por lo que no necesita tooadditionally identificador hello controlador en orden tooestablish conectividad tooOracle y, también puede experimentar un mejor rendimiento de copia con este controlador. Se admiten las siguientes versiones de bases de datos de Oracle:
    - Oracle 12c R1 (12.1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10.1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> Controlador de Microsoft para Oracle sólo admite actualmente copiaría datos de Oracle, pero no escribir tooOracle. Y capacidad de conexión de prueba de nota hello en la pestaña de diagnóstico de puerta de enlace de administración de datos no es compatible con este controlador. Como alternativa, puede usar la conectividad de Hola de hello copia Asistente toovalidate.
>

- **Proveedor de datos de Oracle para. NET:** también puede elegir el proveedor de datos de Oracle toocopy datos de toouse de / tooOracle. Este componente se incluye en [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/) (Componentes de acceso a datos Oracle para Windows). Instale la versión adecuada de hello (32 o 64 bits) en la máquina de Hola donde se instala la puerta de enlace de Hola. [Proveedor de datos de Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) puede tener acceso a tooOracle base de datos 10 g versión 2 o posterior.

    Si elige "Instalación de XCopy", siga los pasos de hello readme.htm. Se recomienda que elegir a instalador Hola con interfaz de usuario (no-XCopy uno).

    Después de instalar el proveedor de hello, **reiniciar** Hola servicio de host de Data Management Gateway en su equipo con servicios de applet (u) Administrador de configuración de Data Management Gateway.  

Si utiliza copia Asistente tooauthor Hola copia canalización, tipo de controlador de hello será determina automáticamente. El controlador de Microsoft se usará de forma predeterminada, a menos que la versión de la puerta de enlace sea inferior a 2.7 o elija Oracle como receptor.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos desde una base de datos de Oracle local o hacia ella mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o más canalizaciones. 
2. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink. Por ejemplo, si va a copiar datos desde un tooan de base de datos de Oralce almacenamiento de blobs de Azure, cree dos toolink servicios vinculados su base de datos de Oracle y la factoría de datos de tooyour de cuenta de almacenamiento de Azure. Para las propiedades de servicio vinculado que son tooOracle específico, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.
3. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. En el ejemplo de Hola mencionado en el último paso de hello, creará una tabla de hello toospecify de conjunto de datos en la base de datos de Oracle que contiene datos de entrada de Hola. Crear contenedor de blobs Hola de otro conjunto de datos toospecify y carpeta Hola que contiene datos de hello copiados de Hola de base de datos de Oracle. Para las propiedades de conjunto de datos que son tooOracle específico, consulte [propiedades de conjunto de datos](#dataset-properties) sección.
4. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. En el ejemplo de Hola que se ha mencionado anteriormente, use OracleSource como un origen y BlobSink como un receptor para la actividad de copia de Hola. De forma similar, si va a copiar desde la base de datos del almacenamiento de blobs de Azure tooOracle, usar BlobSource y OracleSink de actividad de copia de Hola. Para copiar propiedades de actividad que son la base de datos tooOracle específica, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección. Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde una base de datos de Oracle local, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-oracle-database) sección de este artículo.

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos de uso toodefine:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooOracle vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **OnPremisesOracle** |Sí |
| driverType | Especificar qué controlador toouse toocopy datos / tooOracle base de datos. Los valores permitidos son **Microsoft** u **ODP** (valor predeterminado). Consulte la sección [Versiones compatibles e instalación](#supported-versions-and-installation) para obtener información detallada sobre los controladores. | No |
| connectionString | Especifique la información necesaria la instancia de base de datos de Oracle toohello tooconnect para la propiedad connectionString de Hola. | Sí |
| gatewayName | Nombre de puerta de enlace de Hola que es usado tooconnect toohello servidor Oracle local |Sí |

**Ejemplo: Uso del controlador de Microsoft**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Ejemplo: uso del controlador de ODP**

Consulte demasiado[este sitio](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) para hello formatos permitido.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (Oracle, Azure Blob, Azure Table, etc.).

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección de typeProperties Hello para el conjunto de datos de Hola de tipo OracleTable tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola Hola base de datos de Oracle que Hola servicio vinculado que hace referencia a. |No (si se especifica **oracleReaderQuery** de **OracleSource**) |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

> [!NOTE]
> Hola actividad de copia toma solo una entrada y produce un único resultado.

Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

### <a name="oraclesource"></a>OracleSource
En la actividad de copia, cuando el origen de hello es de tipo **OracleSource** Hola propiedades siguientes está disponible en **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| oracleReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: select * from MyTable. <br/><br/>Si no se especifica, Hola instrucción SQL que se ejecuta: seleccione * from MyTable |No (si se especifica **tableName** de **dataset**) |

### <a name="oraclesink"></a>OracleSink
**OracleSink** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: 00:30:00 (30 minutos). |No |
| writeBatchSize |Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. |Entero (número de filas) |No (valor predeterminado: 100) |
| sqlWriterCleanupScript |Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian. |Una instrucción de consulta. |No |
| sliceIdentifierColumnName |Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar. |Nombre de columna de una columna con el tipo de datos binarios (32). |No |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Ejemplos JSON para copiar datos tooand de base de datos de Oracle
Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy datos de Oracle tooan la base de datos de almacenamiento de blobs de Azure. Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Ejemplo: Copiar los datos de Oracle tooAzure Blob

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

1. Un servicio vinculado de tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) como origen y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) como receptor.

ejemplo de Hola copia datos de una tabla en un blob de tooa de base de datos de Oracle local cada hora. Para obtener más información sobre varias propiedades utilizadas en el ejemplo de Hola, consulte la documentación en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de Oracle:**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Servicio vinculado Azure Blob Storage:**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Conjunto de datos de entrada de Oracle:**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en Oracle y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.

Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Canalización con actividad de copia:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**OracleSource** y **receptor** tipo está establecido demasiado**BlobSink**.  consulta SQL Hola especificada con **oracleReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Ejemplo: Copiar los datos de Blob de Azure tooOracle
Este ejemplo muestra cómo toocopy datos desde un almacenamiento de blobs de Azure tooan locales base de datos de Oracle. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de los orígenes de hello indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.  

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

1. Un servicio vinculado de tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) como origen y [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) como receptor.

ejemplo de Hola copia datos de una tabla de tooa de blob en una base de datos de Oracle local cada hora. Para obtener más información sobre varias propiedades utilizadas en el ejemplo de Hola, consulte la documentación en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de Oracle:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Servicio vinculado de almacenamiento de blobs de Azure:**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Conjunto de datos de entrada de blob de Azure**

Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola. "externo": "true" configuración informa a servicio de factoría de datos de Hola que esta tabla es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
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

**Conjunto de datos de salida de Oracle:**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en Oracle. Crear tabla de hello en Oracle con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola. Se agregan nuevas filas toohello tabla cada hora.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**Canalización con actividad de copia:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** hello y **receptor** tipo está establecido demasiado**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>Sugerencias de solución de problemas
### <a name="problem-1-net-framework-data-provider"></a>Problema 1: proveedor de datos .NET Framework

Ve a continuación hello **mensaje de error**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Causas posibles:**

1. no se instaló el proveedor de datos de .NET Framework para Oracle Hola.
2. Hola proveedor de datos de .NET Framework para Oracle era too.NET instalado Framework 2.0 y no se encuentra en carpetas de hello .NET Framework 4.0.

**Resolución o solución alternativa:**

1. Si no ha instalado Hola proveedor .NET para Oracle, [instalarlo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e intente de nuevo escenario de Hola.
2. Si recibe el mensaje de error de hello incluso después de instalar el proveedor de hello, Hola lo siguiente:
   1. Abrir configuración de máquina de .NET 2.0 desde la carpeta de hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Busque **proveedor de datos de Oracle para .NET**, y debe ser capaz de toofind una entrada como se muestra en hello según muestra en **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Proveedor de datos de oracle para .NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />”
3. Copie este archivo de entrada toohello machine.config Hola después carpeta v4.0: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config y too4.xxx.x.x de versión de Hola de cambio.
4. Instalar "< ruta de instalación ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" en la caché de ensamblados global (GAC) de hello ejecutando `gacutil /i [provider path]`. ## sugerencias para solucionar problemas

### <a name="problem-2-datetime-formatting"></a>Problema 2: formato de fecha y hora

Ve a continuación hello **mensaje de error**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Resolución o solución alternativa:**

Puede que necesite tooadjust cadena de consulta de hello en la actividad de copia según cómo se configuran las fechas en la base de datos de Oracle, como se muestra en la siguiente Hola ejemplo (mediante la función to_date de hello):

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Asignación de tipos para Oracle
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover los datos de Oracle, se usa Hola siguiendo las asignaciones del tipo de too.NET del tipo de datos de Oracle y viceversa.

| Tipo de datos de Oracle | Tipo de datos de .NET Framework |
| --- | --- |
| BFILE |Byte[] |
| BLOB |Byte[] |
| CHAR |String |
| CLOB |String |
| DATE |DateTime |
| FLOAT |Decimal, String (si la precisión > 28) |
| INTEGER |Decimal, String (si la precisión > 28) |
| INTERVALO año tooMONTH |Int32 |
| INTERVALO día tooSECOND |TimeSpan |
| LONG |String |
| LONG RAW |Byte[] |
| NCHAR |String |
| NCLOB |String |
| NUMBER |Decimal, String (si la precisión > 28) |
| NVARCHAR2 |String |
| RAW |Byte[] |
| ROWID |String |
| TIMESTAMP |DateTime |
| TIMESTAMP WITH LOCAL TIME ZONE |DateTime |
| TIMESTAMP WITH TIME ZONE |DateTime |
| UNSIGNED INTEGER |NUMBER |
| VARCHAR2 |String |
| XML |String |

> [!NOTE]
> Tipo de datos **año del intervalo tooMONTH** y **tooSECOND INTERVAL DAY** no se admiten cuando se utiliza el controlador de Microsoft.

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
