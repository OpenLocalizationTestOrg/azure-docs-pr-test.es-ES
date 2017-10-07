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
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="2c571-103">Enviar notificaciones multiplataforma toousers con centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="2c571-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="2c571-104">En el tutorial anterior hello [notificar a los usuarios con centros de notificaciones], ha aprendido cómo los dispositivos de toopush notificaciones tooall registran por un usuario autenticado concreto.</span><span class="sxs-lookup"><span data-stu-id="2c571-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="2c571-105">En este tutorial, varias solicitudes eran toosend requiere una plataforma de cliente de tooeach admitida la notificación.</span><span class="sxs-lookup"><span data-stu-id="2c571-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="2c571-106">Notificación de concentradores es compatible con plantillas, que le permiten especificar cómo desea que las notificaciones de tooreceive un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="2c571-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="2c571-107">Con esto se simplifica el envío de notificaciones entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="2c571-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="2c571-108">Este tema se muestra cómo tootake aprovechar toosend de plantillas, en una sola solicitud, una notificación independiente de la plataforma que tenga como destino todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="2c571-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="2c571-109">Para más información sobre las plantillas, consulte [Introducción a Azure Notification Hubs][Templates].</span><span class="sxs-lookup"><span data-stu-id="2c571-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2c571-110">Los proyectos de Windows Phone 8.1 y versiones anteriores no se admiten en Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2c571-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="2c571-111">Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="2c571-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="2c571-112">Centros de notificaciones permite que un dispositivo tooregister varias plantillas con hello misma etiqueta.</span><span class="sxs-lookup"><span data-stu-id="2c571-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="2c571-113">En este caso, un mensaje entrante que se generan varias notificaciones de etiqueta de destino entrega toohello dispositivo, uno por cada plantilla.</span><span class="sxs-lookup"><span data-stu-id="2c571-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="2c571-114">Esto permite toodisplay Hola mismo mensaje en varias notificaciones visuales, por ejemplo, como un distintivo y como una notificación del sistema en una aplicación de la tienda de Windows.</span><span class="sxs-lookup"><span data-stu-id="2c571-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="2c571-115">Completar Hola siguiendo las notificaciones de pasos toosend multiplataforma mediante plantillas:</span><span class="sxs-lookup"><span data-stu-id="2c571-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="2c571-116">Hola el Explorador de soluciones en Visual Studio, expanda hello **controladores** carpeta y, a continuación, archivo de RegisterController.cs de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="2c571-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="2c571-117">Busque el bloque de Hola de código de hello **colocar** método que crea un nuevo registro reemplazar hello `switch` contenido con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="2c571-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="2c571-118">Este código llama Hola método específico de la plataforma toocreate un registro de plantilla en lugar de un registro nativo.</span><span class="sxs-lookup"><span data-stu-id="2c571-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="2c571-119">No se deben modificar los registros existentes, dado que los registros de plantilla derivan de los registros nativos.</span><span class="sxs-lookup"><span data-stu-id="2c571-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="2c571-120">Hola **notificaciones** controlador, replace hello **sendNotification** método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="2c571-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="2c571-121">Este código envía una notificación tooall plataformas en Hola mismo tiempo y sin necesidad de toospecify una carga nativo.</span><span class="sxs-lookup"><span data-stu-id="2c571-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="2c571-122">Compilaciones de centros de notificaciones y entrega Hola dispositivo tooevery de carga correcto con hello proporciona *etiqueta* valor, según lo especificado en las plantillas de hello registrado.</span><span class="sxs-lookup"><span data-stu-id="2c571-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="2c571-123">Publique de nuevo su proyecto de back-end de WebApi.</span><span class="sxs-lookup"><span data-stu-id="2c571-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="2c571-124">Vuelva a ejecutar la aplicación de cliente de hello y compruebe que el registro se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="2c571-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="2c571-125">(Opcional) Implementar el dispositivo de segundo de tooa de aplicación de cliente de Hola y luego ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2c571-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="2c571-126">Observe que aparecerá una notificación en cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2c571-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c571-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c571-127">Next Steps</span></span>
<span data-ttu-id="2c571-128">Ahora que completó este tutorial, obtenga más información acerca de los Centros de notificaciones y las plantillas en estos temas:</span><span class="sxs-lookup"><span data-stu-id="2c571-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="2c571-129">**[Usar toosend centros de notificaciones noticias de última hora]**</span><span class="sxs-lookup"><span data-stu-id="2c571-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="2c571-130">(C# para Tienda Windows / iOS)Muestra otro escenario para el uso de las plantillas</span><span class="sxs-lookup"><span data-stu-id="2c571-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="2c571-131">**[Introducción a Azure Notification Hubs][Templates]**</span><span class="sxs-lookup"><span data-stu-id="2c571-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="2c571-132">Este tema de información general contiene información más detallada sobre las plantillas.</span><span class="sxs-lookup"><span data-stu-id="2c571-132">Overview topic has more detailed information on templates.</span></span>

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
