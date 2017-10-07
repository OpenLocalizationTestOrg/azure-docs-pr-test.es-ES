---
title: "registros de diagnóstico de los centros de eventos aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset los registros de diagnóstico de concentradores de eventos de Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a>Registros de diagnósticos de Event Hubs

Puede ver dos tipos de registros para Event Hubs de Azure:
* **[Registros de actividad](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Estos registros contienen información sobre las operaciones realizadas en un trabajo. registros de Hello siempre están habilitados.
* **[Registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Puede configurar registros de diagnóstico para obtener una vista más completa de todo lo que ocurre con un trabajo. Las actividades de la portada de registros de diagnóstico de tiempo de hello trabajo Hola se crea hasta que se elimina el trabajo de hello, incluidas las actualizaciones y las actividades que se producen mientras se ejecuta el trabajo de Hola.

## <a name="turn-on-diagnostic-logs"></a>Activación de los registros de diagnóstico
Los registros de diagnóstico están inhabilitados de forma predeterminada. registros de diagnóstico de tooenable:

1.  Hola [portal de Azure](https://portal.azure.com), en **supervisión + administración**, haga clic en **registros de diagnóstico**.

    ![Registros de toodiagnostic de navegación de hoja](./media/event-hubs-diagnostic-logs/image1.png)

2.  Haga clic en recurso de Hola que desee toomonitor.

3.  Haga clic en **Activar diagnóstico**.

    ![Activación de los registros de diagnósticos](./media/event-hubs-diagnostic-logs/image2.png)

4.  En **Estado**, haga clic en **Activado**.

    ![Cambiar estado de Hola de registros de diagnóstico](./media/event-hubs-diagnostic-logs/image3.png)

5.  Destino de archivo de Hola de conjunto que desea; Por ejemplo, una cuenta de almacenamiento, un concentrador de eventos o análisis de registros de Azure.

6.  Guardar la configuración de diagnósticos de hello nueva.

La nueva configuración surte efecto en unos 10 minutos. Después de eso, los registros aparecen en el destino de archivo hello configurado, en hello **registros de diagnóstico** hoja.

Para obtener más información acerca de cómo configurar diagnósticos, vea hello [información general de los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-categories"></a>Categorías de registros de diagnósticos
Event Hubs captura registros de diagnósticos de dos categorías:

* **ArchiveLogs**: registros relacionados con archivos de bases de datos centrales de tooEvent, específicamente, registra los errores de tooarchive relacionados.
* **OperationalLogs**: información sobre lo que sucede durante las operaciones de los centros de eventos, en concreto, Hola tipo de operación, incluida la creación de concentrador de eventos, recursos que usa y Hola estado de operación de Hola.

## <a name="diagnostic-logs-schema"></a>Esquema de registros de diagnósticos
Todos los registros se almacenan en el formato de notación de objetos JavaScript (JSON). Cada entrada tiene campos de cadena que usan formato Hola descrito en hello las secciones siguientes.

### <a name="archive-logs-schema"></a>Esquema de registros de archivo

Las cadenas JSON de registro de archivo incluyen elementos enumerados en hello en la tabla siguiente:

Nombre | Descripción
------- | -------
TaskName | Descripción de tarea de Hola que dieron error.
ActivityId | El identificador interno, usado con fines de seguimiento.
trackingId | El identificador interno, usado con fines de seguimiento.
resourceId | Identificador de recursos de Azure Resource Manager.
eventHub | Nombre completo del centro de eventos (incluye el nombre del espacio de nombres).
partitionId | La partición del centro de eventos en la que se escribe.
archiveStep | ArchiveFlushWriter
startTime | Hora de inicio del error.
errores | Número de veces que se ha producido el error.
durationInSeconds | La duración del error.
Mensaje | Mensaje de error.
categoría | ArchiveLogs

Hello código siguiente es un ejemplo de un cadena JSON de registro de archivo:

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a>Esquema de registros operativos

Las cadenas JSON de registro operativo incluyen elementos enumerados en hello en la tabla siguiente:

Nombre | Descripción
------- | -------
ActivityId | Identificador interno, utiliza tootrack propósito.
EventName | Nombre de la operación.  
resourceId | Identificador de recursos de Azure Resource Manager.
SubscriptionId | Id. de suscripción.
EventTimeString | Hora de la operación.
EventProperties | Propiedades de la operación.
Estado | Estado de la operación.
Autor de llamada | Autor de la llamada de la operación (Azure Portal o Management Client).
categoría | OperationalLogs

Hello código siguiente es un ejemplo de una cadena JSON de registro operativo:

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooEvent centros](event-hubs-what-is-event-hubs.md)
* [Introducción a la API de centros de eventos](event-hubs-api-overview.md)
* [Introducción a Event Hubs](event-hubs-csharp-ephcs-getstarted.md)
