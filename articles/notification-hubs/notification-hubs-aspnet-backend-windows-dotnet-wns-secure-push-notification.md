---
title: "aaaAzure notificación concentradores seguros Push"
description: "Obtenga información acerca de cómo toosend segura las notificaciones de inserción en Azure. Ejemplos de código escritos en C# mediante Hola .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="31ebf-104">Inserción segura de los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="31ebf-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31ebf-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="31ebf-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="31ebf-106">iOS</span><span class="sxs-lookup"><span data-stu-id="31ebf-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="31ebf-107">Android</span><span class="sxs-lookup"><span data-stu-id="31ebf-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="31ebf-108">Información general</span><span class="sxs-lookup"><span data-stu-id="31ebf-108">Overview</span></span>
<span data-ttu-id="31ebf-109">Compatibilidad con notificaciones de inserción de Microsoft Azure le permite tooaccess una infraestructura de inserción fácil de usar, varias plataformas y escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas.</span><span class="sxs-lookup"><span data-stu-id="31ebf-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="31ebf-110">A veces debido a restricciones de seguridad o tooregulatory, una aplicación podría querer tooinclude algo en la notificación de Hola que no se transmiten a través de la infraestructura de notificaciones de inserción estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="31ebf-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="31ebf-111">Este tutorial describe cómo tooachieve Hola misma experiencia mediante el envío de información confidencial a través de una conexión segura autenticada entre el dispositivo de cliente de Hola y Hola backend de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31ebf-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="31ebf-112">En un nivel alto, flujo de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="31ebf-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="31ebf-113">Hola aplicación back-end:</span><span class="sxs-lookup"><span data-stu-id="31ebf-113">hello app back-end:</span></span>
   * <span data-ttu-id="31ebf-114">Almacena la carga segura en la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="31ebf-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="31ebf-115">Envía el Id. de Hola de este dispositivo de toohello de notificación (se envía ninguna información segura).</span><span class="sxs-lookup"><span data-stu-id="31ebf-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="31ebf-116">aplicación Hello en dispositivo hello, al recibir la notificación de hello:</span><span class="sxs-lookup"><span data-stu-id="31ebf-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="31ebf-117">dispositivo de Hello contacta con hello back-end que lo solicita Hola carga de seguridad.</span><span class="sxs-lookup"><span data-stu-id="31ebf-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="31ebf-118">aplicación Hello puede mostrar carga hello como una notificación en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31ebf-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="31ebf-119">Es importante toonote que Hola anterior flujo (y en este tutorial), se da por supuesto ese dispositivo Hola almacena un token de autenticación en el almacenamiento local, después de hello usuario inicia sesión en.</span><span class="sxs-lookup"><span data-stu-id="31ebf-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="31ebf-120">Esto garantiza una experiencia completamente sin problemas, como dispositivo de hello puede recuperar la carga de seguridad de la notificación de hello con este token.</span><span class="sxs-lookup"><span data-stu-id="31ebf-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="31ebf-121">Si la aplicación no almacena tokens de autenticación en el dispositivo de hello, o si pueden haber expirado estos tokens, hello del dispositivo, tras recibir la notificación de Hola debe mostrar una notificación genérica preguntar aplicación Hola de hello usuario toolaunch.</span><span class="sxs-lookup"><span data-stu-id="31ebf-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="31ebf-122">aplicación Hello, a continuación, autentica el usuario de Hola y muestra la carga de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="31ebf-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="31ebf-123">Este tutorial de inserción seguros se muestra cómo toosend una notificación de inserción de forma segura.</span><span class="sxs-lookup"><span data-stu-id="31ebf-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="31ebf-124">tutorial de Hola se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, por lo que debe completar los pasos de hello en ese tutorial primero.</span><span class="sxs-lookup"><span data-stu-id="31ebf-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="31ebf-125">En este tutorial se supone que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (Tienda Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="31ebf-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="31ebf-126">Asimismo, tenga en cuenta que Windows Phone 8.1 requiere credenciales de Windows (no de Windows Phone) y que las tareas en segundo plano no funcionan en Windows Phone 8.0 o Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="31ebf-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="31ebf-127">Para las aplicaciones de la tienda Windows, puede recibir notificaciones a través de una tarea en segundo plano únicamente si la aplicación hello está habilitada la pantalla de bloqueo (haga clic en la casilla de verificación de Hola Hola Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="31ebf-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="31ebf-128">Modificar Hola proyecto de Windows Phone</span><span class="sxs-lookup"><span data-stu-id="31ebf-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="31ebf-129">Hola **NotifyUserWindowsPhone** proyecto de equipo y agregar Hola después de la tarea en segundo plano código tooApp.xaml.cs tooregister Hola inserción.</span><span class="sxs-lookup"><span data-stu-id="31ebf-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="31ebf-130">Agregar Hola después de la línea de código al final de Hola de hello `OnLaunched()` método:</span><span class="sxs-lookup"><span data-stu-id="31ebf-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="31ebf-131">Todavía en App.xaml.cs, agregue Hola siguiente código inmediatamente después de hello `OnLaunched()` método:</span><span class="sxs-lookup"><span data-stu-id="31ebf-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="31ebf-132">Agregue los siguiente hello `using` instrucciones en parte superior de hello del archivo de hello App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="31ebf-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="31ebf-133">De hello **archivo** menú en Visual Studio, haga clic en **guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="31ebf-134">Crear hello Push componente en segundo plano</span><span class="sxs-lookup"><span data-stu-id="31ebf-134">Create hello Push Background Component</span></span>
<span data-ttu-id="31ebf-135">Hola siguiente paso es el componente de segundo plano de inserción de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="31ebf-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="31ebf-136">En el Explorador de soluciones, haga clic en el nodo de nivel superior de Hola de solución de Hola (**SecurePush de solución** en este caso), a continuación, haga clic en **agregar**, a continuación, haga clic en **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="31ebf-137">Expanda **Aplicaciones de la Tienda**, haga clic en **Aplicaciones de Windows Phone** y, después, en **Componente de Windows Runtime (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="31ebf-138">Proyecto de hello Name **PushBackgroundComponent**y, a continuación, haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="31ebf-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="31ebf-139">En el Explorador de soluciones, haga clic en hello **PushBackgroundComponent (Windows Phone 8.1)** proyecto, a continuación, haga clic en **agregar**, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="31ebf-140">Hola nueva clase el nombre **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="31ebf-141">Haga clic en **agregar** clase de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="31ebf-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="31ebf-142">Reemplace todo contenido de Hola de hello **PushBackgroundComponent** definición de espacio de nombres con hello siguiente código, sustituyendo el marcador de posición de hello `{back-end endpoint}` con punto de conexión de back-end de hello obtenido durante la implementación de su back-end:</span><span class="sxs-lookup"><span data-stu-id="31ebf-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="31ebf-143">En el Explorador de soluciones, haga clic en hello **PushBackgroundComponent (Windows Phone 8.1)** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="31ebf-144">En el lado izquierdo de hello, haga clic en **Online**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="31ebf-145">Hola **búsqueda** , escriba **cliente Http**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="31ebf-146">En la lista de resultados de hello, haga clic en **Microsoft HTTP Client Libraries**y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="31ebf-147">Completar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="31ebf-147">Complete hello installation.</span></span>
9. <span data-ttu-id="31ebf-148">Nuevo en hello NuGet **búsqueda** , escriba **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="31ebf-149">Instalar hello **Json.NET** paquete y, a continuación, ventana de administrador de paquetes de NuGet de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="31ebf-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="31ebf-150">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **PushBackgroundTask.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="31ebf-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="31ebf-151">En el Explorador de soluciones, en hello **NotifyUserWindowsPhone (Windows Phone 8.1)** proyecto de equipo y haga clic en **referencias**, a continuación, haga clic en **Agregar referencia...** . Cuadro de diálogo Administrador de referencias de hello, casilla Hola junto demasiado**PushBackgroundComponent**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="31ebf-152">En el Explorador de soluciones, haga doble clic en **Package.appxmanifest** en hello **NotifyUserWindowsPhone (Windows Phone 8.1)** proyecto.</span><span class="sxs-lookup"><span data-stu-id="31ebf-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="31ebf-153">En **notificaciones**, establezca **capaz de recibir** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="31ebf-154">Todavía en **Package.appxmanifest**, haga clic en hello **declaraciones** menú cerca de la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="31ebf-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="31ebf-155">Hola **declaraciones disponibles** de lista desplegable, haga clic en **tareas en segundo plano**y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="31ebf-156">En **Package.appxmanifest**, en **Propiedades**, active **Notificación de inserción**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="31ebf-157">En **Package.appxmanifest**, en **configuración de la aplicación**, tipo **PushBackgroundComponent.PushBackgroundTask** en hello **punto de entrada** campo.</span><span class="sxs-lookup"><span data-stu-id="31ebf-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="31ebf-158">De hello **archivo** menú, haga clic en **guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="31ebf-159">Ejecutar aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="31ebf-159">Run hello Application</span></span>
<span data-ttu-id="31ebf-160">toorun Hola aplicación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="31ebf-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="31ebf-161">En Visual Studio, ejecute hello **AppBackend** aplicación de API Web.</span><span class="sxs-lookup"><span data-stu-id="31ebf-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="31ebf-162">Se mostrará una página web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="31ebf-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="31ebf-163">En Visual Studio, ejecute hello **NotifyUserWindowsPhone (Windows Phone 8.1)** aplicación de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="31ebf-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="31ebf-164">emulador de Windows Phone Hola se ejecuta y carga la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="31ebf-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="31ebf-165">Hola **NotifyUserWindowsPhone** aplicación interfaz de usuario, escriba un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="31ebf-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="31ebf-166">Pueden ser cualquier cadena, pero deben ser Hola el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="31ebf-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="31ebf-167">Hola **NotifyUserWindowsPhone** aplicación interfaz de usuario, haga clic en **iniciar sesión y registrar**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="31ebf-168">A continuación, haga clic en **Enviar inserción**.</span><span class="sxs-lookup"><span data-stu-id="31ebf-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
