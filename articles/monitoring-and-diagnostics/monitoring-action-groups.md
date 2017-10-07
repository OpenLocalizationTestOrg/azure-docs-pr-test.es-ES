---
title: aaaCreate y administrar grupos de acciones en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate y administrar grupos de acciones en hello portal de Azure."
author: anirudhcavale
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Crear y administrar grupos de acciones en hello portal de Azure
## <a name="overview"></a>Información general ##
Este artículo muestra cómo toocreate y administrar grupos de acciones en hello portal de Azure.

Los grupos de acciones le permiten configurar una lista de acciones. Estos grupos, a continuación, se pueden usar cuando se definen alertas del registro de actividad. Estos grupos, a continuación, pueden ser reutilizados por cada alerta de registro de actividad que se define, asegurándose de que Hola mismas acciones se realizan cada vez que se desencadene la alerta del registro de actividad de Hola.

Un grupo de acciones puede tener hasta too10 de cada tipo de acción. Cada acción se compone de hello propiedades siguientes:

* **Nombre**: un identificador único en el grupo de acciones de Hola.  
* **Tipo de acción**: enviar un SMS, enviar un correo electrónico o llamar a un webhook.  
* **Detalles**: Hola correspondiente número de teléfono, dirección de correo electrónico o webhook URI.

Para obtener información acerca de cómo toouse grupos de acciones de tooconfigure de plantillas de Azure Resource Manager, consulte [plantillas de administrador de recursos del grupo de acción](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Crear un grupo de acciones mediante Hola portal de Azure ##
1. Hola [portal](https://portal.azure.com), seleccione **Monitor**. Hola **Monitor** hoja consolida todos los valores y los datos en una vista supervisión.

    ![Hola servicio "Monitor"](./media/monitoring-action-groups/home-monitor.png)
2. Hola **registro de actividad** sección, seleccione **grupos de acciones**.

    ![pestaña de "Grupos de acciones" Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. Seleccione **Agregar grupo de acción**y rellene los campos de Hola.

    ![Hola "Agregar grupo de acciones" comando](./media/monitoring-action-groups/add-action-group.png)
4. Escriba un nombre en hello **nombre del grupo de acción** cuadro y escriba un nombre en hello **nombre corto** cuadro. nombre corto de Hola se utiliza en lugar de un nombre de grupo de acción completa cuando se envían las notificaciones mediante este grupo.

      ![cuadro de diálogo grupo de acción de agregar Hello"](./media/monitoring-action-groups/action-group-define.png)

5. Hola **suscripción** cuadro autofills con su suscripción actual. Esta suscripción está Hola uno en el grupo de acción de Hola se guarda.

6. Seleccione hello **grupo de recursos** en qué acción Hola se guarda el grupo.

7. Defina una lista de acciones proporcionando los siguientes valores para cada acción:

    a. **Nombre**: escriba un identificador único para esta acción.

    b. **Tipo de acción**: seleccione SMS, correo electrónico o webhook.

    c. **Detalles**: según el tipo de acción de hello, escriba un número de teléfono, dirección de correo electrónico o webhook URI.

8. Seleccione **Aceptar** grupo de acciones de toocreate Hola.

## <a name="manage-your-action-groups"></a>Administración de los grupos de acciones ##
Después de crear un grupo de acciones, está visible en hello **grupos de acciones** sección de hello **Monitor** hoja. Seleccione el grupo de acciones de hello para que desea toomanage:

* Agregar, editar o quitar acciones.
* Eliminar grupo de acciones de Hola.

## <a name="next-steps"></a>Pasos siguientes ##
* Más información sobre el [comportamiento de las alertas por SMS](monitoring-sms-alert-behavior.md).  
* Obtener un [descripción del esquema de webhook alerta de registro de actividad de hello](monitoring-activity-log-alerts-webhook.md).  
* Más información sobre la [limitación de velocidad](monitoring-alerts-rate-limiting.md) en las alertas. 
* Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md)y obtenga información acerca de cómo tooreceive alertas.  
* Obtenga información acerca de cómo demasiado[configurar alertas siempre que se registra una notificación de estado de servicio](monitoring-activity-log-alerts-on-service-notifications.md).
