---
title: "Interfaz de usuario de Azure Mobile Engagement: configuración"
description: "Obtenga información acerca de cómo administrar la configuración global de la aplicación mediante Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af5c81df2b9f288161b38625d3ac2adde8fb195d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-global-settings-of-your-application"></a><span data-ttu-id="69475-103">Cómo administrar la configuración global de la aplicación</span><span class="sxs-lookup"><span data-stu-id="69475-103">How to manage the global settings of your application</span></span>
<span data-ttu-id="69475-104">Las opciones del menú **Configuración** disponibles para una aplicación varían, dependiendo de la plataforma de la aplicación y de los permisos que se le hayan concedido para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69475-104">The **Settings** menu options available for an application vary, depending on the platform of the application and the permissions you have been granted for the application.</span></span> <span data-ttu-id="69475-105">En la configuración se incluyen lo siguiente: Detalles, Proyectos, Inserción nativa, Velocidad de inserción, Etiquetas de información de la aplicación y Presión comercial.</span><span class="sxs-lookup"><span data-stu-id="69475-105">Settings include the following: Details, Projects, Native Push, Push Speed, Tag (app info), and Commercial Pressure.</span></span> <span data-ttu-id="69475-106">La opción de menú Etiquetas de información de la aplicación de la sección de Configuración puede administrarse mediante la aplicación (con el SDK) o mediante el back-end (con la API del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="69475-106">The Tag (app info) menu option of the Settings section can be managed by your application (using the SDK) or by your backend (using the Device API).</span></span> 

> [!NOTE]
> <span data-ttu-id="69475-107">Muchas de las secciones de la interfaz de usuario del portal de **Mobile Engagement** contienen el botón **MOSTRAR AYUDA**.</span><span class="sxs-lookup"><span data-stu-id="69475-107">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="69475-108">Pulse este botón para obtener más información contextual sobre una sección.</span><span class="sxs-lookup"><span data-stu-id="69475-108">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="details"></a><span data-ttu-id="69475-109">Detalles</span><span class="sxs-lookup"><span data-stu-id="69475-109">Details</span></span>
<span data-ttu-id="69475-110">Le permite cambiar el nombre y la descripción de la aplicación, ver el propietario de la aplicación y los permisos de rol.</span><span class="sxs-lookup"><span data-stu-id="69475-110">Allows you to change the name and description of your application, view the owner of your application and your role permissions.</span></span> 

<span data-ttu-id="69475-111">La configuración de análisis permite ver o cambiar el día en que empieza la semana y el tiempo de retención en días.</span><span class="sxs-lookup"><span data-stu-id="69475-111">Analytics configuration enables  you to view or change the day weeks start on and the retention time in day(s).</span></span>

  ![settings1][46]

## <a name="projects"></a><span data-ttu-id="69475-113">Proyectos</span><span class="sxs-lookup"><span data-stu-id="69475-113">Projects</span></span>
<span data-ttu-id="69475-114">Le permite seleccionar todos los proyectos en los que desea que aparezca la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69475-114">Allows you to select all projects you want your application to appear in.</span></span> 

<span data-ttu-id="69475-115">También puede buscar un proyecto y ver el nombre, descripción, propietario y los permisos del rol de cualquier proyecto del que forme parte la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69475-115">You can also search for a project and view the name, description, owner and your role permissions of any project your application is part of.</span></span>

<span data-ttu-id="69475-116">Para obtener más información, consulte [Documentación de la interfaz de usuario - Inicio][Link 13].</span><span class="sxs-lookup"><span data-stu-id="69475-116">For more information, see: [UI Documentation – Home][Link 13]</span></span>

  ![settings3][48]

## <a name="native-push"></a><span data-ttu-id="69475-118">Inserción nativa:</span><span class="sxs-lookup"><span data-stu-id="69475-118">Native Push</span></span>
<span data-ttu-id="69475-119">Permite registrar un nuevo certificado o la eliminación de un certificado existente para usar con la inserción nativa.</span><span class="sxs-lookup"><span data-stu-id="69475-119">Allows you to register a new certificate or delete and existing certificate for use with native push.</span></span> <span data-ttu-id="69475-120">Inserción nativa permite a Azure Mobile Engagement insertar en su aplicación en cualquier momento, aunque no se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="69475-120">Native Push enables Azure Mobile Engagement to push to your application at any time, even when it is not running.</span></span> 

<span data-ttu-id="69475-121">Después de proporcionar las credenciales o certificados para al menos un servicio de inserción nativa, se puede seleccionar "Cualquier hora" al crear campañas de cobertura y también usar el parámetro "notifier" en la API de INSERCIÓN.</span><span class="sxs-lookup"><span data-stu-id="69475-121">After providing credentials or certificates for at least one Native Push service, you can select "Any time" when creating Reach Campaigns, and also use the "notifier" parameter in the PUSH API.</span></span>

### <a name="apple-push-notification-service-apns"></a><span data-ttu-id="69475-122">Servicio de notificaciones de inserción de Apple (APNS)</span><span class="sxs-lookup"><span data-stu-id="69475-122">Apple Push Notification Service (APNS)</span></span>
<span data-ttu-id="69475-123">Para habilitar la inserción nativa mediante el servicio de notificación de inserción de Apple deberá registrar su certificado.</span><span class="sxs-lookup"><span data-stu-id="69475-123">To enable Native Push using the Apple Push Notification Service you will need to register your certificate.</span></span> <span data-ttu-id="69475-124">Deberá especificar el tipo de certificado como de desarrollo (DEV) o de producción (PROD).</span><span class="sxs-lookup"><span data-stu-id="69475-124">You will need to specify the type of certificate as either development (DEV) or production (PROD).</span></span> <span data-ttu-id="69475-125">A continuación, necesitará cargar su certificado y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="69475-125">Then you will need upload your certificate and the password.</span></span>

<span data-ttu-id="69475-126">Para obtener más información, consulte [Documentación del SDK - iOS - Cómo preparar la aplicación para las notificaciones de inserción de Apple][Link 5]</span><span class="sxs-lookup"><span data-stu-id="69475-126">For more information, see: [SDK Documentation - iOS - How to Prepare your Application for Apple Push notifications][Link 5]</span></span>

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a><span data-ttu-id="69475-128">Servicio de notificación de inserción de Windows (WPNS)</span><span class="sxs-lookup"><span data-stu-id="69475-128">Windows Push Notification Service (WPNS)</span></span>
<span data-ttu-id="69475-129">Para habilitar la inserción nativa mediante el servicio de notificación de Windows, debe proporcionar las credenciales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69475-129">To enable Native Push using Windows Notification Service, you must provide your application's credentials.</span></span> <span data-ttu-id="69475-130">Necesitará el identificador de seguridad del paquete (SID) y la clave secreta.</span><span class="sxs-lookup"><span data-stu-id="69475-130">You will need your Package security identifier (SID) and your Secret key.</span></span>

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a><span data-ttu-id="69475-132">Mensajería en la nube de Google para Android (GCM)</span><span class="sxs-lookup"><span data-stu-id="69475-132">Google Cloud Messaging for Android (GCM)</span></span>
<span data-ttu-id="69475-133">Para habilitar la inserción nativa mediante GCM, deberá seguir las instrucciones de Google.</span><span class="sxs-lookup"><span data-stu-id="69475-133">To enable Native Push using GCM, you need to follow the instructions from Google.</span></span> <span data-ttu-id="69475-134">A continuación, debe pegar una clave de API simple de servidor configurada sin restricciones de IP.</span><span class="sxs-lookup"><span data-stu-id="69475-134">Then you must paste a server simple API key, configured without IP restrictions.</span></span> <span data-ttu-id="69475-135">Requiere la integración con el SDK de Android v1.12.0 +.</span><span class="sxs-lookup"><span data-stu-id="69475-135">Requires integration with the SDK for Android v1.12.0+.</span></span>

<span data-ttu-id="69475-136">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="69475-136">For more information, see:</span></span> 

* <span data-ttu-id="69475-137">[Documentación del SDK - Android - Cómo integrar GCM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="69475-137">[SDK Documentation Android How to Integrate GCM][Link 5]</span></span>
* [<span data-ttu-id="69475-138">Guía sobre GCM de Google Developers</span><span class="sxs-lookup"><span data-stu-id="69475-138">Google Developer GCM Guide</span></span>](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a><span data-ttu-id="69475-139">Mensajería de dispositivos de Amazon para Android (ADM)</span><span class="sxs-lookup"><span data-stu-id="69475-139">Amazon Device Messaging for Android (ADM)</span></span>
<span data-ttu-id="69475-140">Para habilitar la inserción nativa con ADM, debe proporcionar <OAuth credentials> de Amazon compuesta de un identificador de cliente y el secreto del cliente (requiere la integración con el SDK de Android v2.1.0+).</span><span class="sxs-lookup"><span data-stu-id="69475-140">To enable Native Push using ADM, you must provide Amazon <OAuth credentials> consisting of a Client ID and Client Secret (Requires integration with SDK for Android v2.1.0+).</span></span>

<span data-ttu-id="69475-141">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="69475-141">For more information, see:</span></span> 

* <span data-ttu-id="69475-142">[Documentación del SDK - Android - Cómo integrar ADM][Link 5]</span><span class="sxs-lookup"><span data-stu-id="69475-142">[SDK Documentation Android How to Integrate ADM][Link 5]</span></span>
* [<span data-ttu-id="69475-143">Documentación sobre ADM para desarrolladores de Amazon</span><span class="sxs-lookup"><span data-stu-id="69475-143">Amazon Developer ADM Documentation</span></span>](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a><span data-ttu-id="69475-145">Velocidad de inserción</span><span class="sxs-lookup"><span data-stu-id="69475-145">Push Speed</span></span>
<span data-ttu-id="69475-146">Muestra la velocidad de inserción actual de la aplicación y le permite definir la velocidad de inserción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69475-146">Shows the current push speed of your application and allows you to define the push speed of your application.</span></span>

  ![settings7][52]

## <a name="tag-app-info"></a><span data-ttu-id="69475-148">Etiqueta de información de aplicación</span><span class="sxs-lookup"><span data-stu-id="69475-148">Tag (app info)</span></span>
![settings11][56]

## <a name="commercial-pressure"></a><span data-ttu-id="69475-150">Presión comercial</span><span class="sxs-lookup"><span data-stu-id="69475-150">Commercial Pressure</span></span>
![settings12][57]

## <a name="see-also"></a><span data-ttu-id="69475-152">Consulte también</span><span class="sxs-lookup"><span data-stu-id="69475-152">See also</span></span>
* <span data-ttu-id="69475-153">[Conceptos][Link 6]</span><span class="sxs-lookup"><span data-stu-id="69475-153">[Concepts][Link 6]</span></span>
* <span data-ttu-id="69475-154">[Guía de solución de problemas de servicios][Link 24]</span><span class="sxs-lookup"><span data-stu-id="69475-154">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

