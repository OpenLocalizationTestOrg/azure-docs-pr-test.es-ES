---
title: datos de aaaTransform mediante script U-SQL - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo el servicio de proceso tooprocess o transformar datos mediante la ejecución de secuencias de comandos SQL U en análisis de Data Lake de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Transformación de datos mediante la ejecución de scripts de U-SQL en Azure Data Lake Analytics 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Actividad de Hive](data-factory-hive-activity.md) 
> * [Actividad de Pig](data-factory-pig-activity.md)
> * [Actividad MapReduce](data-factory-map-reduce.md)
> * [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Actividad de Spark](data-factory-spark.md)
> * [Actividad de ejecución de Batch de Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Actividad Actualizar recurso de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md)
> * [Actividad U-SQL de Data Lake Analytics](data-factory-usql-activity.md)
> * [Actividad personalizada de .NET](data-factory-use-custom-activities.md)

Una canalización en una factoría de datos de Azure procesa los datos de los servicios de almacenamiento vinculados mediante el uso de servicios de proceso vinculados. Contiene una secuencia de actividades donde cada actividad realiza una operación de procesamiento específica. Este artículo describen hello **actividad de U-SQL de análisis de datos Lake** que se ejecuta un **U-SQL** script en un **análisis de Azure Data Lake** servicio vinculado de proceso. 

> [!NOTE]
> Debe crear una cuenta de Azure Data Lake Analytics antes de crear una canalización con una actividad de U-SQL de este servicio. toolearn sobre análisis de Data Lake de Azure, consulte [empezar a trabajar con análisis de Azure Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Hola de revisión [crear su primer tutorial de canalización](data-factory-build-your-first-pipeline.md) para conocer los pasos detallados toocreate una factoría de datos, servicios vinculados, conjuntos de datos y una canalización. Usar fragmentos de JSON con el Editor de generador de datos o entidades de factoría de datos de toocreate de Visual Studio o PowerShell de Azure.

## <a name="supported-authentication-types"></a>Tipos de autenticación que se admiten
La actividad de U-SQL admite siguientes tipos de autenticación frente a Data Lake Analytics:
* Autenticación de entidad de servicio
* Autenticación de credenciales de usuario (OAuth) 

Se recomienda usar la autenticación de la entidad de servicio, en especial para una ejecución de U-SQL. Con la autenticación se credenciales de usuario puede darse la situación de que expiren los tokens. Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#azure-data-lake-analytics-linked-service) sección.

## <a name="azure-data-lake-analytics-linked-service"></a>Servicio vinculado con el Análisis con Azure Data Lake
Crear un **análisis de Azure Data Lake** vinculado toolink un generador de datos de Azure análisis de Azure Data Lake tooan de servicio de proceso de servicio. actividad de Data Lake Analytics U-SQL en la canalización de Hola Hola hace referencia servicio toothis vinculado. 

Hello tabla siguiente ofrece descripciones de hello genéricos propiedades utilizadas en hello definición de JSON. Puede elegir entre la autenticación de la entidad de servicio y la autenticación de credenciales de usuario.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| **type** |propiedad de tipo Hello debe establecerse en: **AzureDataLakeAnalytics**. |Sí |
| **accountName** |Nombre de la cuenta de Análisis de Azure Data Lake |Sí |
| **dataLakeAnalyticsUri** |Identificador URI de Análisis de Azure Data Lake. |No |
| **subscriptionId** |Identificador de suscripción de Azure |No (si no se especifica, suscripción de Hola se usa la factoría de datos). |
| **resourceGroupName** |Nombre del grupo de recursos de Azure. |No (si no se especifica, el grupo de recursos de Hola se usa la factoría de datos). |

### <a name="service-principal-authentication-recommended"></a>Autenticación de la entidad de servicio (recomendada)
toouse autenticación principal del servicio, registrar una entidad de la aplicación en Azure Active Directory (Azure AD) y conceda a Hola acceso tooData Lake almacén. Consulte [Autenticación entre servicios](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) para ver los pasos detallados. Tome nota de hello después de valores, que se utiliza toodefine Hola servicio vinculado:
* Identificador de aplicación
* Clave de la aplicación 
* Id. de inquilino

Utilizar autenticación de entidad de seguridad de servicio mediante la especificación de hello propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **servicePrincipalId** | Especifique el identificador de cliente de. la aplicación hello | Sí |
| **servicePrincipalKey** | Especifique la clave de la aplicación hello. | Sí |
| **tenant** | Especifique la información de inquilino de hello (inquilino o el nombre de identificador de dominio) en que se encuentra la aplicación. Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello portal de Azure. | Sí |

**Ejemplo: autenticación de la entidad de servicio**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticación de credenciales de usuario
Como alternativa, puede usar la autenticación de credenciales de usuario para el análisis de Data Lake especificando Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **authorization** | Haga clic en hello **Authorize** botón Hola Editor de generador de datos y escriba sus credenciales que asigna la propiedad de hello autogenerado autorización URL toothis. | Sí |
| **sessionId** | Identificador de sesión de OAuth de sesión de autorización de OAuth de Hola. Cada id. de sesión es único y solo se puede usar una vez. Esta configuración se genera automáticamente cuando se usa Hola Editor de generador de datos. | Sí |

**Ejemplo: autenticación de credenciales de usuario**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiración del token
Hola código de autorización ha generado mediante el uso de hello **Authorize** botón expira después de unos minutos. Vea hello en la tabla siguiente para unos tiempos de expiración Hola para diferentes tipos de cuentas de usuario. Es posible que vea Hola mensaje de error siguiente cuando Hola autenticación **expira el token**: error de operación de credenciales: concesión_no_válida - AADSTS70002: Error al validar las credenciales. AADSTS70008: Hola proporciona concesión de acceso expiró o se revocó. Id. de seguimiento: d18629e8-af88-43c5-88e3-d8419eb1fca1 Id. de correlación: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Marca de tiempo: 2015-12-15 21:09:31Z

| Tipo de usuario | Expira después de |
|:--- |:--- |
| Cuentas de usuario NO administradas por Azure Active Directory (@hotmail.com, @live.com, etc.) |12 horas |
| Cuentas de usuario administradas por Azure Active Directory (AAD) |Ejecute 14 días después de último segmento de Hola. <br/><br/>Noventa días, si un segmento basado en el servicio vinculado basado en OAuth se ejecuta al menos una vez cada catorce días. |

tooavoid/resolve este error, volver a autorizar mediante hello **Authorize** botón cuando hello **expira el token** y vuelva a implementar el servicio de hello vinculado. También puede generar valores para las propiedades **sessionId** y **authorization** mediante programación, para lo que usará el código siguiente:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Vea [azuredatalakestorelinkedservice clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), y [AuthorizationSessionGetResponse clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) temas para obtener más información acerca de clases de factoría de datos de hello utilizadas en el código de hello. Agregue una referencia a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para hello WindowsFormsWebAuthenticationDialog clase. 

## <a name="data-lake-analytics-u-sql-activity"></a>Actividad U-SQL de Análisis de Data Lake
Hola siguiente fragmento JSON define una canalización con la actividad de U-SQL de análisis de datos Lake. definición de actividad de Hello tiene un servicio de análisis de Azure Data Lake vinculado que creó anteriormente toohello de referencia.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Hello tabla siguiente describen nombres y descripciones de propiedades de actividad toothis específico. 

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type |se debe establecer propiedad de tipo Hello demasiado**DataLakeAnalyticsU SQL**. |Sí |
| scriptPath |Toofolder de ruta de acceso que contiene el script de Hola U-SQL. Nombre del archivo hello distingue mayúsculas de minúsculas. |No (si se utiliza el script) |
| scriptLinkedService |Servicio vinculado que se vincula el almacenamiento de Hola que contiene la factoría de datos de hello script toohello |No (si se utiliza el script) |
| script |Especifique el script en línea en lugar de scriptPath y scriptLinkedService. Por ejemplo: `"script": "CREATE DATABASE test"`. |No (si usa scriptPath y scriptLinkedService) |
| degreeOfParallelism |número máximo de Hola de nodos simultáneamente utiliza trabajo de hello toorun. |No |
| prioridad |Determina qué trabajos de todos los que se ponen en cola deberían estar seleccionado toorun en primer lugar. Hola Hola número inferior, prioridad Hola Hola. |No |
| parameters |Parámetros de script de Hola U-SQL |No |
| runtimeVersion | Versión del Runtime de hello U-SQL motor toouse | No | 
| compilationMode | <p>Modo de compilación de U-SQL. Debe ser uno de los valores siguientes:</p> <ul><li>**Semantic:** solo realiza comprobaciones semánticas y comprobaciones de integridad necesarias.</li><li>**Completo:** realizar Hola completos de la compilación, incluida la comprobación de sintaxis, optimización, generación de código, etcetera.</li><li>**SingleBox:** realizar Hola completos de la compilación, con TargetType configuración tooSingleBox.</li></ul><p>Si no especifica un valor para esta propiedad, servidor hello determina el modo de compilación óptimo de Hola. </p>| No | 

Vea [SearchLogProcessing.txt Script definición](#sample-u-sql-script) para la definición de script de Hola. 

## <a name="sample-input-and-output-datasets"></a>Conjuntos de datos de entrada y salida de ejemplo
### <a name="input-dataset"></a>Conjunto de datos de entrada
En este ejemplo, los datos de entrada de hello residen en un almacén de Azure Data Lake (archivo de SearchLog.tsv de carpeta de entrada/datalake Hola). 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Conjunto de datos de salida
En este ejemplo, los datos de salida de hello generados por script U-SQL Hola se almacenan en un almacén de Azure Data Lake (carpeta de datalake/salida). 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Ejemplo de servicio vinculado de Data Lake Store
Aquí es definición de Hola de ejemplo de Hola a que almacén de Azure Data Lake vinculado servicio utilizado por los conjuntos de datos de entrada/salida de hello. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

Vea [mover tooand de datos de almacén de Azure Data Lake](data-factory-azure-datalake-connector.md) artículo para obtener descripciones de propiedades JSON. 

## <a name="sample-u-sql-script"></a>Script U-SQL

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

Hola valores para  **@in**  y  **@out**  parámetros en el script de Hola U-SQL se pasan dinámicamente por ADF mediante hello 'parameters' sección. Vea la sección de "parámetros" de hello en la definición de la canalización de Hola.

También puede especificar otras propiedades, como degreeOfParallelism y la prioridad en la definición de canalización para los trabajos de Hola que se ejecutan en el servicio de análisis de Azure Data Lake Hola.

## <a name="dynamic-parameters"></a>Parámetros dinámicos
En la definición de la canalización de ejemplo de Hola, los parámetros de entrada y salida se asignan con valores codificados de forma rígida. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

Es posible toouse los parámetros dinámicos en su lugar. Por ejemplo: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

En este caso, todavía se recogen los archivos de entrada desde la carpeta de /datalake/input de Hola y archivos de salida se generan en la carpeta de /datalake/output Hola. nombres de archivo de Hello son dinámicos en función de la hora de inicio del segmento de Hola.  

