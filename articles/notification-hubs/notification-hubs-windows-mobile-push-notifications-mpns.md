---
title: "notificaciones de inserción de aaaSending con centros de notificaciones de Azure en Windows Phone | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo las notificaciones de toouse centros de notificaciones de Azure toopush tooa Windows Phone 8 o una aplicación de Silverlight de Windows Phone 8.1."
services: notification-hubs
documentationcenter: windows
keywords: "notificación push, notificación push, notificación push de windows phone"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="33380-104">Envío de notificaciones push con los Centros de notificaciones de Azure en Windows Phone</span><span class="sxs-lookup"><span data-stu-id="33380-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="33380-105">Información general</span><span class="sxs-lookup"><span data-stu-id="33380-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="33380-106">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="33380-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="33380-107">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="33380-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="33380-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="33380-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="33380-109">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend aplicación de Windows Phone 8 o Windows Phone 8.1 Silverlight tooa notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="33380-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="33380-110">Si desea usar Windows Phone 8.1 (no de Silverlight), a continuación, consulte toohello [universales de Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versión.</span><span class="sxs-lookup"><span data-stu-id="33380-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="33380-111">En este tutorial, creará una aplicación de Windows Phone 8 en blanco que recibe notificaciones de inserción mediante Hola servicio de notificaciones de inserción de Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="33380-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="33380-112">Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33380-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="33380-113">Hola notificación centros de Windows Phone SDK no admite el uso de hello servicios de notificación de inserción de Windows (WNS) con aplicaciones de Silverlight de Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="33380-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="33380-114">toouse WNS (en lugar de MPNS) con aplicaciones de Silverlight de Windows Phone 8.1, siga hello [centros de notificaciones: tutorial de Windows Phone Silverlight], que usa las API de REST.</span><span class="sxs-lookup"><span data-stu-id="33380-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="33380-115">tutorial de Hello muestra el escenario sencillo de difusión hello en usar centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="33380-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33380-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="33380-116">Prerequisites</span></span>
<span data-ttu-id="33380-117">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="33380-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="33380-118">[Visual Studio 2012 Express para Windows Phone], o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="33380-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="33380-119">La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones de Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="33380-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="33380-120">Creación de su centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="33380-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="33380-121">Haga clic en hello <b>Notification Services</b> sección (dentro de <i>configuración</i>), haga clic en <b>Windows Phone (MPNS)</b> y, a continuación, haga clic en hello <b>Habilitar inserción no autenticadas </b> casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="33380-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portal de Azure: Habilitación de notificaciones push sin autenticar.](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="33380-123">El concentrador ahora es notificación creada y configurada toosend no autenticado de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="33380-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="33380-124">Este tutorial usa MPNS en modo sin autenticar.</span><span class="sxs-lookup"><span data-stu-id="33380-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="33380-125">Modo MPNS no autenticado incluye restricciones en las notificaciones que puede enviar tooeach canal.</span><span class="sxs-lookup"><span data-stu-id="33380-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="33380-126">Es compatible con los centros de notificaciones [MPNS autenticado modo](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) permitiéndole tooupload su certificado.</span><span class="sxs-lookup"><span data-stu-id="33380-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="33380-127">Conectar el centro de notificaciones de toohello de aplicación</span><span class="sxs-lookup"><span data-stu-id="33380-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="33380-128">En Visual Studio, cree una aplicación nueva de Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="33380-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="33380-129">En Visual Studio 2013 Update 2 o versiones posteriores, cree en su lugar una aplicación Silverlight de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="33380-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio, nuevo proyecto, aplicación vacía, Windows Phone Silverlight][11]
2. <span data-ttu-id="33380-131">En Visual Studio, haga clic en soluciones de hello y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="33380-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="33380-132">Esto muestra hello **administrar paquetes de NuGet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33380-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="33380-133">Busque `WindowsAzure.Messaging.Managed` y haga clic en **instalar**y, a continuación, acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="33380-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio, Administrador de paquetes NuGet][20]
   
    <span data-ttu-id="33380-135">Esto descarga, se instala y se agrega una biblioteca de referencia para la mensajería de Azure de toohello para Windows mediante el uso de Hola <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">paquete WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="33380-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="33380-136">Abra el archivo hello App.xaml.cs y agregue Hola siguiente `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="33380-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="33380-137">Agregar Hola siguiente código en la parte superior de Hola de **Application_Launching** método en App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="33380-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="33380-138">Hola valor **MyPushChannel** es un índice que está toolookup usa un canal existente en hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) colección.</span><span class="sxs-lookup"><span data-stu-id="33380-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="33380-139">Si no hay uno ya allí, cree una nueva entrada con ese nombre.</span><span class="sxs-lookup"><span data-stu-id="33380-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="33380-140">Asegúrese de que tooinsert Hola nombre de la cadena de conexión de concentrador y Hola llamada **DefaultListenSharedAccessSignature** que obtuvo en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="33380-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="33380-141">Este código recupera el URI del canal de hello para la aplicación hello de MPNS y, a continuación, registra ese URI del canal con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="33380-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="33380-142">También se garantiza que ese canal Hola que URI está registrado en el centro de notificaciones que se inicia cada aplicación Hola de tiempo.</span><span class="sxs-lookup"><span data-stu-id="33380-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="33380-143">Este tutorial, envía un dispositivo de toohello de notificación de notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="33380-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="33380-144">Cuando se envía una notificación de mosaico, en su lugar, debe llamar a hello **BindToShellTile** método en el canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="33380-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="33380-145">toosupport notificaciones notificaciones del sistema y el icono, llame a ambos **BindToShellTile** y **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="33380-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="33380-146">En el Explorador de soluciones, expanda **propiedades**, abra hello `WMAppManifest.xml` de archivos, haga clic en hello **capacidades** pestaña y asegúrese de que ese hello **ID_CAP_PUSH_NOTIFICATION** se comprueba la capacidad.</span><span class="sxs-lookup"><span data-stu-id="33380-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="33380-147">Hola presione `F5` toorun clave Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="33380-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="33380-148">Se muestra un mensaje de registro en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="33380-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="33380-149">Aplicación de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="33380-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="33380-150">tooreceive una notificación de inserción del sistema, aplicación hello no debe disponer en primer plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="33380-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="33380-151">Envío de notificaciones push desde su backend</span><span class="sxs-lookup"><span data-stu-id="33380-151">Send push notifications from your backend</span></span>
<span data-ttu-id="33380-152">Puede enviar notificaciones de inserción con centros de notificaciones desde cualquier back-end a través de hello público <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaz REST</a>.</span><span class="sxs-lookup"><span data-stu-id="33380-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="33380-153">En este tutorial, enviará notificaciones push con una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="33380-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="33380-154">Para obtener un ejemplo de cómo toosend notificaciones de inserción desde un back-end de WebAPI de ASP.NET que se integra con centros de notificaciones, consulte [Azure notificación centros de informar a los usuarios con back-end de .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="33380-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="33380-155">Para obtener un ejemplo de cómo las notificaciones de inserción de toosend mediante el uso de Hola [API de REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), visite [cómo toouse centros de notificaciones de Java](notification-hubs-java-push-notification-tutorial.md) y [cómo toouse centros de notificaciones de PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="33380-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="33380-156">Solución de Hola de menú contextual, seleccione **agregar** y **nuevo proyecto...** y, a continuación, en **Visual C#**, haga clic en **Windows** y **aplicación de consola**y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="33380-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="33380-157">Esto agrega una nueva solución de toohello para aplicaciones de Visual C# consola.</span><span class="sxs-lookup"><span data-stu-id="33380-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="33380-158">También puede hacer esto en una solución separada.</span><span class="sxs-lookup"><span data-stu-id="33380-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="33380-159">Haga clic en **Herramientas**, **Administrador de paquetes de biblioteca** y **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="33380-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="33380-160">Esto muestra hello Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="33380-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="33380-161">Hola **Package Manager Console** (ventana), conjunto hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="33380-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="33380-162">Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="33380-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="33380-163">Abra hello `Program.cs` de archivos y agregue Hola siguiente `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="33380-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="33380-164">Hola `Program` clase, agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="33380-164">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="33380-165">Realizar seguro hello tooreplace `<hub name>` marcador de posición con nombre de hello del centro de notificaciones de Hola que aparece en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="33380-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="33380-166">También, Reemplazar marcador de posición de cadena de conexión de hello con cadena de conexión de hello llama **DefaultFullSharedAccessSignature** que obtuvo en la sección de Hola "Configurar el centro de notificaciones".</span><span class="sxs-lookup"><span data-stu-id="33380-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="33380-167">Asegúrese de que usar cadena de conexión de hello con **completa** acceso, no **escuchar** acceso.</span><span class="sxs-lookup"><span data-stu-id="33380-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="33380-168">cadena de acceso de la escucha de Hello no tiene las notificaciones de inserción de toosend de permisos.</span><span class="sxs-lookup"><span data-stu-id="33380-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="33380-169">Agregar Hola línea siguiente en su `Main` método:</span><span class="sxs-lookup"><span data-stu-id="33380-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="33380-170">Con su Windows Phone emulador que se ejecuta y el proyecto de aplicación de consola de aplicación Hola cerrado, establezca como Hola predeterminado el proyecto de inicio y, a continuación, presione hello `F5` toorun clave Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="33380-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="33380-171">Recibirá una notificación push del sistema.</span><span class="sxs-lookup"><span data-stu-id="33380-171">You will receive a toast push notification.</span></span> <span data-ttu-id="33380-172">Al puntear en banner de notificación de hello carga la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="33380-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="33380-173">Puede encontrar todas las cargas posibles Hola Hola [catálogo del sistema] y [catálogo iconos] temas en MSDN.</span><span class="sxs-lookup"><span data-stu-id="33380-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33380-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33380-174">Next steps</span></span>
<span data-ttu-id="33380-175">En este sencillo ejemplo, difunden tooall de notificaciones de inserción los dispositivos Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="33380-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="33380-176">En el orden tootarget a usuarios específicos, consulte toohello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial.</span><span class="sxs-lookup"><span data-stu-id="33380-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="33380-177">Si desea que toosegment los usuarios por grupos de interés, puede leer [toosend de centros de notificaciones utilice noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="33380-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="33380-178">Más información acerca de cómo toouse centros de notificaciones de [instrucciones de los centros de notificación].</span><span class="sxs-lookup"><span data-stu-id="33380-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express para Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[instrucciones de los centros de notificación]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[toousers de notificaciones de los centros de notificaciones de uso toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catálogo del sistema]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[catálogo iconos]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[centros de notificaciones: tutorial de Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

