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
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="8061f-103">Creación de alertas del registro de actividad en notificaciones del servicio</span><span class="sxs-lookup"><span data-stu-id="8061f-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="8061f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8061f-104">Overview</span></span>
<span data-ttu-id="8061f-105">Este artículo muestra cómo las alertas tooset seguridad del registro de actividad de las notificaciones de estado de servicio mediante el uso de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8061f-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="8061f-106">Puede recibir una alerta cuando Azure envía tooyour de notificaciones de estado de servicio suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8061f-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="8061f-107">Puede configurar la alerta de hello basada en:</span><span class="sxs-lookup"><span data-stu-id="8061f-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="8061f-108">clase de Hello de notificación de estado de servicio (incidentes, mantenimiento, información, etcetera).</span><span class="sxs-lookup"><span data-stu-id="8061f-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="8061f-109">Hola o los servicios afectados.</span><span class="sxs-lookup"><span data-stu-id="8061f-109">hello service(s) affected.</span></span>
- <span data-ttu-id="8061f-110">Hola regiones afectadas.</span><span class="sxs-lookup"><span data-stu-id="8061f-110">hello region(s) affected.</span></span>
- <span data-ttu-id="8061f-111">estado de Hola de notificación de hello (active frente a resuelto).</span><span class="sxs-lookup"><span data-stu-id="8061f-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="8061f-112">nivel de Hola de notificaciones de hello (informativo, advertencia, error).</span><span class="sxs-lookup"><span data-stu-id="8061f-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="8061f-113">También puede configurar que se debe enviar alerta hello:</span><span class="sxs-lookup"><span data-stu-id="8061f-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="8061f-114">Seleccione un grupo de acciones existente.</span><span class="sxs-lookup"><span data-stu-id="8061f-114">Select an existing action group.</span></span>
- <span data-ttu-id="8061f-115">Cree un nuevo grupo de acciones (que puede usarse para futuras alertas).</span><span class="sxs-lookup"><span data-stu-id="8061f-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="8061f-116">toolearn más información acerca de los grupos de acciones, vea [crear y administrar grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="8061f-117">Para obtener información sobre cómo alertas de notificación de estado del servicio de tooconfigure mediante el uso de plantillas del Administrador de recursos de Azure, consulte [plantillas del Administrador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="8061f-118">Crear una alerta para una notificación de estado de servicio para un nuevo grupo de acción mediante el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8061f-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="8061f-119">Hola [portal](https://portal.azure.com), seleccione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="8061f-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Hola servicio "Monitor"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="8061f-121">Hola **registro de actividad** sección, seleccione **alertas**.</span><span class="sxs-lookup"><span data-stu-id="8061f-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![pestaña de "Alertas" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="8061f-123">Seleccione **Agregar alerta de registro de actividad**y rellene los campos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8061f-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![Hola "Agregar alerta de registro de actividad" comando](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="8061f-125">Escriba un nombre en hello **nombre de alerta de registro de actividad** cuadro y proporcione un **descripción**.</span><span class="sxs-lookup"><span data-stu-id="8061f-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![cuadro de diálogo "Agregar alerta de registro de actividad" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="8061f-127">Hola **suscripción** cuadro autofills con su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="8061f-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="8061f-128">Esta suscripción está alerta de registro de actividad de hello toosave usado.</span><span class="sxs-lookup"><span data-stu-id="8061f-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="8061f-129">recurso de alerta de Hello es eventos de suscripción y los monitores de toothis implementado en el registro de actividad de hello para el mismo.</span><span class="sxs-lookup"><span data-stu-id="8061f-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="8061f-130">Seleccione hello **grupo de recursos** en qué Hola alerta recurso se haya creado.</span><span class="sxs-lookup"><span data-stu-id="8061f-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="8061f-131">Esto no es grupo de recursos de hello supervisado por alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8061f-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="8061f-132">En su lugar, es grupo de recursos de Hola donde se encuentra Hola alertas recurso.</span><span class="sxs-lookup"><span data-stu-id="8061f-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="8061f-133">Hola **categoría de eventos** cuadro, seleccione **estado del servicio**.</span><span class="sxs-lookup"><span data-stu-id="8061f-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="8061f-134">Si lo desea, seleccione hello **servicio**, **región**, **tipo**, **estado**, y **nivel** de servicio notificaciones de estado que desea tooreceive.</span><span class="sxs-lookup"><span data-stu-id="8061f-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="8061f-135">En **alertas a través de**, seleccione hello **New** botón de acción de grupo.</span><span class="sxs-lookup"><span data-stu-id="8061f-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="8061f-136">Escriba un nombre en hello **nombre del grupo de acción** cuadro y escriba un nombre en hello **nombre corto** cuadro.</span><span class="sxs-lookup"><span data-stu-id="8061f-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="8061f-137">nombre corto de Hola se hace referencia en las notificaciones de Hola que se envían cuando se desencadene esta alerta.</span><span class="sxs-lookup"><span data-stu-id="8061f-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="8061f-138">Definir una lista de destinatarios proporcionando del receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8061f-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="8061f-139">a.</span><span class="sxs-lookup"><span data-stu-id="8061f-139">a.</span></span> <span data-ttu-id="8061f-140">**Nombre**: escriba el nombre del receptor de hello, alias o identificador.</span><span class="sxs-lookup"><span data-stu-id="8061f-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="8061f-141">b.</span><span class="sxs-lookup"><span data-stu-id="8061f-141">b.</span></span> <span data-ttu-id="8061f-142">**Tipo de acción**: seleccione SMS, correo electrónico o webhook.</span><span class="sxs-lookup"><span data-stu-id="8061f-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="8061f-143">c.</span><span class="sxs-lookup"><span data-stu-id="8061f-143">c.</span></span> <span data-ttu-id="8061f-144">**Detalles**: según el tipo de acción de hello elegido, escriba un número de teléfono, dirección de correo electrónico o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="8061f-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="8061f-145">Seleccione **Aceptar** alerta de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8061f-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="8061f-146">Dentro de unos minutos, alerta de hello está activa y empieza tootrigger según las condiciones de hello especificados durante la creación.</span><span class="sxs-lookup"><span data-stu-id="8061f-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="8061f-147">Para obtener información sobre el esquema de webhook de Hola para las alertas de registro de actividad, vea [Webhook para la actividad de Azure registra alertas](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="8061f-148">grupo de acciones de Hello definida en estos pasos es reutilizable como un grupo de acciones existente para todas las definiciones de alerta futuras.</span><span class="sxs-lookup"><span data-stu-id="8061f-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="8061f-149">Crear una alerta para una notificación de estado de servicio para un grupo de acción existente mediante el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8061f-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="8061f-150">Siga los pasos del 1 al 7 en hello anterior sección toocreate la notificación de estado de servicio.</span><span class="sxs-lookup"><span data-stu-id="8061f-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="8061f-151">En **alertas a través de**, seleccione hello **existente** botón de acción de grupo.</span><span class="sxs-lookup"><span data-stu-id="8061f-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="8061f-152">Seleccionar grupo de acciones apropiado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8061f-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="8061f-153">Seleccione **Aceptar** alerta de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8061f-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="8061f-154">Dentro de unos minutos, alerta de hello está activa y empieza tootrigger según las condiciones de hello especificados durante la creación.</span><span class="sxs-lookup"><span data-stu-id="8061f-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="8061f-155">Administración de alertas</span><span class="sxs-lookup"><span data-stu-id="8061f-155">Manage your alerts</span></span>

<span data-ttu-id="8061f-156">Después de crear una alerta, es visible en hello **alertas** sección de hello **Monitor** hoja.</span><span class="sxs-lookup"><span data-stu-id="8061f-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="8061f-157">Seleccione la alerta de hello para que desea toomanage:</span><span class="sxs-lookup"><span data-stu-id="8061f-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="8061f-158">Editarla.</span><span class="sxs-lookup"><span data-stu-id="8061f-158">Edit it.</span></span>
* <span data-ttu-id="8061f-159">Eliminarla.</span><span class="sxs-lookup"><span data-stu-id="8061f-159">Delete it.</span></span>
* <span data-ttu-id="8061f-160">Deshabilitar o habilitar, si desea que tootemporarily detener o reanudar la recepción de notificaciones de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8061f-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8061f-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8061f-161">Next steps</span></span>
- <span data-ttu-id="8061f-162">Más información acerca de las [Notificaciones del estado del servicio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="8061f-163">Más información sobre la [Limitación del número de notificaciones](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="8061f-164">Hola de revisión [esquema de webhook alerta de registro de actividad](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="8061f-165">Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md)y obtenga información acerca de cómo tooreceive alertas.</span><span class="sxs-lookup"><span data-stu-id="8061f-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="8061f-166">Más información sobre los [grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
