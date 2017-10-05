---
title: Expresiones de etiqueta y enrutamiento
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
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="14aa4-103">Expresiones de etiqueta y enrutamiento</span><span class="sxs-lookup"><span data-stu-id="14aa4-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="14aa4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="14aa4-104">Overview</span></span>
<span data-ttu-id="14aa4-105">Las expresiones de etiqueta le permiten dirigirse a conjuntos específicos de dispositivos, o más específicamente a registros, al enviar una notificación push a través de Centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="14aa4-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="14aa4-106">Selección del destino de registros específicos</span><span class="sxs-lookup"><span data-stu-id="14aa4-106">Targeting specific registrations</span></span>
<span data-ttu-id="14aa4-107">La única forma de seleccionar el destino de registros de notificaciones específicos es asociar etiquetas con ellos y, a continuación, seleccionar el destino de esas etiquetas.</span><span class="sxs-lookup"><span data-stu-id="14aa4-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="14aa4-108">Como se describe en [Administración de registros](notification-hubs-push-notification-registration-management.md), con el fin de recibir notificaciones de inserción, una aplicación tiene que registrar un identificador de dispositivo en un centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="14aa4-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="14aa4-109">Una vez que se crea un registro en un centro de notificaciones, el back-end de la aplicación puede enviar notificaciones de inserción a este.</span><span class="sxs-lookup"><span data-stu-id="14aa4-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="14aa4-110">El back-end de la aplicación puede elegir a qué registros dirigirse con una notificación específica de las maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="14aa4-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="14aa4-111">**Difusión**: todos los registros del centro de notificaciones reciben la notificación.</span><span class="sxs-lookup"><span data-stu-id="14aa4-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="14aa4-112">**Etiquetar**: todos los registros que contienen la etiqueta especificada reciben la notificación.</span><span class="sxs-lookup"><span data-stu-id="14aa4-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="14aa4-113">**Expresión de etiqueta**: todos los registros cuyo conjunto de etiquetas coincide con la expresión especificada reciben la notificación.</span><span class="sxs-lookup"><span data-stu-id="14aa4-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="14aa4-114">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="14aa4-114">Tags</span></span>
<span data-ttu-id="14aa4-115">Una etiqueta puede ser cualquier cadena, hasta 120 caracteres, que contiene y los siguientes caracteres no alfanuméricos: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="14aa4-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="14aa4-116">En el ejemplo siguiente se muestra una aplicación desde la que puede recibir notificaciones del sistema sobre grupos musicales específicos.</span><span class="sxs-lookup"><span data-stu-id="14aa4-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="14aa4-117">En este escenario, una manera sencilla de enrutar notificaciones es etiquetar los registros con etiquetas que representan las distintas bandas, como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="14aa4-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="14aa4-118">En esta imagen, el mensaje etiquetado **Beatles** llega solamente a la tableta registrada con la etiqueta **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="14aa4-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="14aa4-119">Para obtener más información acerca de la creación de registros de etiquetas, consulte [Administración de registros](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="14aa4-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="14aa4-120">Puede enviar notificaciones a etiquetas mediante los métodos de las notificaciones de envío de la clase `Microsoft.Azure.NotificationHubs.NotificationHubClient` en el SDK de [Centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) .</span><span class="sxs-lookup"><span data-stu-id="14aa4-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="14aa4-121">También puede usar Node.js o las API de REST de notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="14aa4-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="14aa4-122">A continuación se facilita un ejemplo mediante el uso del SDK.</span><span class="sxs-lookup"><span data-stu-id="14aa4-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="14aa4-123">Las etiquetas no tienen que aprovisionarse previamente y pueden hacer referencia a varios conceptos específicos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="14aa4-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="14aa4-124">Por ejemplo, los usuarios de esta aplicación de ejemplo pueden comentar sobre bandas y desean recibir notificaciones del sistema, no solo de los comentarios sobre sus bandas preferidas, sino también de todos los comentarios de sus amigos, independientemente de la banda sobre la que estén comentando.</span><span class="sxs-lookup"><span data-stu-id="14aa4-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="14aa4-125">En la siguiente imagen se muestra un ejemplo de este escenario:</span><span class="sxs-lookup"><span data-stu-id="14aa4-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="14aa4-126">En esta imagen, Ana está interesada en recibir actualizaciones sobre los Beatles y Pedro está interesado en las actualizaciones sobre los Wailers.</span><span class="sxs-lookup"><span data-stu-id="14aa4-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="14aa4-127">Bob también está interesado en los comentarios de Juan Carlos, y Juan Carlos está interesado en los Wailers.</span><span class="sxs-lookup"><span data-stu-id="14aa4-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="14aa4-128">Cuando se envía una notificación sobre el comentario de Juan Carlos acerca de los Beatles, Ana y Pedro la reciben.</span><span class="sxs-lookup"><span data-stu-id="14aa4-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="14aa4-129">Aunque se pueden codificar varios intereses en etiquetas (por ejemplo, "banda_Beatles" o "sigue_Juan Carlos"), las etiquetas son cadenas simples y no propiedades con valores.</span><span class="sxs-lookup"><span data-stu-id="14aa4-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="14aa4-130">Los registros coinciden solo con la presencia o ausencia de una etiqueta específica.</span><span class="sxs-lookup"><span data-stu-id="14aa4-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="14aa4-131">Para obtener un tutorial completo detallado sobre cómo usar etiquetas para enviar a grupos de interés, consulte [Noticias de última hora](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="14aa4-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="14aa4-132">Uso de etiquetas para los usuarios de destino</span><span class="sxs-lookup"><span data-stu-id="14aa4-132">Using tags to target users</span></span>
<span data-ttu-id="14aa4-133">Otra forma de usar etiquetas es identificar todos los dispositivos de un usuario concreto.</span><span class="sxs-lookup"><span data-stu-id="14aa4-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="14aa4-134">Los registros se pueden etiquetar con una etiqueta que contenga un identificador de usuario, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="14aa4-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="14aa4-135">En esta imagen, el mensaje etiquetado mediante uid:Ana llega a todos los registros etiquetados como uid:Ana; por lo tanto, a todos los dispositivos de Ana.</span><span class="sxs-lookup"><span data-stu-id="14aa4-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="14aa4-136">Expresiones de etiqueta</span><span class="sxs-lookup"><span data-stu-id="14aa4-136">Tag expressions</span></span>
<span data-ttu-id="14aa4-137">Hay casos en que una notificación tiene como destino un conjunto de registros identificado no por una sola etiqueta, sino por una expresión booleana en las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="14aa4-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="14aa4-138">Tome una aplicación de deportes que envía un recordatorio a todas las personas de Boston sobre un partido entre los Red Sox y los Cardinals.</span><span class="sxs-lookup"><span data-stu-id="14aa4-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="14aa4-139">Si la aplicación cliente registra etiquetas sobre intereses en equipos y ubicaciones, la notificación deberá dirigirse a todas las personas de Boston interesadas en los Red Sox o en los Cardinals.</span><span class="sxs-lookup"><span data-stu-id="14aa4-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="14aa4-140">Esta condición se puede expresar mediante la siguiente expresión booleana:</span><span class="sxs-lookup"><span data-stu-id="14aa4-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="14aa4-141">Las expresiones de etiqueta pueden contener todos los operadores booleanos, por ejemplo, AND (& &), OR (||) y NOT (!).</span><span class="sxs-lookup"><span data-stu-id="14aa4-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="14aa4-142">También pueden contener paréntesis.</span><span class="sxs-lookup"><span data-stu-id="14aa4-142">They can also contain parentheses.</span></span> <span data-ttu-id="14aa4-143">Las expresiones de etiqueta se limita a 20 etiquetas si contienen solamente OR; de lo contrario, se limitan a 6 etiquetas.</span><span class="sxs-lookup"><span data-stu-id="14aa4-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="14aa4-144">A continuación se muestra un ejemplo de envío de notificaciones con expresiones de etiqueta mediante el SDK.</span><span class="sxs-lookup"><span data-stu-id="14aa4-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
