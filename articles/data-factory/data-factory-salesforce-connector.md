---
title: "aaaMove datos de Salesforce con factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de Salesforce con Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Movimiento de datos de Salesforce mediante el uso de Data Factory de Azure
En este artículo se describe cómo puede usar actividad de copia en un Azure generador toocopy datos de almacén de datos de Salesforce tooany que aparece en la columna de receptor de Hola Hola [admite orígenes y receptores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia y combinaciones de almacén de datos admitidos.

Factoría de datos de Azure admite actualmente solo mover datos de Salesforce demasiado[admite almacenes de datos del receptor](data-factory-data-movement-activities.md#supported-data-stores-and-formats), pero no admite la migración de datos de otro tooSalesforce de almacenes de datos.

## <a name="supported-versions"></a>Versiones compatibles
Este conector es compatible con hello siguientes ediciones de Salesforce: Developer Edition, Professional Edition, Enterprise Edition o edición ilimitado. Y admite la copia del dominio personalizado, producción y espacio aislado de Salesforce.

## <a name="prerequisites"></a>Requisitos previos
* Debe estar habilitado el permiso API. Consulte [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* toocopy datos de almacenes de datos de Salesforce tooon local, debe tener al menos 2.0 de puerta de enlace de administración de datos instalados en su entorno local.

## <a name="salesforce-request-limits"></a>Límites de solicitudes de Salesforce
Salesforce tiene límites para el número total de solicitudes de API y el de solicitudes de API simultáneas. Tenga en cuenta Hola siguientes puntos:

- Si el número de Hola de solicitudes simultáneas supera el límite de hello, se produce una limitación y verá errores aleatorios.
- Si el número total de Hola de solicitudes supera el límite de hello, Hola cuenta de Salesforce se bloqueará durante 24 horas.

También puede recibir errores de "REQUEST_LIMIT_EXCEEDED" hello en ambos escenarios. Consulte la sección Hola "API límites de solicitudes" Hola [límites de desarrollador de Salesforce](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artículo para obtener más información.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con actividad de copia que mueva datos desde Salesforce mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son toocopy usa datos de Salesforce, consulte [ejemplo de JSON: copiar los datos de Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos usado toodefine tooSalesforce específico: 

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona descripciones para los elementos JSON que son toohello específico del servicio vinculado de Salesforce.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **Salesforce**. |Sí |
| environmentUrl | Especifique la instancia de la dirección URL de Salesforce de Hola. <br><br> - La dirección predeterminada es "https://login.salesforce.com". <br> -toocopy datos de espacio aislado, especifique "https://test.salesforce.com". <br> -toocopy datos de dominio personalizado, especifique, por ejemplo, "https://[domain].my.salesforce.com". |No |
| nombre de usuario |Especifique un nombre de usuario de cuenta de usuario de Hola. |Sí |
| Contraseña |Especifique una contraseña para la cuenta de usuario de Hola. |Sí |
| securityToken |Especifique un token de seguridad para la cuenta de usuario de Hola. Vea [obtener token de seguridad](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obtener instrucciones sobre cómo tooreset/obtener un token de seguridad. en general, vea toolearn acerca de los tokens de seguridad [API hello y seguridad](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Sí |

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades que están disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola typeProperties sección un conjunto de datos de tipo hello **RelationalTable** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en Salesforce. |No (si se especifica una **consulta** de **RelationalSource**) |

> [!IMPORTANT]
> parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades que están disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Propiedades como name, description, tablas input y output y varias directivas están disponibles para todos los tipos de actividades.

propiedades de Hola que están disponibles en Hola typeProperties sección de actividad de hello, en hello en otra parte, varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

En la actividad de copia, al origen de hello es del tipo hello **RelationalSource** (que incluye Salesforce), Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Consulta de SQL-92 o de [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Por ejemplo: `select * from MyTable__c`. |No (si hello **tableName** de hello **conjunto de datos** se especifica) |

> [!IMPORTANT]
> parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Sugerencias de consulta
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Recuperación de datos mediante la cláusula WHERE en la columna DateTime
Cuando especifique consultas SQL o SOQL de hello, preste atención toohello diferencia de formato de fecha y hora. Por ejemplo:

* **Ejemplo SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **Ejemplo de SQL**:
    * **Mediante copia Asistente toospecify Hola consulta:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **Usar JSON editar toospecify Hola consulta (carácter de escape correctamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Recuperación de datos de informes de Salesforce
Puede recuperar datos de informes de Salesforce especificando las consultas como `{call "<report name>"}`; por ejemplo,. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Recuperación de los registros eliminados desde la papelera de reciclaje de Salesforce
tooquery Hola suave elimina registros de Papelera de reciclaje de Salesforce, puede especificar **"IsDeleted = 1"** en la consulta. Por ejemplo,

* Especifique tooquery sólo los registros eliminado de hello, "Seleccione * de MyTable__c **donde IsDeleted = 1**"
* especificar tooquery todos Hola registros incluso existente de Hola y Hola eliminado, "Seleccione * de MyTable__c **donde IsDeleted = 0 o IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de Salesforce tooAzure Blob
Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy datos de Salesforce tooAzure almacenamiento de blobs. Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.   

Estos son artefactos de la factoría de datos de Hola que necesitará escenario de toocreate tooimplement Hola. secciones de Hola que siguen la lista de hello proporcionan detalles acerca de estos pasos.

* Un servicio vinculado de tipo hello [Salesforce](#linked-service-properties)
* Un servicio vinculado de tipo hello [azurestorage.](data-factory-azure-blob-connector.md#linked-service-properties)
* Una entrada [conjunto de datos](data-factory-create-datasets.md) de tipo hello [RelationalTable](#dataset-properties)
* Una salida [conjunto de datos](data-factory-create-datasets.md) de tipo hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**Servicio vinculado de Salesforce**

Este ejemplo utiliza hello **Salesforce** servicio vinculado. Vea hello [servicio vinculado de Salesforce](#linked-service-properties) sección de propiedades de Hola que son compatibles con este servicio vinculado.  Vea [obtener token de seguridad](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obtener instrucciones sobre cómo tooreset/get Hola token de seguridad.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
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
**Conjunto de datos de entrada de Salesforce**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
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

> [!IMPORTANT]
> parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Conjunto de datos de salida de blob de Azure**

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
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Canalización con actividad de copia:**

canalización Hello contiene actividad de copia, que se configura toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource**, hello y **receptor** tipo está establecido demasiado**BlobSink**.

Vea [propiedades de tipo RelationalSource](#copy-activity-properties) para lista de Hola de propiedades que son compatibles con hello RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> parte de "__c" Hello de nombre de la API de hello es necesario para cualquier objeto personalizado.

![Data Factory - Conexión a Salesforce - Nombre de la API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Asignación de tipos para Salesforce
| Tipo de Salesforce | Tipo basado en .NET |
| --- | --- |
| Numeración automática |String |
| Casilla de verificación |Booleano |
| Moneda |Doble |
| Date |DateTime |
| Fecha y hora |DateTime |
| Email |String |
| Id |String |
| Relación de búsqueda |String |
| Lista desplegable de selección múltiple |String |
| Number |Doble |
| Percent |Doble |
| Teléfono |String |
| Lista desplegable |String |
| Texto |String |
| Área de texto |String |
| Área de texto (largo) |String |
| Área de texto (enriquecido) |String |
| Texto (cifrado) |String |
| URL |String |

> [!NOTE]
> columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
