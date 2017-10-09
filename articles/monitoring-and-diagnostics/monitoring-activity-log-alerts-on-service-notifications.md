---
title: alertas de registro de actividad de aaaReceive en las notificaciones del servicio | Documentos de Microsoft
description: "Reciba notificaciones por SMS, correo electrónico o webhook cuando se produzcan eventos en el servicio de Azure."
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Creación de alertas del registro de actividad en notificaciones del servicio
## <a name="overview"></a>Información general
Este artículo muestra cómo las alertas tooset seguridad del registro de actividad de las notificaciones de estado de servicio mediante el uso de hello portal de Azure.  

Puede recibir una alerta cuando Azure envía tooyour de notificaciones de estado de servicio suscripción de Azure. Puede configurar la alerta de hello basada en:

- clase de Hello de notificación de estado de servicio (incidentes, mantenimiento, información, etcetera).
- Hola o los servicios afectados.
- Hola regiones afectadas.
- estado de Hola de notificación de hello (active frente a resuelto).
- nivel de Hola de notificaciones de hello (informativo, advertencia, error).

También puede configurar que se debe enviar alerta hello:

- Seleccione un grupo de acciones existente.
- Cree un nuevo grupo de acciones (que puede usarse para futuras alertas).

toolearn más información acerca de los grupos de acciones, vea [crear y administrar grupos de acciones](monitoring-action-groups.md).

Para obtener información sobre cómo alertas de notificación de estado del servicio de tooconfigure mediante el uso de plantillas del Administrador de recursos de Azure, consulte [plantillas del Administrador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Crear una alerta para una notificación de estado de servicio para un nuevo grupo de acción mediante el uso de hello portal de Azure
1. Hola [portal](https://portal.azure.com), seleccione **Monitor**.

    ![Hola servicio "Monitor"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. Hola **registro de actividad** sección, seleccione **alertas**.

    ![pestaña de "Alertas" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. Seleccione **Agregar alerta de registro de actividad**y rellene los campos de Hola.

    ![Hola "Agregar alerta de registro de actividad" comando](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Escriba un nombre en hello **nombre de alerta de registro de actividad** cuadro y proporcione un **descripción**.

    ![cuadro de diálogo "Agregar alerta de registro de actividad" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. Hola **suscripción** cuadro autofills con su suscripción actual. Esta suscripción está alerta de registro de actividad de hello toosave usado. recurso de alerta de Hello es eventos de suscripción y los monitores de toothis implementado en el registro de actividad de hello para el mismo.

6. Seleccione hello **grupo de recursos** en qué Hola alerta recurso se haya creado. Esto no es grupo de recursos de hello supervisado por alerta de Hola. En su lugar, es grupo de recursos de Hola donde se encuentra Hola alertas recurso.

7. Hola **categoría de eventos** cuadro, seleccione **estado del servicio**. Si lo desea, seleccione hello **servicio**, **región**, **tipo**, **estado**, y **nivel** de servicio notificaciones de estado que desea tooreceive.

8. En **alertas a través de**, seleccione hello **New** botón de acción de grupo. Escriba un nombre en hello **nombre del grupo de acción** cuadro y escriba un nombre en hello **nombre corto** cuadro. nombre corto de Hola se hace referencia en las notificaciones de Hola que se envían cuando se desencadene esta alerta.

9. Definir una lista de destinatarios proporcionando del receptor de Hola.

    a. **Nombre**: escriba el nombre del receptor de hello, alias o identificador.

    b. **Tipo de acción**: seleccione SMS, correo electrónico o webhook.

    c. **Detalles**: según el tipo de acción de hello elegido, escriba un número de teléfono, dirección de correo electrónico o webhook URI.

10. Seleccione **Aceptar** alerta de hello toocreate.

Dentro de unos minutos, alerta de hello está activa y empieza tootrigger según las condiciones de hello especificados durante la creación.

Para obtener información sobre el esquema de webhook de Hola para las alertas de registro de actividad, vea [Webhook para la actividad de Azure registra alertas](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>grupo de acciones de Hello definida en estos pasos es reutilizable como un grupo de acciones existente para todas las definiciones de alerta futuras.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Crear una alerta para una notificación de estado de servicio para un grupo de acción existente mediante el uso de hello portal de Azure

1. Siga los pasos del 1 al 7 en hello anterior sección toocreate la notificación de estado de servicio. 

2. En **alertas a través de**, seleccione hello **existente** botón de acción de grupo. Seleccionar grupo de acciones apropiado de Hola.

3. Seleccione **Aceptar** alerta de hello toocreate.

Dentro de unos minutos, alerta de hello está activa y empieza tootrigger según las condiciones de hello especificados durante la creación.

## <a name="manage-your-alerts"></a>Administración de alertas

Después de crear una alerta, es visible en hello **alertas** sección de hello **Monitor** hoja. Seleccione la alerta de hello para que desea toomanage:

* Editarla.
* Eliminarla.
* Deshabilitar o habilitar, si desea que tootemporarily detener o reanudar la recepción de notificaciones de alerta de Hola.

## <a name="next-steps"></a>Pasos siguientes
- Más información acerca de las [Notificaciones del estado del servicio](monitoring-service-notifications.md).
- Más información sobre la [Limitación del número de notificaciones](monitoring-alerts-rate-limiting.md).
- Hola de revisión [esquema de webhook alerta de registro de actividad](monitoring-activity-log-alerts-webhook.md).
- Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md)y obtenga información acerca de cómo tooreceive alertas. 
- Más información sobre los [grupos de acciones](monitoring-action-groups.md).
