---
title: "limitar aaaRate de SMS, mensajes de correo electrónico y webhooks | Documentos de Microsoft"
description: "Entender cómo Azure limita el número de Hola de notificaciones de SMS, correo electrónico o webhook posibles de un grupo de acción."
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="7f1b0-103">Limitación del número de mensajes SMS, correo electrónico y envíos webhook</span><span class="sxs-lookup"><span data-stu-id="7f1b0-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="7f1b0-104">Limitación de velocidad es una suspensión de las notificaciones que se produce cuando se envían notificaciones demasiados tooa dirección de correo electrónico o número de teléfono específico.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="7f1b0-105">La limitación del índice asegura que las alertas son fáciles de administrar y procesar.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="7f1b0-106">reglas de Hola de SMS y correo electrónico no son Hola igual.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="7f1b0-107">umbral de límite de velocidad de Hello es:</span><span class="sxs-lookup"><span data-stu-id="7f1b0-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="7f1b0-108">**SMS**: 10 mensajes en una hora.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="7f1b0-109">**Correo electrónico**: 100 mensajes en una hora.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="7f1b0-110">Reglas de limitación de número</span><span class="sxs-lookup"><span data-stu-id="7f1b0-110">Rate limit rules</span></span>
- <span data-ttu-id="7f1b0-111">Un número de teléfono particular o correo electrónico es velocidad limitada cuando recibe los mensajes de más de umbral de Hola que permite.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="7f1b0-112">Un número de teléfono o correo electrónico puede formar parte de grupos de acciones de muchas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="7f1b0-113">La limitación de número se aplica en todas las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="7f1b0-114">Se aplica en cuanto se alcanza el umbral de hello, incluso si se envían los mensajes de varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="7f1b0-115">Cuando un número de teléfono o correo electrónico es tasa limitado, se envía una notificación de adicional toocommunicate Hola de limitación de velocidad.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="7f1b0-116">Hello notificación Estados cuando hello velocidad limitar expira.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="7f1b0-117">Limitación de número para los webhooks</span><span class="sxs-lookup"><span data-stu-id="7f1b0-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="7f1b0-118">Actualmente, no hay ninguna limitación en vigor para webhooks.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f1b0-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f1b0-119">Next steps</span></span> ##
* <span data-ttu-id="7f1b0-120">Más información sobre el [comportamiento de las alertas por SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7f1b0-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="7f1b0-121">Obtener un [información general de alertas de registro de actividad](monitoring-overview-alerts.md)y obtenga información acerca de cómo tooreceive alertas.</span><span class="sxs-lookup"><span data-stu-id="7f1b0-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="7f1b0-122">Obtenga información acerca de cómo demasiado[configurar alertas siempre que se registra una notificación de estado de servicio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7f1b0-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
