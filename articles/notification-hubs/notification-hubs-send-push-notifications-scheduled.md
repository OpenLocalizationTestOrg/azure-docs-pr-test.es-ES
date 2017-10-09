---
title: aaaHow toosend programada notificaciones | Documentos de Microsoft
description: "En este tema se describe cómo usar Notificaciones programadas con Centros de notificaciones de Azure."
services: notification-hubs
documentationcenter: .net
keywords: "notificaciones push, notificación push, programación de notificaciones push"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a>Envío de notificaciones programadas
## <a name="overview"></a>Información general
Si tiene un escenario en el que desea toosend una notificación en algún punto de hello futura, pero no tiene un toowake fácilmente la notificación de hello toosend código del back-end. Los centros de notificaciones de nivel estándar admite una característica que permite tooschedule notificaciones días laborables too7 Hola futuras.

Cuando se envía una notificación, utilice simplemente hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) clase hello SDK de los centros de notificaciones como se muestra en el siguiente ejemplo de Hola:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

Además, puede cancelar una notificación programada anteriormente con su notificationId:

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

No hay ningún límite en el número de Hola de notificaciones programadas que se puede enviar.

