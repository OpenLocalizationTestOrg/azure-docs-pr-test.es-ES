---
title: estado de aaaCheck, configurar el registro y reciba alertas - Azure Logic Apps | Documentos de Microsoft
description: "Supervise el estado y el rendimiento de aplicaciones lógicas, registre datos de diagnóstico y configure alertas"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>Supervisar el estado, configurar el registro de diagnósticos y activar alertas para Azure Logic Apps

Después de [crear y ejecutar una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md), puede comprobar su historial de ejecuciones, historial de desencadenadores, estado y rendimiento. Para la supervisión de eventos en tiempo real y una depuración más rica, configure el [registro de diagnósticos](#azure-diagnostics) de la aplicación lógica. De este modo, puede [buscar y ver eventos](#find-events), como eventos de desencadenador, eventos de ejecución y eventos de acción. También puede usar estos [datos de diagnóstico con otros servicios](#extend-diagnostic-data), como Azure Storage y Azure Event Hubs. 

Configurar notificaciones de tooget sobre errores u otros problemas posibles, [alertas](#add-azure-alerts). Por ejemplo, puede crear una alerta que detecte "cuando se produzcan errores en más de cinco ejecuciones en una hora". También puede configurar la supervisión, el seguimiento y el registro mediante programación con la [configuración de eventos y las propiedades de Azure Diagnostics](#diagnostic-event-properties).

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>Visualización del historial de ejecuciones y desencadenadores de la aplicación lógica

1. toofind la aplicación lógica en hello [portal de Azure](https://portal.azure.com), en Hola menú principal de Azure, elija **más servicios**. En el cuadro de búsqueda de hello, busque "logic apps" y elija **aplicaciones lógicas**.

   ![Búsqueda de la aplicación lógica](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   Hola portal de Azure muestra todas las aplicaciones de la lógica de Hola que están asociadas a su suscripción de Azure. 

2. Seleccione la aplicación lógica y luego elija **Información general**.

   Hola portal de Azure muestra el historial de ejecuciones de Hola y el historial de desencadenador para la aplicación lógica. Por ejemplo:

   ![Historial de ejecuciones e historial de desencadenadores de la aplicación lógica](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **Se ejecuta historial** muestra todas las ejecuciones de hello para la aplicación lógica. 
   * **Desencadenar historial** muestra todas las actividades de desencadenador de hello para la aplicación lógica.

   Para obtener descripciones de estado, vea [Diagnóstico de errores en las aplicaciones lógicas](../logic-apps/logic-apps-diagnosing-failures.md).

   > [!TIP]
   > Si no encuentra datos Hola que espera, en la barra de herramientas de hello, elija **actualizar**.

3. Hola tooview los pasos de una ejecución específica, en **ejecuta historial**, seleccione que se ejecutan. 

   vista de monitor de Hello muestra cada paso en el que se ejecutan. Por ejemplo:

   ![Acciones de una ejecución concreta](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. tooget más detalles sobre Hola ejecutar, elija **detalles de la ejecución**. Esta información resume los pasos de hello, estado, entradas y salidas de hello ejecutan. 

   ![Selección de "Detalles de ejecución"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   Por ejemplo, puede obtener Hola de ejecución **Id. de correlación**, que pueden requerir cuando usas hello [API de REST para las aplicaciones lógicas](https://docs.microsoft.com/rest/api/logic).

5. tooget obtener más información acerca de un paso concreto, elija ese paso. Ahora puede revisar detalles como las entradas, las salidas y los errores acontecidos en ese paso. Por ejemplo:

   ![Detalles del paso](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Todos los detalles de tiempo de ejecución y eventos se cifran en hello servicio Logic Apps. Se descifran solo cuando un usuario solicita tooview esos datos. También puede controlar eventos de acceso a toothese con [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).

6. detalles de tooget sobre un evento de desencadenador específico, vuelva atrás toohello **Introducción** panel. En **desencadenar historial**, seleccione los eventos de desencadenador de Hola. Ahora puede revisar detalles como las entradas y salidas, por ejemplo:

   ![Detalles de salida de evento de desencadenador](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>Activación del registro de diagnósticos de la aplicación lógica

Para una depuración más rica con detalles y eventos de runtime, puede configurar el registro de diagnósticos con [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Análisis de registros es un servicio en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) que supervisa la nube y locales toohelp entornos mantener su disponibilidad y rendimiento. 

Antes de empezar, deberá toohave un área de trabajo OMS. Obtenga información acerca de [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).

1. Hola [portal de Azure](https://portal.azure.com), busque y seleccione la aplicación lógica. 

2. En el menú de hoja de la aplicación de lógica hello, en **supervisión**, elija **diagnósticos** > **configuración de diagnóstico**.

   ![Vaya a configuración de diagnóstico de tooMonitoring, diagnósticos,](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. En **Configuración de diagnóstico**, elija **Activado**.

   ![Activación de los registros de diagnóstico](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. Ahora seleccione categoría de evento y el área de trabajo OMS de hello para el registro como se muestra:

   1. Seleccione **enviar tooLog análisis**. 
   2. En **Log Analytics**, elija **Configurar**. 
   3. En **áreas de trabajo de OMS**, seleccione toouse de área de trabajo OMS de hello para el registro.
   4. En **registro**, seleccione hello **WorkflowRuntime** categoría.
   5. Elija el intervalo de métrica de saludo.
   6. Cuando termine, seleccione **Guardar**.

   ![Selección del área de trabajo de OMS y los datos para el registro](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

Ahora puede buscar eventos y otros datos de los eventos de desencadenador, los eventos de ejecución y los eventos de acción.

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>Búsqueda de eventos y datos de la aplicación lógica

toofind y ver los eventos en la aplicación lógica, como eventos de desencadenador, ejecute los eventos y los eventos de acción, siguen estos pasos.

1. Hola [portal de Azure](https://portal.azure.com), elija **más servicios**. Busque "log analytics" y luego elija **Log Analytics** como se muestra aquí:

   ![Selección de "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. En **Log Analytics**, busque y seleccione el área de trabajo de OMS. 

   ![Selección del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. En **Administración**, elija **Portal de OMS**.

   ![Selección de "Portal de OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. En la página principal de OMS, seleccione **Búsqueda de registros**.

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   O bien

   ![En el menú OMS de hello, elija "Búsqueda de registros"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. En el cuadro de búsqueda de hello, especificar un campo que desea que toofind y presione **ENTRAR**. Cuando empiece a escribir, OMS le mostrará posibles coincidencias y operaciones que puede usar. 

   Por ejemplo, toofind Hola primeros 10 eventos que se produjeron, escriba y seleccione esta consulta de búsqueda: **categoría = WorkflowRuntime | top 10**

   ![Especificación de cadena de búsqueda](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   Obtenga más información sobre [cómo toofind datos de análisis de registros](../log-analytics/log-analytics-log-searches.md).

6. En la página de resultados de hello, en la barra de la izquierda hello, elija Hola período de tiempo que desea tooview.
Elija la consulta agregando un filtro de toorefine **+ agregar**.

   ![Selección del marco temporal de los resultados de la consulta](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. En **agregar filtros**, escriba el nombre de filtro de Hola para que pueda encontrar el filtro de Hola que desee. Seleccione el filtro de Hola y elija **+ agregar**.

   Este ejemplo usa hello word "status" toofind no pudo eventos bajo **AzureDiagnostics**.
   Hola aquí el filtro para **status_s** ya está seleccionado.

   ![Selección de filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. En la barra de la izquierda hello, seleccione el valor de filtro de Hola que desee toouse y elija **aplicar**.

   ![Selección del valor de filtro y de "Aplicar"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. Consulta de toohello devuelven ahora que va a compilar. La consulta se ha actualizado con el filtro y el valor seleccionados. Los resultados anteriores también se filtraron.

   ![Devolver tooyour consulta con los resultados filtrados](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. Elija de la consulta para un uso futuro, toosave **guardar**. Obtenga información acerca de [cómo toosave la consulta](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Extensión de cómo y dónde usa los datos de diagnóstico con otros servicios

Además de con Azure Log Analytics, puede usar los datos de diagnóstico de la aplicación lógica con otros servicios de Azure, por ejemplo: 

* [Archivar registros de Diagnósticos de Azure en Azure Storage](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Transmitir tooAzure centros de eventos de los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Luego puede obtener supervisión en tiempo real mediante la telemetría y los análisis de otros servicios, como [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) y [Power BI](../log-analytics/log-analytics-powerbi.md). Por ejemplo:

* [Datos de la secuencia de los centros de eventos tooStream análisis](../stream-analytics/stream-analytics-define-inputs.md)
* [Analizar datos que se están transmitiendo con Stream Analytics y crear un panel de análisis en tiempo real en Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

En función de las opciones de Hola que desee configurar, asegúrese de que se primera [crear una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) o [crear un concentrador de eventos Azure](../event-hubs/event-hubs-create.md). A continuación, seleccione opciones de Hola para donde desea que los datos de diagnóstico de toosend:

![Enviar datos tooAzure almacenamiento cuenta o evento de un centro](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Períodos de retención se aplican únicamente cuando elija toouse una cuenta de almacenamiento.

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>Configuración de alertas de la aplicación lógica

toomonitor determinadas métricas o superados umbrales para la aplicación lógica, configurar [alertas en Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md). Más información sobre [métricas de Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md). 

tooset las alertas sin [Azure Log Analytics](../log-analytics/log-analytics-overview.md), siga estos pasos. Para usar criterios y acciones de alerta más avanzados, [configure Log Analytics](#azure-diagnostics) también.

1. En el menú de hoja de la aplicación de lógica hello, en **supervisión**, elija **diagnósticos** > **reglas de alerta** > **Agregar alerta**tal y como se muestra aquí:

   ![Adición de una alerta de la aplicación lógica](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. En hello **agregar una regla de alerta** hoja, crear la alerta, como se muestra:

   1. En **Recurso**, seleccione la aplicación lógica si aún no está seleccionada. 
   2. Proporcione un nombre y una descripción para la alerta.
   3. Seleccione un **métrica** o evento que desee tootrack.
   4. Seleccione un **condición**, especifique un **umbral** de métrica de Hola y Hola seleccione **período** para la supervisión de esta métrica.
   5. Seleccione si toosend de correo de alerta de Hola. 
   6. Especificar ninguna otra dirección de correo electrónico para enviar alerta Hola. 
   También puede especificar una dirección URL del webhook que desee toosend Hola alert.

   Por ejemplo, esta regla envía una alerta cuando hay errores en cinco o más ejecuciones en una hora:

   ![Creación de regla de alerta de métrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> toorun una aplicación de la lógica de una alerta, puede incluir hello [desencadenador de solicitud](../connectors/connectors-native-reqres.md) en el flujo de trabajo, que le permite realizar tareas como en estos ejemplos:
> 
> * [Registrar tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [Enviar un texto](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [Agregar una cola de mensajes tooa](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Configuración de eventos y detalles de Azure Diagnostics

Cada evento de diagnóstico incluye detalles acerca de la aplicación lógica y ese evento, por ejemplo, el estado de hello, hora de inicio, hora de finalización y así sucesivamente. tooprogrammatically configurar la supervisión, el seguimiento y registro, unidad organizativa puede usar estos detalles con hello [API de REST para aplicaciones de Azure lógica](https://docs.microsoft.com/rest/api/logic) hello y [API de REST para diagnósticos de Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).

Por ejemplo, hello `ActionCompleted` evento tiene hello `clientTrackingId` y `trackedProperties` propiedades que puede usar para el seguimiento y supervisión:

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`: Si no siempre, Azure genera este Id. y correlaciona eventos a través de una aplicación de lógica que se ejecuta automáticamente, incluidos los flujos de trabajo anidados que se denominan de aplicación lógica de hello. Puede especificar manualmente este Id. de un desencadenador pasando un `x-ms-client-tracking-id` encabezado con el valor de identificador personalizado en la solicitud de desencadenador de Hola. Puede usar un desencadenador de solicitud, un desencadenador HTTP o un desencadenador de webhook.

* `trackedProperties`: tootrack entradas o salidas en datos de diagnóstico, puede agregar propiedades sometidas a seguimiento tooactions en definición de JSON de la aplicación lógica. Pueden realizar un seguimiento de propiedades sometidas a seguimiento únicamente una sola acción entradas y salidas, pero puede usar hello `correlation` propiedades de toocorrelate de eventos a través de acciones en una ejecución.

  tootrack una o varias propiedades, agregar hello `trackedProperties` hello y sección propiedades que desee toohello definición de acción. Por ejemplo, imagine que desea tootrack datos como un "identificador de pedido" en la telemetría:

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>Pasos siguientes

* [Creación de plantillas para administrar la implementación y liberación de aplicaciones lógicas](../logic-apps/logic-apps-create-deploy-template.md)
* [Escenarios B2B y comunicación con Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Supervisión de mensajes B2B](../logic-apps/logic-apps-monitor-b2b-message.md)