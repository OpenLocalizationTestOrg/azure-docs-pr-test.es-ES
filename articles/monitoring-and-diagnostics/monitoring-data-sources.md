---
title: "aaaConsume datos de supervisión de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello todos los orígenes de datos disponibles en Azure de supervisión de hoy en día."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/27/2017
ms.author: johnkem
ms.openlocfilehash: 3c7fdad7c25b4d456df395b453fa0e75d514b0b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consume-monitoring-data-from-azure"></a>Consume monitoring data from Azure (Consumo de datos de supervisión de Azure)

A través de hello Azure plataforma, ofrecemos juntos los datos en un solo lugar con la canalización de hello Azure Monitor de supervisión, pero casi reconoce que actualmente no todos los datos de supervisión está disponible en esa canalización aún. En este artículo, se mostrará un resumen de hello diversas maneras mediante programación puede tener acceso a datos de supervisión de servicios de Azure.

## <a name="options-for-data-consumption"></a>Opciones para el consumo de datos

| Tipo de datos | Categoría | Servicios admitidos | Métodos de acceso |
| --- | --- | --- | --- |
| Métricas en el nivel de plataforma de Azure Monitor | Métricas | [Consulte la lista aquí](monitoring-supported-metrics.md) | <ul><li>**API de REST:**[API de métrica de Azure Monitor](https://docs.microsoft.com/rest/api/monitor/metrics)</li><li>**Storage Blob o centro de eventos:**[configuración de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)</li></ul> |
| Métricas de SO invitado de proceso (p. ej., contadores de rendimiento) | Métricas | Máquinas virtuales [Windows](../virtual-machines-dotnet-diagnostics.md) y Linux (v2), [Cloud Services](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md), [Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md) | <ul><li>**Tabla de almacenamiento o Storage Blob:**[diagnósticos de Azure para Windows o Linux](../cloud-services/cloud-services-dotnet-diagnostics-storage.md)</li><li>**Centro de eventos:**[diagnósticos de Azure para Windows](../event-hubs/event-hubs-streaming-azure-diags-data.md)</li></ul> |
| Métricas personalizadas o de la aplicación | Métricas | Cualquier aplicación instrumentada con Application Insights | <ul><li>**API de REST:**[API de REST de Application Insights](https://dev.applicationinsights.io/reference)</li></ul> |
| Métricas de almacenamiento | Métricas | Almacenamiento de Azure | <ul><li>**Tabla de almacenamiento:**[análisis de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/storage-analytics)</li></ul> |
| Datos de facturación | Métricas | Todos los servicios de Azure | <ul><li>**API de REST:**[uso de Azure Resource y API de RateCard](../billing/billing-usage-rate-card-overview.md)</li></ul> |
| Registro de actividad | Eventos | Todos los servicios de Azure | <ul><li>**API de REST:**[API de eventos de Azure Monitor](https://docs.microsoft.com/rest/api/monitor/events)</li><li>**Storage Blob o centro de eventos:**[perfil de registro](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)</li></ul> |
| Registros de diagnóstico de Azure Monitor | Eventos | [Consulte la lista aquí](monitoring-diagnostic-logs-schema.md) | <ul><li>**Storage Blob o centro de eventos:**[configuración de diagnóstico](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)</li></ul> |
| Registros de SO invitado de proceso (p. ej., IIS, ETW, syslogs) | Eventos | Máquinas virtuales [Windows](../virtual-machines-dotnet-diagnostics.md) y Linux (v2), [Cloud Services](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md), [Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md) | <ul><li>**Tabla de almacenamiento o Storage Blob:**[diagnósticos de Azure para Windows o Linux](../cloud-services/cloud-services-dotnet-diagnostics-storage.md)</li><li>**Centro de eventos:**[diagnósticos de Azure para Windows](../event-hubs/event-hubs-streaming-azure-diags-data.md)</li></ul> |
| Registros de App Service | Eventos | App Services | <ul><li>**File Storage, Table Storage o Blob Storage:**[diagnósticos de la aplicación web](../app-service-web/web-sites-enable-diagnostic-log.md)</li></ul> |
| Registros de almacenamiento | Eventos | Almacenamiento de Azure | <ul><li>**Tabla de almacenamiento:**[análisis de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/storage-analytics)</li></ul> |
| Alertas de Security Center | Eventos | Azure Security Center | <ul><li>**API de REST:**[alertas de seguridad](https://msdn.microsoft.com/library/mt704050.aspx)</li></ul> |
| Informes de Active Directory | Eventos | Azure Active Directory | <ul><li>**API de REST:**[API Graph de Azure Active Directory](../active-directory/active-directory-reporting-api-getting-started.md)</li></ul> |
| Estado del recurso de Security Center | Estado | [Todos los recursos admitidos](https://msdn.microsoft.com/library/mt704041.aspx#Anchor_1) | <ul><li>**API de REST:**[estados de seguridad](https://msdn.microsoft.com/library/mt704041.aspx)</li></ul> |
| Estado de los recursos | Estado | Servicios admitidos | <ul><li>**API de REST:**[API de REST de Resource Health](https://azure.microsoft.com/blog/reduce-troubleshooting-time-with-azure-resource-health/)</li></ul> |
| Alertas de métricas de Azure Monitor | Notificaciones | [Consulte la lista aquí](monitoring-supported-metrics.md) | <ul><li>**Webhook:**[alertas de métricas de Azure](insights-webhooks-alerts.md)</li></ul> |
| Alertas de registro de actividad de Azure Monitor | Notificaciones | Todos los servicios de Azure | <ul><li>**Webhook:** alertas de registro de actividad de Azure</li></ul> |
| Notificaciones de escalado automático | Notificaciones | [Consulte la lista aquí](monitoring-overview-autoscale.md#supported-services-for-autoscale) | <ul><li>**Webhook:**[esquema de carga útil de Webhook de notificación de escalado automático](insights-autoscale-to-webhook-email.md#autoscale-notification-webhook-payload-schema)</li></ul> |
| Alertas de consulta de búsqueda de registros de OMS | Notificaciones | Log Analytics de OMS | <ul><li>**Webhook:**[alertas de Log Analytics](../log-analytics/log-analytics-alerts-actions.md#webhook-actions)</li></ul> |
| Alertas de métricas de Application Insights | Notificaciones | Application Insights | <ul><li>**Webhook:**[alertas de Application Insights](../application-insights/app-insights-alerts.md)</li></ul> |
| Pruebas web de Application Insights | Notificaciones | Application Insights | <ul><li>**Webhook:**[alertas de Application Insights](../application-insights/app-insights-alerts.md)</li></ul> |

## <a name="next-steps"></a>Pasos siguientes

- Más información sobre las [métricas de Azure Monitor](monitoring-overview-metrics.md)
- Obtenga más información sobre [Hola registro de actividad de Azure](monitoring-overview-activity-logs.md)
- Más información sobre los [registros de diagnóstico de Azure](monitoring-overview-of-diagnostic-logs.md)
