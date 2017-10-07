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
# <a name="routing-and-tag-expressions"></a>Expresiones de etiqueta y enrutamiento
## <a name="overview"></a>Información general
Expresiones de etiqueta permiten tootarget conjuntos específicos de dispositivos, o más específicamente registros, al enviar una notificación de inserción a través de los centros de notificaciones.

## <a name="targeting-specific-registrations"></a>Selección del destino de registros específicos
Hello solo forma tootarget notificación específica registros es tooassociate etiquetas con ellos, a continuación, tener como destino esas etiquetas. Como se describe en [administración de registro](notification-hubs-push-notification-registration-management.md), en la inserción de pedido tooreceive controlen las notificaciones de una aplicación tiene tooregister un dispositivo en un centro de notificaciones. Una vez que se crea un registro en un centro de notificaciones, el back-end de hello aplicación puede enviar tooit de notificaciones de inserción.
back-end de Hello aplicación puede elegir Hola registros tootarget con una notificación específica de hello siguientes maneras:

1. **Difusión**: todos los registros en el centro de notificaciones de Hola reciban una notificación de Hola.
2. **Etiqueta**: todos los registros que contienen Hola especificado etiqueta recibir una notificación de Hola.
3. **Expresión de etiqueta**: todos los registros cuyo conjunto de coincidencia de etiquetas Hola expresión especificada reciben notificación Hola.

## <a name="tags"></a>Etiquetas
Una etiqueta puede ser cualquier cadena, los caracteres de too120, que contiene alfanuméricos y Hola siguientes caracteres no alfanuméricos: '_', ' @', '#', '. ',':', '-'. Hello en el ejemplo siguiente se muestra una aplicación desde el que puede recibir notificaciones del sistema sobre grupos musicales específicos. En este escenario, un notificaciones de tooroute de manera sencilla es toolabel registros con etiquetas que representan distintas bandas hello, como en hello después de la imagen.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

En esta imagen, el mensaje de Hola etiquetado **Beatles** tableta Hola solo alcanza registrada con etiqueta de hello **Beatles**.

Para obtener más información acerca de la creación de registros de etiquetas, consulte [Administración de registros](notification-hubs-push-notification-registration-management.md).

Se puede enviar tootags notificaciones mediante Hola métodos de las notificaciones de hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` clase Hola [centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK. También puede usar Node.js, u Hola API de REST de notificaciones de inserción.  Este es un ejemplo con hello SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Las etiquetas no tiene toobe aprovisionado previamente y pueden hacer referencia los conceptos de toomultiple específico de la aplicación. Por ejemplo, los usuarios de esta aplicación de ejemplo pueden comentar sobre bandas y desea tooreceive notificaciones del sistema, no solo para los comentarios de Hola en sus bandas preferidas, sino también para todos los comentarios de sus amigos, independientemente de la banda de hello en el que desea hacer comentarios. Hola siguiente imagen muestra un ejemplo de este escenario:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

En esta imagen, Alice está interesada en las actualizaciones de hello Beatles y Bob está interesado en las actualizaciones de hello Wailers. Bob también está interesado en comentarios de Charlie, y Charlie está interesado en hello Wailers. Cuando se envía una notificación de comentario de Charlie sobre Hola Beatles, Alice y Bob recibirlo.

Aunque se pueden codificar varios intereses en etiquetas (por ejemplo, "banda_Beatles" o "sigue_Juan Carlos"), las etiquetas son cadenas simples y no propiedades con valores. Un registro coincide solo con hello presencia o ausencia de una etiqueta específica.

Para obtener un tutorial completo paso a paso sobre cómo toouse etiquetas para enviar toointerest grupos, consulte [noticias de última hora](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>Use etiquetas tootarget usuarios
Etiquetas de toouse de otra manera es tooidentify todos los dispositivos de Hola de un usuario concreto. Los registros se pueden etiquetar con una etiqueta que contiene un identificador de usuario, como en hello después de imagen:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

En esta imagen, etiquetada de mensaje de Hola UID: Alice llega a todos los registros etiquetados UID: Alice; por lo tanto, todos los dispositivos de Alice.

## <a name="tag-expressions"></a>Expresiones de etiqueta
Hay casos en que una notificación tiene tootarget un conjunto de registros identificado no por una sola etiqueta, sino por una expresión booleana en las etiquetas.

Considere la posibilidad de una aplicación de deportes que envía un recordatorio tooeveryone en Boston sobre un partido entre Hola Red Sox y Cardinals. Si la aplicación de cliente de hello registra etiquetas sobre interés en los equipos y la ubicación, notificación de hello debe ser destino tooeveryone en Boston interesadas en hello Red Sox u Hola Cardinals. Esta condición se puede expresar con hello siguiente expresión booleana:

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

Las expresiones de etiqueta pueden contener todos los operadores booleanos, por ejemplo, AND (& &), OR (||) y NOT (!). También pueden contener paréntesis. Expresiones de etiqueta están limitados too20 etiquetas si contienen solo or; en caso contrario, son etiquetas too6 limitado.

Este es un ejemplo para enviar notificaciones con expresiones de etiqueta con hello SDK.

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
