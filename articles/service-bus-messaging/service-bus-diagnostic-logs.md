---
title: "registros de diagnóstico de Bus de servicio de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset los registros de diagnóstico de Service Bus en Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Registros de diagnóstico de Service Bus

Puede ver dos tipos de registros para Azure Service Bus:
* **[Registros de actividad](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Estos registros contienen información relativa a las operaciones realizadas en un trabajo. registros de Hello siempre están habilitados.
* **[Registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Puede configurar registros de diagnóstico para obtener información más completa sobre todo lo que ocurre en un trabajo. Las actividades de la portada de registros de diagnóstico de tiempo de hello trabajo Hola se crea hasta que se elimina el trabajo de hello, incluidas las actualizaciones y las actividades que se producen mientras se ejecuta el trabajo de Hola.

## <a name="turn-on-diagnostic-logs"></a>Activación de los registros de diagnóstico

Los registros de diagnóstico están inhabilitados de forma predeterminada. registros de diagnóstico de tooenable, lleve a cabo Hola pasos:

1.  Hola [portal de Azure](https://portal.azure.com), en **supervisión + administración**, haga clic en **registros de diagnóstico**.

    ![Registros de toodiagnostic de navegación de hoja](./media/service-bus-diagnostic-logs/image1.png)

2. Haga clic en recurso de Hola que desee toomonitor.  

3.  Haga clic en **Activar diagnóstico**.

    ![activar los registros de diagnósticos](./media/service-bus-diagnostic-logs/image2.png)

4.  En **Estado**, haga clic en **Activado**.

    ![cambiar el estado de los registros de diagnósticos](./media/service-bus-diagnostic-logs/image3.png)

5.  Destino de archivo de Hola de conjunto que desea; Por ejemplo, una cuenta de almacenamiento, un concentrador de eventos o análisis de registros de Azure.

6.  Guardar la configuración de diagnósticos de hello nueva.

La nueva configuración surte efecto en unos 10 minutos. Después de eso, los registros aparecen en el destino de archivo hello configurado, en hello **registros de diagnóstico** hoja.

Para obtener más información acerca de cómo configurar diagnósticos, vea hello [información general de los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Esquema de registros de diagnósticos

Todos los registros se almacenan en el formato de notación de objetos JavaScript (JSON). Cada entrada tiene campos de cadena que utilizan el formato de hello descrito en hello pasos de la sección.

## <a name="operational-logs-schema"></a>Esquema de registros operativos

Inicia sesión en hello **OperationalLogs** categoría capturar lo que sucede durante las operaciones de Bus de servicio. En concreto, estos registros capturar el tipo de operación de hello, incluida la creación de cola, los recursos que usa y Hola estado de operación de Hola.

Las cadenas JSON de registro operativo incluyen elementos enumerados en hello en la tabla siguiente:

Nombre | Descripción
------- | -------
ActivityId | El identificador interno, usado con fines de seguimiento
EventName | Nombre de la operación           
resourceId | El identificador de recursos de Azure Resource Manager
SubscriptionId | Id. de suscripción
EventTimeString | Hora de la operación
EventProperties | Propiedades de la operación
Estado | Estado de la operación
Autor de llamada | Autor de la llamada de la operación (Azure Portal o Management Client)
categoría | OperationalLogs

Este es un ejemplo de una cadena JSON de registro operativo:

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Pasos siguientes

Visite Hola siguiendo vínculos toolearn más acerca de Bus de servicio:

* [Introducción tooService Bus](service-bus-messaging-overview.md)
* [Introducción a Service Bus](service-bus-dotnet-get-started-with-queues.md)
