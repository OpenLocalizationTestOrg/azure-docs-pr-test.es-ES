---
title: "Limitación del número de SMS, correos electrónicos y webhooks | Microsoft Docs"
description: "Conozca cómo limita Azure el número de notificaciones de webhook, mensajes de correo electrónico o SMS posibles desde un grupo de acciones."
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
ms.openlocfilehash: bde645624ab1860d19ba18470f55845855a7d1fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="7b882-103">Limitación del número de mensajes SMS, correo electrónico y envíos webhook</span><span class="sxs-lookup"><span data-stu-id="7b882-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="7b882-104">La limitación de número supone una suspensión de las notificaciones que se produce cuando se envían demasiadas a un número de teléfono o dirección de correo electrónico determinados.</span><span class="sxs-lookup"><span data-stu-id="7b882-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number or email address.</span></span> <span data-ttu-id="7b882-105">La limitación del índice asegura que las alertas son fáciles de administrar y procesar.</span><span class="sxs-lookup"><span data-stu-id="7b882-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="7b882-106">Las reglas para SMS y correo electrónico son las mismas.</span><span class="sxs-lookup"><span data-stu-id="7b882-106">The rules for SMS and email are the same.</span></span> <span data-ttu-id="7b882-107">El umbral de la limitación de número es:</span><span class="sxs-lookup"><span data-stu-id="7b882-107">The rate limit threshold is:</span></span>

 - <span data-ttu-id="7b882-108">**SMS**: 10 mensajes en una hora.</span><span class="sxs-lookup"><span data-stu-id="7b882-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="7b882-109">**Correo electrónico**: 100 mensajes en una hora.</span><span class="sxs-lookup"><span data-stu-id="7b882-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="7b882-110">Reglas de limitación de número</span><span class="sxs-lookup"><span data-stu-id="7b882-110">Rate limit rules</span></span>
- <span data-ttu-id="7b882-111">Un número de teléfono o correo electrónico particular se limitan cuando reciben más mensajes de los que permite el umbral.</span><span class="sxs-lookup"><span data-stu-id="7b882-111">A particular phone number or email is rate limited when it receives more messages than the threshold allows.</span></span>
- <span data-ttu-id="7b882-112">Un número de teléfono o correo electrónico puede formar parte de grupos de acciones de muchas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="7b882-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="7b882-113">La limitación de número se aplica en todas las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="7b882-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="7b882-114">En cuanto se alcanza el umbral, se aplica incluso si se envían los mensajes desde varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="7b882-114">It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="7b882-115">Cuando un número de teléfono o un correo electrónico están limitados, se envía una notificación adicional del mismo tipo para comunicar la limitación.</span><span class="sxs-lookup"><span data-stu-id="7b882-115">When a phone number or email is rate limited, an additional notification is sent to communicate the rate limiting.</span></span> <span data-ttu-id="7b882-116">La notificación indica cuándo expira la limitación.</span><span class="sxs-lookup"><span data-stu-id="7b882-116">The notification states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="7b882-117">Limitación de número para los webhooks</span><span class="sxs-lookup"><span data-stu-id="7b882-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="7b882-118">Actualmente, no hay ninguna limitación en vigor para webhooks.</span><span class="sxs-lookup"><span data-stu-id="7b882-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b882-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b882-119">Next steps</span></span> ##
* <span data-ttu-id="7b882-120">Más información sobre el [comportamiento de las alertas por SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7b882-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="7b882-121">Consulte la [introducción a las alertas del registro de actividad](monitoring-overview-alerts.md) y aprenda cómo puede recibir alertas.</span><span class="sxs-lookup"><span data-stu-id="7b882-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="7b882-122">Aprenda a [configurar alertas siempre que se publique una notificación de mantenimiento de un servicio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7b882-122">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
