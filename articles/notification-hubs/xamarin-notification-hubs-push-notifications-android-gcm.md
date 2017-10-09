---
title: aaaGet a trabajar con los centros de notificaciones para las aplicaciones de Xamarin.Android | Documentos de Microsoft
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push notificaciones tooa aplicación Xamarin para Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="8df16-103">Introducción a Centros de notificaciones con Xamarin para Android</span><span class="sxs-lookup"><span data-stu-id="8df16-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="8df16-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8df16-104">Overview</span></span>
<span data-ttu-id="8df16-105">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de notificaciones de tooa Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="8df16-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="8df16-106">Creará una aplicación Xamarin.Android en blanco que reciba notificaciones push mediante el servicio de mensajería en la nube de Google (GCM).</span><span class="sxs-lookup"><span data-stu-id="8df16-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="8df16-107">Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8df16-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="8df16-108">Hello terminado código está disponible en hello [NotificationHubs aplicación] [ GitHub] ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8df16-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="8df16-109">Este tutorial muestra el escenario sencillo de difusión hello en usar centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="8df16-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8df16-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8df16-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="8df16-111">código de Hello completado para este tutorial se puede encontrar en GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="8df16-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8df16-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8df16-112">Prerequisites</span></span>
<span data-ttu-id="8df16-113">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="8df16-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="8df16-114">Las instrucciones de instalación completas de Visual Studio con Xamarin en Windows o Xamarin Studio en Mac OS X se encuentran en [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="8df16-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="8df16-115">Cuenta de Google activa</span><span class="sxs-lookup"><span data-stu-id="8df16-115">Active Google account</span></span>
* <span data-ttu-id="8df16-116">[Componente de mensajería de Azure]</span><span class="sxs-lookup"><span data-stu-id="8df16-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="8df16-117">[Componente del Cliente de mensajería en la nube de Google]</span><span class="sxs-lookup"><span data-stu-id="8df16-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="8df16-118">Completar este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="8df16-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8df16-119">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="8df16-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8df16-120">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="8df16-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8df16-121">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="8df16-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="8df16-122">Habilitación del servicio de mensajería en la nube de Google</span><span class="sxs-lookup"><span data-stu-id="8df16-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="8df16-123">Configuración de su Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="8df16-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="8df16-124">Haga clic en hello <b>configurar</b> ficha en la parte superior de hello, escriba Hola <b>clave de API</b> valor obtenidas en la sección anterior de hello y, a continuación, haga clic en <b>guardar</b>.</span><span class="sxs-lookup"><span data-stu-id="8df16-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="8df16-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="8df16-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="8df16-126">El centro de notificaciones está ahora configurado toowork con GCM y tiene tooboth de cadenas de conexión de hello registrar los notificaciones de tooreceive de aplicación y las notificaciones de inserción de toosend.</span><span class="sxs-lookup"><span data-stu-id="8df16-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="8df16-127">Conectar el centro de notificaciones de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="8df16-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="8df16-128">Crear un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="8df16-128">Create a new project</span></span>
1. <span data-ttu-id="8df16-129">En Xamarin Studio, haga clic en **Nueva solución**, haga clic en **Aplicación Android**, y luego en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8df16-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="8df16-130">Escriba su **Nombre de la aplicación** e **Identificador**.</span><span class="sxs-lookup"><span data-stu-id="8df16-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="8df16-131">Haga clic en hello **las plataformas de destino** que desee toosupport y, a continuación, haga clic en **siguiente** y **crear**.</span><span class="sxs-lookup"><span data-stu-id="8df16-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="8df16-132">Esto crea un nuevo proyecto de Android.</span><span class="sxs-lookup"><span data-stu-id="8df16-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="8df16-133">Abrir propiedades del proyecto Hola haciendo clic en el proyecto nuevo en hello vista soluciones y elegir **opciones**.</span><span class="sxs-lookup"><span data-stu-id="8df16-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="8df16-134">Seleccione hello **aplicación Android** elemento Hola **generar** sección.</span><span class="sxs-lookup"><span data-stu-id="8df16-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="8df16-135">Asegúrese de que la primera letra Hola de su **nombre del paquete** es en minúscula.</span><span class="sxs-lookup"><span data-stu-id="8df16-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8df16-136">Hola la primera letra del nombre del paquete Hola debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8df16-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="8df16-137">De lo contrario, recibirá errores de manifiesto de la aplicación al registrar **BroadcastReceiver** y **IntentFilter** para las notificaciones push siguientes.</span><span class="sxs-lookup"><span data-stu-id="8df16-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="8df16-138">Si lo desea, un conjunto de hello **versión mínimo Android** tooanother nivel de API.</span><span class="sxs-lookup"><span data-stu-id="8df16-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="8df16-139">Si lo desea, un conjunto de hello **versión de destino Android** toohello otra versión de API que desea tootarget (debe ser el nivel de API 8 o posterior).</span><span class="sxs-lookup"><span data-stu-id="8df16-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="8df16-140">Haga clic en **Aceptar** y cuadro de diálogo de opciones de proyecto de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="8df16-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="8df16-141">Agregar proyecto de tooyour de componentes necesarios de Hola</span><span class="sxs-lookup"><span data-stu-id="8df16-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="8df16-142">Hola Google nube cliente de mensajería disponible en el almacén de componentes de Xamarin Hola simplifica el proceso Hola de admitir las notificaciones de inserción en Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="8df16-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="8df16-143">Haga clic en carpeta de componentes de hello en aplicación Xamarin.Android y elija **obtener más componentes**.</span><span class="sxs-lookup"><span data-stu-id="8df16-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="8df16-144">Busque hello **la mensajería de Azure** componentes y agregue el proyecto de toohello.</span><span class="sxs-lookup"><span data-stu-id="8df16-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="8df16-145">Busque hello **el cliente de mensajería de nube de Google** componentes y agregue el proyecto de toohello.</span><span class="sxs-lookup"><span data-stu-id="8df16-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="8df16-146">Configuración de los centros de notificaciones en su proyecto</span><span class="sxs-lookup"><span data-stu-id="8df16-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="8df16-147">Recopile Hola siguiendo la información de la aplicación ni notificación al centro Android:</span><span class="sxs-lookup"><span data-stu-id="8df16-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="8df16-148">**GoogleProjectNumber**: obtener este valor de número de proyecto de información general de saludo de la aplicación en hello Portal para desarrolladores de Google.</span><span class="sxs-lookup"><span data-stu-id="8df16-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="8df16-149">Realiza una nota de este valor anteriormente cuando se creó la aplicación hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="8df16-150">**Cadena de conexión de escucha**: en panel de Hola Hola [Portal clásico de Azure], haga clic en **ver cadenas de conexión**.</span><span class="sxs-lookup"><span data-stu-id="8df16-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="8df16-151">Hola copia *DefaultListenSharedAccessSignature* cadena de conexión para este valor.</span><span class="sxs-lookup"><span data-stu-id="8df16-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="8df16-152">**Nombre del concentrador**: este es el nombre de Hola de su centro de hello [Portal clásico de Azure].</span><span class="sxs-lookup"><span data-stu-id="8df16-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="8df16-153">Por ejemplo, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="8df16-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="8df16-154">Crear un **Constants.cs** clase para el proyecto de Xamarin y definir Hola después de valores constantes en la clase hello.</span><span class="sxs-lookup"><span data-stu-id="8df16-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="8df16-155">Reemplace los marcadores de posición de hello con sus valores.</span><span class="sxs-lookup"><span data-stu-id="8df16-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="8df16-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="8df16-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="8df16-157">}</span><span class="sxs-lookup"><span data-stu-id="8df16-157">}</span></span>
2. <span data-ttu-id="8df16-158">Agregue los siguiente hello mediante instrucciones demasiado**MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="8df16-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="8df16-159">Agregar un toohello de variable de instancia `MainActivity` clase que será usado tooshow un cuadro de diálogo Alerta cuando se ejecuta la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="8df16-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="8df16-160">Crear hello siguiente método Hola **MainActivity** clase:</span><span class="sxs-lookup"><span data-stu-id="8df16-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="8df16-161">Hola `OnCreate` método **MainActivity.cs**, inicializar hello `instance` variable y agregue una llamada demasiado`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="8df16-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="8df16-162">Cree una nueva clase, **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="8df16-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8df16-163">Más adelante, se explicará cómo crear una clase **BroadcastReceiver** desde el principio.</span><span class="sxs-lookup"><span data-stu-id="8df16-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="8df16-164">Sin embargo, una creación rápida toomanually alternativo **MyBroadcastReceiver.cs** es toorefer toohello **GcmService.cs** archivo encontrado en el proyecto de Xamarin.Android de ejemplo de Hola incluido con hello [Ejemplos de NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="8df16-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="8df16-165">Duplicar **GcmService.cs** y cambiar los nombres de clase puede tener también un toostart perfectos.</span><span class="sxs-lookup"><span data-stu-id="8df16-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="8df16-166">Agregue los siguiente hello mediante instrucciones demasiado**MyBroadcastReceiver.cs** (que hace referencia el componente de toohello y el ensamblado que agregó anteriormente):</span><span class="sxs-lookup"><span data-stu-id="8df16-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="8df16-167">En **MyBroadcastReceiver.cs**, agregar Hola siguiendo las solicitudes de permiso entre hello **con** hello e instrucciones **espacio de nombres** declaración:</span><span class="sxs-lookup"><span data-stu-id="8df16-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="8df16-168">En **MyBroadcastReceiver.cs**, cambiar hello **MyBroadcastReceiver** clase siguiente de Hola toomatch:</span><span class="sxs-lookup"><span data-stu-id="8df16-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="8df16-169">Agregue otra clase en **MyBroadcastReceiver.cs** llamada **PushHandlerService** que derive de **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="8df16-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="8df16-170">Realizar seguro hello tooapply **servicio** toohello clase de atributos:</span><span class="sxs-lookup"><span data-stu-id="8df16-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="8df16-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** y **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="8df16-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="8df16-172">Nuestro **PushHandlerService** clase de implementación debe invalidar estos métodos, y estos métodos se activarán en toointeracting de respuesta con el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="8df16-173">Invalidar hello **OnRegistered()** método **PushHandlerService** mediante el uso de hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8df16-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="8df16-174">Hola **OnRegistered()** código encima, tenga en cuenta Hola capacidad toospecify etiquetas tooregister para los canales de mensajes específicos.</span><span class="sxs-lookup"><span data-stu-id="8df16-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="8df16-175">Invalidar hello **OnMessage** método **PushHandlerService** mediante el uso de hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8df16-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="8df16-176">Agregue los siguiente hello **createNotification** y **dialogNotify** métodos demasiado**PushHandlerService** para informar a los usuarios cuando se recibe una notificación.</span><span class="sxs-lookup"><span data-stu-id="8df16-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="8df16-177">El diseño de notificaciones en Android versión 5.0 y posteriores representa un cambio significativo respecto al de las versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="8df16-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="8df16-178">Si se prueba en Android 5.0 o versiones posteriores, aplicación hello deberá toobe ejecuta tooreceive Hola notification.</span><span class="sxs-lookup"><span data-stu-id="8df16-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="8df16-179">Para más información, consulte [Notificaciones de Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="8df16-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="8df16-180">Reemplace los miembros abstractos **OnUnRegistered()**, **OnRecoverableError()** y **OnError()** para que el código se compile:</span><span class="sxs-lookup"><span data-stu-id="8df16-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="8df16-181">Ejecutar la aplicación en el emulador Hola</span><span class="sxs-lookup"><span data-stu-id="8df16-181">Run your app in hello emulator</span></span>
<span data-ttu-id="8df16-182">Si ejecuta esta aplicación en el emulador de hello, asegúrese de que utiliza un dispositivos virtuales Android (AVD) que es compatible con Google APIs.</span><span class="sxs-lookup"><span data-stu-id="8df16-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8df16-183">Notificaciones de inserción de orden tooreceive, debe configurar una cuenta de Google en el dispositivo Virtual Android.</span><span class="sxs-lookup"><span data-stu-id="8df16-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="8df16-184">(En el emulador de Windows hello, navegue demasiado**configuración** y haga clic en **Agregar cuenta**.) Además, asegúrese de que ese emulador hello es toohello conectado Internet.</span><span class="sxs-lookup"><span data-stu-id="8df16-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="8df16-185">El diseño de notificaciones en Android versión 5.0 y posteriores representa un cambio significativo respecto al de las versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="8df16-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="8df16-186">Para más información, consulte [Notificaciones de Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="8df16-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="8df16-187">En **Tools** (Herramientas), haga clic en **Open Android Emulator Manager** (Abrir Administrador de emulador Android), seleccione su dispositivo y, a continuación, haga clic en **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="8df16-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="8df16-188">Seleccione **API de Google** en **Destino** y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8df16-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="8df16-189">En la barra de herramientas superior hello, haga clic en **ejecutar**y, a continuación, seleccione la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8df16-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="8df16-190">Esto inicia el emulador de Hola y ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8df16-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="8df16-191">aplicación Hello recupera hello *registrationId* de GCM y se registra con el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="8df16-192">Envío de notificaciones desde su backend</span><span class="sxs-lookup"><span data-stu-id="8df16-192">Send notifications from your backend</span></span>
<span data-ttu-id="8df16-193">Puede probar recibir notificaciones en la aplicación mediante el envío de notificaciones en hello [Portal clásico de Azure] a través de hello depurar pestaña en el centro de notificaciones de hello, como se muestra en la siguiente pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="8df16-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="8df16-194">Las notificaciones push se envían normalmente en un servicio back-end como Servicios móviles o ASP.NET mediante una biblioteca compatible.</span><span class="sxs-lookup"><span data-stu-id="8df16-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="8df16-195">También puede utilizar Hola API de REST directamente si una biblioteca no está disponible para el back-end de los mensajes de notificación toosend.</span><span class="sxs-lookup"><span data-stu-id="8df16-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="8df16-196">Esta es una lista de algunos otros tutoriales que puede que desee tooreview para enviar notificaciones:</span><span class="sxs-lookup"><span data-stu-id="8df16-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="8df16-197">ASP.NET: Vea [toousers de notificaciones de los centros de notificaciones de uso toopush].</span><span class="sxs-lookup"><span data-stu-id="8df16-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="8df16-198">Java de bases de datos centrales de notificación Azure SDK: vea [cómo toouse centros de notificaciones desde Java](notification-hubs-java-push-notification-tutorial.md) para enviar notificaciones de Java.</span><span class="sxs-lookup"><span data-stu-id="8df16-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="8df16-199">Esto se probó en Eclipse para el desarrollo de Android.</span><span class="sxs-lookup"><span data-stu-id="8df16-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="8df16-200">PHP: Vea [cómo toouse centros de notificaciones de PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8df16-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="8df16-201">En las subsecciones siguientes de Hola de tutorial de hello, enviar notificaciones mediante el uso de una aplicación de consola .NET y mediante el uso de un servicio móvil a través de una secuencia de comandos de nodo.</span><span class="sxs-lookup"><span data-stu-id="8df16-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="8df16-202">Envío de notificaciones mediante una aplicación .NET (opcional)</span><span class="sxs-lookup"><span data-stu-id="8df16-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="8df16-203">En esta sección enviará notificaciones con una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="8df16-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="8df16-204">Cree una aplicación de consola nueva de Visual C#:</span><span class="sxs-lookup"><span data-stu-id="8df16-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="8df16-205">En Visual Studio, haga clic en **Herramientas**, **Administrador de paquetes NuGet** y, después, en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="8df16-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="8df16-206">Esto muestra hello consola de administrador de paquetes en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8df16-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="8df16-207">En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8df16-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="8df16-208">Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="8df16-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="8df16-209">Abra el archivo Program.cs de hello y agregue Hola siguiente `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="8df16-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="8df16-210">En su `Program` clase, agregue Hola siguiendo el método.</span><span class="sxs-lookup"><span data-stu-id="8df16-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="8df16-211">Actualizar el texto de marcador de posición de hello con su *DefaultFullSharedAccessSignature* nombre de concentrador y la cadena de conexión de hello [Portal clásico de Azure].</span><span class="sxs-lookup"><span data-stu-id="8df16-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="8df16-212">Agregar Hola siguiendo las líneas en el **Main** método:</span><span class="sxs-lookup"><span data-stu-id="8df16-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="8df16-213">Presione aplicación Hola de hello F5 toorun clave.</span><span class="sxs-lookup"><span data-stu-id="8df16-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="8df16-214">Debería recibir una notificación en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8df16-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="8df16-215">Envío de notificaciones mediante un servicio móvil (opcional)</span><span class="sxs-lookup"><span data-stu-id="8df16-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="8df16-216">Siga [Introducción a Servicios móviles].</span><span class="sxs-lookup"><span data-stu-id="8df16-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="8df16-217">Inicie sesión en toohello [Portal clásico de Azure]y seleccione su servicio móvil.</span><span class="sxs-lookup"><span data-stu-id="8df16-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="8df16-218">Seleccione hello **programador** ficha en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="8df16-219">Cree un nuevo trabajo programado, inserte un nombre y seleccione **A petición**.</span><span class="sxs-lookup"><span data-stu-id="8df16-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="8df16-220">Cuando se crea el trabajo de hello, haga clic en el nombre del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="8df16-221">A continuación, haga clic en hello **Script** ficha en la barra superior Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="8df16-222">Inserte la siguiente secuencia de comandos dentro de la función de programador de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="8df16-223">Asegúrese de los marcadores de posición hello tooreplace seguro con la notificación concentrador hello y nombre de cadena de conexión para *DefaultFullSharedAccessSignature* que ha obtenido antes.</span><span class="sxs-lookup"><span data-stu-id="8df16-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="8df16-224">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8df16-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="8df16-225">Haga clic en **ejecutar una vez** en la barra de la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8df16-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="8df16-226">Debería recibir una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="8df16-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8df16-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8df16-227">Next steps</span></span>
<span data-ttu-id="8df16-228">En este sencillo ejemplo, difunden notificaciones tooall sus dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="8df16-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="8df16-229">En el orden tootarget a usuarios específicos, consulte tutorial toohello [toousers de notificaciones de los centros de notificaciones de uso toopush].</span><span class="sxs-lookup"><span data-stu-id="8df16-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="8df16-230">Si desea que toosegment los usuarios por grupos de interés, puede leer [toosend de centros de notificaciones utilice noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="8df16-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="8df16-231">Más información acerca de cómo toouse centros de notificaciones de [Guía de centros de notificaciones] y Hola [centros de notificaciones toofor cómo Android].</span><span class="sxs-lookup"><span data-stu-id="8df16-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Introducción a Servicios móviles]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Portal clásico de Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Guía de centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx
[centros de notificaciones toofor cómo Android]: http://msdn.microsoft.com/library/dn282661.aspx

[toousers de notificaciones de los centros de notificaciones de uso toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de centros de notificaciones utilice noticias de última hora]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Componente del Cliente de mensajería en la nube de Google]: http://components.xamarin.com/view/GCMClient/
[Componente de mensajería de Azure]: http://components.xamarin.com/view/azure-messaging
