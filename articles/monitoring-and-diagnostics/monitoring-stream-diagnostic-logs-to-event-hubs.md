---
title: "aaaStream registros de diagnóstico de Azure tooan Namespace de concentradores de eventos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toostream diagnóstico de Azure registra el espacio de nombres de tooan centros de eventos."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Transmitir tooan Namespace de concentradores de eventos de registros de diagnóstico de Azure
**[Registros de diagnóstico de Azure](monitoring-overview-of-diagnostic-logs.md)**  se puede transmitir cerca de la aplicación de tooany de en tiempo real mediante la opción "Exportación tooEvent concentradores" integrada Hola Hola Portal o habilitando Hola Id. de regla de Bus de servicio en una configuración de diagnóstico a través de hello Azure PowerShell CLI de Azure o cmdlets.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Qué se puede hacer con registros de diagnóstico y Event Hubs
Aquí se muestran unos pocos maneras puede usar Hola capacidad de streaming para registros de diagnóstico:

* **Secuencia de registros de sistemas de registro y telemetría de terceros too3rd** – con el tiempo, los concentradores de eventos de transmisión por secuencias se convertirá en hello mecanismo toopipe los registros de diagnóstico de SIEM toothird terceros y soluciones de análisis de registro.
* **Ver estado del servicio de transmisión por secuencias "ruta de acceso activa" datos tooPowerBI** : uso y centros de eventos, análisis de transmisiones, Power BI, puede transformar fácilmente los datos de diagnóstico en toonear de información en tiempo real en los servicios de Azure. [Este artículo de documentación ofrece una excelente introducción de cómo procesar datos con análisis de transmisiones tooset los concentradores de eventos y usar Power BI como una salida de](../stream-analytics/stream-analytics-power-bi-dashboard.md). Estas son algunas recomendaciones para la configuración con los registros de diagnóstico:
  
  * Un concentrador de eventos para una categoría de registros de diagnóstico se crea automáticamente cuando compruebe la opción de hello en el portal de Hola o habilitarlo mediante PowerShell, por lo que desee tooselect concentrador de eventos de hello en hello espacio de nombres con el nombre de hello comienza con **visión**.
  * Hola después el código SQL es un ejemplo de análisis de transmisiones de consulta que puede usar todos los datos de registro de hello tooparse en la tabla de PowerBI tooa:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Crear una plataforma de registro y telemetría personalizada** : si ya dispone de una plataforma de telemetría personalizada o son solo pensar en uno, Hola altamente escalable publicación / suscripción de edificio naturaleza de los centros de eventos permite tooflexibly introducir diagnóstico registros. [Consulte toousing de guía de Dan Rosanova centros de eventos en una plataforma de telemetría de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Habilitación del streaming de registros de diagnóstico
Puede habilitar la transmisión por secuencias de registros de diagnóstico mediante programación, mediante el portal de hello, o utilizando hello [API de REST de Azure Monitor](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). En cualquier caso, cree una configuración de diagnóstico en el que puede especificar un espacio de nombres de los centros de eventos y categorías de registro de hello y métricas que desee toosend en el espacio de nombres de toohello. Un concentrador de eventos se crea en el espacio de nombres de Hola para cada categoría de registro que se habilita. Una **categoría de registro** de diagnóstico es un tipo de registro que un recurso puede recopilar.

> [!WARNING]
> La habilitación y streaming de registros de diagnóstico desde recursos de proceso (por ejemplo, máquinas virtuales o Service Fabric) [requiere ejecutar una serie de pasos distinta](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Hola Bus de servicio o concentradores de eventos del espacio de nombres no tiene toobe en Hola misma suscripción como recurso de hello emitir registros como usuario de Hola que configura los valores de hello tiene suscripciones de tooboth de acceso RBAC adecuadas.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Registros de diagnóstico de la secuencia mediante el portal de Hola
1. En el portal de hello, navegue tooAzure Monitor y haga clic en **configuración de diagnóstico**

    ![Sección de supervisión de Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Si lo desea Hola lista Filtrar por tipo de recurso o grupo de recursos, a continuación, haga clic en el recurso de hello para el que le gustaría tooset una configuración de diagnóstico.

3. Si ninguna configuración existe en el recurso de Hola que ha seleccionado, son toocreate solicitada una configuración. Haga clic en "Activar diagnóstico".

   ![Agregar configuración de diagnóstico: sin configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Si hay una configuración existente en el recurso de hello, verá una lista de configuraciones ya configurado en este recurso. Haga clic en "Agregar configuración de diagnóstico".

   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Asigne un nombre de su configuración y casilla hello para **concentrador de eventos de flujo tooan**, a continuación, seleccione un espacio de nombres de los centros de eventos.
   
   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Hello espacio de nombres seleccionado será donde se crea (si se trata de la primera vez que los registros de diagnóstico de streaming) o se transmiten demasiado concentrador de eventos de hello (si ya hay recursos que están transmitiendo por secuencias ese espacio de nombres de toothis de categoría de registro), y la directiva de hello define Hola permisos que tiene el mecanismo de transmisión por secuencias de Hola. En la actualidad, streaming tooan concentrador de eventos requiere permisos de administración, envío y escuchar. Puede crear o modificar directivas de acceso de espacio de nombres compartido centros de eventos en el portal de hello en la ficha configurar de hello para el espacio de nombres. tooupdate uno de estos valores de diagnóstico, el cliente hello debe tener permiso de ListKey de hello en la regla de autorización de los centros de eventos de Hola.

4. Haga clic en **Guardar**.

Transcurridos unos instantes, nueva configuración de hello aparece en la lista de valores para este recurso y registros de diagnóstico se transmiten cuenta de almacenamiento toothat tan pronto como se generan nuevos datos de evento.

### <a name="via-powershell-cmdlets"></a>Mediante cmdlets de PowerShell
tooenable transmisión por secuencias a través de hello [Cmdlets de PowerShell de Azure](insights-powershell-samples.md), puede usar hello `Set-AzureRmDiagnosticSetting` cmdlet con estos parámetros:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Hola Id. de regla de Bus de servicio es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`, por ejemplo, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>Mediante la CLI de Azure
tooenable transmisión por secuencias a través de hello [CLI de Azure](insights-cli-samples.md), puede usar hello `insights diagnostic set` comando similar al siguiente:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Usar hello mismo formato para el Id. de regla de Bus de servicio, como se explica para hello Cmdlet de PowerShell.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>¿Cómo se puede consumir datos de registro de hello de centros de eventos?
Estos son datos de salida de ejemplo de Event Hubs:

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Nombre del elemento | Description |
| --- | --- |
| records |Matriz de todos los eventos de registro de esta carga. |
| Twitter en tiempo |Hora en que hello evento se produjo. |
| categoría |Categoría de registro para este evento. |
| resourceId |Id. de recurso del recurso de Hola que generó este evento. |
| operationName |Nombre de operación de Hola. |
| level |Opcional. Indica el nivel de registro de eventos de Hola. |
| propiedades |Propiedades de evento de Hola. |

Puede ver una lista de todos los proveedores de recursos que admiten la transmisión por secuencias concentradores tooEvent [aquí](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Transmisión de datos de Recursos de proceso
También puede transmitir los registros de diagnóstico de recursos de proceso con el agente de hello diagnósticos de Windows Azure. [Consulte este artículo](../event-hubs/event-hubs-streaming-azure-diags-data.md) para saber cómo tooset esa copia.

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre los registros de Diagnósticos de Azure](monitoring-overview-of-diagnostic-logs.md)
* [Introducción a los Centros de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

