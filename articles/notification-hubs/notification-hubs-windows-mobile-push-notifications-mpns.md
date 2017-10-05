---
title: "Envío de notificaciones push con los Azure Notification Hubs en Windows Phone | Microsoft Docs"
description: "En este tutorial aprenderá a usar Centros de notificaciones de Azure para enviar notificaciones push a aplicaciones Windows Phone 8 o Windows Phone 8.1 Silverlight."
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
ms.openlocfilehash: f0bfe81f849813d146d644b32490af657b1071b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="18768-104">Envío de notificaciones push con los Centros de notificaciones de Azure en Windows Phone</span><span class="sxs-lookup"><span data-stu-id="18768-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="18768-105">Información general</span><span class="sxs-lookup"><span data-stu-id="18768-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="18768-106">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="18768-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="18768-107">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="18768-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="18768-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="18768-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="18768-109">Este tutorial muestra cómo puede usar Centros de notificaciones de Azure para enviar notificaciones push a aplicaciones Windows Phone 8 o Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="18768-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="18768-110">Si va a desarrollar para Windows Phone 8.1 (no Silverlight), consulte entonces la versión [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="18768-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="18768-111">En este tutorial puede crear una aplicación de Windows Phone 8 vacía que recibe notificaciones push mediante el Servicio de notificaciones de inserción de Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="18768-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="18768-112">Cuando haya finalizado, podrá usar el centro de notificaciones para difundir notificaciones push a todos los dispositivos que ejecutan su aplicación.</span><span class="sxs-lookup"><span data-stu-id="18768-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="18768-113">El SDK de Windows Phone para Centros de notificaciones no admite el uso de Servicios de notificaciones de inserción de Windows (WNS) con aplicaciones de Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="18768-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="18768-114">Para usar WNS (en lugar de MPNS) con aplicaciones de Windows Phone 8.1 Silverlight, siga el [tutorial Centros de notificaciones: Windows Phone Silverlight], que usa API de REST.</span><span class="sxs-lookup"><span data-stu-id="18768-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="18768-115">En este tutorial se demuestra el escenario de difusión sencillo con centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="18768-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18768-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18768-116">Prerequisites</span></span>
<span data-ttu-id="18768-117">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="18768-117">This tutorial requires the following:</span></span>

* <span data-ttu-id="18768-118">[Visual Studio 2012 Express para Windows Phone], o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="18768-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="18768-119">La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones de Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="18768-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="18768-120">Creación de su centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="18768-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="18768-121">Haga clic en la sección <b>Servicios de notificaciones</b> (en <i>Configuración</i>), haga clic en <b>Windows Phone (MPNS)</b> y, después, en la casilla <b>Habilitar notificaciones de inserción sin autenticar</b>.</span><span class="sxs-lookup"><span data-stu-id="18768-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portal de Azure: Habilitación de notificaciones push sin autenticar.](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="18768-123">El concentrador se crea y configura ahora para enviar una notificación sin autenticar para Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="18768-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="18768-124">Este tutorial usa MPNS en modo sin autenticar.</span><span class="sxs-lookup"><span data-stu-id="18768-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="18768-125">El modo sin autenticar de MPNS viene con restricciones sobre las notificaciones que puede enviar a cada canal.</span><span class="sxs-lookup"><span data-stu-id="18768-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span></span> <span data-ttu-id="18768-126">Los Centros de notificaciones admiten el [modo autenticado de MPNS](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) al permitir que cargue su certificado.</span><span class="sxs-lookup"><span data-stu-id="18768-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a><span data-ttu-id="18768-127">Conexión de su aplicación al centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="18768-127">Connecting your app to the notification hub</span></span>
1. <span data-ttu-id="18768-128">En Visual Studio, cree una aplicación nueva de Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="18768-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="18768-129">En Visual Studio 2013 Update 2 o versiones posteriores, cree en su lugar una aplicación Silverlight de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="18768-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio, nuevo proyecto, aplicación vacía, Windows Phone Silverlight][11]
2. <span data-ttu-id="18768-131">En Visual Studio, haga clic con el botón derecho en la solución y, luego, haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="18768-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="18768-132">De este modo aparece el cuadro de diálogo **Administrar paquetes de NuGet** .</span><span class="sxs-lookup"><span data-stu-id="18768-132">This displays the **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="18768-133">Busque `WindowsAzure.Messaging.Managed` , haga clic en **Instalar**y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="18768-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span></span>
   
    ![Visual Studio, Administrador de paquetes NuGet][20]
   
    <span data-ttu-id="18768-135">A continuación, se descarga, instala y agrega una referencia a la biblioteca de Mensajería de Azure para Windows mediante el <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">paquete de NuGet WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="18768-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="18768-136">Abra el archivo App.xaml.cs y agregue las siguientes instrucciones `using` :</span><span class="sxs-lookup"><span data-stu-id="18768-136">Open the file App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="18768-137">Agregue el siguiente código en la parte superior del método **Application_Launching** en App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="18768-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span></span>
   
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
   > <span data-ttu-id="18768-138">El valor **MyPushChannel** es un índice que se utiliza para buscar un canal existente en la colección [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="18768-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="18768-139">Si no hay uno ya allí, cree una nueva entrada con ese nombre.</span><span class="sxs-lookup"><span data-stu-id="18768-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="18768-140">Asegúrese de insertar el nombre del centro y la cadena de conexión llamada **DefaultListenSharedAccessSignature** que obtuvo en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="18768-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span></span>
    <span data-ttu-id="18768-141">Este código recupera el URI del canal de la aplicación desde MPNS y, luego, lo registra con su centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="18768-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="18768-142">Garantiza también que el URI del canal se registre en su centro de notificaciones cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18768-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="18768-143">Este tutorial envía una notificación del sistema al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="18768-143">This tutorial sends a toast notification to the device.</span></span> <span data-ttu-id="18768-144">Cuando envía una notificación de icono, debe llamar al método **BindToShellTile** en el canal.</span><span class="sxs-lookup"><span data-stu-id="18768-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span></span> <span data-ttu-id="18768-145">Para admitir notificaciones del sistema y notificaciones de icono, llame a ambos métodos, **BindToShellTile** y  **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="18768-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="18768-146">En el Explorador de soluciones, expanda **Propiedades**, abra el archivo `WMAppManifest.xml`, haga clic en la pestaña **Funcionalidades** y asegúrese de que la funcionalidad **ID_CAP_PUSH_NOTIFICATION** esté marcada.</span><span class="sxs-lookup"><span data-stu-id="18768-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. <span data-ttu-id="18768-147">Presione la tecla `F5` para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18768-147">Press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="18768-148">Se muestra un mensaje de registro en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18768-148">A registration message is displayed in the app.</span></span>
8. <span data-ttu-id="18768-149">Cierre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18768-149">Close the app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="18768-150">Para recibir una notificación push, la aplicación no se debe estar ejecutando en primer plano.</span><span class="sxs-lookup"><span data-stu-id="18768-150">To receive a toast push notification, the application must not be running in the foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="18768-151">Envío de notificaciones push desde su backend</span><span class="sxs-lookup"><span data-stu-id="18768-151">Send push notifications from your backend</span></span>
<span data-ttu-id="18768-152">Puede enviar notificaciones push mediante Centros de notificaciones desde cualquier back-end a través de la <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaz de REST</a>.</span><span class="sxs-lookup"><span data-stu-id="18768-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="18768-153">En este tutorial, enviará notificaciones push con una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="18768-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="18768-154">Para ver un ejemplo de cómo enviar notificaciones push desde un back-end de WebAPI de ASP.NET integrado en Notification Hubs, consulte [Azure Notification Hubs notifican a los usuarios con back-end de .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="18768-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="18768-155">Para ver un ejemplo de cómo enviar notificaciones push con las [API de REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), consulte [Uso de Notification Hubs desde Java](notification-hubs-java-push-notification-tutorial.md) y [Uso de los Notification Hubs desde PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="18768-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="18768-156">Haga clic con el botón derecho en la solución, seleccione **Agregar** y **Nuevo proyecto...** y, a continuación, en **Visual C#**, haga clic en **Windows**, **Aplicación de consola** y **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="18768-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="18768-157">Esta acción agrega una aplicación de consola nueva de Visual C# a la solución.</span><span class="sxs-lookup"><span data-stu-id="18768-157">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="18768-158">También puede hacer esto en una solución separada.</span><span class="sxs-lookup"><span data-stu-id="18768-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="18768-159">Haga clic en **Herramientas**, **Administrador de paquetes de biblioteca** y **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="18768-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="18768-160">Esto muestra la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="18768-160">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="18768-161">En la ventana de la **Consola del Administrador de paquetes**, seleccione en **Proyecto predeterminado** el nuevo proyecto de aplicación de consola y, a continuación, ejecute el siguiente comando en la ventana de la consola:</span><span class="sxs-lookup"><span data-stu-id="18768-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="18768-162">Así se agrega una referencia al SDK de Centros de notificaciones de Azure mediante el <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="18768-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="18768-163">Abra el archivo `Program.cs` y agregue la siguiente instrucción `using`:</span><span class="sxs-lookup"><span data-stu-id="18768-163">Open the `Program.cs` file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="18768-164">En la clase `Program`, agregue el método siguiente:</span><span class="sxs-lookup"><span data-stu-id="18768-164">In the `Program` class, add the following method:</span></span>
   
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
   
    <span data-ttu-id="18768-165">Asegúrese de reemplazar el marcador de posición `<hub name>` por el nombre del centro de notificaciones que aparece en el portal.</span><span class="sxs-lookup"><span data-stu-id="18768-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span></span> <span data-ttu-id="18768-166">Reemplace también el marcador de posición de la cadena de conexión por la cadena de conexión llamada **DefaultFullSharedAccessSignature** que obtuvo en la sección "Configuración del Centro de notificaciones".</span><span class="sxs-lookup"><span data-stu-id="18768-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="18768-167">Asegúrese de usar la cadena de conexión con acceso **Total**, no con acceso **Escuchar**.</span><span class="sxs-lookup"><span data-stu-id="18768-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="18768-168">La cadena de acceso de escucha no tiene permisos para enviar notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="18768-168">The listen-access string does not have permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="18768-169">Agregue la siguiente línea al método `Main` :</span><span class="sxs-lookup"><span data-stu-id="18768-169">Add the following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="18768-170">Con el emulador de Windows Phone en ejecución y su aplicación cerrada, establezca el proyecto de aplicación de consola como el proyecto de inicio predeterminado y, luego, presione la tecla `F5` para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18768-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="18768-171">Recibirá una notificación push del sistema.</span><span class="sxs-lookup"><span data-stu-id="18768-171">You will receive a toast push notification.</span></span> <span data-ttu-id="18768-172">Al pulsar en el mensaje emergente, se carga la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18768-172">Tapping the toast banner loads the app.</span></span>

<span data-ttu-id="18768-173">Puede encontrar todas las cargas posibles en los temas de [catálogo de notificaciones del sistema] y [catálogo de iconos] de MSDN.</span><span class="sxs-lookup"><span data-stu-id="18768-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18768-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18768-174">Next steps</span></span>
<span data-ttu-id="18768-175">En este sencillo ejemplo, ha difundido notificaciones push a todos los dispositivos Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="18768-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="18768-176">Para dirigirse a usuarios específicos, consulte el tutorial [Uso de los Centros de notificaciones para insertar notificaciones para los usuarios] .</span><span class="sxs-lookup"><span data-stu-id="18768-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span></span> 

<span data-ttu-id="18768-177">Si desea segmentar a sus usuarios por grupos de interés, puede leer [Uso de Centros de notificaciones para enviar noticias de último minuto].</span><span class="sxs-lookup"><span data-stu-id="18768-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="18768-178">Obtenga más información sobre el uso de Centros de notificaciones en la [orientación sobre los Centros de notificaciones](en inglés).</span><span class="sxs-lookup"><span data-stu-id="18768-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="18768-179">[Visual Studio 2012 Express para Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span><span class="sxs-lookup"><span data-stu-id="18768-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span></span>
<span data-ttu-id="18768-180">[orientación sobre los Centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="18768-180">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
<span data-ttu-id="18768-181">[Uso de los Centros de notificaciones para insertar notificaciones para los usuarios]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="18768-181">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="18768-182">[Uso de Centros de notificaciones para enviar noticias de último minuto]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span><span class="sxs-lookup"><span data-stu-id="18768-182">[Use Notification Hubs to send breaking news]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span></span>
<span data-ttu-id="18768-183">[catálogo de notificaciones del sistema]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="18768-183">[toast catalog]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span></span>
<span data-ttu-id="18768-184">[catálogo de iconos]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="18768-184">[tile catalog]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span></span>
<span data-ttu-id="18768-185">[tutorial Centros de notificaciones: Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span><span class="sxs-lookup"><span data-stu-id="18768-185">[Notification Hubs - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span></span>

