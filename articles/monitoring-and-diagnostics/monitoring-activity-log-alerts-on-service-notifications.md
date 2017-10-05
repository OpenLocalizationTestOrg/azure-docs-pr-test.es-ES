---
title: "Recepción de alertas del registro de actividad en notificaciones del servicio | Microsoft Docs"
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
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="46798-103">Creación de alertas del registro de actividad en notificaciones del servicio</span><span class="sxs-lookup"><span data-stu-id="46798-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="46798-104">Información general</span><span class="sxs-lookup"><span data-stu-id="46798-104">Overview</span></span>
<span data-ttu-id="46798-105">En este artículo se explica cómo configurar las alertas del registro de actividad para las notificaciones de mantenimiento de un servicio mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="46798-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="46798-106">Puede recibir una alerta cuando Azure envía notificaciones de estado del servicio a la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="46798-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="46798-107">Puede configurar la alerta en función de:</span><span class="sxs-lookup"><span data-stu-id="46798-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="46798-108">La clase de notificación de mantenimiento del servicio (incidente, mantenimiento, información, etc.).</span><span class="sxs-lookup"><span data-stu-id="46798-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="46798-109">Los servicios afectados.</span><span class="sxs-lookup"><span data-stu-id="46798-109">The service(s) affected.</span></span>
- <span data-ttu-id="46798-110">Las regiones afectadas.</span><span class="sxs-lookup"><span data-stu-id="46798-110">The region(s) affected.</span></span>
- <span data-ttu-id="46798-111">El estado de la notificación (activa o resuelta).</span><span class="sxs-lookup"><span data-stu-id="46798-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="46798-112">El nivel de las notificaciones (informativo, advertencia, error).</span><span class="sxs-lookup"><span data-stu-id="46798-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="46798-113">También puede configurar a quién se debe enviar la alerta:</span><span class="sxs-lookup"><span data-stu-id="46798-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="46798-114">Seleccione un grupo de acciones existente.</span><span class="sxs-lookup"><span data-stu-id="46798-114">Select an existing action group.</span></span>
- <span data-ttu-id="46798-115">Cree un nuevo grupo de acciones (que puede usarse para futuras alertas).</span><span class="sxs-lookup"><span data-stu-id="46798-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="46798-116">Para más información sobre los grupos de acciones, consulte [Creación y administración de grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="46798-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="46798-117">Para obtener información sobre cómo configurar las alertas de notificación de mantenimiento del servicio mediante plantillas de Azure Resource Manager, consulte [Plantillas de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="46798-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="46798-118">Creación de una alerta basada en una notificación de mantenimiento del servicio para un nuevo grupo de acciones con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="46798-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="46798-119">En el [portal](https://portal.azure.com), seleccione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="46798-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Servicio "Monitor"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="46798-121">En la sección **Registro de actividad**, seleccione **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="46798-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![Pestaña "Alertas"](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="46798-123">Seleccione **Agregar alerta de registro de actividad** y rellene los campos.</span><span class="sxs-lookup"><span data-stu-id="46798-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![Comando "Agregar alerta de registro de actividad"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="46798-125">Escriba un nombre en el cuadro de texto **Nombre de alerta de registro de actividad** y proporcione una **Descripción**.</span><span class="sxs-lookup"><span data-stu-id="46798-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![Cuadro de diálogo "Agregar alerta de registro de actividad"](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="46798-127">El cuadro de texto **Suscripción** se rellena automáticamente con la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="46798-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="46798-128">Esta suscripción se usa para guardar la alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="46798-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="46798-129">El recurso de la alerta se implementa en esta suscripción y supervisa los eventos en el registro de actividad para dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="46798-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="46798-130">Seleccione el **Grupo de recursos** en el que se crea el recurso de la alerta.</span><span class="sxs-lookup"><span data-stu-id="46798-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="46798-131">Este no es el grupo de recursos que está supervisado por la alerta.</span><span class="sxs-lookup"><span data-stu-id="46798-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="46798-132">En su lugar, es el grupo de recursos donde se encuentra el recurso de la alerta.</span><span class="sxs-lookup"><span data-stu-id="46798-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="46798-133">En el cuadro de texto **Categoría de evento**, seleccione **Estado del servicio**.</span><span class="sxs-lookup"><span data-stu-id="46798-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="46798-134">Si lo desea, seleccione los valores de **Servicio**, **Región**, **Tipo**, **Estado** y **Nivel** de notificaciones de mantenimiento del servicio que desea recibir.</span><span class="sxs-lookup"><span data-stu-id="46798-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="46798-135">En **Alertar mediante**, seleccione el botón de grupo de acciones **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="46798-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="46798-136">Escriba un nombre en el cuadro de texto **Nombre del grupo de acciones** y especifique un nombre en el cuadro de texto **Nombre corto**.</span><span class="sxs-lookup"><span data-stu-id="46798-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="46798-137">Se hace referencia al nombre corto en las notificaciones que se envían cuando se desencadena esta alerta.</span><span class="sxs-lookup"><span data-stu-id="46798-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="46798-138">A continuación, defina una lista de destinatarios proporcionando:</span><span class="sxs-lookup"><span data-stu-id="46798-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="46798-139">a.</span><span class="sxs-lookup"><span data-stu-id="46798-139">a.</span></span> <span data-ttu-id="46798-140">**Nombre**: el nombre, alias o identificador del destinatario.</span><span class="sxs-lookup"><span data-stu-id="46798-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="46798-141">b.</span><span class="sxs-lookup"><span data-stu-id="46798-141">b.</span></span> <span data-ttu-id="46798-142">**Tipo de acción**: seleccione SMS, correo electrónico o webhook.</span><span class="sxs-lookup"><span data-stu-id="46798-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="46798-143">c.</span><span class="sxs-lookup"><span data-stu-id="46798-143">c.</span></span> <span data-ttu-id="46798-144">**Detalles**: según el tipo de acción elegido, proporcione un número de teléfono, una dirección de correo electrónico o un identificador URI de webhook.</span><span class="sxs-lookup"><span data-stu-id="46798-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="46798-145">Seleccione **Aceptar** para crear la alerta.</span><span class="sxs-lookup"><span data-stu-id="46798-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="46798-146">En unos minutos, la alerta está activa y comienza a desencadenarse en función de las condiciones especificadas durante la creación.</span><span class="sxs-lookup"><span data-stu-id="46798-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="46798-147">Para obtener información sobre el esquema de webhook para las alertas del registro de actividad, consulte [Webhooks para alertas del registro de actividad de Azure](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="46798-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="46798-148">El grupo de acciones definido en estos pasos es reutilizable, como grupo de acciones existente, en todas las futuras definiciones de alertas.</span><span class="sxs-lookup"><span data-stu-id="46798-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="46798-149">Creación de una alerta basada en una notificación de mantenimiento del servicio para un grupo de acciones existente con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="46798-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="46798-150">Siga los pasos del 1 al 7 de la sección anterior para crear la notificación de mantenimiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="46798-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="46798-151">En **Alertar mediante**, seleccione el botón de grupo de acciones **Existente**.</span><span class="sxs-lookup"><span data-stu-id="46798-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="46798-152">Seleccione el grupo adecuado.</span><span class="sxs-lookup"><span data-stu-id="46798-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="46798-153">Seleccione **Aceptar** para crear la alerta.</span><span class="sxs-lookup"><span data-stu-id="46798-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="46798-154">En unos minutos, la alerta está activa y comienza a desencadenarse en función de las condiciones especificadas durante la creación.</span><span class="sxs-lookup"><span data-stu-id="46798-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="46798-155">Administración de alertas</span><span class="sxs-lookup"><span data-stu-id="46798-155">Manage your alerts</span></span>

<span data-ttu-id="46798-156">Después de crear una alerta, es visible en la sección **Alertas** de la hoja **Supervisión**.</span><span class="sxs-lookup"><span data-stu-id="46798-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="46798-157">Seleccione la alerta que desea administrar para:</span><span class="sxs-lookup"><span data-stu-id="46798-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="46798-158">Editarla.</span><span class="sxs-lookup"><span data-stu-id="46798-158">Edit it.</span></span>
* <span data-ttu-id="46798-159">Eliminarla.</span><span class="sxs-lookup"><span data-stu-id="46798-159">Delete it.</span></span>
* <span data-ttu-id="46798-160">Deshabilitarla o habilitarla, si desea detener temporalmente o reanudar la recepción de notificaciones de la alerta.</span><span class="sxs-lookup"><span data-stu-id="46798-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46798-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46798-161">Next steps</span></span>
- <span data-ttu-id="46798-162">Más información acerca de las [Notificaciones del estado del servicio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="46798-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="46798-163">Más información sobre la [Limitación del número de notificaciones](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="46798-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="46798-164">Revise el [Esquema de webhook de alertas del registro de actividad](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="46798-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="46798-165">Consulte la [introducción a las alertas del registro de actividad](monitoring-overview-alerts.md) y aprenda cómo puede recibir alertas.</span><span class="sxs-lookup"><span data-stu-id="46798-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="46798-166">Más información sobre los [grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="46798-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
