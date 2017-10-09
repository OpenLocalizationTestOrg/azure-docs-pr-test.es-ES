---
title: "registros de diagnóstico de aaaViewing de almacén de Azure Data Lake | Documentos de Microsoft"
description: "Comprender cómo toosetup y acceso a registros de diagnóstico de almacén de Azure Data Lake "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Acceso a los registros de diagnóstico de Azure Data Lake Store
Obtenga información acerca de cómo se recopila tooenable el registro de diagnóstico para su cuenta de almacén de Data Lake y funcionamiento de los registros tooview Hola para su cuenta.

Las organizaciones pueden habilitar el registro de diagnóstico para su almacén de Azure Data Lake cuenta toocollect datos acceso a los seguimientos de auditoría que proporciona información como la lista de usuarios que acceden a datos de hello, con qué frecuencia se tiene acceso a datos de hello, la cantidad de datos se almacena en hello cuenta, etcetera.

## <a name="prerequisites"></a>Requisitos previos
* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Cuenta del Almacén de Azure Data Lake**. Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Habilitar el registro de diagnósticos en la cuenta de Data Lake Store
1. Inicio de sesión toohello nueva [Portal de Azure](https://portal.azure.com).
2. Abra la cuenta de Data Lake Store y, en la hoja de la cuenta de Data Lake Store, haga clic en **Configuración** y en **Registros de diagnóstico**.
3. Hola **registros de diagnóstico** hoja, haga clic en **Activar diagnósticos**.

    ![Habilitar el registro de diagnóstico](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Habilitar registros de diagnóstico")

3. Hola **diagnóstico** hoja, que Hola después de registro de diagnóstico de tooconfigure de cambios.
   
    ![Habilitar el registro de diagnóstico](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Habilitar registros de diagnóstico")
   
   * Establecer **estado** demasiado**en** tooenable el registro de diagnóstico.
   * Puede elegir datos hello toostore o proceso de maneras diferentes.
     
        * Seleccione la opción de hello demasiado**tooa cuenta de almacenamiento de archivo** toostore registros tooan cuenta de almacenamiento de Azure. Utilice esta opción si desea que los datos de hello tooarchive que será procesado por lotes en una fecha posterior. Si selecciona esta opción debe proporcionar una cuenta de almacenamiento de Azure toosave registros Hola.
        
        * Seleccione la opción de hello demasiado**concentrador de eventos de flujo tooan** tooan de datos de registro de toostream centro de eventos de Azure. Probablemente utilizará esta opción si tiene un procesamiento en dirección descendente tooanalyze registros entrantes en tiempo real de la canalización. Si selecciona esta opción, debe proporcionar detalles de Hola para hello concentrador de eventos de Azure que desee toouse.

        * Seleccione también la opción de hello**enviar tooLog análisis** toouse Hola datos de registro de análisis de registros de Azure servicio tooanalyze Hola generado. Si selecciona esta opción, debe proporcionar Hola detalles para el área de trabajo de hello Operations Management Suite que realizaría Hola usar análisis de registros.
     
   * Especifique si desea que los registros de auditoría tooget, registros de solicitudes o ambos.
   * Especifique el número de Hola de días para el que se deben conservar los datos de Hola. Retención solo es aplicable si usa datos de registro de tooarchive de cuenta de almacenamiento de Azure.
   * Haga clic en **Guardar**.

Una vez que se ha habilitado la configuración de diagnóstico, puede ver registros de Hola Hola **registros de diagnóstico** ficha.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Ver registros de diagnóstico de la cuenta de Data Lake Store
Hay dos formas de datos de registro de hello tooview para su cuenta de almacén de Data Lake.

* Desde la cuenta de almacén de Data Lake Hola ver configuración
* De cuenta de almacenamiento de Azure de Hola donde se almacenan los datos de Hola

### <a name="using-hello-data-lake-store-settings-view"></a>Con hello ver la configuración del almacén de datos Lake
1. En la hoja **Configuración** de su cuenta de Data Lake Store, haga clic en **Registros de diagnóstico**.
   
    ![Ver registro de diagnóstico](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Ver registros de diagnóstico") 
2. Hola **registros de diagnóstico** hoja, debería ver los registros de hello clasificados por **los registros de auditoría** y **los registros de solicitudes**.
   
   * Registros de solicitudes de captura todas las solicitudes API realizadas en hello cuenta de almacén de Data Lake.
   * Registros de auditoría son registros de toorequest similares pero proporcionan un análisis mucho más detallado de las operaciones de Hola se realiza en la cuenta de almacén de Data Lake Hola. Por ejemplo, podría dar lugar a una llamada de API de carga única en los registros de solicitud en varias operaciones de "Agregar" en los registros de auditoría de Hola.
3. Haga clic en hello **descargar** registros de hello toodownload de entrada de registro de vínculo en todas.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>De hello cuenta de almacenamiento de Azure contiene datos del registro
1. Abra la hoja de cuenta de almacenamiento de Azure Hola asociado con el almacén de Data Lake para el registro y, a continuación, haga clic en Blobs. Hola **servicio Blob** hoja muestra dos contenedores.
   
    ![Ver registro de diagnóstico](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Ver registros de diagnóstico")
   
   * contenedor de Hello **auditoría de registros de visión** contiene registros de auditoría de Hola.
   * contenedor de Hello **las solicitudes de registros de visión** contiene registros de solicitudes de Hola.
2. Dentro de estos contenedores, registros de Hola se almacenan en hello siguiendo la estructura.
   
    ![Ver registro de diagnóstico](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Ver registros de diagnóstico")
   
    Por ejemplo, podría ser el registro de auditoría de tooan de ruta de acceso completa de Hola`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Registro de solicitudes de tooa de ruta de acceso completa de hello similar, podría ser`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Comprender la estructura de Hola Hola de datos de registro
Hello registros de auditoría y solicitud están en un formato JSON. En esta sección, consultamos estructura Hola de JSON para la solicitud y los registros de auditoría.

### <a name="request-logs"></a>Request Logs
Este es un ejemplo de entrada en el registro de solicitudes con formato JSON de Hola. Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Esquema de un registro de solicitud
| Nombre | Tipo | Description |
| --- | --- | --- |
| Twitter en tiempo |String |Hola marca de tiempo (en UTC) del registro de hello |
| resourceId |String |Id. de Hello del recurso de Hola que realizó la operación de colocar en |
| categoría |String |categoría de registro de Hello. Por ejemplo, **Requests**. |
| operationName |String |Nombre de operación de Hola que inició sesión. Por ejemplo, getfilestatus. |
| resultType |String |estado de Hola de operación de hello, por ejemplo, 200. |
| callerIpAddress |String |dirección IP de Hola de cliente de Hola que realiza la solicitud de Hola |
| correlationId |String |Id. de Hello del registro de hello que puede usar toogroup conjuntamente un conjunto de entradas de registro relacionadas |
| identidad |Objeto |identidad de Hola que generó el registro de hello |
| propiedades |JSON |Vea más abajo para obtener más información. |

#### <a name="request-log-properties-schema"></a>Esquema de propiedades de un registro de solicitud
| Nombre | Tipo | Description |
| --- | --- | --- |
| HttpMethod |String |Hello método HTTP utilizado para la operación de Hola. Por ejemplo, GET. |
| Ruta de acceso |String |se realizó la operación de Hola de ruta de acceso de Hello en |
| RequestContentLength |int |longitud del contenido Hola de solicitud de hello HTTP |
| ClientRequestId |String |Hola Id. que identifica esta solicitud |
| StartTime |String |hora de Hello en qué servidor recibido una petición Hola Hola |
| EndTime |String |tiempo de Hello en qué Hola servidor envió una respuesta |

### <a name="audit-logs"></a>Registros de auditoría
Este es un ejemplo de entrada en el registro de auditoría con formato JSON de Hola. Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Esquema de un registro de auditoría
| Nombre | Tipo | Description |
| --- | --- | --- |
| Twitter en tiempo |String |Hola marca de tiempo (en UTC) del registro de hello |
| resourceId |String |Id. de Hello del recurso de Hola que realizó la operación de colocar en |
| categoría |String |categoría de registro de Hello. Por ejemplo, **Audit**. |
| operationName |String |Nombre de operación de Hola que inició sesión. Por ejemplo, getfilestatus. |
| resultType |String |estado de Hola de operación de hello, por ejemplo, 200. |
| correlationId |String |Id. de Hello del registro de hello que puede usar toogroup conjuntamente un conjunto de entradas de registro relacionadas |
| identidad |Objeto |identidad de Hola que generó el registro de hello |
| propiedades |JSON |Vea más abajo para obtener más información. |

#### <a name="audit-log-properties-schema"></a>Esquema de propiedades de un registro de auditoría
| Nombre | Tipo | Description |
| --- | --- | --- |
| StreamName |String |se realizó la operación de Hola de ruta de acceso de Hello en |

## <a name="samples-tooprocess-hello-log-data"></a>Datos de registro de hello ejemplos tooprocess
Almacén de Data Lake de Azure proporciona un ejemplo sobre cómo tooprocess y analizar los datos de registro de saludo. Puede encontrar el ejemplo hello en [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Otras referencias
* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)

