---
title: "Envío de notificaciones entre plataformas a los usuarios con Centros de notificaciones (ASP.NET)"
description: "Obtenga información acerca de cómo utilizar las plantillas de los Centros de notificaciones para enviar, en una sola solicitud, una notificación independiente de plataforma que tenga como destino todas las plataformas."
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
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="9636d-103">Envío de notificaciones entre plataformas a los usuarios con Centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9636d-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="9636d-104">En el tutorial anterior, [Notificación a los usuarios con Centros de notificaciones], aprendió a insertar notificaciones en todos los dispositivos que tiene registrado un usuario autenticado específico.</span><span class="sxs-lookup"><span data-stu-id="9636d-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="9636d-105">En ese tutorial, se necesitaban varias solicitudes para enviar una notificación a cada plataforma de cliente compatible.</span><span class="sxs-lookup"><span data-stu-id="9636d-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="9636d-106">Los Centros de notificaciones son compatibles con plantillas, que le permiten especificar cómo un dispositivo específico desea recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9636d-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="9636d-107">Con esto se simplifica el envío de notificaciones entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="9636d-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="9636d-108">Este tema muestra cómo aprovecha las plantillas para enviar, en una sola solicitud, una notificación independiente de la plataforma que se dirige a todas las plataformas.</span><span class="sxs-lookup"><span data-stu-id="9636d-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="9636d-109">Para más información sobre las plantillas, consulte [Introducción a Azure Notification Hubs][Templates].</span><span class="sxs-lookup"><span data-stu-id="9636d-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9636d-110">Los proyectos de Windows Phone 8.1 y versiones anteriores no se admiten en Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9636d-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="9636d-111">Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="9636d-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="9636d-112">Los Centros de notificaciones permiten que un dispositivo registre varias plantillas con la misma etiqueta.</span><span class="sxs-lookup"><span data-stu-id="9636d-112">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="9636d-113">En este caso, un mensaje entrante dirigido a esa etiqueta da lugar a que se entreguen varias notificaciones al dispositivo, una por cada plantilla.</span><span class="sxs-lookup"><span data-stu-id="9636d-113">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="9636d-114">Esto le permite mostrar el mismo mensaje en varias notificaciones visuales, como distintivo y como notificación del sistema en una aplicación de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="9636d-114">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="9636d-115">Lleve a cabo los siguientes pasos para enviar notificaciones entre plataformas mediante plantillas:</span><span class="sxs-lookup"><span data-stu-id="9636d-115">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="9636d-116">En el Explorador de soluciones en Visual Studio, expanda la carpeta **Controladores** y, a continuación, abra el archivo RegisterController.cs.</span><span class="sxs-lookup"><span data-stu-id="9636d-116">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="9636d-117">Encuentre el bloque de código en el método **Put** que crea un registro y reemplace el contenido de `switch` por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="9636d-117">Locate the block of code in the **Put** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
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
   
    <span data-ttu-id="9636d-118">Este código llama al método específico de la plataforma para crear un registro de plantilla en lugar de un registro nativo.</span><span class="sxs-lookup"><span data-stu-id="9636d-118">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="9636d-119">No se deben modificar los registros existentes, dado que los registros de plantilla derivan de los registros nativos.</span><span class="sxs-lookup"><span data-stu-id="9636d-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="9636d-120">En el controlador **Notifications**, reemplace el método **sendNotification** por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="9636d-120">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="9636d-121">Este código envía una notificación a todas las plataformas al mismo tiempo y sin que sea necesario especificar una carga nativa.</span><span class="sxs-lookup"><span data-stu-id="9636d-121">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="9636d-122">Los Centros de notificaciones crean y entregan la carga correcta a cada dispositivo con el valor de *etiqueta* especificado, como se indica en las plantillas registradas.</span><span class="sxs-lookup"><span data-stu-id="9636d-122">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="9636d-123">Publique de nuevo su proyecto de back-end de WebApi.</span><span class="sxs-lookup"><span data-stu-id="9636d-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="9636d-124">Ejecute la aplicación cliente otra vez y compruebe que el registro se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="9636d-124">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="9636d-125">(Opcional) Implemente la aplicación cliente en un segundo dispositivo y, a continuación, ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9636d-125">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="9636d-126">Observe que aparecerá una notificación en cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9636d-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9636d-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9636d-127">Next Steps</span></span>
<span data-ttu-id="9636d-128">Ahora que completó este tutorial, obtenga más información acerca de los Centros de notificaciones y las plantillas en estos temas:</span><span class="sxs-lookup"><span data-stu-id="9636d-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="9636d-129">**[Uso de los Centros de notificaciones para enviar noticias de última hora]**</span><span class="sxs-lookup"><span data-stu-id="9636d-129">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="9636d-130">(C# para Tienda Windows / iOS)Muestra otro escenario para el uso de las plantillas</span><span class="sxs-lookup"><span data-stu-id="9636d-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="9636d-131">**[Introducción a Azure Notification Hubs][Templates]**</span><span class="sxs-lookup"><span data-stu-id="9636d-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="9636d-132">Este tema de información general contiene información más detallada sobre las plantillas.</span><span class="sxs-lookup"><span data-stu-id="9636d-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

<span data-ttu-id="9636d-133">[Uso de los Centros de notificaciones para enviar noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="9636d-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
<span data-ttu-id="9636d-134">[Notificación a los usuarios con Centros de notificaciones]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="9636d-134">[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
