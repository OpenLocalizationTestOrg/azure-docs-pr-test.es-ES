---
title: "aaaMonitor administración de API con el Monitor de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor administración de API de Azure service mediante el Monitor de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Supervisión de API Management con Azure Monitor
Azure Monitor es un servicio de Azure que proporciona un único origen para la supervisión de todos los recursos de Azure. Con el Monitor de Azure, puede visualizar, consultar, enrutar, archivar y realizar acciones en las métricas de Hola y registros procedentes de recursos de Azure como la API de administración. 

Hola siguiendo el vídeo muestra cómo toomonitor administración de API con el Monitor de Azure. Para más información acerca de Azure Monitor, consulte [Introducción a Azure Monitor]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Métricas
Administración de API actualmente emite cinco métricas y tenemos previsto tooadd más en hello futuras. Estas métricas se emiten cada minuto, lo que le ofrece visibilidad en tiempo real en estado de Hola y el estado de sus API casi. Aquí te mostramos un resumen de las métricas de hello:
* Nº total de puerta de enlace solicitudes: número de Hola de API de solicitudes en el período de Hola. 
* Solicitudes correctas de puerta de enlace: número de Hola de solicitudes de API que recibió correctamente códigos de respuesta HTTP como 304, 307 y nada más pequeño que 301 (por ejemplo, 200). 
* Puerta de enlace solicitudes con error: el número de Hola de solicitudes de API que recibió erróneos códigos de respuesta HTTP como 400 y cualquier valor mayor que 500.
* Solicitudes no autorizadas de puerta de enlace: número de Hola de solicitudes de API que reciben los códigos de respuesta HTTP incluidos 401 y 403, 429. 
* Otras solicitudes de puerta de enlace: número de Hola de solicitudes de API que reciben los códigos de respuesta HTTP que no pertenecen tooany de hello anteriores categorías (por ejemplo, 418).

Puede acceder a métricas en el servicio API Management o a las métricas de todos los recursos de Azure en Azure Monitor. métricas de tooview en el servicio de administración de API:
1. Hola abrir portal de Azure.
2. Servicio de administración de API de tooyour go.
3. Haga clic en **Métricas**.

![Hoja Métricas][metrics-blade]

Para obtener más información acerca de cómo toouse métricas, vea [información general de las métricas].

## <a name="activity-logs"></a>Registros de actividad
Registros de actividad proporcionan una visión general de las operaciones de Hola que se realizaron en los servicios de administración de API. Antes se los conocía como "registros de auditoría" o "registros operativos". Utilizar registros de actividad, puede determinar Hola "qué, quién y cuándo" para las operaciones (PUT, POST, DELETE) realizadas en los servicios de administración de API de escritura. 

> [!NOTE]
> Registros de actividad no incluyen las operaciones de lectura (GET) o las operaciones realizadas en Hola clásico Portal para desarrolladores o usar Hola original de las API de administración.

Puede acceder a registros de actividad en el servicio API Management o a los registros de todos los recursos de Azure en Azure Monitor. actividad de tooview se registra en el servicio de administración de API:
1. Hola abrir portal de Azure.
2. Servicio de administración de API de tooyour go.
3. Haga clic en **Registro de actividad**.

![Hoja Registro de actividad][activity-logs-blade]

Para obtener más información acerca de cómo toouse métricas, vea [información general de los registros de actividad].

## <a name="alerts"></a>Alertas
Puede configurar alertas de tooreceive basadas en métricas y registros de actividades. Monitor de Azure permite tooconfigure una alerta toodo hello las siguientes cuando se desencadena:

* Enviar una notificación por correo electrónico
* Llamar a un webhook
* Invocar una aplicación lógica de Azure

Puede configurar reglas de alerta en el servicio API Management o en Azure Monitor. tooconfigure en administración de API: 
1. Hola abrir portal de Azure.
2. Servicio de administración de API de tooyour go.
3. Haga clic en **Reglas de alerta**.

![Hoja Reglas de alertas][alert-rules-blade]

Para más información sobre el uso de alertas, consulte la [introducción a las alertas].

## <a name="diagnostic-logs"></a>Registros de diagnóstico
Los registros de diagnóstico proporcionan información valiosa acerca de las operaciones y los errores que son importantes para la auditoría, así como para solucionar problemas. Los registros de diagnóstico son diferentes de los registros de actividad. Registros de actividad proporcionan información sobre las operaciones de Hola que se realizaron en los recursos de Azure. Los registros de diagnóstico proporcionan información detallada sobre las operaciones que el mismo recurso realiza.

Administración de API actualmente proporciona diagnósticos de registros (cada hora por lotes) sobre API individual solicitar a cada entrada de hello siguiente estructura:

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

Puede acceder a registros de diagnóstico en el servicio API Management o a los registros de todos los recursos de Azure en Azure Monitor. tooview registros de diagnóstico en el servicio de administración de API:
1. Hola abrir portal de Azure.
2. Servicio de administración de API de tooyour go.
3. Haga clic en **Registro de diagnóstico**.

![Hoja Registros de diagnóstico][diagnostic-logs-blade]

Para obtener más información acerca de cómo toouse métricas, vea [información general de registros de diagnóstico].

## <a name="next-step"></a>siguiente paso

* [Introducción a Azure Monitor]
* [información general de las métricas]
* [información general de los registros de actividad]
* [información general de registros de diagnóstico]
* [introducción a las alertas]

[Introducción a Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[información general de las métricas]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[información general de los registros de actividad]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[información general de registros de diagnóstico]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[introducción a las alertas]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
