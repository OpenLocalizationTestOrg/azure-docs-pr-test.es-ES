---
title: "registros de diagnóstico de aaaViewing de análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Comprender el funcionamiento toosetup y diagnóstico de acceso de los registros de datos de Azure análisis Lake "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Acceso a los registros de diagnóstico de Azure Data Lake Analytics

Registro de diagnóstico le permite los seguimientos de auditoría de acceso de datos de toocollect. Estos registros proporcionan información como:

* Una lista de usuarios que tiene acceso a datos de Hola.
* Con qué frecuencia se tiene acceso a datos de Hola.
* La cantidad de datos se almacena en la cuenta de hello.

## <a name="enable-logging"></a>Habilitación del registro

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).

2. Abra su cuenta de análisis de Data Lake y seleccione **registros de diagnóstico** de hello __Monitor__ sección. Después, seleccione __Activar diagnósticos__.

    ![Activar la auditoría de toocollect de diagnóstico y registros de solicitudes](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. De __configuración de diagnóstico__, establezca too__On__ de estado de Hola y seleccionar opciones de registro.

    ![Activar la auditoría de toocollect de diagnóstico y registros de solicitudes](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "habilitar registros de diagnóstico")

   * Establecer **estado** demasiado**en** tooenable el registro de diagnóstico.

   * Puede elegir datos hello toostore o proceso de tres maneras diferentes.

     * Seleccione __tooa cuenta de almacenamiento de archivo__ toostore se registra en una cuenta de almacenamiento de Azure. Utilice esta opción si desea que los datos de hello tooarchive. Si selecciona esta opción, debe proporcionar un almacenamiento de Azure cuenta toosave Hola los registros a.

     * Seleccione **tooan concentrador de eventos de secuencia** tooan de datos de registro de toostream centro de eventos de Azure. Use esta opción si tiene una canalización de procesamiento de bajada que está analizando los registros entrantes en tiempo real. Si selecciona esta opción, debe proporcionar detalles de Hola para hello concentrador de eventos de Azure que desee toouse.

     * Seleccione __enviar tooLog análisis__ toosend Hola datos toohello servicio de análisis de registros. Utilice esta opción si desea toouse toogather de análisis de registros y analizar los registros.
   * Especifique si desea que los registros de auditoría tooget, registros de solicitudes o ambos.  Un registro de solicitudes captura todas las solicitudes de API. Un registro de auditoría registra todas las operaciones que esa solicitud de API desencadena.

   * Para __tooa cuenta de almacenamiento de archivo__, especificar número de Hola de datos de hello tooretain días.

   * Haga clic en __Guardar__.

        > [!NOTE]
        > Debe seleccionar __tooa cuenta de almacenamiento de archivo__, __tooan concentrador de eventos de secuencia__ o __enviar tooLog análisis__ antes de hacer clic hello __guardar__botón.

Una vez que se ha habilitado la configuración de diagnóstico, puede devolver toohello __registros de diagnóstico__ hoja tooview Hola registros.

## <a name="view-logs"></a>Ver registros

### <a name="use-hello-data-lake-analytics-view"></a>Utilizar la vista de análisis de Data Lake Hola

1. En el análisis de Data Lake cuenta hoja, en **supervisión**, seleccione **registros de diagnóstico** y, a continuación, seleccione los registros para un toodisplay de entrada.

    ![Ver registro de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Ver registros de diagnóstico")

2. Hello registros se dividen por categorías **los registros de auditoría** y **los registros de solicitudes**.

    ![entradas del registro](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * Registros de solicitudes de captura todas las solicitudes API realizadas en hello cuenta de análisis de Data Lake.
   * Registros de auditoría son registros de toorequest similar pero proporciona un desglose de las operaciones de hello mucho más detallado. Por ejemplo, una llamada de API de carga única en un registro de solicitud podría producir varias operaciones "Append" en el registro de auditoría correspondiente.

3. Haga clic en hello **descargar** vínculo para un toodownload de entrada de registro que inicie sesión.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Usar cuenta de almacenamiento de Azure de Hola que contiene datos del registro

1. Abra la hoja de cuenta de almacenamiento de Azure Hola asociado con análisis de Data Lake para el registro y, a continuación, haga clic en __Blobs__. Hola **servicio Blob** hoja muestra dos contenedores.

    ![Ver registro de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Ver registros de diagnóstico")

   * contenedor de Hello **auditoría de registros de visión** contiene registros de auditoría de Hola.
   * contenedor de Hello **las solicitudes de registros de visión** contiene registros de solicitudes de Hola.
2. Dentro de estos contenedores, Hola registros se almacenan en hello siguiente estructura:

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > Hola `##` las entradas de ruta de acceso de hello contengan Hola año, mes, día y hora en que Hola se creó el registro. Data Lake Analytics crea un archivo cada hora, por lo que `m=` siempre contiene un valor de `00`.

    Por ejemplo, podría ser el registro de auditoría de tooan de ruta de acceso completa de hello:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    De igual forma, podría ser el registro de solicitudes de tooa de ruta de acceso completa de hello:

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Estructura de los registros

Hello registros de auditoría y solicitud están en un formato estructurado de JSON.

### <a name="request-logs"></a>Request Logs

Este es un ejemplo de entrada en el registro de solicitudes con formato JSON de Hola. Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Esquema de un registro de solicitud

| Nombre | Tipo | Description |
| --- | --- | --- |
| Twitter en tiempo |String |Hola marca de tiempo (en UTC) del registro de hello |
| resourceId |String |identificador de Hello del recurso de Hola que realizó la operación de colocar en |
| categoría |String |categoría de registro de Hello. Por ejemplo, **Requests**. |
| operationName |String |Nombre de operación de Hola que inició sesión. Por ejemplo, GetAggregatedJobHistory. |
| resultType |String |estado de Hola de operación de hello, por ejemplo, 200. |
| callerIpAddress |String |dirección IP de Hola de cliente de Hola que realiza la solicitud de Hola |
| correlationId |String |identificador de Hello del registro de hello. Este valor puede ser toogroup usa un conjunto de entradas de registro relacionadas. |
| identidad |Objeto |identidad de Hola que generó el registro de hello |
| propiedades |JSON |Consulte la sección siguiente hello (esquema de propiedades de registro de solicitud) para obtener más información |

#### <a name="request-log-properties-schema"></a>Esquema de propiedades de un registro de solicitud

| Nombre | Tipo | Description |
| --- | --- | --- |
| HttpMethod |String |Hello método HTTP utilizado para la operación de Hola. Por ejemplo, GET. |
| Ruta de acceso |String |se realizó la operación de Hola de ruta de acceso de Hello en |
| RequestContentLength |int |longitud del contenido Hola de solicitud de hello HTTP |
| ClientRequestId |String |Hola identificador que identifica de forma única esta solicitud |
| StartTime |String |hora de Hello en qué servidor recibido una petición Hola Hola |
| EndTime |String |tiempo de Hello en qué Hola servidor envió una respuesta |

### <a name="audit-logs"></a>Registros de auditoría

Este es un ejemplo de entrada en el registro de auditoría con formato JSON de Hola. Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Esquema de un registro de auditoría

| Nombre | Tipo | Description |
| --- | --- | --- |
| Twitter en tiempo |String |Hola marca de tiempo (en UTC) del registro de hello |
| resourceId |String |identificador de Hello del recurso de Hola que realizó la operación de colocar en |
| categoría |String |categoría de registro de Hello. Por ejemplo, **Audit**. |
| operationName |String |Nombre de operación de Hola que inició sesión. Por ejemplo, JobSubmitted. |
| resultType |String |Un subestado del estado del trabajo hello (operationName). |
| resultSignature |String |Obtener más detalles sobre el estado del trabajo de hello (operationName). |
| identidad |String |usuario de Hola que solicitó la operación de Hola. Por ejemplo: susan@contoso.com. |
| propiedades |JSON |Consulte la sección siguiente hello (esquema de propiedades de registro de auditoría) para obtener más información |

> [!NOTE]
> **resultType** y **resultSignature** proporcionan información sobre el resultado de hello de una operación y solo contiene un valor si se ha completado una operación. Por ejemplo, solo contienen un valor cuando **operationName** contiene un valor de **JobStarted** o **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Esquema de propiedades de un registro de auditoría

| Nombre | Tipo | Description |
| --- | --- | --- |
| JobId |String |trabajo de Hello Id. asignado toohello |
| JobName |String |nombre de Hola que se especificó para el trabajo de Hola |
| JobRunTime |String |en tiempo de ejecución de Hello usa trabajos de hello tooprocess |
| SubmitTime |String |tiempo de presentación (en UTC) que el trabajo de hello envió |
| StartTime |String |trabajo Hola Hola empezó a ejecutarse después del envío (en UTC) |
| EndTime |String |finalizó el trabajo Hola Hola |
| Paralelismo |String |número de Hola de unidades de análisis de Data Lake solicitadas para este trabajo durante el envío |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime** y **Parallelism** proporcionan información sobre una operación. Estas entradas solo contienen un valor si la operación se ha iniciado o completado. Por ejemplo, **SubmitTime** sólo contiene un valor una vez **operationName** tiene el valor de hello **JobSubmitted**.

## <a name="process-hello-log-data"></a>Datos del registro de hello procesos

Análisis de Azure Data Lake proporciona un ejemplo sobre cómo tooprocess y analizar los datos de registro de saludo. Puede encontrar el ejemplo hello en [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Pasos siguientes
* [Información general de Azure Data Lake Analytics](data-lake-analytics-overview.md)
