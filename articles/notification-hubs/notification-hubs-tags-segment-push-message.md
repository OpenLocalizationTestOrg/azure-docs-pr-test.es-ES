---
title: aaaRouting y expresiones de etiqueta
description: En este tema se explican las expresiones de etiqueta y enrutamiento de los Centros de notificaciones de Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="b0584-103">Expresiones de etiqueta y enrutamiento</span><span class="sxs-lookup"><span data-stu-id="b0584-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="b0584-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b0584-104">Overview</span></span>
<span data-ttu-id="b0584-105">Expresiones de etiqueta permiten tootarget conjuntos específicos de dispositivos, o más específicamente registros, al enviar una notificación de inserción a través de los centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="b0584-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="b0584-106">Selección del destino de registros específicos</span><span class="sxs-lookup"><span data-stu-id="b0584-106">Targeting specific registrations</span></span>
<span data-ttu-id="b0584-107">Hello solo forma tootarget notificación específica registros es tooassociate etiquetas con ellos, a continuación, tener como destino esas etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b0584-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="b0584-108">Como se describe en [administración de registro](notification-hubs-push-notification-registration-management.md), en la inserción de pedido tooreceive controlen las notificaciones de una aplicación tiene tooregister un dispositivo en un centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="b0584-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="b0584-109">Una vez que se crea un registro en un centro de notificaciones, el back-end de hello aplicación puede enviar tooit de notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="b0584-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="b0584-110">back-end de Hello aplicación puede elegir Hola registros tootarget con una notificación específica de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="b0584-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="b0584-111">**Difusión**: todos los registros en el centro de notificaciones de Hola reciban una notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0584-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="b0584-112">**Etiqueta**: todos los registros que contienen Hola especificado etiqueta recibir una notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0584-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="b0584-113">**Expresión de etiqueta**: todos los registros cuyo conjunto de coincidencia de etiquetas Hola expresión especificada reciben notificación Hola.</span><span class="sxs-lookup"><span data-stu-id="b0584-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="b0584-114">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="b0584-114">Tags</span></span>
<span data-ttu-id="b0584-115">Una etiqueta puede ser cualquier cadena, los caracteres de too120, que contiene alfanuméricos y Hola siguientes caracteres no alfanuméricos: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="b0584-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="b0584-116">Hello en el ejemplo siguiente se muestra una aplicación desde el que puede recibir notificaciones del sistema sobre grupos musicales específicos.</span><span class="sxs-lookup"><span data-stu-id="b0584-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="b0584-117">En este escenario, un notificaciones de tooroute de manera sencilla es toolabel registros con etiquetas que representan distintas bandas hello, como en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="b0584-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="b0584-118">En esta imagen, el mensaje de Hola etiquetado **Beatles** tableta Hola solo alcanza registrada con etiqueta de hello **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="b0584-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="b0584-119">Para obtener más información acerca de la creación de registros de etiquetas, consulte [Administración de registros](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="b0584-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="b0584-120">Se puede enviar tootags notificaciones mediante Hola métodos de las notificaciones de hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` clase Hola [centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span><span class="sxs-lookup"><span data-stu-id="b0584-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="b0584-121">También puede usar Node.js, u Hola API de REST de notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="b0584-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="b0584-122">Este es un ejemplo con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="b0584-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="b0584-123">Las etiquetas no tiene toobe aprovisionado previamente y pueden hacer referencia los conceptos de toomultiple específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0584-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="b0584-124">Por ejemplo, los usuarios de esta aplicación de ejemplo pueden comentar sobre bandas y desea tooreceive notificaciones del sistema, no solo para los comentarios de Hola en sus bandas preferidas, sino también para todos los comentarios de sus amigos, independientemente de la banda de hello en el que desea hacer comentarios.</span><span class="sxs-lookup"><span data-stu-id="b0584-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="b0584-125">Hola siguiente imagen muestra un ejemplo de este escenario:</span><span class="sxs-lookup"><span data-stu-id="b0584-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="b0584-126">En esta imagen, Alice está interesada en las actualizaciones de hello Beatles y Bob está interesado en las actualizaciones de hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="b0584-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="b0584-127">Bob también está interesado en comentarios de Charlie, y Charlie está interesado en hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="b0584-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="b0584-128">Cuando se envía una notificación de comentario de Charlie sobre Hola Beatles, Alice y Bob recibirlo.</span><span class="sxs-lookup"><span data-stu-id="b0584-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="b0584-129">Aunque se pueden codificar varios intereses en etiquetas (por ejemplo, "banda_Beatles" o "sigue_Juan Carlos"), las etiquetas son cadenas simples y no propiedades con valores.</span><span class="sxs-lookup"><span data-stu-id="b0584-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="b0584-130">Un registro coincide solo con hello presencia o ausencia de una etiqueta específica.</span><span class="sxs-lookup"><span data-stu-id="b0584-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="b0584-131">Para obtener un tutorial completo paso a paso sobre cómo toouse etiquetas para enviar toointerest grupos, consulte [noticias de última hora](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="b0584-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="b0584-132">Use etiquetas tootarget usuarios</span><span class="sxs-lookup"><span data-stu-id="b0584-132">Using tags tootarget users</span></span>
<span data-ttu-id="b0584-133">Etiquetas de toouse de otra manera es tooidentify todos los dispositivos de Hola de un usuario concreto.</span><span class="sxs-lookup"><span data-stu-id="b0584-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="b0584-134">Los registros se pueden etiquetar con una etiqueta que contiene un identificador de usuario, como en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="b0584-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="b0584-135">En esta imagen, etiquetada de mensaje de Hola UID: Alice llega a todos los registros etiquetados UID: Alice; por lo tanto, todos los dispositivos de Alice.</span><span class="sxs-lookup"><span data-stu-id="b0584-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="b0584-136">Expresiones de etiqueta</span><span class="sxs-lookup"><span data-stu-id="b0584-136">Tag expressions</span></span>
<span data-ttu-id="b0584-137">Hay casos en que una notificación tiene tootarget un conjunto de registros identificado no por una sola etiqueta, sino por una expresión booleana en las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="b0584-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="b0584-138">Considere la posibilidad de una aplicación de deportes que envía un recordatorio tooeveryone en Boston sobre un partido entre Hola Red Sox y Cardinals.</span><span class="sxs-lookup"><span data-stu-id="b0584-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="b0584-139">Si la aplicación de cliente de hello registra etiquetas sobre interés en los equipos y la ubicación, notificación de hello debe ser destino tooeveryone en Boston interesadas en hello Red Sox u Hola Cardinals.</span><span class="sxs-lookup"><span data-stu-id="b0584-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="b0584-140">Esta condición se puede expresar con hello siguiente expresión booleana:</span><span class="sxs-lookup"><span data-stu-id="b0584-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="b0584-141">Las expresiones de etiqueta pueden contener todos los operadores booleanos, por ejemplo, AND (& &), OR (||) y NOT (!).</span><span class="sxs-lookup"><span data-stu-id="b0584-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="b0584-142">También pueden contener paréntesis.</span><span class="sxs-lookup"><span data-stu-id="b0584-142">They can also contain parentheses.</span></span> <span data-ttu-id="b0584-143">Expresiones de etiqueta están limitados too20 etiquetas si contienen solo or; en caso contrario, son etiquetas too6 limitado.</span><span class="sxs-lookup"><span data-stu-id="b0584-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="b0584-144">Este es un ejemplo para enviar notificaciones con expresiones de etiqueta con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="b0584-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
