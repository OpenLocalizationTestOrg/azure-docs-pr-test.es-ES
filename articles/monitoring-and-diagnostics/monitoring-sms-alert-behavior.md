---
title: Comportamiento de las alertas por SMS en los grupos de acciones | Microsoft Docs
description: "Formato de mensajes SMS y respuesta a los mensajes SMS de cancelación de suscripción, segunda suscripción o solicitud de ayuda."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3e4eca174209eeb9cbce1d45111d1e5cc30af8b0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="8e2e0-103">Comportamiento de las alertas por SMS en los grupos de acciones</span><span class="sxs-lookup"><span data-stu-id="8e2e0-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="8e2e0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8e2e0-104">Overview</span></span> ##
<span data-ttu-id="8e2e0-105">Los grupos de acciones permiten configurar una lista de destinatarios.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-105">Action groups enable you to configure a list of receivers.</span></span> <span data-ttu-id="8e2e0-106">Luego se pueden aprovechar estos grupos al definir alertas de registro de actividad, lo que garantiza que cuando se activa una alerta de registro de actividad, un grupo de acciones concreto recibe la notificación.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span></span> <span data-ttu-id="8e2e0-107">Uno de los mecanismos de alerta que se admiten es el SMS; las alertas admiten la comunicación bidireccional.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-107">One of the alerting mechanisms supported is SMS; the alerts support bi-directional communication.</span></span> <span data-ttu-id="8e2e0-108">Un usuario puede responder a una alerta para:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-108">A user can respond to an alert to:</span></span>

- <span data-ttu-id="8e2e0-109">**Cancelar la suscripción a alertas:** un usuario puede cancelar la suscripción a todas las alertas por SMS para todos los grupos de acciones o para un grupo de acciones singular.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="8e2e0-110">**Volver a suscribirse a alertas:** un usuario puede volver a suscribirse a todas las alertas por SMS para todos los grupos de acciones o para un grupo de acciones singular.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-110">**Resubscribe to alerts:** A user can resubscribe to all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="8e2e0-111">**Solicitar ayuda:** un usuario puede pedir más información acerca del SMS.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-111">**Request help:** A user can ask for more information on the SMS.</span></span> <span data-ttu-id="8e2e0-112">Se le redirigirá a este artículo</span><span class="sxs-lookup"><span data-stu-id="8e2e0-112">They will be redirected to this article</span></span>

<span data-ttu-id="8e2e0-113">En este artículo se trata el comportamiento de las alertas por SMS y las acciones de respuesta que el usuario puede realizar en función de su configuración regional:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-113">This article covers the behavior of the SMS alerts and the response actions the user can take based on the locale of the user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="8e2e0-114">Comportamiento de SMS en Estados Unidos y Canadá</span><span class="sxs-lookup"><span data-stu-id="8e2e0-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="8e2e0-115">Recepción de una alerta por SMS</span><span class="sxs-lookup"><span data-stu-id="8e2e0-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="8e2e0-116">Un receptor de SMS, que se configura como parte de un grupo de acciones, recibirá un SMS cuando se desencadene una alerta.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="8e2e0-117">El SMS contendrá la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-117">The SMS will carry the following information:</span></span>
* <span data-ttu-id="8e2e0-118">El nombre corto del grupo de acciones al que se envió esta alerta</span><span class="sxs-lookup"><span data-stu-id="8e2e0-118">Shortname of the action group this alert was sent to</span></span>
- <span data-ttu-id="8e2e0-119">El título de la alerta</span><span class="sxs-lookup"><span data-stu-id="8e2e0-119">Title of the alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="8e2e0-120">Cancelación de la suscripción a alertas por SMS para un grupo de acciones</span><span class="sxs-lookup"><span data-stu-id="8e2e0-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="8e2e0-121">Para que un usuario cancele la suscripción a los SMS para las alertas de un grupo de acciones, debe responder al código corto 20873 con las palabras clave: "DISABLE &lt;Nombre corto del grupo de acciones&gt;".</span><span class="sxs-lookup"><span data-stu-id="8e2e0-121">A user can unsubscribe from SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="8e2e0-122">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-122">Ex.</span></span> <span data-ttu-id="8e2e0-123">Un usuario que desea cancelar la suscripción a las alertas de un grupo de acciones con el nombre corto "Azure", tendría que enviar el siguiente SMS al código corto 20873: "DISABLE Azure"</span><span class="sxs-lookup"><span data-stu-id="8e2e0-123">A user wishing to unsubscribe from alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="8e2e0-124">Cancelación de la suscripción a alertas por SMS para todos los grupos de acciones</span><span class="sxs-lookup"><span data-stu-id="8e2e0-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="8e2e0-125">Un usuario puede cancelar la suscripción a todas las alertas por SMS para todos los grupos de acción respondiendo al código corto 20873 con cualquiera de las siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-125">A user can unsubscribe from all SMS alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="8e2e0-126">STOP</span><span class="sxs-lookup"><span data-stu-id="8e2e0-126">STOP</span></span>

<span data-ttu-id="8e2e0-127">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-127">Ex.</span></span> <span data-ttu-id="8e2e0-128">Un usuario que desea cancelar la suscripción a todas las alertas por SMS para todos los grupos tendría que enviar el siguiente SMS al código corto 20873: "STOP"</span><span class="sxs-lookup"><span data-stu-id="8e2e0-128">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="8e2e0-129">Si un usuario ha cancelado la suscripción a las alertas por SMS, pero luego se agrega a un nuevo grupo de acciones; SE recibirán alertas por SMS para el grupo de acciones nuevo, pero permanecerán sin suscripción de todos los grupos de acciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-129">If a user has unsubscribed from SMS alerts, but is then added to a new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a><span data-ttu-id="8e2e0-130">Segunda suscripción a alertas por SMS para un grupo de acciones</span><span class="sxs-lookup"><span data-stu-id="8e2e0-130">Resubscribing to SMS alerts for one action group</span></span>
<span data-ttu-id="8e2e0-131">Para que un usuario vuelva a suscribirse a los SMS para las alertas de un grupo de acciones, debe responder al código corto 20873 con las palabras clave: "ENABLE &lt;Nombre corto del grupo de acciones&gt;".</span><span class="sxs-lookup"><span data-stu-id="8e2e0-131">A user can resubscribe to SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="8e2e0-132">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-132">Ex.</span></span> <span data-ttu-id="8e2e0-133">Un usuario que desea volver a suscribirse a las alertas de un grupo de acciones con el nombre corto "Azure", tendría que enviar el siguiente SMS al código corto 20873: "ENABLE Azure"</span><span class="sxs-lookup"><span data-stu-id="8e2e0-133">A user wishing to resubscribe to alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a><span data-ttu-id="8e2e0-134">Segunda suscripción a alertas por SMS para todos los grupo de acciones</span><span class="sxs-lookup"><span data-stu-id="8e2e0-134">Resubscribing to SMS alerts for all action groups</span></span>
<span data-ttu-id="8e2e0-135">Un usuario puede volver a suscribirse a todas las alertas por SMS para todos los grupos de acción respondiendo al código corto 20873 con cualquiera de las siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-135">A user can resubscribe to all SMS for alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>

* <span data-ttu-id="8e2e0-136">START</span><span class="sxs-lookup"><span data-stu-id="8e2e0-136">START</span></span>

<span data-ttu-id="8e2e0-137">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-137">Ex.</span></span> <span data-ttu-id="8e2e0-138">Un usuario que desea volver a suscribirse a todas las alertas por SMS para todos los grupos tendría que enviar el siguiente SMS al código corto 20873: "STOP"</span><span class="sxs-lookup"><span data-stu-id="8e2e0-138">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="8e2e0-139">Solicitud de ayuda a través de SMS</span><span class="sxs-lookup"><span data-stu-id="8e2e0-139">Requesting help via SMS</span></span>
<span data-ttu-id="8e2e0-140">Un usuario puede solicitar más información acerca de SMS que ha recibido. Para ello, debe responder al código corto 20873 con cualquiera de las siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="8e2e0-140">A user can ask for more information about the SMS they have received by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="8e2e0-141">HELP</span><span class="sxs-lookup"><span data-stu-id="8e2e0-141">HELP</span></span>

<span data-ttu-id="8e2e0-142">Se enviará una respuesta al usuario con un vínculo a este artículo.</span><span class="sxs-lookup"><span data-stu-id="8e2e0-142">A response will be sent to the user with a link to this article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e2e0-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e2e0-143">Next Steps</span></span>
<span data-ttu-id="8e2e0-144">Obtener una [introducción a las alertas del registro de actividad](monitoring-overview-alerts.md) y aprender cómo puede recibir alertas</span><span class="sxs-lookup"><span data-stu-id="8e2e0-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="8e2e0-145">Más información sobre la [limitación de la tasa de SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="8e2e0-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="8e2e0-146">Más información sobre los [grupos de acciones](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="8e2e0-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
