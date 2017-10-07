---
title: comportamiento de alertas de aaaSMS en grupos de acciones | Documentos de Microsoft
description: Formato de mensaje SMS y responde tooSMS mensajes toounsubscribe, suscribirse o solicitar ayuda.
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="d0e72-103">Comportamiento de las alertas por SMS en los grupos de acciones</span><span class="sxs-lookup"><span data-stu-id="d0e72-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="d0e72-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d0e72-104">Overview</span></span> ##
<span data-ttu-id="d0e72-105">Grupos de acciones le permiten tooconfigure una lista de destinatarios.</span><span class="sxs-lookup"><span data-stu-id="d0e72-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="d0e72-106">A continuación, se pueden aprovechar estos grupos al definir las alertas del registro de actividad; asegurarse de que se notifique un grupo de acción determinado cuando se desencadene la alerta del registro de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0e72-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="d0e72-107">Uno de hello admiten mecanismos de alerta es SMS; las alertas de Hello admiten la comunicación bidireccional.</span><span class="sxs-lookup"><span data-stu-id="d0e72-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="d0e72-108">Un usuario puede responder tooan alerta:</span><span class="sxs-lookup"><span data-stu-id="d0e72-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="d0e72-109">**Cancelar la suscripción a alertas:** un usuario puede cancelar la suscripción a todas las alertas por SMS para todos los grupos de acciones o para un grupo de acciones singular.</span><span class="sxs-lookup"><span data-stu-id="d0e72-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="d0e72-110">**Suscribirse tooalerts:** un usuario puede volver a suscribirse tooall alertas SMS para todos los grupos de acciones o un grupo de acción singular.</span><span class="sxs-lookup"><span data-stu-id="d0e72-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="d0e72-111">**Solicitar ayuda:** puede pedir un usuario para obtener más información sobre Hola SMS.</span><span class="sxs-lookup"><span data-stu-id="d0e72-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="d0e72-112">Estarán artículo toothis redirigida</span><span class="sxs-lookup"><span data-stu-id="d0e72-112">They will be redirected toothis article</span></span>

<span data-ttu-id="d0e72-113">Este artículo explica el comportamiento de Hola de alertas SMS de Hola y Hola usuario de Hola de acciones de respuesta puede tomar en función de configuración regional de saludo del usuario de hello:</span><span class="sxs-lookup"><span data-stu-id="d0e72-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="d0e72-114">Comportamiento de SMS en Estados Unidos y Canadá</span><span class="sxs-lookup"><span data-stu-id="d0e72-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="d0e72-115">Recepción de una alerta por SMS</span><span class="sxs-lookup"><span data-stu-id="d0e72-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="d0e72-116">Un receptor de SMS, que se configura como parte de un grupo de acciones, recibirá un SMS cuando se desencadene una alerta.</span><span class="sxs-lookup"><span data-stu-id="d0e72-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="d0e72-117">Hola SMS transmitirá Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d0e72-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="d0e72-118">Nombre corto de grupo de acciones de hello esta alerta se envió a</span><span class="sxs-lookup"><span data-stu-id="d0e72-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="d0e72-119">Título de alerta de Hola</span><span class="sxs-lookup"><span data-stu-id="d0e72-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="d0e72-120">Cancelación de la suscripción a alertas por SMS para un grupo de acciones</span><span class="sxs-lookup"><span data-stu-id="d0e72-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="d0e72-121">Un usuario puede cancelar la suscripción de SMS para las alertas para el grupo de acciones de una forma responde toohello 20873 con las palabras clave de hello: "Deshabilitar &lt;Shortname del grupo de acción&gt;".</span><span class="sxs-lookup"><span data-stu-id="d0e72-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="d0e72-122">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0e72-122">Ex.</span></span> <span data-ttu-id="d0e72-123">Un usuario que quieran toounsubscribe de alertas para un grupo de acciones con hello shortname "Azure", enviaría un toohello SMS 20873 que dice "Deshabilitar Azure"</span><span class="sxs-lookup"><span data-stu-id="d0e72-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="d0e72-124">Cancelación de la suscripción a alertas por SMS para todos los grupos de acciones</span><span class="sxs-lookup"><span data-stu-id="d0e72-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="d0e72-125">Un usuario puede cancelar la suscripción a todas las alertas SMS para todos los grupos de acciones por responde toohello 20873 con cualquiera de hello siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="d0e72-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="d0e72-126">STOP</span><span class="sxs-lookup"><span data-stu-id="d0e72-126">STOP</span></span>

<span data-ttu-id="d0e72-127">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0e72-127">Ex.</span></span> <span data-ttu-id="d0e72-128">Un usuario que quieran toounsubscribe de todas las alertas SMS para todos los grupos de acciones, enviaría un toohello SMS 20873 que dice "Detener"</span><span class="sxs-lookup"><span data-stu-id="d0e72-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="d0e72-129">Si un usuario ha cancelado la suscripción a alertas SMS, pero, a continuación, se agrega el nuevo grupo de acciones tooa; SE recibir avisos SMS para ese grupo de acción nueva, pero permanecen sin suscripciones de todos los grupos de acción anterior.</span><span class="sxs-lookup"><span data-stu-id="d0e72-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="d0e72-130">Resubscribing tooSMS alertas para un grupo de acciones</span><span class="sxs-lookup"><span data-stu-id="d0e72-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="d0e72-131">Un usuario puede volver a suscribirse tooSMS para las alertas para el grupo de una acción por responde toohello 20873 con las palabras clave de hello: "Habilitar &lt;Shortname del grupo de acción&gt;".</span><span class="sxs-lookup"><span data-stu-id="d0e72-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="d0e72-132">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0e72-132">Ex.</span></span> <span data-ttu-id="d0e72-133">Un usuario que quieran tooresubscribe tooalerts para un grupo de acciones con hello shortname "Azure", enviaría un toohello SMS 20873 que dice "Habilitar Azure"</span><span class="sxs-lookup"><span data-stu-id="d0e72-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="d0e72-134">Resubscribing tooSMS alertas para todos los grupos de acciones</span><span class="sxs-lookup"><span data-stu-id="d0e72-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="d0e72-135">Un usuario puede volver a suscribirse tooall SMS para las alertas para todos los grupos de acciones por responde toohello 20873 con cualquiera de hello siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="d0e72-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="d0e72-136">START</span><span class="sxs-lookup"><span data-stu-id="d0e72-136">START</span></span>

<span data-ttu-id="d0e72-137">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d0e72-137">Ex.</span></span> <span data-ttu-id="d0e72-138">Un usuario que quieran toounsubscribe de todas las alertas SMS para todos los grupos de acciones, enviaría un toohello SMS 20873 que dice "START"</span><span class="sxs-lookup"><span data-stu-id="d0e72-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="d0e72-139">Solicitud de ayuda a través de SMS</span><span class="sxs-lookup"><span data-stu-id="d0e72-139">Requesting help via SMS</span></span>
<span data-ttu-id="d0e72-140">Un usuario puede solicitar para obtener más información acerca de hello SMS que han recibido por responde toohello 20873 con cualquiera de hello siguientes palabras clave:</span><span class="sxs-lookup"><span data-stu-id="d0e72-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="d0e72-141">HELP</span><span class="sxs-lookup"><span data-stu-id="d0e72-141">HELP</span></span>

<span data-ttu-id="d0e72-142">Usuario toohello con un artículo de toothis de vínculo se enviará una respuesta.</span><span class="sxs-lookup"><span data-stu-id="d0e72-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0e72-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d0e72-143">Next Steps</span></span>
<span data-ttu-id="d0e72-144">Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md) y obtenga información acerca de cómo tooget una alerta</span><span class="sxs-lookup"><span data-stu-id="d0e72-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="d0e72-145">Más información sobre la [limitación de la tasa de SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="d0e72-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="d0e72-146">Más información sobre los [grupos de acciones](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="d0e72-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
