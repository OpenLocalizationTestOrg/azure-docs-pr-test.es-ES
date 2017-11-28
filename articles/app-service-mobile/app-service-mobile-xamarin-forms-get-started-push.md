---
title: "aaaAdd inserción notificaciones tooyour Xamarin.Forms aplicación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure services toosend multiplataforma inserción notificaciones tooyour Xamarin.Forms aplicaciones."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="0f1f9-103">Agregar aplicación de Xamarin.Forms de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="0f1f9-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="0f1f9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0f1f9-104">Overview</span></span>
<span data-ttu-id="0f1f9-105">En este tutorial, agregará proyectos Hola de tooall de notificaciones de inserción que dan como resultado de hello [inicio rápido de Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f1f9-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="0f1f9-106">Esto significa que se envía una notificación de inserción clientes multiplataforma de tooall cada vez que se inserta un registro.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="0f1f9-107">Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="0f1f9-108">Para obtener más información, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0f1f9-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f1f9-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0f1f9-109">Prerequisites</span></span>
<span data-ttu-id="0f1f9-110">Para iOS, necesitará una [suscripción de Apple Developer Program](https://developer.apple.com/programs/ios/) y un dispositivo de iOS físico.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="0f1f9-111">Hola [simulador de iOS no admite notificaciones de inserción](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="0f1f9-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="0f1f9-112"><a name="configure-hub"></a>Configurar un Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="0f1f9-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="0f1f9-113">Actualizar notificaciones de inserción de hello servidor proyecto toosend</span><span class="sxs-lookup"><span data-stu-id="0f1f9-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="0f1f9-114">Configurar y ejecutar el proyecto de Android de hello (opcional)</span><span class="sxs-lookup"><span data-stu-id="0f1f9-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="0f1f9-115">Completar esta sección tooenable las notificaciones de inserción hello Xamarin.Forms Droid proyecto para Android.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="0f1f9-116">Habilitar la mensajería en la nube Firebase (FCM)</span><span class="sxs-lookup"><span data-stu-id="0f1f9-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="0f1f9-117">Configurar solicitudes de inserción de hello aplicaciones móviles back-end toosend mediante FCM</span><span class="sxs-lookup"><span data-stu-id="0f1f9-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="0f1f9-118">Agregar proyecto de Android de toohello de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="0f1f9-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="0f1f9-119">Con hello back-end configurado con FCM, puede agregar componentes y códigos tooregister de cliente de toohello con FCM.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="0f1f9-120">También puede registrar las notificaciones de inserción con centros de notificaciones de Azure a través de hello aplicaciones móviles volver finalizar y recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="0f1f9-121">Hola **Droid** proyecto de equipo y haga clic en hello **componentes** carpeta y haga clic en **obtener más componentes de...** . A continuación, busque hello **el cliente de mensajería de nube de Google** componente y agregue el proyecto de toohello.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="0f1f9-122">Este componente es compatible con las notificaciones push para un proyecto de Xamarin para Android.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="0f1f9-123">Abrir archivo de proyecto de hello MainActivity.cs y agregue Hola siguiente instrucción al principio de hello del archivo de hello:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="0f1f9-124">Agregar Hola después código toohello **OnCreate** llamada al método después de hello demasiado**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="0f1f9-125">Agregue un nuevo método auxiliar **CreateAndShowDialog** , como sigue:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="0f1f9-126">Agregar Hola después código toohello **MainActivity** clase:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-126">Add hello following code toohello **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="0f1f9-127">Esto expone Hola actual **MainActivity** de instancia, por lo que podemos ejecutar en el subproceso de interfaz de usuario principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="0f1f9-128">Inicializar hello `instance` variable al principio de Hola de hello **OnCreate** método, tal como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="0f1f9-129">Agregar un nuevo toohello de archivo de clase **Droid** proyecto denominado `GcmService.cs`y asegúrese de seguro siguiente hello **con** instrucciones están presentes en la parte superior de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. <span data-ttu-id="0f1f9-130">Agregar Hola siguiendo las solicitudes de permiso al principio de hello del archivo de hello, después de hello **con** instrucciones y antes de hello **espacio de nombres** declaración.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="0f1f9-131">Agregar Hola tras el espacio de nombres de clase definición toohello.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="0f1f9-132">Reemplace **<PROJECT_NUMBER>** por el número de proyecto que anotó antes.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="0f1f9-133">Reemplace Hola vacía **GcmService** clase con hello siguiente código, que usa el receptor de difusión de hello nueva:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="0f1f9-134">Agregar Hola después código toohello **GcmService** clase.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="0f1f9-135">Esto invalida hello **OnRegistered** controlador de eventos e implementa un **registrar** método.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    <span data-ttu-id="0f1f9-136">Tenga en cuenta que este código usa hello `messageParam` parámetro en el registro de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="0f1f9-137">Agregar Hola después el código que implementa **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-137">Add hello following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="0f1f9-138">Esto controla las notificaciones entrantes y los envía toobe manager toohello notificación que muestra.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="0f1f9-139">**GcmServiceBase** también requiere hello tooimplement **OnUnRegistered** y **OnError** métodos de controlador, lo que puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="0f1f9-140">Ahora, está listo pruebas notificaciones de inserción en la aplicación hello que se ejecuta en un dispositivo Android u Hola emulador.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="0f1f9-141">Prueba de las notificaciones push en la aplicación de Android</span><span class="sxs-lookup"><span data-stu-id="0f1f9-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="0f1f9-142">Hola dos primeros pasos son necesarios cuando se está probando en un emulador.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="0f1f9-143">Asegúrese de que se va a implementar tooor depuración en un dispositivo virtual que tiene Google APIs establecer como destino de hello, tal y como se muestra a continuación, en el Administrador de dispositivos virtuales Android Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="0f1f9-144">Agregar un dispositivo Android de Google cuenta toohello haciendo clic en **aplicaciones** > **configuración** > **Agregar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="0f1f9-145">A continuación, siga Hola indicaciones tooadd un dispositivo existente de toohello de cuenta de Google o toocreate uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="0f1f9-146">En Visual Studio o Xamarin Studio, haga clic en hello **Droid** del proyecto y haga clic en **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="0f1f9-147">Haga clic en **ejecutar** toobuild Hola proyecto e iniciar aplicación hello en el emulador o dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="0f1f9-148">En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello signo más (**+**) icono.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="0f1f9-149">Compruebe que se recibe una notificación cuando se agrega un artículo.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="0f1f9-150">Configurar y ejecutar el proyecto de iOS de hello (opcional)</span><span class="sxs-lookup"><span data-stu-id="0f1f9-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="0f1f9-151">Esta sección es para ejecutar el proyecto de iOS de Xamarin Hola para dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="0f1f9-152">Puede omitir esta sección si no está trabajando con dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="0f1f9-153">Centro de notificaciones de Hola de configuración de APNS</span><span class="sxs-lookup"><span data-stu-id="0f1f9-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="0f1f9-154">A continuación, configurará configuración del proyecto de iOS de hello en Xamarin Studio o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="0f1f9-155">Agregar aplicación de iOS de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="0f1f9-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="0f1f9-156">Hola **iOS** del proyecto, abra AppDelegate.cs y agregue Hola después de la parte superior de toohello de instrucción del archivo de código de hello.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="0f1f9-157">Hola **AppDelegate** de clases, agregue una invalidación para hello **RegisteredForRemoteNotifications** tooregister de eventos para las notificaciones:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. <span data-ttu-id="0f1f9-158">En **AppDelegate**, agregar Hola después de invalidación para hello **DidReceiveRemoteNotification** controlador de eventos:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    <span data-ttu-id="0f1f9-159">Este método controla las notificaciones entrantes mientras se ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="0f1f9-160">Hola **AppDelegate** clase, agregue Hola después código toohello **FinishedLaunching** método:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="0f1f9-161">Tras esto, se habilita la compatibilidad con las notificaciones remotas y el registro de inserción de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="0f1f9-162">La aplicación ya está actualizado toosupport notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="0f1f9-163">Prueba de las notificaciones push en su aplicación de iOS</span><span class="sxs-lookup"><span data-stu-id="0f1f9-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="0f1f9-164">Haga clic en proyecto de iOS de Hola y haga clic en **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="0f1f9-165">Hola presione **ejecutar** botón o **F5** en Visual Studio toobuild Hola proyecto e iniciar aplicación hello en un dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="0f1f9-166">A continuación, haga clic en **Aceptar** tooaccept notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0f1f9-167">Debe aceptar de forma explícita las notificaciones push desde su aplicación.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="0f1f9-168">Esta solicitud sólo produce a Hola primera vez que Hola se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="0f1f9-169">En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello signo más (**+**) icono.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="0f1f9-170">Compruebe que se recibe una notificación y, a continuación, haga clic en **Aceptar** toodismiss Hola notificación.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="0f1f9-171">Configuración y ejecución de proyectos de Windows (opcional)</span><span class="sxs-lookup"><span data-stu-id="0f1f9-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="0f1f9-172">En esta sección es para ejecutar Hola Xamarin.Forms WinApp y WinPhone81 proyectos para dispositivos de Windows.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="0f1f9-173">Estos pasos también son compatibles con los proyectos de Plataforma universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="0f1f9-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="0f1f9-174">Puede omitir esta sección si no está trabajando con dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="0f1f9-175">Registro de la aplicación de Windows para notificaciones de inserción en el Servicio de notificaciones de Windows (WNS)</span><span class="sxs-lookup"><span data-stu-id="0f1f9-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="0f1f9-176">Centro de notificaciones de Hola de configuración de WNS</span><span class="sxs-lookup"><span data-stu-id="0f1f9-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="0f1f9-177">Agregar aplicación de Windows de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="0f1f9-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="0f1f9-178">En Visual Studio, abra **App.xaml.cs** en una ventana de proyecto y agregar Hola siguiendo las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="0f1f9-179">Reemplace `<your_TodoItemManager_portable_class_namespace>` con hello espacio de nombres del proyecto portátil que contiene Hola `TodoItemManager` clase.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="0f1f9-180">En App.xaml.cs, agregue el siguiente de hello **InitNotificationsAsync** método:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    <span data-ttu-id="0f1f9-181">Este método obtiene el canal de notificación de inserción de Hola y registra un notificaciones de plantilla de tooreceive plantilla desde el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="0f1f9-182">Una notificación de plantilla que admita *messageParam* se entregarán toothis cliente.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="0f1f9-183">En App.xaml.cs, actualice hello **OnLaunched** definición de método de controlador de eventos mediante la adición de hello `async` modificador.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="0f1f9-184">A continuación, agregue Hola después de la línea de código al final de hello del método hello:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="0f1f9-185">Esto garantiza que se crea o se actualiza cada vez que se inicia la aplicación hello registro de notificaciones de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="0f1f9-186">Es importante toodo esta tooguarantee que Hola WNS inserción canal siempre está activo.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="0f1f9-187">En el Explorador de soluciones de Visual Studio, abra hello **Package.appxmanifest** de archivos y establecer **capaz de recibir** demasiado**Sí** en **notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="0f1f9-188">Compilar la aplicación hello y compruebe que no dispone de ningún error.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="0f1f9-189">La aplicación cliente ahora debe registrar para notificaciones de plantilla de Hola de hello que terminar de aplicaciones móviles de nuevo.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="0f1f9-190">Repita esta sección para cada proyecto de Windows de la solución.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="0f1f9-191">Prueba de las notificaciones push en su aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="0f1f9-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="0f1f9-192">En Visual Studio, haga clic con el botón derecho en un proyecto de Windows y luego haga clic en **Establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="0f1f9-193">Hola presione **ejecutar** botón proyecto de hello toobuild e iniciar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="0f1f9-194">En la aplicación hello, escriba un nombre para un todoitem nueva y, a continuación, haga clic en hello signo más (**+**) tooadd de icono.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="0f1f9-195">Compruebe que se recibe una notificación cuando se agrega el elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f1f9-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f1f9-196">Next steps</span></span>
<span data-ttu-id="0f1f9-197">Puede obtener más información sobre las notificaciones de inserción:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="0f1f9-198">Diagnosticar problemas de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="0f1f9-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="0f1f9-199">: existen varias razones para que las notificaciones se pierdan o no lleguen a los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="0f1f9-200">Este tema muestra cómo hacer que tooanalyze y averiguar la raíz de Hola de errores de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="0f1f9-201">También puede seguir en tooone de hello tutoriales:</span><span class="sxs-lookup"><span data-stu-id="0f1f9-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="0f1f9-202">Agregar aplicación de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="0f1f9-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="0f1f9-203">Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="0f1f9-204">Activación de la sincronización sin conexión para la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="0f1f9-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="0f1f9-205">Obtenga información acerca de cómo tooadd compatibilidad sin conexión para la aplicación mediante el uso de aplicaciones móviles de un back-end.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="0f1f9-206">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="0f1f9-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
