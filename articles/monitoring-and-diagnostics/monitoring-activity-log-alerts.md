---
title: alertas de registro de actividad de aaaCreate | Documentos de Microsoft
description: "Recibirá una notificación por correo electrónico, SMS y webhook cuando se producen determinados eventos en el registro de actividad de Hola."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Creación de alertas del registro de actividad

## <a name="overview"></a>Información general
Alertas de registro de actividad son alertas que se activa cuando produce un nuevo evento de registro de actividad que coincida con las condiciones de hello especificadas en la alerta de Hola. Son recursos de Azure, por lo que pueden crearse con una plantilla de Azure Resource Manager. También pueden crear, actualizar o elimina en hello portal de Azure. Este artículo presenta los conceptos de hello detrás de las alertas de registro de actividad. A continuación, se muestra cómo toouse hello Azure portal tooset una alerta sobre los eventos de registro de actividad.

Normalmente, para crear alertas de registro de actividad tooreceive notificaciones cuando:

* Se producen cambios específicos en su suscripción de Azure, grupos de recursos de tooparticular a menudo con ámbito o recursos de los recursos. Por ejemplo, puede toobe una notificación cuando se elimina una máquina virtual myProductionResourceGroup. O bien, puede querer toobe una notificación si los nuevos roles se asignan a tooa usuario en su suscripción.
* Se produce un evento de mantenimiento del servicio. Eventos de estado de servicio incluyen notificaciones de incidentes y eventos de mantenimiento que se aplican tooresources en su suscripción.

En cualquier caso, una alerta de registro de actividad se supervisa solo para eventos de suscripción de hello en qué Hola se creó la alerta.

Puede configurar una alerta de registro de actividad basada en cualquier propiedad de nivel superior en el objeto JSON de Hola para un evento de registro de actividad. Sin embargo, el portal de hello muestra opciones más comunes de hello:

- **Categoría**: Administración, Mantenimiento del servicio, Escalado automático y Recomendación. Para obtener más información, consulte [información general sobre el registro de actividad de Azure de hello](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). toolearn más información acerca de los eventos de estado del servicio, consulte [recibir avisos de registro de actividad en las notificaciones del servicio](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Grupos de recursos**
- **Recurso**
- **Tipo de recurso**
- **Nombre de la operación**: nombre de la operación de hello Control de acceso basado en roles de administrador de recursos.
- **Nivel**: Hola a nivel de gravedad del evento de hello (detallado, informativo, advertencia, Error o crítico).
- **Estado**: estado de hello del evento hello, que normalmente se inician, error o se realizó correctamente.
- **Evento iniciado por**: Hola también se denomina "llamador". dirección de correo electrónico de Hola o identificador de Azure Active Directory del usuario de Hola que realizó la operación de Hola.

>[!NOTE]
>Debe especificar al menos dos de hello precede a criterios de la alerta, con la que se va a una categoría de Hola. No puede crear una alerta que se activa cada vez que se crea un evento en los registros de actividad de Hola.
>
>

Cuando se activa una alerta de registro de actividad, usa la acción toogenerate acciones o notificaciones de grupo. Un grupo de acciones es un conjunto reutilizable de destinatarios de notificación, como direcciones de correo electrónico, direcciones URL del webhook o números de teléfono para SMS. receptores de Hello pueden hacer referencia desde varios toocentralize de alertas y los canales de notificación de grupo. Al definir la alerta del registro de actividad, tiene dos opciones. Puede:

* Usar un grupo de acciones existente en la alerta del registro de actividad. 
* Crear un nuevo grupo de acciones. 

toolearn más información acerca de los grupos de acciones, vea [crear y administrar grupos de acciones en el portal de Azure hello](monitoring-action-groups.md).

toolearn más información acerca de las notificaciones de estado de servicio, consulte [recibir avisos de registro de actividad en las notificaciones de estado de servicio](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Crear una alerta para un evento de registro de actividad con un nuevo grupo de acción mediante el uso de hello portal de Azure
1. Hola [portal](https://portal.azure.com), seleccione **Monitor**.

    ![Hola servicio "Monitor"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. Hola **registro de actividad** sección, seleccione **alertas**.

    ![pestaña de "Alertas" Hello](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Seleccione **Agregar alerta de registro de actividad**y rellene los campos de Hola.

4. Escriba un nombre en hello **nombre de alerta de registro de actividad** cuadro y seleccione un **descripción**.

    ![Hola "Agregar alerta de registro de actividad" comando](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Hola **suscripción** cuadro autofills con su suscripción actual. Esta suscripción está Hola uno en el grupo de acción de Hola se guarda. recurso de alerta de Hello es implementado toothis suscripción y monitores actividad eventos de registro del mismo.

    ![cuadro de diálogo "Agregar alerta de registro de actividad" Hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Seleccione hello **grupo de recursos** en qué Hola alerta recurso se haya creado. No es grupo de recursos de hello supervisado por alerta de Hola. En su lugar, es grupo de recursos de Hola donde se encuentra Hola alertas recurso.

7. Si lo desea, seleccione una **categoría de eventos** toomodify Hola filtros adicionales que se muestran. Para los eventos administrativos, los filtros de hello incluyen **grupo de recursos**, **recursos**, **tipo de recurso**, **nombre de la operación**, **Nivel**, **estado**, y **evento iniciado por**. Estos valores identifican los eventos que debe supervisar esta alerta.

    >[!NOTE]
    >Debe especificar al menos uno de hello precede a criterios de la alerta. No puede crear una alerta que se activa cada vez que se crea un evento en los registros de actividad de Hola.
    >
    >

8. Escriba un nombre en hello **nombre del grupo de acción** cuadro y escriba un nombre en hello **nombre corto** cuadro. nombre corto de Hola se utiliza en lugar de un nombre de grupo de acción completa cuando se envían las notificaciones mediante este grupo.

9.  Definir una lista de acciones proporcionando la acción de Hola.

    a. **Nombre**: escriba el nombre de la acción de hello, alias o identificador.

    b. **Tipo de acción**: seleccione SMS, correo electrónico o webhook.

    c. **Detalles**: según el tipo de acción de hello, escriba un número de teléfono, dirección de correo electrónico o webhook URI.

10. Seleccione **Aceptar** alerta de hello toocreate.

alerta de Hello tarda unos minutos toofully propagar y, a continuación, vuelva a activar. Desencadena cuando nuevos eventos coincide con los criterios de la alerta de Hola.

Para obtener más información, consulte [esquema de webhook de hello entender utilizado en las alertas de registro de actividad](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>grupo de acciones de Hello definida en estos pasos es reutilizable como un grupo de acciones existente para todas las definiciones de alerta futuras.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Crear una alerta para un evento de registro de actividad para un grupo de acciones existente mediante el uso de hello portal de Azure
1. Siga los pasos del 1 al 7 en hello anterior sección toocreate la alerta de registro de actividad.

2. En **notificar a través de**, seleccione hello **existente** botón de acción de grupo. Seleccione un grupo existente de la acción de lista de Hola.

3. Seleccione **Aceptar** alerta de hello toocreate.

alerta de Hello tarda unos minutos toofully propagar y, a continuación, vuelva a activar. Desencadena cuando nuevos eventos coincide con los criterios de la alerta de Hola.

## <a name="manage-your-alerts"></a>Administración de alertas

Después de crear una alerta, está visible en la sección de alertas de Hola de hoja de Monitor de Hola. Seleccione la alerta de hello para que desea toomanage:

* Editarla.
* Eliminarla.
* Deshabilitar o habilitar, si desea que tootemporarily detener o reanudar la recepción de notificaciones de alerta de Hola.

## <a name="next-steps"></a>Pasos siguientes
- Obtener una [Introducción a las alertas](monitoring-overview-alerts.md).
- Más información sobre la [Limitación del número de notificaciones](monitoring-alerts-rate-limiting.md).
- Hola de revisión [esquema de webhook alerta de registro de actividad](monitoring-activity-log-alerts-webhook.md).
- Más información sobre los [grupos de acciones](monitoring-action-groups.md).  
- Más información acerca de las [Notificaciones del estado del servicio](monitoring-service-notifications.md).
- Crear un [actividad de registro de alerta toomonitor todas las operaciones de motor de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Crear un [actividad de registro de alerta toomonitor todas las operaciones de escala-escalabilidad de escalado automático errores en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
