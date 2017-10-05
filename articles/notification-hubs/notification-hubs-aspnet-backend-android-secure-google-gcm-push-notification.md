---
title: "Envío de notificaciones push seguras a los Centros de notificaciones de Azure"
description: "Obtenga información acerca de cómo enviar notificaciones de inserción seguras en una aplicación Android desde Azure. Ejemplos de código escritos en Java y C#."
documentationcenter: android
keywords: push notification,push notifications,push messages,android push notifications
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 29f8c516e611c13fb73c7edc15e7c52708c75bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="d92bb-105">Envío de notificaciones push seguras a los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d92bb-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d92bb-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="d92bb-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="d92bb-107">iOS</span><span class="sxs-lookup"><span data-stu-id="d92bb-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="d92bb-108">Android</span><span class="sxs-lookup"><span data-stu-id="d92bb-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d92bb-109">Información general</span><span class="sxs-lookup"><span data-stu-id="d92bb-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d92bb-110">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d92bb-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d92bb-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d92bb-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d92bb-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="d92bb-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="d92bb-113">La compatibilidad con las notificaciones push en Microsoft Azure le permite tener acceso a una infraestructura de mensajes multiplataforma y de escalamiento horizontal fácil de usar, que simplifica considerablemente la implementación de notificaciones push tanto en aplicaciones de consumidor como en aplicaciones empresariales para plataformas móviles.</span><span class="sxs-lookup"><span data-stu-id="d92bb-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="d92bb-114">Debido a restricciones reguladoras o de seguridad, algunas veces una aplicación podría querer incluir algo en la notificación que no se puede trasmitir a través de la infraestructura de las notificaciones de inserción estándar.</span><span class="sxs-lookup"><span data-stu-id="d92bb-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="d92bb-115">En este tutorial se describe cómo lograr la misma experiencia enviando información importante a través de una conexión segura y autenticada entre el dispositivo Android y el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d92bb-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span></span>

<span data-ttu-id="d92bb-116">A un alto nivel, el flujo es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="d92bb-116">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="d92bb-117">El back-end de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d92bb-117">The app back-end:</span></span>
   * <span data-ttu-id="d92bb-118">Almacena la carga segura en la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="d92bb-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="d92bb-119">Envía el identificador de esta notificación al dispositivo Android (no se envía información segura).</span><span class="sxs-lookup"><span data-stu-id="d92bb-119">Sends the ID of this notification to the Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="d92bb-120">La aplicación del dispositivo, cuando recibe la información:</span><span class="sxs-lookup"><span data-stu-id="d92bb-120">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="d92bb-121">El dispositivo Android entra en contacto con el back-end que solicita la carga segura.</span><span class="sxs-lookup"><span data-stu-id="d92bb-121">The Android device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="d92bb-122">La aplicación puede mostrar la carga como una notificación en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d92bb-122">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="d92bb-123">Es importante tener en cuenta que en el flujo anterior (y en este tutorial), asumimos que el dispositivo almacena un token de autenticación localmente y, después, el usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="d92bb-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="d92bb-124">Esto garantiza una experiencia sin ningún problema, ya que el dispositivo puede recuperar la carga segura de la notificación usando este token.</span><span class="sxs-lookup"><span data-stu-id="d92bb-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="d92bb-125">Si la aplicación no almacena tokens de autenticación en el dispositivo, o si estos tokens pueden haber caducado, la aplicación del dispositivo, al recibir la notificación push, debe mostrar una notificación genérica pidiendo al usuario que inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d92bb-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="d92bb-126">Después, la aplicación autentica al usuario y muestra la carga de la notificación.</span><span class="sxs-lookup"><span data-stu-id="d92bb-126">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="d92bb-127">Este tutorial muestra cómo enviar notificaciones push seguras.</span><span class="sxs-lookup"><span data-stu-id="d92bb-127">This tutorial shows how to send secure push notifications.</span></span> <span data-ttu-id="d92bb-128">Se basa en el tutorial sobre [notificar a los usuarios](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) , por lo que debe completar los pasos de ese tutorial primero si no lo ha hecho todavía.</span><span class="sxs-lookup"><span data-stu-id="d92bb-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="d92bb-129">En este tutorial se supone que se ha creado y configurado el Centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d92bb-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a><span data-ttu-id="d92bb-130">Modificación del proyecto Android</span><span class="sxs-lookup"><span data-stu-id="d92bb-130">Modify the Android project</span></span>
<span data-ttu-id="d92bb-131">Una vez modificado el back-end de la aplicación para enviar solamente el *identificador* de una notificación push, deberá modificar la aplicación Android para que administre dicha notificación y devuelva la llamada a su back-end para recuperar el mensaje seguro que se debe mostrar.</span><span class="sxs-lookup"><span data-stu-id="d92bb-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>
<span data-ttu-id="d92bb-132">Para lograr este objetivo, tiene que asegurarse de que la aplicación Android sabe cómo autenticarse a sí misma con el back-end cuando recibe las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="d92bb-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span></span>

<span data-ttu-id="d92bb-133">A continuación, modificaremos el flujo de *inicio de sesión* para guardar el valor de encabezado de autenticación en las preferencias compartidas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d92bb-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span></span> <span data-ttu-id="d92bb-134">Se pueden usar mecanismos similares para almacenar cualquier token de autenticación (por ejemplo tokens OAuth) que la aplicación tendrá que usar sin solicitar credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="d92bb-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span></span>

1. <span data-ttu-id="d92bb-135">En el proyecto de la aplicación Android, agregue las siguientes constantes en la parte superior de la clase **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="d92bb-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="d92bb-136">Todavía en la clase **MainActivity**, actualice el método `getAuthorizationHeader()` para que contenga el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d92bb-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="d92bb-137">Agregue la siguientes instrucciones `import` en la parte superior del archivo **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="d92bb-137">Add the following `import` statements at the top of the **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="d92bb-138">Ahora cambiaremos el controlador al que se llama cuando se recibe la notificación.</span><span class="sxs-lookup"><span data-stu-id="d92bb-138">Now we will change the handler that is called when the notification is received.</span></span>

1. <span data-ttu-id="d92bb-139">En la clase **MyHandler**, cambie el método `OnReceive()` para que contenga:</span><span class="sxs-lookup"><span data-stu-id="d92bb-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="d92bb-140">Después, agregue el método `retrieveNotification()`, reemplazando el marcador de posición `{back-end endpoint}` con el extremo back-end obtenido mientras se implementa su back-end:</span><span class="sxs-lookup"><span data-stu-id="d92bb-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed to retrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="d92bb-141">Este método llama al back-end de la aplicación para recuperar el contenido de la notificación usando las credenciales almacenadas en las preferencias compartidas y lo muestra como una notificación normal.</span><span class="sxs-lookup"><span data-stu-id="d92bb-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="d92bb-142">El aspecto de la notificación para el usuario de la aplicación es exactamente el mismo que cualquier otra notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="d92bb-142">The notification looks to the app user exactly like any other push notification.</span></span>

<span data-ttu-id="d92bb-143">Tenga en cuenta que es preferible administrar los casos de propiedad de encabezado de autenticación ausente o rechazo por el backend.</span><span class="sxs-lookup"><span data-stu-id="d92bb-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="d92bb-144">La administración específica de estos casos depende principalmente de la experiencia del usuario de destino.</span><span class="sxs-lookup"><span data-stu-id="d92bb-144">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="d92bb-145">Una opción es mostrar una notificación con un mensaje genérico para el usuario con el fin de que se autentique para recuperar la notificación real.</span><span class="sxs-lookup"><span data-stu-id="d92bb-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="d92bb-146">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d92bb-146">Run the Application</span></span>
<span data-ttu-id="d92bb-147">Para ejecutar la aplicación, realice las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="d92bb-147">To run the application, do the following:</span></span>

1. <span data-ttu-id="d92bb-148">Asegúrese de que **AppBackend** se ha implementado en Azure.</span><span class="sxs-lookup"><span data-stu-id="d92bb-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="d92bb-149">Si usa Visual Studio, ejecute la aplicación de API web **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="d92bb-149">If using Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="d92bb-150">Se mostrará una página web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d92bb-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="d92bb-151">En Eclipse, ejecute la aplicación en un dispositivo Android físico o en el emulador.</span><span class="sxs-lookup"><span data-stu-id="d92bb-151">In Eclipse, run the app on a physical Android device or the emulator.</span></span>
3. <span data-ttu-id="d92bb-152">En la interfaz de usuario de la aplicación Android, escriba un nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="d92bb-152">In the Android app UI, enter a username and password.</span></span> <span data-ttu-id="d92bb-153">Esta información puede ser cualquier cadena, pero deben tener el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="d92bb-153">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="d92bb-154">En la interfaz de usuario de la aplicación Android, haga clic en **Log in**(Iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="d92bb-154">In the Android app UI, click **Log in**.</span></span> <span data-ttu-id="d92bb-155">A continuación, haga clic en **Send push**(Enviar inserción).</span><span class="sxs-lookup"><span data-stu-id="d92bb-155">Then click **Send push**.</span></span>

