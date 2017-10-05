---
title: "Inserción segura de los Centros de notificaciones de Azure"
description: "Obtenga información acerca de cómo enviar notificaciones de inserción seguras en Azure. Ejemplos de código escritos en C# con la API de .NET."
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
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="fd64f-104">Inserción segura de los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="fd64f-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd64f-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="fd64f-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="fd64f-106">iOS</span><span class="sxs-lookup"><span data-stu-id="fd64f-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="fd64f-107">Android</span><span class="sxs-lookup"><span data-stu-id="fd64f-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="fd64f-108">Información general</span><span class="sxs-lookup"><span data-stu-id="fd64f-108">Overview</span></span>
<span data-ttu-id="fd64f-109">La compatibilidad con las notificaciones push en Microsoft Azure le permite tener acceso a una infraestructura multiplataforma y de escalamiento horizontal fácil de usar, que simplifica considerablemente la implementación de notificaciones push tanto en aplicaciones de consumidor como en aplicaciones empresariales para plataformas móviles.</span><span class="sxs-lookup"><span data-stu-id="fd64f-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="fd64f-110">Debido a restricciones reguladoras o de seguridad, algunas veces una aplicación podría querer incluir algo en la notificación que no se puede trasmitir a través de la infraestructura de las notificaciones de inserción estándar.</span><span class="sxs-lookup"><span data-stu-id="fd64f-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="fd64f-111">En este tutorial se describe cómo lograr la misma experiencia enviando información importante a través de una conexión segura y autenticada entre el dispositivo cliente y el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd64f-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="fd64f-112">A un alto nivel, el flujo es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd64f-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="fd64f-113">El back-end de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="fd64f-113">The app back-end:</span></span>
   * <span data-ttu-id="fd64f-114">Almacena la carga segura en la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="fd64f-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="fd64f-115">Envía el identificador de esta notificación al dispositivo (no se envía información segura).</span><span class="sxs-lookup"><span data-stu-id="fd64f-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="fd64f-116">La aplicación del dispositivo, cuando recibe la información:</span><span class="sxs-lookup"><span data-stu-id="fd64f-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="fd64f-117">El dispositivo entra en contacto con el back-end que solicita la carga segura.</span><span class="sxs-lookup"><span data-stu-id="fd64f-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="fd64f-118">La aplicación puede mostrar la carga como una notificación en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fd64f-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="fd64f-119">Es importante tener en cuenta que en el flujo anterior (y en este tutorial), asumimos que el dispositivo almacena un token de autenticación localmente y, después, el usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="fd64f-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="fd64f-120">Esto garantiza una experiencia sin ningún problema, ya que el dispositivo puede recuperar la carga segura de la notificación usando este token.</span><span class="sxs-lookup"><span data-stu-id="fd64f-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="fd64f-121">Si la aplicación no almacena tokens de autenticación en el dispositivo, o si estos tokens han expirado, la aplicación del dispositivo, al recibir la notificación, debe mostrar una notificación genérica pidiendo al usuario que inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd64f-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="fd64f-122">Después, la aplicación autentica al usuario y muestra la carga de la notificación.</span><span class="sxs-lookup"><span data-stu-id="fd64f-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="fd64f-123">Este tutorial Inserción segura muestra cómo enviar una notificación de inserción de forma segura.</span><span class="sxs-lookup"><span data-stu-id="fd64f-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="fd64f-124">El tutorial se basa en el tutorial [Notificar a los usuarios](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) , por lo que debe completar los pasos de ese tutorial primero.</span><span class="sxs-lookup"><span data-stu-id="fd64f-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="fd64f-125">En este tutorial se supone que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (Tienda Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="fd64f-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="fd64f-126">Asimismo, tenga en cuenta que Windows Phone 8.1 requiere credenciales de Windows (no de Windows Phone) y que las tareas en segundo plano no funcionan en Windows Phone 8.0 o Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="fd64f-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="fd64f-127">Para aplicaciones de la Tienda Windows, puede recibir notificaciones a través de una tarea en segundo plano solamente si la aplicación tiene la pantalla de bloqueo habilitada (haga clic en la casilla en el manifiesto de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="fd64f-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="fd64f-128">Modificación del proyecto de Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fd64f-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="fd64f-129">En el proyecto **NotifyUserWindowsPhone** , agregue el siguiente código a App.xaml.cs para registrar la tarea de segundo plano de inserción.</span><span class="sxs-lookup"><span data-stu-id="fd64f-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="fd64f-130">Agregue la siguiente línea de código al final del método `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="fd64f-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="fd64f-131">Todavía en App.xaml.cs, agregue el siguiente código inmediatamente después del método `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="fd64f-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="fd64f-132">Agregue las siguientes instrucciones `using` en la parte superior del archivo App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="fd64f-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="fd64f-133">En el menú **Archivo** de Visual Studio, haga clic en **Guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="fd64f-134">Creación del componente de segundo plano de inserción</span><span class="sxs-lookup"><span data-stu-id="fd64f-134">Create the Push Background Component</span></span>
<span data-ttu-id="fd64f-135">El paso siguiente es crear el componente de segundo plano de inserción.</span><span class="sxs-lookup"><span data-stu-id="fd64f-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="fd64f-136">En el Explorador de soluciones, haga clic con el botón derecho en el nodo de nivel superior de la solución (en este caso, **Solución SecurePush**), haga clic en **Agregar** y, después, haga clic en **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="fd64f-137">Expanda **Aplicaciones de la Tienda**, haga clic en **Aplicaciones de Windows Phone** y, después, en **Componente de Windows Runtime (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="fd64f-138">Asigne al proyecto el nombre **PushBackgroundComponent** y, después, haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="fd64f-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="fd64f-139">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **PushBackgroundComponent (Windows Phone 8.1)**, haga clic en **Agregar** y, después, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="fd64f-140">Asigne un nombre a la nueva clase **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="fd64f-141">Haga clic en **Agregar** para generar la clase.</span><span class="sxs-lookup"><span data-stu-id="fd64f-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="fd64f-142">Reemplace todo el contenido de la definición del espacio de nombres **PushBackgroundComponent** por el código siguiente, reemplazando el marcador de posición `{back-end endpoint}` por el punto de conexión de back-end obtenido al implementar el back-end:</span><span class="sxs-lookup"><span data-stu-id="fd64f-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store the content received from the notification so it can be retrieved from the UI.
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
5. <span data-ttu-id="fd64f-143">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **PushBackgroundComponent (Windows Phone 8.1)** y, después, seleccione **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="fd64f-144">A la izquierda, haga clic en **En línea**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="fd64f-145">En el cuadro **Buscar**, escriba **Cliente http**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="fd64f-146">En la lista de resultados, haga clic en **Bibliotecas de cliente HTTP de Microsoft** y, a continuación, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="fd64f-147">Complete la instalación.</span><span class="sxs-lookup"><span data-stu-id="fd64f-147">Complete the installation.</span></span>
9. <span data-ttu-id="fd64f-148">Nuevamente en el cuadro **Buscar** de NuGet, escriba **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="fd64f-149">Instale el paquete **Json.NET** y cierre la ventana Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd64f-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="fd64f-150">Agregue las siguientes instrucciones `using` en la parte superior del archivo **PushBackgroundTask.cs** :</span><span class="sxs-lookup"><span data-stu-id="fd64f-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="fd64f-151">En el Explorador de soluciones, en el proyecto **NotifyUserWindowsPhone (Windows Phone 8.1)**, haga clic con el botón derecho en **Referencias** y, después, haga clic en **Agregar referencia…**</span><span class="sxs-lookup"><span data-stu-id="fd64f-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="fd64f-152">En el diálogo Administrador de referencias, active la casilla junto a **PushBackgroundComponent** y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="fd64f-153">En el Explorador de soluciones, haga doble clic en **Package.appxmanifest** en el proyecto **NotifyUserWindowsPhone (Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="fd64f-154">En **Notificaciones**, establezca la opción **Capacidad de aviso** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="fd64f-155">Sin salir de **Package.appxmanifest**, haga clic en el menú **Declaraciones** cerca de la parte superior.</span><span class="sxs-lookup"><span data-stu-id="fd64f-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="fd64f-156">En el cuadro desplegable **Declaraciones disponibles**, haga clic en **Tareas en segundo plano** y, después, en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="fd64f-157">En **Package.appxmanifest**, en **Propiedades**, active **Notificación de inserción**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="fd64f-158">En **Package.appxmanifest**, en **Configuración de la aplicación**, escriba **PushBackgroundComponent.PushBackgroundTask** en el campo **Punto de entrada**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="fd64f-159">En el menú **Archivo**, haga clic en **Guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="fd64f-160">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fd64f-160">Run the Application</span></span>
<span data-ttu-id="fd64f-161">Para ejecutar la aplicación, realice las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="fd64f-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="fd64f-162">En Visual Studio, ejecute la aplicación Web API **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="fd64f-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="fd64f-163">Se mostrará una página web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fd64f-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="fd64f-164">En Visual Studio, ejecute la aplicación de Windows Phone **NotifyUserWindowsPhone (Windows Phone 8.1)** .</span><span class="sxs-lookup"><span data-stu-id="fd64f-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="fd64f-165">El emulador de Windows Phone se ejecuta y carga la aplicación automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fd64f-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="fd64f-166">En la interfaz de usuario de la aplicación **NotifyUserWindowsPhone** , escriba un nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="fd64f-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="fd64f-167">Esta información puede ser cualquier cadena, pero deben tener el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="fd64f-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="fd64f-168">En la interfaz de usuario de la aplicación **NotifyUserWindowsPhone**, haga clic en **Iniciar sesión y registrarse**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="fd64f-169">A continuación, haga clic en **Enviar inserción**.</span><span class="sxs-lookup"><span data-stu-id="fd64f-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
