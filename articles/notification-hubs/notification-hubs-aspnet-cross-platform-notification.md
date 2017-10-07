---
title: aaaSend notificaciones multiplataforma toousers con centros de notificaciones (ASP.NET)
description: "Obtenga información acerca de cómo toosend toouse de las plantillas de los centros de notificaciones, en una sola solicitud, una notificación independiente de la plataforma que tenga como destino todas las plataformas."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Enviar notificaciones multiplataforma toousers con centros de notificaciones
En el tutorial anterior hello [notificar a los usuarios con centros de notificaciones], ha aprendido cómo los dispositivos de toopush notificaciones tooall registran por un usuario autenticado concreto. En este tutorial, varias solicitudes eran toosend requiere una plataforma de cliente de tooeach admitida la notificación. Notificación de concentradores es compatible con plantillas, que le permiten especificar cómo desea que las notificaciones de tooreceive un dispositivo específico. Con esto se simplifica el envío de notificaciones entre plataformas. Este tema se muestra cómo tootake aprovechar toosend de plantillas, en una sola solicitud, una notificación independiente de la plataforma que tenga como destino todas las plataformas. Para más información sobre las plantillas, consulte [Introducción a Azure Notification Hubs][Templates].
> [!IMPORTANT]
> Los proyectos de Windows Phone 8.1 y versiones anteriores no se admiten en Visual Studio 2017. Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Centros de notificaciones permite que un dispositivo tooregister varias plantillas con hello misma etiqueta. En este caso, un mensaje entrante que se generan varias notificaciones de etiqueta de destino entrega toohello dispositivo, uno por cada plantilla. Esto permite toodisplay Hola mismo mensaje en varias notificaciones visuales, por ejemplo, como un distintivo y como una notificación del sistema en una aplicación de la tienda de Windows.
> 
> 

Completar Hola siguiendo las notificaciones de pasos toosend multiplataforma mediante plantillas:

1. Hola el Explorador de soluciones en Visual Studio, expanda hello **controladores** carpeta y, a continuación, archivo de RegisterController.cs de hello abierto.
2. Busque el bloque de Hola de código de hello **colocar** método que crea un nuevo registro reemplazar hello `switch` contenido con el siguiente código de hello:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Este código llama Hola método específico de la plataforma toocreate un registro de plantilla en lugar de un registro nativo. No se deben modificar los registros existentes, dado que los registros de plantilla derivan de los registros nativos.
3. Hola **notificaciones** controlador, replace hello **sendNotification** método con el siguiente código de hello:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Este código envía una notificación tooall plataformas en Hola mismo tiempo y sin necesidad de toospecify una carga nativo. Compilaciones de centros de notificaciones y entrega Hola dispositivo tooevery de carga correcto con hello proporciona *etiqueta* valor, según lo especificado en las plantillas de hello registrado.
4. Publique de nuevo su proyecto de back-end de WebApi.
5. Vuelva a ejecutar la aplicación de cliente de hello y compruebe que el registro se realiza correctamente.
6. (Opcional) Implementar el dispositivo de segundo de tooa de aplicación de cliente de Hola y luego ejecute la aplicación hello.
   
    Observe que aparecerá una notificación en cada dispositivo.

## <a name="next-steps"></a>Pasos siguientes
Ahora que completó este tutorial, obtenga más información acerca de los Centros de notificaciones y las plantillas en estos temas:

* **[Usar toosend centros de notificaciones noticias de última hora]** <br/>(C# para Tienda Windows / iOS)Muestra otro escenario para el uso de las plantillas
* **[Introducción a Azure Notification Hubs][Templates]**<br/>Este tema de información general contiene información más detallada sobre las plantillas.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Usar toosend centros de notificaciones noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[notificar a los usuarios con centros de notificaciones]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
