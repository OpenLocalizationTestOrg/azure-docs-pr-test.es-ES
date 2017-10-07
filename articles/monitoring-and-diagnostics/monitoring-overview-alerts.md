---
title: aaaOverview de alertas en el Monitor de Azure y Microsoft Azure | Documentos de Microsoft
description: "Las alertas le permiten toomonitor métricas de recursos de Azure, eventos o registros y recibir una notificación cuando se cumple una condición especificada."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>¿Qué son las alertas en Microsoft Azure?
Este artículo describe Hola diversos orígenes de alertas en Microsoft Azure, ¿qué Hola propósitos para las alertas, sus ventajas y cómo tooget Introducción al uso de ellos. En concreto se aplica tooAzure Monitor, pero proporciona punteros tooother servicios con las alertas también. Las alertas ofrecen un método de supervisión de Azure que le permiten condiciones tooconfigure sobre los datos y se convierten en una notificación cuando condiciones Hola coincide con los datos de supervisión más reciente de hello.

## <a name="taxonomy-of-azure-alerts"></a>Taxonomía de las alertas de Azure
A continuación hello Azure usa términos toodescribe alertas y sus funciones:
* **Alerta**: una definición de criterios (una o más reglas o condiciones) que se activa cuando se cumplen.
* **Active** : hello estado cuando hello se cumplen los criterios definidos por una alerta.
* **Resolver** : hello estado cuando hello ya no se cumple el criterio definido por una alerta después previamente se ha cumplido la necesidad.
* **Notificación** -Hola acción llevada a cabo según fuera de una alerta que se pasan a estar activos.
* **Acción** -un receptor de tooa llamada específica que se envían de una notificación (por ejemplo, un correo electrónico a una dirección o el registro de dirección URL del webhook tooa). Las notificaciones normalmente pueden desencadenar varias acciones.

## <a name="alerts-in-different-azure-services"></a>Alertas en los distintos servicios de Azure
Las alertas están disponibles a través de varios servicios de supervisión de Azure. Para obtener información sobre cómo y cuándo toouse estos servicios, [consulte este artículo](./monitoring-overview.md). Este es un desglose de los tipos de alerta de hello disponibles a través de Azure:

| Servicio | Tipo de alerta | Servicios admitidos | Descripción |
|---|---|---|---|
| Azure Monitor | [Alertas de métricas](./insights-alerts-portal.md) | [Métricas compatibles con Azure Monitor](./monitoring-supported-metrics.md) | Recibir una notificación cuando cualquier métrica de nivel de plataforma cumple una condición específica (por ejemplo, % de CPU en una máquina virtual es mayor que 90 para hello últimos 5 minutos). |
| Azure Monitor | [Alertas de registro de actividad](./monitoring-activity-log-alerts.md) | Todos los tipos de recursos disponibles en Azure Resource Manager | Recibir una notificación cuando se da alguna nuevo evento en hello [Azure Activity Log](./monitoring-overview-activity-logs.md) coincide con las condiciones específicas (por ejemplo, cuando se produce una operación "Eliminar VM" en myProductionResourceGroup o cuando un nuevo evento de estado del servicio con "Activo" como estado de Hello aparece). |
| Application Insights | [Alertas de métricas](../application-insights/app-insights-alerts.md) | Cualquier aplicación instrumentada toosend datos tooApplication visión | Reciba una notificación cuando cualquier métrica de nivel de plataforma cumple una condición específica (por ejemplo, el tiempo de respuesta del servidor es superior a 2 segundos). |
| Application Insights | [Alertas de prueba web](../application-insights/app-insights-monitor-web-app-availability.md) | Cualquier sitio Web instrumentado toosend datos tooApplication visión | Reciba una notificación cuando la disponibilidad o la capacidad de respuesta de un sitio web está por debajo de las expectativas. |
| Log Analytics | [Alertas de Log Analytics](../log-analytics/log-analytics-alerts.md) | Todos los servicios configurados toosend datos en análisis de registros | Reciba una notificación cuando una consulta de búsqueda de Log Analytics sobre datos de métrica o de evento cumple determinados criterios. |

## <a name="alerts-on-azure-monitor-data"></a>Alertas sobre datos de Azure Monitor
Existen dos tipos de alertas de los datos disponibles en Azure Monitor: alertas métricas y alertas de registro de actividad.

* **Alertas de métrica** -esta alerta se desencadena cuando el valor de Hola de una métrica especificada está fuera de un umbral que se asigna. alerta de Hello genera una notificación cuando alerta Hola está "activado" (si se sobrepasa el umbral de Hola y se cumple la condición de alerta de hello) así como cuando queda "resuelto" (cuando se cruza nuevo umbral de Hola y ya no se cumple la condición de hello). Para ver una lista creciente de las métricas disponibles compatibles con Azure Monitor, consulte la [lista de métricas que se admiten en Azure Monitor](monitoring-supported-metrics.md).
* **Alertas de registro de actividad**: una alerta de registro de streaming que se desencadena cuando se genera un evento de registro de actividad que coincide con los criterios de filtro que se han asignado. Estas alertas tienen sólo un estado "Activado", puesto que el motor de alertas de hello simplemente aplica el nuevo evento tooany del criterio de filtro de Hola. Estas alertas pueden ser utilizado toobecome una notificación cuando se produce un incidente de estado del servicio nuevo o cuando un usuario o una aplicación realiza una operación en su suscripción, por ejemplo, "Eliminar la máquina virtual".

Para los datos de registro de diagnóstico disponibles a través del Monitor de Azure, se recomienda enrutamiento datos hello en análisis de registros y el uso de una alerta de análisis de registros. Hello diagrama siguiente resume los orígenes de datos en el Monitor de Azure y, conceptualmente, cómo puede avisar fuera de esos datos.

![Alertas explicadas](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>¿Cómo se puede recibir una notificación sobre una alerta de Azure Monitor?
Históricamente, las alertas de Azure de distintos servicios usan sus propios métodos de notificación integrados. A partir de ahora, Azure Monitor ofrece una agrupación de notificación reutilizable denominada Grupos de acciones. Grupos de acciones de especifican un conjunto de receptores para una notificación de cualquier número de direcciones de correo electrónico, números de teléfono (de SMS) o las direcciones URL del webhook--y siempre que se activa una alerta que referencias Hola grupo de acciones, esa notificación de recepción de todos los destinatarios. Esto le permite tooreuse una agrupación de destinatarios (por ejemplo, la de llamada ingeniero lista) a través de muchos objetos de alerta. Actualmente, solo las alertas de registro de actividad hacen uso de lo Grupos de acciones, pero se está trabajando para que otros tipos de alerta de Azure utilicen también los Grupos de acciones.

Grupos de acciones admiten la notificación mediante el registro de dirección URL del webhook tooa en direcciones de tooemail de adición y números SMS. Esto permite la automatización y corrección, por ejemplo, mediante:
    - Runbook de Azure Automation
    - Función de Azure
    - Aplicación lógica de Azure
    - un servicio de terceros

Las alertas de métricas aún no utilizan los Grupos de acciones. En una alerta de métrica individual puede configurar notificaciones para:
* Enviar correo electrónico notificaciones toohello servicio Administrador, administradores de tooco o tooadditional direcciones de correo electrónico que especifique.
* Llamar a un webhook, que le permite toolaunch acciones de automatización adicionales.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información sobre las reglas de alertas y su configuración mediante:

* Más información sobre las [métricas](monitoring-overview-metrics.md)
* Configuración de [alertas de métricas a través de Azure Portal](insights-alerts-portal.md)
* Configuración de [alertas de métricas con PowerShell](insights-alerts-powershell.md)
* Configuración de [alertas de métricas con la interfaz de línea de comandos (CLI)](insights-alerts-command-line-interface.md)
* Configuración de [alertas de métricas con la API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* Más información sobre el [registro de actividad](monitoring-overview-activity-logs.md)
* Configuración de [alertas del registro de actividad a través de Azure Portal](monitoring-activity-log-alerts.md)
* Configuración de [alertas del registro de actividad a través de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Hola de revisión [esquema de webhook alerta de registro de actividad](monitoring-activity-log-alerts-webhook.md)
* Más información sobre las [notificaciones del servicio](monitoring-service-notifications.md)
* Más información sobre los [grupos de acciones](monitoring-action-groups.md)
