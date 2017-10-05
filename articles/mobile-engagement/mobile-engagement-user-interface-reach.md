---
title: 'Interfaz de usuario de Azure Mobile Engagement: cobertura'
description: "Obtenga información acerca de cómo llegar a los usuarios de su aplicación mediante notificaciones de inserción usando Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: ce30456e41ff1a2f4824bcb64246ee115fdd1ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="99918-103">Cómo llegar a los usuarios de su aplicación mediante notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="99918-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="99918-104">En este artículo se describe la pestaña **ALCANCE** del portal de **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="99918-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="99918-105">Utilice el portal **Mobile Engagement** para supervisar y administrar sus aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="99918-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="99918-106">Tenga en cuenta que, para comenzar a usar el portal, debe crear en primer lugar una cuenta de **Azure Mobile Engagement** .</span><span class="sxs-lookup"><span data-stu-id="99918-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="99918-107">Para obtener más información, consulte [Crear una cuenta de Azure Mobile Engagement](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="99918-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="99918-108">La sección de cobertura de la interfaz de usuario es la herramienta de administración de campaña de inserción en la que puede crear/editar/activar/finalizar/supervisar y obtener estadísticas de las campañas de notificaciones de inserción y funciones a las que también se puede acceder a través de la API de cobertura (y algunos elementos de la API de inserción de bajo nivel).</span><span class="sxs-lookup"><span data-stu-id="99918-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="99918-109">Recuerde que tanto si está utilizando las API o la interfaz de usuario, deberá integrar Azure Mobile Engagement y la cobertura en la aplicación para cada plataforma con el SDK para poder utilizar campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="99918-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="99918-110">Muchas de las secciones de la interfaz de usuario del portal de **Mobile Engagement** contienen el botón **MOSTRAR AYUDA**.</span><span class="sxs-lookup"><span data-stu-id="99918-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="99918-111">Pulse este botón para obtener más información contextual sobre una sección.</span><span class="sxs-lookup"><span data-stu-id="99918-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="99918-112">Cuatro tipos de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="99918-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="99918-113">Anuncios: le permiten enviar mensajes de publicidad a los usuarios que los redireccionan a otra ubicación dentro de la aplicación o enviarlos a una página web o tienda fuera de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99918-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="99918-114">Sondeos: le permiten reunir información de los usuarios finales formulándoles preguntas.</span><span class="sxs-lookup"><span data-stu-id="99918-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="99918-115">Inserciones de datos: le permiten enviar un archivo de datos binario o base64.</span><span class="sxs-lookup"><span data-stu-id="99918-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="99918-116">La información contenida en una inserción de datos se envía a la aplicación para modificar la actual experiencia del usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99918-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="99918-117">La aplicación debe ser capaz de procesar los datos de una inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="99918-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="99918-118">Detalles de la campaña</span><span class="sxs-lookup"><span data-stu-id="99918-118">Campaign Details</span></span>
<span data-ttu-id="99918-119">Puede editar, clonar, eliminar o activar las campañas que no se han activado todavía pasando el mouse sobre sus nombres o puede hacer clic para abrirlas.</span><span class="sxs-lookup"><span data-stu-id="99918-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="99918-120">Se pueden clonar las campañas que ya se han activado pasando el mouse sobre sus nombres o puede hacer clic para abrirlas.</span><span class="sxs-lookup"><span data-stu-id="99918-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="99918-121">Sin embargo, no puede cambiar una campaña una vez activada.</span><span class="sxs-lookup"><span data-stu-id="99918-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="99918-123">Comentarios sobre la cobertura</span><span class="sxs-lookup"><span data-stu-id="99918-123">Reach Feedback</span></span>
<span data-ttu-id="99918-124">Haga clic en **Estadísticas** para ver los detalles de una campaña de cobertura.</span><span class="sxs-lookup"><span data-stu-id="99918-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="99918-125">La vista **sencilla** proporciona una representación visual en forma de un gráfico de barras de columnas de lo que ha ocurrido después de que se activara una campaña.</span><span class="sxs-lookup"><span data-stu-id="99918-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="99918-126">La vista **avanzada** proporciona detalles más específicos sorbe la campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="99918-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="99918-127">Estos detalles no estarán disponibles si va a enviar una campaña de prueba, es decir, se envía una inserción a un dispositivo de prueba.</span><span class="sxs-lookup"><span data-stu-id="99918-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="99918-128">A continuación le mostramos cómo interpretar estos detalles:</span><span class="sxs-lookup"><span data-stu-id="99918-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="99918-129">**Insertados** : especifica el número de mensajes insertados en los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="99918-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="99918-130">Este número dependerá de la audiencia de destino que especificara al crear la campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="99918-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="99918-131">Si no especifica ninguna audiencia de destino, se enviará esta inserción a todos los dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="99918-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="99918-132">Al igual que sucede con todos los demás servicios de inserción, no inserte las notificaciones directamente en el dispositivo, insértelas en los servicios de notificaciones de inserción específicos de la plataforma respectiva (PNS: APNs/GCM/WNS) para que puedan entregar las notificaciones a los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="99918-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="99918-133">**Entregados** : especifica el número de mensajes que el PNS entrega correctamente al dispositivo y que el SDK de Mobile Engagement confirma como recibidos.</span><span class="sxs-lookup"><span data-stu-id="99918-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="99918-134">*Razones de que el número de entregados sea inferior al número de insertados:*</span><span class="sxs-lookup"><span data-stu-id="99918-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="99918-135">Si el usuario ha desinstalado la aplicación del dispositivo pero el PNS no lo sabe cuando le enviamos la inserción, el mensaje se eliminará.</span><span class="sxs-lookup"><span data-stu-id="99918-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="99918-136">Si el dispositivo tiene la aplicación, pero ha estado desconectado durante largos períodos de tiempo, el PNS no podrá entregar el mensaje al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="99918-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="99918-137">Si el mensaje se entrega al dispositivo, pero el SDK de Mobile Engagement en la aplicación no reconoce su contenido, entonces se elimina ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="99918-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="99918-138">Esto podría ocurrir si la personalización de la notificación en la aplicación genera una excepción que capturamos en el SDK y eliminamos el mensaje.</span><span class="sxs-lookup"><span data-stu-id="99918-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="99918-139">Esto también puede ocurrir si la aplicación en el dispositivo utiliza una versión del SDK de Mobile Engagement que no es capaz de entender la versión más reciente del mensaje de inserción enviado desde la plataforma. Pero esto solo sucede, si la aplicación se ha actualizado después de que la notificación se distribuyera desde la plataforma de servicio.</span><span class="sxs-lookup"><span data-stu-id="99918-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="99918-140">La pestaña **Opciones avanzadas** indicará cuántos mensajes se han eliminado.</span><span class="sxs-lookup"><span data-stu-id="99918-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="99918-141">En dispositivos iOS, los mensajes a veces no se entregan si el dispositivo tiene poca batería o si la aplicación consume demasiada energía al procesar las notificaciones remotas.</span><span class="sxs-lookup"><span data-stu-id="99918-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="99918-142">Se trata de una limitación de los dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="99918-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="99918-143">**Mostrados** : especifica el número de mensajes que se muestran correctamente al usuario de la aplicación en el dispositivo en forma de una notificación push del sistema o de fuera de aplicación en el centro de notificaciones, o en forma de una notificación en aplicación dentro de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="99918-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="99918-144">La pestaña **Avanzadas** le indicará cuántas eran notificaciones del sistema y cuántas notificaciones en aplicación.</span><span class="sxs-lookup"><span data-stu-id="99918-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="99918-145">*Razones para que el recuento mostrado sea menor que el recuento entregado (esperando a que se muestre)*</span><span class="sxs-lookup"><span data-stu-id="99918-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span></span>
   
   1. <span data-ttu-id="99918-146">Si la campaña de notificación tenía una fecha de finalización, es posible que la notificación se entregara, pero en el momento de abrirla y mostrarla al usuario de la aplicación ya había expirado, por lo que nunca se mostró.</span><span class="sxs-lookup"><span data-stu-id="99918-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="99918-147">Si la notificación es una notificación en aplicación, se muestra solo cuando el usuario abre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99918-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="99918-148">Si el usuario no ha abierto la aplicación, el SDK informará de que la notificación se entregó pero no se mostrará hasta que la aplicación se abra.</span><span class="sxs-lookup"><span data-stu-id="99918-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="99918-149">Si la notificación es una notificación en aplicación y está configurada para mostrarse en una pantalla o actividad específica, también se notificará como entregada, pero no se entregará hasta que el usuario abra la aplicación en una pantalla específica.</span><span class="sxs-lookup"><span data-stu-id="99918-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="99918-150">**Interacciones de usuario** : especifica el número de mensajes con los que ha interactuado el usuario de la aplicación e incluye los mensajes que están accionados o cerrados.</span><span class="sxs-lookup"><span data-stu-id="99918-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="99918-151">*El usuario de la aplicación puede accionar una notificación de las siguientes formas:*</span><span class="sxs-lookup"><span data-stu-id="99918-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="99918-152">Si la notificación es una notificación del sistema o de fuera de aplicación o una notificación en aplicación enviada solo como notificación, el usuario de la aplicación hace clic en la notificación.</span><span class="sxs-lookup"><span data-stu-id="99918-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="99918-153">Si la notificación es una notificación en aplicación con una vista de texto o web o sondeos, el usuario de la aplicación hace clic entonces en el botón de acción en la notificación.</span><span class="sxs-lookup"><span data-stu-id="99918-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="99918-154">Si la notificación es una notificación en aplicación con una vista web, el usuario de la aplicación hace clic en una dirección URL en la vista web [solo para Android]</span><span class="sxs-lookup"><span data-stu-id="99918-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="99918-155">*El usuario de la aplicación puede cerrar una notificación de las siguientes formas:*</span><span class="sxs-lookup"><span data-stu-id="99918-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="99918-156">Haciendo clic directamente en el botón Cerrar en la notificación.</span><span class="sxs-lookup"><span data-stu-id="99918-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="99918-157">Con el gesto de deslizarla hacia afuera o eliminándola.</span><span class="sxs-lookup"><span data-stu-id="99918-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="99918-158">Las notificaciones en aplicación con contenido de texto o web y sondeos normalmente se muestran al usuario de la aplicación en un proceso de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="99918-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="99918-159">Primero ven una notificación y, cuando hacen clic en ella, ven el contenido de texto, web o sondeo subsiguiente.</span><span class="sxs-lookup"><span data-stu-id="99918-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="99918-160">El usuario de la aplicación puede cerrar una notificación en cualquiera de estos pasos y los detalles de la vista avanzada capturan esta acción.</span><span class="sxs-lookup"><span data-stu-id="99918-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="99918-161">**Accionados** : especifica el número de mensajes que el usuario de la aplicación accionó explícitamente.</span><span class="sxs-lookup"><span data-stu-id="99918-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="99918-162">Es el número más interesante ya que le indica cuántos usuarios de la aplicación estuvieron interesados en el mensaje que se expulsó en la notificación.</span><span class="sxs-lookup"><span data-stu-id="99918-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="99918-163">En las plataformas iOS y Windows, si el usuario tiene abierta la aplicación y la campaña era de tipo "Cualquier hora", es posible que tanto las notificaciones en aplicación como fuera de aplicación se muestren al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="99918-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="99918-164">Como consecuencia, el número de mensajes mostrados podría ser superior al de los entregados.</span><span class="sxs-lookup"><span data-stu-id="99918-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="99918-165">Si el usuario interactúa con la notificación o la resuelve, incluso el número de interacciones de usuario o de mensajes resueltos podría ser superior al de los entregados.</span><span class="sxs-lookup"><span data-stu-id="99918-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="99918-167">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="99918-167">See also</span></span>
* <span data-ttu-id="99918-168">[Conceptos][Link 6]</span><span class="sxs-lookup"><span data-stu-id="99918-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="99918-169">[Guía de solución de problemas de servicios][Link 24]</span><span class="sxs-lookup"><span data-stu-id="99918-169">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

