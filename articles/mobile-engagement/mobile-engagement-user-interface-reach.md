---
title: Interfaz de usuario de Mobile Engagement - alcance aaaAzure
description: "Obtenga información acerca de cómo tooreach toohello usuarios de la aplicación con las notificaciones de inserción con Azure Mobile Engagement"
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
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="57eb5-103">Cómo tooreach toohello usuarios de la aplicación con las notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="57eb5-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="57eb5-104">Este artículo describe hello **ALCANZAR** ficha de hello **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="57eb5-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="57eb5-105">Usar hello **Mobile Engagement** toomonitor portal y administrar aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="57eb5-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="57eb5-106">Tenga en cuenta que toostart mediante portal Hola primero debe toocreate una **Azure Mobile Engagement** cuenta.</span><span class="sxs-lookup"><span data-stu-id="57eb5-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="57eb5-107">Para obtener más información, consulte [Crear una cuenta de Azure Mobile Engagement](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="57eb5-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="57eb5-108">Hola llegar a sección de hello es la interfaz de usuario de herramienta de administración de campaña Hola inserción siempre que sea posible crear/editar/activar/finalizar/monitor y obtener estadísticas sobre las campañas de notificación de inserción y otras características que también son accesibles a través de API de cobertura de hello (y algunos elementos del programa Hola baja nivel de API de inserción).</span><span class="sxs-lookup"><span data-stu-id="57eb5-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="57eb5-109">Recuerde que si utiliza las API de Hola o hello interfaz de usuario, necesitará toointegrate Azure Mobile Engagement y alcance en la aplicación para cada plataforma con hello SDK para poder utilizar alcanzan las campañas.</span><span class="sxs-lookup"><span data-stu-id="57eb5-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="57eb5-110">Muchas de las secciones de hello **Mobile Engagement** portal de interfaz de usuario contienen hello **ayuda para mostrar** botón.</span><span class="sxs-lookup"><span data-stu-id="57eb5-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="57eb5-111">Presione este botón tooget más información contextual sobre una sección.</span><span class="sxs-lookup"><span data-stu-id="57eb5-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="57eb5-112">Cuatro tipos de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="57eb5-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="57eb5-113">Anuncios - permitir toosend publicidad mensajes toousers que redirigirá tooanother ubicación dentro de su aplicación o toosend su página Web tooa o almacenar fuera de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="57eb5-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="57eb5-114">Sondeos - permitir toogather información a los usuarios finales cuando les pregunta preguntas.</span><span class="sxs-lookup"><span data-stu-id="57eb5-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="57eb5-115">Inserciones de datos - permitir toosend un archivo de datos binarios o de base64.</span><span class="sxs-lookup"><span data-stu-id="57eb5-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="57eb5-116">información de Hello contenida en una inserción de datos es enviado tooyour aplicación toomodify experiencia actual de los usuarios de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="57eb5-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="57eb5-117">La aplicación necesita datos de hello toobe tooprocess pueda en una inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="57eb5-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="57eb5-118">Detalles de la campaña</span><span class="sxs-lookup"><span data-stu-id="57eb5-118">Campaign Details</span></span>
<span data-ttu-id="57eb5-119">Puede editar, clonar, eliminar o activar las campañas que todavía no ha activado todavía desplazando el puntero sobre sus nombres o puede hacer clic en tooopen ellos.</span><span class="sxs-lookup"><span data-stu-id="57eb5-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="57eb5-120">Puede clonar las campañas que ya se han activado desplazando el puntero sobre sus nombres o puede hacer clic en tooopen ellos.</span><span class="sxs-lookup"><span data-stu-id="57eb5-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="57eb5-121">Sin embargo, no puede cambiar una campaña una vez activada.</span><span class="sxs-lookup"><span data-stu-id="57eb5-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="57eb5-123">Comentarios sobre la cobertura</span><span class="sxs-lookup"><span data-stu-id="57eb5-123">Reach Feedback</span></span>
<span data-ttu-id="57eb5-124">Haga clic en **estadísticas** detalles de hello toosee de una campaña de cobertura.</span><span class="sxs-lookup"><span data-stu-id="57eb5-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="57eb5-125">Hola **Simple** vista proporciona una representación visual en forma de Hola de un gráfico de barras de columna sobre lo que sucedieron después de que se activó una campaña.</span><span class="sxs-lookup"><span data-stu-id="57eb5-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="57eb5-126">Hola **avanzadas** vista proporciona detalles más granulares acerca de la campaña de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="57eb5-127">Estos detalles no estará disponibles si va a enviar una campaña de prueba, es decir, un dispositivo de prueba de tooa enviado de inserción.</span><span class="sxs-lookup"><span data-stu-id="57eb5-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="57eb5-128">A continuación le mostramos cómo interpretar estos detalles:</span><span class="sxs-lookup"><span data-stu-id="57eb5-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="57eb5-129">**Insertar** -especifica Hola número de mensajes insertados toohello dispositivos.</span><span class="sxs-lookup"><span data-stu-id="57eb5-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="57eb5-130">Este número dependerá de la audiencia de destino de hello que especifica al crear una campaña de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="57eb5-131">Si no especifica ninguna audiencia de destino, se enviará este inserción out tooall Hola registrado dispositivos.</span><span class="sxs-lookup"><span data-stu-id="57eb5-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="57eb5-132">Al igual que todos los demás servicios de inserción, se no hello las notificaciones de inserción directamente toohello dispositivos pero en su lugar insertarlas toohello respectivos plataforma servicios específicos de notificaciones de inserción (PNS - APN/GCM/WNS) para que pueden entregar notificaciones de hello toohello dispositivos.</span><span class="sxs-lookup"><span data-stu-id="57eb5-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="57eb5-133">**Entregar** -especifica Hola número de mensajes entregados por dispositivo de toohello PNS de Hola y confirmado correctamente como recibido por el SDK de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="57eb5-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="57eb5-134">*Razones de que el número de entregados sea inferior al número de insertados:*</span><span class="sxs-lookup"><span data-stu-id="57eb5-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="57eb5-135">Si usuario de hello ha desinstalado la aplicación hello de dispositivo de hello pero no sabe hello PNS sobre él en tiempo de hello que enviamos Hola inserción toohello PNS se eliminarán los mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="57eb5-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="57eb5-136">Si dispositivo hello tiene aplicación hello pero propios dispositivos Hola estaban sin conexión durante largos períodos de tiempo, a continuación, hello PNS producirá dispositivo toohello de toodeliver Hola mensajes.</span><span class="sxs-lookup"><span data-stu-id="57eb5-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="57eb5-137">Si mensaje Hola se entrega toohello dispositivo pero Hola SDK de Mobile Engagement en la aplicación hello no reconoce el contenido de hello del mensaje de bienvenida, coloca ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="57eb5-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="57eb5-138">Esto podría suceder si personalización Hola de notificación de hello en la aplicación hello genera una excepción que se captura en mensaje de saludo SDK y drop Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="57eb5-139">Esto también puede ocurrir si la aplicación hello en dispositivo Hola está usando una versión de SDK de Mobile Engagement que no es capaz de toounderstand Hola versión posterior de mensaje de inserción de Hola Hola enviados desde la plataforma de Hola pero se trata solo cuando la aplicación hello se actualizó después de la notificación de Hola se distribuyó de plataforma del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="57eb5-140">Hola **avanzadas** ficha indicará cuántos mensajes se han quitado.</span><span class="sxs-lookup"><span data-stu-id="57eb5-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="57eb5-141">En dispositivos iOS, mensajes a veces no se entrega si cualquiera de estos dispositivos Hola de batería baja o si aplicación hello consume gran cantidad de energía al procesar notificaciones remotas.</span><span class="sxs-lookup"><span data-stu-id="57eb5-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="57eb5-142">Se trata de una limitación de los dispositivos de iOS de Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="57eb5-143">**Muestra** -especifica Hola número de mensajes que se correctamente muestran toohello usuario de aplicación en dispositivos de hello en forma de Hola de una notificación de inserción/out-de-app del sistema en el centro de notificaciones de Hola o una notificación en la aplicación dentro de hello móviles aplicación.</span><span class="sxs-lookup"><span data-stu-id="57eb5-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="57eb5-144">Hola **avanzadas** ficha le indicará cuántos estaban notificaciones del sistema y cuántas notificaciones en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="57eb5-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="57eb5-145">*Razones para mostradas recuento es menor que el recuento de entregado (toobe de espera muestra)*</span><span class="sxs-lookup"><span data-stu-id="57eb5-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="57eb5-146">Si campaña de notificación de hello tenía una fecha de finalización en el es posible que se entregó notificación Hola pero al tiempo de hello suministrada tooopen y mostrar toohello usuario de aplicación, ya había expirado para que nunca se visualizó.</span><span class="sxs-lookup"><span data-stu-id="57eb5-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="57eb5-147">Si la notificación de hello es una notificación en la aplicación, a continuación, notificación de hello solo se muestra al usuario de aplicación Hola abre la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="57eb5-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="57eb5-148">En casos donde usuario de aplicación hello no ha abierto la aplicación hello, Hola SDK notificará que notificación Hola se entrega pero aún no aparece hasta que se abra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="57eb5-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="57eb5-149">Si la notificación de hello es una notificación en la aplicación y configura toobe que se muestra en una pantalla/actividad específica, a continuación, también se notificará notificación Hola tal como se entrega pero todavía no se han entregado hasta que el usuario de hello abre la aplicación hello en una pantalla específica.</span><span class="sxs-lookup"><span data-stu-id="57eb5-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="57eb5-150">**Las interacciones del usuario** -especifica Hola número de mensajes que usuario de la aplicación hello ha interactuado con e incluirá los mensajes de Hola que son accionado o cerrado.</span><span class="sxs-lookup"><span data-stu-id="57eb5-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="57eb5-151">*usuario de aplicación Hola puede accionar una notificación en la vista de hello siguientes maneras:*</span><span class="sxs-lookup"><span data-stu-id="57eb5-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="57eb5-152">Si hello notificación es una notificación de sistema/out-de-app o envía una notificación de aplicación como de solo notificación, a continuación, haga clic en usuario de aplicación hello en la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="57eb5-153">Si la notificación de hello es una notificación en la aplicación con un texto o una vista web o sondeos Hola, a continuación, el usuario de la aplicación hace clic en hello botón de acción de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="57eb5-154">Si la notificación de hello es una notificación en la aplicación, a continuación, con una vista web Hola aplicación clics del usuario en una dirección URL en hello web solo en la vista [Android]</span><span class="sxs-lookup"><span data-stu-id="57eb5-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="57eb5-155">*usuario de aplicación Hola puede cerrar una notificación en la vista de hello siguientes maneras:*</span><span class="sxs-lookup"><span data-stu-id="57eb5-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="57eb5-156">Haga clic en botón de cierre de hello en la notificación de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="57eb5-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="57eb5-157">Eliminar notificación Hola o Deslizar rápidamente inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="57eb5-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="57eb5-158">Las notificaciones de aplicación con sondeos y contenido web y de texto son normalmente muestran toohello usuario de aplicación en un proceso de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="57eb5-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="57eb5-159">Verán una notificación en primer lugar y cuando haga clic en él, podrán ver contenido de texto/web/sondeo subsiguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="57eb5-160">usuario de aplicación Hola puede salir de una notificación en cualquiera de estos pasos y captura los detalles de hello en vista avanzada de hello esto.</span><span class="sxs-lookup"><span data-stu-id="57eb5-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="57eb5-161">**Accionado** -especifica Hola número de mensajes que hayan sido accionados explícitamente por el usuario de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="57eb5-162">Éste es el número de más interesante de hello como esto indica cuántos usuarios de aplicación se está interesados mensaje Hola que sobresale en la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="57eb5-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="57eb5-163">En iOS y plataformas de Windows, si usuario hello tiene aplicación Hola abierta y campaña Hola era una campaña "En cualquier momento" es posible que ambos fuera de la aplicación y en la aplicación de notificaciones se muestran en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="57eb5-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="57eb5-164">Esto puede provocar un recuento de mostradas superior Hola entregado.</span><span class="sxs-lookup"><span data-stu-id="57eb5-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="57eb5-165">Si Hola usuario interactúa o notificación de Hola de acciones, hello, a continuación, incluso el recuento de las interacciones de usuario/Actioned podría ser mayor que entregado.</span><span class="sxs-lookup"><span data-stu-id="57eb5-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="57eb5-167">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="57eb5-167">See also</span></span>
* <span data-ttu-id="57eb5-168">[Conceptos][Link 6]</span><span class="sxs-lookup"><span data-stu-id="57eb5-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="57eb5-169">[Guía de solución de problemas de servicios][Link 24]</span><span class="sxs-lookup"><span data-stu-id="57eb5-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

