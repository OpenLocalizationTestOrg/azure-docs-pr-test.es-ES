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
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="90b16-103">Crear y administrar grupos de acciones en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="90b16-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="90b16-104">Información general</span><span class="sxs-lookup"><span data-stu-id="90b16-104">Overview</span></span> ##
<span data-ttu-id="90b16-105">Este artículo muestra cómo toocreate y administrar grupos de acciones en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="90b16-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="90b16-106">Los grupos de acciones le permiten configurar una lista de acciones.</span><span class="sxs-lookup"><span data-stu-id="90b16-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="90b16-107">Estos grupos, a continuación, se pueden usar cuando se definen alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="90b16-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="90b16-108">Estos grupos, a continuación, pueden ser reutilizados por cada alerta de registro de actividad que se define, asegurándose de que Hola mismas acciones se realizan cada vez que se desencadene la alerta del registro de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b16-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="90b16-109">Un grupo de acciones puede tener hasta too10 de cada tipo de acción.</span><span class="sxs-lookup"><span data-stu-id="90b16-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="90b16-110">Cada acción se compone de hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="90b16-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="90b16-111">**Nombre**: un identificador único en el grupo de acciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b16-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="90b16-112">**Tipo de acción**: enviar un SMS, enviar un correo electrónico o llamar a un webhook.</span><span class="sxs-lookup"><span data-stu-id="90b16-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="90b16-113">**Detalles**: Hola correspondiente número de teléfono, dirección de correo electrónico o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="90b16-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="90b16-114">Para obtener información acerca de cómo toouse grupos de acciones de tooconfigure de plantillas de Azure Resource Manager, consulte [plantillas de administrador de recursos del grupo de acción](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="90b16-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="90b16-115">Crear un grupo de acciones mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="90b16-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="90b16-116">Hola [portal](https://portal.azure.com), seleccione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="90b16-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="90b16-117">Hola **Monitor** hoja consolida todos los valores y los datos en una vista supervisión.</span><span class="sxs-lookup"><span data-stu-id="90b16-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Hola servicio "Monitor"](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="90b16-119">Hola **registro de actividad** sección, seleccione **grupos de acciones**.</span><span class="sxs-lookup"><span data-stu-id="90b16-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![pestaña de "Grupos de acciones" Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="90b16-121">Seleccione **Agregar grupo de acción**y rellene los campos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b16-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![Hola "Agregar grupo de acciones" comando](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="90b16-123">Escriba un nombre en hello **nombre del grupo de acción** cuadro y escriba un nombre en hello **nombre corto** cuadro.</span><span class="sxs-lookup"><span data-stu-id="90b16-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="90b16-124">nombre corto de Hola se utiliza en lugar de un nombre de grupo de acción completa cuando se envían las notificaciones mediante este grupo.</span><span class="sxs-lookup"><span data-stu-id="90b16-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![cuadro de diálogo grupo de acción de agregar Hello"](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="90b16-126">Hola **suscripción** cuadro autofills con su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="90b16-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="90b16-127">Esta suscripción está Hola uno en el grupo de acción de Hola se guarda.</span><span class="sxs-lookup"><span data-stu-id="90b16-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="90b16-128">Seleccione hello **grupo de recursos** en qué acción Hola se guarda el grupo.</span><span class="sxs-lookup"><span data-stu-id="90b16-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="90b16-129">Defina una lista de acciones proporcionando los siguientes valores para cada acción:</span><span class="sxs-lookup"><span data-stu-id="90b16-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="90b16-130">a.</span><span class="sxs-lookup"><span data-stu-id="90b16-130">a.</span></span> <span data-ttu-id="90b16-131">**Nombre**: escriba un identificador único para esta acción.</span><span class="sxs-lookup"><span data-stu-id="90b16-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="90b16-132">b.</span><span class="sxs-lookup"><span data-stu-id="90b16-132">b.</span></span> <span data-ttu-id="90b16-133">**Tipo de acción**: seleccione SMS, correo electrónico o webhook.</span><span class="sxs-lookup"><span data-stu-id="90b16-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="90b16-134">c.</span><span class="sxs-lookup"><span data-stu-id="90b16-134">c.</span></span> <span data-ttu-id="90b16-135">**Detalles**: según el tipo de acción de hello, escriba un número de teléfono, dirección de correo electrónico o webhook URI.</span><span class="sxs-lookup"><span data-stu-id="90b16-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="90b16-136">Seleccione **Aceptar** grupo de acciones de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="90b16-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="90b16-137">Administración de los grupos de acciones</span><span class="sxs-lookup"><span data-stu-id="90b16-137">Manage your action groups</span></span> ##
<span data-ttu-id="90b16-138">Después de crear un grupo de acciones, está visible en hello **grupos de acciones** sección de hello **Monitor** hoja.</span><span class="sxs-lookup"><span data-stu-id="90b16-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="90b16-139">Seleccione el grupo de acciones de hello para que desea toomanage:</span><span class="sxs-lookup"><span data-stu-id="90b16-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="90b16-140">Agregar, editar o quitar acciones.</span><span class="sxs-lookup"><span data-stu-id="90b16-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="90b16-141">Eliminar grupo de acciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b16-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90b16-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90b16-142">Next steps</span></span> ##
* <span data-ttu-id="90b16-143">Más información sobre el [comportamiento de las alertas por SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="90b16-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="90b16-144">Obtener un [descripción del esquema de webhook alerta de registro de actividad de hello](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="90b16-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="90b16-145">Más información sobre la [limitación de velocidad](monitoring-alerts-rate-limiting.md) en las alertas.</span><span class="sxs-lookup"><span data-stu-id="90b16-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="90b16-146">Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md)y obtenga información acerca de cómo tooreceive alertas.</span><span class="sxs-lookup"><span data-stu-id="90b16-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="90b16-147">Obtenga información acerca de cómo demasiado[configurar alertas siempre que se registra una notificación de estado de servicio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="90b16-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
