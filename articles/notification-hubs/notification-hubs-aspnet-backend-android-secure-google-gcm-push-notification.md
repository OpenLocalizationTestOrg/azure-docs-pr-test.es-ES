---
title: aaaSending Secure notificaciones Push con centros de notificaciones de Azure
description: "Obtenga información acerca de cómo toosend segura push aplicación Android tooan de notificaciones de Azure. Ejemplos de código escritos en Java y C#."
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
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="866b1-105">Envío de notificaciones push seguras a los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="866b1-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="866b1-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="866b1-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="866b1-107">iOS</span><span class="sxs-lookup"><span data-stu-id="866b1-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="866b1-108">Android</span><span class="sxs-lookup"><span data-stu-id="866b1-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="866b1-109">Información general</span><span class="sxs-lookup"><span data-stu-id="866b1-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="866b1-110">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="866b1-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="866b1-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="866b1-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="866b1-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="866b1-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="866b1-113">Compatibilidad con notificaciones de inserción de Microsoft Azure le permite tooaccess una infraestructura de mensaje de inserción de fácil de usar, varias plataformas y escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa plataformas móviles.</span><span class="sxs-lookup"><span data-stu-id="866b1-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="866b1-114">A veces debido a restricciones de seguridad o tooregulatory, una aplicación podría querer tooinclude algo en la notificación de Hola que no se transmiten a través de la infraestructura de notificaciones de inserción estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="866b1-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="866b1-115">Este tutorial describe cómo tooachieve Hola misma experiencia mediante el envío de información confidencial a través de una conexión segura y autenticada entre dispositivos Android de cliente de Hola y Hola backend de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="866b1-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="866b1-116">En un nivel alto, flujo de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="866b1-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="866b1-117">Hola aplicación back-end:</span><span class="sxs-lookup"><span data-stu-id="866b1-117">hello app back-end:</span></span>
   * <span data-ttu-id="866b1-118">Almacena la carga segura en la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="866b1-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="866b1-119">Envía el Id. de Hola de este dispositivo Android de notificación toohello (se envía ninguna información segura).</span><span class="sxs-lookup"><span data-stu-id="866b1-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="866b1-120">aplicación Hello en dispositivo hello, al recibir la notificación de hello:</span><span class="sxs-lookup"><span data-stu-id="866b1-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="866b1-121">dispositivos Android Hola contacta con hello back-end que lo solicita Hola carga de seguridad.</span><span class="sxs-lookup"><span data-stu-id="866b1-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="866b1-122">aplicación Hello puede mostrar carga hello como una notificación en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="866b1-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="866b1-123">Es importante toonote que Hola anterior flujo (y en este tutorial), se da por supuesto ese dispositivo Hola almacena un token de autenticación en el almacenamiento local, después de hello usuario inicia sesión en.</span><span class="sxs-lookup"><span data-stu-id="866b1-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="866b1-124">Esto garantiza una experiencia completamente sin problemas, como dispositivo de hello puede recuperar la carga de seguridad de la notificación de hello con este token.</span><span class="sxs-lookup"><span data-stu-id="866b1-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="866b1-125">Si la aplicación no almacena tokens de autenticación en el dispositivo de hello, o si pueden haber expirado estos tokens, aplicación de dispositivo de hello, tras recibir la notificación de inserción de hello debe mostrar una notificación genérica preguntar aplicación Hola de hello usuario toolaunch.</span><span class="sxs-lookup"><span data-stu-id="866b1-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="866b1-126">aplicación Hello, a continuación, autentica el usuario de Hola y muestra la carga de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="866b1-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="866b1-127">Este tutorial muestra cómo las notificaciones de inserción toosend segura.</span><span class="sxs-lookup"><span data-stu-id="866b1-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="866b1-128">Se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, por lo que debe completar los pasos de hello en este tutorial primero si no lo ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="866b1-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="866b1-129">En este tutorial se supone que se ha creado y configurado el Centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="866b1-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="866b1-130">Modificar el proyecto de Android Hola</span><span class="sxs-lookup"><span data-stu-id="866b1-130">Modify hello Android project</span></span>
<span data-ttu-id="866b1-131">Ahora que ha modificado su Hola solo de aplicación back-end toosend *identificador* de una notificación de inserción, tienen toochange su toohandle aplicación Android notificación y devolución de llamada su hello tooretrieve de back-end seguros toobe de mensaje que se muestra.</span><span class="sxs-lookup"><span data-stu-id="866b1-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="866b1-132">tooachieve este objetivo tiene toomake seguro de que la aplicación Android sabe cómo tooauthenticate con el back-end cuando recibe notificaciones de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="866b1-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="866b1-133">Ahora modificaremos hello *inicio de sesión* flujo en el valor del encabezado de autenticación orden toosave Hola Hola comparten las preferencias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="866b1-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="866b1-134">Mecanismos análogos pueden ser utilizado toostore cualquier token de autenticación (por ejemplo, tokens de OAuth) que Hola aplicación tendrá toouse sin necesidad de credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="866b1-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="866b1-135">En el proyecto de aplicación de Android, agregar Hola siguientes constantes en parte superior de Hola de hello **MainActivity** clase:</span><span class="sxs-lookup"><span data-stu-id="866b1-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="866b1-136">Aún en hello **MainActivity** (clase), actualización hello `getAuthorizationHeader()` hello toocontain de método siguiente código:</span><span class="sxs-lookup"><span data-stu-id="866b1-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="866b1-137">Agregue los siguiente hello `import` las instrucciones en la parte superior de Hola de hello **MainActivity** archivo:</span><span class="sxs-lookup"><span data-stu-id="866b1-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="866b1-138">Ahora cambiaremos controlador Hola que se llama cuando se recibe la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="866b1-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="866b1-139">Hola **MyHandler** clase cambiar hello `OnReceive()` método toocontain:</span><span class="sxs-lookup"><span data-stu-id="866b1-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="866b1-140">A continuación, agregue hello `retrieveNotification()` método, reemplazando el marcador de posición de hello `{back-end endpoint}` con punto de conexión de back-end de hello obtenido al implementar el back-end:</span><span class="sxs-lookup"><span data-stu-id="866b1-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="866b1-141">Este método llama a su contenido usando credenciales de hello almacenadas en hello compartido preferencias y lo muestra como una notificación normal de notificación de Hola de tooretrieve de back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="866b1-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="866b1-142">notificación de Hello busca toohello de usuario de aplicación exactamente igual que cualquier otra notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="866b1-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="866b1-143">Tenga en cuenta que es preferible toohandle casos de Hola de propiedad de encabezado de autenticación que falta o el rechazo por hello back-end.</span><span class="sxs-lookup"><span data-stu-id="866b1-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="866b1-144">control específico de Hola de estos casos dependen principalmente de la experiencia del usuario de destino.</span><span class="sxs-lookup"><span data-stu-id="866b1-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="866b1-145">Una opción es toodisplay una notificación con un mensaje genérico para la notificación de real de hello usuario tooauthenticate tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="866b1-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="866b1-146">Ejecutar aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="866b1-146">Run hello Application</span></span>
<span data-ttu-id="866b1-147">toorun Hola aplicación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="866b1-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="866b1-148">Asegúrese de que **AppBackend** se ha implementado en Azure.</span><span class="sxs-lookup"><span data-stu-id="866b1-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="866b1-149">Si utiliza Visual Studio, ejecute hello **AppBackend** aplicación de API Web.</span><span class="sxs-lookup"><span data-stu-id="866b1-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="866b1-150">Se mostrará una página web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="866b1-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="866b1-151">En Eclipse, ejecutar la aplicación hello en un emulador de dispositivo o hello Android físico.</span><span class="sxs-lookup"><span data-stu-id="866b1-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="866b1-152">En la aplicación hello Android interfaz de usuario, escriba un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="866b1-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="866b1-153">Pueden ser cualquier cadena, pero deben ser Hola el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="866b1-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="866b1-154">En la aplicación hello Android interfaz de usuario, haga clic en **sesión**.</span><span class="sxs-lookup"><span data-stu-id="866b1-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="866b1-155">A continuación, haga clic en **Enviar inserción**.</span><span class="sxs-lookup"><span data-stu-id="866b1-155">Then click **Send push**.</span></span>

