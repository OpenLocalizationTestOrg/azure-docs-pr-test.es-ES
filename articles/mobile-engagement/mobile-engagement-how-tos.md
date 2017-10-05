---
title: "Interfaz de usuario de Azure Mobile Engagement - Guía práctica de Cobertura"
description: "Introducción de la interfaz de usuario de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 33a0a9d0c399cb7f0a791c4c16dde2e2d62364ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-using-and-managing-pushes-to-reach-out-to-your-end-users"></a><span data-ttu-id="17f21-103">Cómo empezar a usar y administrar inserciones para llegar a los usuarios finales</span><span class="sxs-lookup"><span data-stu-id="17f21-103">How to get started using and managing pushes to reach out to your end users</span></span>
<span data-ttu-id="17f21-104">Una vez que el SDK está totalmente integrado en la aplicación, puede empezar a usar la sección Cobertura de la interfaz de usuario para enviar notificaciones a los usuarios de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17f21-104">Once the SDK is fully integrated into your app, you can get started using the the Reach section of the UI to Push notifications to the users of your app.</span></span>  

## <a name="do-your-first-push-notification-campaign"></a><span data-ttu-id="17f21-105">Creación de la primera campaña de notificación de inserción</span><span class="sxs-lookup"><span data-stu-id="17f21-105">Do Your First Push Notification Campaign</span></span>
* <span data-ttu-id="17f21-106">Confirme que tiene integrado Reach en la aplicación con el SDK.</span><span class="sxs-lookup"><span data-stu-id="17f21-106">Confirm that your Reach is integrated into your app with the SDK.</span></span> 
* <span data-ttu-id="17f21-107">Seleccione la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17f21-107">Select your application</span></span>

![First1][1]

* <span data-ttu-id="17f21-109">Vaya a la sección "Reach" y haga clic en "Nuevo anuncio".</span><span class="sxs-lookup"><span data-stu-id="17f21-109">Go to the "Reach" Section and Click "New announcement"</span></span>

![First2][2]

* <span data-ttu-id="17f21-111">Cree una campaña nueva y asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="17f21-111">Create a new campaign and name it</span></span>
  
![First3][3]

* <span data-ttu-id="17f21-113">Seleccione cómo se debe entregar la notificación, por ejemplo, si es solo en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17f21-113">Select how the notification should be delivered, as In-app only</span></span>

![First4][4]

* <span data-ttu-id="17f21-115">Cree el mensaje que desea insertar.</span><span class="sxs-lookup"><span data-stu-id="17f21-115">Create the message you want to push</span></span>

![First5][5]

* <span data-ttu-id="17f21-117">Puede escribir un título en la notificación (opcional).</span><span class="sxs-lookup"><span data-stu-id="17f21-117">You may write a title on the notification (Optional).</span></span>
* <span data-ttu-id="17f21-118">Escriba el contenido del mensaje de inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-118">Write push message content.</span></span>
* <span data-ttu-id="17f21-119">Puede cargar una imagen.</span><span class="sxs-lookup"><span data-stu-id="17f21-119">You can upload an image.</span></span> <span data-ttu-id="17f21-120">Tenga en cuenta que el tamaño del archivo no puede superar 32.768 bytes.</span><span class="sxs-lookup"><span data-stu-id="17f21-120">Be aware that the size of the file cannot exceed 32,768 bytes.</span></span>
* <span data-ttu-id="17f21-121">También tiene la posibilidad de seleccionar más opciones, pero para el objetivo de este tutorial, las veremos más adelante.</span><span class="sxs-lookup"><span data-stu-id="17f21-121">You also have the ability to select further options, but for the focus of this tutorial, we will see that later.</span></span>
* <span data-ttu-id="17f21-122">Seleccionar tipo de contenido como Solo notificación</span><span class="sxs-lookup"><span data-stu-id="17f21-122">Select the content type as Notification only</span></span>

![First6][6]

* <span data-ttu-id="17f21-124">Cree la campaña de inserción, que aparecerá en la lista de campañas.</span><span class="sxs-lookup"><span data-stu-id="17f21-124">Create your push campaign and it will appear in your campaign list.</span></span>

![First7][7]

## <a name="test-your-push-notification-campaign"></a><span data-ttu-id="17f21-126">Prueba de la campaña de notificación de inserción</span><span class="sxs-lookup"><span data-stu-id="17f21-126">Test Your Push Notification Campaign</span></span>
![Test1][8]

* <span data-ttu-id="17f21-128">Registre el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="17f21-128">Register your device.</span></span>
* <span data-ttu-id="17f21-129">Haga clic en la casilla del dispositivo donde desea realizar la inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-129">Click on the checkbox of the device you want to push.</span></span>
* <span data-ttu-id="17f21-130">Haga clic en el botón "Probar" para enviar la inserción al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="17f21-130">Click on the "Test" button to send the push to the device.</span></span>

![Test2][9]

* <span data-ttu-id="17f21-132">Activar la campaña</span><span class="sxs-lookup"><span data-stu-id="17f21-132">Activate the campaign</span></span>

![Test3][10]

* <span data-ttu-id="17f21-134">Ahora que ha creado la campaña, basta con activarla para insertar la notificación para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="17f21-134">Now that you have created your campaign you just need to activate it for the notification to be pushed to your users.</span></span>

## <a name="send-personalized-pushes"></a><span data-ttu-id="17f21-135">Envío de inserciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="17f21-135">Send Personalized Pushes</span></span>
* <span data-ttu-id="17f21-136">En este ejemplo se crea una inserción donde se introduce un código de descuento personalizado en la notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-136">This example creates a push where a custom rebate code is entered into the push notification.</span></span>

![Personalize1][11]

<span data-ttu-id="17f21-138">La personalización funciona mediante la sustitución del marcador de una etiqueta de información de la aplicación, por lo que antes tendrá que asegúrese de que el usuario tiene definida la información de la aplicación adecuada.</span><span class="sxs-lookup"><span data-stu-id="17f21-138">Personalization works by replacing a marker by from an app info tag so, you'll have to make sure the user has the proper app-info defined first.</span></span> <span data-ttu-id="17f21-139">En este ejemplo, los usuarios de destino tienen una etiqueta definida de información de la aplicación que se denomina rebate_code.</span><span class="sxs-lookup"><span data-stu-id="17f21-139">In this example the targeted users will have an app info tag named rebate_code defined.</span></span>
<span data-ttu-id="17f21-140">Como puede ver, el contenido de la notificación de inserción incluye el marcador ${rebate_code}, que indica que se tiene que reemplazar por el contenido real de la etiqueta de información de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17f21-140">As you see above the push notification content includes the marker ${rebate_code} which will indicate that it is to be replaced by the actual content of the app info tag.</span></span>

> [!WARNING]
> <span data-ttu-id="17f21-141">Si el usuario no define la etiqueta de información de la aplicación, no recibirá la inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-141">If the app info tag is not defined for the user, the user will not receive the push.</span></span>

* <span data-ttu-id="17f21-142">Resultado</span><span class="sxs-lookup"><span data-stu-id="17f21-142">Result</span></span>

![Personalize2][12]

### <a name="you-can-further-personalize-the-text-your-notification"></a><span data-ttu-id="17f21-144">Puede personalizar aún más el texto de la notificación,</span><span class="sxs-lookup"><span data-stu-id="17f21-144">You can further personalize the text your notification</span></span>
![Personalize3][13]

* <span data-ttu-id="17f21-146">incluido el título dela notificación</span><span class="sxs-lookup"><span data-stu-id="17f21-146">Including the title of the notification,</span></span>
* <span data-ttu-id="17f21-147">y el contenido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="17f21-147">And the content of the message.</span></span>
* <span data-ttu-id="17f21-148">Elija el tipo de anuncio (vista de texto o vista web).</span><span class="sxs-lookup"><span data-stu-id="17f21-148">Choose the type of announcement (Text view or Web view)</span></span>

![Personalize4][14]

### <a name="the-body-of-an-announcement-may-also-be-personalized-with"></a><span data-ttu-id="17f21-150">También se puede personalizar el cuerpo de un anuncio con:</span><span class="sxs-lookup"><span data-stu-id="17f21-150">The body of an announcement may also be personalized with:</span></span>
* <span data-ttu-id="17f21-151">la URL de acción, en caso de que quiera personalizar la página de inicio;</span><span class="sxs-lookup"><span data-stu-id="17f21-151">The action URL, should you want to customize the landing page</span></span>
* <span data-ttu-id="17f21-152">el título y</span><span class="sxs-lookup"><span data-stu-id="17f21-152">The title,</span></span>
* <span data-ttu-id="17f21-153">el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="17f21-153">The body of the message.</span></span>

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a><span data-ttu-id="17f21-154">Diferenciación de la notificación de inserción (en la aplicación o fuera de ella)</span><span class="sxs-lookup"><span data-stu-id="17f21-154">Differentiate Your Push Notification (in or out of app)</span></span>
* <span data-ttu-id="17f21-155">Elija el tipo de notificación que insertará, seleccione la aplicación, vaya a la sección "Reach", seleccione o cree una campaña de inserción y vaya a la sección "Notificación".</span><span class="sxs-lookup"><span data-stu-id="17f21-155">Choose the type of notification you will push, select your application, go to the "Reach" section, select or create a push campaign and go to the "Notification" section.</span></span>
* <span data-ttu-id="17f21-156">Haga clic en el "modo de entrega" que desee.</span><span class="sxs-lookup"><span data-stu-id="17f21-156">Click on the "delivery mode" you want.</span></span>
* <span data-ttu-id="17f21-157">Haga clic en la casilla "Restringir actividades" cuando quiera que la notificación se produzca en actividades concretas (pantallas).</span><span class="sxs-lookup"><span data-stu-id="17f21-157">Click on the "Restrict Activities" checkbox when you want the notification occurs on specific activities (screens).</span></span>

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a><span data-ttu-id="17f21-159">Modo de entrega "Solo fuera de la aplicación"</span><span class="sxs-lookup"><span data-stu-id="17f21-159">"Out of App Only" delivery mode</span></span>
![Differentiate2][16]

<span data-ttu-id="17f21-161">El modo de entrega "Solo fuera de la aplicación sólo" proporciona una notificación de inserción cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17f21-161">"Out of App Only" delivery mode provides push notification when the application is closed.</span></span> <span data-ttu-id="17f21-162">Se trata de la notificación de inserción estándar.</span><span class="sxs-lookup"><span data-stu-id="17f21-162">This is the standard push notification.</span></span>
<span data-ttu-id="17f21-163">Al seleccionar "Solo fuera de la aplicación", debe haber proporcionado antes los certificados de la plataforma en la que se basa la aplicación (APN o GCM).</span><span class="sxs-lookup"><span data-stu-id="17f21-163">When you select "out of app only" ,you must have already provided the certificates from the platform that your application is building on (APNS or GCM).</span></span>

### <a name="see-also"></a><span data-ttu-id="17f21-164">Consulte también</span><span class="sxs-lookup"><span data-stu-id="17f21-164">See also</span></span>
* <span data-ttu-id="17f21-165">[Apple Push Notification Service: certificados](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging: certificado](http://developer.android.com/google/gcm/index.html)</span><span class="sxs-lookup"><span data-stu-id="17f21-165">[Apple Push Notification Service – Certificates](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificate](http://developer.android.com/google/gcm/index.html)</span></span> 

### <a name="in-app-only-delivery-mode"></a><span data-ttu-id="17f21-166">Modo de entrega "Solo en la aplicación"</span><span class="sxs-lookup"><span data-stu-id="17f21-166">"in-App Only" delivery mode</span></span>
![Differentiate3][17]

<span data-ttu-id="17f21-168">El modo de entrega "Solo en la aplicación" proporciona notificaciones de inserción cuando la aplicación se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="17f21-168">"In-App Only" delivery mode provides push notification when the application is running.</span></span>
<span data-ttu-id="17f21-169">En el caso de esta notificación, es necesario pasar por el sistema de APNS y GCM.</span><span class="sxs-lookup"><span data-stu-id="17f21-169">For this notification, you do not need to go through the APNS and GCM system.</span></span>
<span data-ttu-id="17f21-170">Puede usar el sistema de entrega en la aplicación para llegar a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="17f21-170">You can use the in-app delivery system to reach your end-users.</span></span>
<span data-ttu-id="17f21-171">Puede personalizar totalmente la notificación y decidir en que actividad (pantalla) aparecerá la notificación.</span><span class="sxs-lookup"><span data-stu-id="17f21-171">You can fully customize the notification and decide in which activity (screen) the notification will appear.</span></span>

### <a name="anytime-delivery-mode"></a><span data-ttu-id="17f21-172">Modo de entrega "En cualquier momento"</span><span class="sxs-lookup"><span data-stu-id="17f21-172">"Anytime" delivery mode</span></span>
<span data-ttu-id="17f21-173">Si elige el modo de entrega "En cualquier momento", se asegurará de llegar a los usuarios finales tanto si la aplicación se está ejecutando como si no.</span><span class="sxs-lookup"><span data-stu-id="17f21-173">You can choose an "Anytime" delivery mode, ensures you to reach your end-user whether the application is running or not.</span></span>
<span data-ttu-id="17f21-174">Al seleccionar "En cualquier momento", deben haber proporcionado antes los certificados de la plataforma en la que se basa la aplicación (APN o GCM).</span><span class="sxs-lookup"><span data-stu-id="17f21-174">When you select "Anytime" , you must have already provided the certificates from the platform that your application is building upon (APNS or GCM).</span></span> 

## <a name="schedule-a-push-campaign"></a><span data-ttu-id="17f21-175">Programación una campaña de inserción</span><span class="sxs-lookup"><span data-stu-id="17f21-175">Schedule a Push Campaign</span></span>
### <a name="plan-to-start-a-campaign"></a><span data-ttu-id="17f21-176">Planeación del inicio de una campaña</span><span class="sxs-lookup"><span data-stu-id="17f21-176">Plan to Start a campaign</span></span>
![Shedule1][18]

<span data-ttu-id="17f21-178">Es 21 de marzo y tiene un anuncio que hacer, planeado para el 22 de marzo a medianoche.</span><span class="sxs-lookup"><span data-stu-id="17f21-178">It is the 21st of March and you have an announcement to make and planed for the 22nd of March at midnight.</span></span> <span data-ttu-id="17f21-179">No es necesario que esté delante de la interfaz para realizar una inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-179">You don’t have to stay in front of the interface to do a push!</span></span> <span data-ttu-id="17f21-180">Puede planear de antemano el minuto exacto en que se enviarán las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="17f21-180">You can plan in advance the exact minute notifications will be sent.</span></span>

* <span data-ttu-id="17f21-181">Desactive la casilla "Ninguna" y seleccione una hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="17f21-181">Un-check the "None" checkbox and select a start time</span></span> 
* <span data-ttu-id="17f21-182">Elija la fecha y la hora en que desea iniciar la campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-182">Choose the date and the time you want to start the push campaign.</span></span>

### <a name="plan-to-end-a-campaign"></a><span data-ttu-id="17f21-183">Planeación del fin de una campaña</span><span class="sxs-lookup"><span data-stu-id="17f21-183">Plan to end a campaign</span></span>
![Shedule2][19]

<span data-ttu-id="17f21-185">Desea que la campaña finalice el 25 de marzo a las 15:00 h pero sabe que no estará presente para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="17f21-185">You want your campaign to stop on the 25th of March at 3.00 pm but you know you won't be there to do it.</span></span>
<span data-ttu-id="17f21-186">No es necesario que esté delante de la interfaz para realizar la inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-186">You don’t have to stay in front of the interface to push!</span></span> <span data-ttu-id="17f21-187">Puede planear de antemano el minuto exacto en que se detendrá la campaña.</span><span class="sxs-lookup"><span data-stu-id="17f21-187">You can plan in advance the exact minute your campaign will stop.</span></span>

* <span data-ttu-id="17f21-188">Haga clic en la casilla "Ninguna" o seleccione una hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="17f21-188">Click on the "None" checkbox or select a end time</span></span>
* <span data-ttu-id="17f21-189">Elija la fecha y la hora en que desea finalizar la campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-189">Choose the date and the time you want to finish the push campaign.</span></span>

### <a name="end-a-campaign-manually"></a><span data-ttu-id="17f21-190">Finalización de una campaña manualmente</span><span class="sxs-lookup"><span data-stu-id="17f21-190">End a campaign manually</span></span>
![Shedule3][20]

<span data-ttu-id="17f21-192">De forma predeterminada, las casillas "Ninguna" están seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="17f21-192">By default, the "None" check-boxes are selected.</span></span>
<span data-ttu-id="17f21-193">Esto significa que la campaña comenzará en cuanto la active en la sección "Reach" y finalizará cuando la detenga en dicha sección.</span><span class="sxs-lookup"><span data-stu-id="17f21-193">This means that the campaign will start as soon as you activate it in the reach section and will end when you will stop it on the reach section.</span></span>

> [!NOTE]
> <span data-ttu-id="17f21-194">Las campañas creadas sin una fecha de finalización almacenan la inserción de forma local en el dispositivo y la muestran la próxima vez que se abre la aplicación incluso si la campaña ha finalizado manualmente.</span><span class="sxs-lookup"><span data-stu-id="17f21-194">Campaigns created without an end date store the push locally on the device and show it the next time the app is opened even if the campaign is manually ended.</span></span>

## <a name="enhance-a-push-notification-with-a-text-view"></a><span data-ttu-id="17f21-195">Mejora de una notificación de inserción con una vista de texto</span><span class="sxs-lookup"><span data-stu-id="17f21-195">Enhance a Push Notification with a Text View</span></span>
### <a name="what-is-a-text-view"></a><span data-ttu-id="17f21-196">¿Qué es una vista de texto?</span><span class="sxs-lookup"><span data-stu-id="17f21-196">What is a Text View?</span></span>
![TextView1][21]

<span data-ttu-id="17f21-198">Una vista de texto es un elemento emergente con contenido de texto.</span><span class="sxs-lookup"><span data-stu-id="17f21-198">A text view is a pop-up with text content.</span></span> <span data-ttu-id="17f21-199">Este elemento emergente aparece cuando el usuario final hace clic en la notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-199">This pop-up appears after the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="17f21-200">Una vista de texto permite presentar más contenido al usuario final.</span><span class="sxs-lookup"><span data-stu-id="17f21-200">A text view allows you to present more content to your end-user.</span></span> <span data-ttu-id="17f21-201">Esto también es una oportunidad de presentar una llamada a la acción, como saltar a una página de la aplicación, redirigir a una Tienda, abrir una página web, enviar un correo electrónico, iniciar una búsqueda localizada geográficamente, etc.</span><span class="sxs-lookup"><span data-stu-id="17f21-201">This is also the opportunity to present a call to action such as jumping to a page of your app, redirecting to a Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-text-view"></a><span data-ttu-id="17f21-202">Ejemplo: vista de texto</span><span class="sxs-lookup"><span data-stu-id="17f21-202">Example: Text View</span></span>
* <span data-ttu-id="17f21-203">Cree la campaña de notificación de inserción en la sección "Reach" y asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="17f21-203">Create your Push notification campaign in the "Reach" section and give your campaign a name</span></span>

![TextView2][22]

* <span data-ttu-id="17f21-205">Escriba el mensaje que aparecerá en la notificación.</span><span class="sxs-lookup"><span data-stu-id="17f21-205">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="17f21-206">Seleccione el tipo de contenido del anuncio de "texto".</span><span class="sxs-lookup"><span data-stu-id="17f21-206">Select the Announcement Content Type of “text”</span></span>

![TextView3][23]

> [!NOTE]
> <span data-ttu-id="17f21-208">Cuando inserta una vista de texto, siempre va acompañada de una notificación en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="17f21-208">When you push a text view, it always comes with a notification first.</span></span> 

* <span data-ttu-id="17f21-209">Defina el texto (después de seleccionar el contenido del anuncio de texto, aparecerá la subsección, que le permite definir el texto que desea que se muestre).</span><span class="sxs-lookup"><span data-stu-id="17f21-209">Define the text (After having selected the text announcement content, the sub-section will appear, allowing you to define the text you want to be displayed.)</span></span>

![TextView4][24]

* <span data-ttu-id="17f21-211">Escriba el título que aparecerá en la parte superior del mensaje.</span><span class="sxs-lookup"><span data-stu-id="17f21-211">Write the title that will appear at the top of the message.</span></span>
* <span data-ttu-id="17f21-212">Escriba el contenido principal de la vista de texto.</span><span class="sxs-lookup"><span data-stu-id="17f21-212">Write the main content of the text view.</span></span>
* <span data-ttu-id="17f21-213">Escriba el contenido que aparecerá en el botón de acción (un botón de acción permite a la aplicación realizar una acción concreta, como abrir una página de la aplicación, redirigir a una tienda de aplicaciones o cualquier tipo de orígenes que proporcione).</span><span class="sxs-lookup"><span data-stu-id="17f21-213">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to an App store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="17f21-214">Escriba el contenido que aparecerá en el botón Salir (haciendo clic en el botón Salir, la vista de texto desaparecerá).</span><span class="sxs-lookup"><span data-stu-id="17f21-214">Write the content that will appear on the exit button (by clicking on the exit button, the text view will disappear.)</span></span>
* <span data-ttu-id="17f21-215">Cree la campaña de notificación de inserción, que aparecerá en la lista de campañas.</span><span class="sxs-lookup"><span data-stu-id="17f21-215">Create your push notification campaign and it will appear on the campaign list.</span></span>

![TextView5][25]

* <span data-ttu-id="17f21-217">Active la campaña de notificación de inserción para enviar la vista de texto a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="17f21-217">Activate your push notification campaign to send the text view to your users.</span></span>

![TextView6][26]

* <span data-ttu-id="17f21-219">Resultado</span><span class="sxs-lookup"><span data-stu-id="17f21-219">Result</span></span>

![TextView7][27]

* <span data-ttu-id="17f21-221">El usuario recibe la notificación y hace clic en ella.</span><span class="sxs-lookup"><span data-stu-id="17f21-221">The user receives the notification and click on it.</span></span>
* <span data-ttu-id="17f21-222">La vista de texto aparece como un elemento emergente que permite al usuario interactuar con él.</span><span class="sxs-lookup"><span data-stu-id="17f21-222">The text view appears as a pop-up allowing the user to interact with it.</span></span>

## <a name="enhance-a-push-notification-with-a-web-view"></a><span data-ttu-id="17f21-223">Mejora de una notificación de inserción con una vista web</span><span class="sxs-lookup"><span data-stu-id="17f21-223">Enhance a Push Notification with a Web View</span></span>
### <a name="what-is-a-web-view"></a><span data-ttu-id="17f21-224">¿Qué es una vista web?</span><span class="sxs-lookup"><span data-stu-id="17f21-224">What is a Web View?</span></span>
![WebView1][28]

<span data-ttu-id="17f21-226">Una vista web es un elemento emergente con contenido web.</span><span class="sxs-lookup"><span data-stu-id="17f21-226">A web view is a pop-up with web content.</span></span> <span data-ttu-id="17f21-227">Este elemento emergente aparece cuando el usuario final hace clic en la notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="17f21-227">This pop-up appears when the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="17f21-228">Una vista web le permite interactuar más con el usuario final.</span><span class="sxs-lookup"><span data-stu-id="17f21-228">A web view allows you to have more interaction with the end-user.</span></span>
<span data-ttu-id="17f21-229">Esto también es una oportunidad de presentar una llamada a la acción, como redirigir a una tienda de aplicaciones, abrir una página web, enviar un correo electrónico, iniciar una búsqueda localizada geográficamente, etc.</span><span class="sxs-lookup"><span data-stu-id="17f21-229">This is also the opportunity to present a call to action such as redirection to App Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-web-view"></a><span data-ttu-id="17f21-230">Ejemplo: vista web</span><span class="sxs-lookup"><span data-stu-id="17f21-230">Example: Web View</span></span>
* <span data-ttu-id="17f21-231">Cree la campaña de inserción en la sección "Reach" y asígnele un nombre.</span><span class="sxs-lookup"><span data-stu-id="17f21-231">Create your Push campaign in the "Reach" section and give your campaign a name.</span></span>

![WebView2][29]

* <span data-ttu-id="17f21-233">Escriba el mensaje que aparecerá en la notificación.</span><span class="sxs-lookup"><span data-stu-id="17f21-233">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="17f21-234">Seleccione el tipo de contenido del anuncio como "web".</span><span class="sxs-lookup"><span data-stu-id="17f21-234">Select the Announcement Content Type as “web”</span></span>

![WebView3][30]

### <a name="about-announcement-types"></a><span data-ttu-id="17f21-236">Acerca de los tipos de anuncio:</span><span class="sxs-lookup"><span data-stu-id="17f21-236">About Announcement types:</span></span>
* <span data-ttu-id="17f21-237">Solo notificación: es una notificación estándar simple.</span><span class="sxs-lookup"><span data-stu-id="17f21-237">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="17f21-238">Lo que significa que si un usuario hace clic en él, no aparecerá ninguna vista adicional, pero se producirá solo la acción asociada a él.</span><span class="sxs-lookup"><span data-stu-id="17f21-238">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="17f21-239">Anuncio de texto: es una notificación que compromete al usuario a echar un vistazo a una vista de texto.</span><span class="sxs-lookup"><span data-stu-id="17f21-239">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="17f21-240">Anuncio web: es una notificación que compromete al usuario a echar un vistazo a una vista de texto.</span><span class="sxs-lookup"><span data-stu-id="17f21-240">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>
  <span data-ttu-id="17f21-241">Seleccione el contenido de "Anuncio web".</span><span class="sxs-lookup"><span data-stu-id="17f21-241">Select the "Web announcement" content.</span></span>

> [!NOTE]
> <span data-ttu-id="17f21-242">cuando inserta una vista de web, siempre va acompañada de una notificación en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="17f21-242">When you push a web view, it always comes with a notification first.</span></span>

* <span data-ttu-id="17f21-243">Defina el contenido web (después de seleccionar el contenido del anuncio de web, aparecerá la subsección, que le permite definir el contenido de la vista web que desea que se muestre).</span><span class="sxs-lookup"><span data-stu-id="17f21-243">Define the web content (After having selected the web announcement content, the subsection will appear, allowing you to define the web view content you want to be displayed.)</span></span>

![WebView4][31]

* <span data-ttu-id="17f21-245">Escribir el título que aparecerá en la parte superior del mensaje (opcional).</span><span class="sxs-lookup"><span data-stu-id="17f21-245">Write the title that will appear at the top of the message (optional).</span></span>
* <span data-ttu-id="17f21-246">Escriba el código HTML aquí.</span><span class="sxs-lookup"><span data-stu-id="17f21-246">Write your HTML code here.</span></span>
* <span data-ttu-id="17f21-247">Haga clic en el botón de modo de edición de origen para cambiar la edición y ver su aspecto.</span><span class="sxs-lookup"><span data-stu-id="17f21-247">Click on the source editing mode button to switch edition and see how it looks like.</span></span>
* <span data-ttu-id="17f21-248">Escriba el contenido que aparecerá en el botón de acción (un botón de acción permite a la aplicación realizar una acción concreta, como abrir una página de la aplicación, redirigir a una tienda o cualquier tipo de orígenes que proporcione).</span><span class="sxs-lookup"><span data-stu-id="17f21-248">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to a Store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="17f21-249">Escriba el contenido que aparecerá en el botón Salir (haciendo clic en el botón Salir, la vista de web desaparecerá).</span><span class="sxs-lookup"><span data-stu-id="17f21-249">Write the content that will appear on the exit button (by clicking on the exit button, the web view will disappear).</span></span>
* <span data-ttu-id="17f21-250">Resultado</span><span class="sxs-lookup"><span data-stu-id="17f21-250">Result</span></span>

![WebView5][32]

* <span data-ttu-id="17f21-252">El usuario recibe la notificación y hace clic en ella.</span><span class="sxs-lookup"><span data-stu-id="17f21-252">The user receive the notification and click on it.</span></span>
* <span data-ttu-id="17f21-253">La vista de texto aparece como un elemento emergente que permite al usuario interactuar con él.</span><span class="sxs-lookup"><span data-stu-id="17f21-253">The text view appears as a pop-up allowing the user to interact with it.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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

