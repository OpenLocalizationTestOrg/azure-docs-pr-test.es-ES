---
title: "aaaiOS notificaciones de inserción con centros de notificaciones para las aplicaciones de Xamarin | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de notificaciones de tooa Xamarin."
services: notification-hubs
keywords: "notificaciones push de ios,mensajes de inserción,notificaciones push,mensaje de notificación"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="1a3d7-104">Notificaciones push de iOS con Centros de notificaciones para aplicaciones Xamarin</span><span class="sxs-lookup"><span data-stu-id="1a3d7-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1a3d7-105">Información general</span><span class="sxs-lookup"><span data-stu-id="1a3d7-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1a3d7-106">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1a3d7-107">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1a3d7-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="1a3d7-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="1a3d7-109">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de tooan de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="1a3d7-110">Se creará una aplicación de Xamarin.iOS en blanco que recibe notificaciones de inserción mediante hello [servicio de notificaciones de inserción de Apple (APN)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="1a3d7-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="1a3d7-111">Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="1a3d7-112">Hello terminado código está disponible en hello [NotificationHubs aplicación] [ GitHub] ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="1a3d7-113">Este tutorial muestra el escenario de difusión mensajes de Hola simple inserción con centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a3d7-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1a3d7-114">Prerequisites</span></span>
<span data-ttu-id="1a3d7-115">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="1a3d7-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="1a3d7-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="1a3d7-117">Un dispositivo compatible con iOS 7.0 (o una versión posterior)</span><span class="sxs-lookup"><span data-stu-id="1a3d7-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="1a3d7-118">Pertenencia al programa para desarrolladores de iOS</span><span class="sxs-lookup"><span data-stu-id="1a3d7-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="1a3d7-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="1a3d7-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="1a3d7-120">Debido a los requisitos de configuración para las notificaciones de inserción de iOS, debe implementar y probar la aplicación de ejemplo de Hola en un dispositivo físico iOS (iPhone o iPad) en lugar de en el simulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="1a3d7-121">La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones Xamarin para iOS.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="1a3d7-122">Configuración de su Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="1a3d7-122">Configure your notification hub</span></span>
<span data-ttu-id="1a3d7-123">En esta sección le guía a través de la creación de un nuevo centro de notificaciones y configurar la autenticación con APNS mediante hello **. p12** certificado de inserción que creó.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="1a3d7-124">Si desea toouse un centro de notificaciones que ya haya creado, puede omitir toostep 5.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="1a3d7-125">Puesto que queremos conexión de APN hello tooconfigure, Hola Portal de Azure, abra la configuración del centro de notificaciones, ande haga clic en <b>Notification Services</b>y, a continuación, haga clic en hello <b>Apple (APN)</b> elemento de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="1a3d7-126">Una vez terminado, haga clic en <b>cargar certificado</b> y seleccione hello <b>. p12</b> certificado que exportó anteriormente, así como la contraseña de hello para el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="1a3d7-127">Asegúrese de que tooselect <b>espacio aislado</b> modo desde que se van a enviar inserción los mensajes en un entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="1a3d7-128">Usar solo hello <b>producción</b> establecer si desea toousers de notificaciones de inserción de toosend que ya ha adquirido la aplicación desde el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="1a3d7-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="1a3d7-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="1a3d7-130">El centro de notificaciones está ahora configurado toowork con APNS, y tiene la aplicación de tooregister de cadenas de conexión de Hola y enviar notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="1a3d7-131">Conectar el centro de notificaciones de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="1a3d7-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="1a3d7-132">Crear un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="1a3d7-132">Create a new project</span></span>
1. <span data-ttu-id="1a3d7-133">En Xamarin Studio, cree un nuevo proyecto de iOS y seleccione hello **API unificada** > **única aplicación de vista** plantilla.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio: Selección del tipo de aplicación][31]
2. <span data-ttu-id="1a3d7-135">Agregue un componente de mensajería de Azure toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="1a3d7-136">Hola vista de soluciones, haga clic en hello **componentes** carpeta de su proyecto y elija **obtener más componentes**.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="1a3d7-137">Busque hello **la mensajería de Azure** componentes y agregue Hola componente tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="1a3d7-138">En **AppDelegate.cs**, agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="1a3d7-139">Declare una instancia de **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="1a3d7-140">Crear un **Constants.cs** clase con hello siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="1a3d7-141">En **AppDelegate.cs**, actualizar **FinishedLaunching()** siguiente de Hola toomatch:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="1a3d7-142">Invalidar hello **RegisteredForRemoteNotifications()** método **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="1a3d7-143">Invalidar hello **ReceivedRemoteNotification()** método **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="1a3d7-144">Cree Hola siguiente **ProcessNotification()** método **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="1a3d7-145">Puede elegir toooverride **FailedToRegisterForRemoteNotifications()** toohandle situaciones como no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="1a3d7-146">Esto es especialmente importante que usuario Hola podría iniciar la aplicación en modo sin conexión (por ejemplo, avión) y desee inserción toohandle aplicación tooyour específico de escenarios de mensajería.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="1a3d7-147">Ejecute la aplicación hello en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="1a3d7-148">Envío de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="1a3d7-148">Sending Push Notifications</span></span>
<span data-ttu-id="1a3d7-149">Puede probar recibiendo notificaciones de inserción en la aplicación mediante el envío de notificaciones en hello [Portal de Azure] a través de hello **probar envío** capacidad en hello **solución de problemas** conjunto de herramientas y a la derecha en la página de concentrador de notificación hello, como se muestra en la siguiente pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="1a3d7-150">Las notificaciones push se envían normalmente en un servicio back-end como Servicios móviles o ASP.NET mediante una biblioteca compatible.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="1a3d7-151">También puede utilizar Hola API de REST directamente toosend inserción mensajes si una biblioteca no está disponible en el escenario.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="1a3d7-152">En este tutorial, agregaremos simplificar y solo muestran probar la aplicación cliente mediante el envío de notificaciones mediante Hola .NET SDK centrales de notificaciones en una aplicación de consola en lugar de un servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="1a3d7-153">Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial como paso siguiente de Hola para enviar notificaciones desde un back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="1a3d7-154">Sin embargo, Hola siguiendo métodos puede utilizarse para enviar notificaciones:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="1a3d7-155">**Interfaz REST**: puede admitir la notificación de inserción en cualquier plataforma de back-end mediante hello [interfaz REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a3d7-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="1a3d7-156">**SDK de .NET de Microsoft Azure notificación concentradores**: Hola Administrador de paquetes de Nuget para Visual Studio, ejecutar [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="1a3d7-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="1a3d7-157">**Node.js** : [cómo toouse centros de notificaciones de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1a3d7-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="1a3d7-158">**Aplicaciones móviles**: para obtener un ejemplo de cómo toosend notificaciones desde un back-end de aplicaciones de Mobile de servicio de aplicación de Azure que se integra con centros de notificaciones, consulte [Agregar aplicación móvil de inserción notificaciones tooyour](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="1a3d7-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="1a3d7-159">**Java / PHP**: para obtener un ejemplo de cómo las notificaciones de inserción de toosend mediante el uso de hello las API de REST, vea "cómo toouse centros de notificaciones de Java y PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="1a3d7-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="1a3d7-160">Envío de notificaciones push desde una aplicación de consola .NET (opcional)</span><span class="sxs-lookup"><span data-stu-id="1a3d7-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="1a3d7-161">En esta sección, enviará notificaciones push con una aplicación sencilla de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="1a3d7-162">Para fines de Hola de este ejemplo, se cambiará el entorno de desarrollo de Windows tooa que tiene Visual Studio instalado.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="1a3d7-163">En Visual Studio, cree una nueva aplicación de consola en Visual C#:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="1a3d7-164">En Visual Studio, haga clic en **Herramientas**, **Administrador de paquetes NuGet** y, después, en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="1a3d7-165">consola del Administrador de paquetes de saludo debe aparecer toohello acoplada inferior del área de trabajo de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="1a3d7-166">En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="1a3d7-167">Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="1a3d7-168">Abra hello `Program.cs` de archivos y agregue Hola siguiente `using` instrucción, garantizando así que podemos usar Azure clases y funciones dentro de la clase principal:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="1a3d7-169">En su `Program` clase, agregue Hola siguiendo el método (no olvide hello tooreplace **cadena de conexión** y **nombre del concentrador**):</span><span class="sxs-lookup"><span data-stu-id="1a3d7-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="1a3d7-170">Agregar Hola después de las líneas de su `Main` método:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="1a3d7-171">Presione aplicación Hola de hello F5 toorun clave.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="1a3d7-172">En unos segundos, verá que aparece una notificación push en su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="1a3d7-173">Si usas Wi-Fi o una red de datos móviles, asegúrese de que haya una conexión a internet activa en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="1a3d7-174">Puede encontrar todas las cargas posibles Hola Hola Apple [locales y Guía de programación de notificaciones de inserción].</span><span class="sxs-lookup"><span data-stu-id="1a3d7-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="1a3d7-175">Envío de notificaciones desde un servicio móvil (opcional)</span><span class="sxs-lookup"><span data-stu-id="1a3d7-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="1a3d7-176">En esta sección, enviaremos notificaciones push mediante un servicio móvil a través de un script de Node.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="1a3d7-177">toosend una notificación mediante el uso de un servicio móvil, siga [empezar a trabajar con servicios móviles]y, a continuación:</span><span class="sxs-lookup"><span data-stu-id="1a3d7-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="1a3d7-178">Inicie sesión en toohello [Portal clásico de Azure]y seleccione su servicio móvil.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="1a3d7-179">Seleccione hello **programador** ficha en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="1a3d7-180">Cree un nuevo trabajo programado, inserte un nombre y seleccione **A petición**.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="1a3d7-181">Cuando se crea el trabajo de hello, haga clic en el nombre del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="1a3d7-182">A continuación, haga clic en hello **Script** ficha en la barra superior Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="1a3d7-183">Inserte la siguiente secuencia de comandos dentro de la función de programador de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="1a3d7-184">Asegúrese de los marcadores de posición hello tooreplace seguro con la notificación concentrador hello y nombre de cadena de conexión para *DefaultFullSharedAccessSignature* que ha obtenido antes.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="1a3d7-185">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="1a3d7-186">Haga clic en **ejecutar una vez** en la barra de la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="1a3d7-187">Debe recibir una alerta en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a3d7-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a3d7-188">Next steps</span></span>
<span data-ttu-id="1a3d7-189">En este sencillo ejemplo, difunden tooall de notificaciones de inserción los dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="1a3d7-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="1a3d7-190">En el orden tootarget a usuarios específicos, consulte tutorial toohello [toousers de notificaciones de los centros de notificaciones de uso toopush].</span><span class="sxs-lookup"><span data-stu-id="1a3d7-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="1a3d7-191">Si desea que toosegment los usuarios por grupos de interés, puede leer [toosend de centros de notificaciones utilice noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="1a3d7-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="1a3d7-192">Más información acerca de cómo toouse centros de notificaciones de [Guía de centros de notificaciones] y Hola [iOS de centros de notificaciones cómo-toofor].</span><span class="sxs-lookup"><span data-stu-id="1a3d7-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[empezar a trabajar con servicios móviles]: /develop/mobile/tutorials/get-started-xamarin-ios
[Portal clásico de Azure]: https://manage.windowsazure.com/
[Guía de centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS de centros de notificaciones cómo-toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[toousers de notificaciones de los centros de notificaciones de uso toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de centros de notificaciones utilice noticias de última hora]: /manage/services/notification-hubs/breaking-news-dotnet

[locales y Guía de programación de notificaciones de inserción]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Portal de Azure]: https://portal.azure.com
