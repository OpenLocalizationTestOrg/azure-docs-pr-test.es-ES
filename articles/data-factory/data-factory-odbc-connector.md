---
title: aaaMove datos de almacenes de datos ODBC | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure de almacenes de datos de toomove de datos ODBC."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Movimiento de datos desde almacenes de datos ODBC mediante Factoría de datos de Azure
Este artículo explica cómo almacenar toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un datos ODBC local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos desde un almacén de datos ODBC datos almacén tooany admitida receptor. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos desde un datos ODBC, pero no para mover los datos de otro almacén de datos ODBC tooan de datos almacenes. 

## <a name="enabling-connectivity"></a>Habilitación de la conectividad
Servicio de factoría de datos admite conectar orígenes ODBC de tooon locales mediante Hola Data Management Gateway. Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola. Usar almacén de datos ODBC de tooan tooconnect de puerta de enlace de hello incluso si está hospedado en una máquina virtual de IaaS de Azure.

Puede instalar la puerta de enlace de Hola en hello local mismo equipo u Hola VM de Azure como almacén de datos ODBC de Hola. Sin embargo, recomendamos que instale la puerta de enlace de hello en un equipo independiente/Azure IaaS VM tooavoid contención de recursos y para mejorar el rendimiento. Cuando se instala la puerta de enlace de hello en un equipo independiente, máquina Hola debe ser tooaccess capaz de máquina de hello con almacén de datos ODBC Hola.

Además de hello Data Management Gateway, también se necesita el controlador ODBC de tooinstall Hola para Hola de almacén de datos en la máquina de puerta de enlace de Hola.

> [!NOTE]
> Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos desde un almacén de datos ODBC mediante diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos ODBC, vea [ejemplo de JSON: tooAzure Blob del almacén de datos de copia de datos ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sección de este artículo. 

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son el almacén de datos de uso toodefine factoría de datos entidades tooODBC específico:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooODBC vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **OnPremisesOdbc** |Sí |
| connectionString |parte de credencial de acceso no Hola de cadena de conexión de Hola y opcional cifra credenciales. Vea los ejemplos de hello las secciones siguientes. |Sí |
| credential |Hola credencial parte de acceso a cadena de conexión de hello especificada en formato de valores de propiedad específicos del controlador. Ejemplo: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”. |No |
| authenticationType |Tipo de autenticación que utiliza el almacén de datos ODBC tooconnect toohello. Los valores posibles son: Anonymous y Basic. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación básica. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el almacén de datos ODBC tooconnect toohello. |Sí |

### <a name="using-basic-authentication"></a>Uso de la autenticación básica

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Uso de la autenticación básica con credenciales cifradas
Puede cifrar las credenciales de hello con hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versión de PowerShell de Azure) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versión o una anterior de hello Azure PowerShell).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Uso de autenticación anónima

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos ODBC) tiene Hola propiedades siguientes

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en el almacén de datos ODBC Hola. |Sí |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Propiedades disponibles en hello **typeProperties** sección de actividad de hello en hello varían con cada tipo de actividad en otra parte. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

En la actividad de copia, cuando el origen es de tipo **RelationalSource** (que incluye ODBC), Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: select * from MyTable. |Sí |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>Ejemplo de JSON: tooAzure Blob del almacén de datos de copia de datos ODBC
Este ejemplo proporciona definiciones de JSON que puede usar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestra cómo del origen de datos de toocopy desde un ODBC tooan almacenamiento de blobs de Azure. Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

1. Un servicio vinculado del tipo [OnPremisesOdbc](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de un resultado de consulta en un blob de tooa del almacén de datos ODBC cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

Como primer paso, configurar la puerta de enlace de administración de datos de Hola. instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.

**Servicio vinculado de ODBC** en este ejemplo utiliza la autenticación básica de Hola. Consulte la sección [Propiedades del servicio vinculado de ODBC](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Servicio vinculado de Almacenamiento de Azure**

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

**Conjunto de datos de entrada de ODBC**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en una base de datos ODBC y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.

Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Actividad de copia en una canalización con origen ODBC (RelationalSource) y receptor blob (BlobSink)**

canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Asignación de tipos para ODBC
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover los datos de almacenes de datos ODBC, tipos de datos ODBC son tipos de too.NET asignado como se mencionó en hello [asignaciones de tipos de datos de ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tema.

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>Almacén GE Historian
Crear un toolink de servicio ODBC vinculada una [Proficy en GE historia (ahora en historia GE)](http://www.geautomation.com/products/proficy-historian) tooan factoría de datos de Azure del almacén de datos tal y como se muestra en el siguiente ejemplo de Hola:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Instalar Data Management Gateway en un equipo local y registrar la puerta de enlace de hello con el portal de Hola. puerta de enlace de Hello instalada en el equipo local utiliza el controlador ODBC de Hola para en historia GE tooconnect toohello almacén de datos en historia GE. Por lo tanto, instalar a controladores de hello si aún no está instalado en la máquina de puerta de enlace de Hola. Consulte la sección [Habilitación de la conectividad](#enabling-connectivity) para más información.

Antes de usar hello en historia GE almacenar en una solución de factoría de datos, compruebe si la puerta de enlace de hello puede conectarse toohello almacén de datos siguiendo las instrucciones en la sección siguiente de Hola.

Leer el artículo de Hola desde el principio de Hola para obtener una descripción detallada del uso de datos ODBC se almacena como almacenes de datos de origen en una operación de copia.  

## <a name="troubleshoot-connectivity-issues"></a>Solución de problemas de conectividad
problemas de conexión de tootroubleshoot, usar hello **diagnósticos** ficha de **Administrador de configuración de Data Management Gateway**.

1. Inicie el **Administrador de configuración de Data Management Gateway**. Se puede ejecutar para la búsqueda de "C:\Program Files\Microsoft datos administración Gateway\1.0\Shared\ConfigManager.exe" directamente (o) **puerta de enlace** toofind un vínculo demasiado**Microsoft Data Management Gateway** aplicación tal como se muestra en hello después de la imagen.

    ![Buscar puerta de enlace](./media/data-factory-odbc-connector/search-gateway.png)
2. Cambiar toohello **diagnósticos** ficha.

    ![Diagnóstico de puerta de enlace](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Seleccione hello **tipo** (servicio vinculado) del almacén de datos.
4. Especifique **autenticación** y escriba **credenciales** (o) Especifique **cadena de conexión** que es el almacén de datos de uso tooconnect toohello.
5. Haga clic en **Probar conexión** tootest Hola conexión toohello almacén de datos.

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
