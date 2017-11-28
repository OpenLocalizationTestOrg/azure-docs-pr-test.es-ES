---
title: "Creación de alertas del registro de actividad | Microsoft Docs"
description: "Reciba notificaciones por SMS, webhook y correo electrónico cuando se produzcan determinados eventos en el registro de actividad."
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
ms.openlocfilehash: 3885469ec0e1fcc31386dd0ad7fe6cb5d03ab28e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="7b517-103">Creación de alertas del registro de actividad</span><span class="sxs-lookup"><span data-stu-id="7b517-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="7b517-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7b517-104">Overview</span></span>
<span data-ttu-id="7b517-105">Las alertas del registro de actividad son alertas que se activan cuando un nuevo evento del registro de actividad cumple las condiciones especificadas en la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches the conditions specified in the alert.</span></span> <span data-ttu-id="7b517-106">Son recursos de Azure, por lo que pueden crearse con una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7b517-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="7b517-107">También se pueden crear, actualizar o eliminar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7b517-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="7b517-108">Este artículo presenta los conceptos relativos a las alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="7b517-109">Seguidamente, se explica cómo usar Azure Portal para configurar alertas en eventos del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-109">It then shows you how to use the Azure portal to set up an alert on activity log events.</span></span>

<span data-ttu-id="7b517-110">Por lo general, se crean alertas del registro de actividad para recibir notificaciones cuando:</span><span class="sxs-lookup"><span data-stu-id="7b517-110">Typically, you create activity log alerts to receive notifications when:</span></span>

* <span data-ttu-id="7b517-111">Se produzcan cambios específicos en los recursos de la suscripción de Azure, que abarcan normalmente grupos de recursos o recursos en particular.</span><span class="sxs-lookup"><span data-stu-id="7b517-111">Specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resources.</span></span> <span data-ttu-id="7b517-112">Por ejemplo, si quiere que le notifiquen cuando se elimine alguna máquina virtual de myProductionResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="7b517-112">For example, you might want to be notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="7b517-113">O, podría querer recibir una notificación si se asigna algún rol nuevo a un usuario de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="7b517-113">Or, you might want to be notified if any new roles are assigned to a user in your subscription.</span></span>
* <span data-ttu-id="7b517-114">Se produce un evento de mantenimiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="7b517-114">A service health event occurs.</span></span> <span data-ttu-id="7b517-115">Los eventos de mantenimiento del servicio incluyen la notificación de incidentes y eventos de mantenimiento que se aplican a recursos de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="7b517-115">Service health events include notification of incidents and maintenance events that apply to resources in your subscription.</span></span>

<span data-ttu-id="7b517-116">En cualquier caso, una alerta del registro de actividad solo supervisa eventos de la suscripción en la que se ha creado la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-116">In either case, an activity log alert monitors only for events in the subscription in which the alert is created.</span></span>

<span data-ttu-id="7b517-117">Puede configurar una alerta del registro de actividad según las propiedades de nivel superior del objeto JSON de un evento del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-117">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="7b517-118">Sin embargo, el portal muestra las opciones más comunes:</span><span class="sxs-lookup"><span data-stu-id="7b517-118">However, the portal shows the most common options:</span></span>

- <span data-ttu-id="7b517-119">**Categoría**: Administración, Mantenimiento del servicio, Escalado automático y Recomendación.</span><span class="sxs-lookup"><span data-stu-id="7b517-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="7b517-120">Para más información, consulte [Información general sobre el registro de actividad de Azure](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="7b517-120">For more information, see [Overview of the Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="7b517-121">Para más información acerca de los eventos de mantenimiento del servicio, consulte [Recibir alertas del registro de actividad con las notificaciones del servicio](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-121">To learn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="7b517-122">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="7b517-122">**Resource group**</span></span>
- <span data-ttu-id="7b517-123">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="7b517-123">**Resource**</span></span>
- <span data-ttu-id="7b517-124">**Tipo de recurso**</span><span class="sxs-lookup"><span data-stu-id="7b517-124">**Resource type**</span></span>
- <span data-ttu-id="7b517-125">**Nombre de la operación**: el nombre de la operación de control de acceso basado en rol de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7b517-125">**Operation name**: The Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="7b517-126">**Nivel**: el nivel de gravedad del evento (detallado, informativo, advertencia, error o crítico).</span><span class="sxs-lookup"><span data-stu-id="7b517-126">**Level**: The severity level of the event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="7b517-127">**Estado**: el estado del evento, normalmente Iniciado, Error o Correcto.</span><span class="sxs-lookup"><span data-stu-id="7b517-127">**Status**: The status of the event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="7b517-128">**Evento iniciado por**: también se conoce como el "llamador."</span><span class="sxs-lookup"><span data-stu-id="7b517-128">**Event initiated by**: Also known as the "caller."</span></span> <span data-ttu-id="7b517-129">La dirección de correo electrónico o el identificador de Azure Active Directory del usuario que realizó la operación.</span><span class="sxs-lookup"><span data-stu-id="7b517-129">The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

>[!NOTE]
><span data-ttu-id="7b517-130">Debe especificar al menos dos de los criterios anteriores en la alerta, siendo uno de ellos la categoría.</span><span class="sxs-lookup"><span data-stu-id="7b517-130">You must specify at least two of the preceding criteria in your alert, with one being the category.</span></span> <span data-ttu-id="7b517-131">No puede crear una alerta que se active cada vez que se crea un evento en los registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-131">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>
>

<span data-ttu-id="7b517-132">Cuando se activa una alerta del registro de actividad, usa un grupo de acciones para generar acciones o notificaciones.</span><span class="sxs-lookup"><span data-stu-id="7b517-132">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="7b517-133">Un grupo de acciones es un conjunto reutilizable de destinatarios de notificación, como direcciones de correo electrónico, direcciones URL del webhook o números de teléfono para SMS.</span><span class="sxs-lookup"><span data-stu-id="7b517-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="7b517-134">Se puede hacer referencia a los receptores desde varias alertas para centralizar y agrupar los canales de notificación.</span><span class="sxs-lookup"><span data-stu-id="7b517-134">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="7b517-135">Al definir la alerta del registro de actividad, tiene dos opciones.</span><span class="sxs-lookup"><span data-stu-id="7b517-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="7b517-136">Puede:</span><span class="sxs-lookup"><span data-stu-id="7b517-136">You can:</span></span>

* <span data-ttu-id="7b517-137">Usar un grupo de acciones existente en la alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="7b517-138">Crear un nuevo grupo de acciones.</span><span class="sxs-lookup"><span data-stu-id="7b517-138">Create a new action group.</span></span> 

<span data-ttu-id="7b517-139">Para más información sobre los grupos de acciones, consulte [Creación y administración de grupos de acciones en Azure Portal](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-139">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="7b517-140">Para más información acerca de las notificaciones de mantenimiento del servicio, consulte [Recibir alertas del registro de actividad con las notificaciones de mantenimiento del servicio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-140">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="7b517-141">Creación de una alerta para un evento del registro de actividad con un nuevo grupo de acciones mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b517-141">Create an alert on an activity log event with a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="7b517-142">En el [portal](https://portal.azure.com), seleccione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="7b517-142">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Servicio "Monitor"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="7b517-144">En la sección **Registro de actividad**, seleccione **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="7b517-144">In the **Activity log** section, select **Alerts**.</span></span>

    ![Pestaña "Alertas"](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="7b517-146">Seleccione **Agregar alerta de registro de actividad** y rellene los campos.</span><span class="sxs-lookup"><span data-stu-id="7b517-146">Select **Add activity log alert**, and fill in the fields.</span></span>

4. <span data-ttu-id="7b517-147">Escriba un nombre en el cuadro de texto **Nombre de alerta del registro de actividad** y seleccione una **Descripción**.</span><span class="sxs-lookup"><span data-stu-id="7b517-147">Enter a name in the **Activity log alert name** box, and select a **Description**.</span></span>

    ![Comando "Agregar alerta de registro de actividad"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="7b517-149">El cuadro de texto **Suscripción** se rellena automáticamente con la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="7b517-149">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="7b517-150">La suscripción es aquella en la que se guarda el grupo de acciones.</span><span class="sxs-lookup"><span data-stu-id="7b517-150">This subscription is the one in which the action group is saved.</span></span> <span data-ttu-id="7b517-151">Esta es la suscripción en la que se implementa el recurso de alerta y desde la que se supervisan los eventos del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-151">The alert resource is deployed to this subscription and monitors activity log events from it.</span></span>

    ![Cuadro de diálogo "Agregar alerta de registro de actividad"](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="7b517-153">Seleccione el **Grupo de recursos** en el que se crea el recurso de la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-153">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="7b517-154">Este no es el grupo de recursos supervisado por la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-154">This is not the resource group that's monitored by the alert.</span></span> <span data-ttu-id="7b517-155">En su lugar, es el grupo de recursos donde se encuentra el recurso de la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-155">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="7b517-156">Opcionalmente, seleccione una **Categoría de evento** para modificar los filtros adicionales que se muestran.</span><span class="sxs-lookup"><span data-stu-id="7b517-156">Optionally, select an **Event category** to modify the additional filters that are shown.</span></span> <span data-ttu-id="7b517-157">Para eventos administrativos, los filtros incluyen **Grupo de recursos**, **Recurso**, **Tipo de recurso**, **Nombre de la operación**, **Nivel**, **Estado** y **Evento iniciado por**.</span><span class="sxs-lookup"><span data-stu-id="7b517-157">For Administrative events, the filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="7b517-158">Estos valores identifican los eventos que debe supervisar esta alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="7b517-159">Debe especificar al menos uno de los criterios anteriores en la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-159">You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="7b517-160">No puede crear una alerta que se active cada vez que se crea un evento en los registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-160">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
    >
    >

8. <span data-ttu-id="7b517-161">Escriba un nombre en el cuadro de texto **Nombre del grupo de acciones** y especifique un nombre en el cuadro de texto **Nombre corto**.</span><span class="sxs-lookup"><span data-stu-id="7b517-161">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="7b517-162">El nombre corto se utiliza en lugar del nombre completo del grupo de acciones cuando se envían notificaciones mediante este grupo.</span><span class="sxs-lookup"><span data-stu-id="7b517-162">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="7b517-163">Defina una lista de acciones proporcionando la siguiente información de la acción:</span><span class="sxs-lookup"><span data-stu-id="7b517-163">Define a list of actions by providing the action’s:</span></span>

    <span data-ttu-id="7b517-164">a.</span><span class="sxs-lookup"><span data-stu-id="7b517-164">a.</span></span> <span data-ttu-id="7b517-165">**Nombre**: escriba el nombre, alias o identificador de la acción.</span><span class="sxs-lookup"><span data-stu-id="7b517-165">**Name**: Enter the action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="7b517-166">b.</span><span class="sxs-lookup"><span data-stu-id="7b517-166">b.</span></span> <span data-ttu-id="7b517-167">**Tipo de acción**: seleccione SMS, correo electrónico o webhook.</span><span class="sxs-lookup"><span data-stu-id="7b517-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="7b517-168">c.</span><span class="sxs-lookup"><span data-stu-id="7b517-168">c.</span></span> <span data-ttu-id="7b517-169">**Detalles**: según el tipo de acción, proporcione un número de teléfono, una dirección de correo electrónico o un identificador URI de webhook.</span><span class="sxs-lookup"><span data-stu-id="7b517-169">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="7b517-170">Seleccione **Aceptar** para crear la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-170">Select **OK** to create the alert.</span></span>

<span data-ttu-id="7b517-171">La alerta tarda unos minutos en propagarse completamente y, a continuación, se activa.</span><span class="sxs-lookup"><span data-stu-id="7b517-171">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="7b517-172">Se desencadena cuando los nuevos eventos coinciden con los criterios de la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-172">It triggers when new events match the alert's criteria.</span></span>

<span data-ttu-id="7b517-173">Para más información, consulte [Conocer el esquema de webhook que se utiliza en las alertas del registro de actividad](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-173">For more information, see [Understand the webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="7b517-174">El grupo de acciones definido en estos pasos es reutilizable, como grupo de acciones existente, en todas las futuras definiciones de alertas.</span><span class="sxs-lookup"><span data-stu-id="7b517-174">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="7b517-175">Creación de una alerta para un evento del registro de actividad para un grupo de acciones ya existente con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b517-175">Create an alert on an activity log event for an existing action group by using the Azure portal</span></span>
1. <span data-ttu-id="7b517-176">Siga los pasos del 1 al 7 de la sección anterior para crear la alerta del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="7b517-176">Follow steps 1 through 7 in the previous section to create your activity log alert.</span></span>

2. <span data-ttu-id="7b517-177">En **Notificar a través de**, seleccione el botón grupo de acciones **Existente**.</span><span class="sxs-lookup"><span data-stu-id="7b517-177">Under **Notify via**, select the **Existing** action group button.</span></span> <span data-ttu-id="7b517-178">Seleccione un grupo de acciones existente de la lista.</span><span class="sxs-lookup"><span data-stu-id="7b517-178">Select an existing action group from the list.</span></span>

3. <span data-ttu-id="7b517-179">Seleccione **Aceptar** para crear la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-179">Select **OK** to create the alert.</span></span>

<span data-ttu-id="7b517-180">La alerta tarda unos minutos en propagarse completamente y, a continuación, se activa.</span><span class="sxs-lookup"><span data-stu-id="7b517-180">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="7b517-181">Se desencadena cuando los nuevos eventos coinciden con los criterios de la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-181">It triggers when new events match the alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="7b517-182">Administración de alertas</span><span class="sxs-lookup"><span data-stu-id="7b517-182">Manage your alerts</span></span>

<span data-ttu-id="7b517-183">Después de crear una alerta, es visible en la sección Alertas de la hoja Supervisión.</span><span class="sxs-lookup"><span data-stu-id="7b517-183">After you create an alert, it's visible in the Alerts section of the Monitor blade.</span></span> <span data-ttu-id="7b517-184">Seleccione la alerta que desea administrar para:</span><span class="sxs-lookup"><span data-stu-id="7b517-184">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="7b517-185">Editarla.</span><span class="sxs-lookup"><span data-stu-id="7b517-185">Edit it.</span></span>
* <span data-ttu-id="7b517-186">Eliminarla.</span><span class="sxs-lookup"><span data-stu-id="7b517-186">Delete it.</span></span>
* <span data-ttu-id="7b517-187">Deshabilitarla o habilitarla, si desea detener temporalmente o reanudar la recepción de notificaciones de la alerta.</span><span class="sxs-lookup"><span data-stu-id="7b517-187">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b517-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b517-188">Next steps</span></span>
- <span data-ttu-id="7b517-189">Obtener una [Introducción a las alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="7b517-190">Más información sobre la [Limitación del número de notificaciones](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="7b517-191">Revise el [Esquema de webhook de alertas del registro de actividad](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-191">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="7b517-192">Más información sobre los [grupos de acciones](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="7b517-193">Más información acerca de las [Notificaciones del estado del servicio](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7b517-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="7b517-194">Creación de una [alerta del registro de actividad para supervisar todas las operaciones del motor de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="7b517-194">Create an [activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="7b517-195">Creación de una [alerta del registro de actividad para supervisar todas las operaciones con errores de escalado automático y reducción horizontal en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="7b517-195">Create an [activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
